---
title: Como consultar dados do Graph no Azure Cosmos DB? | Microsoft Docs
description: Aprenda a consultar dados do Graph no Azure Cosmos DB
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
ms.openlocfilehash: 81713c72da037f127e81239d214d7a877247dca1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-how-to-query-with-the-graph-api-preview"></a><span data-ttu-id="520d0-104">Azure Cosmos DB: Como consultar com a API do Graph (visualização)?</span><span class="sxs-lookup"><span data-stu-id="520d0-104">Azure Cosmos DB: How to query with the Graph API (preview)?</span></span>

<span data-ttu-id="520d0-105">A [API do Graph](graph-introduction.md) (visualização) do Azure Cosmos DB oferece suporte a consultas do [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/).</span><span class="sxs-lookup"><span data-stu-id="520d0-105">The Azure Cosmos DB [Graph API](graph-introduction.md) (preview) supports [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) queries.</span></span> <span data-ttu-id="520d0-106">Este artigo fornece exemplos de documentos e consultas para você começar.</span><span class="sxs-lookup"><span data-stu-id="520d0-106">This article provides sample documents and queries to get you started.</span></span> <span data-ttu-id="520d0-107">Uma referência detalhada do Gremlin é fornecida no artigo [Suporte a Gremlin](gremlin-support.md).</span><span class="sxs-lookup"><span data-stu-id="520d0-107">A detailed Gremlin reference is provided in the [Gremlin support](gremlin-support.md) article.</span></span>

<span data-ttu-id="520d0-108">Este artigo aborda as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="520d0-108">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="520d0-109">Consultar dados com o Gremlin</span><span class="sxs-lookup"><span data-stu-id="520d0-109">Querying data with Gremlin</span></span>

## <a name="prerequisites"></a><span data-ttu-id="520d0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="520d0-110">Prerequisites</span></span>

<span data-ttu-id="520d0-111">Para essas consultas funcionarem, você deve ter uma conta do Azure Cosmos DB e ter dados de gráfico no contêiner.</span><span class="sxs-lookup"><span data-stu-id="520d0-111">For these queries to work, you must have an Azure Cosmos DB account and have graph data in the container.</span></span> <span data-ttu-id="520d0-112">Não tenho nenhum deles?</span><span class="sxs-lookup"><span data-stu-id="520d0-112">Don't have any of those?</span></span> <span data-ttu-id="520d0-113">Complete o [Guia de início rápido de cinco minutos](create-graph-dotnet.md) ou o [tutorial de desenvolvedor](tutorial-query-graph.md) para criar uma conta e preencher seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="520d0-113">Complete the [5-minute quickstart](create-graph-dotnet.md) or the [developer tutorial](tutorial-query-graph.md) to create an account and populate your database.</span></span> <span data-ttu-id="520d0-114">Você pode executar as seguintes consultas usando a [Biblioteca de gráficos do .NET do Azure Cosmos DB](graph-sdk-dotnet.md), [Console do Gremlin](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) ou o seu driver favorito do Gremlin.</span><span class="sxs-lookup"><span data-stu-id="520d0-114">You can run the following queries using the [Azure Cosmos DB .NET graph library](graph-sdk-dotnet.md), [Gremlin console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), or your favorite Gremlin driver.</span></span>

## <a name="count-vertices-in-the-graph"></a><span data-ttu-id="520d0-115">Contagem de vértices no gráfico</span><span class="sxs-lookup"><span data-stu-id="520d0-115">Count vertices in the graph</span></span>

<span data-ttu-id="520d0-116">O trecho a seguir mostra como contar o número de vértices no gráfico:</span><span class="sxs-lookup"><span data-stu-id="520d0-116">The following snippet shows how to count the number of vertices in the graph:</span></span>

```
g.V().count()
```

## <a name="filters"></a><span data-ttu-id="520d0-117">Filtros</span><span class="sxs-lookup"><span data-stu-id="520d0-117">Filters</span></span>

