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
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a><span data-ttu-id="30ebe-103">Monitorar e gerenciar um pool elástico com o Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="30ebe-103">Monitor and manage an elastic pool with Transact-SQL</span></span>
<span data-ttu-id="30ebe-104">Este tópico mostra como toomanage escalonável [pools Elásticos](sql-database-elastic-pool.md) com Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="30ebe-104">This topic shows you how toomanage scalable [elastic pools](sql-database-elastic-pool.md) with Transact-SQL.</span></span>  <span data-ttu-id="30ebe-105">Você também pode criar e gerenciar uma saudação do Azure pool Elástico [portal do Azure](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), Olá API REST, ou [c#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="30ebe-105">You can also create and manage an Azure elastic pool hello [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="30ebe-106">Você também pode criar e mover bancos de dados de e para os pools elásticos usando [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="30ebe-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>


<span data-ttu-id="30ebe-107">Saudação de uso [Create Database (banco de dados do SQL Azure)](https://msdn.microsoft.com/library/dn268335.aspx) e [Database(Azure SQL Database) Alter](https://msdn.microsoft.com/library/mt574871.aspx) comandos toocreate e mover bancos de dados dentro e fora de pools elásticos.</span><span class="sxs-lookup"><span data-stu-id="30ebe-107">Use hello [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) and [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commands toocreate and move databases into and out of elastic pools.</span></span> <span data-ttu-id="30ebe-108">pool Elástico Olá deve existir antes que você pode usar esses comandos.</span><span class="sxs-lookup"><span data-stu-id="30ebe-108">hello elastic pool must exist before you can use these commands.</span></span> <span data-ttu-id="30ebe-109">Esses comandos afetam somente bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="30ebe-109">These commands affect only databases.</span></span> <span data-ttu-id="30ebe-110">Criação de novos pools e configuração de saudação de propriedades de pool (como eDTUs min e max) não podem ser alterados com comandos T-SQL.</span><span class="sxs-lookup"><span data-stu-id="30ebe-110">Creation of new pools and hello setting of pool properties (such as min and max eDTUs) cannot be changed with T-SQL commands.</span></span>

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="30ebe-111">Criar um banco de dados em pool em um pool elástico</span><span class="sxs-lookup"><span data-stu-id="30ebe-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="30ebe-112">Use o comando de criar o banco de dados de saudação com hello opção SERVICE_OBJECTIVE.</span><span class="sxs-lookup"><span data-stu-id="30ebe-112">Use hello CREATE DATABASE command with hello SERVICE_OBJECTIVE option.</span></span>   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

<span data-ttu-id="30ebe-113">Todos os bancos de dados em um pool Elástico herdam da camada de serviço de saudação do pool Elástico de saudação (Basic, Standard e Premium).</span><span class="sxs-lookup"><span data-stu-id="30ebe-113">All databases in an elastic pool inherit hello service tier of hello elastic pool (Basic, Standard, Premium).</span></span> 

## <a name="move-a-database-between-elastic-pools"></a><span data-ttu-id="30ebe-114">Mover um banco de dados entre pools elásticos</span><span class="sxs-lookup"><span data-stu-id="30ebe-114">Move a database between elastic pools</span></span>
<span data-ttu-id="30ebe-115">Use o comando ALTER DATABASE de saudação com hello modificar e configurar serviço de\_opção objetiva como ELÁSTICA\_POOL.</span><span class="sxs-lookup"><span data-stu-id="30ebe-115">Use hello ALTER DATABASE command with hello MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC\_POOL.</span></span> <span data-ttu-id="30ebe-116">Olá nome toohello nome do pool de destino de saudação do conjunto.</span><span class="sxs-lookup"><span data-stu-id="30ebe-116">Set hello name toohello name of hello target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move hello database named db1 tooan elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="30ebe-117">Mover um banco de dados para um pool elástico</span><span class="sxs-lookup"><span data-stu-id="30ebe-117">Move a database into an elastic pool</span></span>
<span data-ttu-id="30ebe-118">Use o comando ALTER DATABASE de saudação com hello modificar e configurar serviço\_opção objetiva como ELASTIC_POOL.</span><span class="sxs-lookup"><span data-stu-id="30ebe-118">Use hello ALTER DATABASE command with hello MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC_POOL.</span></span> <span data-ttu-id="30ebe-119">Olá nome toohello nome do pool de destino de saudação do conjunto.</span><span class="sxs-lookup"><span data-stu-id="30ebe-119">Set hello name toohello name of hello target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move hello database named db1 tooan elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="30ebe-120">Remover um banco de dados de um pool elástico</span><span class="sxs-lookup"><span data-stu-id="30ebe-120">Move a database out of an elastic pool</span></span>
<span data-ttu-id="30ebe-121">Use o comando ALTER DATABASE de saudação e defina Olá SERVICE_OBJECTIVE tooone Olá níveis de desempenho (como S0 ou S1).</span><span class="sxs-lookup"><span data-stu-id="30ebe-121">Use hello ALTER DATABASE command and set hello SERVICE_OBJECTIVE tooone of hello performance levels (such as S0 or S1).</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes hello database into a stand-alone database with hello service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="30ebe-122">Listar bancos de dados em um pool elástico</span><span class="sxs-lookup"><span data-stu-id="30ebe-122">List databases in an elastic pool</span></span>
<span data-ttu-id="30ebe-123">Saudação de uso [sys\_service \_exibição objetivos](https://msdn.microsoft.com/library/mt712619) toolist Olá a todos os bancos de dados em um pool Elástico.</span><span class="sxs-lookup"><span data-stu-id="30ebe-123">Use hello [sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619) toolist all hello databases in an elastic pool.</span></span> <span data-ttu-id="30ebe-124">Faça logon no mestre toohello exibição do banco de dados tooquery hello.</span><span class="sxs-lookup"><span data-stu-id="30ebe-124">Log in toohello master database tooquery hello view.</span></span>

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="30ebe-125">Obter dados de uso de recursos para um pool elástico</span><span class="sxs-lookup"><span data-stu-id="30ebe-125">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="30ebe-126">Saudação de uso [sys.elastic\_pool \_recurso \_estatísticas de exibição](https://msdn.microsoft.com/library/mt280062.aspx) tooexamine estatísticas de uso de recurso Olá de um pool Elástico em um servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="30ebe-126">Use hello [sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx) tooexamine hello resource usage statistics of an elastic pool on a logical server.</span></span> <span data-ttu-id="30ebe-127">Faça logon no mestre toohello exibição do banco de dados tooquery hello.</span><span class="sxs-lookup"><span data-stu-id="30ebe-127">Log in toohello master database tooquery hello view.</span></span>

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a><span data-ttu-id="30ebe-128">Obter o uso de recursos para um banco de dados em pool</span><span class="sxs-lookup"><span data-stu-id="30ebe-128">Get resource usage for a pooled database</span></span>
<span data-ttu-id="30ebe-129">Saudação de uso [sys.dm\_ db\_ recurso\_exibição de estatísticas](https://msdn.microsoft.com/library/dn800981.aspx) ou [sys.resource \_exibição de estatísticas](https://msdn.microsoft.com/library/dn269979.aspx) tooexamine estatísticas de uso de recurso saudação de um banco de dados em um pool Elástico.</span><span class="sxs-lookup"><span data-stu-id="30ebe-129">Use hello [sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) or [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx) tooexamine hello resource usage statistics of a database in an elastic pool.</span></span> <span data-ttu-id="30ebe-130">Esse processo é o uso de recursos de tooquerying semelhante para um único banco de dados.</span><span class="sxs-lookup"><span data-stu-id="30ebe-130">This process is similar tooquerying resource usage for a single database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30ebe-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="30ebe-131">Next steps</span></span>
<span data-ttu-id="30ebe-132">Depois de criar um pool Elástico, você pode gerenciar bancos de dados Elásticos no pool de saudação Criando trabalhos elásticos.</span><span class="sxs-lookup"><span data-stu-id="30ebe-132">After creating an elastic pool, you can manage elastic databases in hello pool by creating elastic jobs.</span></span> <span data-ttu-id="30ebe-133">Trabalhos Elásticos facilitam a execução de scripts T-SQL em relação a qualquer número de bancos de dados no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="30ebe-133">Elastic jobs facilitate running T-SQL scripts against any number of databases in hello pool.</span></span> <span data-ttu-id="30ebe-134">Para saber mais, confira [Visão geral sobre os trabalhos elásticos de banco de dados](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="30ebe-134">For more information, see [Elastic database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

<span data-ttu-id="30ebe-135">Consulte [expansão com o Azure SQL Database](sql-database-elastic-scale-introduction.md): usar o banco de dados Elástico ferramentas tooscale out, mover dados, consultar ou criar transações.</span><span class="sxs-lookup"><span data-stu-id="30ebe-135">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic database tools tooscale out, move data, query, or create transactions.</span></span>

