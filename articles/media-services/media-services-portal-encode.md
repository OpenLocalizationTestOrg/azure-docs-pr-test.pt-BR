---
title: "aaaEncode um ativo usando o codificador de mídia padrão com hello portal do Azure | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de saudação de codificar um ativo usando o codificador de mídia padrão com hello portal do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 0d118bbbe1fa9f4ba0bfa3ea3b10fb541d1d6379
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a><span data-ttu-id="ff4bc-103">Codificar um ativo usando o codificador de mídia padrão com hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ff4bc-103">Encode an asset using Media Encoder Standard with hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="ff4bc-104">toocomplete neste tutorial, você precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff4bc-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="ff4bc-105">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff4bc-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="ff4bc-106">Ao trabalhar com um dos cenários mais comuns de saudação está entregando uma taxa de bits adaptável streaming tooyour clientes de serviços de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff4bc-106">When working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="ff4bc-107">Serviços de mídia oferece suporte a saudação seguintes tecnologias de streaming de taxa de bits adaptável: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="ff4bc-107">Media Services supports hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="ff4bc-108">tooprepare vídeos para streaming de taxa de bits adaptável, você precisa tooencode sua fonte de vídeo em arquivos de várias taxas de bits.</span><span class="sxs-lookup"><span data-stu-id="ff4bc-108">tooprepare your videos for adaptive bitrate streaming, you need tooencode your source video into multi-bitrate files.</span></span> <span data-ttu-id="ff4bc-109">Você deve usar o hello **codificador de mídia padrão** tooencode codificador seus vídeos.</span><span class="sxs-lookup"><span data-stu-id="ff4bc-109">You should use hello **Media Encoder Standard** encoder tooencode your videos.</span></span>  

<span data-ttu-id="ff4bc-110">Serviços de mídia também fornecem empacotamento dinâmico que permite que você toodeliver seus MP4s de múltiplas taxas de bits nos seguintes formatos de streaming de saudação: MPEG DASH, HLS, Smooth Streaming, sem a necessidade de toore-package nesses formatos de fluxo contínuo.</span><span class="sxs-lookup"><span data-stu-id="ff4bc-110">Media Services also provides dynamic packaging which allows you toodeliver your multi-bitrate MP4s in hello following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having toore-package into these streaming formats.</span></span> <span data-ttu-id="ff4bc-111">Com o empacotamento dinâmico só é necessário toostore e pagamento para arquivos de saudação em único formato de armazenamento e os serviços de mídia criará e enviará a resposta apropriada hello, com base nas solicitações de um cliente.</span><span class="sxs-lookup"><span data-stu-id="ff4bc-111">With dynamic packaging you only need toostore and pay for hello files in single storage format and Media Services will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="ff4bc-112">tootake proveito do empacotamento dinâmico, você precisa de tooencode seu arquivo de origem em um conjunto de arquivos MP4 com múltiplas taxas de bits (etapas de codificação Olá são demonstradas posteriormente nesta seção).</span><span class="sxs-lookup"><span data-stu-id="ff4bc-112">tootake advantage of dynamic packaging, you need tooencode your source file into a set of multi-bitrate MP4 files (hello encoding steps are demonstrated later in this section).</span></span>

<span data-ttu-id="ff4bc-113">mídia tooscale processamento, consulte [isso](media-services-portal-scale-media-processing.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="ff4bc-113">tooscale media processing, see [this](media-services-portal-scale-media-processing.md) topic.</span></span>

## <a name="encode-with-hello-azure-portal"></a><span data-ttu-id="ff4bc-114">Codificar com hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ff4bc-114">Encode with hello Azure portal</span></span>
<span data-ttu-id="ff4bc-115">Esta seção descreve Olá etapas tooencode seu conteúdo com o codificador de mídia padrão.</span><span class="sxs-lookup"><span data-stu-id="ff4bc-115">This section describes hello steps you can take tooencode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="ff4bc-116">Em Olá [portal do Azure](https://portal.azure.com/), selecione sua conta de serviços de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff4bc-116">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="ff4bc-117">Em Olá **configurações** janela, selecione **ativos**.</span><span class="sxs-lookup"><span data-stu-id="ff4bc-117">In hello **Settings** window, select **Assets**.</span></span>  
3. <span data-ttu-id="ff4bc-118">Em Olá **ativos** janela, ativo Olá selecione que você gostaria que tooencode.</span><span class="sxs-lookup"><span data-stu-id="ff4bc-118">In hello **Assets** window, select hello asset that you would like tooencode.</span></span>
4. <span data-ttu-id="ff4bc-119">Olá pressione **Encode** botão.</span><span class="sxs-lookup"><span data-stu-id="ff4bc-119">Press hello **Encode** button.</span></span>
5. <span data-ttu-id="ff4bc-120">Em Olá **codificar um ativo** janela, processador "Padrão de codificador de mídia" hello select e uma predefinição.</span><span class="sxs-lookup"><span data-stu-id="ff4bc-120">In hello **Encode an asset** window, select hello "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="ff4bc-121">Para saber mais sobre as predefinições, confira [Gerar automaticamente uma escada de taxa de bits](media-services-autogen-bitrate-ladder-with-mes.md) e [Predefinições de tarefa para MES](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ff4bc-121">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="ff4bc-122">Se você planejar toocontrol quais predefinição de codificação é usada, lembre-se disso: é importante tooselect Olá predefinição mais apropriado para o vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="ff4bc-122">If you plan toocontrol which encoding preset is used, keep this in mind: it is important tooselect hello preset that is most appropriate for your input video.</span></span> <span data-ttu-id="ff4bc-123">Por exemplo, se você souber o vídeo de entrada com uma resolução de 1920 x 1080 pixels, você pode usar hello "H264 taxas de bits múltiplas 1080p" predefinido.</span><span class="sxs-lookup"><span data-stu-id="ff4bc-123">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use hello "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="ff4bc-124">Se você tiver um vídeo de baixa resolução (640 x 360), não deverá usar a predefinição "H264 Múltiplas Taxas de Bits 1080p".</span><span class="sxs-lookup"><span data-stu-id="ff4bc-124">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="ff4bc-125">Para facilitar o gerenciamento, você tem uma opção da edição nome Olá Olá ativo de saída e o nome de saudação do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff4bc-125">For easier management, you have an option of editing hello name of hello output asset, and hello name of hello job.</span></span>
   
   ![Codificar ativos](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. <span data-ttu-id="ff4bc-127">Pressione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ff4bc-127">Press **Create**.</span></span>

## <a name="next-step"></a><span data-ttu-id="ff4bc-128">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="ff4bc-128">Next step</span></span>
<span data-ttu-id="ff4bc-129">Você pode monitorar o andamento do trabalho codificação com hello portal do Azure, conforme descrito em [isso](media-services-portal-check-job-progress.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="ff4bc-129">You can monitor encoding job progress with hello Azure portal, as described in [this](media-services-portal-check-job-progress.md) article.</span></span>  

## <a name="media-services-learning-paths"></a><span data-ttu-id="ff4bc-130">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="ff4bc-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ff4bc-131">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="ff4bc-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

