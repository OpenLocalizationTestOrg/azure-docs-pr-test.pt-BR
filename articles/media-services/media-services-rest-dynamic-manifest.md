---
title: "Criando Filtros com a API REST dos Serviços de Mídia do Azure | Microsoft Docs"
description: "Este tópico descreve como criar filtros para que seu cliente possa usá-los na transmissão de seções específicas de um fluxo. Os Serviços de Mídia criam manifestos dinâmicos para atingir esse streaming seletivo."
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
ms.openlocfilehash: 76d2721138668d9f0a908af3fa42840309b068ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="creating-filters-with-azure-media-services-rest-api"></a><span data-ttu-id="995d7-104">Criando filtros com a API REST dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="995d7-104">Creating Filters with Azure Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="995d7-105">.NET</span><span class="sxs-lookup"><span data-stu-id="995d7-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="995d7-106">REST</span><span class="sxs-lookup"><span data-stu-id="995d7-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="995d7-107">A partir da versão 2.11, os Serviços de Mídia permitem definir filtros para seus ativos.</span><span class="sxs-lookup"><span data-stu-id="995d7-107">Starting with 2.11 release, Media Services enables you to define filters for your assets.</span></span> <span data-ttu-id="995d7-108">Esses filtros são regras do lado do servidor que permitirão aos clientes optar por realizar ações como: reproduzir apenas uma seção de um vídeo (em vez de reproduzir o vídeo inteiro) ou especificar apenas um subconjunto de representações de áudio e vídeo com o qual o dispositivo do cliente pode lidar (em vez de todas as representações que estão associadas ao ativo).</span><span class="sxs-lookup"><span data-stu-id="995d7-108">These filters are server side rules that will allow your customers to choose to do things like: playback only a section of a video (instead of playing the whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all the renditions that are associated with the asset).</span></span> <span data-ttu-id="995d7-109">A filtragem de ativos é arquivada por meio de **Manifestos Dinâmicos**criados mediante solicitação do cliente para transmitir um vídeo com base em filtros especificados.</span><span class="sxs-lookup"><span data-stu-id="995d7-109">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request to stream a video based on specified filter(s).</span></span>

