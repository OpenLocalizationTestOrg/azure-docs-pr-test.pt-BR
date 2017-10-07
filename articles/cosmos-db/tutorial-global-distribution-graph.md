---
title: "tutorial de distribuição global de banco de dados do Cosmos aaaAzure API do Graph | Microsoft Docs"
description: "Saiba como distribuição global usando o banco de dados do Azure Cosmos toosetup Olá API do Graph."
services: cosmos-db
keywords: "distribuição global, graph, gremlin"
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 1629a31e12a18079f63e07c4909862b36b5f4c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-graph-api"></a><span data-ttu-id="d786c-104">Como a distribuição global usando o banco de dados do Azure Cosmos toosetup Olá API do Graph</span><span class="sxs-lookup"><span data-stu-id="d786c-104">How toosetup Azure Cosmos DB global distribution using hello Graph API</span></span>

<span data-ttu-id="d786c-105">Neste artigo, mostramos como toouse Olá distribuição global do banco de dados do Azure Cosmos toosetup portal do Azure e, em seguida, conecte-se usando Olá Graph API (visualização).</span><span class="sxs-lookup"><span data-stu-id="d786c-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello Graph API (preview).</span></span>

<span data-ttu-id="d786c-106">Este artigo aborda Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d786c-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="d786c-107">Configurar a distribuição global usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d786c-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="d786c-108">Configurar a distribuição global usando Olá [Graph APIs](graph-introduction.md) (visualização)</span><span class="sxs-lookup"><span data-stu-id="d786c-108">Configure global distribution using hello [Graph APIs](graph-introduction.md) (preview)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-graph-api-using-hello-net-sdk"></a><span data-ttu-id="d786c-109">Conectar-se a região preferida tooa usando a API do Graph do hello usando Olá SDK .NET</span><span class="sxs-lookup"><span data-stu-id="d786c-109">Connecting tooa preferred region using hello Graph API using hello .NET SDK</span></span>

<span data-ttu-id="d786c-110">Olá Graph API é exposta como uma biblioteca de extensões sobre Olá SDK do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="d786c-110">hello Graph API is exposed as an extension library on top of hello DocumentDB SDK.</span></span>

<span data-ttu-id="d786c-111">Em ordem tootake aproveitar [distribuição global](distribute-data-globally.md), aplicativos cliente podem especificar Olá ordenados lista de preferência de regiões toobe usada tooperform operações de documento.</span><span class="sxs-lookup"><span data-stu-id="d786c-111">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="d786c-112">Isso pode ser feito definindo a diretiva de conexão hello.</span><span class="sxs-lookup"><span data-stu-id="d786c-112">This can be done by setting hello connection policy.</span></span> <span data-ttu-id="d786c-113">Com base na configuração de conta do banco de dados do Azure Cosmos hello, disponibilidade regional atual e a lista de preferência de saudação especificado, Olá ponto de extremidade mais ideal será escolhido por gravação de tooperform SDK hello e operações de leitura.</span><span class="sxs-lookup"><span data-stu-id="d786c-113">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello SDK tooperform write and read operations.</span></span>

<span data-ttu-id="d786c-114">Esta lista de preferência é especificada durante a inicialização de uma conexão usando Olá SDKs.</span><span class="sxs-lookup"><span data-stu-id="d786c-114">This preference list is specified when initializing a connection using hello SDKs.</span></span> <span data-ttu-id="d786c-115">Olá SDKs aceitar um parâmetro opcional "PreferredLocations" que é uma lista ordenada de regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="d786c-115">hello SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

