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
# <a name="creating-filters-with-azure-media-services-rest-api"></a><span data-ttu-id="383f6-104">Criando filtros com a API REST dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="383f6-104">Creating Filters with Azure Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="383f6-105">.NET</span><span class="sxs-lookup"><span data-stu-id="383f6-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="383f6-106">REST</span><span class="sxs-lookup"><span data-stu-id="383f6-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="383f6-107">A partir da versão 2.11, serviços de mídia permitem toodefine filtros para os ativos.</span><span class="sxs-lookup"><span data-stu-id="383f6-107">Starting with 2.11 release, Media Services enables you toodefine filters for your assets.</span></span> <span data-ttu-id="383f6-108">Esses filtros são regras de servidor que permitirá que os clientes toochoose toodo coisas como: reprodução apenas uma seção de um vídeo (em vez de execução Olá vídeo inteiro), ou especifique apenas um subconjunto de representações de áudio e vídeo que o dispositivo do cliente pode manipular ( em vez de todas as representações de saudação que estão associados com o ativo de saudação).</span><span class="sxs-lookup"><span data-stu-id="383f6-108">These filters are server side rules that will allow your customers toochoose toodo things like: playback only a section of a video (instead of playing hello whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all hello renditions that are associated with hello asset).</span></span> <span data-ttu-id="383f6-109">A filtragem de seus ativos é arquivada por meio de **manifesto dinâmico**s serão criados após o toostream de solicitação do cliente, um vídeo com base no filtro (s) especificado.</span><span class="sxs-lookup"><span data-stu-id="383f6-109">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request toostream a video based on specified filter(s).</span></span>

