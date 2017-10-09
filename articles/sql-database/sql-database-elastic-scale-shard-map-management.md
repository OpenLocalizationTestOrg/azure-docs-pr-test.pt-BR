---
title: aaaScale-out de um banco de dados SQL do Azure | Microsoft Docs
description: "Como toouse Olá ShardMapManager, biblioteca de cliente do banco de dados Elástico"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 4cf670d42ad7ded98fb8d6f0830154587dd2c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-out-databases-with-hello-shard-map-manager"></a><span data-ttu-id="4e1b5-103">Expansão de bancos de dados com o Gerenciador do mapa de fragmentos Olá</span><span class="sxs-lookup"><span data-stu-id="4e1b5-103">Scale out databases with hello shard map manager</span></span>
<span data-ttu-id="4e1b5-104">tooeasily expansão de bancos de dados no SQL Azure, use um Gerenciador de mapa do fragmento.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-104">tooeasily scale out databases on SQL Azure, use a shard map manager.</span></span> <span data-ttu-id="4e1b5-105">Gerenciador do mapa de fragmentos Olá é um banco de dados especial que mantém as informações sobre todos os fragmentos (bancos de dados) em um conjunto de fragmentos de mapeamento global.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-105">hello shard map manager is a special database that maintains global mapping information about all shards (databases) in a shard set.</span></span> <span data-ttu-id="4e1b5-106">Olá metadados permitem que um aplicativo tooconnect toohello banco de dados correto com base no valor Olá Olá **chave de fragmentação**.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-106">hello metadata allows an application tooconnect toohello correct database based upon hello value of hello **sharding key**.</span></span> <span data-ttu-id="4e1b5-107">Além disso, cada fragmento no conjunto de saudação contém mapas que acompanham os dados de local de fragmento de saudação (conhecido como **shardlets**).</span><span class="sxs-lookup"><span data-stu-id="4e1b5-107">In addition, every shard in hello set contains maps that track hello local shard data (known as **shardlets**).</span></span> 

![Gerenciamento de mapa de fragmentos](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

<span data-ttu-id="4e1b5-109">Noções básicas sobre como esses mapas são construídos é tooshard essenciais de gerenciamento de mapa.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-109">Understanding how these maps are constructed is essential tooshard map management.</span></span> <span data-ttu-id="4e1b5-110">Isso é feito usando Olá [ShardMapManager classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), encontrado em Olá [biblioteca de cliente do banco de dados Elástico](sql-database-elastic-database-client-library.md) toomanage fragmento é mapeado.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-110">This is done using hello [ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), found in hello [Elastic Database client library](sql-database-elastic-database-client-library.md) toomanage shard maps.</span></span>  

## <a name="shard-maps-and-shard-mappings"></a><span data-ttu-id="4e1b5-111">Mapas de fragmentos e mapeamentos de fragmentos</span><span class="sxs-lookup"><span data-stu-id="4e1b5-111">Shard maps and shard mappings</span></span>
<span data-ttu-id="4e1b5-112">Para cada fragmento, você deve selecionar o tipo de saudação do toocreate de mapa do fragmento.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-112">For each shard, you must select hello type of shard map toocreate.</span></span> <span data-ttu-id="4e1b5-113">Olá escolha depende da arquitetura de banco de dados de saudação:</span><span class="sxs-lookup"><span data-stu-id="4e1b5-113">hello choice depends on hello database architecture:</span></span> 

1. <span data-ttu-id="4e1b5-114">Um locatário único por banco de dados</span><span class="sxs-lookup"><span data-stu-id="4e1b5-114">Single tenant per database</span></span>  
2. <span data-ttu-id="4e1b5-115">Vários locatários por banco de dados (dois tipos):</span><span class="sxs-lookup"><span data-stu-id="4e1b5-115">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="4e1b5-116">Mapeamento de lista</span><span class="sxs-lookup"><span data-stu-id="4e1b5-116">List mapping</span></span>
   2. <span data-ttu-id="4e1b5-117">Mapeamento de intervalo</span><span class="sxs-lookup"><span data-stu-id="4e1b5-117">Range mapping</span></span>

<span data-ttu-id="4e1b5-118">Para um modelo de locatário único, crie um mapa de fragmentos de **mapeamento de lista** .</span><span class="sxs-lookup"><span data-stu-id="4e1b5-118">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="4e1b5-119">modelo de único locatário Olá atribui um banco de dados por locatário.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-119">hello single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="4e1b5-120">Esse é um modelo eficaz para desenvolvedores de SaaS, pois simplifica o gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-120">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Mapeamento de lista][1]

<span data-ttu-id="4e1b5-122">modelo de multilocatário Olá atribui vários locatários tooa único banco de dados (e você pode distribuir os grupos de locatários entre vários bancos de dados).</span><span class="sxs-lookup"><span data-stu-id="4e1b5-122">hello multi-tenant model assigns several tenants tooa single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="4e1b5-123">Use este modelo quando você espera que precisam de cada locatário toohave pequenos de dados.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-123">Use this model when you expect each tenant toohave small data needs.</span></span> <span data-ttu-id="4e1b5-124">Nesse modelo, nós atribuímos um intervalo de locatários usando o banco de dados tooa **mapeamento intervalo**.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-124">In this model, we assign a range of tenants tooa database using **range mapping**.</span></span> 

![Mapeamento de intervalo][2]

<span data-ttu-id="4e1b5-126">Ou você pode implementar um modelo de banco de dados de vários locatários usando um *mapeamento de lista* tooassign vários locatários tooa único banco de dados.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-126">Or you can implement a multi-tenant database model using a *list mapping* tooassign multiple tenants tooa single database.</span></span> <span data-ttu-id="4e1b5-127">Por exemplo, DB1 é usado toostore informações sobre a id de locatário 1 e 5 e DB2 armazena dados de locatário 7 e locatário 10.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-127">For example, DB1 is used toostore information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Vários locatários em um banco de dados individual][3] 

