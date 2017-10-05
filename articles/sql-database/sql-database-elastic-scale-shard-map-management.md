---
title: Escalar horizontalmente um banco de dados SQL do Azure | Microsoft Docs
description: "Como usar o ShardMapManager, a biblioteca de cliente do banco de dados elástico"
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
ms.openlocfilehash: f626cf417d8b3f1761f3c900d49039b3ff83b093
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-out-databases-with-the-shard-map-manager"></a><span data-ttu-id="51567-103">Escale horizontalmente os bancos de dados com o gerenciador do mapa de fragmentos</span><span class="sxs-lookup"><span data-stu-id="51567-103">Scale out databases with the shard map manager</span></span>
<span data-ttu-id="51567-104">Para escalar horizontalmente os bancos de dados no SQL Azure, use um gerenciador do mapa de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="51567-104">To easily scale out databases on SQL Azure, use a shard map manager.</span></span> <span data-ttu-id="51567-105">O gerenciador do mapa de fragmentos é um banco de dados especial que mantém informações de mapeamento global sobre todos os fragmentos (bancos de dados) em um conjunto de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="51567-105">The shard map manager is a special database that maintains global mapping information about all shards (databases) in a shard set.</span></span> <span data-ttu-id="51567-106">Os metadados permitem que um aplicativo se conecte ao banco de dados correto com base no valor da **chave de fragmentação**.</span><span class="sxs-lookup"><span data-stu-id="51567-106">The metadata allows an application to connect to the correct database based upon the value of the **sharding key**.</span></span> <span data-ttu-id="51567-107">Além disso, cada fragmento no conjunto contém mapas que acompanham os dados de fragmento local (conhecido como **shardlets**).</span><span class="sxs-lookup"><span data-stu-id="51567-107">In addition, every shard in the set contains maps that track the local shard data (known as **shardlets**).</span></span> 

![Gerenciamento de mapa de fragmentos](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

<span data-ttu-id="51567-109">Entender como esses mapas são construídos é essencial para o gerenciamento de mapa de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="51567-109">Understanding how these maps are constructed is essential to shard map management.</span></span> <span data-ttu-id="51567-110">Isso é feito usando a [classe ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), localizada na [biblioteca de cliente do Banco de Dados Elástico](sql-database-elastic-database-client-library.md) para gerenciar mapas de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="51567-110">This is done using the [ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), found in the [Elastic Database client library](sql-database-elastic-database-client-library.md) to manage shard maps.</span></span>  

## <a name="shard-maps-and-shard-mappings"></a><span data-ttu-id="51567-111">Mapas de fragmentos e mapeamentos de fragmentos</span><span class="sxs-lookup"><span data-stu-id="51567-111">Shard maps and shard mappings</span></span>
<span data-ttu-id="51567-112">Para cada fragmento, você deve selecionar o tipo do mapa de fragmentos a ser criado.</span><span class="sxs-lookup"><span data-stu-id="51567-112">For each shard, you must select the type of shard map to create.</span></span> <span data-ttu-id="51567-113">A escolha depende da arquitetura do banco de dados:</span><span class="sxs-lookup"><span data-stu-id="51567-113">The choice depends on the database architecture:</span></span> 

1. <span data-ttu-id="51567-114">Um locatário único por banco de dados</span><span class="sxs-lookup"><span data-stu-id="51567-114">Single tenant per database</span></span>  
2. <span data-ttu-id="51567-115">Vários locatários por banco de dados (dois tipos):</span><span class="sxs-lookup"><span data-stu-id="51567-115">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="51567-116">Mapeamento de lista</span><span class="sxs-lookup"><span data-stu-id="51567-116">List mapping</span></span>
   2. <span data-ttu-id="51567-117">Mapeamento de intervalo</span><span class="sxs-lookup"><span data-stu-id="51567-117">Range mapping</span></span>

<span data-ttu-id="51567-118">Para um modelo de locatário único, crie um mapa de fragmentos de **mapeamento de lista** .</span><span class="sxs-lookup"><span data-stu-id="51567-118">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="51567-119">O modelo de locatário único atribui um banco de dados por locatário.</span><span class="sxs-lookup"><span data-stu-id="51567-119">The single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="51567-120">Esse é um modelo eficaz para desenvolvedores de SaaS, pois simplifica o gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="51567-120">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Mapeamento de lista][1]

<span data-ttu-id="51567-122">O modelo multilocatário atribui vários locatários a um banco de dados individual (e você pode distribuir grupos de locatários entre vários bancos de dados).</span><span class="sxs-lookup"><span data-stu-id="51567-122">The multi-tenant model assigns several tenants to a single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="51567-123">Use esse modelo quando você esperar que cada locatário tenha necessidades de dados pequenas.</span><span class="sxs-lookup"><span data-stu-id="51567-123">Use this model when you expect each tenant to have small data needs.</span></span> <span data-ttu-id="51567-124">Nesse modelo, atribuímos um intervalo de locatários a um banco de dados usando **mapeamento de intervalo**.</span><span class="sxs-lookup"><span data-stu-id="51567-124">In this model, we assign a range of tenants to a database using **range mapping**.</span></span> 

![Mapeamento de intervalo][2]

<span data-ttu-id="51567-126">Ou então, você pode implementar um modelo de banco de dados multilocatário usando um *mapeamento de lista* para atribuir vários locatários a um banco de dados individual.</span><span class="sxs-lookup"><span data-stu-id="51567-126">Or you can implement a multi-tenant database model using a *list mapping* to assign multiple tenants to a single database.</span></span> <span data-ttu-id="51567-127">Por exemplo, DB1 é usado para armazenar informações sobre os locatários com IDs 1 e 5, e DB2 armazena dados dos locatários 7 e 10.</span><span class="sxs-lookup"><span data-stu-id="51567-127">For example, DB1 is used to store information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Vários locatários em um banco de dados individual][3] 

