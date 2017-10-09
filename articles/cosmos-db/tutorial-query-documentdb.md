---
title: aaaHow tooquery com SQL no banco de dados do Azure Cosmos? | Microsoft Docs
description: Saiba tooquery com dados de documentos com SQL no banco de dados do Azure Cosmos
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: tutorial-develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: d3dc51acf92cb78d4f4d9dbac7ec54b1382431cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-using-sql"></a><span data-ttu-id="42245-104">Cosmos do Azure DB: Como tooquery usando SQL?</span><span class="sxs-lookup"><span data-stu-id="42245-104">Azure Cosmos DB: How tooquery using SQL?</span></span>

<span data-ttu-id="42245-105">Olá banco de dados do Azure Cosmos [API DocumentDB](documentdb-introduction.md) dá suporte a consultar documentos usando SQL.</span><span class="sxs-lookup"><span data-stu-id="42245-105">hello Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) supports querying documents using SQL.</span></span> <span data-ttu-id="42245-106">Este artigo fornece um exemplo de documento e dois exemplos de consultas SQL e resultados.</span><span class="sxs-lookup"><span data-stu-id="42245-106">This article provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="42245-107">Este artigo aborda Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="42245-107">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="42245-108">Consultar dados com SQL</span><span class="sxs-lookup"><span data-stu-id="42245-108">Querying data with SQL</span></span>

## <a name="sample-document"></a><span data-ttu-id="42245-109">Exemplo de documento</span><span class="sxs-lookup"><span data-stu-id="42245-109">Sample document</span></span>

<span data-ttu-id="42245-110">consultas SQL Olá neste artigo utilizar Olá documento de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="42245-110">hello SQL queries in this article use hello following sample document.</span></span>

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```
## <a name="where-can-i-run-sql-queries"></a><span data-ttu-id="42245-111">Onde é possível executar consultas SQL?</span><span class="sxs-lookup"><span data-stu-id="42245-111">Where can I run SQL queries?</span></span>

<span data-ttu-id="42245-112">Você pode executar consultas usando Olá Explorador de dados em Olá portal do Azure, por meio de saudação [API REST e SDKs](documentdb-sdk-dotnet.md)e até mesmo hello [parque de consulta](https://www.documentdb.com/sql/demo), que executa consultas em um conjunto de dados de exemplo existentes.</span><span class="sxs-lookup"><span data-stu-id="42245-112">You can run queries using hello Data Explorer in hello Azure portal, via hello [REST API and SDKs](documentdb-sdk-dotnet.md), and even hello [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.</span></span>

<span data-ttu-id="42245-113">Para saber mais sobre consultas SQL, confira:</span><span class="sxs-lookup"><span data-stu-id="42245-113">For more information about SQL queries, see:</span></span>
* [<span data-ttu-id="42245-114">Consulta e sintaxe SQL</span><span class="sxs-lookup"><span data-stu-id="42245-114">SQL query and SQL syntax</span></span>](documentdb-sql-query.md)

## <a name="prerequisites"></a><span data-ttu-id="42245-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="42245-115">Prerequisites</span></span>

<span data-ttu-id="42245-116">Este tutorial presume que você tem uma conta e uma coleção do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="42245-116">This tutorial assumes you have an Azure Cosmos DB account and collection.</span></span> <span data-ttu-id="42245-117">Não tenho nenhum deles?</span><span class="sxs-lookup"><span data-stu-id="42245-117">Don't have any of those?</span></span> <span data-ttu-id="42245-118">Olá completa [início rápido de 5 minutos](create-mongodb-nodejs.md) ou hello [tutorial de desenvolvedor](tutorial-develop-mongodb.md) toocreate uma conta e uma coleção.</span><span class="sxs-lookup"><span data-stu-id="42245-118">Complete hello [5-minute quickstart](create-mongodb-nodejs.md) or hello [developer tutorial](tutorial-develop-mongodb.md) toocreate an account and collection.</span></span>

## <a name="example-query-1"></a><span data-ttu-id="42245-119">Exemplo de consulta 1</span><span class="sxs-lookup"><span data-stu-id="42245-119">Example query 1</span></span>

<span data-ttu-id="42245-120">Dado documento família de exemplo de hello acima, consulta SQL a seguir retorna Olá documentos em que o campo de id de saudação corresponde `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="42245-120">Given hello sample family document above, following SQL query returns hello documents where hello id field matches `WakefieldFamily`.</span></span> <span data-ttu-id="42245-121">Uma vez que ele é um `SELECT *` declaração de saída de saudação da consulta de saudação é documento JSON completo hello:</span><span class="sxs-lookup"><span data-stu-id="42245-121">Since it's a `SELECT *` statement, hello output of hello query is hello complete JSON document:</span></span>

<span data-ttu-id="42245-122">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="42245-122">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

<span data-ttu-id="42245-123">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="42245-123">**Results**</span></span>

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

## <a name="example-query-2"></a><span data-ttu-id="42245-124">Exemplo de consulta 2</span><span class="sxs-lookup"><span data-stu-id="42245-124">Example query 2</span></span>

<span data-ttu-id="42245-125">consulta seguinte Olá retorna todos os nomes de fornecido de saudação de filhos na família Olá cuja id corresponde `WakefieldFamily` ordenados por sua classificação.</span><span class="sxs-lookup"><span data-stu-id="42245-125">hello next query returns all hello given names of children in hello family whose id matches `WakefieldFamily` ordered by their grade.</span></span>

<span data-ttu-id="42245-126">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="42245-126">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

<span data-ttu-id="42245-127">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="42245-127">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a><span data-ttu-id="42245-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="42245-128">Next steps</span></span>

<span data-ttu-id="42245-129">Neste tutorial, você fez a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="42245-129">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="42245-130">Aprendeu como tooquery usando SQL</span><span class="sxs-lookup"><span data-stu-id="42245-130">Learned how tooquery using SQL</span></span>  

<span data-ttu-id="42245-131">Você pode continuar toolearn tutorial do próximo toohello como toodistribute seus dados globalmente.</span><span class="sxs-lookup"><span data-stu-id="42245-131">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="42245-132">Distribuir os dados globalmente</span><span class="sxs-lookup"><span data-stu-id="42245-132">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