<span data-ttu-id="995d7-110">Para obter mais informações relacionadas a filtros e ao Manifesto Dinâmico, consulte [Visão geral de manifestos dinâmicos](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="995d7-110">For more detailed information related to filters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="995d7-111">Este tópico mostra como usar APIs REST para criar, atualizar e excluir os filtros.</span><span class="sxs-lookup"><span data-stu-id="995d7-111">This topic shows how to use REST APIs to create, update, and delete filters.</span></span> 

## <a name="types-used-to-create-filters"></a><span data-ttu-id="995d7-112">Tipos usados para criar filtros</span><span class="sxs-lookup"><span data-stu-id="995d7-112">Types used to create filters</span></span>
<span data-ttu-id="995d7-113">Os tipos a seguir são usados durante a criação de filtros:</span><span class="sxs-lookup"><span data-stu-id="995d7-113">The following types are used when creating filters:</span></span>  

* [<span data-ttu-id="995d7-114">Filter</span><span class="sxs-lookup"><span data-stu-id="995d7-114">Filter</span></span>](https://docs.microsoft.com/rest/api/media/operations/filter)
* [<span data-ttu-id="995d7-115">AssetFilter</span><span class="sxs-lookup"><span data-stu-id="995d7-115">AssetFilter</span></span>](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* [<span data-ttu-id="995d7-116">PresentationTimeRange</span><span class="sxs-lookup"><span data-stu-id="995d7-116">PresentationTimeRange</span></span>](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* [<span data-ttu-id="995d7-117">FilterTrackSelect e FilterTrackPropertyCondition</span><span class="sxs-lookup"><span data-stu-id="995d7-117">FilterTrackSelect and FilterTrackPropertyCondition</span></span>](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

>[!NOTE]

><span data-ttu-id="995d7-118">Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="995d7-118">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="995d7-119">Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="995d7-119">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="995d7-120">Conectar-se aos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="995d7-120">Connect to Media Services</span></span>

<span data-ttu-id="995d7-121">Para saber mais sobre como conectar-se à API do AMS, veja [Acessar a API dos Serviços de Mídia do Azure com a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="995d7-121">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="995d7-122">Depois de se conectar com êxito em https://media.windows.net, você receberá um redirecionamento 301 especificando outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="995d7-122">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="995d7-123">Você deve fazer chamadas subsequentes para o novo URI.</span><span class="sxs-lookup"><span data-stu-id="995d7-123">You must make subsequent calls to the new URI.</span></span>

## <a name="create-filters"></a><span data-ttu-id="995d7-124">Criar filtros</span><span class="sxs-lookup"><span data-stu-id="995d7-124">Create filters</span></span>
### <a name="create-global-filters"></a><span data-ttu-id="995d7-125">Criar filtros globais</span><span class="sxs-lookup"><span data-stu-id="995d7-125">Create global Filters</span></span>
<span data-ttu-id="995d7-126">Para criar um filtro global, use as seguintes solicitações HTTP:</span><span class="sxs-lookup"><span data-stu-id="995d7-126">To create a global Filter, use the following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="995d7-127">Solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="995d7-127">HTTP Request</span></span>
<span data-ttu-id="995d7-128">Cabeçalhos de solicitação</span><span class="sxs-lookup"><span data-stu-id="995d7-128">Request Headers</span></span>

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

<span data-ttu-id="995d7-129">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="995d7-129">Request body</span></span> 

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




#### <a name="http-response"></a><span data-ttu-id="995d7-130">Resposta HTTP</span><span class="sxs-lookup"><span data-stu-id="995d7-130">HTTP Response</span></span>
    HTTP/1.1 201 Created 

### <a name="create-local-assetfilters"></a><span data-ttu-id="995d7-131">Criar AssetFilters local</span><span class="sxs-lookup"><span data-stu-id="995d7-131">Create local AssetFilters</span></span>
<span data-ttu-id="995d7-132">Para criar um AssetFilter local, use as seguintes solicitações HTTP:</span><span class="sxs-lookup"><span data-stu-id="995d7-132">To create a local AssetFilter, use the following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="995d7-133">Solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="995d7-133">HTTP Request</span></span>
<span data-ttu-id="995d7-134">Cabeçalhos de solicitação</span><span class="sxs-lookup"><span data-stu-id="995d7-134">Request Headers</span></span>

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

<span data-ttu-id="995d7-135">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="995d7-135">Request body</span></span> 

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

#### <a name="http-response"></a><span data-ttu-id="995d7-136">Resposta HTTP</span><span class="sxs-lookup"><span data-stu-id="995d7-136">HTTP Response</span></span>
    HTTP/1.1 201 Created 
    . . . 

## <a name="list-filters"></a><span data-ttu-id="995d7-137">Listar filtros</span><span class="sxs-lookup"><span data-stu-id="995d7-137">List filters</span></span>
### <a name="get-all-global-filters-in-the-ams-account"></a><span data-ttu-id="995d7-138">Obter todos os **filtros**globais na conta AMS</span><span class="sxs-lookup"><span data-stu-id="995d7-138">Get all global **Filter**s in the AMS account</span></span>
<span data-ttu-id="995d7-139">Para listar filtros, use as seguintes solicitações HTTP:</span><span class="sxs-lookup"><span data-stu-id="995d7-139">To list filters, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="995d7-140">Solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="995d7-140">HTTP Request</span></span>
    GET https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

### <a name="get-assetfilters-associated-with-an-asset"></a><span data-ttu-id="995d7-141">Obter **AssetFilter**s associados a um ativo</span><span class="sxs-lookup"><span data-stu-id="995d7-141">Get **AssetFilter**s associated with an asset</span></span>
#### <a name="http-request"></a><span data-ttu-id="995d7-142">Solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="995d7-142">HTTP Request</span></span>
    GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

### <a name="get-an-assetfilter-based-on-its-id"></a><span data-ttu-id="995d7-143">Obter um **AssetFilter** com base em sua ID</span><span class="sxs-lookup"><span data-stu-id="995d7-143">Get an **AssetFilter** based on its Id</span></span>
#### <a name="http-request"></a><span data-ttu-id="995d7-144">Solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="995d7-144">HTTP Request</span></span>
    GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000


## <a name="update-filters"></a><span data-ttu-id="995d7-145">Atualizar filtros</span><span class="sxs-lookup"><span data-stu-id="995d7-145">Update filters</span></span>
<span data-ttu-id="995d7-146">Use o PATCH, PUT ou MERGE para atualizar um filtro com novos valores de propriedade.</span><span class="sxs-lookup"><span data-stu-id="995d7-146">Use PATCH, PUT or MERGE to update a filter with new property values.</span></span>  <span data-ttu-id="995d7-147">Para obter mais informações sobre essas operações, consulte [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="995d7-147">For more information about these operations, see [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="995d7-148">Ao atualizar um filtro, talvez sejam necessários até 2 minutos para que o ponto de extremidade do streaming atualize as regras.</span><span class="sxs-lookup"><span data-stu-id="995d7-148">If you update a filter, it can take up to 2 minutes for streaming endpoint to refresh the rules.</span></span> <span data-ttu-id="995d7-149">Se o conteúdo foi servido usando esse filtro (e armazenado em cache nos proxies e caches CDN), atualizar esse filtro pode resultar em falhas do player.</span><span class="sxs-lookup"><span data-stu-id="995d7-149">If the content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="995d7-150">É recomendável limpar o cache depois de atualizar o filtro.</span><span class="sxs-lookup"><span data-stu-id="995d7-150">It is recommend to clear the cache after updating the filter.</span></span> <span data-ttu-id="995d7-151">Se essa opção não for possível, considere usar um filtro diferente.</span><span class="sxs-lookup"><span data-stu-id="995d7-151">If this option is not possible, consider using a different filter.</span></span>  

### <a name="update-global-filters"></a><span data-ttu-id="995d7-152">Atualizar filtros globais</span><span class="sxs-lookup"><span data-stu-id="995d7-152">Update global Filters</span></span>
<span data-ttu-id="995d7-153">Para atualizar um filtro global, use as seguintes solicitações HTTP:</span><span class="sxs-lookup"><span data-stu-id="995d7-153">To update a global filter, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="995d7-154">Solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="995d7-154">HTTP Request</span></span>
<span data-ttu-id="995d7-155">Cabeçalhos de solicitação:</span><span class="sxs-lookup"><span data-stu-id="995d7-155">Request headers:</span></span> 

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

<span data-ttu-id="995d7-156">Corpo da solicitação:</span><span class="sxs-lookup"><span data-stu-id="995d7-156">Request body:</span></span> 

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

### <a name="update-local-assetfilters"></a><span data-ttu-id="995d7-157">Atualizar AssetFilters local</span><span class="sxs-lookup"><span data-stu-id="995d7-157">Update local AssetFilters</span></span>
<span data-ttu-id="995d7-158">Para atualizar um filtro local, use as seguintes solicitações HTTP:</span><span class="sxs-lookup"><span data-stu-id="995d7-158">To update a local filter, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="995d7-159">Solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="995d7-159">HTTP Request</span></span>
<span data-ttu-id="995d7-160">Cabeçalhos de solicitação:</span><span class="sxs-lookup"><span data-stu-id="995d7-160">Request headers:</span></span> 

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

<span data-ttu-id="995d7-161">Corpo da solicitação:</span><span class="sxs-lookup"><span data-stu-id="995d7-161">Request body:</span></span> 

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


## <a name="delete-filters"></a><span data-ttu-id="995d7-162">Excluir filtros</span><span class="sxs-lookup"><span data-stu-id="995d7-162">Delete filters</span></span>
### <a name="delete-global-filters"></a><span data-ttu-id="995d7-163">Excluir filtros globais</span><span class="sxs-lookup"><span data-stu-id="995d7-163">Delete global Filters</span></span>
<span data-ttu-id="995d7-164">Para excluir um filtro global, use as seguintes solicitações HTTP:</span><span class="sxs-lookup"><span data-stu-id="995d7-164">To delete a global Filter, use the following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="995d7-165">Solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="995d7-165">HTTP Request</span></span>
    DELETE https://media.windows.net/api/Filters('GlobalFilter') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 


### <a name="delete-local-assetfilters"></a><span data-ttu-id="995d7-166">Excluir AssetFilters local</span><span class="sxs-lookup"><span data-stu-id="995d7-166">Delete local AssetFilters</span></span>
<span data-ttu-id="995d7-167">Para excluir um AssetFilter local, use as seguintes solicitações HTTP:</span><span class="sxs-lookup"><span data-stu-id="995d7-167">To delete a local AssetFilter, use the following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="995d7-168">Solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="995d7-168">HTTP Request</span></span>
    DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__LocalFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="995d7-169">Criar URLs de streaming que usam filtros</span><span class="sxs-lookup"><span data-stu-id="995d7-169">Build streaming URLs that use filters</span></span>
<span data-ttu-id="995d7-170">Para obter informações sobre como publicar e distribuir seus ativos, consulte [Visão geral do fornecimento de conteúdo a clientes](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="995d7-170">For information on how to publish and deliver your assets, see [Delivering Content to Customers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="995d7-171">Os exemplos a seguir mostram como adicionar filtros às URLs de streaming.</span><span class="sxs-lookup"><span data-stu-id="995d7-171">The following examples show how to add filters to your streaming URLs.</span></span>

<span data-ttu-id="995d7-172">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="995d7-172">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="995d7-173">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="995d7-173">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="995d7-174">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="995d7-174">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="995d7-175">**Streaming Suave**</span><span class="sxs-lookup"><span data-stu-id="995d7-175">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)

    
## <a name="media-services-learning-paths"></a><span data-ttu-id="995d7-176">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="995d7-176">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="995d7-177">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="995d7-177">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="995d7-178">Consulte também</span><span class="sxs-lookup"><span data-stu-id="995d7-178">See Also</span></span>
[<span data-ttu-id="995d7-179">Visão geral de manifestos dinâmicos</span><span class="sxs-lookup"><span data-stu-id="995d7-179">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

