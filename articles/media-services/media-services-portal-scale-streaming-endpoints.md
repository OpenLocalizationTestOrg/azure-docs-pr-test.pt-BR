---
title: Dimensionar pontos de extremidade de streaming com o portal do Azure | Microsoft Docs
description: "Este tutorial orienta você pelas etapas de dimensionar pontos de extremidade de streaming usando o portal do Azure."
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
ms.openlocfilehash: 4bb891371e3fc802fa667688a88878db18e32422
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="scale-streaming-endpoints-with-the-azure-portal"></a><span data-ttu-id="e2d66-103">Dimensionar pontos de extremidade de streaming com o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e2d66-103">Scale streaming endpoints with the Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="e2d66-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e2d66-104">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="e2d66-105">Para concluir este tutorial, você precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2d66-105">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="e2d66-106">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e2d66-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="e2d66-107">Os pontos de extremidade de streaming **Premium** são adequados para cargas de trabalho avançadas, fornecendo capacidade de largura de banda escalonável e dedicada.</span><span class="sxs-lookup"><span data-stu-id="e2d66-107">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="e2d66-108">Os clientes que têm um ponto de extremidade de streaming **Premium**, por padrão, obtêm uma US (Unidade de Streaming).</span><span class="sxs-lookup"><span data-stu-id="e2d66-108">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="e2d66-109">O ponto de extremidade de streaming pode ser dimensionado adicionando USs.</span><span class="sxs-lookup"><span data-stu-id="e2d66-109">The streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="e2d66-110">Cada SU fornece uma capacidade de largura de banda adicional para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e2d66-110">Each SU provides additional bandwidth capacity to the application.</span></span> <span data-ttu-id="e2d66-111">Para saber mais sobre tipos de ponto de extremidade de streaming e configuração de CDN, confira o tópico [Visão geral do Ponto de Extremidade do Streaming](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="e2d66-111">For more information about streaming endpoint types and CDN configuration, see the [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) topic.</span></span>
 
<span data-ttu-id="e2d66-112">Este tópico mostra como dimensionar um ponto de extremidade de streaming.</span><span class="sxs-lookup"><span data-stu-id="e2d66-112">This topic shows how to scale a streaming endpoint.</span></span>

<span data-ttu-id="e2d66-113">Para saber mais sobre os detalhes de preços, consulte [Detalhes de preços dos Serviços de Mídia](http://go.microsoft.com/fwlink/?LinkId=275107).</span><span class="sxs-lookup"><span data-stu-id="e2d66-113">For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).</span></span>

## <a name="scale-streaming-endpoints"></a><span data-ttu-id="e2d66-114">Dimensionar pontos de extremidade de streaming</span><span class="sxs-lookup"><span data-stu-id="e2d66-114">Scale streaming endpoints</span></span>

<span data-ttu-id="e2d66-115">Para alterar o número de unidades de streaming, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e2d66-115">To change the number of streaming units, do the following:</span></span>

1. <span data-ttu-id="e2d66-116">No [Portal do Azure](https://portal.azure.com/), selecione sua conta dos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2d66-116">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="e2d66-117">Na janela **Configurações**, selecione **Pontos de extremidade de streaming**.</span><span class="sxs-lookup"><span data-stu-id="e2d66-117">In the **Settings** window, select **Streaming endpoints**.</span></span>
3. <span data-ttu-id="e2d66-118">Clique no ponto de extremidade de streaming que você deseja dimensionar.</span><span class="sxs-lookup"><span data-stu-id="e2d66-118">Click on the streaming endpoint that you want to scale.</span></span> 

    [!NOTE] <span data-ttu-id="e2d66-119">É possível dimensionar apenas pontos de extremidade de streaming **Premium**.</span><span class="sxs-lookup"><span data-stu-id="e2d66-119">You can only scale **Premium** streaming endpoints.</span></span>

4. <span data-ttu-id="e2d66-120">Mova o controle deslizante para especificar o número de unidades de streaming.</span><span class="sxs-lookup"><span data-stu-id="e2d66-120">Move the slider to specify the number of streaming units.</span></span>

    ![ponto de extremidade de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a><span data-ttu-id="e2d66-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e2d66-122">Next steps</span></span>
<span data-ttu-id="e2d66-123">Examine os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="e2d66-123">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e2d66-124">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="e2d66-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