### <a name="supported-net-types-for-sharding-keys"></a><span data-ttu-id="4e1b5-129">Tipos .Net com suporte para chaves de fragmentação</span><span class="sxs-lookup"><span data-stu-id="4e1b5-129">Supported .Net types for sharding keys</span></span>
<span data-ttu-id="4e1b5-130">Elástico Olá de suporte de escala após o .net Framework tipos como chaves de fragmentação:</span><span class="sxs-lookup"><span data-stu-id="4e1b5-130">Elastic Scale support hello following .Net Framework types as sharding keys:</span></span>

* <span data-ttu-id="4e1b5-131">inteiro</span><span class="sxs-lookup"><span data-stu-id="4e1b5-131">integer</span></span>
* <span data-ttu-id="4e1b5-132">longo</span><span class="sxs-lookup"><span data-stu-id="4e1b5-132">long</span></span>
* <span data-ttu-id="4e1b5-133">guid</span><span class="sxs-lookup"><span data-stu-id="4e1b5-133">guid</span></span>
* <span data-ttu-id="4e1b5-134">byte[]</span><span class="sxs-lookup"><span data-stu-id="4e1b5-134">byte[]</span></span>  
* <span data-ttu-id="4e1b5-135">datetime</span><span class="sxs-lookup"><span data-stu-id="4e1b5-135">datetime</span></span>
* <span data-ttu-id="4e1b5-136">timespan</span><span class="sxs-lookup"><span data-stu-id="4e1b5-136">timespan</span></span>
* <span data-ttu-id="4e1b5-137">datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="4e1b5-137">datetimeoffset</span></span>

### <a name="list-and-range-shard-maps"></a><span data-ttu-id="4e1b5-138">Mapas de fragmentos de lista e intervalo</span><span class="sxs-lookup"><span data-stu-id="4e1b5-138">List and range shard maps</span></span>
<span data-ttu-id="4e1b5-139">Mapas de fragmentos podem ser construídos usando **listas de valores de chave de fragmentação individuais** ou **intervalos de valores de chave de fragmentação**.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-139">Shard maps can be constructed using **lists of individual sharding key values**, or they can be constructed using **ranges of sharding key values**.</span></span> 

### <a name="list-shard-maps"></a><span data-ttu-id="4e1b5-140">Mapas de fragmentos de lista</span><span class="sxs-lookup"><span data-stu-id="4e1b5-140">List shard maps</span></span>
<span data-ttu-id="4e1b5-141">**Fragmentos** contêm **shardlets** e mapeamento de saudação do shardlets tooshards é mantido por um mapa do fragmento.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-141">**Shards** contain **shardlets** and hello mapping of shardlets tooshards is maintained by a shard map.</span></span> <span data-ttu-id="4e1b5-142">Um **mapa do fragmento lista** é uma associação entre Olá individuais valores de chave que identificam Olá shardlets e bancos de dados de saudação que servem como fragmentos.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-142">A **list shard map** is an association between hello individual key values that identify hello shardlets and hello databases that serve as shards.</span></span>  <span data-ttu-id="4e1b5-143">**Lista de mapeamentos de** são explícita e diferentes valores de chave podem ser mapeada toohello mesmo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-143">**List mappings** are explicit and different key values can be mapped toohello same database.</span></span> <span data-ttu-id="4e1b5-144">Por exemplo, a chave 1 mapeia tooDatabase A e B. o banco de dados de referência de valores de chave 3 e 6</span><span class="sxs-lookup"><span data-stu-id="4e1b5-144">For example, key 1 maps tooDatabase A, and key values 3 and 6 both reference Database B.</span></span>

| <span data-ttu-id="4e1b5-145">Chave</span><span class="sxs-lookup"><span data-stu-id="4e1b5-145">Key</span></span> | <span data-ttu-id="4e1b5-146">Local de fragmento</span><span class="sxs-lookup"><span data-stu-id="4e1b5-146">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="4e1b5-147">1</span><span class="sxs-lookup"><span data-stu-id="4e1b5-147">1</span></span> |<span data-ttu-id="4e1b5-148">Database_A</span><span class="sxs-lookup"><span data-stu-id="4e1b5-148">Database_A</span></span> |
| <span data-ttu-id="4e1b5-149">3</span><span class="sxs-lookup"><span data-stu-id="4e1b5-149">3</span></span> |<span data-ttu-id="4e1b5-150">Database_B</span><span class="sxs-lookup"><span data-stu-id="4e1b5-150">Database_B</span></span> |
| <span data-ttu-id="4e1b5-151">4</span><span class="sxs-lookup"><span data-stu-id="4e1b5-151">4</span></span> |<span data-ttu-id="4e1b5-152">Database_C</span><span class="sxs-lookup"><span data-stu-id="4e1b5-152">Database_C</span></span> |
| <span data-ttu-id="4e1b5-153">6</span><span class="sxs-lookup"><span data-stu-id="4e1b5-153">6</span></span> |<span data-ttu-id="4e1b5-154">Database_B</span><span class="sxs-lookup"><span data-stu-id="4e1b5-154">Database_B</span></span> |
| <span data-ttu-id="4e1b5-155">...</span><span class="sxs-lookup"><span data-stu-id="4e1b5-155">...</span></span> |<span data-ttu-id="4e1b5-156">...</span><span class="sxs-lookup"><span data-stu-id="4e1b5-156">...</span></span> |

