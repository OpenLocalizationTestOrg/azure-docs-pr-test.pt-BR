---
title: "  Publicar conteúdo com o Portal do Azure | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de publicar o conteúdo com o portal do Azure."
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
ms.openlocfilehash: 68a2fbdda0996cf4ba5ea3b09816bf845af756f4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="publish-content-with-the-azure-portal"></a><span data-ttu-id="d6b83-103">Publicar conteúdo com o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d6b83-103">Publish content with the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d6b83-104">Portal</span><span class="sxs-lookup"><span data-stu-id="d6b83-104">Portal</span></span>](media-services-portal-publish.md)
> * [<span data-ttu-id="d6b83-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d6b83-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="d6b83-106">REST</span><span class="sxs-lookup"><span data-stu-id="d6b83-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="d6b83-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d6b83-107">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="d6b83-108">Para concluir este tutorial, você precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6b83-108">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="d6b83-109">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d6b83-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="d6b83-110">Para fornecer a seus usuários uma URL que pode ser usada para transmitir ou baixar seu conteúdo, primeiro você precisa "publicar" o ativo criando um localizador.</span><span class="sxs-lookup"><span data-stu-id="d6b83-110">To provide your user with a  URL that can be used to stream or download your content, you first need to "publish" your asset by creating a locator.</span></span> <span data-ttu-id="d6b83-111">Os localizadores fornecem acesso aos arquivos contidos no ativo.</span><span class="sxs-lookup"><span data-stu-id="d6b83-111">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="d6b83-112">Os Serviços de Mídia oferecem suporte a dois tipos de localizadores:</span><span class="sxs-lookup"><span data-stu-id="d6b83-112">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="d6b83-113">Localizadores de transmissão (OnDemandOrigin), usados para a transmissão adaptável (por exemplo, para transmitir MPEG DASH, HLS ou Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="d6b83-113">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, to stream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="d6b83-114">Para criar um localizador de transmissão, seu ativo deve conter um arquivo .ism.</span><span class="sxs-lookup"><span data-stu-id="d6b83-114">To create a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="d6b83-115">Localizadores progressivos (SAS), usados para a entrega de vídeo por meio do download progressivo.</span><span class="sxs-lookup"><span data-stu-id="d6b83-115">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="d6b83-116">Uma URL de streaming tem o formato a seguir e você pode usá-la para reproduzir ativos de Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="d6b83-116">A streaming URL has the following format and you can use it to play Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="d6b83-117">Para criar uma URL de streaming de HLS, anexe (format=m3u8-aapl) à URL.</span><span class="sxs-lookup"><span data-stu-id="d6b83-117">To build an HLS streaming URL, append (format=m3u8-aapl) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="d6b83-118">Para criar uma URL de streaming MPEG DASH, anexe (format=mpd-time-csf) à URL.</span><span class="sxs-lookup"><span data-stu-id="d6b83-118">To build an  MPEG DASH streaming URL, append (format=mpd-time-csf) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

<span data-ttu-id="d6b83-119">Uma URL SAS tem o seguinte formato.</span><span class="sxs-lookup"><span data-stu-id="d6b83-119">A SAS URL has the following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="d6b83-120">Para obter mais informações, consulte [Visão geral sobre fornecimento de conteúdo](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d6b83-120">For more information, see [Delivering content overview](media-services-deliver-content-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d6b83-121">Se você usou o portal para criar localizadores antes de março de 2015, foram criados localizadores com uma data de validade de dois anos.</span><span class="sxs-lookup"><span data-stu-id="d6b83-121">If you used the portal to create locators before March 2015, locators with a two year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="d6b83-122">Para atualizar uma data de validade em um localizador, use as APIs [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) ou [.NET](http://go.microsoft.com/fwlink/?LinkID=533259).</span><span class="sxs-lookup"><span data-stu-id="d6b83-122">To update an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="d6b83-123">Observe que, quando você atualiza a data de validade de um localizador SAS, a URL é alterada.</span><span class="sxs-lookup"><span data-stu-id="d6b83-123">Note that when you update the expiration date of a SAS locator, the URL changes.</span></span>

### <a name="to-use-the-portal-to-publish-an-asset"></a><span data-ttu-id="d6b83-124">Para usar o portal para publicar um ativo</span><span class="sxs-lookup"><span data-stu-id="d6b83-124">To use the portal to publish an asset</span></span>
<span data-ttu-id="d6b83-125">Para usar o portal para publicar um ativo, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d6b83-125">To use the portal to publish an asset, do the following:</span></span>

1. <span data-ttu-id="d6b83-126">No [Portal do Azure](https://portal.azure.com/), selecione sua conta dos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6b83-126">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="d6b83-127">Selecione **Configurações** > **Ativos**.</span><span class="sxs-lookup"><span data-stu-id="d6b83-127">Select **Settings** > **Assets**.</span></span>
3. <span data-ttu-id="d6b83-128">Selecione o ativo que você deseja publicar.</span><span class="sxs-lookup"><span data-stu-id="d6b83-128">Select the asset that you want to publish.</span></span>
4. <span data-ttu-id="d6b83-129">Clique no botão **Publicar** .</span><span class="sxs-lookup"><span data-stu-id="d6b83-129">Click the **Publish** button.</span></span>
5. <span data-ttu-id="d6b83-130">Selecione o tipo de localizador.</span><span class="sxs-lookup"><span data-stu-id="d6b83-130">Select the locator type.</span></span>
6. <span data-ttu-id="d6b83-131">Pressione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d6b83-131">Press **Add**.</span></span>
   
    ![Publicar](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="d6b83-133">A URL será adicionada à lista de **URLs Publicadas**.</span><span class="sxs-lookup"><span data-stu-id="d6b83-133">The URL will be added to the list of **Published URLs**.</span></span>

## <a name="play-content-from-the-portal"></a><span data-ttu-id="d6b83-134">Reproduzir conteúdo do portal</span><span class="sxs-lookup"><span data-stu-id="d6b83-134">Play content from the portal</span></span>
<span data-ttu-id="d6b83-135">O portal do Azure fornece um player de conteúdo que você pode usar para testar o vídeo.</span><span class="sxs-lookup"><span data-stu-id="d6b83-135">The Azure portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="d6b83-136">Clique no vídeo desejado e clique no botão **Reproduzir** .</span><span class="sxs-lookup"><span data-stu-id="d6b83-136">Click the desired video and then click the **Play** button.</span></span>

![Publicar](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="d6b83-138">Algumas considerações se aplicam:</span><span class="sxs-lookup"><span data-stu-id="d6b83-138">Some considerations apply:</span></span>

* <span data-ttu-id="d6b83-139">Verifique se que o vídeo foi publicado.</span><span class="sxs-lookup"><span data-stu-id="d6b83-139">Make sure the video has been published.</span></span>
* <span data-ttu-id="d6b83-140">Esse **Media player** reproduz do ponto de extremidade de streaming padrão.</span><span class="sxs-lookup"><span data-stu-id="d6b83-140">This **Media player** plays from the default streaming endpoint.</span></span> <span data-ttu-id="d6b83-141">Se você quiser reproduzir a partir de um ponto de extremidade da transmissão não padrão, clique para copiar a URL e use outra reprodução.</span><span class="sxs-lookup"><span data-stu-id="d6b83-141">If you want to play from a non-default streaming endpoint, click to copy the URL and use another player.</span></span> <span data-ttu-id="d6b83-142">Por exemplo, o [Player dos Serviços de Mídia do Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="d6b83-142">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
* <span data-ttu-id="d6b83-143">O ponto de extremidade de streaming do qual você estiver transmitindo deverá estar em execução.</span><span class="sxs-lookup"><span data-stu-id="d6b83-143">The streaming endpoint from which you are streaming must be running.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d6b83-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d6b83-144">Next steps</span></span>
<span data-ttu-id="d6b83-145">Examine os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="d6b83-145">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d6b83-146">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="d6b83-146">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

