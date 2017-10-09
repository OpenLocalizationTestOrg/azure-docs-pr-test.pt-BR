---
title: "Cosmos do Azure DB: Como tooquery usando Olá API DocumentDB? | Microsoft Docs"
description: Saiba mais sobre o tooquery com hello API DocumentDB para o banco de dados do Azure Cosmos
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
ms.openlocfilehash: e3e5a49f7510942bcfb15330e5f86c5dd8b1e5d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-api-for-mongodb"></a><span data-ttu-id="0b094-104">Cosmos do Azure DB: Como tooquery com a API para o MongoDB?</span><span class="sxs-lookup"><span data-stu-id="0b094-104">Azure Cosmos DB: How tooquery with API for MongoDB?</span></span>

<span data-ttu-id="0b094-105">Olá banco de dados do Azure Cosmos [API para o MongoDB](mongodb-introduction.md) dá suporte a [consultas de shell do MongoDB](https://docs.mongodb.com/manual/tutorial/query-documents/).</span><span class="sxs-lookup"><span data-stu-id="0b094-105">hello Azure Cosmos DB [API for MongoDB](mongodb-introduction.md) supports [MongoDB shell queries](https://docs.mongodb.com/manual/tutorial/query-documents/).</span></span> 

<span data-ttu-id="0b094-106">Este artigo aborda Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0b094-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="0b094-107">Consultar dados com o MongoDB</span><span class="sxs-lookup"><span data-stu-id="0b094-107">Querying data with MongoDB</span></span>

## <a name="sample-document"></a><span data-ttu-id="0b094-108">Exemplo de documento</span><span class="sxs-lookup"><span data-stu-id="0b094-108">Sample document</span></span>

<span data-ttu-id="0b094-109">consultas de saudação neste artigo usam Olá documento de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="0b094-109">hello queries in this article use hello following sample document.</span></span>

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
## <span data-ttu-id="0b094-110"><a id="examplequery1"></a>Exemplo de consulta 1</span><span class="sxs-lookup"><span data-stu-id="0b094-110"><a id="examplequery1"></a> Example query 1</span></span> 

<span data-ttu-id="0b094-111">Dado documento família de exemplo de hello acima, retorna documentos de saudação em que o campo de id de saudação corresponde de consulta a seguir Olá `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="0b094-111">Given hello sample family document above, hello following query returns hello documents where hello id field matches `WakefieldFamily`.</span></span>

<span data-ttu-id="0b094-112">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="0b094-112">**Query**</span></span>
    
    db.families.find({ id: “WakefieldFamily”})

<span data-ttu-id="0b094-113">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="0b094-113">**Results**</span></span>

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

## <span data-ttu-id="0b094-114"><a id="examplequery2"></a>Exemplo de consulta 2</span><span class="sxs-lookup"><span data-stu-id="0b094-114"><a id="examplequery2"></a>Example query 2</span></span> 

<span data-ttu-id="0b094-115">consulta seguinte Olá retorna todos os filhos de saudação da família de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b094-115">hello next query returns all hello children in hello family.</span></span> 

<span data-ttu-id="0b094-116">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="0b094-116">**Query**</span></span>
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

<span data-ttu-id="0b094-117">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="0b094-117">**Results**</span></span>

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


## <span data-ttu-id="0b094-118"><a id="examplequery3"></a>Exemplo de consulta 3</span><span class="sxs-lookup"><span data-stu-id="0b094-118"><a id="examplequery3"></a>Example query 3</span></span> 

<span data-ttu-id="0b094-119">consulta seguinte Olá retorna todas as famílias de saudação que são registradas.</span><span class="sxs-lookup"><span data-stu-id="0b094-119">hello next query returns all hello families which are registered.</span></span> 

<span data-ttu-id="0b094-120">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="0b094-120">**Query**</span></span>
    
    db.families.find( { "isRegistered" : true })
<span data-ttu-id="0b094-121">**Resultados** nenhum documento será retornado.</span><span class="sxs-lookup"><span data-stu-id="0b094-121">**Results** No document will be returned.</span></span> 

## <span data-ttu-id="0b094-122"><a id="examplequery4"></a>Exemplo de consulta 4</span><span class="sxs-lookup"><span data-stu-id="0b094-122"><a id="examplequery4"></a>Example query 4</span></span>

<span data-ttu-id="0b094-123">consulta seguinte Olá retorna todas as famílias de saudação que não estão registradas.</span><span class="sxs-lookup"><span data-stu-id="0b094-123">hello next query returns all hello families which are not registered.</span></span> 

<span data-ttu-id="0b094-124">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="0b094-124">**Query**</span></span>
    
    db.families.find( { "isRegistered" : false })
<span data-ttu-id="0b094-125">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="0b094-125">**Results**</span></span>

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
<span data-ttu-id="0b094-126">}</span><span class="sxs-lookup"><span data-stu-id="0b094-126">}</span></span>

## <span data-ttu-id="0b094-127"><a id="examplequery5"></a>Exemplo de consulta 5</span><span class="sxs-lookup"><span data-stu-id="0b094-127"><a id="examplequery5"></a>Example query 5</span></span>

<span data-ttu-id="0b094-128">consulta seguinte Olá retorna todas as famílias de saudação que não estão registradas e o estado é NY.</span><span class="sxs-lookup"><span data-stu-id="0b094-128">hello next query returns all hello families which are not registered and state is NY.</span></span> 

<span data-ttu-id="0b094-129">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="0b094-129">**Query**</span></span>
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

<span data-ttu-id="0b094-130">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="0b094-130">**Results**</span></span>

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
<span data-ttu-id="0b094-131">}</span><span class="sxs-lookup"><span data-stu-id="0b094-131">}</span></span>


## <span data-ttu-id="0b094-132"><a id="examplequery6"></a>Exemplo de consulta 6</span><span class="sxs-lookup"><span data-stu-id="0b094-132"><a id="examplequery6"></a>Example query 6</span></span>

<span data-ttu-id="0b094-133">consulta seguinte Olá retorna todas as famílias de saudação onde notas filhos são 8.</span><span class="sxs-lookup"><span data-stu-id="0b094-133">hello next query returns all hello families where children grades are 8.</span></span>

<span data-ttu-id="0b094-134">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="0b094-134">**Query**</span></span>
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

<span data-ttu-id="0b094-135">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="0b094-135">**Results**</span></span>

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
<span data-ttu-id="0b094-136">}</span><span class="sxs-lookup"><span data-stu-id="0b094-136">}</span></span>

## <span data-ttu-id="0b094-137"><a id="examplequery7"></a>Exemplo de consulta 7</span><span class="sxs-lookup"><span data-stu-id="0b094-137"><a id="examplequery7"></a>Example query 7</span></span>

<span data-ttu-id="0b094-138">consulta seguinte Olá retorna todas as famílias de saudação em que o tamanho da matriz de filhos é 3.</span><span class="sxs-lookup"><span data-stu-id="0b094-138">hello next query returns all hello families where size of children array is 3.</span></span>

<span data-ttu-id="0b094-139">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="0b094-139">**Query**</span></span>
  
      db.Family.find( {children: { $size:3} } )

<span data-ttu-id="0b094-140">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="0b094-140">**Results**</span></span>

<span data-ttu-id="0b094-141">Nenhum resultado retornará, pois não temos mais de dois filhos.</span><span class="sxs-lookup"><span data-stu-id="0b094-141">No results will be returned as we do not have more than 2 children.</span></span> <span data-ttu-id="0b094-142">Somente quando o parâmetro é 2 essa consulta será bem-sucedida e retornar documento completo hello.</span><span class="sxs-lookup"><span data-stu-id="0b094-142">Only when parameter is 2 this query will succeed and return hello full document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b094-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0b094-143">Next steps</span></span>

<span data-ttu-id="0b094-144">Neste tutorial, você fez a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="0b094-144">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0b094-145">Aprendeu como tooquery usando o MongoDB</span><span class="sxs-lookup"><span data-stu-id="0b094-145">Learned how tooquery using MongoDB</span></span> 

<span data-ttu-id="0b094-146">Você pode continuar toolearn tutorial do próximo toohello como toodistribute seus dados globalmente.</span><span class="sxs-lookup"><span data-stu-id="0b094-146">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0b094-147">Distribuir os dados globalmente</span><span class="sxs-lookup"><span data-stu-id="0b094-147">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

