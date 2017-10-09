---
title: "replicação geográfica aaaConfigure para o banco de dados SQL Azure com o Transact-SQL | Microsoft Docs"
description: "Configurar a replicação geográfica para o banco de dados SQL do Azure usando o Transact-SQL"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d94d89a6-3234-46c5-8279-5eb8daad10ac
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: carlrab
ms.openlocfilehash: 295b6b12f257dfb15131d5ee28fbe65c6476352d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-with-transact-sql"></a>Configurar a replicação geográfica ativa para o Banco de Dados SQL do Azure com o Transact-SQL

Este artigo mostra como tooconfigure replicação geográfica ativa para um banco de dados do SQL Azure com o Transact-SQL.

failover tooinitiate usando Transact-SQL, consulte [iniciar um failover planejado ou não planejado para o banco de dados SQL Azure com o Transact-SQL](sql-database-geo-replication-failover-transact-sql.md).

> [!NOTE]
> Quando você usa replicação geográfica ativa (secundários legíveis) para a recuperação de desastres, você deve configurar um grupo de failover para todos os bancos de dados dentro de um failover de aplicativo tooenable automático e transparente. Esse recurso está em visualização. Para saber mais, confira [Grupos de failover automático e replicação geográfica](sql-database-geo-replication-overview.md).
> 
> 

tooconfigure replicação geográfica usando Transact-SQL, você precisa seguir hello:

* Uma assinatura do Azure
* Um servidor de banco de dados do Azure SQL lógico <MyLocalServer> e um banco de dados SQL <MyDB> -banco de dados primário Olá que você deseja tooreplicate
* Um ou mais banco de dados do Azure SQL servidores lógicos < MySecondaryServer(n) > - Olá servidores lógicos que devem ser servidores de saudação do parceiro no qual você criará os bancos de dados secundários
* Um logon que seja DBManager em Olá primário
* Ter db_ownership do banco de dados local Olá que você irá replicar geograficamente
* Ser DBManager em toowhich de servidores de parceiro Olá você irá configurar a replicação geográfica
* versão mais recente de saudação do SQL Server Management Studio (SSMS)

