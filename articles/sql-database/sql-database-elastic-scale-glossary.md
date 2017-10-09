---
title: "Glossário de ferramentas de banco de dados aaaElastic | Microsoft Docs"
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
ms.openlocfilehash: d6573aad9a097e07135b0a64d1dafec19bb8cc7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-glossary"></a><span data-ttu-id="1237f-103">Glossário de ferramentas do banco de dados elástico</span><span class="sxs-lookup"><span data-stu-id="1237f-103">Elastic Database tools glossary</span></span>
<span data-ttu-id="1237f-104">Olá termos a seguir são definidos para Olá [ferramentas de banco de dados Elástico](sql-database-elastic-scale-introduction.md), um recurso do banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1237f-104">hello following terms are defined for hello [Elastic Database tools](sql-database-elastic-scale-introduction.md), a feature of Azure SQL Database.</span></span> <span data-ttu-id="1237f-105">ferramentas Hello são usada toomanage [mapas de fragmento](sql-database-elastic-scale-shard-map-management.md)e incluem hello [biblioteca de cliente](sql-database-elastic-database-client-library.md), Olá [ferramenta de mesclagem de divisão](sql-database-elastic-scale-overview-split-and-merge.md), [pools Elásticos](sql-database-elastic-pool.md), e [consultas](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1237f-105">hello tools are used toomanage [shard maps](sql-database-elastic-scale-shard-map-management.md), and include hello [client library](sql-database-elastic-database-client-library.md), hello [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastic pools](sql-database-elastic-pool.md), and [queries](sql-database-elastic-query-overview.md).</span></span> 

<span data-ttu-id="1237f-106">Esses termos são usados em [adicionando um fragmento usando as ferramentas de banco de dados Elástico](sql-database-elastic-scale-add-a-shard.md) e [usando problemas de mapa de fragmento Olá RecoveryManager classe toofix](sql-database-elastic-database-recovery-manager.md).</span><span class="sxs-lookup"><span data-stu-id="1237f-106">These terms are used in [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Using hello RecoveryManager class toofix shard map problems](sql-database-elastic-database-recovery-manager.md).</span></span>

![Termos de escala elástica][1]

<span data-ttu-id="1237f-108">**Banco de dados**: um Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="1237f-108">**Database**: An Azure SQL database.</span></span> 

