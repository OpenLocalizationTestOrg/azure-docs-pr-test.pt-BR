---
title: "AAA\"publicar conteúdo com hello portal do Azure | Microsoft Docs\""
description: "Este tutorial orienta você pelas etapas de saudação de publicação de conteúdo com hello portal do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: a7a3867a6939b4b9da883176c6cc20c99d6c54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-content-with-hello-azure-portal"></a><span data-ttu-id="c8cf3-103">Publicar o conteúdo com hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c8cf3-103">Publish content with hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c8cf3-104">Portal</span><span class="sxs-lookup"><span data-stu-id="c8cf3-104">Portal</span></span>](media-services-portal-publish.md)
> * [<span data-ttu-id="c8cf3-105">.NET</span><span class="sxs-lookup"><span data-stu-id="c8cf3-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="c8cf3-106">REST</span><span class="sxs-lookup"><span data-stu-id="c8cf3-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="c8cf3-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c8cf3-107">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="c8cf3-108">toocomplete neste tutorial, você precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-108">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="c8cf3-109">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c8cf3-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="c8cf3-110">tooprovide o usuário com uma URL que pode ser usado toostream ou baixar o conteúdo, você primeiro precisa muito "Publicar" seu ativo, criando um localizador.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-110">tooprovide your user with a  URL that can be used toostream or download your content, you first need too"publish" your asset by creating a locator.</span></span> <span data-ttu-id="c8cf3-111">Os localizadores fornecem acesso toofiles contidos em Olá ativo.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-111">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="c8cf3-112">Os Serviços de Mídia oferecem suporte a dois tipos de localizadores:</span><span class="sxs-lookup"><span data-stu-id="c8cf3-112">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="c8cf3-113">Transmitindo os localizadores (OnDemandOrigin), usados para streaming adaptável (por exemplo, toostream MPEG DASH, HLS ou Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="c8cf3-113">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, toostream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="c8cf3-114">toocreate um localizador de transmissão seu ativo deve conter um arquivo. ISM.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-114">toocreate a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="c8cf3-115">Localizadores progressivos (SAS), usados para a entrega de vídeo por meio do download progressivo.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-115">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="c8cf3-116">Uma URL de streaming tem Olá formato a seguir e você pode usá-lo tooplay ativos do Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-116">A streaming URL has hello following format and you can use it tooplay Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="c8cf3-117">Acrescentar toobuild uma URL de streaming de HLS (format = m3u8-aapl) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-117">toobuild an HLS streaming URL, append (format=m3u8-aapl) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="c8cf3-118">Acrescentar toobuild um MPEG DASH URL de streaming (formato = mpd-tempo-csf) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-118">toobuild an  MPEG DASH streaming URL, append (format=mpd-time-csf) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

<span data-ttu-id="c8cf3-119">Uma URL SAS tem Olá formato a seguir.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-119">A SAS URL has hello following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="c8cf3-120">Para obter mais informações, consulte [Visão geral sobre fornecimento de conteúdo](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c8cf3-120">For more information, see [Delivering content overview](media-services-deliver-content-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c8cf3-121">Se você usou os localizadores de portal toocreate Olá antes de março de 2015, os localizadores com uma data de validade de dois anos foram criados.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-121">If you used hello portal toocreate locators before March 2015, locators with a two year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="c8cf3-122">tooupdate uma data de expiração em um localizador, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) ou [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-122">tooupdate an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="c8cf3-123">Observe que quando você atualizar a data de expiração de saudação de um localizador SAS, Olá URL é alterado.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-123">Note that when you update hello expiration date of a SAS locator, hello URL changes.</span></span>

### <a name="toouse-hello-portal-toopublish-an-asset"></a><span data-ttu-id="c8cf3-124">toouse de saudação portal toopublish um ativo</span><span class="sxs-lookup"><span data-stu-id="c8cf3-124">toouse hello portal toopublish an asset</span></span>
<span data-ttu-id="c8cf3-125">toouse de saudação portal toopublish um ativo, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8cf3-125">toouse hello portal toopublish an asset, do hello following:</span></span>

1. <span data-ttu-id="c8cf3-126">Em Olá [portal do Azure](https://portal.azure.com/), selecione sua conta de serviços de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-126">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="c8cf3-127">Selecione **Configurações** > **Ativos**.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-127">Select **Settings** > **Assets**.</span></span>
3. <span data-ttu-id="c8cf3-128">Selecione Olá ativo que você deseja toopublish.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-128">Select hello asset that you want toopublish.</span></span>
4. <span data-ttu-id="c8cf3-129">Clique em Olá **publicar** botão.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-129">Click hello **Publish** button.</span></span>
5. <span data-ttu-id="c8cf3-130">Selecione o tipo de localizador de saudação.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-130">Select hello locator type.</span></span>
6. <span data-ttu-id="c8cf3-131">Pressione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-131">Press **Add**.</span></span>
   
    ![Publicar](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="c8cf3-133">Olá URL será adicionado lista toohello de **publicado URLs**.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-133">hello URL will be added toohello list of **Published URLs**.</span></span>

## <a name="play-content-from-hello-portal"></a><span data-ttu-id="c8cf3-134">Reproduzir conteúdo do portal de saudação</span><span class="sxs-lookup"><span data-stu-id="c8cf3-134">Play content from hello portal</span></span>
<span data-ttu-id="c8cf3-135">Olá, portal do Azure fornece um player de conteúdo que você pode usar tootest o vídeo.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-135">hello Azure portal provides a content player that you can use tootest your video.</span></span>

<span data-ttu-id="c8cf3-136">Clique em vídeo Olá desejado e clique em Olá **reproduzir** botão.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-136">Click hello desired video and then click hello **Play** button.</span></span>

![Publicar](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="c8cf3-138">Algumas considerações se aplicam:</span><span class="sxs-lookup"><span data-stu-id="c8cf3-138">Some considerations apply:</span></span>

* <span data-ttu-id="c8cf3-139">Certifique-se de saudação vídeo foi publicada.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-139">Make sure hello video has been published.</span></span>
* <span data-ttu-id="c8cf3-140">Isso **Media player** reproduz do ponto de extremidade de streaming de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-140">This **Media player** plays from hello default streaming endpoint.</span></span> <span data-ttu-id="c8cf3-141">Se você quiser tooplay de não-padrão streaming de ponto de extremidade, clique toocopy Olá URL e use outro player.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-141">If you want tooplay from a non-default streaming endpoint, click toocopy hello URL and use another player.</span></span> <span data-ttu-id="c8cf3-142">Por exemplo, o [Player dos Serviços de Mídia do Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="c8cf3-142">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
* <span data-ttu-id="c8cf3-143">saudação do qual são de streaming de ponto de extremidade de streaming deve estar em execução.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-143">hello streaming endpoint from which you are streaming must be running.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="c8cf3-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c8cf3-144">Next steps</span></span>
<span data-ttu-id="c8cf3-145">Examine os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="c8cf3-145">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c8cf3-146">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="c8cf3-146">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

