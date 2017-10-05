---
title: "Publicar conteúdo dos Serviços de Mídia do Azure usando o REST"
description: "Saiba como criar um localizador que é usado para construir um URL de transmissão. O código usa a API REST."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: ff332c30-30c6-4ed1-99d0-5fffd25d4f23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: d1e0a112040f6aa4cfa9e8c323507b1c0a223f3e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="publish-azure-media-services-content-using-rest"></a><span data-ttu-id="bb93c-104">Publicar conteúdo dos Serviços de Mídia do Azure usando o REST</span><span class="sxs-lookup"><span data-stu-id="bb93c-104">Publish Azure Media Services content using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bb93c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="bb93c-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="bb93c-106">REST</span><span class="sxs-lookup"><span data-stu-id="bb93c-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="bb93c-107">Portal</span><span class="sxs-lookup"><span data-stu-id="bb93c-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="bb93c-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="bb93c-108">Overview</span></span>
<span data-ttu-id="bb93c-109">Você pode transmitir um conjunto de MP4 com taxa de bits adaptável ao criar um localizador de streaming sob demanda e criar uma URL de transmissão.</span><span class="sxs-lookup"><span data-stu-id="bb93c-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="bb93c-110">O tópico [codificando um ativo](media-services-rest-encode-asset.md) mostra como codificar um conjunto de MP4 de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="bb93c-110">The [encoding an asset](media-services-rest-encode-asset.md) topic shows how to encode into an adaptive bitrate MP4 set.</span></span> <span data-ttu-id="bb93c-111">Se o seu conteúdo for criptografado, configure a política de entrega de ativos (conforme descrito [neste](media-services-rest-configure-asset-delivery-policy.md) tópico) antes de criar um localizador.</span><span class="sxs-lookup"><span data-stu-id="bb93c-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-rest-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 

<span data-ttu-id="bb93c-112">Você também pode usar um localizador de streaming sob demanda para criar URLs que apontam para arquivos MP4 que podem ser baixados progressivamente.</span><span class="sxs-lookup"><span data-stu-id="bb93c-112">You can also use an OnDemand streaming locator to build URLs that point to MP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="bb93c-113">Este tópico mostra como criar um localizador de streaming sob demanda para publicar seu ativo e compilar um Smooth, MPEG DASH e URLs de streaming do HLS.</span><span class="sxs-lookup"><span data-stu-id="bb93c-113">This topic shows how to create an OnDemand streaming locator in order to publish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="bb93c-114">Ele também mostra se mostra muito interessado em criar URLs de download progressivo.</span><span class="sxs-lookup"><span data-stu-id="bb93c-114">It also shows hot to build progressive download URLs.</span></span>