<span data-ttu-id="1237f-109">**Roteamento dependente de dados**: Olá funcionalidade que permite que um fragmento de tooa tooconnect aplicativo recebe uma chave de fragmentação específico.</span><span class="sxs-lookup"><span data-stu-id="1237f-109">**Data dependent routing**: hello functionality that enables an application tooconnect tooa shard given a specific sharding key.</span></span> <span data-ttu-id="1237f-110">Consulte [Roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="1237f-110">See [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="1237f-111">Comparar muito**[vários fragmentos consulta](sql-database-elastic-scale-multishard-querying.md)**.</span><span class="sxs-lookup"><span data-stu-id="1237f-111">Compare too**[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span></span>

<span data-ttu-id="1237f-112">**Mapa do fragmento global**: Olá mapa entre as chaves de fragmentação e seus respectivos fragmentos em um **conjunto de fragmentos**.</span><span class="sxs-lookup"><span data-stu-id="1237f-112">**Global shard map**: hello map between sharding keys and their respective shards within a **shard set**.</span></span> <span data-ttu-id="1237f-113">mapa do fragmento global de saudação é armazenado no hello **Gerenciador do mapa de fragmentos**.</span><span class="sxs-lookup"><span data-stu-id="1237f-113">hello global shard map is stored in hello **shard map manager**.</span></span> <span data-ttu-id="1237f-114">Comparar muito**mapa do fragmento local**.</span><span class="sxs-lookup"><span data-stu-id="1237f-114">Compare too**local shard map**.</span></span>

<span data-ttu-id="1237f-115">**Mapa de fragmentos de lista**: um mapa de fragmentos no qual as chaves de fragmentação são mapeadas individualmente.</span><span class="sxs-lookup"><span data-stu-id="1237f-115">**List shard map**: A shard map in which sharding keys are mapped individually.</span></span> <span data-ttu-id="1237f-116">Comparar muito**mapa do fragmento intervalo**.</span><span class="sxs-lookup"><span data-stu-id="1237f-116">Compare too**Range Shard Map**.</span></span>   

<span data-ttu-id="1237f-117">**Mapa do fragmento local**: armazenado em um fragmento, mapa de fragmento local Olá contém mapeamentos de saudação shardlets que residem em um fragmento de saudação.</span><span class="sxs-lookup"><span data-stu-id="1237f-117">**Local shard map**: Stored on a shard, hello local shard map contains mappings for hello shardlets that reside on hello shard.</span></span>

<span data-ttu-id="1237f-118">**Consulta de vários fragmento**: Olá capacidade tooissue uma consulta em vários fragmentos; os conjuntos de resultados são retornados usando UNION ALL semânticas (também conhecido como "consulta de fan-out").</span><span class="sxs-lookup"><span data-stu-id="1237f-118">**Multi-shard query**: hello ability tooissue a query against multiple shards; results sets are returned using UNION ALL semantics (also known as “fan-out query”).</span></span> <span data-ttu-id="1237f-119">Comparar muito**roteamento dependente de dados**.</span><span class="sxs-lookup"><span data-stu-id="1237f-119">Compare too**data dependent routing**.</span></span>

<span data-ttu-id="1237f-120">**Multilocatário** e **Locatário único**: mostra um banco de dados com locatário único e um banco de dados multilocatário:</span><span class="sxs-lookup"><span data-stu-id="1237f-120">**Multi-tenant** and **Single-tenant**: This shows a single-tenant database and a multi-tenant database:</span></span>

![Bancos de dados de único locatário e multilocatário](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

<span data-ttu-id="1237f-122">Esta é uma representação de bancos de dados de único locatário e multilocatário **fragmentados** .</span><span class="sxs-lookup"><span data-stu-id="1237f-122">Here is a representation of **sharded** single and multi-tenant databases.</span></span> 

![Bancos de dados de único locatário e multilocatário](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

<span data-ttu-id="1237f-124">**Mapa do fragmento intervalo**: um mapa do fragmento que Olá estratégia de distribuição do fragmento é baseada em vários intervalos de valores contíguos.</span><span class="sxs-lookup"><span data-stu-id="1237f-124">**Range shard map**: A shard map in which hello shard distribution strategy is based on multiple ranges of contiguous values.</span></span> 

<span data-ttu-id="1237f-125">**Tabelas de referência**: tabelas que não são fragmentadas, mas replicadas nos fragmentos.</span><span class="sxs-lookup"><span data-stu-id="1237f-125">**Reference tables**: Tables that are not sharded but are replicated across shards.</span></span> <span data-ttu-id="1237f-126">Por exemplo, códigos postais podem ser armazenados em uma tabela de referência.</span><span class="sxs-lookup"><span data-stu-id="1237f-126">For example, zip codes can be stored in a reference table.</span></span> 

<span data-ttu-id="1237f-127">**Fragmento**: um banco de dados SQL do Azure que armazena dados de um conjunto de dados fragmentados.</span><span class="sxs-lookup"><span data-stu-id="1237f-127">**Shard**: An Azure SQL database that stores data from a sharded data set.</span></span> 

<span data-ttu-id="1237f-128">**Elasticidade de fragmento**: Olá capacidade tooperform **escalonamento horizontal** e **dimensionamento vertical**.</span><span class="sxs-lookup"><span data-stu-id="1237f-128">**Shard elasticity**: hello ability tooperform both **horizontal scaling** and **vertical scaling**.</span></span>

<span data-ttu-id="1237f-129">**Tabelas fragmentadas**: tabelas que são fragmentadas, ou seja, cujos dados são distribuídos por meio de fragmentos com base em seus valores de chave de fragmentação.</span><span class="sxs-lookup"><span data-stu-id="1237f-129">**Sharded tables**: Tables that are sharded, i.e., whose data is distributed across shards based on their sharding key values.</span></span> 

<span data-ttu-id="1237f-130">**Chave de fragmentação**: um valor de coluna que determina como os dados são distribuídos nos fragmentos.</span><span class="sxs-lookup"><span data-stu-id="1237f-130">**Sharding key**: A column value that determines how data is distributed across shards.</span></span> <span data-ttu-id="1237f-131">Olá tipo de valor pode ser um dos seguintes Olá: **int**, **bigint**, **varbinary**, ou **uniqueidentifier**.</span><span class="sxs-lookup"><span data-stu-id="1237f-131">hello value type can be one of hello following: **int**, **bigint**, **varbinary**, or **uniqueidentifier**.</span></span> 

<span data-ttu-id="1237f-132">**Conjunto de fragmentos**: Olá coleção de fragmentos são toohello atribuído mesmo mapa do fragmento no Gerenciador do mapa de fragmentos hello.</span><span class="sxs-lookup"><span data-stu-id="1237f-132">**Shard set**: hello collection of shards that are attributed toohello same shard map in hello shard map manager.</span></span>  

<span data-ttu-id="1237f-133">**Shardlet**: todos os dados de saudação associados a um único valor de uma chave de fragmentação em um fragmento.</span><span class="sxs-lookup"><span data-stu-id="1237f-133">**Shardlet**: All of hello data associated with a single value of a sharding key on a shard.</span></span> <span data-ttu-id="1237f-134">Um shardlet é a menor unidade Olá de movimentação de dados possível quando redistribuindo tabelas fragmentadas.</span><span class="sxs-lookup"><span data-stu-id="1237f-134">A shardlet is hello smallest unit of data movement possible when redistributing sharded tables.</span></span> 

<span data-ttu-id="1237f-135">**Mapa do fragmento**: Olá conjunto de mapeamentos entre as chaves de fragmentação e seus respectivos fragmentos.</span><span class="sxs-lookup"><span data-stu-id="1237f-135">**Shard map**: hello set of mappings between sharding keys and their respective shards.</span></span>

<span data-ttu-id="1237f-136">**Gerenciador do mapa de fragmentos**: um repositório de dados e o objeto de gerenciamento que contém mapas de fragmento hello, locais de fragmento e mapeamentos para um ou mais conjuntos de fragmento.</span><span class="sxs-lookup"><span data-stu-id="1237f-136">**Shard map manager**: A management object and data store that contains hello shard map(s), shard locations, and mappings for one or more shard sets.</span></span>

![Mapeamentos][2]

## <a name="verbs"></a><span data-ttu-id="1237f-138">Verbos</span><span class="sxs-lookup"><span data-stu-id="1237f-138">Verbs</span></span>
<span data-ttu-id="1237f-139">**Escalonamento horizontal**: ato de saudação de scaling out (ou em) um conjunto de fragmentos, adicionando ou removendo o mapa do fragmento tooa fragmentos, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="1237f-139">**Horizontal scaling**: hello act of scaling out (or in) a collection of shards by adding or removing shards tooa shard map, as shown below.</span></span>

![Dimensionamento horizontal e vertical][3]

<span data-ttu-id="1237f-141">**Mesclar**: ato de saudação de mover shardlets de fragmento de tooone dois fragmentos e atualizando o mapa do fragmento Olá adequadamente.</span><span class="sxs-lookup"><span data-stu-id="1237f-141">**Merge**: hello act of moving shardlets from two shards tooone shard and updating hello shard map accordingly.</span></span>

<span data-ttu-id="1237f-142">**Mover Shardlets**: ato de saudação de movimentação de um fragmento diferente de tooa único shardlet.</span><span class="sxs-lookup"><span data-stu-id="1237f-142">**Shardlet move**: hello act of moving a single shardlet tooa different shard.</span></span> 

<span data-ttu-id="1237f-143">**Fragmento**: ato de saudação de particionamento horizontal de forma idêntica dados estruturados em vários bancos de dados com base em uma chave de fragmentação.</span><span class="sxs-lookup"><span data-stu-id="1237f-143">**Shard**: hello act of horizontally partitioning identically structured data across multiple databases based on a sharding key.</span></span>

<span data-ttu-id="1237f-144">**Divisão**: act Olá mover vários shardlets do fragmento (normalmente novo) de tooanother um fragmento.</span><span class="sxs-lookup"><span data-stu-id="1237f-144">**Split**: hello act of moving several shardlets from one shard tooanother (typically new) shard.</span></span> <span data-ttu-id="1237f-145">Uma chave de fragmentação é fornecida pelo usuário Olá Olá ponto de divisão.</span><span class="sxs-lookup"><span data-stu-id="1237f-145">A sharding key is provided by hello user as hello split point.</span></span>

<span data-ttu-id="1237f-146">**Escala vertical**: ato de saudação de dimensionamento para cima (ou para baixo) Olá nível de desempenho de um fragmento individual.</span><span class="sxs-lookup"><span data-stu-id="1237f-146">**Vertical Scaling**: hello act of scaling up (or down) hello performance level of an individual shard.</span></span> <span data-ttu-id="1237f-147">Por exemplo, alterar um fragmento de tooPremium padrão (o que resulta em mais recursos de computação).</span><span class="sxs-lookup"><span data-stu-id="1237f-147">For example, changing a shard from Standard tooPremium (which results in more computing resources).</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

