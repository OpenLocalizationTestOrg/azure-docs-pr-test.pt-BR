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
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-mongodb-api"></a><span data-ttu-id="bbd79-104">Como a distribuição global usando o banco de dados do Azure Cosmos toosetup Olá MongoDB API</span><span class="sxs-lookup"><span data-stu-id="bbd79-104">How toosetup Azure Cosmos DB global distribution using hello MongoDB API</span></span>

<span data-ttu-id="bbd79-105">Neste artigo, mostramos como toouse Olá toosetup portal do Azure distribuição global do banco de dados do Azure Cosmos e, em seguida, conecte-se usando Olá MongoDB API.</span><span class="sxs-lookup"><span data-stu-id="bbd79-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello MongoDB API.</span></span>

<span data-ttu-id="bbd79-106">Este artigo aborda Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="bbd79-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="bbd79-107">Configurar a distribuição global usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bbd79-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="bbd79-108">Configurar a distribuição global usando Olá [API do MongoDB](mongodb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="bbd79-108">Configure global distribution using hello [MongoDB API](mongodb-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-hello-mongodb-api"></a><span data-ttu-id="bbd79-109">Verificando a configuração regional usando Olá MongoDB API</span><span class="sxs-lookup"><span data-stu-id="bbd79-109">Verifying your regional setup using hello MongoDB API</span></span>
<span data-ttu-id="bbd79-110">a maneira mais simples de saudação de duplo verificando sua configuração global dentro de API para o MongoDB é Olá toorun *isMaster()* comando Olá Shell Mongo.</span><span class="sxs-lookup"><span data-stu-id="bbd79-110">hello simplest way of double checking your global configuration within API for MongoDB is toorun hello *isMaster()* command from hello Mongo Shell.</span></span>

<span data-ttu-id="bbd79-111">No Shell do Mongo:</span><span class="sxs-lookup"><span data-stu-id="bbd79-111">From your Mongo Shell:</span></span>

   ```
      db.isMaster()
   ```
   
<span data-ttu-id="bbd79-112">Exemplos de resultados:</span><span class="sxs-lookup"><span data-stu-id="bbd79-112">Example results:</span></span>

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

## <a name="connecting-tooa-preferred-region-using-hello-mongodb-api"></a><span data-ttu-id="bbd79-113">Conectar-se a região preferida tooa usando Olá MongoDB API</span><span class="sxs-lookup"><span data-stu-id="bbd79-113">Connecting tooa preferred region using hello MongoDB API</span></span>

<span data-ttu-id="bbd79-114">Olá MongoDB API permite que você toospecify preferência de leitura da coleção para um banco de dados globalmente distribuído.</span><span class="sxs-lookup"><span data-stu-id="bbd79-114">hello MongoDB API enables you toospecify your collection's read preference for a globally distributed database.</span></span> <span data-ttu-id="bbd79-115">Para ambos baixa leituras de latência e alta disponibilidade global, é recomendável definir preferência de leitura da coleção muito*mais próximo*.</span><span class="sxs-lookup"><span data-stu-id="bbd79-115">For both low latency reads and global high availability, we recommend setting your collection's read preference too*nearest*.</span></span> <span data-ttu-id="bbd79-116">Uma preferência de leitura de *mais próximo* é configurado tooread da região mais próxima hello.</span><span class="sxs-lookup"><span data-stu-id="bbd79-116">A read preference of *nearest* is configured tooread from hello closest region.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

<span data-ttu-id="bbd79-117">Para aplicativos com um primário leitura/gravação região e uma região secundária para a recuperação de desastres (DR) cenários, é recomendável definir preferência de leitura da coleção muito*secundário preferido*.</span><span class="sxs-lookup"><span data-stu-id="bbd79-117">For applications with a primary read/write region and a secondary region for disaster recovery (DR) scenarios, we recommend setting your collection's read preference too*secondary preferred*.</span></span> <span data-ttu-id="bbd79-118">Uma preferência de leitura de *secundário preferido* é configurado tooread da região secundária hello quando a região primária Olá não está disponível.</span><span class="sxs-lookup"><span data-stu-id="bbd79-118">A read preference of *secondary preferred* is configured tooread from hello secondary region when hello primary region is unavailable.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

<span data-ttu-id="bbd79-119">Por fim, se você como toomanually especificaria as regiões de leitura.</span><span class="sxs-lookup"><span data-stu-id="bbd79-119">Lastly, if you would like toomanually specify your read regions.</span></span> <span data-ttu-id="bbd79-120">Você pode definir a região Olá marca dentro de sua preferência de leitura.</span><span class="sxs-lookup"><span data-stu-id="bbd79-120">You can set hello region Tag within your read preference.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

<span data-ttu-id="bbd79-121">Assim, concluímos este tutorial.</span><span class="sxs-lookup"><span data-stu-id="bbd79-121">That's it, that completes this tutorial.</span></span> <span data-ttu-id="bbd79-122">Você pode aprender como toomanage Olá consistência da sua conta global replicada lendo [níveis de consistência no banco de dados do Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="bbd79-122">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="bbd79-123">E para saber mais sobre como a replicação de banco de dados global funciona no Azure Cosmos DB, veja [Distribuir dados globalmente com o Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="bbd79-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbd79-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bbd79-124">Next steps</span></span>

<span data-ttu-id="bbd79-125">Neste tutorial, você fez a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="bbd79-125">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bbd79-126">Configurar a distribuição global usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bbd79-126">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="bbd79-127">Configurar a distribuição global usando Olá APIs do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="bbd79-127">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="bbd79-128">Você pode continuar toolearn tutorial do próximo toohello como toodevelop localmente usando Olá emulador local do banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bbd79-128">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bbd79-129">Desenvolva localmente com o emulador de saudação</span><span class="sxs-lookup"><span data-stu-id="bbd79-129">Develop locally with hello emulator</span></span>](local-emulator.md)
