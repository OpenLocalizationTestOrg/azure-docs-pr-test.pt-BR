---
title: "Configurar política de autorização de chave de conteúdo usando o SDK do .NET dos Serviços de Mídia | Microsoft Docs"
description: "Saiba como configurar uma política de autorização para uma chave de conteúdo usando o SDK do .NET dos Serviços de Mídia do Azure."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 1a0aedda-5b87-4436-8193-09fc2f14310c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: 75dd9107dca215a0b31db3d44bada69210fe9ac6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="8656f-103">Criptografia dinâmica: configurar a política de autorização de chave de conteúdo</span><span class="sxs-lookup"><span data-stu-id="8656f-103">Dynamic encryption: configure content key authorization policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="8656f-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="8656f-104">Overview</span></span>
<span data-ttu-id="8656f-105">Os Serviços de Mídia do Microsoft Azure permitem distribuir fluxos MPEG-DASH, Smooth Streaming e HLS (HTTP-Live-Streaming) protegidos com a criptografia AES (usando chaves de criptografia de 128 bits) ou com o [DRM do Microsoft PlayReady](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="8656f-105">Microsoft Azure Media Services enables you to deliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="8656f-106">O AMS também permite distribuir fluxos DASH criptografados com o DRM do Widevine.</span><span class="sxs-lookup"><span data-stu-id="8656f-106">AMS also enables you to deliver DASH streams encrypted with Widevine DRM.</span></span> <span data-ttu-id="8656f-107">PlayReady e Widevine são criptografados de acordo com a especificação de criptografia comum (ISO/IEC 23001-7 CENC).</span><span class="sxs-lookup"><span data-stu-id="8656f-107">Both PlayReady and Widevine are encrypted per the Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span>

<span data-ttu-id="8656f-108">Os Serviços de Mídia também fornecem um **Serviço de Entrega de Chaves/Licenças** por meio do qual os clientes podem obter chaves AES ou licenças do PlayReady/Widevine para reproduzir o conteúdo criptografado.</span><span class="sxs-lookup"><span data-stu-id="8656f-108">Media Services also provides a **Key/License Delivery Service** from which clients can obtain AES keys or PlayReady/Widevine licenses to play the encrypted content.</span></span>

<span data-ttu-id="8656f-109">Se desejar que os Serviços de Mídia criptografem um ativo, você precisará associar uma chave de criptografia (**CommonEncryption** ou **EnvelopeEncryption**) ao ativo (conforme descrito [aqui](media-services-dotnet-create-contentkey.md)) e também configurar políticas de autorização para a chave (conforme descrito neste artigo).</span><span class="sxs-lookup"><span data-stu-id="8656f-109">If you want for Media Services to encrypt an asset, you need to associate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with the asset (as described [here](media-services-dotnet-create-contentkey.md)) and also configure authorization policies for the key (as described in this article).</span></span>

<span data-ttu-id="8656f-110">Quando um fluxo é solicitado por um player, os Serviços de Mídia usam a chave especificada para criptografar dinamicamente o conteúdo usando a criptografia AES ou DRM.</span><span class="sxs-lookup"><span data-stu-id="8656f-110">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content using AES or DRM encryption.</span></span> <span data-ttu-id="8656f-111">Para descriptografar o fluxo, o player solicitará a chave do serviço de distribuição de chaves.</span><span class="sxs-lookup"><span data-stu-id="8656f-111">To decrypt the stream, the player will request the key from the key delivery service.</span></span> <span data-ttu-id="8656f-112">Para decidir se o usuário está autorizado para obter a chave ou não, o serviço avalia as políticas de autorização que você especificou para a chave.</span><span class="sxs-lookup"><span data-stu-id="8656f-112">To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="8656f-113">Os serviços de mídia oferecem suporte a várias maneiras de autenticar os usuários que fazem solicitações de chave.</span><span class="sxs-lookup"><span data-stu-id="8656f-113">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="8656f-114">A política de autorização de chave de conteúdo pode ter uma ou mais restrições de autorização: **aberta** ou **de token**.</span><span class="sxs-lookup"><span data-stu-id="8656f-114">The content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="8656f-115">A política restrita do token deve ser acompanhada por um token emitido por um Secure Token Service (STS).</span><span class="sxs-lookup"><span data-stu-id="8656f-115">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="8656f-116">Os Serviços de Mídia oferecem suporte a tokens no formato **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) e no formato **Token Web JSON** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)).</span><span class="sxs-lookup"><span data-stu-id="8656f-116">Media Services supports tokens in the **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.</span></span>

