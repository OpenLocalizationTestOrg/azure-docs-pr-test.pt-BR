---
title: "dados do gráfico aaaHow tooquery no banco de dados do Azure Cosmos? | Microsoft Docs"
description: "Saiba mais dados do gráfico tooquery no banco de dados do Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 8bde5c80-581c-4f70-acb4-9578873c92fa
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: fdde881edd6c488e2fea51e5c9665e1d736009fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-hello-graph-api-preview"></a><span data-ttu-id="f0c7c-104">Cosmos do Azure DB: Como tooquery com hello Graph API (visualização)?</span><span class="sxs-lookup"><span data-stu-id="f0c7c-104">Azure Cosmos DB: How tooquery with hello Graph API (preview)?</span></span>

<span data-ttu-id="f0c7c-105">Olá banco de dados do Azure Cosmos [API do Graph](graph-introduction.md) (visualização) oferece suporte a [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) consultas.</span><span class="sxs-lookup"><span data-stu-id="f0c7c-105">hello Azure Cosmos DB [Graph API](graph-introduction.md) (preview) supports [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) queries.</span></span> <span data-ttu-id="f0c7c-106">Este artigo fornece documentos de exemplo e consultas tooget que é iniciado.</span><span class="sxs-lookup"><span data-stu-id="f0c7c-106">This article provides sample documents and queries tooget you started.</span></span> <span data-ttu-id="f0c7c-107">Uma referência detalhada de Gremlin é fornecida no hello [suporte Gremlin](gremlin-support.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="f0c7c-107">A detailed Gremlin reference is provided in hello [Gremlin support](gremlin-support.md) article.</span></span>

<span data-ttu-id="f0c7c-108">Este artigo aborda Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0c7c-108">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="f0c7c-109">Consultar dados com o Gremlin</span><span class="sxs-lookup"><span data-stu-id="f0c7c-109">Querying data with Gremlin</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0c7c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f0c7c-110">Prerequisites</span></span>

<span data-ttu-id="f0c7c-111">Para toowork essas consultas, você deve ter uma conta de banco de dados do Azure Cosmos e ter dados de gráfico no contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0c7c-111">For these queries toowork, you must have an Azure Cosmos DB account and have graph data in hello container.</span></span> <span data-ttu-id="f0c7c-112">Não tenho nenhum deles?</span><span class="sxs-lookup"><span data-stu-id="f0c7c-112">Don't have any of those?</span></span> <span data-ttu-id="f0c7c-113">Olá completa [início rápido de 5 minutos](create-graph-dotnet.md) ou hello [tutorial de desenvolvedor](tutorial-query-graph.md) toocreate uma conta e preencher o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f0c7c-113">Complete hello [5-minute quickstart](create-graph-dotnet.md) or hello [developer tutorial](tutorial-query-graph.md) toocreate an account and populate your database.</span></span> <span data-ttu-id="f0c7c-114">Você pode executar Olá consultas usando Olá a seguir [biblioteca gráfica do Azure Cosmos DB .NET](graph-sdk-dotnet.md), [console Gremlin](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), ou o driver Gremlin favorito.</span><span class="sxs-lookup"><span data-stu-id="f0c7c-114">You can run hello following queries using hello [Azure Cosmos DB .NET graph library](graph-sdk-dotnet.md), [Gremlin console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), or your favorite Gremlin driver.</span></span>

## <a name="count-vertices-in-hello-graph"></a><span data-ttu-id="f0c7c-115">Contagem de vértices no gráfico de saudação</span><span class="sxs-lookup"><span data-stu-id="f0c7c-115">Count vertices in hello graph</span></span>

<span data-ttu-id="f0c7c-116">saudação de trecho de código a seguir mostra como toocount Olá número de vértices no gráfico de saudação:</span><span class="sxs-lookup"><span data-stu-id="f0c7c-116">hello following snippet shows how toocount hello number of vertices in hello graph:</span></span>

```
g.V().count()
```

## <a name="filters"></a><span data-ttu-id="f0c7c-117">Filtros</span><span class="sxs-lookup"><span data-stu-id="f0c7c-117">Filters</span></span>

<span data-ttu-id="f0c7c-118">Você pode executar filtros usando do Gremlin `has` e `hasLabel` etapas e combiná-los usando `and`, `or`, e `not` toobuild os filtros mais complexos.</span><span class="sxs-lookup"><span data-stu-id="f0c7c-118">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` toobuild more complex filters.</span></span> <span data-ttu-id="f0c7c-119">O Azure Cosmos DB fornece indexação independente do esquema de todas as propriedades em seus vértices e graus para consultas rápidas:</span><span class="sxs-lookup"><span data-stu-id="f0c7c-119">Azure Cosmos DB provides schema-agnostic indexing of all properties within your vertices and degrees for fast queries:</span></span>

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a><span data-ttu-id="f0c7c-120">Projeção</span><span class="sxs-lookup"><span data-stu-id="f0c7c-120">Projection</span></span>

<span data-ttu-id="f0c7c-121">Você pode projetar determinadas propriedades em resultados da consulta hello usando Olá `values` etapa:</span><span class="sxs-lookup"><span data-stu-id="f0c7c-121">You can project certain properties in hello query results using hello `values` step:</span></span>

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a><span data-ttu-id="f0c7c-122">Localizar os vértices e bordas relacionadas</span><span class="sxs-lookup"><span data-stu-id="f0c7c-122">Find related edges and vertices</span></span>

<span data-ttu-id="f0c7c-123">Até agora, só vimos operadores de consulta que funcionam em qualquer banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f0c7c-123">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="f0c7c-124">Gráficos são rápidos e eficientes para operações de passagem quando você precisa toonavigate toorelated bordas e vértices.</span><span class="sxs-lookup"><span data-stu-id="f0c7c-124">Graphs are fast and efficient for traversal operations when you need toonavigate toorelated edges and vertices.</span></span> <span data-ttu-id="f0c7c-125">Vamos encontrar todos os amigos de Thomas.</span><span class="sxs-lookup"><span data-stu-id="f0c7c-125">Let's find all friends of Thomas.</span></span> <span data-ttu-id="f0c7c-126">Podemos fazer isso por meio do Gremlin `outE` etapa toofind Olá todas as out-bordas de Thomas, em seguida, passar toohello nos vértices das bordas usando do Gremlin `inV` etapa:</span><span class="sxs-lookup"><span data-stu-id="f0c7c-126">We do this by using Gremlin's `outE` step toofind all hello out-edges from Thomas, then traversing toohello in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="f0c7c-127">executa a consulta seguinte Olá toofind de dois saltos todos "amigos Thomas intitulado dos amigos", chamando `outE` e `inV` duas vezes.</span><span class="sxs-lookup"><span data-stu-id="f0c7c-127">hello next query performs two hops toofind all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="f0c7c-128">Você pode criar consultas mais complexas e implementar a lógica de passagem de gráfico avançado usando Gremlin, incluindo filtro combinação expressões, executar um loop usando Olá `loop` etapa e implementação navegação condicional usando Olá `choose` etapa.</span><span class="sxs-lookup"><span data-stu-id="f0c7c-128">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using hello `loop` step, and implementing conditional navigation using hello `choose` step.</span></span> <span data-ttu-id="f0c7c-129">Saiba mais sobre o que você pode fazer com o [Suporte do Gremlin](gremlin-support.md)!</span><span class="sxs-lookup"><span data-stu-id="f0c7c-129">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0c7c-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f0c7c-130">Next steps</span></span>

<span data-ttu-id="f0c7c-131">Neste tutorial, você fez a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="f0c7c-131">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f0c7c-132">Aprendeu como tooquery usando o Graph</span><span class="sxs-lookup"><span data-stu-id="f0c7c-132">Learned how tooquery using Graph</span></span> 

<span data-ttu-id="f0c7c-133">Você pode continuar toolearn tutorial do próximo toohello como toodistribute seus dados globalmente.</span><span class="sxs-lookup"><span data-stu-id="f0c7c-133">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f0c7c-134">Distribuir os dados globalmente</span><span class="sxs-lookup"><span data-stu-id="f0c7c-134">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)