### <a name="range-shard-maps"></a><span data-ttu-id="4e1b5-157">Mapas de fragmentos de intervalo</span><span class="sxs-lookup"><span data-stu-id="4e1b5-157">Range shard maps</span></span>
<span data-ttu-id="4e1b5-158">Em um **mapa do fragmento intervalo**, intervalo de chave Olá é descrito por um par de **[valor baixo, alto valor)** onde Olá *valor baixo* Olá de chave mínimo no intervalo de saudação e Olá *Valor alto* é Olá primeiro valor maior do que o intervalo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-158">In a **range shard map**, hello key range is described by a pair **[Low Value, High Value)** where hello *Low Value* is hello minimum key in hello range, and hello *High Value* is hello first value higher than hello range.</span></span> 

<span data-ttu-id="4e1b5-159">Por exemplo, **(0, 100)** inclui todos os números inteiros iguais ou maiores que 0 e menores que 100.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-159">For example, **[0, 100)** includes all integers greater than or equal 0 and less than 100.</span></span> <span data-ttu-id="4e1b5-160">Observe que várias toohello intervalos da ponto pode mesmo banco de dados e intervalos de separação têm suporte (por exemplo, [100,200) e [400,600) ambos os ponto tooDatabase C exemplo hello abaixo.)</span><span class="sxs-lookup"><span data-stu-id="4e1b5-160">Note that multiple ranges can point toohello same database, and disjoint ranges are supported (e.g., [100,200) and [400,600) both point tooDatabase C in hello example below.)</span></span>

| <span data-ttu-id="4e1b5-161">Chave</span><span class="sxs-lookup"><span data-stu-id="4e1b5-161">Key</span></span> | <span data-ttu-id="4e1b5-162">Local de fragmento</span><span class="sxs-lookup"><span data-stu-id="4e1b5-162">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="4e1b5-163">[1,50)</span><span class="sxs-lookup"><span data-stu-id="4e1b5-163">[1,50)</span></span> |<span data-ttu-id="4e1b5-164">Database_A</span><span class="sxs-lookup"><span data-stu-id="4e1b5-164">Database_A</span></span> |
| <span data-ttu-id="4e1b5-165">[50,100)</span><span class="sxs-lookup"><span data-stu-id="4e1b5-165">[50,100)</span></span> |<span data-ttu-id="4e1b5-166">Database_B</span><span class="sxs-lookup"><span data-stu-id="4e1b5-166">Database_B</span></span> |
| <span data-ttu-id="4e1b5-167">[100,200)</span><span class="sxs-lookup"><span data-stu-id="4e1b5-167">[100,200)</span></span> |<span data-ttu-id="4e1b5-168">Database_C</span><span class="sxs-lookup"><span data-stu-id="4e1b5-168">Database_C</span></span> |
| <span data-ttu-id="4e1b5-169">[400,600)</span><span class="sxs-lookup"><span data-stu-id="4e1b5-169">[400,600)</span></span> |<span data-ttu-id="4e1b5-170">Database_C</span><span class="sxs-lookup"><span data-stu-id="4e1b5-170">Database_C</span></span> |
| <span data-ttu-id="4e1b5-171">...</span><span class="sxs-lookup"><span data-stu-id="4e1b5-171">...</span></span> |<span data-ttu-id="4e1b5-172">...</span><span class="sxs-lookup"><span data-stu-id="4e1b5-172">...</span></span> |

<span data-ttu-id="4e1b5-173">Cada uma das tabelas de saudação mostradas acima é um exemplo conceitual de um **ShardMap** objeto.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-173">Each of hello tables shown above is a conceptual example of a **ShardMap** object.</span></span> <span data-ttu-id="4e1b5-174">Cada linha é um exemplo simplificado de um indivíduo **PointMapping** (para o mapa do fragmento lista Olá) ou **RangeMapping** (para o mapa do fragmento de intervalo de saudação) objeto.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-174">Each row is a simplified example of an individual **PointMapping** (for hello list shard map) or **RangeMapping** (for hello range shard map) object.</span></span>

## <a name="shard-map-manager"></a><span data-ttu-id="4e1b5-175">Gerenciador de mapa de fragmentos</span><span class="sxs-lookup"><span data-stu-id="4e1b5-175">Shard map manager</span></span>
<span data-ttu-id="4e1b5-176">Na biblioteca de cliente Olá, o Gerenciador do mapa de fragmentos Olá é uma coleção de mapas de fragmento.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-176">In hello client library, hello shard map  manager is a collection of shard maps.</span></span> <span data-ttu-id="4e1b5-177">Olá dados gerenciados por um **ShardMapManager** instância é mantida em três locais:</span><span class="sxs-lookup"><span data-stu-id="4e1b5-177">hello data managed by a **ShardMapManager** instance is kept in three places:</span></span> 