### <a name="supported-net-types-for-sharding-keys"></a><span data-ttu-id="51567-129">Tipos .Net com suporte para chaves de fragmentação</span><span class="sxs-lookup"><span data-stu-id="51567-129">Supported .Net types for sharding keys</span></span>
<span data-ttu-id="51567-130">A Escala Elástica dá suporte aos seguintes tipos de .Net Framework como chaves de fragmentação:</span><span class="sxs-lookup"><span data-stu-id="51567-130">Elastic Scale support the following .Net Framework types as sharding keys:</span></span>

* <span data-ttu-id="51567-131">inteiro</span><span class="sxs-lookup"><span data-stu-id="51567-131">integer</span></span>
* <span data-ttu-id="51567-132">longo</span><span class="sxs-lookup"><span data-stu-id="51567-132">long</span></span>
* <span data-ttu-id="51567-133">guid</span><span class="sxs-lookup"><span data-stu-id="51567-133">guid</span></span>
* <span data-ttu-id="51567-134">byte[]</span><span class="sxs-lookup"><span data-stu-id="51567-134">byte[]</span></span>  
* <span data-ttu-id="51567-135">datetime</span><span class="sxs-lookup"><span data-stu-id="51567-135">datetime</span></span>
* <span data-ttu-id="51567-136">timespan</span><span class="sxs-lookup"><span data-stu-id="51567-136">timespan</span></span>
* <span data-ttu-id="51567-137">datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="51567-137">datetimeoffset</span></span>

### <a name="list-and-range-shard-maps"></a><span data-ttu-id="51567-138">Mapas de fragmentos de lista e intervalo</span><span class="sxs-lookup"><span data-stu-id="51567-138">List and range shard maps</span></span>
<span data-ttu-id="51567-139">Mapas de fragmentos podem ser construídos usando **listas de valores de chave de fragmentação individuais** ou **intervalos de valores de chave de fragmentação**.</span><span class="sxs-lookup"><span data-stu-id="51567-139">Shard maps can be constructed using **lists of individual sharding key values**, or they can be constructed using **ranges of sharding key values**.</span></span> 

### <a name="list-shard-maps"></a><span data-ttu-id="51567-140">Mapas de fragmentos de lista</span><span class="sxs-lookup"><span data-stu-id="51567-140">List shard maps</span></span>
<span data-ttu-id="51567-141">**Fragmentos** contêm **shardlets** e o mapeamento de shardlets para fragmentos é mantido por um mapa de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="51567-141">**Shards** contain **shardlets** and the mapping of shardlets to shards is maintained by a shard map.</span></span> <span data-ttu-id="51567-142">Uma **lista de mapas de fragmento** é uma associação entre os valores de chave individuais, que identificam os shardlets e os bancos de dados que servem como fragmentos.</span><span class="sxs-lookup"><span data-stu-id="51567-142">A **list shard map** is an association between the individual key values that identify the shardlets and the databases that serve as shards.</span></span>  <span data-ttu-id="51567-143">**Mapeamentos de lista** são valores de chaves explícitos e diferentes que podem ser mapeados para o mesmo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="51567-143">**List mappings** are explicit and different key values can be mapped to the same database.</span></span> <span data-ttu-id="51567-144">Por exemplo, a chave 1 é mapeada para o banco de dados A e os valores 3 e 6 fazem referência ao banco de dados B.</span><span class="sxs-lookup"><span data-stu-id="51567-144">For example, key 1 maps to Database A, and key values 3 and 6 both reference Database B.</span></span>

| <span data-ttu-id="51567-145">Chave</span><span class="sxs-lookup"><span data-stu-id="51567-145">Key</span></span> | <span data-ttu-id="51567-146">Local de fragmento</span><span class="sxs-lookup"><span data-stu-id="51567-146">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="51567-147">1</span><span class="sxs-lookup"><span data-stu-id="51567-147">1</span></span> |<span data-ttu-id="51567-148">Database_A</span><span class="sxs-lookup"><span data-stu-id="51567-148">Database_A</span></span> |
| <span data-ttu-id="51567-149">3</span><span class="sxs-lookup"><span data-stu-id="51567-149">3</span></span> |<span data-ttu-id="51567-150">Database_B</span><span class="sxs-lookup"><span data-stu-id="51567-150">Database_B</span></span> |
| <span data-ttu-id="51567-151">4</span><span class="sxs-lookup"><span data-stu-id="51567-151">4</span></span> |<span data-ttu-id="51567-152">Database_C</span><span class="sxs-lookup"><span data-stu-id="51567-152">Database_C</span></span> |
| <span data-ttu-id="51567-153">6</span><span class="sxs-lookup"><span data-stu-id="51567-153">6</span></span> |<span data-ttu-id="51567-154">Database_B</span><span class="sxs-lookup"><span data-stu-id="51567-154">Database_B</span></span> |
| <span data-ttu-id="51567-155">...</span><span class="sxs-lookup"><span data-stu-id="51567-155">...</span></span> |<span data-ttu-id="51567-156">...</span><span class="sxs-lookup"><span data-stu-id="51567-156">...</span></span> |

