---
title: "Usar players existentes para reproduzir seu conteúdo - Azure | Microsoft Docs"
description: "Este tópico lista os players existentes que você pode usar para reproduzir conteúdo."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7e9fcf89-0fb6-4fa4-96cb-666320684d69
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: 48f373b013b1192c353352b801876d706d91dd28
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="playing-your-content-with-existing-players"></a><span data-ttu-id="cf18b-103">Reprodução de seu conteúdo com players existentes</span><span class="sxs-lookup"><span data-stu-id="cf18b-103">Playing your content with existing players</span></span>
<span data-ttu-id="cf18b-104">Os serviços de mídia do Microsoft Azure suporta muitos formatos populares de streaming, como Smooth Streaming, HTTP Live Streaming e MPEG-Dash.</span><span class="sxs-lookup"><span data-stu-id="cf18b-104">Azure Media Services supports many popular streaming formats, such as Smooth Streaming, HTTP Live Streaming, and MPEG-Dash.</span></span> <span data-ttu-id="cf18b-105">Este tópico aponta para players existentes que você pode usar para testar os fluxos.</span><span class="sxs-lookup"><span data-stu-id="cf18b-105">This topic points you to existing players that you can use to test your streams.</span></span>

### <a name="the-azure-portal-media-services-content-player"></a><span data-ttu-id="cf18b-106">Player de conteúdo dos Serviços de Mídia do Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cf18b-106">The Azure portal Media Services content player</span></span>
<span data-ttu-id="cf18b-107">O portal do **Azure** fornece um player de conteúdo que você pode usar para testar o vídeo.</span><span class="sxs-lookup"><span data-stu-id="cf18b-107">The **Azure** portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="cf18b-108">Clique no vídeo desejado (verifique se ele foi [publicado](media-services-portal-publish.md)) e clique no botão **Reproduzir** na parte inferior do portal.</span><span class="sxs-lookup"><span data-stu-id="cf18b-108">Click on the desired video (make sure it was [published](media-services-portal-publish.md)) and click the **Play** button at the bottom of the portal.</span></span>

<span data-ttu-id="cf18b-109">Algumas considerações se aplicam:</span><span class="sxs-lookup"><span data-stu-id="cf18b-109">Some considerations apply:</span></span>

* <span data-ttu-id="cf18b-110">O **PLAYER DE CONTEÚDO DOS SERVIÇOS DE MÍDIA** é reproduzido por meio do ponto de extremidade de streaming padrão.</span><span class="sxs-lookup"><span data-stu-id="cf18b-110">The **MEDIA SERVICES CONTENT PLAYER** plays from the default streaming endpoint.</span></span> <span data-ttu-id="cf18b-111">Se você deseja reproduzir por meio de um ponto de extremidade de streaming não padrão, use outro reprodutor.</span><span class="sxs-lookup"><span data-stu-id="cf18b-111">If you want to play from a non-default streaming endpoint, use another player.</span></span> <span data-ttu-id="cf18b-112">Por exemplo, [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="cf18b-112">For example, [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a><span data-ttu-id="cf18b-114">Azure Media Player</span><span class="sxs-lookup"><span data-stu-id="cf18b-114">Azure Media Player</span></span>
<span data-ttu-id="cf18b-115">Use o [Media Player do Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html) para reproduzir conteúdo (protegido ou não) em qualquer um dos seguintes formatos:</span><span class="sxs-lookup"><span data-stu-id="cf18b-115">Use [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to playback your content (clear or protected) in any of the following formats:</span></span>

* <span data-ttu-id="cf18b-116">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="cf18b-116">Smooth Streaming</span></span>
* <span data-ttu-id="cf18b-117">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="cf18b-117">MPEG DASH</span></span>
* <span data-ttu-id="cf18b-118">HLS</span><span class="sxs-lookup"><span data-stu-id="cf18b-118">HLS</span></span>
* <span data-ttu-id="cf18b-119">MP4 progressivo</span><span class="sxs-lookup"><span data-stu-id="cf18b-119">Progressive MP4</span></span>

### <a name="flash-player"></a><span data-ttu-id="cf18b-120">Flash Player</span><span class="sxs-lookup"><span data-stu-id="cf18b-120">Flash Player</span></span>
#### <a name="aes-encrypted-with-token"></a><span data-ttu-id="cf18b-121">Criptografado com AES com token</span><span class="sxs-lookup"><span data-stu-id="cf18b-121">AES-encrypted with Token</span></span>
[<span data-ttu-id="cf18b-122">http://aestoken.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="cf18b-122">http://aestoken.azurewebsites.net</span></span>](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a><span data-ttu-id="cf18b-123">Players Silverlight</span><span class="sxs-lookup"><span data-stu-id="cf18b-123">Silverlight Players</span></span>
#### <a name="monitoring"></a><span data-ttu-id="cf18b-124">Monitoramento</span><span class="sxs-lookup"><span data-stu-id="cf18b-124">Monitoring</span></span>
[<span data-ttu-id="cf18b-125">http://smf.cloudapp.net/healthmonitor</span><span class="sxs-lookup"><span data-stu-id="cf18b-125">http://smf.cloudapp.net/healthmonitor</span></span>](http://smf.cloudapp.net/healthmonitor)

#### <a name="playready-with-token"></a><span data-ttu-id="cf18b-126">PlayReady com token</span><span class="sxs-lookup"><span data-stu-id="cf18b-126">PlayReady with Token</span></span>
[<span data-ttu-id="cf18b-127">http://sltoken.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="cf18b-127">http://sltoken.azurewebsites.net</span></span>](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a><span data-ttu-id="cf18b-128">Players DASH</span><span class="sxs-lookup"><span data-stu-id="cf18b-128">DASH Players</span></span>
[<span data-ttu-id="cf18b-129">http://dashplayer.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="cf18b-129">http://dashplayer.azurewebsites.net</span></span>](http://dashplayer.azurewebsites.net)

[<span data-ttu-id="cf18b-130">http://dashif.org</span><span class="sxs-lookup"><span data-stu-id="cf18b-130">http://dashif.org</span></span>](http://dashif.org)

### <a name="other"></a><span data-ttu-id="cf18b-131">Outros</span><span class="sxs-lookup"><span data-stu-id="cf18b-131">Other</span></span>
<span data-ttu-id="cf18b-132">Para testar as URLs de HLS, você também pode usar:</span><span class="sxs-lookup"><span data-stu-id="cf18b-132">To test HLS URLs you can also use:</span></span>

* <span data-ttu-id="cf18b-133">**Safari** em um dispositivo iOS ou</span><span class="sxs-lookup"><span data-stu-id="cf18b-133">**Safari** on an iOS device or</span></span>
* <span data-ttu-id="cf18b-134">**Player 3ivx HLS** no Windows.</span><span class="sxs-lookup"><span data-stu-id="cf18b-134">**3ivx HLS Player** on Windows.</span></span>

## <a name="developing-video-players"></a><span data-ttu-id="cf18b-135">Desenvolvendo players de vídeo</span><span class="sxs-lookup"><span data-stu-id="cf18b-135">Developing video players</span></span>
<span data-ttu-id="cf18b-136">Para obter informações sobre como desenvolver seus próprios players, consulte [Desenvolvendo players de vídeo](media-services-develop-video-players.md)</span><span class="sxs-lookup"><span data-stu-id="cf18b-136">For information about how to develop your own players, see [Developing video players](media-services-develop-video-players.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="cf18b-137">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="cf18b-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cf18b-138">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="cf18b-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