1. <span data-ttu-id="4e1b5-178">**Mapa de fragmento global (GSM)**: especificar um tooserve de banco de dados como repositório Olá para todos os seus mapas de fragmento e mapeamentos.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-178">**Global Shard Map (GSM)**: You specify a database tooserve as hello repository for all of its shard maps and mappings.</span></span> <span data-ttu-id="4e1b5-179">Procedimentos armazenados e tabelas especiais são criados automaticamente informações de saudação toomanage.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-179">Special tables and stored procedures are automatically created toomanage hello information.</span></span> <span data-ttu-id="4e1b5-180">Isso geralmente é um banco de dados pequeno e pouco acessados e não deve ser usado para outras necessidades de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-180">This is typically a small database and lightly accessed, and it should not be used for other needs of hello application.</span></span> <span data-ttu-id="4e1b5-181">Olá tabelas estão em um esquema especial chamado **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-181">hello tables are in a special schema named **__ShardManagement**.</span></span> 
2. <span data-ttu-id="4e1b5-182">**Mapa de fragmento local (LSM)**: cada banco de dados que você especificar toobe um fragmento é modificado toocontain várias tabelas pequenas e procedimentos armazenados especiais que contêm e gerenciar o fragmento do fragmento mapa informações toothat específico.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-182">**Local Shard Map (LSM)**: Every database that you specify toobe a shard is modified toocontain several small tables and special stored procedures that contain and manage shard map information specific toothat shard.</span></span> <span data-ttu-id="4e1b5-183">Essas informações são redundantes com informações Olá Olá GSM e permite que informações de mapa de fragmento do hello aplicativo toovalidate armazenado em cache sem colocar nenhuma carga no hello GSM; aplicativo Hello usa Olá LSM toodetermine se um mapeamento em cache ainda é válido.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-183">This information is redundant with hello information in hello GSM, and it allows hello application toovalidate cached shard map information without placing any load on hello GSM; hello application uses hello LSM toodetermine if a cached mapping is still valid.</span></span> <span data-ttu-id="4e1b5-184">Olá tabelas correspondente toohello LSM em cada fragmento também estão no esquema de saudação **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-184">hello tables corresponding toohello LSM on each shard are also in hello schema **__ShardManagement**.</span></span>
3. <span data-ttu-id="4e1b5-185">**Cache do aplicativo**: cada instância do aplicativo que acessa um objeto **ShardMapManager** mantém um cache na memória local dos seus mapeamentos.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-185">**Application cache**: Each application instance accessing a **ShardMapManager** object maintains a local in-memory cache of its mappings.</span></span> <span data-ttu-id="4e1b5-186">Ele armazena informações de roteamento que recentemente foi recuperadas.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-186">It stores routing information that has recently been retrieved.</span></span> 

