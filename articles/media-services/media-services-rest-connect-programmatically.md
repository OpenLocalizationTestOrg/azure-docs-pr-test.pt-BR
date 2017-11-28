---
title: "Conectando a Conta dos Serviços de Mídia usando a API REST | Microsoft Docs"
description: "Este tópico demonstra como conectar os Serviços de Mídia usando a API REST."
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
ms.openlocfilehash: 4feb0eb81823835e8e0b701463d85b27f5598019
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="connecting-to-media-services-account-using-media-services-rest-api"></a><span data-ttu-id="0430f-103">Conectando-se a conta dos serviços de mídia usando a API REST dos serviços de mídia</span><span class="sxs-lookup"><span data-stu-id="0430f-103">Connecting to Media Services Account using Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0430f-104">.NET</span><span class="sxs-lookup"><span data-stu-id="0430f-104">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> * [<span data-ttu-id="0430f-105">REST</span><span class="sxs-lookup"><span data-stu-id="0430f-105">REST</span></span>](media-services-rest-connect-programmatically.md)
> 
> 

<span data-ttu-id="0430f-106">Este tópico descreve como obter uma conexão programática com os Serviços de Mídia do Microsoft Azure quando você está programando com a API REST dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="0430f-106">This topic describes how to obtain a programmatic connection to Microsoft Azure Media Services when you are programming with the Media Services REST API.</span></span>

<span data-ttu-id="0430f-107">Duas coisas são necessárias ao acessar os Serviços de Mídia do Microsoft Azure: um token de acesso fornecido pelos ACSs (Serviços de Controle de Acesso) e o URI dos Serviços de Mídia em si.</span><span class="sxs-lookup"><span data-stu-id="0430f-107">Two things are required when accessing Microsoft Azure Media Services: An access token provided by Azure Access Control Services (ACS), and the URI of Media Services itself.</span></span> <span data-ttu-id="0430f-108">Você pode usar os meios que desejar ao criar essas solicitações desde que especifique os valores de cabeçalho corretos e passar o token de acesso corretamente ao chamar nos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="0430f-108">You can use any means you want when creating these requests as long as you specify the correct header values and pass in the access token correctly when calling into Media Services.</span></span>

<span data-ttu-id="0430f-109">As etapas a seguir descrevem o fluxo de trabalho mais comum ao usar a API REST dos serviços de mídia para se conectar aos serviços de mídia:</span><span class="sxs-lookup"><span data-stu-id="0430f-109">The following steps describe the most common workflow when using the Media Services REST API to connect to Media Services:</span></span>

1. <span data-ttu-id="0430f-110">Obtendo um token de acesso</span><span class="sxs-lookup"><span data-stu-id="0430f-110">Getting an access token</span></span> 
2. <span data-ttu-id="0430f-111">Conectando o URI dos serviços de mídia</span><span class="sxs-lookup"><span data-stu-id="0430f-111">Connecting to the Media Services URI</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="0430f-112">Depois de se conectar com êxito em https://media.windows.net, você receberá um redirecionamento 301 especificando outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="0430f-112">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="0430f-113">Você deve fazer chamadas subsequentes para o novo URI.</span><span class="sxs-lookup"><span data-stu-id="0430f-113">You must make subsequent calls to the new URI.</span></span>
   > <span data-ttu-id="0430f-114">Você também poderá receber uma resposta HTTP/1.1 200 que contém a descrição de metadados API ODATA.</span><span class="sxs-lookup"><span data-stu-id="0430f-114">You may also receive a HTTP/1.1 200 response that contains the ODATA API metadata description.</span></span>
   > 
   > 
3. <span data-ttu-id="0430f-115">Poste suas chamadas de API subsequentes para a nova URL.</span><span class="sxs-lookup"><span data-stu-id="0430f-115">Post your subsequent API calls to the new URL.</span></span> 
   
    <span data-ttu-id="0430f-116">Por exemplo, se depois de tentar se conectar, você tem o seguinte:</span><span class="sxs-lookup"><span data-stu-id="0430f-116">For example, if after trying to connect, you got the following:</span></span>
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    <span data-ttu-id="0430f-117">Você deve postar suas chamadas de API subsequentes para https://wamsbayclus001rest-hs.cloudapp.net/api/.</span><span class="sxs-lookup"><span data-stu-id="0430f-117">You should post your subsequent API calls to https://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

    >[!NOTE]
    ><span data-ttu-id="0430f-118">Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="0430f-118">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="0430f-119">Use a mesma ID de política, se você estiver sempre usando os mesmos dias/permissões de acesso, por exemplo, políticas de localizadores que devem permanecer no local por um longo período (políticas de não carregamento).</span><span class="sxs-lookup"><span data-stu-id="0430f-119">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="0430f-120">Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="0430f-120">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="access-control-address"></a><span data-ttu-id="0430f-121">Endereço de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="0430f-121">Access control address</span></span>