<span data-ttu-id="8656f-117">Os serviços de mídia não fornecem Secure Token Services.</span><span class="sxs-lookup"><span data-stu-id="8656f-117">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="8656f-118">Você pode criar um STS personalizado ou usar o Microsoft Azure ACS para emitir tokens.</span><span class="sxs-lookup"><span data-stu-id="8656f-118">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="8656f-119">O STS deve ser configurado para criar um token assinado com a chave especificada e declarações de emissão que você especificou na configuração de restrição do token (conforme descrito neste artigo).</span><span class="sxs-lookup"><span data-stu-id="8656f-119">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration (as described in this article).</span></span> <span data-ttu-id="8656f-120">O serviço de distribuição de chaves dos serviços de mídia retornará a chave de criptografia para o cliente se o token for válido e as declarações no token corresponderem aos configurados para a chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="8656f-120">The Media Services key delivery service will return the encryption key to the client if the token is valid and the claims in the token match those configured for the content key.</span></span>

<span data-ttu-id="8656f-121">Para obter mais informações, consulte</span><span class="sxs-lookup"><span data-stu-id="8656f-121">For more information, see</span></span>

[<span data-ttu-id="8656f-122">Autenticação do token JWT</span><span class="sxs-lookup"><span data-stu-id="8656f-122">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="8656f-123"><seg>
  [Integrar o aplicativo do MVC OWIN dos serviços de mídia do Azure com base no aplicativo com Active Directory do Azure e restringir o fornecimento da chave de conteúdo com base em declarações JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</seg></span><span class="sxs-lookup"><span data-stu-id="8656f-123">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="8656f-124">[Usar o ACS do Azure para emitir tokens](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="8656f-124">[Use Azure ACS to issue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="8656f-125">Algumas considerações se aplicam:</span><span class="sxs-lookup"><span data-stu-id="8656f-125">Some considerations apply:</span></span>
* <span data-ttu-id="8656f-126">Quando sua conta AMS é criada, um ponto de extremidade de streaming **padrão** é adicionado à sua conta em estado **Parado**.</span><span class="sxs-lookup"><span data-stu-id="8656f-126">When your AMS account is created a **default** streaming endpoint is added  to your account in the **Stopped** state.</span></span> <span data-ttu-id="8656f-127">Para começar a transmitir seu conteúdo e aproveitar o empacotamento dinâmico e a criptografia dinâmica, o ponto de extremidade de streaming deve estar no estado **Executando**.</span><span class="sxs-lookup"><span data-stu-id="8656f-127">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, your streaming endpoint has to be in the **Running** state.</span></span> 
* <span data-ttu-id="8656f-128">O ativo deve conter um conjunto de MP4s de taxa de bits adaptável ou arquivos de Smooth Streaming de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="8656f-128">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="8656f-129">Para obter mais informações, consulte [Codificar um ativo](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="8656f-129">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="8656f-130">Carregar e codificar seus ativos usando a opção **AssetCreationOptions.StorageEncrypted** .</span><span class="sxs-lookup"><span data-stu-id="8656f-130">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="8656f-131">Se você planeja ter várias chaves de conteúdo que exigem a mesma configuração de política, é altamente recomendável criar uma política de autorização única e reutilizá-la com várias chaves de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="8656f-131">If you plan to have multiple content keys that require the same policy configuration, it is strongly recommended to create a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="8656f-132">O serviço de entrega de chave armazena em cache ContentKeyAuthorizationPolicy e seus objetos relacionados (opções e restrições da política) por 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="8656f-132">The Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="8656f-133">Se você criar um ContentKeyAuthorizationPolicy e optar por usar uma restrição "Token", testá-lo e, em seguida, atualizar a política de restrição "Aberta", levará aproximadamente 15 minutos antes da política alternar para a versão "Aberta" da política.</span><span class="sxs-lookup"><span data-stu-id="8656f-133">If you create a ContentKeyAuthorizationPolicy and specify to use a “Token” restriction, then test it, and then update the policy to “Open” restriction, it will take roughly 15 minutes before the policy switches to the “Open” version of the policy.</span></span>
* <span data-ttu-id="8656f-134">Se você adicionar ou atualizar a política de fornecimento do ativo, você deve excluir um localizador existente (se houver) e criar um novo localizador.</span><span class="sxs-lookup"><span data-stu-id="8656f-134">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="8656f-135">No momento, não é possível criptografar downloads progressivos.</span><span class="sxs-lookup"><span data-stu-id="8656f-135">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="8656f-136">Criptografia dinâmica AES-128</span><span class="sxs-lookup"><span data-stu-id="8656f-136">AES-128 Dynamic Encryption</span></span>
### <a name="open-restriction"></a><span data-ttu-id="8656f-137">Restrição aberta</span><span class="sxs-lookup"><span data-stu-id="8656f-137">Open Restriction</span></span>
<span data-ttu-id="8656f-138">A restrição aberta significa que o sistema fornecerá a chave para qualquer pessoa que fizer uma solicitação de chave.</span><span class="sxs-lookup"><span data-stu-id="8656f-138">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="8656f-139">Essa restrição pode ser útil para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="8656f-139">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="8656f-140">O exemplo a seguir cria uma política de autorização aberta e o adiciona à chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="8656f-140">The following example creates an open authorization policy and adds it to the content key.</span></span>

    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {
        // Create ContentKeyAuthorizationPolicy with Open restrictions
        // and create authorization policy
        IContentKeyAuthorizationPolicy policy = _context.
        ContentKeyAuthorizationPolicies.
        CreateAsync("Open Authorization Policy").Result;
        
        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "HLS Open Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                Requirements = null // no requirements needed for HLS
            };

        restrictions.Add(restriction);

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy", 
            ContentKeyDeliveryType.BaselineHttp, 
            restrictions, 
            "");

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);
    }


### <a name="token-restriction"></a><span data-ttu-id="8656f-141">Restrição de token</span><span class="sxs-lookup"><span data-stu-id="8656f-141">Token Restriction</span></span>
<span data-ttu-id="8656f-142">Esta seção descreve como criar uma política de autorização de chave de conteúdo e associá-la com a chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="8656f-142">This section describes how to create a content key authorization policy and associate it with the content key.</span></span> <span data-ttu-id="8656f-143">A política de autorização descreve quais requisitos de autorização devem ser atendidos para determinar se o usuário está autorizado a receber a chave (por exemplo, a lista de "chave de verificação" contém a chave que o token foi assinado).</span><span class="sxs-lookup"><span data-stu-id="8656f-143">The authorization policy describes what authorization requirements must be met to determine if the user is authorized to receive the key (for example, does the “verification key” list contain the key that the token was signed with).</span></span>

<span data-ttu-id="8656f-144">Para configurar a opção de restrição de token, você precisa usar um XML para descrever os requisitos da autorização do token.</span><span class="sxs-lookup"><span data-stu-id="8656f-144">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="8656f-145">O XML de configuração de restrição de token deve estar de acordo com o esquema XML a seguir.</span><span class="sxs-lookup"><span data-stu-id="8656f-145">The token restriction configuration XML must conform to the following XML schema.</span></span>

#### <span data-ttu-id="8656f-146"><a id="schema"></a>Esquema de restrição de token</span><span class="sxs-lookup"><span data-stu-id="8656f-146"><a id="schema"></a>Token restriction schema</span></span>
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

<span data-ttu-id="8656f-147">Ao configurar a política restrita do **token**, você deve especificar os parâmetros da** chave de verificação** primária, **emissor** e **audiência**.</span><span class="sxs-lookup"><span data-stu-id="8656f-147">When configuring the **token** restricted policy, you must specify the primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="8656f-148">A **chave de verificação primária **contém a chave que o token foi assinado, o **emissor** é o serviço de token seguro que emite o token.</span><span class="sxs-lookup"><span data-stu-id="8656f-148">The **primary verification key **contains the key that the token was signed with, **issuer** is the secure token service that issues the token.</span></span> <span data-ttu-id="8656f-149">O **público** (às vezes chamada de **escopo**) descreve a intenção do token ou o recurso ao qual o token autoriza o acesso.</span><span class="sxs-lookup"><span data-stu-id="8656f-149">The **audience** (sometimes called **scope**) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="8656f-150">O serviço de distribuição de chaves dos serviços de mídia valida que esses valores no token correspondem aos valores no modelo.</span><span class="sxs-lookup"><span data-stu-id="8656f-150">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span> 

<span data-ttu-id="8656f-151">Ao usar o **SDK dos Serviços de Mídia para .NET**, você pode usar a classe **TokenRestrictionTemplate** para gerar o token de restrição.</span><span class="sxs-lookup"><span data-stu-id="8656f-151">When using **Media Services SDK for .NET**, you can use the **TokenRestrictionTemplate** class to generate the restriction token.</span></span>
<span data-ttu-id="8656f-152">O exemplo a seguir cria uma política de autorização com uma restrição de token.</span><span class="sxs-lookup"><span data-stu-id="8656f-152">The following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="8656f-153">Neste exemplo, o cliente precisa apresentar um token que contém: chave de assinatura (VerificationKey), um emissor de token e declarações necessárias.</span><span class="sxs-lookup"><span data-stu-id="8656f-153">In this example, the client would have to present a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString
                };

        restrictions.Add(restriction);

        //You could have multiple options 
        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
                "Token option for HLS",
                ContentKeyDeliveryType.BaselineHttp,
                restrictions,
                null  // no key delivery data is needed for HLS
                );

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);

        return tokenTemplateString;
    }

    static private string GenerateTokenRequirements()
    {
        TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

        template.PrimaryVerificationKey = new SymmetricVerificationKey();
        template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();

        template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

        return TokenRestrictionTemplateSerializer.Serialize(template);
    }

