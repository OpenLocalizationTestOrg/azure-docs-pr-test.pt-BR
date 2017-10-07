---
title: "tooAzure de migração de banco de dados do aaaSQL servidor banco de dados SQL | Microsoft Docs"
description: "Saiba como sobre SQL Server banco de dados migração tooAzure banco de dados SQL na nuvem hello. Use a migração do banco de dados migração ferramentas tootest compatibilidade toodatabase anterior."
keywords: "migração de banco de dados, migração de banco de dados do sql server, ferramentas de migração de banco de dados, migrar banco de dados, migrar banco de dados sql"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 9cf09000-87fc-4589-8543-a89175151bc2
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sqldb-migrate
ms.date: 02/08/2017
ms.author: carlrab
ms.openlocfilehash: 3a5e879404dd2da1dd5254a6134e3ee1517648db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-database-migration-toosql-database-in-hello-cloud"></a>TooSQL de migração de banco de dados do SQL Server na nuvem de saudação do banco de dados
Neste artigo, você aprenderá sobre Olá dois métodos principais para a migração de um SQL Server 2005 ou posterior tooAzure de banco de dados SQL de banco de dados. Olá primeiro método é mais simples, mas requer algum, possivelmente significativo, tempo de inatividade durante a migração de saudação. método segundo Hello é mais complexo, mas elimina substancialmente o tempo de inatividade durante a migração de saudação.

