---
title: "Tutorial de distribuição global do Azure Cosmos DB para a API do Graph | Microsoft Docs"
description: "Saiba como configurar a distribuição global do Azure Cosmos DB usando a API do Graph."
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
ms.openlocfilehash: 3c8794fe33c2ff5aa79559ea2c323cf8d92b426a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-graph-api"></a><span data-ttu-id="52f13-104">Como configurar a distribuição global do Azure Cosmos DB usando a API do Graph</span><span class="sxs-lookup"><span data-stu-id="52f13-104">How to setup Azure Cosmos DB global distribution using the Graph API</span></span>

<span data-ttu-id="52f13-105">Neste artigo, mostraremos como usar o Portal do Azure para configurar a distribuição global do Azure Cosmos DB e, depois, conectar-se usando a API do Graph (visualização).</span><span class="sxs-lookup"><span data-stu-id="52f13-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the Graph API (preview).</span></span>

<span data-ttu-id="52f13-106">Este artigo aborda as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="52f13-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="52f13-107">Configurar a distribuição global usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="52f13-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="52f13-108">Configurar a distribuição global usando a [API do Graph](graph-introduction.md) (visualização)</span><span class="sxs-lookup"><span data-stu-id="52f13-108">Configure global distribution using the [Graph APIs](graph-introduction.md) (preview)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-graph-api-using-the-net-sdk"></a><span data-ttu-id="52f13-109">Conectar-se a uma região preferencial usando a API do Graph com o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="52f13-109">Connecting to a preferred region using the Graph API using the .NET SDK</span></span>

<span data-ttu-id="52f13-110">A API do Graph é exposta como uma biblioteca de extensão sobre o SDK do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="52f13-110">The Graph API is exposed as an extension library on top of the DocumentDB SDK.</span></span>

<span data-ttu-id="52f13-111">Para aproveitar a [distribuição global](distribute-data-globally.md), os aplicativos cliente podem especificar a lista de preferências ordenadas de regiões a serem usadas para executar operações de documento.</span><span class="sxs-lookup"><span data-stu-id="52f13-111">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="52f13-112">Isso pode ser feito definindo a política de conexão.</span><span class="sxs-lookup"><span data-stu-id="52f13-112">This can be done by setting the connection policy.</span></span> <span data-ttu-id="52f13-113">Com base na configuração da conta do Azure Cosmos DB, na disponibilidade regional atual e na lista de preferências especificada, o ponto de extremidade mais adequado será escolhido pelo SDK para executar operações de gravação e leitura.</span><span class="sxs-lookup"><span data-stu-id="52f13-113">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the SDK to perform write and read operations.</span></span>

<span data-ttu-id="52f13-114">Essa lista de preferências é especificada ao inicializar uma conexão usando os SDKs.</span><span class="sxs-lookup"><span data-stu-id="52f13-114">This preference list is specified when initializing a connection using the SDKs.</span></span> <span data-ttu-id="52f13-115">Os SDKs aceitam um parâmetro opcional "PreferredLocations", que é uma lista ordenada de regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="52f13-115">The SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

