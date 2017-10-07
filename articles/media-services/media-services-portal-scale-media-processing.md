---
title: "mídia aaaScale processamento usando Olá portal do Azure | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de saudação de dimensionamento mídia processamento usando Olá portal do Azure."
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
ms.openlocfilehash: 89240c6f7579b8795e7b47f2b1c398b1d5477e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-reserved-unit-type"></a><span data-ttu-id="2dcce-103">Alterar tipo de unidade de saudação reservado</span><span class="sxs-lookup"><span data-stu-id="2dcce-103">Change hello reserved unit type</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2dcce-104">.NET</span><span class="sxs-lookup"><span data-stu-id="2dcce-104">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="2dcce-105">Portal</span><span class="sxs-lookup"><span data-stu-id="2dcce-105">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="2dcce-106">REST</span><span class="sxs-lookup"><span data-stu-id="2dcce-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="2dcce-107">Java</span><span class="sxs-lookup"><span data-stu-id="2dcce-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="2dcce-108">PHP</span><span class="sxs-lookup"><span data-stu-id="2dcce-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="2dcce-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="2dcce-109">Overview</span></span>

<span data-ttu-id="2dcce-110">Uma conta de serviços de mídia está associada um tipo de unidade reservada, que determina a velocidade de saudação com a qual a mídia de processamento de tarefas é processada.</span><span class="sxs-lookup"><span data-stu-id="2dcce-110">A Media Services account is associated with a Reserved Unit Type, which determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="2dcce-111">Você pode escolher entre os seguintes Olá reservado tipos de unidade: **S1**, **S2**, ou **S3**.</span><span class="sxs-lookup"><span data-stu-id="2dcce-111">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="2dcce-112">Por exemplo, Olá mesmo trabalho de codificação é executada mais rapidamente ao usar o hello **S2** tipo de unidade reservada comparar toohello **S1** tipo.</span><span class="sxs-lookup"><span data-stu-id="2dcce-112">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span>

<span data-ttu-id="2dcce-113">Além disso, toospecifying Olá reservado tipo de unidade, você pode especificar tooprovision sua conta com **unidades reservadas** (RUs).</span><span class="sxs-lookup"><span data-stu-id="2dcce-113">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="2dcce-114">número de saudação de RUs provisionados determina o número de saudação de tarefas de mídia que podem ser processadas simultaneamente em uma conta.</span><span class="sxs-lookup"><span data-stu-id="2dcce-114">hello number of provisioned RUs determines hello number of media tasks that can be processed concurrently in a given account.</span></span>

>[!NOTE]
><span data-ttu-id="2dcce-115">As URs trabalham para paralelizar todo o processamento de mídia, incluindo os trabalhos de indexação, usando o Azure Media Indexer.</span><span class="sxs-lookup"><span data-stu-id="2dcce-115">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="2dcce-116">No entanto, ao contrário da codificação, a indexação de trabalhos não será processada mais rapidamente com unidades reservadas mais rápidas.</span><span class="sxs-lookup"><span data-stu-id="2dcce-116">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2dcce-117">Verifique se Olá de tooreview [visão geral](media-services-scale-media-processing-overview.md) tooget tópico para obter mais informações sobre como dimensionar um tópico de processamento de mídia.</span><span class="sxs-lookup"><span data-stu-id="2dcce-117">Make sure tooreview hello [overview](media-services-scale-media-processing-overview.md) topic tooget more information about scaling media processing topic.</span></span>
> 
> 

## <a name="scale-media-processing"></a><span data-ttu-id="2dcce-118">Processamento de mídia de escala</span><span class="sxs-lookup"><span data-stu-id="2dcce-118">Scale media processing</span></span>
<span data-ttu-id="2dcce-119">toochange Olá reservado hello e tipo de número de unidade de unidades reservadas, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="2dcce-119">toochange hello reserved unit type and hello number of reserved units, do hello following:</span></span>

1. <span data-ttu-id="2dcce-120">Em Olá [portal do Azure](https://portal.azure.com/), selecione sua conta de serviços de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="2dcce-120">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="2dcce-121">Em Olá **configurações** janela, selecione **unidades reservadas para mídia**.</span><span class="sxs-lookup"><span data-stu-id="2dcce-121">In hello **Settings** window, select **Media reserved units**.</span></span>
   
    <span data-ttu-id="2dcce-122">número de saudação do toochange de unidades reservadas para Olá selecionou o tipo de unidade reservada, use Olá **mídia servido unidades** controle deslizante.</span><span class="sxs-lookup"><span data-stu-id="2dcce-122">toochange hello number of reserved units for hello selected reserved unit type, use hello **Media Served Units** slider.</span></span>
   
    <span data-ttu-id="2dcce-123">Olá toochange **o tipo de unidade RESERVADA**, pressione S1, S2 ou S3.</span><span class="sxs-lookup"><span data-stu-id="2dcce-123">toochange hello **RESERVED UNIT TYPE**, press S1, S2, or S3.</span></span>
   
    ![Página processadores](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. <span data-ttu-id="2dcce-125">Olá Pressione Salvar botão toosave suas alterações.</span><span class="sxs-lookup"><span data-stu-id="2dcce-125">Press hello SAVE button toosave your changes.</span></span>
   
    <span data-ttu-id="2dcce-126">novas unidades reservadas de saudação são alocadas quando você pressiona Salvar.</span><span class="sxs-lookup"><span data-stu-id="2dcce-126">hello new reserved units are allocated when you press SAVE.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2dcce-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2dcce-127">Next steps</span></span>
<span data-ttu-id="2dcce-128">Examine os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="2dcce-128">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2dcce-129">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="2dcce-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

