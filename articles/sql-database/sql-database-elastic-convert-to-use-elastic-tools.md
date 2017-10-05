---
title: Migrar bancos de dados existentes para escala horizontal | Microsoft Docs
description: "Converter bancos de dados fragmentados para usar ferramentas de banco de dados elástico criando um gerenciador de mapa de fragmentos"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 8c851d8e-8fd5-4327-89c1-9178b20ddd69
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 099f40d00753b7c86ba726a818f17d440a125221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-existing-databases-to-scale-out"></a><span data-ttu-id="ad137-103">Migrar bancos de dados existentes para escala horizontal</span><span class="sxs-lookup"><span data-stu-id="ad137-103">Migrate existing databases to scale-out</span></span>
<span data-ttu-id="ad137-104">Gerencie com facilidade seus bancos de dados fragmentados e escalonados horizontalmente existentes, usando as ferramentas de banco de dados do Banco de Dados SQL (como a [biblioteca de cliente do Banco de Dados Elástico](sql-database-elastic-database-client-library.md)).</span><span class="sxs-lookup"><span data-stu-id="ad137-104">Easily manage your existing scaled-out sharded databases using Azure SQL Database database tools (such as the [Elastic Database client library](sql-database-elastic-database-client-library.md)).</span></span> <span data-ttu-id="ad137-105">Você deve primeiro converter um conjunto existente de bancos de dados para usar o [gerenciador de mapa de fragmentos](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="ad137-105">You must first convert an existing set of databases to use the [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="ad137-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ad137-106">Overview</span></span>
<span data-ttu-id="ad137-107">Para migrar um banco de dados fragmentado existente:</span><span class="sxs-lookup"><span data-stu-id="ad137-107">To migrate an existing sharded database:</span></span> 

1. <span data-ttu-id="ad137-108">Prepare o [banco de dados do gerenciador de mapa de fragmentos](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="ad137-108">Prepare the [shard map manager database](sql-database-elastic-scale-shard-map-management.md).</span></span>
2. <span data-ttu-id="ad137-109">Criar o mapa de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="ad137-109">Create the shard map.</span></span>
3. <span data-ttu-id="ad137-110">Preparar os fragmentos individuais.</span><span class="sxs-lookup"><span data-stu-id="ad137-110">Prepare the individual shards.</span></span>  
4. <span data-ttu-id="ad137-111">Adicione os mapeamentos ao mapa de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="ad137-111">Add mappings to the shard map.</span></span>

<span data-ttu-id="ad137-112">Essas técnicas podem ser implementadas usando a [biblioteca de cliente do .NET Framework](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) ou os scripts do PowerShell encontrados em [Azure SQL DB – Scripts de ferramentas de Banco de Dados Elástico](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="ad137-112">These techniques can be implemented using either the [.NET Framework client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), or the PowerShell scripts found at [Azure SQL DB - Elastic Database tools scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span> <span data-ttu-id="ad137-113">Os exemplos aqui usam os scripts do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ad137-113">The examples here use the PowerShell scripts.</span></span>

<span data-ttu-id="ad137-114">Para saber mais sobre o ShardMapManager, confira [Gerenciamento de mapa de fragmentos](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="ad137-114">For more information about the ShardMapManager, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="ad137-115">Para obter uma visão geral das ferramentas de banco de dados elástico, confira [Visão geral dos recursos do Banco de Dados Elástico](sql-database-elastic-scale-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ad137-115">For an overview of the elastic database tools, see [Elastic Database features overview](sql-database-elastic-scale-introduction.md).</span></span>

## <a name="prepare-the-shard-map-manager-database"></a><span data-ttu-id="ad137-116">Preparar o banco de dados do gerenciador de mapa de fragmentos</span><span class="sxs-lookup"><span data-stu-id="ad137-116">Prepare the shard map manager database</span></span>
<span data-ttu-id="ad137-117">O gerenciador de mapa de fragmentos é um banco de dados especial que contém os dados para gerenciar bancos de dados escalonados horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="ad137-117">The shard map manager is a special database that contains the data to manage scaled-out databases.</span></span> <span data-ttu-id="ad137-118">Você pode usar um banco de dados existente ou criar um novo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ad137-118">You can use an existing database, or create a new database.</span></span> <span data-ttu-id="ad137-119">Observe que um banco de dados que atua como gerenciador de mapa de fragmentos não deve ser o mesmo banco de dados de um fragmento.</span><span class="sxs-lookup"><span data-stu-id="ad137-119">Note that a database acting as shard map manager should not be the same database as a shard.</span></span> <span data-ttu-id="ad137-120">Observe também que o script do PowerShell não cria o banco de dados para você.</span><span class="sxs-lookup"><span data-stu-id="ad137-120">Also note that the PowerShell script does not create the database for you.</span></span> 

## <a name="step-1-create-a-shard-map-manager"></a><span data-ttu-id="ad137-121">Etapa 1: criar um gerenciador de mapa de fragmentos</span><span class="sxs-lookup"><span data-stu-id="ad137-121">Step 1: create a shard map manager</span></span>
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are the server name and database name 
    # for the new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="to-retrieve-the-shard-map-manager"></a><span data-ttu-id="ad137-122">Para recuperar o gerenciador de mapa de fragmentos</span><span class="sxs-lookup"><span data-stu-id="ad137-122">To retrieve the shard map manager</span></span>
<span data-ttu-id="ad137-123">Após a criação, você pode recuperar o gerenciador de mapa de fragmentos com este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ad137-123">After creation, you can retrieve the shard map manager with this cmdlet.</span></span> <span data-ttu-id="ad137-124">Esta etapa será necessária toda vez que você precisar usar o objeto ShardMapManager.</span><span class="sxs-lookup"><span data-stu-id="ad137-124">This step is needed every time you need to use the ShardMapManager object.</span></span>

    # Try to get a reference to the Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-the-shard-map"></a><span data-ttu-id="ad137-125">Etapa 2: criar o mapa de fragmentos</span><span class="sxs-lookup"><span data-stu-id="ad137-125">Step 2: create the shard map</span></span>
<span data-ttu-id="ad137-126">Você deve selecionar o tipo do mapa de fragmentos a criar.</span><span class="sxs-lookup"><span data-stu-id="ad137-126">You must select the type of shard map to create.</span></span> <span data-ttu-id="ad137-127">A escolha depende da arquitetura do banco de dados:</span><span class="sxs-lookup"><span data-stu-id="ad137-127">The choice depends on the database architecture:</span></span> 

1. <span data-ttu-id="ad137-128">Um locatário único por banco de dados (para termos, consulte o [glossário](sql-database-elastic-scale-glossary.md).)</span><span class="sxs-lookup"><span data-stu-id="ad137-128">Single tenant per database (For terms, see the [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
2. <span data-ttu-id="ad137-129">Vários locatários por banco de dados (dois tipos):</span><span class="sxs-lookup"><span data-stu-id="ad137-129">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="ad137-130">Mapeamento de lista</span><span class="sxs-lookup"><span data-stu-id="ad137-130">List mapping</span></span>
   2. <span data-ttu-id="ad137-131">Mapeamento de intervalo</span><span class="sxs-lookup"><span data-stu-id="ad137-131">Range mapping</span></span>

<span data-ttu-id="ad137-132">Para um modelo de locatário único, crie um mapa de fragmentos de **mapeamento de lista** .</span><span class="sxs-lookup"><span data-stu-id="ad137-132">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="ad137-133">O modelo de locatário único atribui um banco de dados por locatário.</span><span class="sxs-lookup"><span data-stu-id="ad137-133">The single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="ad137-134">Esse é um modelo eficaz para desenvolvedores de SaaS, pois simplifica o gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="ad137-134">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Mapeamento de lista][1]

<span data-ttu-id="ad137-136">O modelo multilocatário atribui vários locatários a um banco de dados individual (e você pode distribuir grupos de locatários entre vários bancos de dados).</span><span class="sxs-lookup"><span data-stu-id="ad137-136">The multi-tenant model assigns several tenants to a single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="ad137-137">Use esse modelo quando você esperar que cada locatário tenha necessidades de dados pequenas.</span><span class="sxs-lookup"><span data-stu-id="ad137-137">Use this model when you expect each tenant to have small data needs.</span></span> <span data-ttu-id="ad137-138">Nesse modelo, atribuímos um intervalo de locatários a um banco de dados usando **mapeamento de intervalo**.</span><span class="sxs-lookup"><span data-stu-id="ad137-138">In this model, we assign a range of tenants to a database using **range mapping**.</span></span> 

![Mapeamento de intervalo][2]

<span data-ttu-id="ad137-140">Ou então, você pode implementar um modelo de banco de dados multilocatário usando um *mapeamento de lista* para atribuir vários locatários a um banco de dados individual.</span><span class="sxs-lookup"><span data-stu-id="ad137-140">Or you can implement a multi-tenant database model using a *list mapping* to assign multiple tenants to a single database.</span></span> <span data-ttu-id="ad137-141">Por exemplo, DB1 é usado para armazenar informações sobre os locatários com IDs 1 e 5, e DB2 armazena dados dos locatários 7 e 10.</span><span class="sxs-lookup"><span data-stu-id="ad137-141">For example, DB1 is used to store information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Vários locatários em um banco de dados individual][3] 

<span data-ttu-id="ad137-143">**Com base na sua escolha, escolha uma destas opções:**</span><span class="sxs-lookup"><span data-stu-id="ad137-143">**Based on your choice, choose one of these options:**</span></span>

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a><span data-ttu-id="ad137-144">Opção 1: criar um mapa de fragmentos para um mapeamento de lista</span><span class="sxs-lookup"><span data-stu-id="ad137-144">Option 1: create a shard map for a list mapping</span></span>
<span data-ttu-id="ad137-145">Crie um mapa de fragmentos usando o objeto ShardMapManager.</span><span class="sxs-lookup"><span data-stu-id="ad137-145">Create a shard map using the ShardMapManager object.</span></span> 

    # $ShardMapManager is the shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a><span data-ttu-id="ad137-146">Opção 2: criar um mapa de fragmentos para um mapeamento de intervalo</span><span class="sxs-lookup"><span data-stu-id="ad137-146">Option 2: create a shard map for a range mapping</span></span>
<span data-ttu-id="ad137-147">Observe que, para utilizar esse padrão de mapeamento, os valores de ID de locatário precisam ser intervalos contínuos. É aceitável ter lacunas nos intervalos simplesmente ignorando o intervalo ao criar os bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="ad137-147">Note that to utilize this mapping pattern, tenant id values needs to be continuous ranges, and it is acceptable to have gap in the ranges by simply skipping the range when creating the databases.</span></span>

    # $ShardMapManager is the shard map manager object 
    # 'RangeShardMap' is the unique identifier for the range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a><span data-ttu-id="ad137-148">Opção 3: mapeamentos de lista em um banco de dados individual</span><span class="sxs-lookup"><span data-stu-id="ad137-148">Option 3: List mappings on a single database</span></span>
<span data-ttu-id="ad137-149">A configuração desse padrão também exige a criação de um mapa de lista conforme mostrado na etapa 2, opção 1.</span><span class="sxs-lookup"><span data-stu-id="ad137-149">Setting up this pattern also requires creation of a list map as shown in step 2, option 1.</span></span>

## <a name="step-3-prepare-individual-shards"></a><span data-ttu-id="ad137-150">Etapa 3: preparar os fragmentos individuais</span><span class="sxs-lookup"><span data-stu-id="ad137-150">Step 3: Prepare individual shards</span></span>
<span data-ttu-id="ad137-151">Adicione cada fragmento (banco de dados)ao gerenciador de mapa de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="ad137-151">Add each shard (database) to the shard map manager.</span></span> <span data-ttu-id="ad137-152">Isso prepara os bancos de dados individuais para armazenar informações de mapeamento.</span><span class="sxs-lookup"><span data-stu-id="ad137-152">This prepares the individual databases for storing mapping information.</span></span> <span data-ttu-id="ad137-153">Execute esse método em cada fragmento.</span><span class="sxs-lookup"><span data-stu-id="ad137-153">Execute this method on each shard.</span></span>

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # The $ShardMap is the shard map created in step 2.


## <a name="step-4-add-mappings"></a><span data-ttu-id="ad137-154">Etapa 4: Adicionar mapeamentos</span><span class="sxs-lookup"><span data-stu-id="ad137-154">Step 4: Add mappings</span></span>
<span data-ttu-id="ad137-155">A adição de mapeamentos depende do tipo de mapa de fragmentos criado.</span><span class="sxs-lookup"><span data-stu-id="ad137-155">The addition of mappings depends on the kind of shard map you created.</span></span> <span data-ttu-id="ad137-156">Se tiver criado um mapa de lista, você adicionará mapeamentos de lista.</span><span class="sxs-lookup"><span data-stu-id="ad137-156">If you created a list map, you add list mappings.</span></span> <span data-ttu-id="ad137-157">Se tiver criado um mapa de intervalo, você adicionará mapeamentos de intervalo.</span><span class="sxs-lookup"><span data-stu-id="ad137-157">If you created a range map, you add range mappings.</span></span>

### <a name="option-1-map-the-data-for-a-list-mapping"></a><span data-ttu-id="ad137-158">Opção 1: mapear os dados para um mapeamento de lista</span><span class="sxs-lookup"><span data-stu-id="ad137-158">Option 1: map the data for a list mapping</span></span>
<span data-ttu-id="ad137-159">Mapeie os dados adicionando um mapeamento de lista para cada locatário.</span><span class="sxs-lookup"><span data-stu-id="ad137-159">Map the data by adding a list mapping for each tenant.</span></span>  

    # Create the mappings and associate it with the new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-the-data-for-a-range-mapping"></a><span data-ttu-id="ad137-160">Opção 2: mapear os dados para um mapeamento de intervalo</span><span class="sxs-lookup"><span data-stu-id="ad137-160">Option 2: map the data for a range mapping</span></span>
<span data-ttu-id="ad137-161">Adicione os mapeamentos de intervalo para todo o intervalo de IDs de locatário – associações de banco de dados:</span><span class="sxs-lookup"><span data-stu-id="ad137-161">Add the range mappings for all the tenant id range - database associations:</span></span>

    # Create the mappings and associate it with the new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-the-data-for-multiple-tenants-on-a-single-database"></a><span data-ttu-id="ad137-162">Etapa 4, opção 3: mapear os dados de vários locatários em um banco de dados individual</span><span class="sxs-lookup"><span data-stu-id="ad137-162">Step 4 option 3: map the data for multiple tenants on a single database</span></span>
<span data-ttu-id="ad137-163">Para cada locatário, execute o Add-ListMapping (opção 1, acima).</span><span class="sxs-lookup"><span data-stu-id="ad137-163">For each tenant, run the Add-ListMapping (option 1, above).</span></span> 

## <a name="checking-the-mappings"></a><span data-ttu-id="ad137-164">Verificando os mapeamentos</span><span class="sxs-lookup"><span data-stu-id="ad137-164">Checking the mappings</span></span>
<span data-ttu-id="ad137-165">Informações sobre os fragmentos existentes e os mapeamentos associados a eles podem ser consultadas usando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="ad137-165">Information about the existing shards and the mappings associated with them can be queried using following commands:</span></span>  

    # List the shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a><span data-ttu-id="ad137-166">Resumo</span><span class="sxs-lookup"><span data-stu-id="ad137-166">Summary</span></span>
<span data-ttu-id="ad137-167">Após ter concluído a configuração, você pode começar a usar a biblioteca de cliente do Banco de Dados Elástico.</span><span class="sxs-lookup"><span data-stu-id="ad137-167">Once you have completed the setup, you can begin to use the Elastic Database client library.</span></span> <span data-ttu-id="ad137-168">Também é possível usar o [roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md) e [consulta de vários fragmentos](sql-database-elastic-scale-multishard-querying.md).</span><span class="sxs-lookup"><span data-stu-id="ad137-168">You can also use [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and [multi-shard query](sql-database-elastic-scale-multishard-querying.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad137-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ad137-169">Next steps</span></span>
<span data-ttu-id="ad137-170">Obtenha os scripts do PowerShell de [Azure SQL DB - Scripts de ferramentas de Banco de Dados Elástico](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="ad137-170">Get the PowerShell scripts from [Azure SQL DB-Elastic Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

<span data-ttu-id="ad137-171">As ferramentas também estão no GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).</span><span class="sxs-lookup"><span data-stu-id="ad137-171">The tools are also on GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).</span></span>

<span data-ttu-id="ad137-172">Use a ferramenta de divisão e mesclagem para mover dados de/para um modelo multilocatário de/para um modelo de locatário único.</span><span class="sxs-lookup"><span data-stu-id="ad137-172">Use the split-merge tool to move data to or from a multi-tenant model to a single tenant model.</span></span> <span data-ttu-id="ad137-173">Consulte [Ferramenta de divisão e mesclagem](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ad137-173">See [Split merge tool](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ad137-174">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ad137-174">Additional resources</span></span>
<span data-ttu-id="ad137-175">Para obter informações sobre os padrões comuns da arquitetura de dados dos aplicativos do banco de dados SaaS (software como serviço) multilocatário, consulte [Padrões de Design para Aplicativos SaaS multilocatário com o Banco de Dados SQL do Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span><span class="sxs-lookup"><span data-stu-id="ad137-175">For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span></span>

## <a name="questions-and-feature-requests"></a><span data-ttu-id="ad137-176">Perguntas e solicitações de recursos</span><span class="sxs-lookup"><span data-stu-id="ad137-176">Questions and Feature Requests</span></span>
<span data-ttu-id="ad137-177">Em caso de dúvidas, entre em contato conosco pelo [fórum do Banco de Dados SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) e, para solicitações de recursos, adicione-as ao [fórum de comentários sobre o Banco de Dados SQL](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="ad137-177">For questions, please reach out to us on the [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them to the [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

