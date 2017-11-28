---
title: "Perguntas frequentes sobre os serviços de mídia de aaaAzure | Microsoft Docs"
description: Perguntas frequentes (FAQs)
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 6d48a5c1291f3c2559d8445921d571718d0a0a6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions"></a><span data-ttu-id="77ef1-103">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="77ef1-103">Frequently asked questions</span></span>

<span data-ttu-id="77ef1-104">Este artigo aborda as perguntas frequentes geradas pela comunidade de usuários de serviços de mídia do Azure (AMS) hello.</span><span class="sxs-lookup"><span data-stu-id="77ef1-104">This article addresses frequently asked questions raised by hello Azure Media Services (AMS) user community.</span></span>

## <a name="general-ams-faqs"></a><span data-ttu-id="77ef1-105">Perguntas frequentes sobre o AMS geral</span><span class="sxs-lookup"><span data-stu-id="77ef1-105">General AMS FAQs</span></span>
<span data-ttu-id="77ef1-106">P: Como você dimensiona indexação?</span><span class="sxs-lookup"><span data-stu-id="77ef1-106">Q: How do you scale indexing?</span></span>

<span data-ttu-id="77ef1-107">R: unidades de Olá reservado são hello mesmo para codificação e tarefas de indexação.</span><span class="sxs-lookup"><span data-stu-id="77ef1-107">A: hello reserved units are hello same for Encoding and Indexing tasks.</span></span> <span data-ttu-id="77ef1-108">Siga as instruções [como unidades reservadas de codificação tooScale](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="77ef1-108">Follow instructions on [How tooScale Encoding Reserved Units](media-services-scale-media-processing-overview.md).</span></span> <span data-ttu-id="77ef1-109">**Observação** o desempenho do indexador não é afetado pelo tipo de unidade reservada.</span><span class="sxs-lookup"><span data-stu-id="77ef1-109">**Note** that Indexer performance is not affected by Reserved Unit Type.</span></span>

<span data-ttu-id="77ef1-110">P: Carreguei, codifiquei e publiquei um vídeo.</span><span class="sxs-lookup"><span data-stu-id="77ef1-110">Q: I uploaded, encoded, and published a video.</span></span> <span data-ttu-id="77ef1-111">Qual seria o vídeo de saudação do motivo de saudação não reproduzido quando tento toostream-lo?</span><span class="sxs-lookup"><span data-stu-id="77ef1-111">What would be hello reason hello video does not play when I try toostream it?</span></span>

<span data-ttu-id="77ef1-112">R: um dos hello mais comuns motivos é não possuem Olá streaming de ponto de extremidade do qual você está tentando tooplayback em Olá **executando** estado.</span><span class="sxs-lookup"><span data-stu-id="77ef1-112">A: One of hello most common reasons is you do not have hello streaming endpoint from which you are trying tooplayback in hello **Running** state.</span></span>  

<span data-ttu-id="77ef1-113">P: Posso fazer a composição em um fluxo ao vivo?</span><span class="sxs-lookup"><span data-stu-id="77ef1-113">Q: Can I do compositing on a live stream?</span></span>

<span data-ttu-id="77ef1-114">R: composição em fluxos ao vivo no momento não é oferecida nos serviços de mídia do Azure, portanto, seria necessário toopre-compor em seu computador.</span><span class="sxs-lookup"><span data-stu-id="77ef1-114">A: Compositing on live streams is currently not offered in Azure Media Services, so you would need toopre-compose on your computer.</span></span>

<span data-ttu-id="77ef1-115">P: Pode usar o CDN do Azure com a transmissão ao vivo?</span><span class="sxs-lookup"><span data-stu-id="77ef1-115">Q: Can I use Azure CDN with Live Streaming?</span></span>

<span data-ttu-id="77ef1-116">R: Media Services dá suporte à integração com o Azure CDN (para obter mais informações, consulte [como tooManage pontos de extremidade de Streaming em uma conta do Media Services](media-services-portal-manage-streaming-endpoints.md)).</span><span class="sxs-lookup"><span data-stu-id="77ef1-116">A: Media Services supports integration with Azure CDN (for more information, see [How tooManage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)).</span></span>  <span data-ttu-id="77ef1-117">Você pode usar a transmissão ao vivo o com CDN.</span><span class="sxs-lookup"><span data-stu-id="77ef1-117">You can use Live streaming with CDN.</span></span> <span data-ttu-id="77ef1-118">Os Serviços de Mídia do Azure fornecem saídas de Smooth Streaming, HLS e MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="77ef1-118">Azure Media Services provides Smooth Streaming, HLS and MPEG-DASH outputs.</span></span> <span data-ttu-id="77ef1-119">Todos esses formatos usam HTTP para transferir dados e obtêm os benefícios do cache de HTTP.</span><span class="sxs-lookup"><span data-stu-id="77ef1-119">All these formats use HTTP for transferring data and get benefits of HTTP caching.</span></span> <span data-ttu-id="77ef1-120">Ao vivo de fluxo de dados de áudio/vídeo reais é dividido toofragments e este fragmentos individuais ficar armazenada em cache na CDN.</span><span class="sxs-lookup"><span data-stu-id="77ef1-120">In live streaming actual video/audio data is divided toofragments and this individual fragments get cached in CDN.</span></span> <span data-ttu-id="77ef1-121">Somente dados necessidades toobe atualizado é dados de manifesto de saudação.</span><span class="sxs-lookup"><span data-stu-id="77ef1-121">Only data needs toobe refreshed is hello manifest data.</span></span> <span data-ttu-id="77ef1-122">A CDN atualiza periodicamente os dados de manifesto.</span><span class="sxs-lookup"><span data-stu-id="77ef1-122">CDN periodically refreshes manifest data.</span></span>

<span data-ttu-id="77ef1-123">P: Os Serviços de Mídia do Azure dão suporte ao armazenamento de imagens?</span><span class="sxs-lookup"><span data-stu-id="77ef1-123">Q: Does Azure Media services support storing images?</span></span>

<span data-ttu-id="77ef1-124">R: se você estiver procurando apenas toostore JPEG ou imagens PNG, você deve manter aqueles no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="77ef1-124">A: If you are just looking toostore JPEG or PNG images, you should keep those in Azure Blob Storage.</span></span> <span data-ttu-id="77ef1-125">Não há nenhum tooputting benefício-los nos serviços de mídia de conta, a menos que você deseja tookeep-los associados com seu vídeo ou áudio ativos.</span><span class="sxs-lookup"><span data-stu-id="77ef1-125">There is no benefit tooputting them in your Media Services account unless you want tookeep them associated with your Video or Audio Assets.</span></span> <span data-ttu-id="77ef1-126">Ou se você pode ter uma necessidade toouse Olá imagens como sobreposições no codificador de vídeo hello. Codificador de mídia padrão suporta sobreposições de imagens na parte superior de vídeos, e que é o que ela lista JPEG e PNG como suporte para formatos de entrada.</span><span class="sxs-lookup"><span data-stu-id="77ef1-126">Or if you might have a need toouse hello images as overlays in hello video encoder.Media Encoder Standard supports overlaying images on top of videos, and that is what it lists JPEG and PNG as supported input formats.</span></span> <span data-ttu-id="77ef1-127">Para obter mais informações, consulte [Criando sobreposições](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="77ef1-127">For more information, see [Creating Overlays](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

<span data-ttu-id="77ef1-128">P: como posso copiar ativos de uma tooanother de conta de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="77ef1-128">Q: How can I copy assets from one Media Services account tooanother.</span></span>

<span data-ttu-id="77ef1-129">R: toocopy ativos de uma tooanother de conta de serviços de mídia usando .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) método de extensão disponível no hello [extensões do SDK do Azure Media Services .NET](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repositório.</span><span class="sxs-lookup"><span data-stu-id="77ef1-129">A: toocopy assets from one Media Services account tooanother using .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) extension method available in hello [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span></span> <span data-ttu-id="77ef1-130">Para saber mais, consulte o thread [deste](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) fórum.</span><span class="sxs-lookup"><span data-stu-id="77ef1-130">For more information, see [this](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span></span>

<span data-ttu-id="77ef1-131">P: quais são Olá caracteres suportados para nomeação de arquivos ao trabalhar com AMS?</span><span class="sxs-lookup"><span data-stu-id="77ef1-131">Q: What are hello supported characters for naming files when working with AMS?</span></span>

<span data-ttu-id="77ef1-132">Unidade: serviços de mídia de usa o valor de saudação do hello IAssetFile.Name propriedade ao criar URLs para Olá streaming de conteúdo (por exemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por esse motivo, não é permitida a codificação por porcentagem.</span><span class="sxs-lookup"><span data-stu-id="77ef1-132">A: Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="77ef1-133">Olá valor Olá **nome** propriedade não pode ter qualquer um dos seguintes Olá [%-caracteres reservados codificados](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ".</span><span class="sxs-lookup"><span data-stu-id="77ef1-133">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="77ef1-134">Além disso, pode haver somente um ‘.’</span><span class="sxs-lookup"><span data-stu-id="77ef1-134">Also, there can only be one ‘.’</span></span> <span data-ttu-id="77ef1-135">para a extensão de nome de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="77ef1-135">for hello file name extension.</span></span>

<span data-ttu-id="77ef1-136">P: como tooconnect usando REST?</span><span class="sxs-lookup"><span data-stu-id="77ef1-136">Q: How tooconnect using REST?</span></span>

<span data-ttu-id="77ef1-137">R: para obter informações sobre como tooconnect toohello AMS API, consulte [Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="77ef1-137">A: For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> <span data-ttu-id="77ef1-138">Após conectar-se toohttps://media.windows.net, você receberá um redirecionamento 301 que especifica outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="77ef1-138">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="77ef1-139">Você deve fazer chamadas subsequentes toohello novo URI.</span><span class="sxs-lookup"><span data-stu-id="77ef1-139">You must make subsequent calls toohello new URI.</span></span> 

<span data-ttu-id="77ef1-140">P: como é possível girar um vídeo durante o processo de codificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="77ef1-140">Q: How can I rotate a video during hello encoding process.</span></span>

<span data-ttu-id="77ef1-141">R: Olá [codificador de mídia padrão](media-services-dotnet-encode-with-media-encoder-standard.md) dá suporte a rotação de ângulos de 180/90/270.</span><span class="sxs-lookup"><span data-stu-id="77ef1-141">A: hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 90/180/270.</span></span> <span data-ttu-id="77ef1-142">comportamento padrão de saudação é "Auto", onde ele tenta toodetect Olá rotação metadados na entrada de arquivo MP4/MOV hello e compensar a ele.</span><span class="sxs-lookup"><span data-stu-id="77ef1-142">hello default behavior is "Auto", where it tries toodetect hello rotation metadata in hello incoming MP4/MOV file and compensate for it.</span></span> <span data-ttu-id="77ef1-143">Incluem hello seguinte **fontes** tooone de elemento de saudação json predefinições definidas [aqui](media-services-mes-presets-overview.md):</span><span class="sxs-lookup"><span data-stu-id="77ef1-143">Include hello following **Sources** element tooone of hello json presets defined [here](media-services-mes-presets-overview.md):</span></span>

    "Version": 1.0,
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...


## <a name="media-services-learning-paths"></a><span data-ttu-id="77ef1-144">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="77ef1-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="77ef1-145">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="77ef1-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