<span data-ttu-id="0430f-122">O endereço de controle de acesso de serviços de mídia é https://wamsprodglobal001acs.accesscontrol.windows.net, exceto para a região norte da China, onde é https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span><span class="sxs-lookup"><span data-stu-id="0430f-122">Media Services access control address is https://wamsprodglobal001acs.accesscontrol.windows.net, except for North China region, where it is https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span></span>

## <a name="getting-an-access-token"></a><span data-ttu-id="0430f-123">Obtendo um token de acesso</span><span class="sxs-lookup"><span data-stu-id="0430f-123">Getting an access token</span></span>
<span data-ttu-id="0430f-124">Para acessar os serviços de mídia diretamente por meio da API REST, recupere um token de acesso do ACS e use-o durante todas as solicitações HTTP feitas no serviço.</span><span class="sxs-lookup"><span data-stu-id="0430f-124">To access Media Services directly through the REST API, retrieve an access token from ACS and use it during every HTTP request you make into the service.</span></span> <span data-ttu-id="0430f-125">Esse token é semelhante aos outros tokens fornecidos pelo ACS com base nas declarações de acesso fornecidas no cabeçalho de uma solicitação HTTP e usando o protocolo OAuth v2.</span><span class="sxs-lookup"><span data-stu-id="0430f-125">This token is similar to other tokens provided by ACS based on access claims provided in the header of an HTTP request and using the OAuth v2 protocol.</span></span> <span data-ttu-id="0430f-126">Não é necessário qualquer outro pré-requisito antes de conectar-se diretamente aos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="0430f-126">You do not need any other prerequisites before directly connecting to Media Services.</span></span>

<span data-ttu-id="0430f-127">O exemplo a seguir mostra o cabeçalho de solicitação HTTP e o corpo usado para recuperar um token.</span><span class="sxs-lookup"><span data-stu-id="0430f-127">The following example shows the HTTP request header and body used to retrieve a token.</span></span>

<span data-ttu-id="0430f-128">**Cabeçalho**:</span><span class="sxs-lookup"><span data-stu-id="0430f-128">**Header**:</span></span>

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


<span data-ttu-id="0430f-129">**Corpo**:</span><span class="sxs-lookup"><span data-stu-id="0430f-129">**Body**:</span></span>

<span data-ttu-id="0430f-130">Você precisa provar os valores de client_id e client_secret no corpo dessa solicitação. O client_id e client_secret correspondem a valores AccountName e AccountKey, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="0430f-130">You need to prove the client_id and client_secret values in the body of this request; client_id and client_secret correspond to the AccountName and AccountKey values, respectively.</span></span> <span data-ttu-id="0430f-131">Esses valores são fornecidos a você pelos serviços de mídia ao configurar sua conta.</span><span class="sxs-lookup"><span data-stu-id="0430f-131">These values are provided to you by Media Services when you set up your account.</span></span> 

