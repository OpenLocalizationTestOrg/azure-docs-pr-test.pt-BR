---
title: "tutorial de distribuição global aaaAzure Cosmos DB para a API do MongoDB | Microsoft Docs"
description: "Saiba como distribuição global usando o banco de dados do Azure Cosmos toosetup Olá MongoDB API."
services: cosmos-db
keywords: "distribuição global, MongoDB"
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 0fc2d670bb4e21ac5f813f9586b407ba06ccf354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-mongodb-api"></a>Como a distribuição global usando o banco de dados do Azure Cosmos toosetup Olá MongoDB API

Neste artigo, mostramos como toouse Olá toosetup portal do Azure distribuição global do banco de dados do Azure Cosmos e, em seguida, conecte-se usando Olá MongoDB API.

Este artigo aborda Olá tarefas a seguir: 

> [!div class="checklist"]
> * Configurar a distribuição global usando Olá portal do Azure
> * Configurar a distribuição global usando Olá [API do MongoDB](mongodb-introduction.md)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-hello-mongodb-api"></a>Verificando a configuração regional usando Olá MongoDB API
a maneira mais simples de saudação de duplo verificando sua configuração global dentro de API para o MongoDB é Olá toorun *isMaster()* comando Olá Shell Mongo.

No Shell do Mongo:

   ```
      db.isMaster()
   ```
   
Exemplos de resultados:

   ```JSON
      {
         "_t": "IsMasterResponse",
         "ok": 1,
         "ismaster": true,
         "maxMessageSizeBytes": 4194304,
         "maxWriteBatchSize": 1000,
         "minWireVersion": 0,
         "maxWireVersion": 2,
         "tags": {
            "region": "South India"
         },
         "hosts": [
            "vishi-api-for-mongodb-southcentralus.documents.azure.com:10255",
            "vishi-api-for-mongodb-westeurope.documents.azure.com:10255",
            "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
         ],
         "setName": "globaldb",
         "setVersion": 1,
         "primary": "vishi-api-for-mongodb-southindia.documents.azure.com:10255",
         "me": "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
      }
   ```

## <a name="connecting-tooa-preferred-region-using-hello-mongodb-api"></a>Conectar-se a região preferida tooa usando Olá MongoDB API

Olá MongoDB API permite que você toospecify preferência de leitura da coleção para um banco de dados globalmente distribuído. Para ambos baixa leituras de latência e alta disponibilidade global, é recomendável definir preferência de leitura da coleção muito*mais próximo*. Uma preferência de leitura de *mais próximo* é configurado tooread da região mais próxima hello.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

Para aplicativos com um primário leitura/gravação região e uma região secundária para a recuperação de desastres (DR) cenários, é recomendável definir preferência de leitura da coleção muito*secundário preferido*. Uma preferência de leitura de *secundário preferido* é configurado tooread da região secundária hello quando a região primária Olá não está disponível.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

Por fim, se você como toomanually especificaria as regiões de leitura. Você pode definir a região Olá marca dentro de sua preferência de leitura.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

Assim, concluímos este tutorial. Você pode aprender como toomanage Olá consistência da sua conta global replicada lendo [níveis de consistência no banco de dados do Azure Cosmos](consistency-levels.md). E para saber mais sobre como a replicação de banco de dados global funciona no Azure Cosmos DB, veja [Distribuir dados globalmente com o Azure Cosmos DB](distribute-data-globally.md).

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você fez a seguir hello:

> [!div class="checklist"]
> * Configurar a distribuição global usando Olá portal do Azure
> * Configurar a distribuição global usando Olá APIs do DocumentDB

Você pode continuar toolearn tutorial do próximo toohello como toodevelop localmente usando Olá emulador local do banco de dados do Azure Cosmos.

> [!div class="nextstepaction"]
> [Desenvolva localmente com o emulador de saudação](local-emulator.md)
