---
title: aaaScale streaming pontos de extremidade com hello portal do Azure | Microsoft Docs
description: "Este tutorial orienta você pelas etapas de saudação do dimensionamento de pontos de extremidade de streaming com hello portal do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1008b3a3-2fa1-4146-85bd-2cf43cd1e00e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: e466edf9232558b9e270f54ee2849cd9b22ad121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-streaming-endpoints-with-hello-azure-portal"></a><span data-ttu-id="db287-103">Dimensionar pontos de extremidade de streaming com hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="db287-103">Scale streaming endpoints with hello Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="db287-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="db287-104">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="db287-105">toocomplete neste tutorial, você precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="db287-105">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="db287-106">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="db287-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="db287-107">Os pontos de extremidade de streaming **Premium** são adequados para cargas de trabalho avançadas, fornecendo capacidade de largura de banda escalonável e dedicada.</span><span class="sxs-lookup"><span data-stu-id="db287-107">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="db287-108">Os clientes que têm um ponto de extremidade de streaming **Premium**, por padrão, obtêm uma US (Unidade de Streaming).</span><span class="sxs-lookup"><span data-stu-id="db287-108">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="db287-109">saudação de ponto de extremidade de streaming pode ser dimensionada adicionando SUs.</span><span class="sxs-lookup"><span data-stu-id="db287-109">hello streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="db287-110">Cada SU fornece capacidade de largura de banda adicional toohello de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="db287-110">Each SU provides additional bandwidth capacity toohello application.</span></span> <span data-ttu-id="db287-111">Para obter mais informações sobre a configuração de CDN e os tipos de ponto de extremidade de streaming, consulte Olá [visão geral de ponto de extremidade de Streaming](media-services-portal-manage-streaming-endpoints.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="db287-111">For more information about streaming endpoint types and CDN configuration, see hello [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) topic.</span></span>
 
<span data-ttu-id="db287-112">Este tópico mostra como tooscale um ponto de extremidade de streaming.</span><span class="sxs-lookup"><span data-stu-id="db287-112">This topic shows how tooscale a streaming endpoint.</span></span>

<span data-ttu-id="db287-113">Para saber mais sobre os detalhes de preços, consulte [Detalhes de preços dos Serviços de Mídia](http://go.microsoft.com/fwlink/?LinkId=275107).</span><span class="sxs-lookup"><span data-stu-id="db287-113">For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).</span></span>

## <a name="scale-streaming-endpoints"></a><span data-ttu-id="db287-114">Dimensionar pontos de extremidade de streaming</span><span class="sxs-lookup"><span data-stu-id="db287-114">Scale streaming endpoints</span></span>

<span data-ttu-id="db287-115">número de saudação toochange de unidades de streaming, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="db287-115">toochange hello number of streaming units, do hello following:</span></span>

1. <span data-ttu-id="db287-116">Em Olá [portal do Azure](https://portal.azure.com/), selecione sua conta de serviços de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="db287-116">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="db287-117">Em Olá **configurações** janela, selecione **pontos de extremidade de Streaming**.</span><span class="sxs-lookup"><span data-stu-id="db287-117">In hello **Settings** window, select **Streaming endpoints**.</span></span>
3. <span data-ttu-id="db287-118">Clique no ponto de extremidade de streaming do hello que você deseja tooscale.</span><span class="sxs-lookup"><span data-stu-id="db287-118">Click on hello streaming endpoint that you want tooscale.</span></span> 

    [!NOTE] <span data-ttu-id="db287-119">É possível dimensionar apenas pontos de extremidade de streaming **Premium**.</span><span class="sxs-lookup"><span data-stu-id="db287-119">You can only scale **Premium** streaming endpoints.</span></span>

4. <span data-ttu-id="db287-120">Mova o número de saudação do hello controle deslizante toospecify de unidades de streaming.</span><span class="sxs-lookup"><span data-stu-id="db287-120">Move hello slider toospecify hello number of streaming units.</span></span>

    ![ponto de extremidade de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a><span data-ttu-id="db287-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="db287-122">Next steps</span></span>
<span data-ttu-id="db287-123">Examine os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="db287-123">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="db287-124">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="db287-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

