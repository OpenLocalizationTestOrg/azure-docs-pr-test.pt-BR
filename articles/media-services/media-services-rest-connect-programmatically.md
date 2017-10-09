---
title: "aaaConnecting tooMedia conta de serviços usando a API REST | Microsoft Docs"
description: "Este tópico demonstra como usar do tooconnect tooMedia serviços REST API."
services: media-services
documentationcenter: 
author: Juliako
manager: erikre
editor: 
ms.assetid: 79dc64f1-15d8-4a81-b9d9-3d3c44d2e1e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 1d5064a3612dc96f5c5ad910d183d84fb70a3b6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a><span data-ttu-id="10011-103">Conectando tooMedia conta de serviços usando a API de REST de serviços de mídia</span><span class="sxs-lookup"><span data-stu-id="10011-103">Connecting tooMedia Services Account using Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="10011-104">.NET</span><span class="sxs-lookup"><span data-stu-id="10011-104">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> * [<span data-ttu-id="10011-105">REST</span><span class="sxs-lookup"><span data-stu-id="10011-105">REST</span></span>](media-services-rest-connect-programmatically.md)
> 
> 

<span data-ttu-id="10011-106">Este tópico descreve como tooobtain tooMicrosoft uma conexão programática Azure Media Services quando você está programando com hello API de REST de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="10011-106">This topic describes how tooobtain a programmatic connection tooMicrosoft Azure Media Services when you are programming with hello Media Services REST API.</span></span>

<span data-ttu-id="10011-107">Duas coisas são necessárias ao acessar os serviços de mídia do Microsoft Azure: um token de acesso fornecido pelo Azure Access Control Services (ACS) e Olá URI do Media Services em si.</span><span class="sxs-lookup"><span data-stu-id="10011-107">Two things are required when accessing Microsoft Azure Media Services: An access token provided by Azure Access Control Services (ACS), and hello URI of Media Services itself.</span></span> <span data-ttu-id="10011-108">Você pode usar os meios que desejar ao criar essas solicitações desde que você especifique valores de cabeçalho corretos hello e passa no token de acesso de saudação corretamente ao chamar nos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="10011-108">You can use any means you want when creating these requests as long as you specify hello correct header values and pass in hello access token correctly when calling into Media Services.</span></span>

<span data-ttu-id="10011-109">Olá, as etapas a seguir descreve o fluxo de trabalho de mais comuns do hello quando usar Olá API REST do Media Services tooconnect tooMedia serviços:</span><span class="sxs-lookup"><span data-stu-id="10011-109">hello following steps describe hello most common workflow when using hello Media Services REST API tooconnect tooMedia Services:</span></span>

1. <span data-ttu-id="10011-110">Obtendo um token de acesso</span><span class="sxs-lookup"><span data-stu-id="10011-110">Getting an access token</span></span> 
2. <span data-ttu-id="10011-111">Conectando toohello URI do Media Services</span><span class="sxs-lookup"><span data-stu-id="10011-111">Connecting toohello Media Services URI</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="10011-112">Após conectar-se toohttps://media.windows.net, você receberá um redirecionamento 301 que especifica outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="10011-112">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="10011-113">Você deve fazer chamadas subsequentes toohello novo URI.</span><span class="sxs-lookup"><span data-stu-id="10011-113">You must make subsequent calls toohello new URI.</span></span>
   > <span data-ttu-id="10011-114">Você também pode receber uma resposta HTTP/1.1 200 que contém Olá descrição de metadados ODATA API.</span><span class="sxs-lookup"><span data-stu-id="10011-114">You may also receive a HTTP/1.1 200 response that contains hello ODATA API metadata description.</span></span>
   > 
   > 
