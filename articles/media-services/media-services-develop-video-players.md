---
title: "aplicativos de player de vídeo aaaDevelop"
description: "tópico de saudação fornece links tooPlayer estruturas e plug-ins que você pode usar toodevelop seus próprios aplicativos de cliente que podem consumir mídia de streaming dos serviços de mídia."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 55e419fc-4c39-4902-9c62-f41cfcd86c6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: a66daa4f006a1f05271cc9ed6a02ea7ee460321d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-video-player-applications"></a>Desenvolver aplicativos de player de vídeo
## <a name="overview"></a>Visão geral
O Azure Media Services fornece ferramentas Olá necessário toocreate avançada, aplicativos de player de cliente dinâmicos para a maioria das plataformas, incluindo: dispositivos iOS, dispositivos Android, Windows, Windows Phone, Xbox e superior do conjunto de caixas. Este tópico também fornece links tooSDKs e estruturas de Player que você pode usar toodevelop seus próprios aplicativos de cliente que podem consumir mídia de streaming dos serviços de mídia do Azure.

>[!NOTE]
>Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado. toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado. 
 
## <a name="azure-media-player"></a>Azure Media Player
[Azure Media Player](http://aka.ms/ampinfo) um player de vídeo web baseia-se conteúdo de mídia back tooplay dos serviços de mídia do Microsoft Azure em uma ampla variedade de navegadores e dispositivos. Padrões do setor, como HTML5, Media Source Extensions (MSE) e extensões de mídia criptografados (EME) tooprovide uma experiência de streaming adaptável enriquecida utiliza o Azure Media Player. Quando esses padrões não estão disponíveis em um dispositivo ou em um navegador, o Azure Media Player usa Flash e Silverlight como tecnologias de fallback. Independentemente da tecnologia de reprodução de saudação usada, os desenvolvedores terá um tooaccess de interface unificada do JavaScript APIs. Isso permite conteúdo servido pelo Azure Media Services toobe executado em vários dispositivos e navegadores sem qualquer esforço extra.

Serviços de mídia do Microsoft Azure permite toobe conteúdo servido DASH, Smooth Streaming e HLS tooplay de formatos de streaming de conteúdo de volta. Azure Media Player leva em conta esses vários formatos e automaticamente desempenha Olá link melhor com base nos recursos de plataforma/navegador hello. Os Serviços de Mídia do Microsoft Azure também permitem a criptografia dinâmica de ativos com criptografia PlayReady ou criptografia de envelope de 128 bits AES. O Azure Media Player permite a descriptografia do conteúdo criptografado com PlayReady e AES de 128 bits, quando configurado adequadamente. 

Para mais informações:

* [Azure Media Player](http://aka.ms/ampinfo)
* [Documentação do Azure Media Player](http://aka.ms/ampdocs) 
* [Blog de Introdução do Azure Media Player](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/)
* [Inscreva-se toostay backup toodate com hello mais recente do Azure Media Player](http://aka.ms/ampsignup)
* [Adicionar novas solicitações de recurso, ideias, comentários](http://aka.ms/ampuservoice) 

## <a name="other-tools-for-creating-player-applications"></a>Outras ferramentas para criar aplicativos de player
Você também pode usar qualquer um dos seguintes SDKs de saudação:

* [SDK do cliente de Smooth Streaming](http://www.iis.net/downloads/microsoft/smooth-streaming) 
* [Aplicativo de Smooth Streaming da Windows Store](media-services-build-smooth-streaming-apps.md)
* [Plataforma de Mídia da Microsoft: Player Framework](http://playerframework.codeplex.com/) 
* [Documentação da estrutura de player HTML5](http://playerframework.codeplex.com/wikipage?title=HTML5%20Player&referringTitle=Documentation) 
* [Plug-in Microsoft Smooth Streaming para OSMF](https://www.microsoft.com/download/details.aspx?id=36057) 
* [Licenciamento do kit de portabilidade de cliente do Microsoft® Smooth Streaming](http://aka.ms/sspk) 
* [Desenvolvimento de aplicativos de vídeo do XBOX](http://xbox.create.msdn.com/) 

## <a name="advertising"></a>Publicidade
Serviços de mídia do Azure fornece suporte para inserção de anúncios por meio de saudação plataforma de mídia do Windows: estruturas de Player. As estruturas de player com suporte a anúncios estão disponíveis para dispositivos com Windows 8, Silverlight, Windows Phone 8 e iOS. Cada estrutura de player contém um código de exemplo que mostra como tooimplement um aplicativo de player. Há três tipos diferentes de anúncios que você pode inserir em sua mídia:

Lineares – anúncios em tela cheia que pausam o vídeo principal Olá

Não lineares – anúncios de sobreposição que são exibidos como a reprodução do vídeo principal hello, geralmente um logotipo ou outra imagem estática colocada no player de saudação

Complementares – anúncios que são exibidos fora do player Olá

Anúncios podem ser inseridos em qualquer ponto na linha do tempo do vídeo principal hello. Você deve informar o player hello quando tooplay Olá ad e qual tooplay de anúncios. Isso é feito usando um conjunto de arquivos padrão baseados em XML: VAST (Video Ad Service Template), VMAP (Digital Video Multiple Ad Playlist), MAST (Media Abstract Sequencing Template) e VPAID (Digital Video Player Ad Interface Definition). Os arquivos VAST especificam quais toodisplay anúncios. Arquivos VMAP especificam quando tooplay diversos anúncios e contêm XML VAST. Os arquivos MAST são outra anúncios de toosequence de forma que também podem conter XML VAST. Os arquivos VPAID definem uma interface entre o player de vídeo hello e ad hello ou servidor do ad. Para saber mais, confira [Inserindo anúncios](https://msdn.microsoft.com/library/dn387398.aspx).

Para obter informações sobre o suporte à legendagem oculta e a anúncios em vídeos de Streaming ao vivo, confira [Padrões de legendagem oculta e inserção de anúncios compatíveis](https://msdn.microsoft.com/library/c49e0b4d-357e-4cca-95e5-2288924d1ff3#caption_ad).

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Consulte também
[Inserindo um vídeo de streaming adaptável MPEG-DASH em um aplicativo HTML5 com DASH.js](media-services-embed-mpeg-dash-in-html5.md)

[Repositório do dash.js do GitHub](https://github.com/Dash-Industry-Forum/dash.js)

