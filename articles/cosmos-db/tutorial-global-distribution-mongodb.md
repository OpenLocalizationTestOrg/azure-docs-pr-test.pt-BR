---
title: "Tutorial de distribuição global do Azure Cosmos DB para a API do MongoDB | Microsoft Docs"
description: "Saiba como configurar a distribuição global do Azure Cosmos DB usando a API do MongoDB."
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
ms.openlocfilehash: a2747102f4d8cac412b67abc3fd07cfa3661bcee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-mongodb-api"></a><span data-ttu-id="4fddd-104">Como configurar a distribuição global do Azure Cosmos DB usando a API do MongoDB</span><span class="sxs-lookup"><span data-stu-id="4fddd-104">How to setup Azure Cosmos DB global distribution using the MongoDB API</span></span>

<span data-ttu-id="4fddd-105">Neste artigo, mostraremos como usar o Portal do Azure para configurar a distribuição global do Azure Cosmos DB e, depois, conectar-se usando a API do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4fddd-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the MongoDB API.</span></span>

<span data-ttu-id="4fddd-106">Este artigo aborda as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="4fddd-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="4fddd-107">Configurar a distribuição global usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4fddd-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="4fddd-108">Configurar a distribuição global usando a [API do MongoDB](mongodb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="4fddd-108">Configure global distribution using the [MongoDB API](mongodb-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-the-mongodb-api"></a><span data-ttu-id="4fddd-109">Verificar a configuração regional usando a API do MongoDB</span><span class="sxs-lookup"><span data-stu-id="4fddd-109">Verifying your regional setup using the MongoDB API</span></span>
<span data-ttu-id="4fddd-110">A maneira mais simples de verificar sua configuração global dentro de API para MongoDB é executar o comando *isMaster()* no Shell do Mongo.</span><span class="sxs-lookup"><span data-stu-id="4fddd-110">The simplest way of double checking your global configuration within API for MongoDB is to run the *isMaster()* command from the Mongo Shell.</span></span>

<span data-ttu-id="4fddd-111">No Shell do Mongo:</span><span class="sxs-lookup"><span data-stu-id="4fddd-111">From your Mongo Shell:</span></span>

   ```
      db.isMaster()
   ```
   
<span data-ttu-id="4fddd-112">Exemplos de resultados:</span><span class="sxs-lookup"><span data-stu-id="4fddd-112">Example results:</span></span>

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

## <a name="connecting-to-a-preferred-region-using-the-mongodb-api"></a><span data-ttu-id="4fddd-113">Conectar-se a uma região preferencial usando a API do MongoDB</span><span class="sxs-lookup"><span data-stu-id="4fddd-113">Connecting to a preferred region using the MongoDB API</span></span>

<span data-ttu-id="4fddd-114">A API do MongoDB permite que você especifique a preferência de leitura de sua coleção para um banco de dados distribuído globalmente.</span><span class="sxs-lookup"><span data-stu-id="4fddd-114">The MongoDB API enables you to specify your collection's read preference for a globally distributed database.</span></span> <span data-ttu-id="4fddd-115">Para leituras de baixa latência e alta disponibilidade global, recomendamos a definição de sua preferência de leitura da coleção como *mais próximo*.</span><span class="sxs-lookup"><span data-stu-id="4fddd-115">For both low latency reads and global high availability, we recommend setting your collection's read preference to *nearest*.</span></span> <span data-ttu-id="4fddd-116">Uma preferência de leitura de *mais próximo* está configurada para ler a região mais próxima.</span><span class="sxs-lookup"><span data-stu-id="4fddd-116">A read preference of *nearest* is configured to read from the closest region.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

<span data-ttu-id="4fddd-117">Para aplicativos com uma região de leitura/gravação primária e uma região secundária para cenários de DR (recuperação de desastres), recomendamos a definição da preferência de leitura da coleção como *secundário preferido*.</span><span class="sxs-lookup"><span data-stu-id="4fddd-117">For applications with a primary read/write region and a secondary region for disaster recovery (DR) scenarios, we recommend setting your collection's read preference to *secondary preferred*.</span></span> <span data-ttu-id="4fddd-118">Uma preferência de leitura de *secundário preferido* é configurada para ler a região secundária quando a região primária não está disponível.</span><span class="sxs-lookup"><span data-stu-id="4fddd-118">A read preference of *secondary preferred* is configured to read from the secondary region when the primary region is unavailable.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

<span data-ttu-id="4fddd-119">Por fim, se você quiser especificar manualmente suas regiões de leitura.</span><span class="sxs-lookup"><span data-stu-id="4fddd-119">Lastly, if you would like to manually specify your read regions.</span></span> <span data-ttu-id="4fddd-120">Defina a marca region dentro de sua preferência de leitura.</span><span class="sxs-lookup"><span data-stu-id="4fddd-120">You can set the region Tag within your read preference.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

<span data-ttu-id="4fddd-121">Assim, concluímos este tutorial.</span><span class="sxs-lookup"><span data-stu-id="4fddd-121">That's it, that completes this tutorial.</span></span> <span data-ttu-id="4fddd-122">Aprenda a gerenciar a consistência de sua conta globalmente replicada lendo [Níveis de consistência no Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="4fddd-122">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="4fddd-123">E para saber mais sobre como a replicação de banco de dados global funciona no Azure Cosmos DB, veja [Distribuir dados globalmente com o Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="4fddd-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fddd-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4fddd-124">Next steps</span></span>

<span data-ttu-id="4fddd-125">Neste tutorial, você fez o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4fddd-125">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4fddd-126">Configurar a distribuição global usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4fddd-126">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="4fddd-127">Configurar a distribuição global usando a API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="4fddd-127">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="4fddd-128">Agora você pode prosseguir para o próximo tutorial e aprender a desenvolver localmente usando o emulador local do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4fddd-128">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4fddd-129">Desenvolver localmente com o emulador</span><span class="sxs-lookup"><span data-stu-id="4fddd-129">Develop locally with the emulator</span></span>](local-emulator.md)