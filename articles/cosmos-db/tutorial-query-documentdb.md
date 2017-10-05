---
title: Como consultar com SQL no Azure Cosmos DB? | Microsoft Docs
description: Aprenda a consulta com os dados do DocumentDB com o SQL no Azure Cosmos DB
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
ms.openlocfilehash: a2a562c06c6302b9548e758b4c6754ec13b6001d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-using-sql"></a><span data-ttu-id="24175-104">Azure Cosmos DB: Como consultar usando SQL?</span><span class="sxs-lookup"><span data-stu-id="24175-104">Azure Cosmos DB: How to query using SQL?</span></span>

<span data-ttu-id="24175-105">A [API do DocumentDB](documentdb-introduction.md) do Azure Cosmos DB oferece suporte à consulta de documentos usando SQL.</span><span class="sxs-lookup"><span data-stu-id="24175-105">The Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) supports querying documents using SQL.</span></span> <span data-ttu-id="24175-106">Este artigo fornece um exemplo de documento e dois exemplos de consultas SQL e resultados.</span><span class="sxs-lookup"><span data-stu-id="24175-106">This article provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="24175-107">Este artigo aborda as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="24175-107">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="24175-108">Consultar dados com SQL</span><span class="sxs-lookup"><span data-stu-id="24175-108">Querying data with SQL</span></span>

## <a name="sample-document"></a><span data-ttu-id="24175-109">Exemplo de documento</span><span class="sxs-lookup"><span data-stu-id="24175-109">Sample document</span></span>

<span data-ttu-id="24175-110">As consultas de SQL neste artigo usam o seguinte exemplo de documento.</span><span class="sxs-lookup"><span data-stu-id="24175-110">The SQL queries in this article use the following sample document.</span></span>

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
## <a name="where-can-i-run-sql-queries"></a><span data-ttu-id="24175-111">Onde é possível executar consultas SQL?</span><span class="sxs-lookup"><span data-stu-id="24175-111">Where can I run SQL queries?</span></span>

<span data-ttu-id="24175-112">Você pode executar consultas usando o Data Explorer no Portal do Azure, por meio da [API REST e SDKs](documentdb-sdk-dotnet.md) e até mesmo o [Playground de consultas](https://www.documentdb.com/sql/demo), que executa consultas em um conjunto existente de dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="24175-112">You can run queries using the Data Explorer in the Azure portal, via the [REST API and SDKs](documentdb-sdk-dotnet.md), and even the [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.</span></span>

<span data-ttu-id="24175-113">Para saber mais sobre consultas SQL, confira:</span><span class="sxs-lookup"><span data-stu-id="24175-113">For more information about SQL queries, see:</span></span>
* [<span data-ttu-id="24175-114">Consulta e sintaxe SQL</span><span class="sxs-lookup"><span data-stu-id="24175-114">SQL query and SQL syntax</span></span>](documentdb-sql-query.md)

## <a name="prerequisites"></a><span data-ttu-id="24175-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="24175-115">Prerequisites</span></span>

<span data-ttu-id="24175-116">Este tutorial presume que você tem uma conta e uma coleção do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="24175-116">This tutorial assumes you have an Azure Cosmos DB account and collection.</span></span> <span data-ttu-id="24175-117">Não tenho nenhum deles?</span><span class="sxs-lookup"><span data-stu-id="24175-117">Don't have any of those?</span></span> <span data-ttu-id="24175-118">Complete o [Guia de início rápido de cinco minutos](create-mongodb-nodejs.md) ou o [tutorial de desenvolvedor](tutorial-develop-mongodb.md) para criar uma conta e uma coleção.</span><span class="sxs-lookup"><span data-stu-id="24175-118">Complete the [5-minute quickstart](create-mongodb-nodejs.md) or the [developer tutorial](tutorial-develop-mongodb.md) to create an account and collection.</span></span>

## <a name="example-query-1"></a><span data-ttu-id="24175-119">Exemplo de consulta 1</span><span class="sxs-lookup"><span data-stu-id="24175-119">Example query 1</span></span>

<span data-ttu-id="24175-120">Com base no exemplo de documento de família acima, a consulta SQL a seguir retorna os documentos cujo campo de id corresponde a `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="24175-120">Given the sample family document above, following SQL query returns the documents where the id field matches `WakefieldFamily`.</span></span> <span data-ttu-id="24175-121">Por se tratar de uma instrução `SELECT *`, a saída da consulta será todo o documento JSON:</span><span class="sxs-lookup"><span data-stu-id="24175-121">Since it's a `SELECT *` statement, the output of the query is the complete JSON document:</span></span>

<span data-ttu-id="24175-122">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="24175-122">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

<span data-ttu-id="24175-123">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="24175-123">**Results**</span></span>

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

## <a name="example-query-2"></a><span data-ttu-id="24175-124">Exemplo de consulta 2</span><span class="sxs-lookup"><span data-stu-id="24175-124">Example query 2</span></span>

<span data-ttu-id="24175-125">A próxima consulta retorna todos os nomes dos filhos na família cuja identificação corresponde ao `WakefieldFamily` organizado por nota.</span><span class="sxs-lookup"><span data-stu-id="24175-125">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by their grade.</span></span>

<span data-ttu-id="24175-126">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="24175-126">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

<span data-ttu-id="24175-127">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="24175-127">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a><span data-ttu-id="24175-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="24175-128">Next steps</span></span>

<span data-ttu-id="24175-129">Neste tutorial, você fez o seguinte:</span><span class="sxs-lookup"><span data-stu-id="24175-129">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="24175-130">Aprendeu a consultar usando SQL</span><span class="sxs-lookup"><span data-stu-id="24175-130">Learned how to query using SQL</span></span>  

<span data-ttu-id="24175-131">Agora você pode prosseguir para o próximo tutorial e aprender a distribuir seus dados globalmente.</span><span class="sxs-lookup"><span data-stu-id="24175-131">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="24175-132">Distribuir os dados globalmente</span><span class="sxs-lookup"><span data-stu-id="24175-132">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

