---
title: "Glossário de ferramentas de Banco de Dados Elástico | Microsoft Docs"
description: "Explicação dos termos usados para as ferramentas de banco de dados elástico"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: a23a4e81-6706-452d-afc1-a550e5e47af9
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 0fda4bb948bbed1c14d468519ba67cce9bc4e6c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="elastic-database-tools-glossary"></a><span data-ttu-id="e4bdb-103">Glossário de ferramentas do banco de dados elástico</span><span class="sxs-lookup"><span data-stu-id="e4bdb-103">Elastic Database tools glossary</span></span>
<span data-ttu-id="e4bdb-104">Os termos a seguir são definidos para as [ferramentas de Banco de Dados Elástico](sql-database-elastic-scale-introduction.md), um recurso do Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-104">The following terms are defined for the [Elastic Database tools](sql-database-elastic-scale-introduction.md), a feature of Azure SQL Database.</span></span> <span data-ttu-id="e4bdb-105">As ferramentas são usadas para gerenciar [mapas de fragmentos](sql-database-elastic-scale-shard-map-management.md) e incluem a [biblioteca de cliente](sql-database-elastic-database-client-library.md), a [ferramenta de divisão e mesclagem](sql-database-elastic-scale-overview-split-and-merge.md), [pools elásticos](sql-database-elastic-pool.md) e [consultas](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e4bdb-105">The tools are used to manage [shard maps](sql-database-elastic-scale-shard-map-management.md), and include the [client library](sql-database-elastic-database-client-library.md), the [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastic pools](sql-database-elastic-pool.md), and [queries](sql-database-elastic-query-overview.md).</span></span> 

