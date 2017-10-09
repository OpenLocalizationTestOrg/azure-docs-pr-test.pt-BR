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
# <a name="azure-cosmos-db-how-tooquery-using-sql"></a>Cosmos do Azure DB: Como tooquery usando SQL?

Olá banco de dados do Azure Cosmos [API DocumentDB](documentdb-introduction.md) dá suporte a consultar documentos usando SQL. Este artigo fornece um exemplo de documento e dois exemplos de consultas SQL e resultados.

Este artigo aborda Olá tarefas a seguir: 

> [!div class="checklist"]
> * Consultar dados com SQL

## <a name="sample-document"></a>Exemplo de documento

consultas SQL Olá neste artigo utilizar Olá documento de exemplo a seguir.

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
## <a name="where-can-i-run-sql-queries"></a>Onde é possível executar consultas SQL?

Você pode executar consultas usando Olá Explorador de dados em Olá portal do Azure, por meio de saudação [API REST e SDKs](documentdb-sdk-dotnet.md)e até mesmo hello [parque de consulta](https://www.documentdb.com/sql/demo), que executa consultas em um conjunto de dados de exemplo existentes.

Para saber mais sobre consultas SQL, confira:
* [Consulta e sintaxe SQL](documentdb-sql-query.md)

## <a name="prerequisites"></a>Pré-requisitos

Este tutorial presume que você tem uma conta e uma coleção do Azure Cosmos DB. Não tenho nenhum deles? Olá completa [início rápido de 5 minutos](create-mongodb-nodejs.md) ou hello [tutorial de desenvolvedor](tutorial-develop-mongodb.md) toocreate uma conta e uma coleção.

## <a name="example-query-1"></a>Exemplo de consulta 1

Dado documento família de exemplo de hello acima, consulta SQL a seguir retorna Olá documentos em que o campo de id de saudação corresponde `WakefieldFamily`. Uma vez que ele é um `SELECT *` declaração de saída de saudação da consulta de saudação é documento JSON completo hello:

**Consulta**

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

**Resultados**

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

## <a name="example-query-2"></a>Exemplo de consulta 2

consulta seguinte Olá retorna todos os nomes de fornecido de saudação de filhos na família Olá cuja id corresponde `WakefieldFamily` ordenados por sua classificação.

**Consulta**

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

**Resultados**

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você fez a seguir hello:

> [!div class="checklist"]
> * Aprendeu como tooquery usando SQL  

Você pode continuar toolearn tutorial do próximo toohello como toodistribute seus dados globalmente.

> [!div class="nextstepaction"]
> [Distribuir os dados globalmente](tutorial-global-distribution-documentdb.md)