<span data-ttu-id="0430f-132">Observe que a AccountKey da sua conta de Serviços de Mídia deve ter a codificação de URL (consulte [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) ao ser usado como o valor de client_secret em sua solicitação de token de acesso.</span><span class="sxs-lookup"><span data-stu-id="0430f-132">Note that the AccountKey for your Media Services account must be URL-encoded (see [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) when using it as the client_secret value in your access token request.</span></span>

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="0430f-133">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0430f-133">For example:</span></span> 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="0430f-134">O exemplo a seguir mostra a resposta HTTP que contém o token de acesso no corpo da resposta.</span><span class="sxs-lookup"><span data-stu-id="0430f-134">The following example shows the HTTP response that contains the access token in the response body.</span></span>

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
> <span data-ttu-id="0430f-135">É recomendável armazenar em cache os valores "access_token" e "expires_in" em um armazenamento externo.</span><span class="sxs-lookup"><span data-stu-id="0430f-135">It is recommended to cache the "access_token " and "expires_in " values to an external storage.</span></span> <span data-ttu-id="0430f-136">Os dados do token podem ser recuperados posteriormente a partir do armazenamento e reutilizados em suas chamadas de API REST dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="0430f-136">The token data could later be retrieved from the storage and re-used in your Media Services REST API calls.</span></span> <span data-ttu-id="0430f-137">Isso é especialmente útil para cenários em que o token pode ser compartilhado com segurança entre vários processos ou computadores.</span><span class="sxs-lookup"><span data-stu-id="0430f-137">This is especially useful for scenarios where the token can be securely shared among multiple processes or computers.</span></span>
> 
> 

<span data-ttu-id="0430f-138">Certifique-se de monitorar o valor "expires_in" do token de acesso e atualizar suas chamadas de API REST com novos tokens, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="0430f-138">Make sure to monitor the "expires_in" value of the access token and update your REST API calls with new tokens as needed.</span></span>

### <a name="connecting-to-the-media-services-uri"></a><span data-ttu-id="0430f-139">Conectando o URI dos serviços de mídia</span><span class="sxs-lookup"><span data-stu-id="0430f-139">Connecting to the Media Services URI</span></span>
<span data-ttu-id="0430f-140">O URI raiz para os serviços de mídia é https://media.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="0430f-140">The root URI for Media Services is https://media.windows.net/.</span></span> <span data-ttu-id="0430f-141">Inicialmente, você deve se conectar a esse URI, e se obtiver um redirecionamento 301 em resposta, deverá fazer chamadas subsequentes para o novo URI.</span><span class="sxs-lookup"><span data-stu-id="0430f-141">You should initially connect to this URI, and if you get a 301 redirect back in response, you should make subsequent calls to the new URI.</span></span> <span data-ttu-id="0430f-142">Além disso, não use nenhuma lógica de redirecionamento/acompanhamento automático nas solicitações.</span><span class="sxs-lookup"><span data-stu-id="0430f-142">In addition, do not use any auto-redirect/follow logic in your requests.</span></span> <span data-ttu-id="0430f-143">Verbos HTTP e corpos de solicitação não serão encaminhados para o novo URI.</span><span class="sxs-lookup"><span data-stu-id="0430f-143">HTTP verbs and request bodies will not be forwarded to the new URI.</span></span>

<span data-ttu-id="0430f-144">Observe que o URI raiz para carregar e baixar arquivos de ativo é https://yourstorageaccount.blob.core.windows.net/ onde o nome da conta de armazenamento é o mesmo usado durante a configuração da conta de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="0430f-144">Note that the root URI for uploading and downloading Asset files is https://yourstorageaccount.blob.core.windows.net/ where the storage account name is the same one you used during your Media Services account setup.</span></span>

<span data-ttu-id="0430f-145">O exemplo a seguir demonstra a solicitação HTTP para o URI raiz dos Serviços de Mídia (https://media.windows.net/).</span><span class="sxs-lookup"><span data-stu-id="0430f-145">The following example demonstrates HTTP request to the Media Services root URI (https://media.windows.net/).</span></span> <span data-ttu-id="0430f-146">A solicitação obtém um redirecionamento 301 em resposta.</span><span class="sxs-lookup"><span data-stu-id="0430f-146">The request gets a 301 redirect back in response.</span></span> <span data-ttu-id="0430f-147">A solicitação subsequente está usando o novo URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span><span class="sxs-lookup"><span data-stu-id="0430f-147">The subsequent request is using the new URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span></span>     

<span data-ttu-id="0430f-148">**Solicitação HTTP**:</span><span class="sxs-lookup"><span data-stu-id="0430f-148">**HTTP Request**:</span></span>

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


<span data-ttu-id="0430f-149">**Resposta HTTP**:</span><span class="sxs-lookup"><span data-stu-id="0430f-149">**HTTP Response**:</span></span>

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
    <h2>Object moved to <a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


<span data-ttu-id="0430f-150">**Solicitação HTTP** (usando o novo URI):</span><span class="sxs-lookup"><span data-stu-id="0430f-150">**HTTP Request** (using the new URI):</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="0430f-151">**Resposta HTTP**:</span><span class="sxs-lookup"><span data-stu-id="0430f-151">**HTTP Response**:</span></span>

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
> <span data-ttu-id="0430f-152">Depois que obtiver o novo URI, este é o URI que deve ser usado para se comunicar com os serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="0430f-152">Once you get the new URI, that is the URI that should be used to communicate with Media Services.</span></span> 
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="0430f-153">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="0430f-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0430f-154">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="0430f-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

