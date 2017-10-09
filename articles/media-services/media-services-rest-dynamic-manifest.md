---
title: "Filtros de aaaCreating com a API de REST de serviços de mídia do Azure | Microsoft Docs"
description: "Este tópico descreve como os filtros de toocreate para que seu cliente pode usá-los toostream a seções específicas de um fluxo. Serviços de mídia cria manifestos dinâmico tooachieve este fluxo seletivo."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f7d23daf-7cd2-49c7-a195-ab902912ab3c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: d0b5af3b193b35f22ac70887963c2f0a06b60bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-rest-api"></a>Criando filtros com a API REST dos Serviços de Mídia do Azure
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-dynamic-manifest.md)
> * [REST](media-services-rest-dynamic-manifest.md)
> 
> 

A partir da versão 2.11, serviços de mídia permitem toodefine filtros para os ativos. Esses filtros são regras de servidor que permitirá que os clientes toochoose toodo coisas como: reprodução apenas uma seção de um vídeo (em vez de execução Olá vídeo inteiro), ou especifique apenas um subconjunto de representações de áudio e vídeo que o dispositivo do cliente pode manipular ( em vez de todas as representações de saudação que estão associados com o ativo de saudação). A filtragem de seus ativos é arquivada por meio de **manifesto dinâmico**s serão criados após o toostream de solicitação do cliente, um vídeo com base no filtro (s) especificado.

Para obter mais informações relacionadas toofilters e manifesto dinâmico, consulte [dinâmico manifestos de visão geral do](media-services-dynamic-manifest-overview.md).

Este tópico mostra como toouse toocreate de APIs REST, atualizar e excluir filtros. 

## <a name="types-used-toocreate-filters"></a>Tipos usados filtros toocreate
tipos seguintes Hello são usados durante a criação de filtros:  

* [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)
* [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* [FilterTrackSelect e FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

>[!NOTE]

>Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP. Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).

## <a name="connect-toomedia-services"></a>Conectar os serviços de tooMedia

Para obter informações sobre como tooconnect toohello AMS API, consulte [Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Após conectar-se toohttps://media.windows.net, você receberá um redirecionamento 301 que especifica outro URI dos serviços de mídia. Você deve fazer chamadas subsequentes toohello novo URI.

## <a name="create-filters"></a>Criar filtros
### <a name="create-global-filters"></a>Criar filtros globais
toocreate um filtro global, use Olá solicitações HTTP a seguir:  

#### <a name="http-request"></a>Solicitação HTTP
Cabeçalhos de solicitação

    POST https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host:media.windows.net 

Corpo da solicitação 

    {  
       "Name":"GlobalFilter",
       "PresentationTimeRange":{  
          "StartTimestamp":"0",
          "EndTimestamp":"9223372036854775807",
          "PresentationWindowDuration":"12000000000",
          "LiveBackoffDuration":"0",
          "Timescale":"10000000"
       },
       "Tracks":[  
          {  
             "PropertyConditions":
                  [  
                {  
                   "Property":"Type",
                   "Value":"audio",
                   "Operator":"Equal"
                },
                {  
                   "Property":"Bitrate",
                   "Value":"0-2147483647",
                   "Operator":"Equal"
                }
             ]
          }
       ]
    }




#### <a name="http-response"></a>Resposta HTTP
    HTTP/1.1 201 Created 

### <a name="create-local-assetfilters"></a>Criar AssetFilters local
toocreate AssetFilter um local, use Olá solicitações HTTP a seguir:  

#### <a name="http-request"></a>Solicitação HTTP
Cabeçalhos de solicitação

    POST https://media.windows.net/API/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net  

Corpo da solicitação 

    {   
       "Name":"AssetFilter", 
       "ParentAssetId":"nb:cid:UUID:536e555d-1500-80c3-92dc-f1e4fdc6c592", 
       "PresentationTimeRange":{   
          "StartTimestamp":"0", 
          "EndTimestamp":"9223372036854775807", 
          "PresentationWindowDuration":"12000000000", 
          "LiveBackoffDuration":"0", 
          "Timescale":"10000000" 
       }, 
       "Tracks":[   
          {   
             "PropertyConditions": 
                  [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

#### <a name="http-response"></a>Resposta HTTP
    HTTP/1.1 201 Created 
    . . . 

## <a name="list-filters"></a>Listar filtros
### <a name="get-all-global-filters-in-hello-ams-account"></a>Obter todos os global **filtro**s na conta Olá AMS
filtros de toolist, use Olá solicitações HTTP a seguir: 

#### <a name="http-request"></a>Solicitação HTTP
    GET https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

### <a name="get-assetfilters-associated-with-an-asset"></a>Obter **AssetFilter**s associados a um ativo
#### <a name="http-request"></a>Solicitação HTTP
    GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

### <a name="get-an-assetfilter-based-on-its-id"></a>Obter um **AssetFilter** com base em sua ID
#### <a name="http-request"></a>Solicitação HTTP
    GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000


## <a name="update-filters"></a>Atualizar filtros
Uso de PATCH, PUT ou mesclagem tooupdate um filtro com novos valores de propriedade.  Para obter mais informações sobre essas operações, consulte [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).

Se você atualizar um filtro, pode demorar até minutos too2 para regras de saudação do toorefresh de ponto de extremidade de streaming. Se conteúdo Olá foi servido usando esse filtro (e armazenado em cache na CDN e proxies caches), esse filtro a atualização pode resultar em falhas de player. É recomendável cache de saudação tooclear depois de atualizar o filtro de saudação. Se essa opção não for possível, considere usar um filtro diferente.  

### <a name="update-global-filters"></a>Atualizar filtros globais
tooupdate um filtro global, use Olá solicitações HTTP a seguir: 

#### <a name="http-request"></a>Solicitação HTTP
Cabeçalhos de solicitação: 

    MERGE https://media.windows.net/API/Filters('filterName') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 
    Content-Length: 384

Corpo da solicitação: 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

### <a name="update-local-assetfilters"></a>Atualizar AssetFilters local
tooupdate um filtro local, use Olá solicitações HTTP a seguir: 

#### <a name="http-request"></a>Solicitação HTTP
Cabeçalhos de solicitação: 

    MERGE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter')  HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

Corpo da solicitação: 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 


## <a name="delete-filters"></a>Excluir filtros
### <a name="delete-global-filters"></a>Excluir filtros globais
toodelete um filtro global, use Olá solicitações HTTP a seguir:

#### <a name="http-request"></a>Solicitação HTTP
    DELETE https://media.windows.net/api/Filters('GlobalFilter') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 


### <a name="delete-local-assetfilters"></a>Excluir AssetFilters local
toodelete AssetFilter um local, use Olá solicitações HTTP a seguir:

#### <a name="http-request"></a>Solicitação HTTP
    DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__LocalFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

## <a name="build-streaming-urls-that-use-filters"></a>Criar URLs de streaming que usam filtros
Para obter informações sobre como toopublish e oferecer seus ativos, consulte [visão geral de entrega de conteúdo tooCustomers](media-services-deliver-content-overview.md).

Olá exemplos a seguir mostram como os filtros de tooadd tooyour URLs de streaming.

**MPEG DASH** 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

**Apple HTTP Live Streaming (HLS) V4**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

**Apple HTTP Live Streaming (HLS) V3**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

**Streaming Suave**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)

    
## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Consulte também
[Visão geral de manifestos dinâmicos](media-services-dynamic-manifest-overview.md)

