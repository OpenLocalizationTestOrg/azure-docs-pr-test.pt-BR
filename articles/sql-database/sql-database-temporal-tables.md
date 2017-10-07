---
title: aaaGetting iniciado com tabelas temporais no banco de dados do SQL Azure | Microsoft Docs
description: Saiba como tooget iniciada com o uso de tabelas temporais no banco de dados do SQL Azure.
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: c8c0f232-0751-4a7f-a36e-67a0b29fa1b8
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 01/10/2017
ms.author: bonova
ms.openlocfilehash: 54f394b51df07aa2f9bb299f207e692171d23479
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a>Introdução às Tabelas Temporais no Banco de Dados SQL do Azure
Tabelas Temporais são um novo recurso de programabilidade do banco de dados do SQL Azure que permite que você tootrack e analisar o histórico completo de saudação de alterações em seus dados, sem necessidade de saudação de codificação personalizada. Tabelas temporais manter dados tootime relacionadas contexto para que os fatos armazenados podem ser interpretados como válido somente dentro de um período específico hello. Essa propriedade das Tabelas Temporais permite uma análise eficiente baseada em tempo e a obtenção de informações da evolução dos dados.

## <a name="temporal-scenario"></a>Cenário Temporal
Este artigo ilustra Olá etapas tooutilize tabelas temporais em um cenário de aplicativo. Suponha que você queira tootrack atividade de usuário em um novo site que está sendo desenvolvido a partir do zero ou em um site existente que você deseja tooextend com a análise da atividade de usuário. Neste exemplo simplificado, vamos supor que o número de saudação de páginas da web visitadas durante um período de tempo é um indicador que precisa toobe capturada e monitorado no banco de dados de site de saudação que é hospedado no banco de dados do SQL Azure. meta de saudação de análise histórica de saudação da atividade do usuário é tooget entradas tooredesign site e fornecer a melhor experiência para os visitantes hello.

modelo de banco de dados de saudação para este cenário é muito simple - métrica de atividade de usuário é representado por um campo único inteiro, **PageVisited**e é capturada juntamente com informações básicas sobre o perfil de usuário de saudação. Além disso, para análise de tempo com base, você mantém uma série de linhas para cada usuário, onde cada linha representa número de saudação de páginas de um determinado usuário visitou em um período de tempo específico.

![Esquema](./media/sql-database-temporal-tables/AzureTemporal1.png)

Felizmente, você não precisa tooput qualquer esforço no seu aplicativo toomaintain essas informações de atividade. Com tabelas temporais, este processo será automatizado - lhe oferece total flexibilidade durante o design do site e toofocus de tempo mais na análise de dados de saudação em si. Olá somente ter toodo é tooensure que **WebSiteInfo** tabela está configurada como [temporal com versão do sistema](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0). Olá as etapas exatas tooutilize tabelas temporais neste cenário são descritos abaixo.

## <a name="step-1-configure-tables-as-temporal"></a>Etapa 1: configurar tabelas como temporais
Dependendo se você estiver iniciando um novo desenvolvimento ou atualizando um aplicativo existente, você criará tabelas temporais ou modificará as existentes ao adicionar atributos temporais. Em geral, seu cenário pode ser uma combinação dessas duas opções. Execute estas ações usando o [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), o [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) ou qualquer outra ferramenta de desenvolvimento do Transact-SQL.

> [!IMPORTANT]
> É recomendável que você sempre use Olá versão mais recente do Management Studio tooremain sincronizado com atualizações tooMicrosoft Azure e banco de dados SQL. [Atualizar o SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

### <a name="create-new-table"></a>Criar nova tabela
Use o item de menu de contexto "Nova tabela com versão do sistema" no editor de consultas do Pesquisador de objetos do SSMS tooopen Olá com um script de modelo de tabela temporal e, em seguida, usar o modelo de saudação de toopopulate de "Especificar valores para parâmetros de modelo" (Ctrl + Shift + M):

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

No SSDT, escolher o modelo de "Tabela Temporal (versão do sistema)" ao adicionar novo projeto de banco de dados de toohello de itens. Que serão o designer de tabela aberta e habilitar tooeasily você especificar Olá layout de tabela:

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

Você também pode uma tabela temporal criar especificando instruções Olá Transact-SQL diretamente, conforme mostrado no exemplo hello abaixo. Observe que Olá elementos obrigatórios de cada tabela temporal são a definição de período hello e cláusula SYSTEM_VERSIONING de saudação com uma tabela de usuário de tooanother de referência que irão armazenar versões de linha de histórico:

````
CREATE TABLE WebsiteUserInfo 
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED 
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL 
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
````

Quando você cria a tabela temporal com versão do sistema, Olá que acompanha a tabela de histórico com a configuração padrão de saudação é criado automaticamente. tabela de histórico padrão Olá contém um índice de árvore B clusterizado nas colunas de período hello (início, fim) com a compactação de página habilitada. Essa configuração é ideal para a maioria de saudação de cenários em que as tabelas Temporais são usadas, especialmente para [dados de auditoria](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0). 

Nesse caso específico, nosso objetivo é análise de tendência com base em tempo de tooperform um histórico de dados maior e com conjuntos de dados maiores, para a opção de armazenamento de Olá Olá tabela de histórico é um índice columnstore clusterizado. Um columnstore clusterizado oferece compactação e desempenho ótimos para consultas analíticas. Temporal oferecem tabelas Olá índices de tooconfigure flexibilidade em Olá tabelas atuais e temporal completamente independentemente. 

> [!NOTE]
> Índices ColumnStore só estão disponíveis na camada de serviço premium Olá.
>

saudação de script a seguir mostra como o índice padrão na tabela de histórico pode ser alterados toohello clusterizada columnstore:

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

Tabelas Temporais são representadas em Olá Pesquisador de objetos com ícone de saudação específico para facilitar sua identificação, enquanto sua tabela de histórico é exibida como um nó filho.

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-tootemporal"></a>Alterar tootemporal de tabela existente
Vamos abordar o cenário de saudação alternativo no qual Olá WebsiteUserInfo tabela já existe, mas não foi projetado tookeep um histórico das alterações. Nesse caso, você pode estender simplesmente Olá existente tabela toobecome temporal, conforme mostrado no exemplo a seguir de saudação:

````
ALTER TABLE WebsiteUserInfo 
ADD 
    ValidFrom datetime2 (0) GENERATED ALWAYS AS ROW START HIDDEN  
        constraint DF_ValidFrom DEFAULT DATEADD(SECOND, -1, SYSUTCDATETIME())
    , ValidTo datetime2 (0)  GENERATED ALWAYS AS ROW END HIDDEN   
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'
    , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo); 

