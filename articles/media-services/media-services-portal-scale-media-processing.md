---
title: "Dimensionar o processamento de mídia usando o portal do Azure | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas do dimensionamento do processamento de mídia usando o portal do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 46ca29d3e66701f2abcb185791089e94761984e8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="change-the-reserved-unit-type"></a><span data-ttu-id="4f166-103">Alterar o tipo de unidade reservada</span><span class="sxs-lookup"><span data-stu-id="4f166-103">Change the reserved unit type</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4f166-104">.NET</span><span class="sxs-lookup"><span data-stu-id="4f166-104">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="4f166-105">Portal</span><span class="sxs-lookup"><span data-stu-id="4f166-105">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="4f166-106">REST</span><span class="sxs-lookup"><span data-stu-id="4f166-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="4f166-107">Java</span><span class="sxs-lookup"><span data-stu-id="4f166-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="4f166-108">PHP</span><span class="sxs-lookup"><span data-stu-id="4f166-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="4f166-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4f166-109">Overview</span></span>

<span data-ttu-id="4f166-110">Uma conta dos Serviços de Mídia está associada a um Tipo de Unidade Reservada que determina a velocidade com que as suas tarefas de processamento de mídia são processadas.</span><span class="sxs-lookup"><span data-stu-id="4f166-110">A Media Services account is associated with a Reserved Unit Type, which determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="4f166-111">Você pode escolher entre os seguintes tipos de unidade reservada: **S1**, **S2** ou **S3**.</span><span class="sxs-lookup"><span data-stu-id="4f166-111">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="4f166-112">Por exemplo, o mesmo trabalho de codificação é executado mais rapidamente quando você usa o tipo de unidade reservada **S2** em comparação ao tipo **S1**.</span><span class="sxs-lookup"><span data-stu-id="4f166-112">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span></span>

<span data-ttu-id="4f166-113">Além de especificar o tipo de unidade reservada, você pode especificar o provisionamento de sua conta com as **URs** (Unidades Reservadas).</span><span class="sxs-lookup"><span data-stu-id="4f166-113">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="4f166-114">O número de URs provisionadas determina o número de tarefas de mídia que podem ser processadas simultaneamente em determinada conta.</span><span class="sxs-lookup"><span data-stu-id="4f166-114">The number of provisioned RUs determines the number of media tasks that can be processed concurrently in a given account.</span></span>

>[!NOTE]
><span data-ttu-id="4f166-115">As URs trabalham para paralelizar todo o processamento de mídia, incluindo os trabalhos de indexação, usando o Azure Media Indexer.</span><span class="sxs-lookup"><span data-stu-id="4f166-115">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="4f166-116">No entanto, ao contrário da codificação, a indexação de trabalhos não será processada mais rapidamente com unidades reservadas mais rápidas.</span><span class="sxs-lookup"><span data-stu-id="4f166-116">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f166-117">Lembre-se de examinar o tópico [Visão geral](media-services-scale-media-processing-overview.md) para obter mais informações sobre o tópico de dimensionamento de processamento de mídia.</span><span class="sxs-lookup"><span data-stu-id="4f166-117">Make sure to review the [overview](media-services-scale-media-processing-overview.md) topic to get more information about scaling media processing topic.</span></span>
> 
> 

## <a name="scale-media-processing"></a><span data-ttu-id="4f166-118">Processamento de mídia de escala</span><span class="sxs-lookup"><span data-stu-id="4f166-118">Scale media processing</span></span>
<span data-ttu-id="4f166-119">Para alterar o tipo de unidade reservada e o número de unidades reservadas, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4f166-119">To change the reserved unit type and the number of reserved units, do the following:</span></span>

1. <span data-ttu-id="4f166-120">No [Portal do Azure](https://portal.azure.com/), selecione sua conta dos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f166-120">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="4f166-121">Na janela **Configurações**, selecione **Unidades reservadas de mídia**.</span><span class="sxs-lookup"><span data-stu-id="4f166-121">In the **Settings** window, select **Media reserved units**.</span></span>
   
    <span data-ttu-id="4f166-122">Para alterar o número de unidades reservadas para o tipo de unidade reservada selecionado, use o controle deslizante **Unidades Reservadas de Mídia** .</span><span class="sxs-lookup"><span data-stu-id="4f166-122">To change the number of reserved units for the selected reserved unit type, use the **Media Served Units** slider.</span></span>
   
    <span data-ttu-id="4f166-123">Para alterar o **TIPO DE UNIDADE RESERVADA**, pressione S1, S2 ou S3.</span><span class="sxs-lookup"><span data-stu-id="4f166-123">To change the **RESERVED UNIT TYPE**, press S1, S2, or S3.</span></span>
   
    ![Página processadores](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. <span data-ttu-id="4f166-125">Pressione o botão SALVAR para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="4f166-125">Press the SAVE button to save your changes.</span></span>
   
    <span data-ttu-id="4f166-126">As novas unidades reservadas são alocadas quando você pressiona SALVAR.</span><span class="sxs-lookup"><span data-stu-id="4f166-126">The new reserved units are allocated when you press SAVE.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f166-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4f166-127">Next steps</span></span>
<span data-ttu-id="4f166-128">Examine os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="4f166-128">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4f166-129">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="4f166-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