#### <span data-ttu-id="8656f-154"><a id="test"></a>Token de teste</span><span class="sxs-lookup"><span data-stu-id="8656f-154"><a id="test"></a>Test token</span></span>
<span data-ttu-id="8656f-155">Para obter um token de teste com base na restrição de token que foi usada para a política de autorização da chave, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="8656f-155">To get a test token based on the token restriction that was used for the key authorization policy, do the following.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on the the data in the given TokenRestrictionTemplate.
    // Note, you need to pass the key id Guid because we specified 
    // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
    Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

    //The GenerateTestToken method returns the token without the word “Bearer” in front
    //so you have to add it in front of the token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
    Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
    Console.WriteLine();


## <a name="playready-dynamic-encryption"></a><span data-ttu-id="8656f-156">Criptografia dinâmica do PlayReady</span><span class="sxs-lookup"><span data-stu-id="8656f-156">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="8656f-157">Os serviços de mídia permitem que você configure os direitos e restrições que você deseja para que o tempo de execução do PlayReady DRM imponha quando um usuário está tentando reproduzir conteúdo protegido.</span><span class="sxs-lookup"><span data-stu-id="8656f-157">Media Services enables you to configure the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user is trying to play back protected content.</span></span> 

<span data-ttu-id="8656f-158">Ao proteger o conteúdo com PlayReady, uma das coisas que você precisa especificar na sua política de autorização é uma cadeia de caracteres XML que define o [modelo de licença do PlayReady](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8656f-158">When protecting your content with PlayReady, one of the things you need to specify in your authorization policy is an XML string that defines the [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> <span data-ttu-id="8656f-159">No SDK dos serviços de mídia para .NET, as classes **PlayReadyLicenseResponseTemplate** e **PlayReadyLicenseTemplate** o ajudarão a definir o modelo de licença do PlayReady.</span><span class="sxs-lookup"><span data-stu-id="8656f-159">In Media Services SDK for .NET, the **PlayReadyLicenseResponseTemplate** and **PlayReadyLicenseTemplate** classes will help you define the PlayReady License Template.</span></span>

<span data-ttu-id="8656f-160">[Este tópico](media-services-protect-with-drm.md) mostra como criptografar o conteúdo com o **PlayReady** e o **Widevine**.</span><span class="sxs-lookup"><span data-stu-id="8656f-160">[This topic](media-services-protect-with-drm.md) shows how to encrypt your content with **PlayReady** and **Widevine**.</span></span>

### <a name="open-restriction"></a><span data-ttu-id="8656f-161">Restrição aberta</span><span class="sxs-lookup"><span data-stu-id="8656f-161">Open Restriction</span></span>
<span data-ttu-id="8656f-162">A restrição aberta significa que o sistema fornecerá a chave para qualquer pessoa que fizer uma solicitação de chave.</span><span class="sxs-lookup"><span data-stu-id="8656f-162">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="8656f-163">Essa restrição pode ser útil para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="8656f-163">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="8656f-164">O exemplo a seguir cria uma política de autorização aberta e o adiciona à chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="8656f-164">The following example creates an open authorization policy and adds it to the content key.</span></span>

    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {

        // Create ContentKeyAuthorizationPolicy with Open restrictions 
        // and create authorization policy          

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Open", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open, 
                Requirements = null
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;


        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate the content key authorization policy with the content key.
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;
    }

### <a name="token-restriction"></a><span data-ttu-id="8656f-165">Restrição de token</span><span class="sxs-lookup"><span data-stu-id="8656f-165">Token Restriction</span></span>
<span data-ttu-id="8656f-166">Para configurar a opção de restrição de token, você precisa usar um XML para descrever os requisitos da autorização do token.</span><span class="sxs-lookup"><span data-stu-id="8656f-166">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="8656f-167">A configuração XML de restrição de token deve estar em conformidade com o esquema XML mostrado [nesta](#schema) seção.</span><span class="sxs-lookup"><span data-stu-id="8656f-167">The token restriction configuration XML must conform to the XML schema shown in [this](#schema) section.</span></span>

    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Token Authorization Policy", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString, 
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate the content key authorization policy with the content key
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;

        return tokenTemplateString;
    }

    static private string GenerateTokenRequirements()
    {

        TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

        template.PrimaryVerificationKey = new SymmetricVerificationKey();
        template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();


        template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

        return TokenRestrictionTemplateSerializer.Serialize(template);
    } 

    static private string ConfigurePlayReadyLicenseTemplate()
    {
        // The following code configures PlayReady License Template using .NET classes
        // and returns the XML string.

        //The PlayReadyLicenseResponseTemplate class represents the template for the response sent back to the end user. 
        //It contains a field for a custom data string between the license server and the application 
        //(may be useful for custom app logic) as well as a list of one or more license templates.
        PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

        // The PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
        // to be returned to the end users. 
        //It contains the data on the content key in the license and any rights or restrictions to be 
        //enforced by the PlayReady DRM runtime when using the content key.
        PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
        //Configure whether the license is persistent (saved in persistent storage on the client) 
        //or non-persistent (only held in memory while the player is using the license).  
        licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

        // AllowTestDevices controls whether test devices can use the license or not.  
        // If true, the MinimumSecurityLevel property of the license
        // is set to 150.  If false (the default), the MinimumSecurityLevel property of the license is set to 2000.
        licenseTemplate.AllowTestDevices = true;


        // You can also configure the Play Right in the PlayReady license by using the PlayReadyPlayRight class. 
        // It grants the user the ability to playback the content subject to the zero or more restrictions 
        // configured in the license and on the PlayRight itself (for playback specific policy). 
        // Much of the policy on the PlayRight has to do with output restrictions 
        // which control the types of outputs that the content can be played over and 
        // any restrictions that must be put in place when using a given output.
        // For example, if the DigitalVideoOnlyContentRestriction is enabled, 
        //then the DRM runtime will only allow the video to be displayed over digital outputs 
        //(analog video outputs won’t be allowed to pass the content).

        //IMPORTANT: These types of restrictions can be very powerful but can also affect the consumer experience. 
        // If the output protections are configured too restrictive, 
        // the content might be unplayable on some clients. For more information, see the PlayReady Compliance Rules document.

        // For example:
        //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

        responseTemplate.LicenseTemplates.Add(licenseTemplate);

        return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
    }


<span data-ttu-id="8656f-168">Para obter um token de teste com base na restrição de token que foi usada para a política de autorização da chave, consulte [esta](#test) seção.</span><span class="sxs-lookup"><span data-stu-id="8656f-168">To get a test token based on the token restriction that was used for the key authorization policy see [this](#test) section.</span></span> 

## <span data-ttu-id="8656f-169"><a id="types"></a>Tipos usados ao definir ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="8656f-169"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="8656f-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="8656f-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="8656f-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="8656f-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <span data-ttu-id="8656f-172"><a id="TokenType"></a>TokenType</span><span class="sxs-lookup"><span data-stu-id="8656f-172"><a id="TokenType"></a>TokenType</span></span>
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="8656f-173">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="8656f-173">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8656f-174">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="8656f-174">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="8656f-175">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="8656f-175">Next step</span></span>
<span data-ttu-id="8656f-176">Agora que você configurou a política de autorização da chave de conteúdo, vá para o tópico [Como configurar a política de entrega de ativos](media-services-dotnet-configure-asset-delivery-policy.md) .</span><span class="sxs-lookup"><span data-stu-id="8656f-176">Now that you have configured content key's authorization policy, go to the [How to configure asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md) topic.</span></span>