Em ambos os casos, você precisa tooensure esse banco de dados de origem de saudação é compatível com o banco de dados do SQL Azure usando Olá [Assistente de migração de dados (DMA)](https://www.microsoft.com/download/details.aspx?id=53595). V12 do banco de dados SQL está se aproximando [paridade de recursos](sql-database-features.md) com o SQL Server, diferente de operações relacionadas problemas tooserver e de bancos de dados. Bancos de dados e aplicativos que dependem de [parcialmente com ou sem suporte funções](sql-database-transact-sql-information.md) precisa [reformulação toofix dessas incompatibilidades](sql-database-cloud-migrate.md#resolving-database-migration-compatibility-issues) saudação do SQL Server antes do banco de dados pode ser migrado.

> [!NOTE]
> toomigrate um banco de dados do SQL Server, incluindo o Microsoft Access, Sybase, MySQL Oracle e DB2 tooAzure banco de dados SQL, consulte [SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2016/12/22/released-sql-server-migration-assistant-ssma-v7-2/).
> 

## <a name="method-1-migration-with-downtime-during-hello-migration"></a>Método 1: A migração com tempo de inatividade durante a migração de saudação

 Use esse método se você puder ter algum tempo de inatividade ou se estiver executando um teste de migração de um banco de dados de produção para migração posterior. Para ver um tutorial, consulte [Migrar um Banco de Dados do SQL Server](sql-database-migrate-your-sql-server-database.md).

Olá lista a seguir contém Olá o fluxo de trabalho geral para uma migração de banco de dados do SQL Server usando esse método.

  ![Diagrama de migração do VSSSDT](./media/sql-database-cloud-migrate/azure-sql-migration-sql-db.png)

1. Avaliar o banco de dados de saudação para compatibilidade usando a versão mais recente de saudação do [Assistente de migração de dados (DMA)](https://www.microsoft.com/download/details.aspx?id=53595).
2. Prepare as correções necessárias como scripts Transact-SQL.
3. Faça uma cópia transacionalmente consistente do banco de dados de origem de saudação que está sendo migrado - e verifique se nenhuma alteração que está sendo feitas toohello banco de dados de origem (ou você pode aplicar tais alterações manualmente após a conclusão da migração de saudação). Há muitos tooquiesce de métodos um banco de dados, a desabilitação de toocreating de conectividade de cliente um [instantâneo de banco de dados](https://msdn.microsoft.com/library/ms175876.aspx).
4. Implante a cópia de banco de dados do hello Transact-SQL scripts tooapply Olá correções toohello.
5. [Exportar](sql-database-export.md) Olá tooa de cópia de banco de dados. Arquivo BACPAC em uma unidade local.
6. [Importação](sql-database-import.md) hello. O arquivo BACPAC como um novo banco de dados SQL do Azure usando qualquer um dos vários BACPAC importe ferramentas, com o SQLPackage.exe sendo Olá recomendado ferramenta para melhor desempenho.

### <a name="optimizing-data-transfer-performance-during-migration"></a>Otimizando o desempenho de transferência de dados durante a migração 

Olá lista a seguir contém recomendações para melhorar o desempenho durante o processo de importação hello.

* Escolha seu orçamento permite o desempenho da transferência toomaximize Olá de camada de hello mais alto nível de serviço e o desempenho. Você pode reduzir após a migração de saudação toosave money. 
* Minimizar Olá distância entre o. BACPAC de arquivo e Olá data center de destino.
* Desabilitar estatísticas automaticamente durante a migração
* Índices e tabelas de partição
* Descartar exibições indexadas e recriá-las após a conclusão
* Remover banco de dados consultados raramente dados históricos tooanother e migrar esse dados históricos tooa SQL Azure banco de dados separado. Em seguida, você pode consultar esses dados históricos usando [consultas elásticas](sql-database-elastic-query-overview.md).

### <a name="optimize-performance-after-hello-migration-completes"></a>Otimizar o desempenho após a conclusão da migração Olá

[Atualizar estatísticas](https://msdn.microsoft.com/library/ms187348.aspx) com uma verificação completa após a migração de saudação.

## <a name="method-2-use-transactional-replication"></a>Método 2: usar replicação transacional

Quando você não puder que tooremove seu banco de dados do SQL Server da produção enquanto Olá migração está ocorrendo, você pode usar a replicação transacional do SQL Server como sua solução de migração. toouse esse método, o banco de dados de origem Olá deve atender Olá [requisitos para replicação transacional](https://msdn.microsoft.com/library/mt589530.aspx) e ser compatível para o banco de dados do SQL Azure. Para obter informações sobre a replicação do SQL com o AlwaysOn, consulte [Configurar a replicação para Grupos de Disponibilidade AlwaysOn (SQL Server)](/sql/database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server).

toouse nesta solução, você configura seu banco de dados do SQL Azure como uma instância de SQL Server do assinante toohello que você deseja toomigrate. distribuidor de replicação transacional Hello sincroniza dados de toobe de banco de dados de saudação sincronizado (publicador Olá) enquanto novas transações continuam a ocorrer. 

Com a replicação transacional, todas as alterações tooyour dados ou esquema aparecem em seu banco de dados do SQL Azure. Depois que Olá sincronização estiver concluída e você está pronto toomigrate, alterar a cadeia de caracteres de conexão de saudação de seu toopoint aplicativos-los tooyour banco de dados do SQL Azure. Depois que a replicação transacional descarrega as alterações restantes no seu banco de dados de origem e todos os seus aplicativos ponto tooAzure banco de dados, você pode desinstalar a replicação transacional. O Banco de Dados SQL do Azure agora é o sistema de produção.

 ![Diagrama do SeedCloudTR](./media/sql-database-cloud-migrate/SeedCloudTR.png)

> [!TIP]
> Você também pode usar a replicação transacional toomigrate um subconjunto de seu banco de dados de origem. publicação Olá replicar tooAzure banco de dados SQL pode ser o subconjunto de tooa limitado de tabelas Olá no banco de dados de hello está sendo replicado. Para cada tabela que está sendo replicada, você pode limitar o subconjunto de tooa Olá dados de linhas de saudação e/ou um subconjunto de colunas de saudação.
>

### <a name="migration-toosql-database-using-transaction-replication-workflow"></a>TooSQL de migração usando o fluxo de trabalho de replicação de transação do banco de dados

> [!IMPORTANT]
> Use Olá última versão do SQL Server Management Studio tooremain sincronizado com atualizações tooMicrosoft Azure e banco de dados SQL. Versões anteriores do SQL Server Management Studio não podem configurar o Banco de Dados SQL como um assinante. [Atualizar o SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 

1. Configurar a distribuição
   -  [Usando o SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms151192.aspx#Anchor_1)
   -  [Usando o Transact-SQL](https://msdn.microsoft.com/library/ms151192.aspx#Anchor_2)
2. Criar a publicação
   -  [Usando o SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms151160.aspx#Anchor_1)
   -  [Usando o Transact-SQL](https://msdn.microsoft.com/library/ms151160.aspx#Anchor_2)
3. Criar a assinatura
   -  [Usando o SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms152566.aspx#Anchor_0)
   -  [Usando o Transact-SQL](https://msdn.microsoft.com/library/ms152566.aspx#Anchor_1)

### <a name="some-tips-and-differences-for-migrating-toosql-database"></a>Algumas dicas e diferenças de migração tooSQL banco de dados

1. Usar um distribuidor local 
   - Isso causa um impacto de desempenho no servidor de saudação. 
   - Se Olá impacto no desempenho é inaceitável, você pode usar outro servidor, mas ele adiciona complexidade no gerenciamento e administração.
2. Ao selecionar uma pasta de instantâneo, a pasta de Olá se tornar que selecionar é grande o suficiente toohold um BCP de cada tabela, você deseja tooreplicate. 
3. Bloqueios de criação do instantâneo Olá tabelas associadas até sua conclusão, portanto agendar o snapshot adequadamente. 
4. Há suporte apenas para assinaturas push no Banco de Dados SQL do Azure. Você só pode adicionar assinantes saudação do banco de dados.

## <a name="resolving-database-migration-compatibility-issues"></a>Resolvendo problemas de compatibilidade de migração do banco de dados
Há uma grande variedade de problemas de compatibilidade que você pode encontrar, dependendo na versão de saudação do SQL Server em complexidade de hello e de banco de dados de origem de saudação do banco de dados de saudação que você está migrando. Versões anteriores do SQL Server têm mais problemas de compatibilidade. Use Olá recursos a seguir, além de tooa direcionados pesquisa na Internet usando o mecanismo de pesquisa de opções:

* [Recursos de banco de dados do SQL Server sem suporte no Banco de Dados SQL do Azure](sql-database-transact-sql-information.md)
* [Discontinued Database Engine Functionality in SQL Server 2016](https://msdn.microsoft.com/library/ms144262%28v=sql.130%29)
* [Discontinued Database Engine Functionality in SQL Server 2014](https://msdn.microsoft.com/library/ms144262%28v=sql.120%29)
* [Discontinued Database Engine Functionality in SQL Server 2012](https://msdn.microsoft.com/library/ms144262%28v=sql.110%29)
* [Discontinued Database Engine Functionality in SQL Server 2008 R2](https://msdn.microsoft.com/library/ms144262%28v=sql.105%29)
* [Discontinued Database Engine Functionality in SQL Server 2005](https://msdn.microsoft.com/library/ms144262%28v=sql.90%29)

Além disso, toosearching Olá Internet e usar esses recursos, use Olá [fóruns da comunidade do MSDN SQL Server](https://social.msdn.microsoft.com/Forums/sqlserver/home?category=sqlserver) ou [StackOverflow](http://stackoverflow.com/).

## <a name="next-steps"></a>Próximas etapas
* Use o script hello no blog do Azure SQL EMEA engenheiros Olá muito[monitorar o uso de tempdb durante a migração](https://blogs.msdn.microsoft.com/azuresqlemea/2016/12/28/lesson-learned-10-monitoring-tempdb-usage/).
* Use o script hello no blog do Azure SQL EMEA engenheiros Olá muito[monitorar o espaço de log de transações de saudação do banco de dados enquanto a migração está ocorrendo](https://blogs.msdn.microsoft.com/azuresqlemea/2016/10/31/lesson-learned-7-monitoring-the-transaction-log-space-of-my-database/0).
* Para um SQL Server Customer Advisory Team blog sobre como migrar usando arquivos BACPAC, consulte [Migrando do SQL Server tooAzure banco de dados SQL usando arquivos BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* Para obter informações sobre como trabalhar com a hora UTC após a migração, consulte [modificando saudação padrão fuso horário para o fuso horário local](https://blogs.msdn.microsoft.com/azuresqlemea/2016/07/27/lesson-learned-4-modifying-the-default-time-zone-for-your-local-time-zone/).
* Para obter informações sobre como alterar o idioma padrão de saudação do banco de dados após a migração, consulte [como toochange Olá idioma padrão do banco de dados do SQL Azure](https://blogs.msdn.microsoft.com/azuresqlemea/2017/01/13/lesson-learned-16-how-to-change-the-default-language-of-azure-sql-database/).


