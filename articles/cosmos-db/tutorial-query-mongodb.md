---
title: 'Azure Cosmos DB: Como consulta usando a API do DocumentDB? | Microsoft Docs'
description: Aprenda a consulta com a API do DocumentDB para o Azure Cosmos DB
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: feffc553a9aa931d96cec71c101674fce08a466b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-with-api-for-mongodb"></a><span data-ttu-id="434f4-104">Azure Cosmos DB: Como consultar com a API para MongoDB?</span><span class="sxs-lookup"><span data-stu-id="434f4-104">Azure Cosmos DB: How to query with API for MongoDB?</span></span>

<span data-ttu-id="434f4-105">A [API para MongoDB](mongodb-introduction.md) do Azure Cosmos DB oferece suporte a [consultas do shell do MongoDB](https://docs.mongodb.com/manual/tutorial/query-documents/).</span><span class="sxs-lookup"><span data-stu-id="434f4-105">The Azure Cosmos DB [API for MongoDB](mongodb-introduction.md) supports [MongoDB shell queries](https://docs.mongodb.com/manual/tutorial/query-documents/).</span></span> 

<span data-ttu-id="434f4-106">Este artigo aborda as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="434f4-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="434f4-107">Consultar dados com o MongoDB</span><span class="sxs-lookup"><span data-stu-id="434f4-107">Querying data with MongoDB</span></span>

## <a name="sample-document"></a><span data-ttu-id="434f4-108">Exemplo de documento</span><span class="sxs-lookup"><span data-stu-id="434f4-108">Sample document</span></span>

<span data-ttu-id="434f4-109">As consultas neste artigo usam o seguinte exemplo de documento.</span><span class="sxs-lookup"><span data-stu-id="434f4-109">The queries in this article use the following sample document.</span></span>

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
## <span data-ttu-id="434f4-110"><a id="examplequery1"></a>Exemplo de consulta 1</span><span class="sxs-lookup"><span data-stu-id="434f4-110"><a id="examplequery1"></a> Example query 1</span></span> 

<span data-ttu-id="434f4-111">Com base no exemplo de documento de família acima, a consulta a seguir retorna os documentos cujo campo de id corresponde a `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="434f4-111">Given the sample family document above, the following query returns the documents where the id field matches `WakefieldFamily`.</span></span>

<span data-ttu-id="434f4-112">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="434f4-112">**Query**</span></span>
    
    db.families.find({ id: “WakefieldFamily”})

<span data-ttu-id="434f4-113">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="434f4-113">**Results**</span></span>

    {
    "_id": "ObjectId(\"58f65e1198f3a12c7090e68c\")",
    "id": "WakefieldFamily",
    "parents": [
      {
        "familyName": "Wakefield",
        "givenName": "Robin"
      },
      {
        "familyName": "Miller",
        "givenName": "Ben"
      }
    ],
    "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
          { "givenName": "Goofy" },
          { "givenName": "Shadow" }
        ]
      },
      {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
      }
    ],
    "address": {
      "state": "NY",
      "county": "Manhattan",
      "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
    }

## <span data-ttu-id="434f4-114"><a id="examplequery2"></a>Exemplo de consulta 2</span><span class="sxs-lookup"><span data-stu-id="434f4-114"><a id="examplequery2"></a>Example query 2</span></span> 

<span data-ttu-id="434f4-115">A próxima consulta retorna todos os filhos da família.</span><span class="sxs-lookup"><span data-stu-id="434f4-115">The next query returns all the children in the family.</span></span> 

<span data-ttu-id="434f4-116">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="434f4-116">**Query**</span></span>
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

<span data-ttu-id="434f4-117">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="434f4-117">**Results**</span></span>

    {
    "_id": "ObjectId("58f65e1198f3a12c7090e68c")",
    "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
          { "givenName": "Goofy" },
          { "givenName": "Shadow" }
        ]
      },
      {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
      }
    ]
    }


## <span data-ttu-id="434f4-118"><a id="examplequery3"></a>Exemplo de consulta 3</span><span class="sxs-lookup"><span data-stu-id="434f4-118"><a id="examplequery3"></a>Example query 3</span></span> 

<span data-ttu-id="434f4-119">A próxima consulta retorna todas as famílias registradas.</span><span class="sxs-lookup"><span data-stu-id="434f4-119">The next query returns all the families which are registered.</span></span> 

<span data-ttu-id="434f4-120">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="434f4-120">**Query**</span></span>
    
    db.families.find( { "isRegistered" : true })
<span data-ttu-id="434f4-121">**Resultados** nenhum documento será retornado.</span><span class="sxs-lookup"><span data-stu-id="434f4-121">**Results** No document will be returned.</span></span> 

## <span data-ttu-id="434f4-122"><a id="examplequery4"></a>Exemplo de consulta 4</span><span class="sxs-lookup"><span data-stu-id="434f4-122"><a id="examplequery4"></a>Example query 4</span></span>

<span data-ttu-id="434f4-123">A próxima consulta retorna todas as famílias que não estão registradas.</span><span class="sxs-lookup"><span data-stu-id="434f4-123">The next query returns all the families which are not registered.</span></span> 

<span data-ttu-id="434f4-124">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="434f4-124">**Query**</span></span>
    
    db.families.find( { "isRegistered" : false })
<span data-ttu-id="434f4-125">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="434f4-125">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="434f4-126">}</span><span class="sxs-lookup"><span data-stu-id="434f4-126">}</span></span>

## <span data-ttu-id="434f4-127"><a id="examplequery5"></a>Exemplo de consulta 5</span><span class="sxs-lookup"><span data-stu-id="434f4-127"><a id="examplequery5"></a>Example query 5</span></span>

<span data-ttu-id="434f4-128">A próxima consulta retorna todas as famílias que não estão registradas e cujo estado é NY.</span><span class="sxs-lookup"><span data-stu-id="434f4-128">The next query returns all the families which are not registered and state is NY.</span></span> 

<span data-ttu-id="434f4-129">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="434f4-129">**Query**</span></span>
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

<span data-ttu-id="434f4-130">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="434f4-130">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="434f4-131">}</span><span class="sxs-lookup"><span data-stu-id="434f4-131">}</span></span>


## <span data-ttu-id="434f4-132"><a id="examplequery6"></a>Exemplo de consulta 6</span><span class="sxs-lookup"><span data-stu-id="434f4-132"><a id="examplequery6"></a>Example query 6</span></span>

<span data-ttu-id="434f4-133">A próxima consulta retorna todas as famílias das quais as notas dos filhos seja 8.</span><span class="sxs-lookup"><span data-stu-id="434f4-133">The next query returns all the families where children grades are 8.</span></span>

<span data-ttu-id="434f4-134">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="434f4-134">**Query**</span></span>
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

<span data-ttu-id="434f4-135">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="434f4-135">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="434f4-136">}</span><span class="sxs-lookup"><span data-stu-id="434f4-136">}</span></span>

## <span data-ttu-id="434f4-137"><a id="examplequery7"></a>Exemplo de consulta 7</span><span class="sxs-lookup"><span data-stu-id="434f4-137"><a id="examplequery7"></a>Example query 7</span></span>

<span data-ttu-id="434f4-138">A próxima consulta retorna todas as famílias das quais o tamanho da matriz de filhos seja três.</span><span class="sxs-lookup"><span data-stu-id="434f4-138">The next query returns all the families where size of children array is 3.</span></span>

<span data-ttu-id="434f4-139">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="434f4-139">**Query**</span></span>
  
      db.Family.find( {children: { $size:3} } )

<span data-ttu-id="434f4-140">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="434f4-140">**Results**</span></span>

<span data-ttu-id="434f4-141">Nenhum resultado retornará, pois não temos mais de dois filhos.</span><span class="sxs-lookup"><span data-stu-id="434f4-141">No results will be returned as we do not have more than 2 children.</span></span> <span data-ttu-id="434f4-142">Somente quando o parâmetro for dois essa consulta será bem-sucedida e retornará o documento completo.</span><span class="sxs-lookup"><span data-stu-id="434f4-142">Only when parameter is 2 this query will succeed and return the full document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="434f4-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="434f4-143">Next steps</span></span>

<span data-ttu-id="434f4-144">Neste tutorial, você fez o seguinte:</span><span class="sxs-lookup"><span data-stu-id="434f4-144">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="434f4-145">Aprendeu a consultar usando o MongoDB</span><span class="sxs-lookup"><span data-stu-id="434f4-145">Learned how to query using MongoDB</span></span> 

<span data-ttu-id="434f4-146">Agora você pode prosseguir para o próximo tutorial e aprender a distribuir seus dados globalmente.</span><span class="sxs-lookup"><span data-stu-id="434f4-146">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="434f4-147">Distribuir os dados globalmente</span><span class="sxs-lookup"><span data-stu-id="434f4-147">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