<span data-ttu-id="383f6-110">Para obter mais informações relacionadas toofilters e manifesto dinâmico, consulte [dinâmico manifestos de visão geral do](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="383f6-110">For more detailed information related toofilters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="383f6-111">Este tópico mostra como toouse toocreate de APIs REST, atualizar e excluir filtros.</span><span class="sxs-lookup"><span data-stu-id="383f6-111">This topic shows how toouse REST APIs toocreate, update, and delete filters.</span></span> 

## <a name="types-used-toocreate-filters"></a><span data-ttu-id="383f6-112">Tipos usados filtros toocreate</span><span class="sxs-lookup"><span data-stu-id="383f6-112">Types used toocreate filters</span></span>
<span data-ttu-id="383f6-113">tipos seguintes Hello são usados durante a criação de filtros:</span><span class="sxs-lookup"><span data-stu-id="383f6-113">hello following types are used when creating filters:</span></span>  

* [<span data-ttu-id="383f6-114">Filter</span><span class="sxs-lookup"><span data-stu-id="383f6-114">Filter</span></span>](https://docs.microsoft.com/rest/api/media/operations/filter)
* [<span data-ttu-id="383f6-115">AssetFilter</span><span class="sxs-lookup"><span data-stu-id="383f6-115">AssetFilter</span></span>](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* [<span data-ttu-id="383f6-116">PresentationTimeRange</span><span class="sxs-lookup"><span data-stu-id="383f6-116">PresentationTimeRange</span></span>](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* [<span data-ttu-id="383f6-117">FilterTrackSelect e FilterTrackPropertyCondition</span><span class="sxs-lookup"><span data-stu-id="383f6-117">FilterTrackSelect and FilterTrackPropertyCondition</span></span>](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

>[!NOTE]

><span data-ttu-id="383f6-118">Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="383f6-118">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="383f6-119">Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="383f6-119">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="383f6-120">Conectar os serviços de tooMedia</span><span class="sxs-lookup"><span data-stu-id="383f6-120">Connect tooMedia Services</span></span>

<span data-ttu-id="383f6-121">Para obter informações sobre como tooconnect toohello AMS API, consulte [Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="383f6-121">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="383f6-122">Após conectar-se toohttps://media.windows.net, você receberá um redirecionamento 301 que especifica outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="383f6-122">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="383f6-123">Você deve fazer chamadas subsequentes toohello novo URI.</span><span class="sxs-lookup"><span data-stu-id="383f6-123">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-filters"></a><span data-ttu-id="383f6-124">Criar filtros</span><span class="sxs-lookup"><span data-stu-id="383f6-124">Create filters</span></span>
### <a name="create-global-filters"></a><span data-ttu-id="383f6-125">Criar filtros globais</span><span class="sxs-lookup"><span data-stu-id="383f6-125">Create global Filters</span></span>
<span data-ttu-id="383f6-126">toocreate um filtro global, use Olá solicitações HTTP a seguir:</span><span class="sxs-lookup"><span data-stu-id="383f6-126">toocreate a global Filter, use hello following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="383f6-127">Solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="383f6-127">HTTP Request</span></span>
<span data-ttu-id="383f6-128">Cabeçalhos de solicitação</span><span class="sxs-lookup"><span data-stu-id="383f6-128">Request Headers</span></span>

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

<span data-ttu-id="383f6-129">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="383f6-129">Request body</span></span> 

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




#### <a name="http-response"></a><span data-ttu-id="383f6-130">Resposta HTTP</span><span class="sxs-lookup"><span data-stu-id="383f6-130">HTTP Response</span></span>
    HTTP/1.1 201 Created 

### <a name="create-local-assetfilters"></a><span data-ttu-id="383f6-131">Criar AssetFilters local</span><span class="sxs-lookup"><span data-stu-id="383f6-131">Create local AssetFilters</span></span>
<span data-ttu-id="383f6-132">toocreate AssetFilter um local, use Olá solicitações HTTP a seguir:</span><span class="sxs-lookup"><span data-stu-id="383f6-132">toocreate a local AssetFilter, use hello following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="383f6-133">Solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="383f6-133">HTTP Request</span></span>
<span data-ttu-id="383f6-134">Cabeçalhos de solicitação</span><span class="sxs-lookup"><span data-stu-id="383f6-134">Request Headers</span></span>

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

<span data-ttu-id="383f6-135">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="383f6-135">Request body</span></span> 

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

#### <a name="http-response"></a><span data-ttu-id="383f6-136">Resposta HTTP</span><span class="sxs-lookup"><span data-stu-id="383f6-136">HTTP Response</span></span>
    HTTP/1.1 201 Created 
    . . . 

## <a name="list-filters"></a><span data-ttu-id="383f6-137">Listar filtros</span><span class="sxs-lookup"><span data-stu-id="383f6-137">List filters</span></span>
### <a name="get-all-global-filters-in-hello-ams-account"></a><span data-ttu-id="383f6-138">Obter todos os global **filtro**s na conta Olá AMS</span><span class="sxs-lookup"><span data-stu-id="383f6-138">Get all global **Filter**s in hello AMS account</span></span>
<span data-ttu-id="383f6-139">filtros de toolist, use Olá solicitações HTTP a seguir:</span><span class="sxs-lookup"><span data-stu-id="383f6-139">toolist filters, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="383f6-140">Solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="383f6-140">HTTP Request</span></span>
    GET https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

### <a name="get-assetfilters-associated-with-an-asset"></a><span data-ttu-id="383f6-141">Obter **AssetFilter**s associados a um ativo</span><span class="sxs-lookup"><span data-stu-id="383f6-141">Get **AssetFilter**s associated with an asset</span></span>
#### <a name="http-request"></a><span data-ttu-id="383f6-142">Solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="383f6-142">HTTP Request</span></span>
    GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

### <a name="get-an-assetfilter-based-on-its-id"></a><span data-ttu-id="383f6-143">Obter um **AssetFilter** com base em sua ID</span><span class="sxs-lookup"><span data-stu-id="383f6-143">Get an **AssetFilter** based on its Id</span></span>
#### <a name="http-request"></a><span data-ttu-id="383f6-144">Solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="383f6-144">HTTP Request</span></span>
    GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000


## <a name="update-filters"></a><span data-ttu-id="383f6-145">Atualizar filtros</span><span class="sxs-lookup"><span data-stu-id="383f6-145">Update filters</span></span>
<span data-ttu-id="383f6-146">Uso de PATCH, PUT ou mesclagem tooupdate um filtro com novos valores de propriedade.</span><span class="sxs-lookup"><span data-stu-id="383f6-146">Use PATCH, PUT or MERGE tooupdate a filter with new property values.</span></span>  <span data-ttu-id="383f6-147">Para obter mais informações sobre essas operações, consulte [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="383f6-147">For more information about these operations, see [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="383f6-148">Se você atualizar um filtro, pode demorar até minutos too2 para regras de saudação do toorefresh de ponto de extremidade de streaming.</span><span class="sxs-lookup"><span data-stu-id="383f6-148">If you update a filter, it can take up too2 minutes for streaming endpoint toorefresh hello rules.</span></span> <span data-ttu-id="383f6-149">Se conteúdo Olá foi servido usando esse filtro (e armazenado em cache na CDN e proxies caches), esse filtro a atualização pode resultar em falhas de player.</span><span class="sxs-lookup"><span data-stu-id="383f6-149">If hello content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="383f6-150">É recomendável cache de saudação tooclear depois de atualizar o filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="383f6-150">It is recommend tooclear hello cache after updating hello filter.</span></span> <span data-ttu-id="383f6-151">Se essa opção não for possível, considere usar um filtro diferente.</span><span class="sxs-lookup"><span data-stu-id="383f6-151">If this option is not possible, consider using a different filter.</span></span>  

### <a name="update-global-filters"></a><span data-ttu-id="383f6-152">Atualizar filtros globais</span><span class="sxs-lookup"><span data-stu-id="383f6-152">Update global Filters</span></span>
<span data-ttu-id="383f6-153">tooupdate um filtro global, use Olá solicitações HTTP a seguir:</span><span class="sxs-lookup"><span data-stu-id="383f6-153">tooupdate a global filter, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="383f6-154">Solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="383f6-154">HTTP Request</span></span>
<span data-ttu-id="383f6-155">Cabeçalhos de solicitação:</span><span class="sxs-lookup"><span data-stu-id="383f6-155">Request headers:</span></span> 

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

<span data-ttu-id="383f6-156">Corpo da solicitação:</span><span class="sxs-lookup"><span data-stu-id="383f6-156">Request body:</span></span> 

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

### <a name="update-local-assetfilters"></a><span data-ttu-id="383f6-157">Atualizar AssetFilters local</span><span class="sxs-lookup"><span data-stu-id="383f6-157">Update local AssetFilters</span></span>
<span data-ttu-id="383f6-158">tooupdate um filtro local, use Olá solicitações HTTP a seguir:</span><span class="sxs-lookup"><span data-stu-id="383f6-158">tooupdate a local filter, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="383f6-159">Solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="383f6-159">HTTP Request</span></span>
<span data-ttu-id="383f6-160">Cabeçalhos de solicitação:</span><span class="sxs-lookup"><span data-stu-id="383f6-160">Request headers:</span></span> 

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

<span data-ttu-id="383f6-161">Corpo da solicitação:</span><span class="sxs-lookup"><span data-stu-id="383f6-161">Request body:</span></span> 

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


## <a name="delete-filters"></a><span data-ttu-id="383f6-162">Excluir filtros</span><span class="sxs-lookup"><span data-stu-id="383f6-162">Delete filters</span></span>
### <a name="delete-global-filters"></a><span data-ttu-id="383f6-163">Excluir filtros globais</span><span class="sxs-lookup"><span data-stu-id="383f6-163">Delete global Filters</span></span>
<span data-ttu-id="383f6-164">toodelete um filtro global, use Olá solicitações HTTP a seguir:</span><span class="sxs-lookup"><span data-stu-id="383f6-164">toodelete a global Filter, use hello following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="383f6-165">Solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="383f6-165">HTTP Request</span></span>
    DELETE https://media.windows.net/api/Filters('GlobalFilter') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 


### <a name="delete-local-assetfilters"></a><span data-ttu-id="383f6-166">Excluir AssetFilters local</span><span class="sxs-lookup"><span data-stu-id="383f6-166">Delete local AssetFilters</span></span>
<span data-ttu-id="383f6-167">toodelete AssetFilter um local, use Olá solicitações HTTP a seguir:</span><span class="sxs-lookup"><span data-stu-id="383f6-167">toodelete a local AssetFilter, use hello following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="383f6-168">Solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="383f6-168">HTTP Request</span></span>
    DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__LocalFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="383f6-169">Criar URLs de streaming que usam filtros</span><span class="sxs-lookup"><span data-stu-id="383f6-169">Build streaming URLs that use filters</span></span>
<span data-ttu-id="383f6-170">Para obter informações sobre como toopublish e oferecer seus ativos, consulte [visão geral de entrega de conteúdo tooCustomers](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="383f6-170">For information on how toopublish and deliver your assets, see [Delivering Content tooCustomers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="383f6-171">Olá exemplos a seguir mostram como os filtros de tooadd tooyour URLs de streaming.</span><span class="sxs-lookup"><span data-stu-id="383f6-171">hello following examples show how tooadd filters tooyour streaming URLs.</span></span>

<span data-ttu-id="383f6-172">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="383f6-172">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="383f6-173">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="383f6-173">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="383f6-174">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="383f6-174">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="383f6-175">**Streaming Suave**</span><span class="sxs-lookup"><span data-stu-id="383f6-175">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)

    
## <a name="media-services-learning-paths"></a><span data-ttu-id="383f6-176">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="383f6-176">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="383f6-177">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="383f6-177">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="383f6-178">Consulte também</span><span class="sxs-lookup"><span data-stu-id="383f6-178">See Also</span></span>
[<span data-ttu-id="383f6-179">Visão geral de manifestos dinâmicos</span><span class="sxs-lookup"><span data-stu-id="383f6-179">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

