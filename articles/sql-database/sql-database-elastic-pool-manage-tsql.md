---
title: "T-SQL: gerenciar um pool elástico do Banco de dados SQL | Microsoft Docs"
description: "Use o T-SQL para gerenciar um pool elástico do Banco de dados SQL do Azure."
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
ms.openlocfilehash: c6b64e4a7fd91283a37a792b294965064d653003
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a><span data-ttu-id="04ef9-103">Monitorar e gerenciar um pool elástico com o Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="04ef9-103">Monitor and manage an elastic pool with Transact-SQL</span></span>
<span data-ttu-id="04ef9-104">Este tópico mostra como gerenciar [pools elásticos](sql-database-elastic-pool.md) escalonáveis com Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="04ef9-104">This topic shows you how to manage scalable [elastic pools](sql-database-elastic-pool.md) with Transact-SQL.</span></span>  <span data-ttu-id="04ef9-105">Você também pode criar e gerenciar um pool elástico do Azure com o [Portal do Azure](https://portal.azure.com/), o [PowerShell](sql-database-elastic-pool-manage-powershell.md), a API REST ou [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="04ef9-105">You can also create and manage an Azure elastic pool the [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="04ef9-106">Você também pode criar e mover bancos de dados de e para os pools elásticos usando [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="04ef9-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>


<span data-ttu-id="04ef9-107">Use os comandos [Create Database (Banco de dados Azure SQL)](https://msdn.microsoft.com/library/dn268335.aspx) e [Alter Database(Banco de dados Azure SQL)](https://msdn.microsoft.com/library/mt574871.aspx) para criar e mover bancos de dados dentro e fora de pools elásticos.</span><span class="sxs-lookup"><span data-stu-id="04ef9-107">Use the [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) and [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commands to create and move databases into and out of elastic pools.</span></span> <span data-ttu-id="04ef9-108">O pool elástico deve existir antes que você possa usar esses comandos.</span><span class="sxs-lookup"><span data-stu-id="04ef9-108">The elastic pool must exist before you can use these commands.</span></span> <span data-ttu-id="04ef9-109">Esses comandos afetam somente bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="04ef9-109">These commands affect only databases.</span></span> <span data-ttu-id="04ef9-110">A criação de novos pools e a configuração de propriedades de pool (como eDTUs mínimos e máximos) não podem ser alteradas com comandos T-SQL.</span><span class="sxs-lookup"><span data-stu-id="04ef9-110">Creation of new pools and the setting of pool properties (such as min and max eDTUs) cannot be changed with T-SQL commands.</span></span>

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="04ef9-111">Criar um banco de dados em pool em um pool elástico</span><span class="sxs-lookup"><span data-stu-id="04ef9-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="04ef9-112">Use o comando CREATE DATABASE com a opção SERVICE_OBJECTIVE.</span><span class="sxs-lookup"><span data-stu-id="04ef9-112">Use the CREATE DATABASE command with the SERVICE_OBJECTIVE option.</span></span>   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

<span data-ttu-id="04ef9-113">Todos os bancos de dados em um pool elástico herdam a camada de serviço do pool elástico (Basic, Standard e Premium).</span><span class="sxs-lookup"><span data-stu-id="04ef9-113">All databases in an elastic pool inherit the service tier of the elastic pool (Basic, Standard, Premium).</span></span> 

## <a name="move-a-database-between-elastic-pools"></a><span data-ttu-id="04ef9-114">Mover um banco de dados entre pools elásticos</span><span class="sxs-lookup"><span data-stu-id="04ef9-114">Move a database between elastic pools</span></span>
<span data-ttu-id="04ef9-115">Use o comando ALTER DATABASE com a modificar e defina o serviço\_opção objetiva como ELÁSTICO\_POOL.</span><span class="sxs-lookup"><span data-stu-id="04ef9-115">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC\_POOL.</span></span> <span data-ttu-id="04ef9-116">Defina o nome como o nome do pool de destino.</span><span class="sxs-lookup"><span data-stu-id="04ef9-116">Set the name to the name of the target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move the database named db1 to an elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="04ef9-117">Mover um banco de dados para um pool elástico</span><span class="sxs-lookup"><span data-stu-id="04ef9-117">Move a database into an elastic pool</span></span>
<span data-ttu-id="04ef9-118">Use o comando ALTER DATABASE com a modificar e defina o serviço\_opção objetiva como ELASTIC_POOL.</span><span class="sxs-lookup"><span data-stu-id="04ef9-118">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC_POOL.</span></span> <span data-ttu-id="04ef9-119">Defina o nome como o nome do pool de destino.</span><span class="sxs-lookup"><span data-stu-id="04ef9-119">Set the name to the name of the target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move the database named db1 to an elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="04ef9-120">Remover um banco de dados de um pool elástico</span><span class="sxs-lookup"><span data-stu-id="04ef9-120">Move a database out of an elastic pool</span></span>
<span data-ttu-id="04ef9-121">Use o comando ALTER DATABASE e defina o SERVICE_OBJECTIVE como um dos níveis de desempenho (como S0 ou S1).</span><span class="sxs-lookup"><span data-stu-id="04ef9-121">Use the ALTER DATABASE command and set the SERVICE_OBJECTIVE to one of the performance levels (such as S0 or S1).</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes the database into a stand-alone database with the service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="04ef9-122">Listar bancos de dados em um pool elástico</span><span class="sxs-lookup"><span data-stu-id="04ef9-122">List databases in an elastic pool</span></span>
<span data-ttu-id="04ef9-123">Use [sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619) para listar todos os bancos de dados em um pool elástico.</span><span class="sxs-lookup"><span data-stu-id="04ef9-123">Use the [sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619) to list all the databases in an elastic pool.</span></span> <span data-ttu-id="04ef9-124">Entre no banco de dados mestre para consultar o modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="04ef9-124">Log in to the master database to query the view.</span></span>

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="04ef9-125">Obter dados de uso de recursos para um pool elástico</span><span class="sxs-lookup"><span data-stu-id="04ef9-125">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="04ef9-126">Use [sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx) para examinar as estatísticas de uso de recursos de um pool elástico em um servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="04ef9-126">Use the [sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx) to examine the resource usage statistics of an elastic pool on a logical server.</span></span> <span data-ttu-id="04ef9-127">Entre no banco de dados mestre para consultar o modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="04ef9-127">Log in to the master database to query the view.</span></span>

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a><span data-ttu-id="04ef9-128">Obter o uso de recursos para um banco de dados em pool</span><span class="sxs-lookup"><span data-stu-id="04ef9-128">Get resource usage for a pooled database</span></span>
<span data-ttu-id="04ef9-129">Use [sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) ou [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx) para examinar as estatísticas de uso de recursos do banco de dados em um pool elástico.</span><span class="sxs-lookup"><span data-stu-id="04ef9-129">Use the [sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) or [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx) to examine the resource usage statistics of a database in an elastic pool.</span></span> <span data-ttu-id="04ef9-130">Esse processo é semelhante à consulta do uso de recursos de um banco de dados individual.</span><span class="sxs-lookup"><span data-stu-id="04ef9-130">This process is similar to querying resource usage for a single database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04ef9-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="04ef9-131">Next steps</span></span>
<span data-ttu-id="04ef9-132">Depois de criar um pool elástico, você pode gerenciar os bancos de dados elásticos no pool criando trabalhos elásticos.</span><span class="sxs-lookup"><span data-stu-id="04ef9-132">After creating an elastic pool, you can manage elastic databases in the pool by creating elastic jobs.</span></span> <span data-ttu-id="04ef9-133">Trabalhos elásticos facilitam a execução de scripts T-SQL em qualquer quantidade de bancos de dados no pool.</span><span class="sxs-lookup"><span data-stu-id="04ef9-133">Elastic jobs facilitate running T-SQL scripts against any number of databases in the pool.</span></span> <span data-ttu-id="04ef9-134">Para saber mais, confira [Visão geral sobre os trabalhos elásticos de banco de dados](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04ef9-134">For more information, see [Elastic database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

<span data-ttu-id="04ef9-135">Confira [Escala horizontal com o Banco de Dados SQL do Azure](sql-database-elastic-scale-introduction.md): use ferramentas de banco de dados elástico para escalar horizontalmente, mover os dados, consultar ou criar transações.</span><span class="sxs-lookup"><span data-stu-id="04ef9-135">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic database tools to scale out, move data, query, or create transactions.</span></span>

