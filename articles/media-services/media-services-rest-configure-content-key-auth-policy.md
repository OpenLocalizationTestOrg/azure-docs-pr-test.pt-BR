---
title: "Configurar política de autorização de chave de conteúdo usando REST - Azure | Microsoft Docs"
description: "Saiba como configurar uma política de autorização para uma chave de conteúdo usando a API REST dos Serviços de Mídia."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7af5f9e2-8ed8-43f2-843b-580ce8759fd4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: ed20fca35070c190bb63925d0a57cf919bcdd96c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="4c409-103">Criptografia dinâmica: configurar a política de autorização de chave de conteúdo</span><span class="sxs-lookup"><span data-stu-id="4c409-103">Dynamic encryption: Configure Content Key Authorization Policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="4c409-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4c409-104">Overview</span></span>
<span data-ttu-id="4c409-105">Os Serviços de Mídia do Microsoft Azure permitem distribuir o conteúdo criptografado (dinamicamente) com a criptografia AES (usando chaves de criptografia de 128 bits) e a criptografia DRM do PlayReady ou Widevine.</span><span class="sxs-lookup"><span data-stu-id="4c409-105">Microsoft Azure Media Services enables you to deliver your content encrypted (dynamically) with Advanced Encryption Standard (AES) (using 128-bit encryption keys) and PlayReady or Widevine DRM.</span></span> <span data-ttu-id="4c409-106">Os Serviços de Mídia também fornecem um serviço de entrega de chaves e licenças do PlayReady/Widevine a clientes autorizados.</span><span class="sxs-lookup"><span data-stu-id="4c409-106">Media Services also provides a service for delivering keys and PlayReady/Widevine licenses to authorized clients.</span></span>

<span data-ttu-id="4c409-107">Se desejar que os Serviços de Mídia criptografem um ativo, você precisará associar uma chave de criptografia (**CommonEncryption** ou **EnvelopeEncryption**) ao ativo (conforme descrito [aqui](media-services-rest-create-contentkey.md)) e também configurar políticas de autorização para a chave (conforme descrito neste artigo).</span><span class="sxs-lookup"><span data-stu-id="4c409-107">If you want for Media Services to encrypt an asset, you need to associate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with the asset (as described [here](media-services-rest-create-contentkey.md)) and also configure authorization policies for the key (as described in this article).</span></span>

<span data-ttu-id="4c409-108">Quando um fluxo é solicitado por um player, os serviços de mídia usam a chave especificada para criptografar dinamicamente o conteúdo usando a criptografia AES ou PlayReady.</span><span class="sxs-lookup"><span data-stu-id="4c409-108">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content using AES or PlayReady encryption.</span></span> <span data-ttu-id="4c409-109">Para descriptografar o fluxo, o player solicitará a chave do serviço de distribuição de chaves.</span><span class="sxs-lookup"><span data-stu-id="4c409-109">To decrypt the stream, the player will request the key from the key delivery service.</span></span> <span data-ttu-id="4c409-110">Para decidir se o usuário está autorizado para obter a chave ou não, o serviço avalia as políticas de autorização que você especificou para a chave.</span><span class="sxs-lookup"><span data-stu-id="4c409-110">To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="4c409-111">Os serviços de mídia oferecem suporte a várias maneiras de autenticar os usuários que fazem solicitações de chave.</span><span class="sxs-lookup"><span data-stu-id="4c409-111">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="4c409-112">A política de autorização de chave de conteúdo pode ter uma ou mais restrições de autorização: **aberta** ou **de token**.</span><span class="sxs-lookup"><span data-stu-id="4c409-112">The content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="4c409-113">A política restrita do token deve ser acompanhada por um token emitido por um Secure Token Service (STS).</span><span class="sxs-lookup"><span data-stu-id="4c409-113">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="4c409-114">Os serviços de mídia oferecem suporte a tokens no formato **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) e no formato **Token Web JSON **(JWT).</span><span class="sxs-lookup"><span data-stu-id="4c409-114">Media Services supports tokens in the **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token **(JWT) format.</span></span>

