---
title: "aaaManage dados históricos em tabelas temporais com a política de retenção | Microsoft Docs"
description: "Saiba como toouse retenção temporal política tookeep dados históricos sob seu controle."
services: sql-database
documentationcenter: 
author: bonova
manager: drasumic
editor: 
ms.assetid: 76cfa06a-e758-453e-942c-9f1ed6a38c2a
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 10/12/2016
ms.author: bonova
ms.openlocfilehash: a72a6111a6cd7322d734d08bf3852e95f5ffea8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a>Gerenciar dados históricos em Tabelas Temporais com a política de retenção
Tabelas Temporais podem aumentar o tamanho do banco de dados mais do que tabelas regulares, especialmente se você mantiver os dados históricos por um período maior de tempo. Portanto, a política de retenção para dados históricos é um aspecto importante do planejamento e gerenciamento do ciclo de vida de saudação de cada tabela temporal. Tabelas temporais no Banco de Dados SQL do Azure vem com um mecanismo de retenção de fácil utilização que ajuda você a realizar essa tarefa.

Retenção de histórico temporal pode ser configurada no nível de tabela individual hello, que permite aos usuários as diretivas de vencimento flexível toocreate. A aplicação de retenção temporal é simple: requer apenas um toobe parâmetro definido durante a alteração de esquema ou criação de tabela.

Após você definir a política de retenção, o Banco de Dados SQL do Azure começa a verificar regularmente se há linhas de histórico qualificadas para limpeza automática de dados. Identificação de linhas correspondentes e sua remoção da tabela de histórico de saudação ocorrem de modo transparente, na tarefa de plano de fundo Olá que é programada e executada pelo sistema hello. Condição de idade para linhas de tabela de histórico de saudação é verificada com base na coluna de saudação que representa o final do período SYSTEM_TIME. Se o período de retenção, por exemplo, é definir toosix em meses, linhas de tabela qualificadas para limpeza satisfazem Olá condição a seguir:

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

Em Olá anterior de exemplo, presumimos que **ValidTo** coluna corresponde toohello final do período SYSTEM_TIME.

## <a name="how-tooconfigure-retention-policy"></a>Como política de retenção tooconfigure?
Antes de configurar a política de retenção para uma tabela temporal, verifique primeiro se a retenção de histórico temporal está habilitada *no nível de banco de dados de saudação*.

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

Sinalizador de banco de dados **is_temporal_history_retention_enabled** é tooON conjunto por padrão, mas os usuários podem alterá-la com a instrução ALTER DATABASE. É também automaticamente conjunto tooOFF após [restauração pontual](sql-database-recovery-using-backups.md) operação. Limpeza de retenção de histórico temporal tooenable para seu banco de dados, execute Olá instrução a seguir:

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> Será possível configurar a retenção para tabelas temporais mesmo se **is_temporal_history_retention_enabled** estiver DESATIVADO, mas a limpeza automática de linhas antigas não será disparada nesse caso.
> 
> 

Política de retenção é configurada durante a criação de uma tabela especificando o valor do parâmetro HISTORY_RETENTION_PERIOD hello:

````
CREATE TABLE dbo.WebsiteUserInfo
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH
 (
     SYSTEM_VERSIONING = ON
     (
        HISTORY_TABLE = dbo.WebsiteUserInfoHistory,
        HISTORY_RETENTION_PERIOD = 6 MONTHS
     )
 );
````

Banco de dados SQL do Azure permite o período de retenção toospecify usando unidades de tempo diferentes: dias, semanas, meses e anos. Se HISTORY_RETENTION_PERIOD for omitido, supõe-se que retenção é INFINITO. Você também pode usar palavra-chave INFINITO explicitamente.

Em alguns cenários, talvez você queira tooconfigure retenção após a criação de tabela ou toochange valor configurado anteriormente. Nesse caso, use a instrução ALTER TABLE:

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> Definir SYSTEM_VERSIONING tooOFF *não preserva* valor do período de retenção. Definir SYSTEM_VERSIONING tooON sem HISTORY_RETENTION_PERIOD explicitamente especificada resulta no período de retenção infinito hello.
> 
> 

