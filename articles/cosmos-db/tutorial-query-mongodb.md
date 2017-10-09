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
# <a name="azure-cosmos-db-how-tooquery-with-api-for-mongodb"></a>Cosmos do Azure DB: Como tooquery com a API para o MongoDB?

Olá banco de dados do Azure Cosmos [API para o MongoDB](mongodb-introduction.md) dá suporte a [consultas de shell do MongoDB](https://docs.mongodb.com/manual/tutorial/query-documents/). 

Este artigo aborda Olá tarefas a seguir: 

> [!div class="checklist"]
> * Consultar dados com o MongoDB

## <a name="sample-document"></a>Exemplo de documento

consultas de saudação neste artigo usam Olá documento de exemplo a seguir.

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
## <a id="examplequery1"></a>Exemplo de consulta 1 

Dado documento família de exemplo de hello acima, retorna documentos de saudação em que o campo de id de saudação corresponde de consulta a seguir Olá `WakefieldFamily`.

**Consulta**
    
    db.families.find({ id: “WakefieldFamily”})

**Resultados**

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

## <a id="examplequery2"></a>Exemplo de consulta 2 

consulta seguinte Olá retorna todos os filhos de saudação da família de saudação. 

**Consulta**
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

**Resultados**

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


## <a id="examplequery3"></a>Exemplo de consulta 3 

consulta seguinte Olá retorna todas as famílias de saudação que são registradas. 

**Consulta**
    
    db.families.find( { "isRegistered" : true })
**Resultados** nenhum documento será retornado. 

## <a id="examplequery4"></a>Exemplo de consulta 4

consulta seguinte Olá retorna todas as famílias de saudação que não estão registradas. 

**Consulta**
    
    db.families.find( { "isRegistered" : false })
**Resultados**

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
}

## <a id="examplequery5"></a>Exemplo de consulta 5

consulta seguinte Olá retorna todas as famílias de saudação que não estão registradas e o estado é NY. 

**Consulta**
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

**Resultados**

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
}


## <a id="examplequery6"></a>Exemplo de consulta 6

consulta seguinte Olá retorna todas as famílias de saudação onde notas filhos são 8.

**Consulta**
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

**Resultados**

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
}

## <a id="examplequery7"></a>Exemplo de consulta 7

consulta seguinte Olá retorna todas as famílias de saudação em que o tamanho da matriz de filhos é 3.

**Consulta**
  
      db.Family.find( {children: { $size:3} } )

**Resultados**

Nenhum resultado retornará, pois não temos mais de dois filhos. Somente quando o parâmetro é 2 essa consulta será bem-sucedida e retornar documento completo hello.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você fez a seguir hello:

> [!div class="checklist"]
> * Aprendeu como tooquery usando o MongoDB 

Você pode continuar toolearn tutorial do próximo toohello como toodistribute seus dados globalmente.

> [!div class="nextstepaction"]
> [Distribuir os dados globalmente](tutorial-global-distribution-documentdb.md)