* <span data-ttu-id="52f13-116">**Gravações**: o SDK enviará automaticamente todas as gravações para a região de gravação atual.</span><span class="sxs-lookup"><span data-stu-id="52f13-116">**Writes**: The SDK will automatically send all writes to the current write region.</span></span>
* <span data-ttu-id="52f13-117">**Leituras**: todas as leituras serão enviadas para a primeira região disponível na lista PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="52f13-117">**Reads**: All reads will be sent to the first available region in the PreferredLocations list.</span></span> <span data-ttu-id="52f13-118">Se a solicitação falhar, o cliente não fará o envio para a próxima região da lista, e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="52f13-118">If the request fails, the client will fail down the list to the next region, and so on.</span></span> <span data-ttu-id="52f13-119">Os SDKs tentarão ler apenas das regiões especificadas em PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="52f13-119">The SDKs will only attempt to read from the regions specified in PreferredLocations.</span></span> <span data-ttu-id="52f13-120">Desse modo, se a Conta do CosmosDB estiver disponível em três regiões, por exemplo, mas o cliente especificar apenas duas das regiões de não gravação para PreferredLocations, nenhuma leitura será atendida fora da região de gravação, mesmo no caso de failover.</span><span class="sxs-lookup"><span data-stu-id="52f13-120">So, for example, if the Cosmos DB account is available in three regions, but the client only specifies two of the non-write regions for PreferredLocations, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="52f13-121">O aplicativo pode verificar o ponto de extremidade de gravação e o ponto de extremidade de leitura atuais escolhidos pelo SDK marcando duas propriedades, WriteEndpoint e ReadEndpoint, disponíveis no SDK versão 1.8 e superiores.</span><span class="sxs-lookup"><span data-stu-id="52f13-121">The application can verify the current write endpoint and read endpoint chosen by the SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span> <span data-ttu-id="52f13-122">Se a propriedade PreferredLocations não estiver definida, todas as solicitações serão atendidas na região de gravação atual.</span><span class="sxs-lookup"><span data-stu-id="52f13-122">If the PreferredLocations property is not set, all requests will be served from the current write region.</span></span>

### <a name="using-the-sdk"></a><span data-ttu-id="52f13-123">Usar o SDK</span><span class="sxs-lookup"><span data-stu-id="52f13-123">Using the SDK</span></span>

<span data-ttu-id="52f13-124">Por exemplo, no SDK do .NET, o parâmetro `ConnectionPolicy` para o construtor `DocumentClient` tem uma propriedade chamada `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="52f13-124">For example, in the .NET SDK, the `ConnectionPolicy` parameter for the `DocumentClient` constructor has a property called `PreferredLocations`.</span></span> <span data-ttu-id="52f13-125">Essa propriedade pode ser definida para uma lista de nomes de região.</span><span class="sxs-lookup"><span data-stu-id="52f13-125">This property can be set to a list of region names.</span></span> <span data-ttu-id="52f13-126">Os nomes de exibição para [Regiões do Azure][regions] podem ser especificados como parte de `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="52f13-126">The display names for [Azure Regions][regions] can be specified as part of `PreferredLocations`.</span></span>

> [!NOTE]
> <span data-ttu-id="52f13-127">As URLs para os pontos de extremidade não devem ser consideradas como constantes de vida longa.</span><span class="sxs-lookup"><span data-stu-id="52f13-127">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="52f13-128">O serviço pode atualizá-las a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="52f13-128">The service may update these at any point.</span></span> <span data-ttu-id="52f13-129">O SDK lida com essa alteração automaticamente.</span><span class="sxs-lookup"><span data-stu-id="52f13-129">The SDK handles this change automatically.</span></span>
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

// connect to Azure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
```

<span data-ttu-id="52f13-130">Assim, concluímos este tutorial.</span><span class="sxs-lookup"><span data-stu-id="52f13-130">That's it, that completes this tutorial.</span></span> <span data-ttu-id="52f13-131">Aprenda a gerenciar a consistência de sua conta globalmente replicada lendo [Níveis de consistência no Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="52f13-131">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="52f13-132">E para saber mais sobre como a replicação de banco de dados global funciona no Azure Cosmos DB, veja [Distribuir dados globalmente com o Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="52f13-132">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="52f13-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="52f13-133">Next steps</span></span>

<span data-ttu-id="52f13-134">Neste tutorial, você fez o seguinte:</span><span class="sxs-lookup"><span data-stu-id="52f13-134">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="52f13-135">Configurar a distribuição global usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="52f13-135">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="52f13-136">Configurar a distribuição global usando a API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="52f13-136">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="52f13-137">Agora você pode prosseguir para o próximo tutorial e aprender a desenvolver localmente usando o emulador local do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="52f13-137">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="52f13-138">Desenvolver localmente com o emulador</span><span class="sxs-lookup"><span data-stu-id="52f13-138">Develop locally with the emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