tooreview o estado atual da política de retenção hello, esse sinalizador de habilitação de retenção temporal junções em nível de banco de dados de saudação com períodos de retenção para tabelas individuais consulta a seguir de saudação de uso:

````
SELECT DB.is_temporal_history_retention_enabled,
SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,
T1.name as TemporalTableName,  SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,
T2.name as HistoryTableName,T1.history_retention_period,
T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases
where name = DB_NAME()) AS DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2
````


## <a name="how-sql-database-deletes-aged-rows"></a>Como o Banco de Dados SQL exclui linhas antigas?
o processo de limpeza Olá depende do layout de índice Olá Olá da tabela de histórico. É importante toonotice que *somente tabelas de histórico com um índice clusterizado (árvore B ou columnstore) podem ter uma política de retenção finito configurada*. Uma tarefa em segundo plano é criada tooperform a limpeza de dados antigos de todas as tabelas temporais com período de retenção finito.
Lógica de limpeza para o índice clusterizado do hello rowstore (árvore B) exclui a linha antigo em partes menores (até too10K) minimizando a pressão no log do banco de dados e o subsistema de e/s. Embora utiliza a lógica de limpeza necessárias índice de árvore B, a ordem de exclusões para linhas de saudação mais antigas que o período de retenção não pode ser garantido firmemente. Portanto, *não terão qualquer dependência em ordem de limpeza de saudação em seus aplicativos*.