* <span data-ttu-id="d786c-116">**Grava**: Olá SDK enviará automaticamente todas as gravações toohello região de gravação atual.</span><span class="sxs-lookup"><span data-stu-id="d786c-116">**Writes**: hello SDK will automatically send all writes toohello current write region.</span></span>
* <span data-ttu-id="d786c-117">**Lê**: todas as leituras serão enviadas toohello primeira região disponível na lista de PreferredLocations hello.</span><span class="sxs-lookup"><span data-stu-id="d786c-117">**Reads**: All reads will be sent toohello first available region in hello PreferredLocations list.</span></span> <span data-ttu-id="d786c-118">Se Olá solicitação falhar, o cliente Olá falhar para baixo próxima região do hello lista toohello e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="d786c-118">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span> <span data-ttu-id="d786c-119">Olá SDKs somente tentará tooread de regiões de saudação especificado em PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="d786c-119">hello SDKs will only attempt tooread from hello regions specified in PreferredLocations.</span></span> <span data-ttu-id="d786c-120">Assim, por exemplo, se Olá conta Cosmos DB está disponível em três regiões, mas somente cliente Olá especifica duas regiões de gravação não Olá para PreferredLocations, em seguida, nenhuma leitura será servida fora da região de gravação hello, mesmo no caso de saudação de failover.</span><span class="sxs-lookup"><span data-stu-id="d786c-120">So, for example, if hello Cosmos DB account is available in three regions, but hello client only specifies two of hello non-write regions for PreferredLocations, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="d786c-121">aplicativo Hello pode verificar o ponto de extremidade de gravação atual Olá e ler escolhido pelo Olá SDK pela verificação duas propriedades, WriteEndpoint e ReadEndpoint, disponível no SDK versão 1.8 e acima do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="d786c-121">hello application can verify hello current write endpoint and read endpoint chosen by hello SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span> <span data-ttu-id="d786c-122">Se Olá PreferredLocations propriedade não for definida, todas as solicitações serão atendidas a partir de região de gravação atual hello.</span><span class="sxs-lookup"><span data-stu-id="d786c-122">If hello PreferredLocations property is not set, all requests will be served from hello current write region.</span></span>

### <a name="using-hello-sdk"></a><span data-ttu-id="d786c-123">Usando Olá SDK</span><span class="sxs-lookup"><span data-stu-id="d786c-123">Using hello SDK</span></span>

<span data-ttu-id="d786c-124">Por exemplo, Olá .NET SDK, Olá `ConnectionPolicy` parâmetro hello `DocumentClient` construtor tem uma propriedade chamada `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="d786c-124">For example, in hello .NET SDK, hello `ConnectionPolicy` parameter for hello `DocumentClient` constructor has a property called `PreferredLocations`.</span></span> <span data-ttu-id="d786c-125">Essa propriedade pode ser definida tooa lista de nomes de região.</span><span class="sxs-lookup"><span data-stu-id="d786c-125">This property can be set tooa list of region names.</span></span> <span data-ttu-id="d786c-126">nomes de exibição Olá para [regiões do Azure] [ regions] pode ser especificado como parte de `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="d786c-126">hello display names for [Azure Regions][regions] can be specified as part of `PreferredLocations`.</span></span>

> [!NOTE]
> <span data-ttu-id="d786c-127">Olá URLs para pontos de extremidade de saudação não devem ser consideradas como constantes e longa duração.</span><span class="sxs-lookup"><span data-stu-id="d786c-127">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="d786c-128">serviço de saudação pode atualizar essas a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="d786c-128">hello service may update these at any point.</span></span> <span data-ttu-id="d786c-129">Olá SDK manipula essa alteração automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d786c-129">hello SDK handles this change automatically.</span></span>
>
>

```cs
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;

ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect tooAzure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
```

<span data-ttu-id="d786c-130">Assim, concluímos este tutorial.</span><span class="sxs-lookup"><span data-stu-id="d786c-130">That's it, that completes this tutorial.</span></span> <span data-ttu-id="d786c-131">Você pode aprender como toomanage Olá consistência da sua conta global replicada lendo [níveis de consistência no banco de dados do Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="d786c-131">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="d786c-132">E para saber mais sobre como a replicação de banco de dados global funciona no Azure Cosmos DB, veja [Distribuir dados globalmente com o Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="d786c-132">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d786c-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d786c-133">Next steps</span></span>

<span data-ttu-id="d786c-134">Neste tutorial, você fez a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="d786c-134">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d786c-135">Configurar a distribuição global usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d786c-135">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="d786c-136">Configurar a distribuição global usando Olá APIs do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="d786c-136">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="d786c-137">Você pode continuar toolearn tutorial do próximo toohello como toodevelop localmente usando Olá emulador local do banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d786c-137">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d786c-138">Desenvolva localmente com o emulador de saudação</span><span class="sxs-lookup"><span data-stu-id="d786c-138">Develop locally with hello emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