<span data-ttu-id="bb93c-115">A seção [a seguir](#types) mostra os tipos de enumeração cujos valores são usados nas chamadas de REST.</span><span class="sxs-lookup"><span data-stu-id="bb93c-115">The [following](#types) section shows the enum types whose values are used in the REST calls.</span></span>   

> [!NOTE]
> <span data-ttu-id="bb93c-116">Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="bb93c-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="bb93c-117">Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="bb93c-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-to-media-services"></a><span data-ttu-id="bb93c-118">Conectar-se aos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="bb93c-118">Connect to Media Services</span></span>

<span data-ttu-id="bb93c-119">Para saber mais sobre como conectar-se à API do AMS, veja [Acessar a API dos Serviços de Mídia do Azure com a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="bb93c-119">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="bb93c-120">Depois de se conectar com êxito em https://media.windows.net, você receberá um redirecionamento 301 especificando outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="bb93c-120">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="bb93c-121">Você deve fazer chamadas subsequentes para o novo URI.</span><span class="sxs-lookup"><span data-stu-id="bb93c-121">You must make subsequent calls to the new URI.</span></span>

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="bb93c-122">Criar um localizador de streaming sob demanda</span><span class="sxs-lookup"><span data-stu-id="bb93c-122">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="bb93c-123">Para criar o localizador de streaming sob demanda e obter URLs, você precisa fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bb93c-123">To create the OnDemand streaming locator and get URLs you need to do the following:</span></span>

1. <span data-ttu-id="bb93c-124">Se o conteúdo for criptografado, defina uma política de acesso.</span><span class="sxs-lookup"><span data-stu-id="bb93c-124">If the content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="bb93c-125">Criar um localizador de streaming sob demanda.</span><span class="sxs-lookup"><span data-stu-id="bb93c-125">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="bb93c-126">Se você planeja transmitir, obtenha o arquivo de manifesto do streaming (.ism) no ativo.</span><span class="sxs-lookup"><span data-stu-id="bb93c-126">If you plan to stream, get the streaming manifest file (.ism) in the asset.</span></span> 
   
   <span data-ttu-id="bb93c-127">Se você planeja fazer download progressivo, obtenha os nomes dos arquivos MP4 no ativo.</span><span class="sxs-lookup"><span data-stu-id="bb93c-127">If you plan to progressively download, get the names of MP4 files in the asset.</span></span> 
4. <span data-ttu-id="bb93c-128">Crie URLs para o arquivo de manifesto ou arquivos MP4.</span><span class="sxs-lookup"><span data-stu-id="bb93c-128">Build URLs to the manifest file or MP4 files.</span></span> 
5. <span data-ttu-id="bb93c-129">Observe que você não pode criar um localizador de streaming usando um AccessPolicy que inclui permissões de gravação ou de exclusão.</span><span class="sxs-lookup"><span data-stu-id="bb93c-129">Note that you cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.</span></span>

### <a name="create-an-access-policy"></a><span data-ttu-id="bb93c-130">Crie uma política de acesso</span><span class="sxs-lookup"><span data-stu-id="bb93c-130">Create an access policy</span></span>

>[!NOTE]
><span data-ttu-id="bb93c-131">Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="bb93c-131">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="bb93c-132">Use a mesma ID de política, se você estiver sempre usando os mesmos dias/permissões de acesso, por exemplo, políticas de localizadores que devem permanecer no local por um longo período (políticas de não carregamento).</span><span class="sxs-lookup"><span data-stu-id="bb93c-132">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="bb93c-133">Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="bb93c-133">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="bb93c-134">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="bb93c-134">Request:</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstest1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1424263184&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=NWE%2f986Hr5lZTzVGKtC%2ftzHm9n6U%2fxpTFULItxKUGC4%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 6bcfd511-a561-448d-a022-a319a89ecffa
    Host: media.windows.net
    Content-Length: 68

    {"Name":"access policy","DurationInMinutes":43200.0,"Permissions":1}

<span data-ttu-id="bb93c-135">Resposta:</span><span class="sxs-lookup"><span data-stu-id="bb93c-135">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 311
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https:/media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3A69c80d98-7830-407f-a9af-e25f4b0d3e5f')
    Server: Microsoft-IIS/8.5
    request-id: a877528a-bdb4-4414-9862-273f8e64f882
    x-ms-request-id: a877528a-bdb4-4414-9862-273f8e64f882
    x-ms-client-request-id: 6bcfd511-a561-448d-a022-a319a89ecffa
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 18 Feb 2015 06:52:09 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AccessPolicies/@Element","Id":"nb:pid:UUID:69c80d98-7830-407f-a9af-e25f4b0d3e5f","Created":"2015-02-18T06:52:09.8862191Z","LastModified":"2015-02-18T06:52:09.8862191Z","Name":"access policy","DurationInMinutes":43200.0,"Permissions":1}

### <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="bb93c-136">Criar um localizador de streaming sob demanda</span><span class="sxs-lookup"><span data-stu-id="bb93c-136">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="bb93c-137">Crie o localizador para o ativo especificado e a política de ativo.</span><span class="sxs-lookup"><span data-stu-id="bb93c-137">Create the locator for the specified asset and asset policy.</span></span>

<span data-ttu-id="bb93c-138">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="bb93c-138">Request:</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstest1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1424263184&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=NWE%2f986Hr5lZTzVGKtC%2ftzHm9n6U%2fxpTFULItxKUGC4%3d
    x-ms-version: 2.11
    x-ms-client-request-id: ac159492-9a0c-40c3-aacc-551b1b4c5f62
    Host: media.windows.net
    Content-Length: 181

    {"AccessPolicyId":"nb:pid:UUID:1480030d-c481-430a-9687-535c6a5cb272","AssetId":"nb:cid:UUID:cc1e445d-1500-80bd-538e-f1e4b71b465e","StartTime":"2015-02-18T06:34:47.267872Z","Type":2}

<span data-ttu-id="bb93c-139">Resposta:</span><span class="sxs-lookup"><span data-stu-id="bb93c-139">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 637
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Abe245661-2bbd-4fc6-b14f-9cf9a1492e5e')
    Server: Microsoft-IIS/8.5
    request-id: 5bd5864a-0afd-44c0-a67a-4044a2c9043b
    x-ms-request-id: 5bd5864a-0afd-44c0-a67a-4044a2c9043b
    x-ms-client-request-id: ac159492-9a0c-40c3-aacc-551b1b4c5f62
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 18 Feb 2015 06:58:37 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#Locators/@Element","Id":"nb:lid:UUID:be245661-2bbd-4fc6-b14f-9cf9a1492e5e","ExpirationDateTime":"2015-03-20T06:34:47.267872+00:00","Type":2,"Path":"http://amstest1.streaming.mediaservices.windows.net/be245661-2bbd-4fc6-b14f-9cf9a1492e5e/","BaseUri":"http://amstest1.streaming.mediaservices.windows.net","ContentAccessComponent":"be245661-2bbd-4fc6-b14f-9cf9a1492e5e","AccessPolicyId":"nb:pid:UUID:1480030d-c481-430a-9687-535c6a5cb272","AssetId":"nb:cid:UUID:cc1e445d-1500-80bd-538e-f1e4b71b465e","StartTime":"2015-02-18T06:34:47.267872+00:00","Name":null}

### <a name="build-streaming-urls"></a><span data-ttu-id="bb93c-140">Criar URLs de streaming</span><span class="sxs-lookup"><span data-stu-id="bb93c-140">Build streaming URLs</span></span>
<span data-ttu-id="bb93c-141">Use o valor **Caminho** retornado após a criação do localizador para criar as URLs MPEG DASH, Smooth e HLS.</span><span class="sxs-lookup"><span data-stu-id="bb93c-141">Use the **Path** value returned after the creation of the locator to build the Smooth, HLS, and MPEG DASH URLs.</span></span> 

<span data-ttu-id="bb93c-142">Smooth Streaming: **Caminho** + nome de arquivo de manifesto + "/manifest"</span><span class="sxs-lookup"><span data-stu-id="bb93c-142">Smooth Streaming: **Path** + manifest file name + "/manifest"</span></span>

<span data-ttu-id="bb93c-143">exemplo:</span><span class="sxs-lookup"><span data-stu-id="bb93c-143">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest

<span data-ttu-id="bb93c-144">HLS: **Caminho** + nome de arquivo de manifesto + "/manifest(format=m3u8-aapl)"</span><span class="sxs-lookup"><span data-stu-id="bb93c-144">HLS: **Path** + manifest file name + "/manifest(format=m3u8-aapl)"</span></span>

<span data-ttu-id="bb93c-145">exemplo:</span><span class="sxs-lookup"><span data-stu-id="bb93c-145">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)


<span data-ttu-id="bb93c-146">DASH: **Caminho** + nome de arquivo de manifesto + "/manifest(format=mpd-time-csf)"</span><span class="sxs-lookup"><span data-stu-id="bb93c-146">DASH: **Path** + manifest file name + "/manifest(format=mpd-time-csf)"</span></span>

<span data-ttu-id="bb93c-147">exemplo:</span><span class="sxs-lookup"><span data-stu-id="bb93c-147">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


### <a name="build-progressive-download-urls"></a><span data-ttu-id="bb93c-148">Crie URLs de download progressivo</span><span class="sxs-lookup"><span data-stu-id="bb93c-148">Build progressive download URLs</span></span>
<span data-ttu-id="bb93c-149">Use o valor **Caminho** retornado após a criação do localizador para criar a URL de download progressivo.</span><span class="sxs-lookup"><span data-stu-id="bb93c-149">Use the **Path** value returned after the creation of the locator to build the progressive download URL.</span></span>   

<span data-ttu-id="bb93c-150">URL: **Caminho** + nome do arquivo MP4 do ativo</span><span class="sxs-lookup"><span data-stu-id="bb93c-150">URL: **Path** + asset file mp4 name</span></span>

<span data-ttu-id="bb93c-151">exemplo:</span><span class="sxs-lookup"><span data-stu-id="bb93c-151">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

## <span data-ttu-id="bb93c-152"><a id="types"></a>Tipos de enum</span><span class="sxs-lookup"><span data-stu-id="bb93c-152"><a id="types"></a>Enum types</span></span>
    [Flags]
    public enum AccessPermissions
    {
        None = 0,
        Read = 1,
        Write = 2,
        Delete = 4,
        List = 8,
    }

    public enum LocatorType
    {
        None = 0,
        Sas = 1,
        OnDemandOrigin = 2,
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="bb93c-153">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="bb93c-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bb93c-154">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="bb93c-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="bb93c-155">Consulte também</span><span class="sxs-lookup"><span data-stu-id="bb93c-155">See also</span></span>
[<span data-ttu-id="bb93c-156">Visão geral da API REST das Operações dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="bb93c-156">Media Services operations REST API overview</span></span>](media-services-rest-how-to-use.md)

[<span data-ttu-id="bb93c-157">Configurar política de entrega de ativos</span><span class="sxs-lookup"><span data-stu-id="bb93c-157">Configure asset delivery policy</span></span>](media-services-rest-configure-asset-delivery-policy.md)