<span data-ttu-id="e4bdb-106">Esses termos são usados em [Adicionando um fragmento usando ferramentas de Banco de Dados Elástico](sql-database-elastic-scale-add-a-shard.md) e [Usando a classe RecoveryManager para corrigir problemas de mapas de fragmentos](sql-database-elastic-database-recovery-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e4bdb-106">These terms are used in [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Using the RecoveryManager class to fix shard map problems](sql-database-elastic-database-recovery-manager.md).</span></span>

![Termos de escala elástica][1]

<span data-ttu-id="e4bdb-108">**Banco de dados**: um Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-108">**Database**: An Azure SQL database.</span></span> 

<span data-ttu-id="e4bdb-109">**Roteamento dependente de dados**: a funcionalidade que permite que um aplicativo se conecte a um fragmento dada uma chave de fragmentação específica.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-109">**Data dependent routing**: The functionality that enables an application to connect to a shard given a specific sharding key.</span></span> <span data-ttu-id="e4bdb-110">Consulte [Roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="e4bdb-110">See [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="e4bdb-111">Compare com a **[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-111">Compare to **[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span></span>

<span data-ttu-id="e4bdb-112">**Mapa de fragmentos global**: o mapa entre chaves de fragmentação e seus respectivos fragmentos em um **conjunto de fragmentos**.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-112">**Global shard map**: The map between sharding keys and their respective shards within a **shard set**.</span></span> <span data-ttu-id="e4bdb-113">O mapa de fragmentos global é armazenado no **gerenciador do mapa de fragmentos**.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-113">The global shard map is stored in the **shard map manager**.</span></span> <span data-ttu-id="e4bdb-114">Compare com o **mapa de fragmentos local**.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-114">Compare to **local shard map**.</span></span>

<span data-ttu-id="e4bdb-115">**Mapa de fragmentos de lista**: um mapa de fragmentos no qual as chaves de fragmentação são mapeadas individualmente.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-115">**List shard map**: A shard map in which sharding keys are mapped individually.</span></span> <span data-ttu-id="e4bdb-116">Compare com o **Mapa de fragmentos de intervalo**.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-116">Compare to **Range Shard Map**.</span></span>   

<span data-ttu-id="e4bdb-117">**Mapa de fragmentos local**: armazenado em um fragmento, o mapa de fragmentos local contém mapeamentos para os shardlets que residem no fragmento.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-117">**Local shard map**: Stored on a shard, the local shard map contains mappings for the shardlets that reside on the shard.</span></span>

<span data-ttu-id="e4bdb-118">**Consulta de vários fragmentos**: a capacidade de executar uma consulta em vários fragmentos; os conjuntos de resultados são retornados usando a semântica UNION ALL (também conhecida como “consulta do tipo fan-out”).</span><span class="sxs-lookup"><span data-stu-id="e4bdb-118">**Multi-shard query**: The ability to issue a query against multiple shards; results sets are returned using UNION ALL semantics (also known as “fan-out query”).</span></span> <span data-ttu-id="e4bdb-119">Compare com o **roteamento dependente de dados**.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-119">Compare to **data dependent routing**.</span></span>

<span data-ttu-id="e4bdb-120">**Multilocatário** e **Locatário único**: mostra um banco de dados com locatário único e um banco de dados multilocatário:</span><span class="sxs-lookup"><span data-stu-id="e4bdb-120">**Multi-tenant** and **Single-tenant**: This shows a single-tenant database and a multi-tenant database:</span></span>

![Bancos de dados de único locatário e multilocatário](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

<span data-ttu-id="e4bdb-122">Esta é uma representação de bancos de dados de único locatário e multilocatário **fragmentados** .</span><span class="sxs-lookup"><span data-stu-id="e4bdb-122">Here is a representation of **sharded** single and multi-tenant databases.</span></span> 

![Bancos de dados de único locatário e multilocatário](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

<span data-ttu-id="e4bdb-124">**Mapa de fragmentos de intervalo**: um mapa de fragmentos em que a estratégia de distribuição de fragmentos é baseada em vários intervalos de valores contíguos.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-124">**Range shard map**: A shard map in which the shard distribution strategy is based on multiple ranges of contiguous values.</span></span> 

<span data-ttu-id="e4bdb-125">**Tabelas de referência**: tabelas que não são fragmentadas, mas replicadas nos fragmentos.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-125">**Reference tables**: Tables that are not sharded but are replicated across shards.</span></span> <span data-ttu-id="e4bdb-126">Por exemplo, códigos postais podem ser armazenados em uma tabela de referência.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-126">For example, zip codes can be stored in a reference table.</span></span> 

<span data-ttu-id="e4bdb-127">**Fragmento**: um banco de dados SQL do Azure que armazena dados de um conjunto de dados fragmentados.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-127">**Shard**: An Azure SQL database that stores data from a sharded data set.</span></span> 

<span data-ttu-id="e4bdb-128">**Elasticidade de fragmento**: a capacidade de executar **escala horizontal** e **escala vertical**.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-128">**Shard elasticity**: The ability to perform both **horizontal scaling** and **vertical scaling**.</span></span>

<span data-ttu-id="e4bdb-129">**Tabelas fragmentadas**: tabelas que são fragmentadas, ou seja, cujos dados são distribuídos por meio de fragmentos com base em seus valores de chave de fragmentação.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-129">**Sharded tables**: Tables that are sharded, i.e., whose data is distributed across shards based on their sharding key values.</span></span> 

<span data-ttu-id="e4bdb-130">**Chave de fragmentação**: um valor de coluna que determina como os dados são distribuídos nos fragmentos.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-130">**Sharding key**: A column value that determines how data is distributed across shards.</span></span> <span data-ttu-id="e4bdb-131">O tipo do valor pode ser um dos seguintes: **int**, **bigint**, **varbinary** ou **uniqueidentifier**.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-131">The value type can be one of the following: **int**, **bigint**, **varbinary**, or **uniqueidentifier**.</span></span> 

<span data-ttu-id="e4bdb-132">**Conjunto de fragmentos**: a coleção de fragmentos que são atribuídos ao mesmo mapa de fragmentos no gerenciador de mapa de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-132">**Shard set**: The collection of shards that are attributed to the same shard map in the shard map manager.</span></span>  

<span data-ttu-id="e4bdb-133">**Shardlet**: todos os dados associados a um único valor de uma chave de fragmentação em um fragmento.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-133">**Shardlet**: All of the data associated with a single value of a sharding key on a shard.</span></span> <span data-ttu-id="e4bdb-134">Um shardlet é a menor unidade de movimentação de dados possível ao redistribuir tabelas fragmentadas.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-134">A shardlet is the smallest unit of data movement possible when redistributing sharded tables.</span></span> 

<span data-ttu-id="e4bdb-135">**Mapa de fragmentos**: o conjunto de mapeamentos entre chaves de fragmentação e seus respectivos fragmentos.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-135">**Shard map**: The set of mappings between sharding keys and their respective shards.</span></span>

<span data-ttu-id="e4bdb-136">**Gerenciador de mapa de fragmentos**: um objeto de gerenciamento e um repositório de dados que contém o(s) mapa(s) de fragmentos, locais de fragmentos e mapeamentos para um ou mais conjuntos de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-136">**Shard map manager**: A management object and data store that contains the shard map(s), shard locations, and mappings for one or more shard sets.</span></span>

![Mapeamentos][2]

## <a name="verbs"></a><span data-ttu-id="e4bdb-138">Verbos</span><span class="sxs-lookup"><span data-stu-id="e4bdb-138">Verbs</span></span>
<span data-ttu-id="e4bdb-139">**Escala horizontal**: o ato de escalar horizontal (ou verticalmente) uma coleção de fragmentos adicionando ou removendo fragmentos de um mapa de fragmentos, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-139">**Horizontal scaling**: The act of scaling out (or in) a collection of shards by adding or removing shards to a shard map, as shown below.</span></span>

![Dimensionamento horizontal e vertical][3]

<span data-ttu-id="e4bdb-141">**Mesclar**: o ato de mover shardlets de dois fragmentos para um e atualizar o mapa de fragmentos de acordo.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-141">**Merge**: The act of moving shardlets from two shards to one shard and updating the shard map accordingly.</span></span>

<span data-ttu-id="e4bdb-142">**Mover shardlet**: o ato de mover um único shardlet para um fragmento diferente.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-142">**Shardlet move**: The act of moving a single shardlet to a different shard.</span></span> 

<span data-ttu-id="e4bdb-143">**Fragmentar**: o ato de particionar horizontalmente dados estruturados de modo idêntico em vários bancos de dados com base em uma chave de fragmentação.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-143">**Shard**: The act of horizontally partitioning identically structured data across multiple databases based on a sharding key.</span></span>

<span data-ttu-id="e4bdb-144">**Dividir**: o ato de mover vários shardlets de um fragmento para outro (normalmente novo).</span><span class="sxs-lookup"><span data-stu-id="e4bdb-144">**Split**: The act of moving several shardlets from one shard to another (typically new) shard.</span></span> <span data-ttu-id="e4bdb-145">Uma chave de fragmentação é fornecida pelo usuário como o ponto de divisão.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-145">A sharding key is provided by the user as the split point.</span></span>

<span data-ttu-id="e4bdb-146">**Dimensionamento vertical**: o ato de escalar (ou reduzir) verticalmente o nível de desempenho de um fragmento individual.</span><span class="sxs-lookup"><span data-stu-id="e4bdb-146">**Vertical Scaling**: The act of scaling up (or down) the performance level of an individual shard.</span></span> <span data-ttu-id="e4bdb-147">Por exemplo, alterar um fragmento de Standard para Premium (o que resulta em mais recursos de computação).</span><span class="sxs-lookup"><span data-stu-id="e4bdb-147">For example, changing a shard from Standard to Premium (which results in more computing resources).</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