### <a name="range-shard-maps"></a><span data-ttu-id="51567-157">Mapas de fragmentos de intervalo</span><span class="sxs-lookup"><span data-stu-id="51567-157">Range shard maps</span></span>
<span data-ttu-id="51567-158">Em um **intervalo de mapas de fragmentos**, o intervalo de chaves é descrito por um par **[Valor baixo, Valor alto)**, em que o *Valor baixo* é a chave mínima no intervalo e o *Valor alto* é o primeiro valor maior que o intervalo.</span><span class="sxs-lookup"><span data-stu-id="51567-158">In a **range shard map**, the key range is described by a pair **[Low Value, High Value)** where the *Low Value* is the minimum key in the range, and the *High Value* is the first value higher than the range.</span></span> 

<span data-ttu-id="51567-159">Por exemplo, **(0, 100)** inclui todos os números inteiros iguais ou maiores que 0 e menores que 100.</span><span class="sxs-lookup"><span data-stu-id="51567-159">For example, **[0, 100)** includes all integers greater than or equal 0 and less than 100.</span></span> <span data-ttu-id="51567-160">Observe que vários intervalos podem apontar para o mesmo banco de dados e intervalos separados tem suporte (por exemplo, ambos [100,200) e [400,600) apontam para o banco de dados C no exemplo abaixo.)</span><span class="sxs-lookup"><span data-stu-id="51567-160">Note that multiple ranges can point to the same database, and disjoint ranges are supported (e.g., [100,200) and [400,600) both point to Database C in the example below.)</span></span>

| <span data-ttu-id="51567-161">Chave</span><span class="sxs-lookup"><span data-stu-id="51567-161">Key</span></span> | <span data-ttu-id="51567-162">Local de fragmento</span><span class="sxs-lookup"><span data-stu-id="51567-162">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="51567-163">[1,50)</span><span class="sxs-lookup"><span data-stu-id="51567-163">[1,50)</span></span> |<span data-ttu-id="51567-164">Database_A</span><span class="sxs-lookup"><span data-stu-id="51567-164">Database_A</span></span> |
| <span data-ttu-id="51567-165">[50,100)</span><span class="sxs-lookup"><span data-stu-id="51567-165">[50,100)</span></span> |<span data-ttu-id="51567-166">Database_B</span><span class="sxs-lookup"><span data-stu-id="51567-166">Database_B</span></span> |
| <span data-ttu-id="51567-167">[100,200)</span><span class="sxs-lookup"><span data-stu-id="51567-167">[100,200)</span></span> |<span data-ttu-id="51567-168">Database_C</span><span class="sxs-lookup"><span data-stu-id="51567-168">Database_C</span></span> |
| <span data-ttu-id="51567-169">[400,600)</span><span class="sxs-lookup"><span data-stu-id="51567-169">[400,600)</span></span> |<span data-ttu-id="51567-170">Database_C</span><span class="sxs-lookup"><span data-stu-id="51567-170">Database_C</span></span> |
| <span data-ttu-id="51567-171">...</span><span class="sxs-lookup"><span data-stu-id="51567-171">...</span></span> |<span data-ttu-id="51567-172">...</span><span class="sxs-lookup"><span data-stu-id="51567-172">...</span></span> |

<span data-ttu-id="51567-173">Cada uma das tabelas mostradas acima é um exemplo conceitual de um objeto **ShardMap** .</span><span class="sxs-lookup"><span data-stu-id="51567-173">Each of the tables shown above is a conceptual example of a **ShardMap** object.</span></span> <span data-ttu-id="51567-174">Cada linha é um exemplo simplificado de um objeto de **PointMapping** individual (para o mapa do fragmento de lista) ou **RangeMapping** (para o mapa do fragmento de mapa).</span><span class="sxs-lookup"><span data-stu-id="51567-174">Each row is a simplified example of an individual **PointMapping** (for the list shard map) or **RangeMapping** (for the range shard map) object.</span></span>

## <a name="shard-map-manager"></a><span data-ttu-id="51567-175">Gerenciador de mapa de fragmentos</span><span class="sxs-lookup"><span data-stu-id="51567-175">Shard map manager</span></span>
<span data-ttu-id="51567-176">Na biblioteca do cliente, o gerenciador de mapa de fragmentos é uma coleção de mapas de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="51567-176">In the client library, the shard map  manager is a collection of shard maps.</span></span> <span data-ttu-id="51567-177">Os dados gerenciados por uma instância **ShardMapManager** são mantidos em três locais:</span><span class="sxs-lookup"><span data-stu-id="51567-177">The data managed by a **ShardMapManager** instance is kept in three places:</span></span> 