3. <span data-ttu-id="10011-115">POST suas chamadas API subsequentes toohello nova URL.</span><span class="sxs-lookup"><span data-stu-id="10011-115">Post your subsequent API calls toohello new URL.</span></span> 
   
    <span data-ttu-id="10011-116">Por exemplo, se depois de tentar tooconnect, você obteve seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="10011-116">For example, if after trying tooconnect, you got hello following:</span></span>
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    <span data-ttu-id="10011-117">Você deve publicar seu subsequentes API chamadas toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span><span class="sxs-lookup"><span data-stu-id="10011-117">You should post your subsequent API calls toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

    >[!NOTE]
    ><span data-ttu-id="10011-118">Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="10011-118">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="10011-119">Você deve usar Olá Olá a mesma ID de política se você estiver usando sempre mesmo dias acesso permissões, por exemplo, as políticas para localizadores são tooremain desejado no local por um longo período (políticas de carregamento não).</span><span class="sxs-lookup"><span data-stu-id="10011-119">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="10011-120">Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="10011-120">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="access-control-address"></a><span data-ttu-id="10011-121">Endereço de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="10011-121">Access control address</span></span>
<span data-ttu-id="10011-122">O endereço de controle de acesso de serviços de mídia é https://wamsprodglobal001acs.accesscontrol.windows.net, exceto para a região norte da China, onde é https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span><span class="sxs-lookup"><span data-stu-id="10011-122">Media Services access control address is https://wamsprodglobal001acs.accesscontrol.windows.net, except for North China region, where it is https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span></span>

## <a name="getting-an-access-token"></a><span data-ttu-id="10011-123">Obtendo um token de acesso</span><span class="sxs-lookup"><span data-stu-id="10011-123">Getting an access token</span></span>
<span data-ttu-id="10011-124">tooaccess serviços de mídia diretamente por meio da API REST do hello, recuperar um token de acesso do ACS e usá-lo durante cada solicitação HTTP que fizer no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="10011-124">tooaccess Media Services directly through hello REST API, retrieve an access token from ACS and use it during every HTTP request you make into hello service.</span></span> <span data-ttu-id="10011-125">Esse token é semelhante tokens tooother fornecidos pelo ACS, com base em declarações de acesso fornecidas no cabeçalho de saudação de uma solicitação HTTP e usar o protocolo de saudação OAuth v2.</span><span class="sxs-lookup"><span data-stu-id="10011-125">This token is similar tooother tokens provided by ACS based on access claims provided in hello header of an HTTP request and using hello OAuth v2 protocol.</span></span> <span data-ttu-id="10011-126">Não é necessário qualquer outro pré-requisito antes de conectar diretamente tooMedia serviços.</span><span class="sxs-lookup"><span data-stu-id="10011-126">You do not need any other prerequisites before directly connecting tooMedia Services.</span></span>

<span data-ttu-id="10011-127">Olá exemplo a seguir mostra cabeçalho de solicitação HTTP hello e tooretrieve do corpo usado um token.</span><span class="sxs-lookup"><span data-stu-id="10011-127">hello following example shows hello HTTP request header and body used tooretrieve a token.</span></span>

<span data-ttu-id="10011-128">**Cabeçalho**:</span><span class="sxs-lookup"><span data-stu-id="10011-128">**Header**:</span></span>

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


<span data-ttu-id="10011-129">**Corpo**:</span><span class="sxs-lookup"><span data-stu-id="10011-129">**Body**:</span></span>

<span data-ttu-id="10011-130">Você precisa os valores tooprove client_id e o client_secret de saudação no corpo de saudação desta solicitação; client_id e o client_secret correspondem toohello AccountName e AccountKey valores, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="10011-130">You need tooprove hello client_id and client_secret values in hello body of this request; client_id and client_secret correspond toohello AccountName and AccountKey values, respectively.</span></span> <span data-ttu-id="10011-131">Esses valores são fornecidos tooyou pelos serviços de mídia quando você configurar sua conta.</span><span class="sxs-lookup"><span data-stu-id="10011-131">These values are provided tooyou by Media Services when you set up your account.</span></span> 

