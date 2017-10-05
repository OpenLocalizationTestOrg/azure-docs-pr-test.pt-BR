---
title: Codificar um ativo usando o Media Encoder Standard com o portal do Azure | Microsoft Docs
description: "Este tutorial guia você pelas etapas de codificação de um ativo usando o Codificador de Mídia Padrão com o portal do Azure."
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
ms.openlocfilehash: a299245e285c4caa68988b184799cd6f4d13e080
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-the-azure-portal"></a><span data-ttu-id="69709-103">Codificar um ativo usando o Codificador de Mídia Padrão com o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="69709-103">Encode an asset using Media Encoder Standard with the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="69709-104">Para concluir este tutorial, você precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="69709-104">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="69709-105">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="69709-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="69709-106">Ao trabalhar com os Serviços de Mídia do Azure, um dos cenários mais comuns é fornecer streaming com uma taxa de bits adaptável aos clientes dos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="69709-106">When working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="69709-107">Os Serviços de Mídia permitem as seguintes tecnologias de streaming de taxa de bits adaptável: HLS (HTTP Live Streaming), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="69709-107">Media Services supports the following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="69709-108">Para preparar os vídeos para a transmissão da taxa de bits adaptável, você precisa codificar o vídeo de origem em arquivos de múltiplas taxas de bits.</span><span class="sxs-lookup"><span data-stu-id="69709-108">To prepare your videos for adaptive bitrate streaming, you need to encode your source video into multi-bitrate files.</span></span> <span data-ttu-id="69709-109">Você deve usar o codificador **Media Encoder Standard** para codificar seus vídeos.</span><span class="sxs-lookup"><span data-stu-id="69709-109">You should use the **Media Encoder Standard** encoder to encode your videos.</span></span>  

<span data-ttu-id="69709-110">Os Serviços de Mídia também fornecem um empacotamento dinâmico que permite entregar os MP4s de múltiplas taxas de bits nos formatos de streaming MPEG DASH, HLS e Smooth Streaming, sem a necessidade de reempacotá-los nesses formatos de streaming.</span><span class="sxs-lookup"><span data-stu-id="69709-110">Media Services also provides dynamic packaging which allows you to deliver your multi-bitrate MP4s in the following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having to re-package into these streaming formats.</span></span> <span data-ttu-id="69709-111">Com o empacotamento dinâmico, você só precisa armazenar e pagar pelos arquivos em um único formato de armazenamento, e os Serviços de Mídia criarão e fornecerão a resposta apropriada com base nas solicitações de um cliente.</span><span class="sxs-lookup"><span data-stu-id="69709-111">With dynamic packaging you only need to store and pay for the files in single storage format and Media Services will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="69709-112">Para tirar proveito do empacotamento dinâmico, você precisa codificar seu arquivo de origem em um conjunto de arquivos MP4 com múltiplas taxas de bits (as etapas da codificação são demonstradas mais tarde nesta seção).</span><span class="sxs-lookup"><span data-stu-id="69709-112">To take advantage of dynamic packaging, you need to encode your source file into a set of multi-bitrate MP4 files (the encoding steps are demonstrated later in this section).</span></span>

<span data-ttu-id="69709-113">Para dimensionar o processamento de mídia, consulte [este](media-services-portal-scale-media-processing.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="69709-113">To scale media processing, see [this](media-services-portal-scale-media-processing.md) topic.</span></span>

## <a name="encode-with-the-azure-portal"></a><span data-ttu-id="69709-114">Codificar com o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="69709-114">Encode with the Azure portal</span></span>
<span data-ttu-id="69709-115">Esta seção descreve as etapas que você pode seguir para codificar o conteúdo com o Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="69709-115">This section describes the steps you can take to encode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="69709-116">No [Portal do Azure](https://portal.azure.com/), selecione sua conta dos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="69709-116">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="69709-117">Na janela **Configurações**, selecione **Ativos**.</span><span class="sxs-lookup"><span data-stu-id="69709-117">In the **Settings** window, select **Assets**.</span></span>  
3. <span data-ttu-id="69709-118">Na janela **Ativos** , selecione o ativo que você gostaria de codificar.</span><span class="sxs-lookup"><span data-stu-id="69709-118">In the **Assets** window, select the asset that you would like to encode.</span></span>
4. <span data-ttu-id="69709-119">Pressione o botão **Codificar** .</span><span class="sxs-lookup"><span data-stu-id="69709-119">Press the **Encode** button.</span></span>
5. <span data-ttu-id="69709-120">Na janela **Codificar um ativo** , selecione o processador "Media Encoder Standard" e uma predefinição.</span><span class="sxs-lookup"><span data-stu-id="69709-120">In the **Encode an asset** window, select the "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="69709-121">Para saber mais sobre as predefinições, confira [Gerar automaticamente uma escada de taxa de bits](media-services-autogen-bitrate-ladder-with-mes.md) e [Predefinições de tarefa para MES](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="69709-121">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="69709-122">Se você pretende controlar qual predefinição de codificação é usada, lembre-se disso: é importante selecionar a predefinição mais apropriada para seu vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="69709-122">If you plan to control which encoding preset is used, keep this in mind: it is important to select the preset that is most appropriate for your input video.</span></span> <span data-ttu-id="69709-123">Por exemplo, se você souber que o vídeo de entrada tem uma resolução de 1920 x 1080 pixels, poderá usar a predefinição "H264 Múltiplas Taxas de Bits 1080p".</span><span class="sxs-lookup"><span data-stu-id="69709-123">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use the "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="69709-124">Se você tiver um vídeo de baixa resolução (640 x 360), não deverá usar a predefinição "H264 Múltiplas Taxas de Bits 1080p".</span><span class="sxs-lookup"><span data-stu-id="69709-124">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="69709-125">Para facilitar o gerenciamento, você tem a opção de editar o nome do ativo de saída e o nome do trabalho.</span><span class="sxs-lookup"><span data-stu-id="69709-125">For easier management, you have an option of editing the name of the output asset, and the name of the job.</span></span>
   
   ![Codificar ativos](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. <span data-ttu-id="69709-127">Pressione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="69709-127">Press **Create**.</span></span>

## <a name="next-step"></a><span data-ttu-id="69709-128">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="69709-128">Next step</span></span>
<span data-ttu-id="69709-129">Você pode monitorar o andamento do trabalho de codificação com o portal do Azure, conforme descrito [neste](media-services-portal-check-job-progress.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="69709-129">You can monitor encoding job progress with the Azure portal, as described in [this](media-services-portal-check-job-progress.md) article.</span></span>  

## <a name="media-services-learning-paths"></a><span data-ttu-id="69709-130">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="69709-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="69709-131">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="69709-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

