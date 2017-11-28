---
title: aaaMigrate existente tooscale fora de bancos de dados | Microsoft Docs
description: "Converter ferramentas de banco de dados Elástico toouse bancos de dados fragmentados, criando um Gerenciador de mapa do fragmento"
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
ms.openlocfilehash: fa2c9e3699f30667cf547d1faadf4504609199be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-existing-databases-tooscale-out"></a><span data-ttu-id="92467-103">Migrar tooscale-out de bancos de dados existente</span><span class="sxs-lookup"><span data-stu-id="92467-103">Migrate existing databases tooscale-out</span></span>
<span data-ttu-id="92467-104">Gerenciar facilmente expandido fragmentados bancos de dados existentes usando as ferramentas de banco de dados do banco de dados SQL (como Olá [biblioteca de cliente do banco de dados Elástico](sql-database-elastic-database-client-library.md)).</span><span class="sxs-lookup"><span data-stu-id="92467-104">Easily manage your existing scaled-out sharded databases using Azure SQL Database database tools (such as hello [Elastic Database client library](sql-database-elastic-database-client-library.md)).</span></span> <span data-ttu-id="92467-105">Você deve primeiro converter um conjunto existente de saudação do bancos de dados toouse [Gerenciador do mapa de fragmentos](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="92467-105">You must first convert an existing set of databases toouse hello [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="92467-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="92467-106">Overview</span></span>
<span data-ttu-id="92467-107">toomigrate um banco de dados fragmentado existente:</span><span class="sxs-lookup"><span data-stu-id="92467-107">toomigrate an existing sharded database:</span></span> 

1. <span data-ttu-id="92467-108">Preparar Olá [banco de dados do fragmento mapa manager](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="92467-108">Prepare hello [shard map manager database](sql-database-elastic-scale-shard-map-management.md).</span></span>
2. <span data-ttu-id="92467-109">Crie um mapa do fragmento hello.</span><span class="sxs-lookup"><span data-stu-id="92467-109">Create hello shard map.</span></span>
3. <span data-ttu-id="92467-110">Prepare os fragmentos individuais hello.</span><span class="sxs-lookup"><span data-stu-id="92467-110">Prepare hello individual shards.</span></span>  
4. <span data-ttu-id="92467-111">Adicione o mapa do fragmento toohello mapeamentos.</span><span class="sxs-lookup"><span data-stu-id="92467-111">Add mappings toohello shard map.</span></span>

<span data-ttu-id="92467-112">Essas técnicas podem ser implementadas usando qualquer Olá [biblioteca de cliente do .NET Framework](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), ou scripts do PowerShell Olá encontrado em [DB do SQL Azure - scripts de ferramentas de banco de dados Elástico](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="92467-112">These techniques can be implemented using either hello [.NET Framework client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), or hello PowerShell scripts found at [Azure SQL DB - Elastic Database tools scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span> <span data-ttu-id="92467-113">Estes exemplos Olá usam scripts do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="92467-113">hello examples here use hello PowerShell scripts.</span></span>

<span data-ttu-id="92467-114">Para obter mais informações sobre Olá ShardMapManager, consulte [gerenciamento de mapa do fragmento](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="92467-114">For more information about hello ShardMapManager, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="92467-115">Para obter uma visão geral das ferramentas de banco de dados Elástico hello, consulte [visão geral dos recursos de banco de dados Elástico](sql-database-elastic-scale-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="92467-115">For an overview of hello elastic database tools, see [Elastic Database features overview](sql-database-elastic-scale-introduction.md).</span></span>

## <a name="prepare-hello-shard-map-manager-database"></a><span data-ttu-id="92467-116">Preparar o banco de dados do hello fragmento mapa manager</span><span class="sxs-lookup"><span data-stu-id="92467-116">Prepare hello shard map manager database</span></span>
<span data-ttu-id="92467-117">Gerenciador do mapa de fragmentos Olá é um banco de dados especial que contém os bancos de dados do hello dados toomanage expansíveis.</span><span class="sxs-lookup"><span data-stu-id="92467-117">hello shard map manager is a special database that contains hello data toomanage scaled-out databases.</span></span> <span data-ttu-id="92467-118">Você pode usar um banco de dados existente ou criar um novo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="92467-118">You can use an existing database, or create a new database.</span></span> <span data-ttu-id="92467-119">Observe que um banco de dados atua como o Gerenciador do mapa do fragmento não deve ser Olá mesmo banco de dados como um fragmento.</span><span class="sxs-lookup"><span data-stu-id="92467-119">Note that a database acting as shard map manager should not be hello same database as a shard.</span></span> <span data-ttu-id="92467-120">Observe também que o script do PowerShell Olá não criar banco de dados de saudação para você.</span><span class="sxs-lookup"><span data-stu-id="92467-120">Also note that hello PowerShell script does not create hello database for you.</span></span> 

## <a name="step-1-create-a-shard-map-manager"></a><span data-ttu-id="92467-121">Etapa 1: criar um gerenciador de mapa de fragmentos</span><span class="sxs-lookup"><span data-stu-id="92467-121">Step 1: create a shard map manager</span></span>
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are hello server name and database name 
    # for hello new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="tooretrieve-hello-shard-map-manager"></a><span data-ttu-id="92467-122">Gerenciador do mapa de fragmentos tooretrieve Olá</span><span class="sxs-lookup"><span data-stu-id="92467-122">tooretrieve hello shard map manager</span></span>
<span data-ttu-id="92467-123">Após a criação, você pode recuperar o Gerenciador do mapa de fragmentos Olá com esse cmdlet.</span><span class="sxs-lookup"><span data-stu-id="92467-123">After creation, you can retrieve hello shard map manager with this cmdlet.</span></span> <span data-ttu-id="92467-124">Essa etapa é necessária sempre que é necessário toouse Olá ShardMapManager objeto.</span><span class="sxs-lookup"><span data-stu-id="92467-124">This step is needed every time you need toouse hello ShardMapManager object.</span></span>

    # Try tooget a reference toohello Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-hello-shard-map"></a><span data-ttu-id="92467-125">Etapa 2: criar um mapa do fragmento Olá</span><span class="sxs-lookup"><span data-stu-id="92467-125">Step 2: create hello shard map</span></span>
<span data-ttu-id="92467-126">Você deve selecionar o tipo de saudação do toocreate de mapa do fragmento.</span><span class="sxs-lookup"><span data-stu-id="92467-126">You must select hello type of shard map toocreate.</span></span> <span data-ttu-id="92467-127">Olá escolha depende da arquitetura de banco de dados de saudação:</span><span class="sxs-lookup"><span data-stu-id="92467-127">hello choice depends on hello database architecture:</span></span> 

1. <span data-ttu-id="92467-128">Único locatário por banco de dados (para termos, consulte Olá [glossário](sql-database-elastic-scale-glossary.md).)</span><span class="sxs-lookup"><span data-stu-id="92467-128">Single tenant per database (For terms, see hello [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
2. <span data-ttu-id="92467-129">Vários locatários por banco de dados (dois tipos):</span><span class="sxs-lookup"><span data-stu-id="92467-129">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="92467-130">Mapeamento de lista</span><span class="sxs-lookup"><span data-stu-id="92467-130">List mapping</span></span>
   2. <span data-ttu-id="92467-131">Mapeamento de intervalo</span><span class="sxs-lookup"><span data-stu-id="92467-131">Range mapping</span></span>

<span data-ttu-id="92467-132">Para um modelo de locatário único, crie um mapa de fragmentos de **mapeamento de lista** .</span><span class="sxs-lookup"><span data-stu-id="92467-132">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="92467-133">modelo de único locatário Olá atribui um banco de dados por locatário.</span><span class="sxs-lookup"><span data-stu-id="92467-133">hello single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="92467-134">Esse é um modelo eficaz para desenvolvedores de SaaS, pois simplifica o gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="92467-134">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Mapeamento de lista][1]

<span data-ttu-id="92467-136">modelo de multilocatário Olá atribui vários locatários tooa único banco de dados (e você pode distribuir os grupos de locatários entre vários bancos de dados).</span><span class="sxs-lookup"><span data-stu-id="92467-136">hello multi-tenant model assigns several tenants tooa single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="92467-137">Use este modelo quando você espera que precisam de cada locatário toohave pequenos de dados.</span><span class="sxs-lookup"><span data-stu-id="92467-137">Use this model when you expect each tenant toohave small data needs.</span></span> <span data-ttu-id="92467-138">Nesse modelo, nós atribuímos um intervalo de locatários usando o banco de dados tooa **mapeamento intervalo**.</span><span class="sxs-lookup"><span data-stu-id="92467-138">In this model, we assign a range of tenants tooa database using **range mapping**.</span></span> 

![Mapeamento de intervalo][2]

<span data-ttu-id="92467-140">Ou você pode implementar um modelo de banco de dados de vários locatários usando um *mapeamento de lista* tooassign vários locatários tooa único banco de dados.</span><span class="sxs-lookup"><span data-stu-id="92467-140">Or you can implement a multi-tenant database model using a *list mapping* tooassign multiple tenants tooa single database.</span></span> <span data-ttu-id="92467-141">Por exemplo, DB1 é usado toostore informações sobre a id de locatário 1 e 5 e DB2 armazena dados de locatário 7 e locatário 10.</span><span class="sxs-lookup"><span data-stu-id="92467-141">For example, DB1 is used toostore information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Vários locatários em um banco de dados individual][3] 

<span data-ttu-id="92467-143">**Com base na sua escolha, escolha uma destas opções:**</span><span class="sxs-lookup"><span data-stu-id="92467-143">**Based on your choice, choose one of these options:**</span></span>

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a><span data-ttu-id="92467-144">Opção 1: criar um mapa de fragmentos para um mapeamento de lista</span><span class="sxs-lookup"><span data-stu-id="92467-144">Option 1: create a shard map for a list mapping</span></span>
<span data-ttu-id="92467-145">Crie um mapa do fragmento usando Olá ShardMapManager objeto.</span><span class="sxs-lookup"><span data-stu-id="92467-145">Create a shard map using hello ShardMapManager object.</span></span> 

    # $ShardMapManager is hello shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a><span data-ttu-id="92467-146">Opção 2: criar um mapa de fragmentos para um mapeamento de intervalo</span><span class="sxs-lookup"><span data-stu-id="92467-146">Option 2: create a shard map for a range mapping</span></span>
<span data-ttu-id="92467-147">Observe que tooutilize esse padrão de mapeamento, valores de id de locatário precisa intervalos contínuos toobe e é o intervalo aceitável toohave em intervalos de saudação simplesmente ignorar o intervalo de saudação durante a criação de bancos de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="92467-147">Note that tooutilize this mapping pattern, tenant id values needs toobe continuous ranges, and it is acceptable toohave gap in hello ranges by simply skipping hello range when creating hello databases.</span></span>

    # $ShardMapManager is hello shard map manager object 
    # 'RangeShardMap' is hello unique identifier for hello range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a><span data-ttu-id="92467-148">Opção 3: mapeamentos de lista em um banco de dados individual</span><span class="sxs-lookup"><span data-stu-id="92467-148">Option 3: List mappings on a single database</span></span>
<span data-ttu-id="92467-149">A configuração desse padrão também exige a criação de um mapa de lista conforme mostrado na etapa 2, opção 1.</span><span class="sxs-lookup"><span data-stu-id="92467-149">Setting up this pattern also requires creation of a list map as shown in step 2, option 1.</span></span>

## <a name="step-3-prepare-individual-shards"></a><span data-ttu-id="92467-150">Etapa 3: preparar os fragmentos individuais</span><span class="sxs-lookup"><span data-stu-id="92467-150">Step 3: Prepare individual shards</span></span>
<span data-ttu-id="92467-151">Adicione o Gerenciador do mapa de fragmento de toohello cada fragmento (banco de dados).</span><span class="sxs-lookup"><span data-stu-id="92467-151">Add each shard (database) toohello shard map manager.</span></span> <span data-ttu-id="92467-152">Isso prepara os bancos de dados individuais Olá para armazenar informações de mapeamento.</span><span class="sxs-lookup"><span data-stu-id="92467-152">This prepares hello individual databases for storing mapping information.</span></span> <span data-ttu-id="92467-153">Execute esse método em cada fragmento.</span><span class="sxs-lookup"><span data-stu-id="92467-153">Execute this method on each shard.</span></span>

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # hello $ShardMap is hello shard map created in step 2.


## <a name="step-4-add-mappings"></a><span data-ttu-id="92467-154">Etapa 4: Adicionar mapeamentos</span><span class="sxs-lookup"><span data-stu-id="92467-154">Step 4: Add mappings</span></span>
<span data-ttu-id="92467-155">adição de saudação de mapeamentos de depende em tipo de saudação do mapa de fragmentos que você criou.</span><span class="sxs-lookup"><span data-stu-id="92467-155">hello addition of mappings depends on hello kind of shard map you created.</span></span> <span data-ttu-id="92467-156">Se tiver criado um mapa de lista, você adicionará mapeamentos de lista.</span><span class="sxs-lookup"><span data-stu-id="92467-156">If you created a list map, you add list mappings.</span></span> <span data-ttu-id="92467-157">Se tiver criado um mapa de intervalo, você adicionará mapeamentos de intervalo.</span><span class="sxs-lookup"><span data-stu-id="92467-157">If you created a range map, you add range mappings.</span></span>

### <a name="option-1-map-hello-data-for-a-list-mapping"></a><span data-ttu-id="92467-158">Opção 1: dados de saudação do mapa para um mapeamento de lista</span><span class="sxs-lookup"><span data-stu-id="92467-158">Option 1: map hello data for a list mapping</span></span>
<span data-ttu-id="92467-159">Mapear dados de saudação adicionando um mapeamento de lista para cada locatário.</span><span class="sxs-lookup"><span data-stu-id="92467-159">Map hello data by adding a list mapping for each tenant.</span></span>  

    # Create hello mappings and associate it with hello new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-hello-data-for-a-range-mapping"></a><span data-ttu-id="92467-160">Opção 2: dados de saudação do mapa para um mapeamento de intervalo</span><span class="sxs-lookup"><span data-stu-id="92467-160">Option 2: map hello data for a range mapping</span></span>
<span data-ttu-id="92467-161">Adicione mapeamentos de intervalo de saudação para todos os Olá locatário intervalo de id - associações de banco de dados:</span><span class="sxs-lookup"><span data-stu-id="92467-161">Add hello range mappings for all hello tenant id range - database associations:</span></span>

    # Create hello mappings and associate it with hello new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-hello-data-for-multiple-tenants-on-a-single-database"></a><span data-ttu-id="92467-162">Etapa 4 opção 3: mapear dados de saudação para vários locatários em um único banco de dados</span><span class="sxs-lookup"><span data-stu-id="92467-162">Step 4 option 3: map hello data for multiple tenants on a single database</span></span>
<span data-ttu-id="92467-163">Para cada locatário, execute Olá adicionar ListMapping (opção 1, acima).</span><span class="sxs-lookup"><span data-stu-id="92467-163">For each tenant, run hello Add-ListMapping (option 1, above).</span></span> 

## <a name="checking-hello-mappings"></a><span data-ttu-id="92467-164">Verificando os mapeamentos de saudação</span><span class="sxs-lookup"><span data-stu-id="92467-164">Checking hello mappings</span></span>
<span data-ttu-id="92467-165">Informações sobre fragmentos existentes hello e mapeamentos de saudação associados a eles podem ser consultadas usando comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="92467-165">Information about hello existing shards and hello mappings associated with them can be queried using following commands:</span></span>  

    # List hello shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a><span data-ttu-id="92467-166">Resumo</span><span class="sxs-lookup"><span data-stu-id="92467-166">Summary</span></span>
<span data-ttu-id="92467-167">Depois de concluir a instalação hello, você pode começar a biblioteca de cliente de banco de dados Elástico toouse hello.</span><span class="sxs-lookup"><span data-stu-id="92467-167">Once you have completed hello setup, you can begin toouse hello Elastic Database client library.</span></span> <span data-ttu-id="92467-168">Também é possível usar o [roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md) e [consulta de vários fragmentos](sql-database-elastic-scale-multishard-querying.md).</span><span class="sxs-lookup"><span data-stu-id="92467-168">You can also use [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and [multi-shard query](sql-database-elastic-scale-multishard-querying.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="92467-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="92467-169">Next steps</span></span>
<span data-ttu-id="92467-170">Obter scripts do PowerShell de saudação do [sripts das ferramentas de banco de dados do Azure SQL DB elástica](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="92467-170">Get hello PowerShell scripts from [Azure SQL DB-Elastic Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

<span data-ttu-id="92467-171">Olá ferramentas também estão no GitHub: [Azure/elástica-db-tools](https://github.com/Azure/elastic-db-tools).</span><span class="sxs-lookup"><span data-stu-id="92467-171">hello tools are also on GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).</span></span>

<span data-ttu-id="92467-172">Use Olá ferramenta de mesclagem de divisão toomove dados tooor de um modelo de locatário único tooa modelo multilocatário.</span><span class="sxs-lookup"><span data-stu-id="92467-172">Use hello split-merge tool toomove data tooor from a multi-tenant model tooa single tenant model.</span></span> <span data-ttu-id="92467-173">Consulte [Ferramenta de divisão e mesclagem](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="92467-173">See [Split merge tool](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="92467-174">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="92467-174">Additional resources</span></span>
<span data-ttu-id="92467-175">Para obter informações sobre os padrões comuns da arquitetura de dados dos aplicativos do banco de dados SaaS (software como serviço) multilocatário, consulte [Padrões de Design para Aplicativos SaaS multilocatário com o Banco de Dados SQL do Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span><span class="sxs-lookup"><span data-stu-id="92467-175">For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span></span>

## <a name="questions-and-feature-requests"></a><span data-ttu-id="92467-176">Perguntas e solicitações de recursos</span><span class="sxs-lookup"><span data-stu-id="92467-176">Questions and Feature Requests</span></span>
<span data-ttu-id="92467-177">Para dúvidas, entre em contato toous em Olá [Fórum do banco de dados SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) e para solicitações de recurso, adicione-toohello [Fórum de comentários do banco de dados SQL](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="92467-177">For questions, please reach out toous on hello [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them toohello [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