<span data-ttu-id="10011-132">Observe que Olá AccountKey para sua conta de serviços de mídia deve ser codificados de URL (consulte [codificação por percentual](http://tools.ietf.org/html/rfc3986#section-2.1) quando usá-lo como o valor de client_secret Olá em sua solicitação de token de acesso.</span><span class="sxs-lookup"><span data-stu-id="10011-132">Note that hello AccountKey for your Media Services account must be URL-encoded (see [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) when using it as hello client_secret value in your access token request.</span></span>

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="10011-133">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="10011-133">For example:</span></span> 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="10011-134">Hello exemplo a seguir mostra Olá HTTP resposta que contém o acesso de saudação token no corpo de resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="10011-134">hello following example shows hello HTTP response that contains hello access token in hello response body.</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache, no-store
    Pragma: no-cache
    Content-Type: application/json; charset=utf-8
    Expires: -1
    request-id: a65150f5-2784-4a01-a4b7-33456187ad83
    X-Content-Type-Options: nosniff
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 15 Jan 2015 08:07:20 GMT
    Content-Length: 670

    {  
       "token_type":"http://schemas.xmlsoap.org/ws/2009/11/swt-token-profile-1.0",
       "access_token":"http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421330840&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=uf69n82KlqZmkJDNxhJkOxpyIpA2HDyeGUTtSnq1vlE%3d",
       "expires_in":"21600",
       "scope":"urn:WindowsAzureMediaServices"
    }


> [!NOTE]
> <span data-ttu-id="10011-135">É recomendável toocache hello "access_token" e "expires_in" valores tooan armazenamento externo.</span><span class="sxs-lookup"><span data-stu-id="10011-135">It is recommended toocache hello "access_token " and "expires_in " values tooan external storage.</span></span> <span data-ttu-id="10011-136">dados do token Olá posteriormente foi recuperados do armazenamento hello e reutilizados em suas chamadas de API de REST de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="10011-136">hello token data could later be retrieved from hello storage and re-used in your Media Services REST API calls.</span></span> <span data-ttu-id="10011-137">Isso é especialmente útil para cenários onde Olá token pode ser compartilhado com segurança entre vários processos ou computadores.</span><span class="sxs-lookup"><span data-stu-id="10011-137">This is especially useful for scenarios where hello token can be securely shared among multiple processes or computers.</span></span>
> 
> 

<span data-ttu-id="10011-138">Certifique-se de valor de "expires_in" hello toomonitor de acesso de saudação token e atualizar suas chamadas de API REST com novos tokens, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="10011-138">Make sure toomonitor hello "expires_in" value of hello access token and update your REST API calls with new tokens as needed.</span></span>

### <a name="connecting-toohello-media-services-uri"></a><span data-ttu-id="10011-139">Conectando toohello URI do Media Services</span><span class="sxs-lookup"><span data-stu-id="10011-139">Connecting toohello Media Services URI</span></span>
<span data-ttu-id="10011-140">Olá URI raiz para os serviços de mídia é https://media.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="10011-140">hello root URI for Media Services is https://media.windows.net/.</span></span> <span data-ttu-id="10011-141">Você deve conectar toothis URI e se você receber um redirecionamento 301 em resposta, você deve fazer chamadas subsequentes toohello novo URI.</span><span class="sxs-lookup"><span data-stu-id="10011-141">You should initially connect toothis URI, and if you get a 301 redirect back in response, you should make subsequent calls toohello new URI.</span></span> <span data-ttu-id="10011-142">Além disso, não use nenhuma lógica de redirecionamento/acompanhamento automático nas solicitações.</span><span class="sxs-lookup"><span data-stu-id="10011-142">In addition, do not use any auto-redirect/follow logic in your requests.</span></span> <span data-ttu-id="10011-143">Verbos HTTP e corpos de solicitação não serão encaminhados toohello novo URI.</span><span class="sxs-lookup"><span data-stu-id="10011-143">HTTP verbs and request bodies will not be forwarded toohello new URI.</span></span>

<span data-ttu-id="10011-144">Observe que raiz Olá URI para carregar e baixar arquivos de ativo https://yourstorageaccount.blob.core.windows.net/ onde é o nome de conta de armazenamento Olá Olá um mesmo usada durante a configuração da conta de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="10011-144">Note that hello root URI for uploading and downloading Asset files is https://yourstorageaccount.blob.core.windows.net/ where hello storage account name is hello same one you used during your Media Services account setup.</span></span>

<span data-ttu-id="10011-145">saudação de exemplo a seguir demonstra toohello a solicitação HTTP raiz de serviços de mídia URI (https://media.windows.net/).</span><span class="sxs-lookup"><span data-stu-id="10011-145">hello following example demonstrates HTTP request toohello Media Services root URI (https://media.windows.net/).</span></span> <span data-ttu-id="10011-146">solicitação de saudação obtém um redirecionamento 301 em resposta.</span><span class="sxs-lookup"><span data-stu-id="10011-146">hello request gets a 301 redirect back in response.</span></span> <span data-ttu-id="10011-147">Olá solicitação subsequente é usando Olá novo URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span><span class="sxs-lookup"><span data-stu-id="10011-147">hello subsequent request is using hello new URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span></span>     

<span data-ttu-id="10011-148">**Solicitação HTTP**:</span><span class="sxs-lookup"><span data-stu-id="10011-148">**HTTP Request**:</span></span>

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


<span data-ttu-id="10011-149">**Resposta HTTP**:</span><span class="sxs-lookup"><span data-stu-id="10011-149">**HTTP Response**:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
    Server: Microsoft-IIS/8.5
    request-id: 987d7652-497a-44e5-b815-f492e02aef97
    x-ms-request-id: 987d7652-497a-44e5-b815-f492e02aef97
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:53 GMT
    Content-Length: 164

    <html><head><title>Object moved</title></head><body>
    <h2>Object moved too<a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


<span data-ttu-id="10011-150">**Solicitação HTTP** (usando Olá novo URI):</span><span class="sxs-lookup"><span data-stu-id="10011-150">**HTTP Request** (using hello new URI):</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="10011-151">**Resposta HTTP**:</span><span class="sxs-lookup"><span data-stu-id="10011-151">**HTTP Response**:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1250
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    x-ms-request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata","value":[{"name":"AccessPolicies","url":"AccessPolicies"},{"name":"Locators","url":"Locators"},{"name":"ContentKeys","url":"ContentKeys"},{"name":"ContentKeyAuthorizationPolicyOptions","url":"ContentKeyAuthorizationPolicyOptions"},{"name":"ContentKeyAuthorizationPolicies","url":"ContentKeyAuthorizationPolicies"},{"name":"Files","url":"Files"},{"name":"Assets","url":"Assets"},{"name":"AssetDeliveryPolicies","url":"AssetDeliveryPolicies"},{"name":"IngestManifestFiles","url":"IngestManifestFiles"},{"name":"IngestManifestAssets","url":"IngestManifestAssets"},{"name":"IngestManifests","url":"IngestManifests"},{"name":"StorageAccounts","url":"StorageAccounts"},{"name":"Tasks","url":"Tasks"},{"name":"NotificationEndPoints","url":"NotificationEndPoints"},{"name":"Jobs","url":"Jobs"},{"name":"TaskTemplates","url":"TaskTemplates"},{"name":"JobTemplates","url":"JobTemplates"},{"name":"MediaProcessors","url":"MediaProcessors"},{"name":"EncodingReservedUnitTypes","url":"EncodingReservedUnitTypes"},{"name":"Operations","url":"Operations"},{"name":"StreamingEndpoints","url":"StreamingEndpoints"},{"name":"Channels","url":"Channels"},{"name":"Programs","url":"Programs"}]}



> [!NOTE]
> <span data-ttu-id="10011-152">Depois de obter Olá novo URI, que é hello URI que deve ser usado toocommunicate com serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="10011-152">Once you get hello new URI, that is hello URI that should be used toocommunicate with Media Services.</span></span> 
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="10011-153">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="10011-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="10011-154">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="10011-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