> [!IMPORTANT]
> É recomendável que você sempre use Olá versão mais recente do Management Studio tooremain sincronizado com atualizações tooMicrosoft Azure e banco de dados SQL. [Atualizar o SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

## <a name="add-secondary-database"></a>Adicionar banco de dados secundário
Você pode usar o hello **ALTER DATABASE** instrução toocreate replicado geograficamente banco de dados secundário em um servidor de parceiro. Execute essa instrução no banco de dados mestre da saudação servidor contendo Olá banco de dados toobe replicada hello. Olá banco de dados replicada geograficamente (hello "banco de dados primário") terá Olá mesmo nome como o banco de dados de saudação sendo replicado e será, por padrão, têm Olá mesmo nível de serviço como o banco de dados primário hello. Olá banco de dados secundário pode ser legível ou ilegível e pode ser um único banco de dados ou em um pool Elástico. Para saber mais, confira [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) e [Camadas de Serviço](sql-database-service-tiers.md).
Depois que o banco de dados secundário Olá é criado e propagado, dados começará a replicar assincronamente do banco de dados primário hello. Olá etapas a seguir descrevem como replicação geográfica tooconfigure usando o Management Studio. Etapas toocreate não legível e legíveis secundários, como um único banco de dados ou em um pool Elástico, são fornecidos.

> [!NOTE]
> Se um banco de dados existe no servidor de parceiro especificado de saudação com hello mesmo nome como o comando de saudação do banco de dados primário Olá falhará.
> 

### <a name="add-readable-secondary-single-database"></a>Adicionar um secundário legível (banco de dados individual)
Use Olá etapas toocreate um secundário legível como um único banco de dados a seguir.

1. No Management Studio, conecte o servidor lógico do banco de dados do Azure SQL tooyour.
2. Abra a pasta de bancos de dados hello, expanda Olá **bancos de dados do sistema** com o botão direito na pasta **mestre**e, em seguida, clique em **nova consulta**.
3. Use os seguintes Olá **ALTER DATABASE** instrução toomake um banco de dados local em um principal de replicação geográfica com um banco de dados secundário legível em um servidor secundário.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer2> WITH (ALLOW_CONNECTIONS = ALL);
4. Clique em **Execute** toorun consulta de saudação.

### <a name="add-readable-secondary-elastic-pool"></a>Adicionar um secundário legível (pool elástico)
Use Olá seguindo as etapas toocreate um secundário legível em um pool Elástico.

1. No Management Studio, conecte o servidor lógico do banco de dados do Azure SQL tooyour.
2. Abra a pasta de bancos de dados hello, expanda Olá **bancos de dados do sistema** com o botão direito na pasta **mestre**e, em seguida, clique em **nova consulta**.
3. Use os seguintes Olá **ALTER DATABASE** instrução toomake um banco de dados local em um principal de replicação geográfica com um banco de dados secundário legível em um servidor secundário em um pool Elástico.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer4> WITH (ALLOW_CONNECTIONS = ALL
           , SERVICE_OBJECTIVE = ELASTIC_POOL (name = MyElasticPool2));
4. Clique em **Execute** toorun consulta de saudação.

## <a name="remove-secondary-database"></a>Remover banco de dados secundário
Você pode usar o hello **ALTER DATABASE** toopermanently de instrução encerrar a parceria de replicação Olá entre um banco de dados secundário e seu principal. Essa instrução é executada no banco de dados mestre Olá no qual Olá banco de dados primário reside. Após o encerramento da relação de hello, banco de dados secundário Olá torna-se um banco de dados de leitura / gravação normal. Se o banco de dados do hello conectividade toosecondary for interrompido Olá comando terá êxito mas Olá secundário se tornará leitura-gravação após restaurar a conectividade. Para saber mais, confira [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) e [Camadas de Serviço](sql-database-service-tiers.md).

Tooremove replicado geograficamente secundário as etapas a seguir de saudação do uso de uma parceria de replicação geográfica.

1. No Management Studio, conecte o servidor lógico do banco de dados do Azure SQL tooyour.
2. Abra a pasta de bancos de dados hello, expanda Olá **bancos de dados do sistema** com o botão direito na pasta **mestre**e, em seguida, clique em **nova consulta**.
3. Use os seguintes Olá **ALTER DATABASE** secundário de tooremove um replicado geograficamente de instrução.
   
        ALTER DATABASE <MyDB>
           REMOVE SECONDARY ON SERVER <MySecondaryServer1>;
4. Clique em **Execute** toorun consulta de saudação.

## <a name="monitor-active-geo-replication-configuration-and-health"></a>Monitorar a configuração e a integridade da replicação geográfica ativa

Tarefas de monitoramento incluem monitoramento de configuração de replicação geográfica hello e monitorando a integridade da replicação de dados.  Você pode usar o hello **sys.dm_geo_replication_links** exibição de gerenciamento dinâmico no hello banco de dados mestre tooreturn obter informações sobre todos os links de replicação existente para cada banco de dados no servidor lógico do hello Azure SQL Database. Essa exibição contém uma linha para cada link de replicação Olá entre bancos de dados primários e secundários. Você pode usar o hello **sys.dm_replication_link_status** exibição de gerenciamento dinâmico tooreturn uma linha para cada banco de dados de SQL do Azure atualmente envolvido em um link de replicação de replicação. Isso inclui os bancos de dados primários e secundários. Se houver mais de um link de replicação contínua para um determinado banco de dados primário, essa tabela contém uma linha para cada uma das relações de saudação. Olá exibição é criada em todos os bancos de dados, incluindo mestre lógico hello. No entanto, a consulta dessa exibição no mestre lógico Olá retorna um conjunto vazio. Você pode usar o hello **sys.DM operation_status** tooshow status de saudação de exibição de gerenciamento dinâmico para todas as operações, incluindo status Olá Olá dos links de replicação de banco de dados. Para saber mais, confira [sys.geo_replication_links (Banco de Dados SQL do Azure)](https://msdn.microsoft.com/library/mt575501.aspx), [sys.dm_geo_replication_link_status (Banco de Dados SQL do Azure)](https://msdn.microsoft.com/library/mt575504.aspx) e [sys.dm_operation_status (Banco de Dados SQL do Azure)](https://msdn.microsoft.com/library/dn270022.aspx).

Use Olá parceria de toomonitor uma replicação geográfica ativa as etapas a seguir.

1. No Management Studio, conecte o servidor lógico do banco de dados do Azure SQL tooyour.
2. Abra a pasta de bancos de dados hello, expanda Olá **bancos de dados do sistema** com o botão direito na pasta **mestre**e, em seguida, clique em **nova consulta**.
3. Olá tooshow instrução a seguir ao use todos os bancos de dados com links de replicação geográfica.
   
        SELECT database_id, start_date, modify_date, partner_server, partner_database, replication_state_desc, role, secondary_allow_connections_desc FROM sys.geo_replication_links;
4. Clique em **Execute** toorun consulta de saudação.
5. Abra a pasta de bancos de dados hello, expanda Olá **bancos de dados do sistema** com o botão direito na pasta **MyDB**e, em seguida, clique em **nova consulta**.
6. Olá Use replicação de saudação tooshow instrução a seguir está atrasada e último tempo de replicação dos meus bancos de dados secundários de MyDB.
   
        SELECT link_guid, partner_server, last_replication, replication_lag_sec FROM sys.dm_geo_replication_link_status
7. Clique em **Execute** toorun consulta de saudação.
8. Saudação de uso instrução tooshow hello mais recentes operações de replicação geográfica associadas com o banco de dados MyDB a seguir.
   
        SELECT * FROM sys.dm_operation_status where major_resource_id = 'MyDB'
        ORDER BY start_time DESC
9. Clique em **Execute** toorun consulta de saudação.

## <a name="next-steps"></a>Próximas etapas
* toolearn mais sobre grupos de failover e replicação geográfica, consulte - [grupos de Failover](sql-database-geo-replication-overview.md)
* Para obter uma visão geral e os cenários de continuidade dos negócios, confira [Visão geral da continuidade dos negócios](sql-database-business-continuity.md)

