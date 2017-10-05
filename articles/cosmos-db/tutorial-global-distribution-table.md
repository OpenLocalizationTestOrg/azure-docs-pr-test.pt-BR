---
title: "Tutorial de distribuição global do Azure Cosmos DB para a API de Tabela | Microsoft Docs"
description: "Saiba como configurar a distribuição global do Azure Cosmos DB usando a API de Tabela."
services: cosmos-db
keywords: "distribuição global, Tabela"
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
ms.openlocfilehash: 63c9e530a4982e2e6e478fea56e015fc77851e1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-table-api"></a><span data-ttu-id="43ebb-104">Como configurar a distribuição global do Azure Cosmos DB usando a API de Tabela</span><span class="sxs-lookup"><span data-stu-id="43ebb-104">How to setup Azure Cosmos DB global distribution using the Table API</span></span>

<span data-ttu-id="43ebb-105">Neste artigo, mostraremos como usar o Portal do Azure para configurar a distribuição global do Azure Cosmos DB e, depois, conectar-se usando a API de Tabela (visualização).</span><span class="sxs-lookup"><span data-stu-id="43ebb-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the Table API (preview).</span></span>

<span data-ttu-id="43ebb-106">Este artigo aborda as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="43ebb-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="43ebb-107">Configurar a distribuição global usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="43ebb-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="43ebb-108">Configurar a distribuição global usando a [API de Tabela](table-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="43ebb-108">Configure global distribution using the [Table API](table-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-table-api"></a><span data-ttu-id="43ebb-109">Conectar-se a uma região preferencial usando a API de Tabela</span><span class="sxs-lookup"><span data-stu-id="43ebb-109">Connecting to a preferred region using the Table API</span></span>

<span data-ttu-id="43ebb-110">Para aproveitar a [distribuição global](distribute-data-globally.md), os aplicativos cliente podem especificar a lista de preferências ordenadas de regiões a serem usadas para executar operações de documento.</span><span class="sxs-lookup"><span data-stu-id="43ebb-110">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="43ebb-111">Isso pode ser feito definindo o valor de configuração `TablePreferredLocations` na configuração do aplicativo para a visualização do SDK do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="43ebb-111">This can be done by setting the `TablePreferredLocations` configuration value in the app config for the preview Azure Storage SDK.</span></span> <span data-ttu-id="43ebb-112">Com base na configuração da conta do Azure Cosmos DB, na disponibilidade regional atual e na lista de preferências especificada, o ponto de extremidade mais adequado será escolhido pelo SDK de Armazenamento do Azure para executar operações de gravação e leitura.</span><span class="sxs-lookup"><span data-stu-id="43ebb-112">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the Azure Storage SDK to perform write and read operations.</span></span>

<span data-ttu-id="43ebb-113">O `TablePreferredLocations` deve conter uma lista separada por vírgulas de locais (hospedagem múltipla) preferenciais para leituras.</span><span class="sxs-lookup"><span data-stu-id="43ebb-113">The `TablePreferredLocations` should contain a comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="43ebb-114">Cada instância do cliente pode especificar um subconjunto dessas regiões na ordem preferida para leituras de baixa latência.</span><span class="sxs-lookup"><span data-stu-id="43ebb-114">Each client instance can specify a subset of these regions in the preferred order for low latency reads.</span></span> <span data-ttu-id="43ebb-115">As regiões devem ser nomeadas usando seus [nomes de exibição](https://msdn.microsoft.com/library/azure/gg441293.aspx), por exemplo, `West US`.</span><span class="sxs-lookup"><span data-stu-id="43ebb-115">The regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span>

<span data-ttu-id="43ebb-116">Todas as leituras serão enviadas para a primeira região disponível na lista `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="43ebb-116">All reads will be sent to the first available region in the `TablePreferredLocations` list.</span></span> <span data-ttu-id="43ebb-117">Se a solicitação falhar, o cliente não fará o envio para a próxima região da lista, e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="43ebb-117">If the request fails, the client will fail down the list to the next region, and so on.</span></span>

<span data-ttu-id="43ebb-118">Os SDKs tentarão ler apenas das regiões especificadas em `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="43ebb-118">The SDK will only attempt to read from the regions specified in `TablePreferredLocations`.</span></span> <span data-ttu-id="43ebb-119">Desse modo, se a Conta do Banco de Dados estiver disponível em três regiões, por exemplo, mas o cliente especificar apenas duas das regiões de não gravação para `TablePreferredLocations`, nenhuma leitura será atendida fora da região de gravação, mesmo no caso de failover.</span><span class="sxs-lookup"><span data-stu-id="43ebb-119">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for `TablePreferredLocations`, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="43ebb-120">O SDK enviará automaticamente todas as gravações para a região de gravação atual.</span><span class="sxs-lookup"><span data-stu-id="43ebb-120">The SDK will automatically send all writes to the current write region.</span></span>

<span data-ttu-id="43ebb-121">Se a propriedade `TablePreferredLocations` não estiver definida, todas as solicitações serão atendidas na região de gravação atual.</span><span class="sxs-lookup"><span data-stu-id="43ebb-121">If the `TablePreferredLocations` property is not set, all requests will be served from the current write region.</span></span>

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

<span data-ttu-id="43ebb-122">Assim, concluímos este tutorial.</span><span class="sxs-lookup"><span data-stu-id="43ebb-122">That's it, that completes this tutorial.</span></span> <span data-ttu-id="43ebb-123">Aprenda a gerenciar a consistência de sua conta globalmente replicada lendo [Níveis de consistência no Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="43ebb-123">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="43ebb-124">E para saber mais sobre como a replicação de banco de dados global funciona no Azure Cosmos DB, veja [Distribuir dados globalmente com o Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="43ebb-124">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="43ebb-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="43ebb-125">Next steps</span></span>

<span data-ttu-id="43ebb-126">Neste tutorial, você fez o seguinte:</span><span class="sxs-lookup"><span data-stu-id="43ebb-126">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="43ebb-127">Configurar a distribuição global usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="43ebb-127">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="43ebb-128">Configurar a distribuição global usando a API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="43ebb-128">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="43ebb-129">Agora você pode prosseguir para o próximo tutorial e aprender a desenvolver localmente usando o emulador local do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="43ebb-129">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="43ebb-130">Desenvolver localmente com o emulador</span><span class="sxs-lookup"><span data-stu-id="43ebb-130">Develop locally with the emulator</span></span>](local-emulator.md)