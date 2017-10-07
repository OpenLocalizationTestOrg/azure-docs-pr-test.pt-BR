---
title: "T-SQL: gerenciar um pool elástico do Banco de dados SQL | Microsoft Docs"
description: "Use T-SQL toomanage um pool Elástico de banco de dados SQL."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 4e288e17-bc3e-4255-9fbe-0a2ac0dbd7dd
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 05/27/2016
ms.author: srinia
ms.openlocfilehash: 666f131b2c88849a1a9ea83381bbc27548e93599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a>Monitorar e gerenciar um pool elástico com o Transact-SQL
Este tópico mostra como toomanage escalonável [pools Elásticos](sql-database-elastic-pool.md) com Transact-SQL.  Você também pode criar e gerenciar uma saudação do Azure pool Elástico [portal do Azure](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), Olá API REST, ou [c#](sql-database-elastic-pool-manage-csharp.md). Você também pode criar e mover bancos de dados de e para os pools elásticos usando [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).


Saudação de uso [Create Database (banco de dados do SQL Azure)](https://msdn.microsoft.com/library/dn268335.aspx) e [Database(Azure SQL Database) Alter](https://msdn.microsoft.com/library/mt574871.aspx) comandos toocreate e mover bancos de dados dentro e fora de pools elásticos. pool Elástico Olá deve existir antes que você pode usar esses comandos. Esses comandos afetam somente bancos de dados. Criação de novos pools e configuração de saudação de propriedades de pool (como eDTUs min e max) não podem ser alterados com comandos T-SQL.

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>Criar um banco de dados em pool em um pool elástico
Use o comando de criar o banco de dados de saudação com hello opção SERVICE_OBJECTIVE.   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

Todos os bancos de dados em um pool Elástico herdam da camada de serviço de saudação do pool Elástico de saudação (Basic, Standard e Premium). 

## <a name="move-a-database-between-elastic-pools"></a>Mover um banco de dados entre pools elásticos
Use o comando ALTER DATABASE de saudação com hello modificar e configurar serviço de\_opção objetiva como ELÁSTICA\_POOL. Olá nome toohello nome do pool de destino de saudação do conjunto.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move hello database named db1 tooan elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a>Mover um banco de dados para um pool elástico
Use o comando ALTER DATABASE de saudação com hello modificar e configurar serviço\_opção objetiva como ELASTIC_POOL. Olá nome toohello nome do pool de destino de saudação do conjunto.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move hello database named db1 tooan elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a>Remover um banco de dados de um pool elástico
Use o comando ALTER DATABASE de saudação e defina Olá SERVICE_OBJECTIVE tooone Olá níveis de desempenho (como S0 ou S1).

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes hello database into a stand-alone database with hello service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a>Listar bancos de dados em um pool elástico
Saudação de uso [sys\_service \_exibição objetivos](https://msdn.microsoft.com/library/mt712619) toolist Olá a todos os bancos de dados em um pool Elástico. Faça logon no mestre toohello exibição do banco de dados tooquery hello.

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>Obter dados de uso de recursos para um pool elástico
Saudação de uso [sys.elastic\_pool \_recurso \_estatísticas de exibição](https://msdn.microsoft.com/library/mt280062.aspx) tooexamine estatísticas de uso de recurso Olá de um pool Elástico em um servidor lógico. Faça logon no mestre toohello exibição do banco de dados tooquery hello.

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a>Obter o uso de recursos para um banco de dados em pool
Saudação de uso [sys.dm\_ db\_ recurso\_exibição de estatísticas](https://msdn.microsoft.com/library/dn800981.aspx) ou [sys.resource \_exibição de estatísticas](https://msdn.microsoft.com/library/dn269979.aspx) tooexamine estatísticas de uso de recurso saudação de um banco de dados em um pool Elástico. Esse processo é o uso de recursos de tooquerying semelhante para um único banco de dados.

## <a name="next-steps"></a>Próximas etapas
Depois de criar um pool Elástico, você pode gerenciar bancos de dados Elásticos no pool de saudação Criando trabalhos elásticos. Trabalhos Elásticos facilitam a execução de scripts T-SQL em relação a qualquer número de bancos de dados no pool de saudação. Para saber mais, confira [Visão geral sobre os trabalhos elásticos de banco de dados](sql-database-elastic-jobs-overview.md). 

Consulte [expansão com o Azure SQL Database](sql-database-elastic-scale-introduction.md): usar o banco de dados Elástico ferramentas tooscale out, mover dados, consultar ou criar transações.