Olá a tarefa de limpeza para Olá clusterizada columnstore remove todo [grupos de linhas](https://msdn.microsoft.com/library/gg492088.aspx) uma vez (normalmente contém 1 milhão de linhas cada), que é muito eficiente, especialmente quando os dados históricos são gerados em uma alta velocidade.

![Retenção de columnstore clusterizado](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

A excelente compactação de dados e a eficiente limpeza retenção tornam o índice columnstore clusterizado uma opção perfeita para cenários em que sua carga de trabalho gera rapidamente uma grande quantidade de dados históricos. Esse padrão é típico para o [cargas de trabalho de processamento transacional intensas que usam tabelas temporais](https://msdn.microsoft.com/library/mt631669.aspx) para controle de alterações e auditoria, análise de tendências ou ingestão de dados de IoT.

## <a name="index-considerations"></a>Considerações de índice
a tarefa de limpeza Olá para tabelas com índice clusterizado rowstore requer toostart de índice com o hello coluna correspondente Olá final do período SYSTEM_TIME. Se esse índice não existir, você não poderá configurar o período de retenção finito:

*Msg 13765, nível 16, estado 1 <br> </br> definir período de retenção finito falhou na tabela temporal com versão do sistema 'temporalstagetestdb.dbo.WebsiteUserInfo' como tabela de histórico de saudação ' temporalstagetestdb.dbo.WebsiteUserInfoHistory' não contém o índice clusterizado necessário. Considere a criação de uma columnstore clusterizada ou o índice de árvore B começando com a coluna de saudação que corresponde a fim de SYSTEM_TIME period na tabela de histórico de saudação.*

É importante toonotice que Olá tabela de histórico padrão criada pelo banco de dados SQL já tem um índice, que é compatível com a política de retenção clusterizado. Se você tentar tooremove índice em uma tabela com o período de retenção finito, a operação falhará com hello erro a seguir:

*Msg 13766, nível 16, estado 1 <br> </br> não é possível descartar o índice clusterizado de saudação 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' porque ele está sendo usado para a limpeza automática de dados antigos. Considere a configuração HISTORY_RETENTION_PERIOD tooINFINITE correspondente tabela temporal com versão do sistema Olá se você precisar toodrop esse índice.*

Limpeza em um índice columnstore clusterizado Olá funcione de maneira ideal se históricos linhas são inseridas no hello ordem crescente (ordenado pela extremidade de saudação da coluna do período), que é sempre Olá caso de tabela de histórico de saudação é populada exclusivamente pelo Olá sistema _ Mecanismo VERSIONIOING. Se as linhas na tabela de histórico de saudação não são ordenadas pelo final da coluna do período (que pode ser o caso de Olá se você migrou os dados de histórico existentes), você deve recriar o índice columnstore clusterizado na parte superior do índice de rowstore de árvore B corretamente é ordenado, tooachieve ideal desempenho.

Evite a recriação de índice columnstore clusterizado na tabela de histórico de saudação com período de retenção finito hello, porque ele pode alterar a ordem em grupos de linhas de saudação naturalmente impostos pela operação de controle de versão de sistema hello. Se você precisar de um índice columnstore clusterizado na tabela de histórico de saudação toorebuild, fazer isso, recriando sobre compatível com índice de árvore B, preservando a ordenação Olá RowGroups necessário para a limpeza de dados regulares. Olá a mesma abordagem deve ser tomada se você criar a tabela temporal com tabela de histórico existente que tem um índice de coluna sem ordem de dados garantida clusterizado:

````
/*Create B-tree ordered by hello end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

Quando o período de retenção finito está configurado para a tabela de histórico de Olá com um índice columnstore clusterizado hello, você não pode criar índices adicionais de árvore B não clusterizado na tabela:

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

Um tooexecute tentativa acima instrução falha com hello erro a seguir:

*Msg 13772, Nível 16, Estado 1 <br></br> Não é possível criar índice não clusterizado em uma tabela de histórico temporal “WebsiteUserInfoHistory”, pois ele tem o período de retenção finito e o índice columnstore clusterizado definido.*

## <a name="querying-tables-with-retention-policy"></a>Consultando tabelas com a política de retenção
Todas as consultas de tabela temporal Olá filtram automaticamente históricas linhas que correspondem a política de retenção finito, tooavoid resultados imprevisíveis e inconsistentes, pois antigas linhas excluídas pela tarefa de limpeza Olá, *em qualquer ponto no tempo e no ordem arbitrária*.

Olá, imagem a seguir mostra Olá plano de consulta para uma consulta simples:

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

consulta Olá plano inclui o filtro aplicado tooend da coluna do período (ValidTo) no operador Clustered Index Scan de saudação na tabela de histórico de saudação (realçada). Este exemplo supõe que o período de retenção de um MÊS foi definido na tabela WebsiteUserInfo.

![Filtro de consulta de retenção](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

No entanto, se você consultar diretamente a tabela de histórico, verá linhas que são mais antigas do que o período de retenção especificado, mas sem qualquer garantia de resultados da consulta repetíveis. Olá imagem a seguir mostra plano de execução de consulta para consulta Olá na tabela de histórico de saudação sem filtros adicionais aplicados:

![Consultando histórico sem filtro de retenção](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

A lógica de negócios não deve contar com a leitura da tabela de histórico além do período de retenção, pois resultados inconsistentes ou inesperados podem ser obtidos. É recomendável usar consultas temporais com a cláusula FOR SYSTEM_TIME para análise de dados em tabelas temporais.

## <a name="point-in-time-restore-considerations"></a>Considerações da recuperação pontual
Quando você cria o novo banco de dados por [restauração existente ponto específico tooa de banco de dados no tempo](sql-database-recovery-using-backups.md), ele tem retenção temporal desabilitada no nível de banco de dados de saudação. (**is_temporal_history_retention_enabled** sinalizador definido tooOFF). Essa funcionalidade permite que você tooexamine todas as linhas após a restauração, sem se preocupar com históricos que antigos linhas são removidas antes de obter tooquery-los. Você pode usá-lo muito*inspecionar dados históricos além do período de retenção configurado*.

Digamos que uma tabela temporal tem o período de retenção de um MÊS especificado. Se seu banco de dados foi criado na camada de serviço Premium, seria toocreate capaz de cópia de banco de dados com o estado do banco de dados Olá backup too35 dias no hello anterior. Que efetivamente permitiria tooanalyze linhas históricos que estão up too65 dias consultando a tabela de histórico de saudação diretamente.

Se desejar que a limpeza de retenção temporal tooactivate, execute Olá após a instrução Transact-SQL após a restauração pontual:

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a>Próximas etapas
como as tabelas temporais em seus aplicativos, toouse check-out de toolearn [Introdução às tabelas temporais no banco de dados do SQL Azure](sql-database-temporal-tables.md).

Visite Channel 9 toohear um [real implementação temporal história de sucesso](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) e inspecionar uma [live temporal demonstração](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).

Para obter informações detalhadas sobre as Tabelas Temporais, leia a [documentação do MSDN](https://msdn.microsoft.com/library/dn935015.aspx).

