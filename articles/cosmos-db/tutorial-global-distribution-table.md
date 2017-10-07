---
title: "tutorial de distribuição global aaaAzure Cosmos DB para a tabela de API | Microsoft Docs"
description: "Saiba como distribuição global usando o banco de dados do Azure Cosmos toosetup Olá API de tabela."
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
ms.openlocfilehash: d2a995e09c37f9449856aef2ab707e95eb8a540c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-table-api"></a><span data-ttu-id="3ae7d-104">Como a distribuição global usando o banco de dados do Azure Cosmos toosetup Olá API de tabela</span><span class="sxs-lookup"><span data-stu-id="3ae7d-104">How toosetup Azure Cosmos DB global distribution using hello Table API</span></span>

<span data-ttu-id="3ae7d-105">Neste artigo, mostramos como toouse Olá distribuição global do banco de dados do Azure Cosmos toosetup portal do Azure e, em seguida, conecte-se usando Olá API de tabela (visualização).</span><span class="sxs-lookup"><span data-stu-id="3ae7d-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello Table API (preview).</span></span>

<span data-ttu-id="3ae7d-106">Este artigo aborda Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ae7d-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="3ae7d-107">Configurar a distribuição global usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3ae7d-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="3ae7d-108">Configurar a distribuição global usando Olá [API de tabela](table-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="3ae7d-108">Configure global distribution using hello [Table API](table-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-table-api"></a><span data-ttu-id="3ae7d-109">Conectar-se a região preferida tooa usando Olá API de tabela</span><span class="sxs-lookup"><span data-stu-id="3ae7d-109">Connecting tooa preferred region using hello Table API</span></span>

<span data-ttu-id="3ae7d-110">Em ordem tootake aproveitar [distribuição global](distribute-data-globally.md), aplicativos cliente podem especificar Olá ordenados lista de preferência de regiões toobe usada tooperform operações de documento.</span><span class="sxs-lookup"><span data-stu-id="3ae7d-110">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="3ae7d-111">Isso pode ser feito por configuração Olá `TablePreferredLocations` valor de configuração na configuração de aplicativo hello para visualização Olá SDK de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ae7d-111">This can be done by setting hello `TablePreferredLocations` configuration value in hello app config for hello preview Azure Storage SDK.</span></span> <span data-ttu-id="3ae7d-112">Com base na configuração de conta do banco de dados do Azure Cosmos hello, disponibilidade regional atual e a lista de preferência de saudação especificado, Olá ponto de extremidade mais ideal será escolhido por hello Azure Storage SDK tooperform gravam e operações de leitura.</span><span class="sxs-lookup"><span data-stu-id="3ae7d-112">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello Azure Storage SDK tooperform write and read operations.</span></span>

<span data-ttu-id="3ae7d-113">Olá `TablePreferredLocations` deve conter uma lista separada por vírgulas de locais (múltipla) preferenciais para leituras.</span><span class="sxs-lookup"><span data-stu-id="3ae7d-113">hello `TablePreferredLocations` should contain a comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="3ae7d-114">Cada instância de cliente pode especificar um subconjunto dessas regiões Olá preferido para leituras de baixa latência.</span><span class="sxs-lookup"><span data-stu-id="3ae7d-114">Each client instance can specify a subset of these regions in hello preferred order for low latency reads.</span></span> <span data-ttu-id="3ae7d-115">regiões de saudação devem ser nomeados usando seus [exibir nomes](https://msdn.microsoft.com/library/azure/gg441293.aspx), por exemplo, `West US`.</span><span class="sxs-lookup"><span data-stu-id="3ae7d-115">hello regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span>

<span data-ttu-id="3ae7d-116">Todas as leituras serão enviadas toohello primeira região disponível em Olá `TablePreferredLocations` lista.</span><span class="sxs-lookup"><span data-stu-id="3ae7d-116">All reads will be sent toohello first available region in hello `TablePreferredLocations` list.</span></span> <span data-ttu-id="3ae7d-117">Se Olá solicitação falhar, o cliente Olá falhar para baixo próxima região do hello lista toohello e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="3ae7d-117">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span>

<span data-ttu-id="3ae7d-118">Olá SDK somente tentará tooread de regiões de saudação especificado em `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="3ae7d-118">hello SDK will only attempt tooread from hello regions specified in `TablePreferredLocations`.</span></span> <span data-ttu-id="3ae7d-119">Portanto, por exemplo, se Olá conta de banco de dados está disponível em três regiões, mas o cliente Olá especifica apenas duas das Olá regiões não-gravação para `TablePreferredLocations`, e nenhuma leitura será servida fora da região de gravação hello, mesmo no caso de saudação de failover.</span><span class="sxs-lookup"><span data-stu-id="3ae7d-119">So, for example, if hello Database Account is available in three regions, but hello client only specifies two of hello non-write regions for `TablePreferredLocations`, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="3ae7d-120">Olá SDK enviará automaticamente todas as gravações toohello gravação região atual.</span><span class="sxs-lookup"><span data-stu-id="3ae7d-120">hello SDK will automatically send all writes toohello current write region.</span></span>

<span data-ttu-id="3ae7d-121">Se hello `TablePreferredLocations` propriedade não for definida, todas as solicitações serão atendidas a partir de região de gravação atual hello.</span><span class="sxs-lookup"><span data-stu-id="3ae7d-121">If hello `TablePreferredLocations` property is not set, all requests will be served from hello current write region.</span></span>

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

<span data-ttu-id="3ae7d-122">Assim, concluímos este tutorial.</span><span class="sxs-lookup"><span data-stu-id="3ae7d-122">That's it, that completes this tutorial.</span></span> <span data-ttu-id="3ae7d-123">Você pode aprender como toomanage Olá consistência da sua conta global replicada lendo [níveis de consistência no banco de dados do Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="3ae7d-123">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="3ae7d-124">E para saber mais sobre como a replicação de banco de dados global funciona no Azure Cosmos DB, veja [Distribuir dados globalmente com o Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="3ae7d-124">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ae7d-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3ae7d-125">Next steps</span></span>

<span data-ttu-id="3ae7d-126">Neste tutorial, você fez a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="3ae7d-126">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3ae7d-127">Configurar a distribuição global usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3ae7d-127">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="3ae7d-128">Configurar a distribuição global usando Olá APIs do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="3ae7d-128">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="3ae7d-129">Você pode continuar toolearn tutorial do próximo toohello como toodevelop localmente usando Olá emulador local do banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="3ae7d-129">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3ae7d-130">Desenvolva localmente com o emulador de saudação</span><span class="sxs-lookup"><span data-stu-id="3ae7d-130">Develop locally with hello emulator</span></span>](local-emulator.md)