ALTER TABLE WebsiteUserInfo  
SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
GO

CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

## <a name="step-2-run-your-workload-regularly"></a>Etapa 2: executar sua carga de trabalho regularmente
a principal vantagem Olá das tabelas temporais é que você não precisa toochange ou ajustar seu site em qualquer controle de alterações tooperform de maneira. Depois de criadas, as Tabelas Temporais fazem as versões de linha persistirem de forma transparente sempre que você executa modificações em seus dados. 

No controle de alterações automáticas ordem tooleverage para essa situação específica, vamos apenas atualizar coluna **PagesVisited** toda vez que quando o usuário termina Component sessão no site de saudação:

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

É importante toonotice que Olá consulta update não precisa de hora exata do tooknow hello quando a operação real Olá ocorreu nem como dados históricos serão preservados para análise futura. Ambos os aspectos são tratados automaticamente pelo hello Azure SQL Database. Olá diagrama a seguir ilustra como dados de histórico são gerados em cada atualização.

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a>Etapa 3: executar a análise de dados históricos
Agora, quando o versionamento pelo sistema temporal estiver habilitado, a análise dos dados históricos estará a apenas uma consulta de distância de você. Neste artigo, podemos fornecer alguns exemplos que abordam os cenários comuns de análise - toolearn todos os detalhes, explorar várias opções introduzidas com hello [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) cláusula.

toosee Olá top 10 usuários ordenados pelo número de saudação de páginas da web visitadas a partir de uma hora atrás, execute esta consulta:

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

Você pode modificar essa consulta tooanalyze Olá visitas ao site a partir de um dia atrás, há um mês ou em qualquer ponto Olá anterior se desejar.

análise estatística básica de tooperform para Olá dia anterior, use Olá exemplo a seguir:

````
DECLARE @twoDaysAgo datetime2 = DATEADD(DAY, -2, SYSUTCDATETIME());
DECLARE @aDayAgo datetime2 = DATEADD(DAY, -1, SYSUTCDATETIME());

SELECT UserID, SUM (PagesVisited) as TotalVisitedPages, AVG (PagesVisited) as AverageVisitedPages,
MAX (PagesVisited) AS MaxVisitedPages, MIN (PagesVisited) AS MinVisitedPages,
STDEV (PagesVisited) as StDevViistedPages
FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME BETWEEN @twoDaysAgo AND @aDayAgo
GROUP BY UserId
````

toosearch atividades de um usuário específico, em um período de tempo, use Olá CONTAINED IN cláusula:

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

A visualização gráfica é especialmente conveniente para consultas temporais porque você pode mostrar com muita facilidade tendências e padrões de uso de uma maneira intuitiva:

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a>Aprimoramento do esquema de tabela
Normalmente, você precisará esquema de tabela temporal Olá toochange enquanto você estiver fazendo o desenvolvimento de aplicativos. Para fazer isso, basta executar instruções ALTER TABLE regulares e banco de dados do SQL Azure propagará adequadamente tabela de histórico de toohello de alterações. Olá script a seguir mostra como você pode adicionar atributos adicionais para o controle:

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

Da mesma forma, você pode alterar a definição de coluna enquanto sua carga de trabalho está ativa:

````
/*Increase hello length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

Por fim, você pode remover uma coluna que já não precisa.

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

Como alternativa, use a versão mais recente [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange temporal esquema de tabela enquanto você estiver conectado toohello banco de dados (modo online) ou como parte do projeto de banco de dados da saudação (modo offline).

## <a name="controlling-retention-of-historical-data"></a>Controle de retenção de dados históricos
Com tabelas temporais com versão do sistema, tabela de histórico de saudação pode aumentar o tamanho do banco de dados hello mais do que tabelas regulares. Uma tabela de histórico grande e crescente pode se tornar um problema ambas toopure os custos de armazenamento, bem como por impor um desempenho imposto sobre consultas Temporais. Portanto, o desenvolvimento de uma política de retenção de dados para o gerenciamento de dados na tabela de histórico de saudação é um aspecto importante do planejamento e gerenciamento do ciclo de vida de saudação de cada tabela temporal. Banco de dados SQL Azure, você tem Olá abordagens para gerenciar dados históricos na tabela temporal Olá a seguir:

* [Particionamento de tabela](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [Script de Limpeza Personalizado](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a>Próximas etapas
Para obter informações detalhadas sobre as Tabelas Temporais, confira a [documentação do MSDN](https://msdn.microsoft.com/library/dn935015.aspx).
Visite Channel 9 toohear um [real implementação temporal história de sucesso](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) e inspecionar uma [live temporal demonstração](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).