1. <span data-ttu-id="51567-178">**GSM (Mapa de Fragmentos Global)**: você especifica um banco de dados para servir como o repositório para todos os seus mapas de fragmento e mapeamentos.</span><span class="sxs-lookup"><span data-stu-id="51567-178">**Global Shard Map (GSM)**: You specify a database to serve as the repository for all of its shard maps and mappings.</span></span> <span data-ttu-id="51567-179">Procedimentos armazenados e tabelas especiais são criados automaticamente para gerenciar as informações.</span><span class="sxs-lookup"><span data-stu-id="51567-179">Special tables and stored procedures are automatically created to manage the information.</span></span> <span data-ttu-id="51567-180">Geralmente trata-se de um banco de dados pequeno e pouco acessado, que não deve ser usado para outras necessidades do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="51567-180">This is typically a small database and lightly accessed, and it should not be used for other needs of the application.</span></span> <span data-ttu-id="51567-181">As tabelas estão em um esquema especial chamado **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="51567-181">The tables are in a special schema named **__ShardManagement**.</span></span> 
2. <span data-ttu-id="51567-182">**LSM (Mapa de Fragmentos Local)**: cada banco de dados que você especificar para ser um fragmento é modificado para conter várias pequenas tabelas e procedimentos especiais armazenados que contêm e gerenciem informações de mapa de fragmentos específicas a esse fragmento.</span><span class="sxs-lookup"><span data-stu-id="51567-182">**Local Shard Map (LSM)**: Every database that you specify to be a shard is modified to contain several small tables and special stored procedures that contain and manage shard map information specific to that shard.</span></span> <span data-ttu-id="51567-183">Essas informações são redundantes com as informações de GSM e permitem que o aplicativo validar informações de mapa do fragmento em cache sem colocar nenhuma carga no GSM. O aplicativo usa o LSM para determinar se um mapeamento em cache ainda é válido.</span><span class="sxs-lookup"><span data-stu-id="51567-183">This information is redundant with the information in the GSM, and it allows the application to validate cached shard map information without placing any load on the GSM; the application uses the LSM to determine if a cached mapping is still valid.</span></span> <span data-ttu-id="51567-184">As tabelas correspondentes ao LSM em cada fragmento também estão no esquema **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="51567-184">The tables corresponding to the LSM on each shard are also in the schema **__ShardManagement**.</span></span>
3. <span data-ttu-id="51567-185">**Cache do aplicativo**: cada instância do aplicativo que acessa um objeto **ShardMapManager** mantém um cache na memória local dos seus mapeamentos.</span><span class="sxs-lookup"><span data-stu-id="51567-185">**Application cache**: Each application instance accessing a **ShardMapManager** object maintains a local in-memory cache of its mappings.</span></span> <span data-ttu-id="51567-186">Ele armazena informações de roteamento que recentemente foi recuperadas.</span><span class="sxs-lookup"><span data-stu-id="51567-186">It stores routing information that has recently been retrieved.</span></span> 

## <a name="constructing-a-shardmapmanager"></a><span data-ttu-id="51567-187">Construindo um ShardMapManager</span><span class="sxs-lookup"><span data-stu-id="51567-187">Constructing a ShardMapManager</span></span>
<span data-ttu-id="51567-188">Um objeto **ShardMapManager** é construído usando um padrão [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) .</span><span class="sxs-lookup"><span data-stu-id="51567-188">A **ShardMapManager** object is constructed using a [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) pattern.</span></span> <span data-ttu-id="51567-189">O método **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** usa credenciais (incluindo o nome do servidor e o nome do banco de dados que contém o GSM) na forma de uma **ConnectionString** e retorna uma instância de um **ShardMapManager**.</span><span class="sxs-lookup"><span data-stu-id="51567-189">The **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** method takes credentials (including the server name and database name holding the GSM) in the form of a **ConnectionString** and returns an instance of a **ShardMapManager**.</span></span>  

<span data-ttu-id="51567-190">**Observação:** o **ShardMapManager** deve ser instanciado apenas uma vez por domínio de aplicativo, dentro do código de inicialização de um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="51567-190">**Please Note:** The **ShardMapManager** should be instantiated only once per app domain, within the initialization code for an application.</span></span> <span data-ttu-id="51567-191">A criação de instâncias adicionais de ShardMapManager no mesmo domínio de aplicativo resultará em uma maior utilização de memória e CPU do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="51567-191">Creation of additional instances of ShardMapManager in the same appdomain, will result in increased memory and CPU utilization of the application.</span></span> <span data-ttu-id="51567-192">Um **ShardMapManager** pode conter diversos mapas de fragmento.</span><span class="sxs-lookup"><span data-stu-id="51567-192">A **ShardMapManager** can contain any number of shard maps.</span></span> <span data-ttu-id="51567-193">Enquanto um mapa do fragmento único pode ser suficiente para muitos aplicativos, há vezes quando conjuntos diferentes de bancos de dados são usados para esquemas diferentes ou para fins exclusivos e, nesses casos, vários mapas de fragmentação podem ser preferíveis.</span><span class="sxs-lookup"><span data-stu-id="51567-193">While a single shard map may be sufficient for many applications, there are times when different sets of databases are used for different schema or for unique purposes; in those cases multiple shard maps may be preferable.</span></span> 

