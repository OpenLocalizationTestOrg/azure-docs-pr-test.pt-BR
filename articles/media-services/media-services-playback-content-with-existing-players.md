---
title: "aaaUse existente players tooplayback seu conteúdo - Azure | Microsoft Docs"
description: "Este tópico lista os players existentes que você pode usar tooplayback seu conteúdo."
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
ms.openlocfilehash: 54817345a19a9d3b18f1e7b352c3342043a569b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="playing-your-content-with-existing-players"></a>Reprodução de seu conteúdo com players existentes
Os serviços de mídia do Microsoft Azure suporta muitos formatos populares de streaming, como Smooth Streaming, HTTP Live Streaming e MPEG-Dash. Este tópico indica players tooexisting que você pode usar tootest os fluxos.

### <a name="hello-azure-portal-media-services-content-player"></a>player de conteúdo Olá portal do Azure Media Services
Olá **Azure** portal fornece um player de conteúdo que você pode usar tootest o vídeo.

Clique em Olá desejado vídeo (Verifique se ele foi [publicado](media-services-portal-publish.md)) e clique em Olá **reproduzir** botão na parte inferior de saudação do portal de saudação.

Algumas considerações se aplicam:

* Olá **PLAYER de conteúdo de serviços de mídia** reproduz do ponto de extremidade de streaming de padrão de saudação. Se você quiser tooplay de um ponto de extremidade de streaming não padrão, use outro player. Por exemplo, [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a>Azure Media Player
Use [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tooplayback seu conteúdo (limpar ou protegido) em qualquer um dos formatos a seguir de saudação:

* Smooth Streaming
* MPEG DASH
* HLS
* MP4 progressivo

### <a name="flash-player"></a>Flash Player
#### <a name="aes-encrypted-with-token"></a>Criptografado com AES com token
[http://aestoken.azurewebsites.net](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a>Players Silverlight
#### <a name="monitoring"></a>Monitoramento
[http://smf.cloudapp.net/healthmonitor](http://smf.cloudapp.net/healthmonitor)

#### <a name="playready-with-token"></a>PlayReady com token
[http://sltoken.azurewebsites.net](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a>Players DASH
[http://dashplayer.azurewebsites.net](http://dashplayer.azurewebsites.net)

[http://dashif.org](http://dashif.org)

### <a name="other"></a>outro
tootest URLs de HLS, você também pode usar:

* **Safari** em um dispositivo iOS ou
* **Player 3ivx HLS** no Windows.

## <a name="developing-video-players"></a>Desenvolvendo players de vídeo
Para obter informações sobre como toodevelop seus próprio players, consulte [desenvolver players de vídeo](media-services-develop-video-players.md)

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