## <a name="constructing-a-shardmapmanager"></a><span data-ttu-id="4e1b5-187">Construindo um ShardMapManager</span><span class="sxs-lookup"><span data-stu-id="4e1b5-187">Constructing a ShardMapManager</span></span>
<span data-ttu-id="4e1b5-188">Um objeto **ShardMapManager** é construído usando um padrão [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4e1b5-188">A **ShardMapManager** object is constructed using a [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) pattern.</span></span> <span data-ttu-id="4e1b5-189">Olá  **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**  método usa as credenciais (incluindo o nome do servidor de saudação e nome de banco de dados, mantendo a saudação GSM) na forma de saudação de um  **ConnectionString** e retorna uma instância de um **ShardMapManager**.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-189">hello **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** method takes credentials (including hello server name and database name holding hello GSM) in hello form of a **ConnectionString** and returns an instance of a **ShardMapManager**.</span></span>  

<span data-ttu-id="4e1b5-190">**Observação:** Olá **ShardMapManager** deve ser instanciada somente uma vez por domínio de aplicativo, no código de inicialização de saudação para um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-190">**Please Note:** hello **ShardMapManager** should be instantiated only once per app domain, within hello initialization code for an application.</span></span> <span data-ttu-id="4e1b5-191">Criação de instâncias adicionais do ShardMapManager em Olá mesmo appdomain, resultará em maior utilização de memória e CPU do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-191">Creation of additional instances of ShardMapManager in hello same appdomain, will result in increased memory and CPU utilization of hello application.</span></span> <span data-ttu-id="4e1b5-192">Um **ShardMapManager** pode conter diversos mapas de fragmento.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-192">A **ShardMapManager** can contain any number of shard maps.</span></span> <span data-ttu-id="4e1b5-193">Enquanto um mapa do fragmento único pode ser suficiente para muitos aplicativos, há vezes quando conjuntos diferentes de bancos de dados são usados para esquemas diferentes ou para fins exclusivos e, nesses casos, vários mapas de fragmentação podem ser preferíveis.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-193">While a single shard map may be sufficient for many applications, there are times when different sets of databases are used for different schema or for unique purposes; in those cases multiple shard maps may be preferable.</span></span> 

<span data-ttu-id="4e1b5-194">Nesse código, um aplicativo tenta tooopen existente **ShardMapManager** com hello [TryGetSqlShardMapManager método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e1b5-194">In this code, an application tries tooopen an existing **ShardMapManager** with hello [TryGetSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span></span>  <span data-ttu-id="4e1b5-195">Se objetos que representam um Global **ShardMapManager** (GSM) ainda não existe no banco de dados de saudação, biblioteca de saudação do cliente cria existe usando Olá [CreateSqlShardMapManager método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e1b5-195">If objects representing a Global **ShardMapManager** (GSM) do not yet exist inside hello database, hello client library creates them there using hello [CreateSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span></span>

    // Try tooget a reference toohello Shard Map Manager 
     // via hello Shard Map Manager database.  
    // If it doesn't already exist, then create it. 
    ShardMapManager shardMapManager; 
    bool shardMapManagerExists = ShardMapManagerFactory.TryGetSqlShardMapManager(
                                        connectionString, 
                                        ShardMapManagerLoadPolicy.Lazy, 
                                        out shardMapManager); 

    if (shardMapManagerExists) 
     { 
        Console.WriteLine("Shard Map Manager already exists");
    } 
    else
    {
        // Create hello Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // hello connectionString contains server name, database name, and admin credentials 
        // for privileges on both hello GSM and hello shards themselves.
    } 

<span data-ttu-id="4e1b5-196">Como alternativa, você pode usar o Powershell toocreate um novo Gerenciador de mapa do fragmento.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-196">As an alternative, you can use Powershell toocreate a new Shard Map Manager.</span></span> <span data-ttu-id="4e1b5-197">Um exemplo está disponível [aqui](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="4e1b5-197">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="get-a-rangeshardmap-or-listshardmap"></a><span data-ttu-id="4e1b5-198">Obter um RangeShardMap ou ListShardMap</span><span class="sxs-lookup"><span data-stu-id="4e1b5-198">Get a RangeShardMap or ListShardMap</span></span>
<span data-ttu-id="4e1b5-199">Depois de criar um fragmento Gerenciador do mapa, você pode obter Olá [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) ou [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) usando Olá [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), Olá [ TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), ou hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) método.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-199">After creating a shard map manager, you can get hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) using hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method.</span></span>

    /// <summary>
    /// Creates a new Range Shard Map with hello specified name, or gets hello Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try tooget a reference toohello Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // hello Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a><span data-ttu-id="4e1b5-200">Credenciais de administração de mapa de fragmentos</span><span class="sxs-lookup"><span data-stu-id="4e1b5-200">Shard map administration credentials</span></span>
<span data-ttu-id="4e1b5-201">Aplicativos que administrarem e manipulam os mapas de fragmento são diferentes daqueles que usam conexões de tooroute de mapas de fragmento hello.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-201">Applications that administer and manipulate shard maps are different from those that use hello shard maps tooroute connections.</span></span> 

<span data-ttu-id="4e1b5-202">mapas de fragmento tooadminister (Adicionar ou alterar os fragmentos, mapas de fragmento, mapeamentos de fragmento, etc.) você deve instanciar Olá **ShardMapManager** usando **leitura/gravação de credenciais que tenham privilégios em ambos os banco de dados GSM hello e em cada banco de dados que serve como um fragmento**.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-202">tooadminister shard maps (add or change shards, shard maps, shard mappings, etc.) you must instantiate hello **ShardMapManager** using **credentials that have read/write privileges on both hello GSM database and on each database that serves as a shard**.</span></span> <span data-ttu-id="4e1b5-203">credenciais de saudação devem permitir gravações nas tabelas de saudação em ambos os Olá GSM e LSM como informações de mapa do fragmento são inseridas ou alteradas, bem como para criar tabelas LSM em novos fragmentos.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-203">hello credentials must allow for writes against hello tables in both hello GSM and LSM as shard map information is entered or changed, as well as for creating LSM tables on new shards.</span></span>  

<span data-ttu-id="4e1b5-204">Consulte [as credenciais usadas biblioteca de cliente de banco de dados Elástico tooaccess Olá](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="4e1b5-204">See [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

### <a name="only-metadata-affected"></a><span data-ttu-id="4e1b5-205">Apenas os metadados afetados</span><span class="sxs-lookup"><span data-stu-id="4e1b5-205">Only metadata affected</span></span>
<span data-ttu-id="4e1b5-206">Métodos usados para popular ou alterando Olá **ShardMapManager** dados não alteram os dados de usuário Olá armazenados em fragmentos Olá próprios.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-206">Methods used for populating or changing hello **ShardMapManager** data do not alter hello user data stored in hello shards themselves.</span></span> <span data-ttu-id="4e1b5-207">Por exemplo, os métodos como **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. afetam Olá fragmento mapa somente metadados.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-207">For example, methods such as **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. affect hello shard map metadata only.</span></span> <span data-ttu-id="4e1b5-208">Não remova, adicionar ou alterar os dados de usuário contidos em fragmentos hello.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-208">They do not remove, add, or alter user data contained in hello shards.</span></span> <span data-ttu-id="4e1b5-209">Em vez disso, esses métodos são projetada toobe usada em conjunto com operações separadas realizar toocreate ou remover bancos de dados reais, ou que você mova as linhas de um fragmento tooanother toorebalance um ambiente fragmentado.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-209">Instead, these methods are designed toobe used in conjunction with separate operations you perform toocreate or remove actual databases, or that move rows from one shard tooanother toorebalance a sharded environment.</span></span>  <span data-ttu-id="4e1b5-210">(Olá **divisão mesclagem** ferramenta incluída com as ferramentas de banco de dados Elástico faz uso dessas APIs junto com orquestrar a movimentação de dados real entre fragmentos.) Consulte [dimensionamento usando a ferramenta Olá direta de divisão de banco de dados Elástico](sql-database-elastic-scale-overview-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="4e1b5-210">(hello **split-merge** tool included with elastic database tools makes use of these APIs along with orchestrating actual data movement between shards.) See [Scaling using hello Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>

## <a name="populating-a-shard-map-example"></a><span data-ttu-id="4e1b5-211">Popular um mapa de fragmentos: exemplo</span><span class="sxs-lookup"><span data-stu-id="4e1b5-211">Populating a shard map example</span></span>
<span data-ttu-id="4e1b5-212">Abaixo está um exemplo de sequência de operações toopopulate um mapa de fragmentos específicos.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-212">An example sequence of operations toopopulate a specific shard map is shown below.</span></span> <span data-ttu-id="4e1b5-213">código de saudação executa estas etapas:</span><span class="sxs-lookup"><span data-stu-id="4e1b5-213">hello code performs these steps:</span></span> 

1. <span data-ttu-id="4e1b5-214">Um novo mapa de fragmento é criado dentro de um Gerenciador de mapa do fragmento.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-214">A new shard map is created within a shard map manager.</span></span> 
2. <span data-ttu-id="4e1b5-215">metadados de saudação para dois fragmentos de diferentes são adicionados toohello mapa do fragmento.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-215">hello metadata for two different shards is added toohello shard map.</span></span> 
3. <span data-ttu-id="4e1b5-216">Uma variedade de mapeamentos de intervalo de chave são adicionados e hello conteúdo geral do mapa do fragmento Olá é exibido.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-216">A variety of key range mappings are added, and hello overall contents of hello shard map are displayed.</span></span> 

<span data-ttu-id="4e1b5-217">código de saudação é gravado para que o método hello pode ser executado novamente, se ocorrer um erro.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-217">hello code is written so that hello method can be rerun if an error occurs.</span></span> <span data-ttu-id="4e1b5-218">Cada solicitação testa se um fragmento ou mapeamento já existe, antes de tentar toocreate-lo.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-218">Each request tests whether a shard or mapping already exists, before attempting toocreate it.</span></span> <span data-ttu-id="4e1b5-219">Olá código assume que os bancos de dados chamado **sample_shard_0**, **sample_shard_1** e **sample_shard_2** já foram criados no servidor de saudação referenciada pela cadeia de caracteres **shardServer**.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-219">hello code assumes that databases named **sample_shard_0**, **sample_shard_1** and **sample_shard_2** have already been created in hello server referenced by string **shardServer**.</span></span> 

    public void CreatePopulatedRangeMap(ShardMapManager smm, string mapName) 
        {            
            RangeShardMap<long> sm = null; 

            // check if shardmap exists and if not, create it 
            if (!smm.TryGetRangeShardMap(mapName, out sm)) 
            { 
                sm = smm.CreateRangeShardMap<long>(mapName); 
            } 

            Shard shard0 = null, shard1=null; 
            // Check if shard exists and if not, 
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetShard(new ShardLocation(
                                     shardServer, 
                                     "sample_shard_0"), 
                                     out shard0)) 
            { 
                Shard0 = sm.CreateShard(new ShardLocation(
                                            shardServer, 
                                            "sample_shard_0")); 
            } 

            if (!sm.TryGetShard(new ShardLocation(
                                    shardServer, 
                                    "sample_shard_1"), 
                                    out shard1)) 
            { 
                Shard1 = sm.CreateShard(new ShardLocation(
                                             shardServer, 
                                            "sample_shard_1"));  
            } 

            RangeMapping<long> rmpg=null; 

            // Check if mapping exists and if not,
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetMappingForKey(0, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                          new RangeMappingCreationInfo<long>
                          (new Range<long>(0, 50), 
                          shard0, 
                          MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(50, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(50, 100), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(100, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long>
                         (new Range<long>(100, 150), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(150, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(150, 200), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(200, out rmpg)) 
            { 
               sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(200, 300), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            // List hello shards and mappings 
            foreach (Shard s in sm.GetShards()
                         .OrderBy(s => s.Location.DataSource)
                         .ThenBy(s => s.Location.Database))
            { 
               Console.WriteLine("shard: "+ s.Location); 
            } 

            foreach (RangeMapping<long> rm in sm.GetMappings()) 
            { 
                Console.WriteLine("range: [" + rm.Value.Low.ToString() + ":" 
                        + rm.Value.High.ToString()+ ")  ==>" +rm.Shard.Location); 
            } 
        } 

<span data-ttu-id="4e1b5-220">Como alternativa você pode usar o PowerShell scripts tooachieve Olá mesmo resultado.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-220">As an alternative you can use PowerShell scripts tooachieve hello same result.</span></span> <span data-ttu-id="4e1b5-221">Alguns dos exemplos do PowerShell de exemplo hello estão disponíveis [aqui](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="4e1b5-221">Some of hello sample PowerShell examples are available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>     

<span data-ttu-id="4e1b5-222">Depois que foram populados mapas de fragmento, aplicativos de acesso de dados podem ser criados ou adaptado toowork com hello mapas.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-222">Once shard maps have been populated, data access applications can be created or adapted toowork with hello maps.</span></span> <span data-ttu-id="4e1b5-223">Popular ou manipulando Olá maps não precisa ocorrer novamente até que **layout de mapa** precisa toochange.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-223">Populating or manipulating hello maps need not occur again until **map layout** needs toochange.</span></span>  

## <a name="data-dependent-routing"></a><span data-ttu-id="4e1b5-224">Roteamento dependente de dados</span><span class="sxs-lookup"><span data-stu-id="4e1b5-224">Data dependent routing</span></span>
<span data-ttu-id="4e1b5-225">Gerenciador do mapa de fragmentos Hello mais será usado em aplicativos que requerem operações de dados específicos de aplicativo do banco de dados conexões tooperform hello.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-225">hello shard map manager will be most used in applications that require database connections tooperform hello app-specific data operations.</span></span> <span data-ttu-id="4e1b5-226">Essas conexões devem ser associadas ao banco de dados correto hello.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-226">Those connections must be associated with hello correct database.</span></span> <span data-ttu-id="4e1b5-227">Isso é conhecido como **Roteamento Dependente de Dados**.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-227">This is known as **Data Dependent Routing**.</span></span> <span data-ttu-id="4e1b5-228">Para esses aplicativos, instanciar um objeto do Gerenciador do mapa de fragmento da fábrica de saudação usando as credenciais que possuem acesso somente leitura no banco de dados do hello GSM.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-228">For these applications, instantiate a shard map manager object from hello factory using credentials that have read-only access on hello GSM database.</span></span> <span data-ttu-id="4e1b5-229">Solicitações individuais para conexões posteriores fornecem as credenciais necessárias para conectar o banco de dados do toohello fragmento apropriado.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-229">Individual requests for later connections supply credentials necessary for connecting toohello appropriate shard database.</span></span>

<span data-ttu-id="4e1b5-230">Observe que esses aplicativos (usando **ShardMapManager** aberta com as credenciais de somente leitura) não é possível fazer alterações toohello mapas ou mapeamentos.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-230">Note that these applications (using **ShardMapManager** opened with read-only credentials) cannot make changes toohello maps or mappings.</span></span> <span data-ttu-id="4e1b5-231">Para essas necessidades, crie aplicativos administrativos específicos ou scripts do PowerShell que fornecem credenciais de privilégios mais altos, conforme discutido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-231">For those needs, create administrative-specific applications or PowerShell scripts that supply higher-privileged credentials as discussed earlier.</span></span> <span data-ttu-id="4e1b5-232">Consulte [as credenciais usadas biblioteca de cliente de banco de dados Elástico tooaccess Olá](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="4e1b5-232">See [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

<span data-ttu-id="4e1b5-233">Para obter mais detalhes, consulte [Roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="4e1b5-233">For more details, see [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> 

## <a name="modifying-a-shard-map"></a><span data-ttu-id="4e1b5-234">Modificar um mapa de fragmentos</span><span class="sxs-lookup"><span data-stu-id="4e1b5-234">Modifying a shard map</span></span>
<span data-ttu-id="4e1b5-235">Um mapa do fragmento pode ser alterado de diferentes maneiras.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-235">A shard map can be changed in different ways.</span></span> <span data-ttu-id="4e1b5-236">Todos os métodos a seguir de saudação modificar Olá metadados descrevendo fragmentos hello e seus mapeamentos, mas eles não modificam dados em fragmentos Olá fisicamente, nem criar ou excluir bancos de dados real hello.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-236">All of hello following methods modify hello metadata describing hello shards and their mappings, but they do not physically modify data within hello shards, nor do they create or delete hello actual databases.</span></span>  <span data-ttu-id="4e1b5-237">Algumas das operações de saudação no mapa do fragmento Olá descrito a seguir podem ser necessário toobe coordenado com ações administrativas que mover fisicamente os dados, ou adicionar e remover bancos de dados que serve como fragmentos.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-237">Some of hello operations on hello shard map described below may need toobe coordinated with administrative actions that physically move data or that add and remove databases serving as shards.</span></span>

<span data-ttu-id="4e1b5-238">Esses métodos funcionam em conjunto como blocos de construção de saudação disponíveis para modificar Olá distribuição geral de dados em seu ambiente de banco de dados fragmentado.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-238">These methods work together as hello building blocks available for modifying hello overall distribution of data in your sharded database environment.</span></span>  

* <span data-ttu-id="4e1b5-239">tooadd ou remover fragmentos: usar  **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)**  e  **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)**  de saudação [Shardmap classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e1b5-239">tooadd or remove shards: use **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** and **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** of hello [Shardmap class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span></span> 
  
    <span data-ttu-id="4e1b5-240">Olá servidor e banco de dados que representa o fragmento de destino Olá já devem existir para tooexecute essas operações.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-240">hello server and database representing hello target shard must already exist for these operations tooexecute.</span></span> <span data-ttu-id="4e1b5-241">Esses métodos não têm qualquer impacto Olá bancos de dados, somente em metadados no mapa do fragmento hello.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-241">These methods do not have any impact on hello databases themselves, only on metadata in hello shard map.</span></span>
* <span data-ttu-id="4e1b5-242">toocreate ou remover pontos ou intervalos que são mapeados toohello fragmentos: usar  **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**,  **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)**  de saudação [RangeShardMapping classe](https://msdn.microsoft.com/library/azure/dn807318.aspx), e  **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)**  de saudação [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span><span class="sxs-lookup"><span data-stu-id="4e1b5-242">toocreate or remove points or ranges that are mapped toohello shards: use **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**, **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** of hello [RangeShardMapping class](https://msdn.microsoft.com/library/azure/dn807318.aspx), and **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** of hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span></span>
  
    <span data-ttu-id="4e1b5-243">Muitos pontos diferentes ou intervalos podem ser mapeada toohello mesmo fragmento.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-243">Many different points or ranges can be mapped toohello same shard.</span></span> <span data-ttu-id="4e1b5-244">Esses métodos afetam somente metadados – eles não afetam os dados que podem já estar presentes em fragmentos.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-244">These methods only affect metadata - they do not affect any data that may already be present in shards.</span></span> <span data-ttu-id="4e1b5-245">Se é necessário toobe removido do banco de dados de saudação em ordem toobe consistente com dados **DeleteMapping** operações, você precisará tooperform essas operações separadamente, mas em conjunto com o uso desses métodos.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-245">If data needs toobe removed from hello database in order toobe consistent with **DeleteMapping** operations, you will need tooperform those operations separately but in conjunction with using these methods.</span></span>  
* <span data-ttu-id="4e1b5-246">intervalos de toosplit existentes em dois ou intervalos adjacentes de mesclagem em uma: usar  **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)**  e  **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-246">toosplit existing ranges into two, or merge adjacent ranges into one: use **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** and **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span></span>  
  
    <span data-ttu-id="4e1b5-247">Observe que a divisão e mesclagem operações **não altere a chave de toowhich de fragmento Olá valores são mapeados**.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-247">Note that split and merge operations **do not change hello shard toowhich key values are mapped**.</span></span> <span data-ttu-id="4e1b5-248">Uma divisão divide um intervalo existente em duas partes, mas deixa como toohello mapeada mesmo fragmento.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-248">A split breaks an existing range into two parts, but leaves both as mapped toohello same shard.</span></span> <span data-ttu-id="4e1b5-249">Uma mesclagem opera em dois intervalos adjacentes que já estão mapeada toohello mesmo fragmento, união-los em um único intervalo.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-249">A merge operates on two adjacent ranges that are already mapped toohello same shard, coalescing them into a single range.</span></span>  <span data-ttu-id="4e1b5-250">movimentação de pontos ou intervalos próprios entre fragmentos Hello precisa toobe coordenada usando **UpdateMapping** em conjunto com a movimentação de dados real.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-250">hello movement of points or ranges themselves between shards needs toobe coordinated by using **UpdateMapping** in conjunction with actual data movement.</span></span>  <span data-ttu-id="4e1b5-251">Você pode usar o hello **divisão/mesclagem** ferramentas de serviço que faz parte do banco de dados Elástico toocoordinate alterações no mapa de fragmentos com movimentação de dados, quando a movimentação é necessária.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-251">You can use hello **Split/Merge** service that is part of elastic database tools toocoordinate shard map changes with data movement, when movement is needed.</span></span> 
* <span data-ttu-id="4e1b5-252">mapa de toore (ou mover) pontos ou intervalos toodifferent fragmentos individuais: usar  **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-252">toore-map (or move) individual points or ranges toodifferent shards: use **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span></span>  
  
    <span data-ttu-id="4e1b5-253">Desde que os dados podem ter toobe movido de um fragmento tooanother em ordem toobe consistente com **UpdateMapping** operações, você precisará tooperform essa movimentação separadamente, mas em conjunto com o uso desses métodos.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-253">Since data may need toobe moved from one shard tooanother in order toobe consistent with **UpdateMapping** operations, you will need tooperform that movement separately but in conjunction with using these methods.</span></span>
* <span data-ttu-id="4e1b5-254">mapeamentos de tootake online e offline: usar  **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)**  e  **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**  toocontrol Olá estado online de um mapeamento.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-254">tootake mappings online and offline: use **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** and **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** toocontrol hello online state of a mapping.</span></span> 
  
    <span data-ttu-id="4e1b5-255">Algumas operações nos mapeamentos de fragmentos são permitidas apenas quando um mapeamento está em um estado “offline”, incluindo **UpdateMapping** e **DeleteMapping**.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-255">Certain operations on shard mappings are only allowed when a mapping is in an “offline” state, including **UpdateMapping** and **DeleteMapping**.</span></span> <span data-ttu-id="4e1b5-256">Quando um mapeamento estiver offline, uma solicitação dependente de dados com base em uma chave incluída nesse mapeamento retornará um erro.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-256">When a mapping is offline, a data-dependent request based on a key included in that mapping will return an error.</span></span> <span data-ttu-id="4e1b5-257">Além disso, quando um intervalo primeiro é colocado offline, todos os fragmentos de toohello afetado conexões serão eliminados automaticamente nos resultados de inconsistente ou incompleta de tooprevent de ordem para consultas direcionadas a intervalos que está sendo alterados.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-257">In addition, when a range is first taken offline, all connections toohello affected shard are automatically killed in order tooprevent inconsistent or incomplete results for queries directed against ranges being changed.</span></span> 

<span data-ttu-id="4e1b5-258">Mapeamentos são objetos imutáveis no .Net.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-258">Mappings are immutable objects in .Net.</span></span>  <span data-ttu-id="4e1b5-259">Todos os métodos de saudação acima que alterar os mapeamentos de invalidam também qualquer toothem referências no seu código.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-259">All of hello methods above that change mappings also invalidate any references toothem in your code.</span></span> <span data-ttu-id="4e1b5-260">toomake it sequências de tooperform mais fácil de operações que alteram o estado do mapeamento, todos os métodos de saudação que alterar um mapeamento de retornam um novo mapeamento de referência, para que as operações podem ser encadeadas.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-260">toomake it easier tooperform sequences of operations that change a mapping’s state, all of hello methods that change a mapping return a new mapping reference, so operations can be chained.</span></span> <span data-ttu-id="4e1b5-261">Por exemplo, toodelete um mapeamento no sm shardmap que contém a chave de saudação 25 existente, você pode executar Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e1b5-261">For example, toodelete an existing mapping in shardmap sm that contains hello key 25, you can execute hello following:</span></span> 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a><span data-ttu-id="4e1b5-262">Adicionar um fragmento</span><span class="sxs-lookup"><span data-stu-id="4e1b5-262">Adding a shard</span></span>
<span data-ttu-id="4e1b5-263">Aplicativos geralmente precisa toosimply adicionar novos fragmentos toohandle dados que são esperados de novas chaves ou intervalos de chaves para um mapa do fragmento que já existe.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-263">Applications often need toosimply add new shards toohandle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="4e1b5-264">Por exemplo, um aplicativo fragmentado por ID de locatário pode ser necessário tooprovision um novo fragmento para um novo locatário ou mensal de dados fragmentados talvez seja necessário um novo fragmento provisionado antes do início da saudação de cada novo mês.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-264">For example, an application sharded by Tenant ID may need tooprovision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before hello start of each new month.</span></span> 

<span data-ttu-id="4e1b5-265">Se o novo intervalo de valores de chave de Olá não ainda estiver parte de um mapeamento existente e nenhuma movimentação de dados é necessária, o que é novo fragmento saudação do tooadd muito simples e associar a nova chave de saudação ou fragmento de toothat do intervalo.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-265">If hello new range of key values is not already part of an existing mapping and no data movement is necessary, it is very simple tooadd hello new shard and associate hello new key or range toothat shard.</span></span> <span data-ttu-id="4e1b5-266">Para obter detalhes sobre como adicionar novos fragmentos, veja [Adicionar um novo fragmento](sql-database-elastic-scale-add-a-shard.md).</span><span class="sxs-lookup"><span data-stu-id="4e1b5-266">For details on adding new shards, see [Adding a new shard](sql-database-elastic-scale-add-a-shard.md).</span></span>

<span data-ttu-id="4e1b5-267">No entanto, para cenários que exigem a movimentação de dados, ferramenta de mesclagem de divisão de saudação é tooorchestrate necessário Olá a movimentação de dados entre fragmentos em combinação com atualizações de mapa de fragmento necessários hello.</span><span class="sxs-lookup"><span data-stu-id="4e1b5-267">For scenarios that require data movement, however, hello split-merge tool is needed tooorchestrate hello data movement between shards in combination with hello necessary shard map updates.</span></span> <span data-ttu-id="4e1b5-268">Para obter detalhes sobre como usar o hello yool de divisão de mesclagem, consulte [visão geral da divisão de mesclagem](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="4e1b5-268">For details on using hello split-merge yool, see [Overview of split-merge](sql-database-elastic-scale-overview-split-and-merge.md)</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