<span data-ttu-id="51567-194">Nesse código, um aplicativo tenta abrir um **ShardMapManager** existente com o [método TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="51567-194">In this code, an application tries to open an existing **ShardMapManager** with the [TryGetSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span></span>  <span data-ttu-id="51567-195">Se os objetos que representam um **ShardMapManager** Global (GSM) ainda não existirem no banco de dados, a biblioteca de cliente os criará no local usando o [método CreateSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="51567-195">If objects representing a Global **ShardMapManager** (GSM) do not yet exist inside the database, the client library creates them there using the [CreateSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span></span>

    // Try to get a reference to the Shard Map Manager 
     // via the Shard Map Manager database.  
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
        // Create the Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // The connectionString contains server name, database name, and admin credentials 
        // for privileges on both the GSM and the shards themselves.
    } 

<span data-ttu-id="51567-196">Como alternativa, é possível usar o Powershell para criar um novo Gerenciador de Mapa de Fragmentos.</span><span class="sxs-lookup"><span data-stu-id="51567-196">As an alternative, you can use Powershell to create a new Shard Map Manager.</span></span> <span data-ttu-id="51567-197">Um exemplo está disponível [aqui](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="51567-197">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="get-a-rangeshardmap-or-listshardmap"></a><span data-ttu-id="51567-198">Obter um RangeShardMap ou ListShardMap</span><span class="sxs-lookup"><span data-stu-id="51567-198">Get a RangeShardMap or ListShardMap</span></span>
<span data-ttu-id="51567-199">Após criar um gerenciador de mapa de fragmentos, você pode obter o [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) ou [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) usando o método [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx) ou [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx).</span><span class="sxs-lookup"><span data-stu-id="51567-199">After creating a shard map manager, you can get the [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) using the [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), the [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or the [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method.</span></span>

    /// <summary>
    /// Creates a new Range Shard Map with the specified name, or gets the Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try to get a reference to the Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // The Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a><span data-ttu-id="51567-200">Credenciais de administração de mapa de fragmentos</span><span class="sxs-lookup"><span data-stu-id="51567-200">Shard map administration credentials</span></span>
<span data-ttu-id="51567-201">Os aplicativos que administram e manipulam mapas de fragmentos são diferentes daqueles que utilizam os mapas de fragmentos para encaminhar conexões.</span><span class="sxs-lookup"><span data-stu-id="51567-201">Applications that administer and manipulate shard maps are different from those that use the shard maps to route connections.</span></span> 

<span data-ttu-id="51567-202">Para administrar mapas de fragmentos (adicionar ou alterar fragmentos, mapas de fragmentos, mapeamentos de fragmentos etc.), é necessário criar uma instância do **ShardMapManager** usando as **credenciais que têm privilégios de leitura/gravação no banco de dados do GSM e em cada banco de dados que atua como um fragmento**.</span><span class="sxs-lookup"><span data-stu-id="51567-202">To administer shard maps (add or change shards, shard maps, shard mappings, etc.) you must instantiate the **ShardMapManager** using **credentials that have read/write privileges on both the GSM database and on each database that serves as a shard**.</span></span> <span data-ttu-id="51567-203">As credenciais devem permitir gravações nas tabelas no GSM e LSM como informações de mapa do fragmento são inseridas ou alteradas, bem como para criar tabelas LSM em novos fragmentos.</span><span class="sxs-lookup"><span data-stu-id="51567-203">The credentials must allow for writes against the tables in both the GSM and LSM as shard map information is entered or changed, as well as for creating LSM tables on new shards.</span></span>  

<span data-ttu-id="51567-204">Veja [Credenciais usadas para acessar a biblioteca de cliente do Banco de Dados Elástico](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="51567-204">See [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

### <a name="only-metadata-affected"></a><span data-ttu-id="51567-205">Apenas os metadados afetados</span><span class="sxs-lookup"><span data-stu-id="51567-205">Only metadata affected</span></span>
<span data-ttu-id="51567-206">Os métodos usados para preencher ou alterar os dados de **ShardMapManager** não alteram os dados de usuário armazenados nos próprios fragmentos.</span><span class="sxs-lookup"><span data-stu-id="51567-206">Methods used for populating or changing the **ShardMapManager** data do not alter the user data stored in the shards themselves.</span></span> <span data-ttu-id="51567-207">Por exemplo, métodos como **CreateShard**, **DeleteShard**, **UpdateMapping** etc., afetam apenas os metadados do mapa de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="51567-207">For example, methods such as **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. affect the shard map metadata only.</span></span> <span data-ttu-id="51567-208">Não remova, adicione ou altere dados de usuário contidos nos fragmentos.</span><span class="sxs-lookup"><span data-stu-id="51567-208">They do not remove, add, or alter user data contained in the shards.</span></span> <span data-ttu-id="51567-209">Em vez disso, esses métodos destinam-se a ser usado em conjunto com operações separadas, que você pode executar para criar ou remover bancos de dados real ou que move linhas de um fragmento para outro para reequilibrar um ambiente fragmentado.</span><span class="sxs-lookup"><span data-stu-id="51567-209">Instead, these methods are designed to be used in conjunction with separate operations you perform to create or remove actual databases, or that move rows from one shard to another to rebalance a sharded environment.</span></span>  <span data-ttu-id="51567-210">(A ferramenta de **divisão e mesclagem** incluída com as ferramentas de banco de dados elástico usa essas APIs, além de orquestrar a movimentação de dados real entre fragmentos.) Veja [Escalando com a ferramenta de divisão e mesclagem de Banco de Dados Elástico](sql-database-elastic-scale-overview-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="51567-210">(The **split-merge** tool included with elastic database tools makes use of these APIs along with orchestrating actual data movement between shards.) See [Scaling using the Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>

## <a name="populating-a-shard-map-example"></a><span data-ttu-id="51567-211">Popular um mapa de fragmentos: exemplo</span><span class="sxs-lookup"><span data-stu-id="51567-211">Populating a shard map example</span></span>
<span data-ttu-id="51567-212">Uma sequência de operações para preencher um mapa de fragmento específicos exemplo é mostrada abaixo.</span><span class="sxs-lookup"><span data-stu-id="51567-212">An example sequence of operations to populate a specific shard map is shown below.</span></span> <span data-ttu-id="51567-213">O código executa estas etapas:</span><span class="sxs-lookup"><span data-stu-id="51567-213">The code performs these steps:</span></span> 

1. <span data-ttu-id="51567-214">Um novo mapa de fragmento é criado dentro de um Gerenciador de mapa do fragmento.</span><span class="sxs-lookup"><span data-stu-id="51567-214">A new shard map is created within a shard map manager.</span></span> 
2. <span data-ttu-id="51567-215">Os metadados para dois fragmentos diferentes é adicionado ao mapa de fragmento.</span><span class="sxs-lookup"><span data-stu-id="51567-215">The metadata for two different shards is added to the shard map.</span></span> 
3. <span data-ttu-id="51567-216">Uma variedade de mapeamentos de intervalo de chave são adicionados e o conteúdo geral do mapa do fragmento é exibido.</span><span class="sxs-lookup"><span data-stu-id="51567-216">A variety of key range mappings are added, and the overall contents of the shard map are displayed.</span></span> 

<span data-ttu-id="51567-217">O código é escrito para que o método possa ser executado novamente caso ocorra um erro.</span><span class="sxs-lookup"><span data-stu-id="51567-217">The code is written so that the method can be rerun if an error occurs.</span></span> <span data-ttu-id="51567-218">Cada solicitação testa se um fragmento ou mapeamento já existe antes de tentar criá-lo.</span><span class="sxs-lookup"><span data-stu-id="51567-218">Each request tests whether a shard or mapping already exists, before attempting to create it.</span></span> <span data-ttu-id="51567-219">O código pressupõe que bancos de dados chamados **sample_shard_0**, **sample_shard_1** e **sample_shard_2** já foram criados no servidor referenciado pela cadeia de caracteres **shardServer**.</span><span class="sxs-lookup"><span data-stu-id="51567-219">The code assumes that databases named **sample_shard_0**, **sample_shard_1** and **sample_shard_2** have already been created in the server referenced by string **shardServer**.</span></span> 

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

            // List the shards and mappings 
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

<span data-ttu-id="51567-220">Como alternativa, você pode usar scripts do PowerShell para alcançar o mesmo resultado.</span><span class="sxs-lookup"><span data-stu-id="51567-220">As an alternative you can use PowerShell scripts to achieve the same result.</span></span> <span data-ttu-id="51567-221">Alguns dos exemplos do PowerShell de exemplo estão disponíveis [aqui](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="51567-221">Some of the sample PowerShell examples are available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>     

<span data-ttu-id="51567-222">Depois de mapas de fragmento são preenchidos, aplicativos de acesso de dados podem ser criados ou adaptados para funcionar com os mapas.</span><span class="sxs-lookup"><span data-stu-id="51567-222">Once shard maps have been populated, data access applications can be created or adapted to work with the maps.</span></span> <span data-ttu-id="51567-223">Não será necessário preencher ou manipular os mapas novamente até que o **layout do mapa** precise ser alterado.</span><span class="sxs-lookup"><span data-stu-id="51567-223">Populating or manipulating the maps need not occur again until **map layout** needs to change.</span></span>  

## <a name="data-dependent-routing"></a><span data-ttu-id="51567-224">Roteamento dependente de dados</span><span class="sxs-lookup"><span data-stu-id="51567-224">Data dependent routing</span></span>
<span data-ttu-id="51567-225">O gerenciador de mapa de fragmento será mais usado em aplicativos que exigem conexões de banco de dados para executar as operações de dados específicos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="51567-225">The shard map manager will be most used in applications that require database connections to perform the app-specific data operations.</span></span> <span data-ttu-id="51567-226">Essas conexões devem estar associadas ao banco de dados correto.</span><span class="sxs-lookup"><span data-stu-id="51567-226">Those connections must be associated with the correct database.</span></span> <span data-ttu-id="51567-227">Isso é conhecido como **Roteamento Dependente de Dados**.</span><span class="sxs-lookup"><span data-stu-id="51567-227">This is known as **Data Dependent Routing**.</span></span> <span data-ttu-id="51567-228">Para esses aplicativos, instancie um objeto do Gerenciador do mapa de fragmento de fábrica usando as credenciais que têm acesso somente leitura no banco de dados GSM.</span><span class="sxs-lookup"><span data-stu-id="51567-228">For these applications, instantiate a shard map manager object from the factory using credentials that have read-only access on the GSM database.</span></span> <span data-ttu-id="51567-229">As solicitações individuais para conexões posteriores fornecerão credenciais necessárias para conectar-se ao banco de dados apropriado do fragmento.</span><span class="sxs-lookup"><span data-stu-id="51567-229">Individual requests for later connections supply credentials necessary for connecting to the appropriate shard database.</span></span>

<span data-ttu-id="51567-230">Observe que esses aplicativos (usando o **ShardMapManager** aberto com as credenciais somente leitura) não poderão alterar os mapas ou mapeamentos.</span><span class="sxs-lookup"><span data-stu-id="51567-230">Note that these applications (using **ShardMapManager** opened with read-only credentials) cannot make changes to the maps or mappings.</span></span> <span data-ttu-id="51567-231">Para essas necessidades, crie aplicativos administrativos específicos ou scripts do PowerShell que fornecem credenciais de privilégios mais altos, conforme discutido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="51567-231">For those needs, create administrative-specific applications or PowerShell scripts that supply higher-privileged credentials as discussed earlier.</span></span> <span data-ttu-id="51567-232">Veja [Credenciais usadas para acessar a biblioteca de cliente do Banco de Dados Elástico](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="51567-232">See [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

<span data-ttu-id="51567-233">Para obter mais detalhes, consulte [Roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="51567-233">For more details, see [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> 

## <a name="modifying-a-shard-map"></a><span data-ttu-id="51567-234">Modificar um mapa de fragmentos</span><span class="sxs-lookup"><span data-stu-id="51567-234">Modifying a shard map</span></span>
<span data-ttu-id="51567-235">Um mapa do fragmento pode ser alterado de diferentes maneiras.</span><span class="sxs-lookup"><span data-stu-id="51567-235">A shard map can be changed in different ways.</span></span> <span data-ttu-id="51567-236">Todos os seguintes métodos de modificar os metadados que descrevem os fragmentos e seus mapeamentos, mas eles não modificam dados dentro de fragmentos fisicamente, nem que criar ou excluir os bancos de dados reais.</span><span class="sxs-lookup"><span data-stu-id="51567-236">All of the following methods modify the metadata describing the shards and their mappings, but they do not physically modify data within the shards, nor do they create or delete the actual databases.</span></span>  <span data-ttu-id="51567-237">Algumas das operações no mapa de fragmento descrito abaixo talvez precisem ser coordenada com ações administrativas que mover fisicamente os dados ou que adicionar e remover bancos de dados que serve como fragmentos.</span><span class="sxs-lookup"><span data-stu-id="51567-237">Some of the operations on the shard map described below may need to be coordinated with administrative actions that physically move data or that add and remove databases serving as shards.</span></span>

<span data-ttu-id="51567-238">Esses métodos funcionam juntos como blocos de construção disponíveis para modificar a distribuição global de dados em seu ambiente de banco de dados fragmentado.</span><span class="sxs-lookup"><span data-stu-id="51567-238">These methods work together as the building blocks available for modifying the overall distribution of data in your sharded database environment.</span></span>  

* <span data-ttu-id="51567-239">Para adicionar ou remover fragmentos: use **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** e **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** da [classe Shardmap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span><span class="sxs-lookup"><span data-stu-id="51567-239">To add or remove shards: use **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** and **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** of the [Shardmap class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span></span> 
  
    <span data-ttu-id="51567-240">O servidor e o banco de dados que representa o fragmento de destino já devem existir para executar essas operações.</span><span class="sxs-lookup"><span data-stu-id="51567-240">The server and database representing the target shard must already exist for these operations to execute.</span></span> <span data-ttu-id="51567-241">Esses métodos não têm qualquer impacto nos bancos de dados, apenas nos metadados no mapa do fragmento.</span><span class="sxs-lookup"><span data-stu-id="51567-241">These methods do not have any impact on the databases themselves, only on metadata in the shard map.</span></span>
* <span data-ttu-id="51567-242">Para criar ou remover pontos ou intervalos mapeados para os fragmentos: use **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**, **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** da [classe RangeShardMapping](https://msdn.microsoft.com/library/azure/dn807318.aspx) e **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** de [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span><span class="sxs-lookup"><span data-stu-id="51567-242">To create or remove points or ranges that are mapped to the shards: use **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**, **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** of the [RangeShardMapping class](https://msdn.microsoft.com/library/azure/dn807318.aspx), and **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** of the [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span></span>
  
    <span data-ttu-id="51567-243">Vários pontos diferentes ou intervalos podem ser mapeados para o mesmo fragmento.</span><span class="sxs-lookup"><span data-stu-id="51567-243">Many different points or ranges can be mapped to the same shard.</span></span> <span data-ttu-id="51567-244">Esses métodos afetam somente metadados – eles não afetam os dados que podem já estar presentes em fragmentos.</span><span class="sxs-lookup"><span data-stu-id="51567-244">These methods only affect metadata - they do not affect any data that may already be present in shards.</span></span> <span data-ttu-id="51567-245">Se for necessário remover os dados do banco de dados para que eles sejam consistentes com as operações **DeleteMapping** , você precisará realizar essas operações separadamente, mas em conjunto com esses métodos.</span><span class="sxs-lookup"><span data-stu-id="51567-245">If data needs to be removed from the database in order to be consistent with **DeleteMapping** operations, you will need to perform those operations separately but in conjunction with using these methods.</span></span>  
* <span data-ttu-id="51567-246">Para dividir intervalos existentes em dois ou mesclar intervalos adjacentes em um: use **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** e **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="51567-246">To split existing ranges into two, or merge adjacent ranges into one: use **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** and **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span></span>  
  
    <span data-ttu-id="51567-247">Observe que as operações de divisão e mesclagem **não alteram o fragmento para o qual os valores de chave são mapeados**.</span><span class="sxs-lookup"><span data-stu-id="51567-247">Note that split and merge operations **do not change the shard to which key values are mapped**.</span></span> <span data-ttu-id="51567-248">Uma divisão divide um intervalo existente em duas partes, mas deixa ambos como mapeada para o mesmo fragmento.</span><span class="sxs-lookup"><span data-stu-id="51567-248">A split breaks an existing range into two parts, but leaves both as mapped to the same shard.</span></span> <span data-ttu-id="51567-249">Uma mesclagem opera em dois intervalos adjacentes que já são mapeados para o mesmo fragmento, juntando-os em um único intervalo.</span><span class="sxs-lookup"><span data-stu-id="51567-249">A merge operates on two adjacent ranges that are already mapped to the same shard, coalescing them into a single range.</span></span>  <span data-ttu-id="51567-250">A movimentação dos próprios pontos ou intervalos entre fragmentos precisa ser coordenada com **UpdateMapping** em conjunto com a movimentação real de dados.</span><span class="sxs-lookup"><span data-stu-id="51567-250">The movement of points or ranges themselves between shards needs to be coordinated by using **UpdateMapping** in conjunction with actual data movement.</span></span>  <span data-ttu-id="51567-251">É possível usar o serviço de **Divisão/Mesclagem** que faz parte das ferramentas de banco de dados elástico para coordenar as alterações de mapa de fragmentos com a movimentação de dados, quando a movimentação for necessária.</span><span class="sxs-lookup"><span data-stu-id="51567-251">You can use the **Split/Merge** service that is part of elastic database tools to coordinate shard map changes with data movement, when movement is needed.</span></span> 
* <span data-ttu-id="51567-252">Para remapear (ou mover) pontos ou intervalos individuais para fragmentos diferentes: use **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="51567-252">To re-map (or move) individual points or ranges to different shards: use **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span></span>  
  
    <span data-ttu-id="51567-253">Já que pode ser necessário mover os dados de um fragmento para outro para que eles sejam consistentes com as operações **UpdateMapping** , você precisará executar essa movimentação separadamente, mas em conjunto com esses métodos.</span><span class="sxs-lookup"><span data-stu-id="51567-253">Since data may need to be moved from one shard to another in order to be consistent with **UpdateMapping** operations, you will need to perform that movement separately but in conjunction with using these methods.</span></span>
* <span data-ttu-id="51567-254">Para deixar mapeamentos online e offline: use **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** e **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** para controlar o estado online de um mapeamento.</span><span class="sxs-lookup"><span data-stu-id="51567-254">To take mappings online and offline: use **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** and **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** to control the online state of a mapping.</span></span> 
  
    <span data-ttu-id="51567-255">Algumas operações nos mapeamentos de fragmentos são permitidas apenas quando um mapeamento está em um estado “offline”, incluindo **UpdateMapping** e **DeleteMapping**.</span><span class="sxs-lookup"><span data-stu-id="51567-255">Certain operations on shard mappings are only allowed when a mapping is in an “offline” state, including **UpdateMapping** and **DeleteMapping**.</span></span> <span data-ttu-id="51567-256">Quando um mapeamento estiver offline, uma solicitação dependente de dados com base em uma chave incluída nesse mapeamento retornará um erro.</span><span class="sxs-lookup"><span data-stu-id="51567-256">When a mapping is offline, a data-dependent request based on a key included in that mapping will return an error.</span></span> <span data-ttu-id="51567-257">Além disso, quando um intervalo primeiro fica offline, todas as conexões para o fragmento afetado serão eliminadas automaticamente para evitar resultados inconsistentes ou incompletos para consultas direcionadas com intervalos que está sendo alterados.</span><span class="sxs-lookup"><span data-stu-id="51567-257">In addition, when a range is first taken offline, all connections to the affected shard are automatically killed in order to prevent inconsistent or incomplete results for queries directed against ranges being changed.</span></span> 

<span data-ttu-id="51567-258">Mapeamentos são objetos imutáveis no .Net.</span><span class="sxs-lookup"><span data-stu-id="51567-258">Mappings are immutable objects in .Net.</span></span>  <span data-ttu-id="51567-259">Todos os métodos acima que alteram mapeamentos também invalidam todas as referências a eles em seu código.</span><span class="sxs-lookup"><span data-stu-id="51567-259">All of the methods above that change mappings also invalidate any references to them in your code.</span></span> <span data-ttu-id="51567-260">Para facilitar a execução de sequências de operações que alteram o estado do mapeamento, todos os métodos que alteram um mapeamento retornam uma nova referência de mapeamento, para que as operações possam ser encadeadas.</span><span class="sxs-lookup"><span data-stu-id="51567-260">To make it easier to perform sequences of operations that change a mapping’s state, all of the methods that change a mapping return a new mapping reference, so operations can be chained.</span></span> <span data-ttu-id="51567-261">Por exemplo, para excluir um mapeamento existente em sm shardmap que contém a chave 25, você pode executar o seguinte:</span><span class="sxs-lookup"><span data-stu-id="51567-261">For example, to delete an existing mapping in shardmap sm that contains the key 25, you can execute the following:</span></span> 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a><span data-ttu-id="51567-262">Adicionar um fragmento</span><span class="sxs-lookup"><span data-stu-id="51567-262">Adding a shard</span></span>
<span data-ttu-id="51567-263">Geralmente, os aplicativos precisam simplesmente adicionar novos fragmentos para lidar com dados que são esperados de novas chaves ou intervalos de chaves para um mapa do fragmento que já existe.</span><span class="sxs-lookup"><span data-stu-id="51567-263">Applications often need to simply add new shards to handle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="51567-264">Por exemplo, um aplicativo fragmentado por ID de locatário talvez tenha provisionar um novo fragmento para um novo locatário ou dados mensalmente fragmentados talvez precisem de um novo fragmento provisionado antes do início de cada novo mês.</span><span class="sxs-lookup"><span data-stu-id="51567-264">For example, an application sharded by Tenant ID may need to provision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before the start of each new month.</span></span> 

<span data-ttu-id="51567-265">Se o novo intervalo de valores de chave já não é parte de um mapeamento existente e nenhuma movimentação de dados é necessária, é muito simples adicionar o novo fragmento e associar a nova chave ou o intervalo para esse fragmento.</span><span class="sxs-lookup"><span data-stu-id="51567-265">If the new range of key values is not already part of an existing mapping and no data movement is necessary, it is very simple to add the new shard and associate the new key or range to that shard.</span></span> <span data-ttu-id="51567-266">Para obter detalhes sobre como adicionar novos fragmentos, veja [Adicionar um novo fragmento](sql-database-elastic-scale-add-a-shard.md).</span><span class="sxs-lookup"><span data-stu-id="51567-266">For details on adding new shards, see [Adding a new shard](sql-database-elastic-scale-add-a-shard.md).</span></span>

<span data-ttu-id="51567-267">Para cenários que exigem a movimentação de dados, no entanto, a ferramenta de divisão/mesclagem é necessária para orquestrar a movimentação dos dados entre os fragmentos em conjunto com as atualizações necessárias do mapa de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="51567-267">For scenarios that require data movement, however, the split-merge tool is needed to orchestrate the data movement between shards in combination with the necessary shard map updates.</span></span> <span data-ttu-id="51567-268">Para obter detalhes sobre como usar a ferramenta de divisão/mesclagem, confira [Visão geral de divisão/mesclagem](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="51567-268">For details on using the split-merge yool, see [Overview of split-merge](sql-database-elastic-scale-overview-split-and-merge.md)</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