<span data-ttu-id="520d0-118">Execute filtros usando as etapas `has` e `hasLabel` do Gremlin e combine-as usando `and`, `or` e `not` para compilar filtros mais complexos.</span><span class="sxs-lookup"><span data-stu-id="520d0-118">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` to build more complex filters.</span></span> <span data-ttu-id="520d0-119">O Azure Cosmos DB fornece indexação independente do esquema de todas as propriedades em seus vértices e graus para consultas rápidas:</span><span class="sxs-lookup"><span data-stu-id="520d0-119">Azure Cosmos DB provides schema-agnostic indexing of all properties within your vertices and degrees for fast queries:</span></span>

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a><span data-ttu-id="520d0-120">Projeção</span><span class="sxs-lookup"><span data-stu-id="520d0-120">Projection</span></span>

<span data-ttu-id="520d0-121">Você pode projetar certas propriedades nos resultados da consulta usando a etapa `values`:</span><span class="sxs-lookup"><span data-stu-id="520d0-121">You can project certain properties in the query results using the `values` step:</span></span>

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a><span data-ttu-id="520d0-122">Localizar os vértices e bordas relacionadas</span><span class="sxs-lookup"><span data-stu-id="520d0-122">Find related edges and vertices</span></span>

<span data-ttu-id="520d0-123">Até agora, só vimos operadores de consulta que funcionam em qualquer banco de dados.</span><span class="sxs-lookup"><span data-stu-id="520d0-123">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="520d0-124">Os gráficos são rápidos e eficientes para operações de passagem quando você precisa navegar até os vértices e bordas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="520d0-124">Graphs are fast and efficient for traversal operations when you need to navigate to related edges and vertices.</span></span> <span data-ttu-id="520d0-125">Vamos encontrar todos os amigos de Thomas.</span><span class="sxs-lookup"><span data-stu-id="520d0-125">Let's find all friends of Thomas.</span></span> <span data-ttu-id="520d0-126">Fazemos isso usando a etapa `outE` do Gremlin para localizar todos as bordas externas de Thomas, depois passamos para os vértices internos dessas bordas usando a etapa `inV` do Gremlin:</span><span class="sxs-lookup"><span data-stu-id="520d0-126">We do this by using Gremlin's `outE` step to find all the out-edges from Thomas, then traversing to the in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="520d0-127">A próxima consulta executa dois saltos para localizar todos os "amigos dos amigos" de Thomas, chamando `outE` e `inV` duas vezes.</span><span class="sxs-lookup"><span data-stu-id="520d0-127">The next query performs two hops to find all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="520d0-128">Você pode criar consultas mais complexas e implementar uma lógica avançada de passagem de gráfico usando o Gremlin, incluindo a combinação de expressões de filtro, executando o loop usando a etapa `loop` e implementando a navegação condicional usando a etapa `choose`.</span><span class="sxs-lookup"><span data-stu-id="520d0-128">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using the `loop` step, and implementing conditional navigation using the `choose` step.</span></span> <span data-ttu-id="520d0-129">Saiba mais sobre o que você pode fazer com o [Suporte do Gremlin](gremlin-support.md)!</span><span class="sxs-lookup"><span data-stu-id="520d0-129">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

## <a name="next-steps"></a><span data-ttu-id="520d0-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="520d0-130">Next steps</span></span>

<span data-ttu-id="520d0-131">Neste tutorial, você fez o seguinte:</span><span class="sxs-lookup"><span data-stu-id="520d0-131">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="520d0-132">Aprendeu a consultar usando o Graph</span><span class="sxs-lookup"><span data-stu-id="520d0-132">Learned how to query using Graph</span></span> 

<span data-ttu-id="520d0-133">Agora você pode prosseguir para o próximo tutorial e aprender a distribuir seus dados globalmente.</span><span class="sxs-lookup"><span data-stu-id="520d0-133">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="520d0-134">Distribuir os dados globalmente</span><span class="sxs-lookup"><span data-stu-id="520d0-134">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)