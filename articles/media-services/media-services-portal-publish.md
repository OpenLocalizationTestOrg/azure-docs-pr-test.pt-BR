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
# <a name="publish-content-with-hello-azure-portal"></a>Publicar o conteúdo com hello portal do Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-publish.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [REST](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a>Visão geral
> [!NOTE]
> toocomplete neste tutorial, você precisa de uma conta do Azure. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

tooprovide o usuário com uma URL que pode ser usado toostream ou baixar o conteúdo, você primeiro precisa muito "Publicar" seu ativo, criando um localizador. Os localizadores fornecem acesso toofiles contidos em Olá ativo. Os Serviços de Mídia oferecem suporte a dois tipos de localizadores: 

* Transmitindo os localizadores (OnDemandOrigin), usados para streaming adaptável (por exemplo, toostream MPEG DASH, HLS ou Smooth Streaming). toocreate um localizador de transmissão seu ativo deve conter um arquivo. ISM. 
* Localizadores progressivos (SAS), usados para a entrega de vídeo por meio do download progressivo.

Uma URL de streaming tem Olá formato a seguir e você pode usá-lo tooplay ativos do Smooth Streaming.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

Acrescentar toobuild uma URL de streaming de HLS (format = m3u8-aapl) toohello URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

Acrescentar toobuild um MPEG DASH URL de streaming (formato = mpd-tempo-csf) toohello URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

Uma URL SAS tem Olá formato a seguir.

    {blob container name}/{asset name}/{file name}/{SAS signature}

Para obter mais informações, consulte [Visão geral sobre fornecimento de conteúdo](media-services-deliver-content-overview.md).

> [!NOTE]
> Se você usou os localizadores de portal toocreate Olá antes de março de 2015, os localizadores com uma data de validade de dois anos foram criados.  
> 
> 

tooupdate uma data de expiração em um localizador, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) ou [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs. Observe que quando você atualizar a data de expiração de saudação de um localizador SAS, Olá URL é alterado.

### <a name="toouse-hello-portal-toopublish-an-asset"></a>toouse de saudação portal toopublish um ativo
toouse de saudação portal toopublish um ativo, Olá a seguir:

1. Em Olá [portal do Azure](https://portal.azure.com/), selecione sua conta de serviços de mídia do Azure.
2. Selecione **Configurações** > **Ativos**.
3. Selecione Olá ativo que você deseja toopublish.
4. Clique em Olá **publicar** botão.
5. Selecione o tipo de localizador de saudação.
6. Pressione **Adicionar**.
   
    ![Publicar](./media/media-services-portal-vod-get-started/media-services-publish1.png)

Olá URL será adicionado lista toohello de **publicado URLs**.

## <a name="play-content-from-hello-portal"></a>Reproduzir conteúdo do portal de saudação
Olá, portal do Azure fornece um player de conteúdo que você pode usar tootest o vídeo.

Clique em vídeo Olá desejado e clique em Olá **reproduzir** botão.

![Publicar](./media/media-services-portal-vod-get-started/media-services-play.png)

Algumas considerações se aplicam:

* Certifique-se de saudação vídeo foi publicada.
* Isso **Media player** reproduz do ponto de extremidade de streaming de padrão de saudação. Se você quiser tooplay de não-padrão streaming de ponto de extremidade, clique toocopy Olá URL e use outro player. Por exemplo, o [Player dos Serviços de Mídia do Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).
* saudação do qual são de streaming de ponto de extremidade de streaming deve estar em execução.  

## <a name="next-steps"></a>Próximas etapas
Examine os roteiros de aprendizagem dos Serviços de Mídia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