<span data-ttu-id="4c409-115">Os serviços de mídia não fornecem Secure Token Services.</span><span class="sxs-lookup"><span data-stu-id="4c409-115">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="4c409-116">Você pode criar um STS personalizado ou usar o Microsoft Azure ACS para emitir tokens.</span><span class="sxs-lookup"><span data-stu-id="4c409-116">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="4c409-117">O STS deve ser configurado para criar um token assinado com a chave especificada e declarações de emissão que você especificou na configuração de restrição do token (conforme descrito neste artigo).</span><span class="sxs-lookup"><span data-stu-id="4c409-117">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration (as described in this article).</span></span> <span data-ttu-id="4c409-118">O serviço de distribuição de chaves dos serviços de mídia retornará a chave de criptografia para o cliente se o token for válido e as declarações no token corresponderem aos configurados para a chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="4c409-118">The Media Services key delivery service will return the encryption key to the client if the token is valid and the claims in the token match those configured for the content key.</span></span>

<span data-ttu-id="4c409-119">Para obter mais informações, consulte</span><span class="sxs-lookup"><span data-stu-id="4c409-119">For more information, see</span></span>

[<span data-ttu-id="4c409-120">Autenticação do token JWT</span><span class="sxs-lookup"><span data-stu-id="4c409-120">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="4c409-121"><seg>
  [Integrar o aplicativo do MVC OWIN dos serviços de mídia do Azure com base no aplicativo com Active Directory do Azure e restringir o fornecimento da chave de conteúdo com base em declarações JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</seg></span><span class="sxs-lookup"><span data-stu-id="4c409-121">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="4c409-122">[Usar o ACS do Azure para emitir tokens](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="4c409-122">[Use Azure ACS to issue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="4c409-123">Algumas considerações se aplicam:</span><span class="sxs-lookup"><span data-stu-id="4c409-123">Some considerations apply:</span></span>
* <span data-ttu-id="4c409-124">Para poder usar o empacotamento dinâmico e a criptografia dinâmica, verifique se o ponto de extremidade de streaming do qual você deseja transmitir seu conteúdo está no estado **Executando**.</span><span class="sxs-lookup"><span data-stu-id="4c409-124">To be able to use dynamic packaging and dynamic encryption, make sure the streaming endpoint from which you want to stream  your content is in the **Running** state.</span></span>
* <span data-ttu-id="4c409-125">O ativo deve conter um conjunto de MP4s de taxa de bits adaptável ou arquivos de Smooth Streaming de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="4c409-125">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="4c409-126">Para obter mais informações, consulte [Codificar um ativo](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="4c409-126">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="4c409-127">Carregar e codificar seus ativos usando a opção **AssetCreationOptions.StorageEncrypted** .</span><span class="sxs-lookup"><span data-stu-id="4c409-127">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="4c409-128">Se você planeja ter várias chaves de conteúdo que exigem a mesma configuração de política, é altamente recomendável criar uma política de autorização única e reutilizá-la com várias chaves de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="4c409-128">If you plan to have multiple content keys that require the same policy configuration, it is strongly recommended to create a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="4c409-129">O serviço de entrega de chave armazena em cache ContentKeyAuthorizationPolicy e seus objetos relacionados (opções e restrições da política) por 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="4c409-129">The Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="4c409-130">Se você criar um ContentKeyAuthorizationPolicy e optar por usar uma restrição "Token", testá-lo e, em seguida, atualizar a política de restrição "Aberta", levará aproximadamente 15 minutos antes da política alternar para a versão "Aberta" da política.</span><span class="sxs-lookup"><span data-stu-id="4c409-130">If you create a ContentKeyAuthorizationPolicy and specify to use a “Token” restriction, then test it, and then update the policy to “Open” restriction, it will take roughly 15 minutes before the policy switches to the “Open” version of the policy.</span></span>
* <span data-ttu-id="4c409-131">Se você adicionar ou atualizar a política de fornecimento do ativo, você deve excluir um localizador existente (se houver) e criar um novo localizador.</span><span class="sxs-lookup"><span data-stu-id="4c409-131">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="4c409-132">No momento, não é possível criptografar downloads progressivos.</span><span class="sxs-lookup"><span data-stu-id="4c409-132">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="4c409-133">Criptografia dinâmica AES-128</span><span class="sxs-lookup"><span data-stu-id="4c409-133">AES-128 Dynamic Encryption</span></span>
> [!NOTE]
> <span data-ttu-id="4c409-134">Ao trabalhar com a API REST dos serviços de mídia, as seguintes considerações se aplicam:</span><span class="sxs-lookup"><span data-stu-id="4c409-134">When working with the Media Services REST API, the following considerations apply:</span></span>
> 
> <span data-ttu-id="4c409-135">Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="4c409-135">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="4c409-136">Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="4c409-136">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 
> <span data-ttu-id="4c409-137">Depois de se conectar com êxito em https://media.windows.net, você receberá um redirecionamento 301 especificando outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="4c409-137">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="4c409-138">Você deve fazer chamadas subsequentes para o novo URI.</span><span class="sxs-lookup"><span data-stu-id="4c409-138">You must make subsequent calls to the new URI.</span></span> <span data-ttu-id="4c409-139">Para saber mais sobre como conectar-se à API do AMS, veja [Acessar a API dos Serviços de Mídia do Azure com a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="4c409-139">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
> 
> 

### <a name="open-restriction"></a><span data-ttu-id="4c409-140">Restrição aberta</span><span class="sxs-lookup"><span data-stu-id="4c409-140">Open Restriction</span></span>
<span data-ttu-id="4c409-141">A restrição aberta significa que o sistema fornecerá a chave para qualquer pessoa que fizer uma solicitação de chave.</span><span class="sxs-lookup"><span data-stu-id="4c409-141">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="4c409-142">Essa restrição pode ser útil para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="4c409-142">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="4c409-143">O exemplo a seguir cria uma política de autorização aberta e o adiciona à chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="4c409-143">The following example creates an open authorization policy and adds it to the content key.</span></span>

#### <span data-ttu-id="4c409-144"><a id="ContentKeyAuthorizationPolicies"></a>Criar ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="4c409-144"><a id="ContentKeyAuthorizationPolicies"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="4c409-145">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="4c409-145">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423578086&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lZlyQ2%2bvH73qtJsb42%2fH3xF7r7EvQFR3UXyezuDENFU%3d
    x-ms-version: 2.11
    x-ms-client-request-id: d732dbfa-54fc-474c-99d6-9b46a006f389
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 36

    {"Name":"Open Authorization Policy"}

<span data-ttu-id="4c409-146">Resposta:</span><span class="sxs-lookup"><span data-stu-id="4c409-146">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 211
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3Adb4593da-f4d1-4cc5-a92a-d20eacbabee4')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d732dbfa-54fc-474c-99d6-9b46a006f389
    request-id: aabfa731-e884-4bf3-8314-492b04747ac4
    x-ms-request-id: aabfa731-e884-4bf3-8314-492b04747ac4
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 08:25:56 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicies/@Element","Id":"nb:ckpid:UUID:db4593da-f4d1-4cc5-a92a-d20eacbabee4","Name":"Open Authorization Policy"}

#### <span data-ttu-id="4c409-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>Criar ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="4c409-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="4c409-148">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="4c409-148">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580006&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Ref3EsonGF7fUKCwGwGgiMnZitzIzsDOvvMTeVrVVPg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: d225e357-e60e-4f42-add8-9d93aba1409a
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 168

    {"Name":"policy","KeyDeliveryType":2,"KeyDeliveryConfiguration":"","Restrictions":[{"Name":"HLS Open Authorization Policy","KeyRestrictionType":0,"Requirements":null}]}

<span data-ttu-id="4c409-149">Resposta:</span><span class="sxs-lookup"><span data-stu-id="4c409-149">Response:</span></span>    

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 349
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A57829b17-1101-4797-919b-f816f4a007b7')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d225e357-e60e-4f42-add8-9d93aba1409a
    request-id: 81bcad37-295b-431f-972f-b23f2e4172c9
    x-ms-request-id: 81bcad37-295b-431f-972f-b23f2e4172c9
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 08:56:40 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:57829b17-1101-4797-919b-f816f4a007b7","Name":"policy","KeyDeliveryType":2,"KeyDeliveryConfiguration":"","Restrictions":[{"Name":"HLS Open Authorization Policy","KeyRestrictionType":0,"Requirements":null}]}

#### <span data-ttu-id="4c409-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>Link ContentKeyAuthorizationPolicies com opções</span><span class="sxs-lookup"><span data-stu-id="4c409-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="4c409-151">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="4c409-151">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3A0baa438b-8ac2-4c40-a53c-4d4722b78715')/$links/Options HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580006&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Ref3EsonGF7fUKCwGwGgiMnZitzIzsDOvvMTeVrVVPg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 9847f705-f2ca-4e95-a478-8f823dbbaa29
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 154

    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A57829b17-1101-4797-919b-f816f4a007b7')"}

<span data-ttu-id="4c409-152">Resposta:</span><span class="sxs-lookup"><span data-stu-id="4c409-152">Response:</span></span>

    HTTP/1.1 204 No Content

#### <span data-ttu-id="4c409-153"><a id="AddAuthorizationPolicyToKey"></a>Adicionar política de autorização para a chave de conteúdo</span><span class="sxs-lookup"><span data-stu-id="4c409-153"><a id="AddAuthorizationPolicyToKey"></a>Add authorization policy to the content key</span></span>
<span data-ttu-id="4c409-154">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="4c409-154">Request:</span></span>

    PUT https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A2e6d36a7-a17c-4e9a-830d-eca23ad1a6f9') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: e613efff-cb6a-41b4-984a-f4f8fb6e76a4
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 78

    {"AuthorizationPolicyId":"nb:ckpid:UUID:c06cebb8-c4f0-4d1a-ba00-3273fb2bc3ad"}

<span data-ttu-id="4c409-155">Resposta:</span><span class="sxs-lookup"><span data-stu-id="4c409-155">Response:</span></span>

    HTTP/1.1 204 No Content

### <a name="token-restriction"></a><span data-ttu-id="4c409-156">Restrição de token</span><span class="sxs-lookup"><span data-stu-id="4c409-156">Token Restriction</span></span>
<span data-ttu-id="4c409-157">Esta seção descreve como criar uma política de autorização de chave de conteúdo e associá-la com a chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="4c409-157">This section describes how to create a content key authorization policy and associate it with the content key.</span></span> <span data-ttu-id="4c409-158">A política de autorização descreve quais requisitos de autorização devem ser atendidos para determinar se o usuário está autorizado a receber a chave (por exemplo, a lista de "chave de verificação" contém a chave que o token foi assinado).</span><span class="sxs-lookup"><span data-stu-id="4c409-158">The authorization policy describes what authorization requirements must be met to determine if the user is authorized to receive the key (for example, does the “verification key” list contain the key that the token was signed with).</span></span>

<span data-ttu-id="4c409-159">Para configurar a opção de restrição de token, você precisa usar um XML para descrever os requisitos da autorização do token.</span><span class="sxs-lookup"><span data-stu-id="4c409-159">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="4c409-160">O XML de configuração de restrição de token deve estar de acordo com o esquema XML a seguir.</span><span class="sxs-lookup"><span data-stu-id="4c409-160">The token restriction configuration XML must conform to the following XML schema.</span></span>

#### <span data-ttu-id="4c409-161"><a id="schema"></a>Esquema de restrição de token</span><span class="sxs-lookup"><span data-stu-id="4c409-161"><a id="schema"></a>Token restriction schema</span></span>
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:complexType name="TokenClaim">
        <xs:sequence>
          <xs:element name="ClaimType" nillable="true" type="xs:string" />
          <xs:element minOccurs="0" name="ClaimValue" nillable="true" type="xs:string" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenClaim" nillable="true" type="tns:TokenClaim" />
      <xs:complexType name="TokenRestrictionTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AlternateVerificationKeys" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
          <xs:element name="Audience" nillable="true" type="xs:anyURI" />
          <xs:element name="Issuer" nillable="true" type="xs:anyURI" />
          <xs:element name="PrimaryVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
          <xs:element minOccurs="0" name="RequiredClaims" nillable="true" type="tns:ArrayOfTokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenRestrictionTemplate" nillable="true" type="tns:TokenRestrictionTemplate" />
      <xs:complexType name="ArrayOfTokenVerificationKey">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenVerificationKey" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
      <xs:complexType name="TokenVerificationKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
      <xs:complexType name="ArrayOfTokenClaim">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenClaim" nillable="true" type="tns:TokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenClaim" nillable="true" type="tns:ArrayOfTokenClaim" />
      <xs:complexType name="SymmetricVerificationKey">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:TokenVerificationKey">
            <xs:sequence>
              <xs:element name="KeyValue" nillable="true" type="xs:base64Binary" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="SymmetricVerificationKey" nillable="true" type="tns:SymmetricVerificationKey" />
    </xs:schema>

<span data-ttu-id="4c409-162">Ao configurar a política restrita do **token**, você deve especificar os parâmetros da** chave de verificação** primária, **emissor** e **audiência**.</span><span class="sxs-lookup"><span data-stu-id="4c409-162">When configuring the **token** restricted policy, you must specify the primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="4c409-163">A **chave de verificação primária **contém a chave que o token foi assinado, o **emissor** é o serviço de token seguro que emite o token.</span><span class="sxs-lookup"><span data-stu-id="4c409-163">The **primary verification key **contains the key that the token was signed with, **issuer** is the secure token service that issues the token.</span></span> <span data-ttu-id="4c409-164">O **público** (às vezes chamada de **escopo**) descreve a intenção do token ou o recurso ao qual o token autoriza o acesso.</span><span class="sxs-lookup"><span data-stu-id="4c409-164">The **audience** (sometimes called **scope**) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="4c409-165">O serviço de distribuição de chaves dos serviços de mídia valida que esses valores no token correspondem aos valores no modelo.</span><span class="sxs-lookup"><span data-stu-id="4c409-165">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span> 

<span data-ttu-id="4c409-166">O exemplo a seguir cria uma política de autorização com uma restrição de token.</span><span class="sxs-lookup"><span data-stu-id="4c409-166">The following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="4c409-167">Neste exemplo, o cliente precisa apresentar um token que contém: chave de assinatura (VerificationKey), um emissor de token e declarações necessárias.</span><span class="sxs-lookup"><span data-stu-id="4c409-167">In this example, the client would have to present a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="4c409-168">Criar ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="4c409-168">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="4c409-169">Criar "Diretiva de restrição Token" como mostrado [aqui](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="4c409-169">Create the "Token Restriction Policy" as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="4c409-170">Criar ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="4c409-170">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="4c409-171">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="4c409-171">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580720&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=5LsNu%2b0D4eD3UOP3BviTLDkUjaErdUx0ekJ8402xidQ%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 2643d836-bfe7-438e-9ba2-bc6ff28e4a53
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 1079

    {"Name":"Token option for HLS","KeyDeliveryType":2,"KeyDeliveryConfiguration":null,"Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>BklyAFiPTQsuJNKriQJBZHYaKM2CkCTDQX2bw9sMYuvEC9sjW0W7GUIBygQL/+POEeUqCYPnmEU2g0o1GW2Oqg==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>E5BUHiN4vBdzUzdP0IWaHFMMU3D1uRZgF16TOhSfwwHGSw+Kbf0XqsHzEIYk11M372viB9vbiacsdcQksA0ftw==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

<span data-ttu-id="4c409-172">Resposta:</span><span class="sxs-lookup"><span data-stu-id="4c409-172">Response:</span></span>    

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1260
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3Ae1ef6145-46e8-4ee6-9756-b1cf96328c23')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 2643d836-bfe7-438e-9ba2-bc6ff28e4a53
    request-id: 2310b716-aeaa-421e-913e-3ce2f6f685ca
    x-ms-request-id: 2310b716-aeaa-421e-913e-3ce2f6f685ca
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:10:37 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:e1ef6145-46e8-4ee6-9756-b1cf96328c23","Name":"Token option for HLS","KeyDeliveryType":2,"KeyDeliveryConfiguration":null,"Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>BklyAFiPTQsuJNKriQJBZHYaKM2CkCTDQX2bw9sMYuvEC9sjW0W7GUIBygQL/+POEeUqCYPnmEU2g0o1GW2Oqg==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>E5BUHiN4vBdzUzdP0IWaHFMMU3D1uRZgF16TOhSfwwHGSw+Kbf0XqsHzEIYk11M372viB9vbiacsdcQksA0ftw==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="4c409-173">Link ContentKeyAuthorizationPolicies com opções</span><span class="sxs-lookup"><span data-stu-id="4c409-173">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="4c409-174">Link ContentKeyAuthorizationPolicies com opções como mostrado [aqui](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="4c409-174">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-to-the-content-key"></a><span data-ttu-id="4c409-175">Adicionar política de autorização para a chave de conteúdo</span><span class="sxs-lookup"><span data-stu-id="4c409-175">Add authorization policy to the content key</span></span>
<span data-ttu-id="4c409-176">Adicionar AuthorizationPolicy para o ContentKey, como mostrado [aqui](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="4c409-176">Add AuthorizationPolicy to the ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <a name="playready-dynamic-encryption"></a><span data-ttu-id="4c409-177">Criptografia dinâmica do PlayReady</span><span class="sxs-lookup"><span data-stu-id="4c409-177">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="4c409-178">Os serviços de mídia permitem que você configure os direitos e restrições que você deseja para que o tempo de execução do PlayReady DRM imponha quando um usuário está tentando reproduzir conteúdo protegido.</span><span class="sxs-lookup"><span data-stu-id="4c409-178">Media Services enables you to configure the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user is trying to play back protected content.</span></span> 

<span data-ttu-id="4c409-179">Ao proteger o conteúdo com PlayReady, uma das coisas que você precisa especificar na sua política de autorização é uma cadeia de caracteres XML que define o [modelo de licença do PlayReady](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4c409-179">When protecting your content with PlayReady, one of the things you need to specify in your authorization policy is an XML string that defines the [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> 

### <a name="open-restriction"></a><span data-ttu-id="4c409-180">Restrição aberta</span><span class="sxs-lookup"><span data-stu-id="4c409-180">Open Restriction</span></span>
<span data-ttu-id="4c409-181">A restrição aberta significa que o sistema fornecerá a chave para qualquer pessoa que fizer uma solicitação de chave.</span><span class="sxs-lookup"><span data-stu-id="4c409-181">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="4c409-182">Essa restrição pode ser útil para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="4c409-182">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="4c409-183">O exemplo a seguir cria uma política de autorização aberta e o adiciona à chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="4c409-183">The following example creates an open authorization policy and adds it to the content key.</span></span>

#### <span data-ttu-id="4c409-184"><a id="ContentKeyAuthorizationPolicies2"></a>Criar ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="4c409-184"><a id="ContentKeyAuthorizationPolicies2"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="4c409-185">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="4c409-185">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 9e7fa407-f84e-43aa-8f05-9790b46e279b
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 58

    {"Name":"Deliver Common Content Key"}

<span data-ttu-id="4c409-186">Resposta:</span><span class="sxs-lookup"><span data-stu-id="4c409-186">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 233
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3Acc3c64a8-e2fc-4e09-bf60-ac954251a387')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 9e7fa407-f84e-43aa-8f05-9790b46e279b
    request-id: b3d33c1b-a9cb-4120-ac0c-18f64846c147
    x-ms-request-id: b3d33c1b-a9cb-4120-ac0c-18f64846c147
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:26:00 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicies/@Element","Id":"nb:ckpid:UUID:cc3c64a8-e2fc-4e09-bf60-ac954251a387","Name":"Deliver Common Content Key"}


#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="4c409-187">Criar ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="4c409-187">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="4c409-188">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="4c409-188">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: f160ad25-b457-4bc6-8197-315604c5e585
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 593

    {"Name":"","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Open","KeyRestrictionType":0,"Requirements":null}]}

<span data-ttu-id="4c409-189">Resposta:</span><span class="sxs-lookup"><span data-stu-id="4c409-189">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 774
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A1052308c-4df7-4fdb-8d21-4d2141fc2be0')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: f160ad25-b457-4bc6-8197-315604c5e585
    request-id: 563f5a42-50a4-4c4a-add8-a833f8364231
    x-ms-request-id: 563f5a42-50a4-4c4a-add8-a833f8364231
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:23:24 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:1052308c-4df7-4fdb-8d21-4d2141fc2be0","Name":"","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Open","KeyRestrictionType":0,"Requirements":null}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="4c409-190">Link ContentKeyAuthorizationPolicies com opções</span><span class="sxs-lookup"><span data-stu-id="4c409-190">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="4c409-191">Link ContentKeyAuthorizationPolicies com opções como mostrado [aqui](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="4c409-191">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-to-the-content-key"></a><span data-ttu-id="4c409-192">Adicionar política de autorização para a chave de conteúdo</span><span class="sxs-lookup"><span data-stu-id="4c409-192">Add authorization policy to the content key</span></span>
<span data-ttu-id="4c409-193">Adicionar AuthorizationPolicy para o ContentKey, como mostrado [aqui](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="4c409-193">Add AuthorizationPolicy to the ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

### <a name="token-restriction"></a><span data-ttu-id="4c409-194">Restrição de token</span><span class="sxs-lookup"><span data-stu-id="4c409-194">Token Restriction</span></span>
<span data-ttu-id="4c409-195">Para configurar a opção de restrição de token, você precisa usar um XML para descrever os requisitos da autorização do token.</span><span class="sxs-lookup"><span data-stu-id="4c409-195">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="4c409-196">A configuração XML de restrição de token deve estar em conformidade com o esquema XML mostrado [nesta](#schema) seção.</span><span class="sxs-lookup"><span data-stu-id="4c409-196">The token restriction configuration XML must conform to the XML schema shown in [this](#schema) section.</span></span>

#### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="4c409-197">Criar ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="4c409-197">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="4c409-198">Criar ContentKeyAuthorizationPolicies como mostrado [aqui](#ContentKeyAuthorizationPolicies2).</span><span class="sxs-lookup"><span data-stu-id="4c409-198">Create ContentKeyAuthorizationPolicies as shown [here](#ContentKeyAuthorizationPolicies2).</span></span>

#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="4c409-199">Criar ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="4c409-199">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="4c409-200">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="4c409-200">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423583561&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=5eZnkOsSv%2fLLEKmS%2bWObBlsNYyee8BQlp%2bUYbjugcJg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: ab079b0e-2ba9-4cf1-b549-a97bfa6cd2d3
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 1525

    {"Name":"Token option","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>w52OyHVqXT8aaupGxuJ3NGt8M6opHDOtx132p4r6q4hLI6ffnLusgEGie1kedUewVoIe1tqDkVE6xsIV7O91KA==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>dYwLKIEMBljLeY9VM7vWdlhps31Fbt0XXhqP5VyjQa33bJXleBtkzQ6dF5AtwI9gDcdM2dV2TvYNhCilBKjMCg==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

<span data-ttu-id="4c409-201">Resposta:</span><span class="sxs-lookup"><span data-stu-id="4c409-201">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1706
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3Ae42bbeae-de42-4077-90e9-a844f297ef70')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: ab079b0e-2ba9-4cf1-b549-a97bfa6cd2d3
    request-id: ccf8a4ba-731e-4124-8192-079592c251cc
    x-ms-request-id: ccf8a4ba-731e-4124-8192-079592c251cc
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:58:47 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:e42bbeae-de42-4077-90e9-a844f297ef70","Name":"Token option","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>w52OyHVqXT8aaupGxuJ3NGt8M6opHDOtx132p4r6q4hLI6ffnLusgEGie1kedUewVoIe1tqDkVE6xsIV7O91KA==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>dYwLKIEMBljLeY9VM7vWdlhps31Fbt0XXhqP5VyjQa33bJXleBtkzQ6dF5AtwI9gDcdM2dV2TvYNhCilBKjMCg==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="4c409-202">Link ContentKeyAuthorizationPolicies com opções</span><span class="sxs-lookup"><span data-stu-id="4c409-202">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="4c409-203">Link ContentKeyAuthorizationPolicies com opções como mostrado [aqui](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="4c409-203">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-to-the-content-key"></a><span data-ttu-id="4c409-204">Adicionar política de autorização para a chave de conteúdo</span><span class="sxs-lookup"><span data-stu-id="4c409-204">Add authorization policy to the content key</span></span>
<span data-ttu-id="4c409-205">Adicionar AuthorizationPolicy para o ContentKey, como mostrado [aqui](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="4c409-205">Add AuthorizationPolicy to the ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <span data-ttu-id="4c409-206"><a id="types"></a>Tipos usados ao definir ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="4c409-206"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="4c409-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="4c409-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="4c409-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="4c409-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
        None = 0,
        PlayReadyLicense = 1,
        BaselineHttp = 2,
        Widevine = 3
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="4c409-209">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="4c409-209">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4c409-210">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="4c409-210">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="4c409-211">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4c409-211">Next Steps</span></span>
<span data-ttu-id="4c409-212">Agora que você configurou a política de autorização da chave de conteúdo, vá para o tópico [Como configurar a política de entrega de ativos](media-services-rest-configure-asset-delivery-policy.md) .</span><span class="sxs-lookup"><span data-stu-id="4c409-212">Now that you have configured content key's authorization policy, go to the [How to configure asset delivery policy](media-services-rest-configure-asset-delivery-policy.md) topic.</span></span>

