---
title: "política de autorização da chave de conteúdo aaaConfigure usando o SDK do Media Services .NET | Microsoft Docs"
description: "Saiba como tooconfigure uma política de autorização para uma chave de conteúdo usando o SDK do .NET de serviços de mídia."
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
ms.openlocfilehash: cfcbc5da9819bcec8b163fef183988a8beff9ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="fff10-103">Criptografia dinâmica: configurar a política de autorização de chave de conteúdo</span><span class="sxs-lookup"><span data-stu-id="fff10-103">Dynamic encryption: configure content key authorization policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="fff10-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="fff10-104">Overview</span></span>
<span data-ttu-id="fff10-105">Serviços de mídia do Microsoft Azure permite que você toodeliver MPEG-DASH, Smooth Streaming e fluxos de HTTP-Live-Streaming (HLS) protegidos com Advanced Encryption Standard (AES) (usando chaves de criptografia de 128 bits) ou [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="fff10-105">Microsoft Azure Media Services enables you toodeliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="fff10-106">AMS também permite que você toodeliver DASH streams criptografados com Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="fff10-106">AMS also enables you toodeliver DASH streams encrypted with Widevine DRM.</span></span> <span data-ttu-id="fff10-107">PlayReady e Widevine são criptografados por Olá especificação de criptografia comum (ISO/IEC 23001-7 CENC).</span><span class="sxs-lookup"><span data-stu-id="fff10-107">Both PlayReady and Widevine are encrypted per hello Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span>

<span data-ttu-id="fff10-108">Serviços de mídia também fornecem um **serviço de entrega de chave ou a licença** dos quais os clientes podem obter chaves AES ou tooplay de licenças do PlayReady/Widevine Olá conteúdo criptografado.</span><span class="sxs-lookup"><span data-stu-id="fff10-108">Media Services also provides a **Key/License Delivery Service** from which clients can obtain AES keys or PlayReady/Widevine licenses tooplay hello encrypted content.</span></span>

<span data-ttu-id="fff10-109">Se você quiser para serviços de mídia tooencrypt um ativo, você precisa tooassociate uma chave de criptografia (**CommonEncryption** ou **EnvelopeEncryption**) com o ativo de saudação (conforme descrito [aqui](media-services-dotnet-create-contentkey.md)) e também configurar políticas de autorização para a chave de saudação (conforme descrito neste artigo).</span><span class="sxs-lookup"><span data-stu-id="fff10-109">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with hello asset (as described [here](media-services-dotnet-create-contentkey.md)) and also configure authorization policies for hello key (as described in this article).</span></span>

<span data-ttu-id="fff10-110">Quando um fluxo é solicitado por um player, o Media Services usa Olá especificado toodynamically chave criptografar seu conteúdo usando a criptografia AES ou DRM.</span><span class="sxs-lookup"><span data-stu-id="fff10-110">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES or DRM encryption.</span></span> <span data-ttu-id="fff10-111">fluxo de saudação toodecrypt, player Olá solicitar chave Olá do serviço de distribuição de chaves de saudação.</span><span class="sxs-lookup"><span data-stu-id="fff10-111">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="fff10-112">toodecide ou não usuário Olá é autorizado chave de saudação tooget, serviço Olá avalia as políticas de autorização de saudação que você especificou para a chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="fff10-112">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="fff10-113">Os serviços de mídia oferecem suporte a várias maneiras de autenticar os usuários que fazem solicitações de chave.</span><span class="sxs-lookup"><span data-stu-id="fff10-113">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="fff10-114">Olá política de autorização da chave de conteúdo pode ter uma ou mais restrições de autorização: **abrir** ou **token** restrição.</span><span class="sxs-lookup"><span data-stu-id="fff10-114">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="fff10-115">política de restrição de token de saudação deve ser acompanhada por um token emitido por um Token STS (serviço seguro).</span><span class="sxs-lookup"><span data-stu-id="fff10-115">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="fff10-116">Serviços de mídia oferece suporte a tokens no hello **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) formato e **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) formato.</span><span class="sxs-lookup"><span data-stu-id="fff10-116">Media Services supports tokens in hello **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.</span></span>

<span data-ttu-id="fff10-117">Os serviços de mídia não fornecem Secure Token Services.</span><span class="sxs-lookup"><span data-stu-id="fff10-117">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="fff10-118">Você pode criar um STS personalizado ou utilizar a tokens de tooissue ACS do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fff10-118">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="fff10-119">Olá STS deve ser configurado toocreate um token assinado com a chave especificada hello e problema declarações que você especificou na configuração de restrição de token da saudação (conforme descrito neste artigo).</span><span class="sxs-lookup"><span data-stu-id="fff10-119">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration (as described in this article).</span></span> <span data-ttu-id="fff10-120">Olá serviço de distribuição de chaves de serviços de mídia retornará cliente de toohello chave de criptografia de saudação se Olá token é válido e hello declarações no token Olá correspondam às configuradas para chave de conteúdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="fff10-120">hello Media Services key delivery service will return hello encryption key toohello client if hello token is valid and hello claims in hello token match those configured for hello content key.</span></span>

<span data-ttu-id="fff10-121">Para obter mais informações, consulte</span><span class="sxs-lookup"><span data-stu-id="fff10-121">For more information, see</span></span>

[<span data-ttu-id="fff10-122">Autenticação do token JWT</span><span class="sxs-lookup"><span data-stu-id="fff10-122">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="fff10-123"><seg>
  [Integrar o aplicativo do MVC OWIN dos serviços de mídia do Azure com base no aplicativo com Active Directory do Azure e restringir o fornecimento da chave de conteúdo com base em declarações JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</seg></span><span class="sxs-lookup"><span data-stu-id="fff10-123">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="fff10-124">[Usar tokens do Azure ACS tooissue](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="fff10-124">[Use Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="fff10-125">Algumas considerações se aplicam:</span><span class="sxs-lookup"><span data-stu-id="fff10-125">Some considerations apply:</span></span>
* <span data-ttu-id="fff10-126">Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado.</span><span class="sxs-lookup"><span data-stu-id="fff10-126">When your AMS account is created a **default** streaming endpoint is added  tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="fff10-127">toostart seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, o ponto de extremidade de streaming de streaming tem toobe em Olá **executando** estado.</span><span class="sxs-lookup"><span data-stu-id="fff10-127">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, your streaming endpoint has toobe in hello **Running** state.</span></span> 
* <span data-ttu-id="fff10-128">O ativo deve conter um conjunto de MP4s de taxa de bits adaptável ou arquivos de Smooth Streaming de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="fff10-128">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="fff10-129">Para obter mais informações, consulte [Codificar um ativo](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="fff10-129">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="fff10-130">Carregar e codificar seus ativos usando a opção **AssetCreationOptions.StorageEncrypted** .</span><span class="sxs-lookup"><span data-stu-id="fff10-130">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="fff10-131">Se você planejar toohave várias chaves de conteúdo que exigem Olá mesma configuração de política, é altamente recomendável toocreate uma única política de autorização e reutilizá-la com várias chaves de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="fff10-131">If you plan toohave multiple content keys that require hello same policy configuration, it is strongly recommended toocreate a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="fff10-132">Olá serviço de entrega de chave armazena ContentKeyAuthorizationPolicy e seus objetos relacionados (restrições e opções de política) por 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="fff10-132">hello Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="fff10-133">Se você criar um ContentKeyAuthorizationPolicy e especifica toouse uma restrição por "Token", em seguida, testá-lo e, em seguida, atualizar a política de saudação muito "abrir" restrição, levará aproximadamente 15 minutos antes de saudação política comutadores toohello versão "Aberta da política de saudação".</span><span class="sxs-lookup"><span data-stu-id="fff10-133">If you create a ContentKeyAuthorizationPolicy and specify toouse a “Token” restriction, then test it, and then update hello policy too“Open” restriction, it will take roughly 15 minutes before hello policy switches toohello “Open” version of hello policy.</span></span>
* <span data-ttu-id="fff10-134">Se você adicionar ou atualizar a política de fornecimento do ativo, você deve excluir um localizador existente (se houver) e criar um novo localizador.</span><span class="sxs-lookup"><span data-stu-id="fff10-134">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="fff10-135">No momento, não é possível criptografar downloads progressivos.</span><span class="sxs-lookup"><span data-stu-id="fff10-135">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="fff10-136">Criptografia dinâmica AES-128</span><span class="sxs-lookup"><span data-stu-id="fff10-136">AES-128 Dynamic Encryption</span></span>
### <a name="open-restriction"></a><span data-ttu-id="fff10-137">Restrição aberta</span><span class="sxs-lookup"><span data-stu-id="fff10-137">Open Restriction</span></span>
<span data-ttu-id="fff10-138">Restrição aberta significa sistema Olá fornecerá Olá tooanyone chave que faz uma solicitação de chave.</span><span class="sxs-lookup"><span data-stu-id="fff10-138">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="fff10-139">Essa restrição pode ser útil para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="fff10-139">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="fff10-140">saudação de exemplo a seguir cria uma política de autorização aberta e o adiciona toohello chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="fff10-140">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

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

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);
    }


### <a name="token-restriction"></a><span data-ttu-id="fff10-141">Restrição de token</span><span class="sxs-lookup"><span data-stu-id="fff10-141">Token Restriction</span></span>
<span data-ttu-id="fff10-142">Esta seção descreve como toocreate um conteúdo de diretiva de autorização de chave e associá-lo a chave de conteúdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="fff10-142">This section describes how toocreate a content key authorization policy and associate it with hello content key.</span></span> <span data-ttu-id="fff10-143">política de autorização Olá descreve quais requisitos de autorização devem ser atendido toodetermine se usuário Olá tooreceive autorizados Olá chave (por exemplo, lista de "chave de verificação" hello contêm chave Olá que Olá token foi assinado com).</span><span class="sxs-lookup"><span data-stu-id="fff10-143">hello authorization policy describes what authorization requirements must be met toodetermine if hello user is authorized tooreceive hello key (for example, does hello “verification key” list contain hello key that hello token was signed with).</span></span>

<span data-ttu-id="fff10-144">opção de restrição de token de saudação tooconfigure, você precisa toouse XML requisitos de autorização do token de saudação toodescribe.</span><span class="sxs-lookup"><span data-stu-id="fff10-144">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="fff10-145">XML de configuração de restrição de token Olá deve estar de acordo com toohello esquema XML a seguir.</span><span class="sxs-lookup"><span data-stu-id="fff10-145">hello token restriction configuration XML must conform toohello following XML schema.</span></span>

#### <span data-ttu-id="fff10-146"><a id="schema"></a>Esquema de restrição de token</span><span class="sxs-lookup"><span data-stu-id="fff10-146"><a id="schema"></a>Token restriction schema</span></span>
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

<span data-ttu-id="fff10-147">Ao configurar Olá **token** restrito a política, você deve especificar Olá primário * * verificação chave * *, **emissor** e **público** parâmetros.</span><span class="sxs-lookup"><span data-stu-id="fff10-147">When configuring hello **token** restricted policy, you must specify hello primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="fff10-148">Olá * * chave de verificação primária * * contém chave Olá Olá token foi assinado, **emissor** é o serviço de token seguro Olá esse token de saudação de problemas.</span><span class="sxs-lookup"><span data-stu-id="fff10-148">hello **primary verification key **contains hello key that hello token was signed with, **issuer** is hello secure token service that issues hello token.</span></span> <span data-ttu-id="fff10-149">Olá **público** (às vezes chamado de **escopo**) descreve a intenção de saudação do token de saudação ou recurso de saudação token Olá autoriza o acesso ao.</span><span class="sxs-lookup"><span data-stu-id="fff10-149">hello **audience** (sometimes called **scope**) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="fff10-150">Olá serviço de distribuição de chaves de serviços de mídia valida que esses valores no token Olá correspondem a valores de saudação no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="fff10-150">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span> 

<span data-ttu-id="fff10-151">Ao usar **SDK de serviços de mídia para .NET**, você pode usar o hello **TokenRestrictionTemplate** token de restrição classe toogenerate hello.</span><span class="sxs-lookup"><span data-stu-id="fff10-151">When using **Media Services SDK for .NET**, you can use hello **TokenRestrictionTemplate** class toogenerate hello restriction token.</span></span>
<span data-ttu-id="fff10-152">saudação de exemplo a seguir cria uma política de autorização com uma restrição de token.</span><span class="sxs-lookup"><span data-stu-id="fff10-152">hello following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="fff10-153">Neste exemplo, Olá cliente terá toopresent um token que contém: assinatura de chave (VerificationKey), um emissor de token e as declarações necessárias.</span><span class="sxs-lookup"><span data-stu-id="fff10-153">In this example, hello client would have toopresent a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

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

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);

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

#### <span data-ttu-id="fff10-154"><a id="test"></a>Token de teste</span><span class="sxs-lookup"><span data-stu-id="fff10-154"><a id="test"></a>Test token</span></span>
<span data-ttu-id="fff10-155">tooget um token de teste com base na restrição de token de saudação que foi usada para a política de autorização da chave hello, Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="fff10-155">tooget a test token based on hello token restriction that was used for hello key authorization policy, do hello following.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
    // Note, you need toopass hello key id Guid because we specified 
    // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
    Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
    Console.WriteLine();


## <a name="playready-dynamic-encryption"></a><span data-ttu-id="fff10-156">Criptografia dinâmica do PlayReady</span><span class="sxs-lookup"><span data-stu-id="fff10-156">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="fff10-157">Serviços de mídia permite que você tooconfigure direitos de saudação e restrições que você deseja para Olá tooenforce de tempo de execução do PlayReady DRM quando um usuário está tentando tooplay novamente o conteúdo protegido.</span><span class="sxs-lookup"><span data-stu-id="fff10-157">Media Services enables you tooconfigure hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplay back protected content.</span></span> 

<span data-ttu-id="fff10-158">Ao proteger o conteúdo com PlayReady, uma das coisas Olá precisar toospecify em sua política de autorização é uma cadeia de caracteres XML que define Olá [modelo de licença do PlayReady](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fff10-158">When protecting your content with PlayReady, one of hello things you need toospecify in your authorization policy is an XML string that defines hello [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> <span data-ttu-id="fff10-159">No SDK do Media Services para .NET, Olá **PlayReadyLicenseResponseTemplate** e **PlayReadyLicenseTemplate** classes ajudará você a definir Olá modelo de licença do PlayReady.</span><span class="sxs-lookup"><span data-stu-id="fff10-159">In Media Services SDK for .NET, hello **PlayReadyLicenseResponseTemplate** and **PlayReadyLicenseTemplate** classes will help you define hello PlayReady License Template.</span></span>

<span data-ttu-id="fff10-160">[Este tópico](media-services-protect-with-drm.md) mostra como tooencrypt seu conteúdo com **PlayReady** e **Widevine**.</span><span class="sxs-lookup"><span data-stu-id="fff10-160">[This topic](media-services-protect-with-drm.md) shows how tooencrypt your content with **PlayReady** and **Widevine**.</span></span>

### <a name="open-restriction"></a><span data-ttu-id="fff10-161">Restrição aberta</span><span class="sxs-lookup"><span data-stu-id="fff10-161">Open Restriction</span></span>
<span data-ttu-id="fff10-162">Restrição aberta significa sistema Olá fornecerá Olá tooanyone chave que faz uma solicitação de chave.</span><span class="sxs-lookup"><span data-stu-id="fff10-162">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="fff10-163">Essa restrição pode ser útil para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="fff10-163">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="fff10-164">saudação de exemplo a seguir cria uma política de autorização aberta e o adiciona toohello chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="fff10-164">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

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

        // Associate hello content key authorization policy with hello content key.
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;
    }

### <a name="token-restriction"></a><span data-ttu-id="fff10-165">Restrição de token</span><span class="sxs-lookup"><span data-stu-id="fff10-165">Token Restriction</span></span>
<span data-ttu-id="fff10-166">opção de restrição de token de saudação tooconfigure, você precisa toouse XML requisitos de autorização do token de saudação toodescribe.</span><span class="sxs-lookup"><span data-stu-id="fff10-166">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="fff10-167">XML de configuração de restrição de token Olá deve estar de acordo com toohello esquema XML mostrada no [isso](#schema) seção.</span><span class="sxs-lookup"><span data-stu-id="fff10-167">hello token restriction configuration XML must conform toohello XML schema shown in [this](#schema) section.</span></span>

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

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate hello content key authorization policy with hello content key
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
        // hello following code configures PlayReady License Template using .NET classes
        // and returns hello XML string.

        //hello PlayReadyLicenseResponseTemplate class represents hello template for hello response sent back toohello end user. 
        //It contains a field for a custom data string between hello license server and hello application 
        //(may be useful for custom app logic) as well as a list of one or more license templates.
        PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

        // hello PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
        // toobe returned toohello end users. 
        //It contains hello data on hello content key in hello license and any rights or restrictions toobe 
        //enforced by hello PlayReady DRM runtime when using hello content key.
        PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
        //Configure whether hello license is persistent (saved in persistent storage on hello client) 
        //or non-persistent (only held in memory while hello player is using hello license).  
        licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

        // AllowTestDevices controls whether test devices can use hello license or not.  
        // If true, hello MinimumSecurityLevel property of hello license
        // is set too150.  If false (hello default), hello MinimumSecurityLevel property of hello license is set too2000.
        licenseTemplate.AllowTestDevices = true;


        // You can also configure hello Play Right in hello PlayReady license by using hello PlayReadyPlayRight class. 
        // It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions 
        // configured in hello license and on hello PlayRight itself (for playback specific policy). 
        // Much of hello policy on hello PlayRight has toodo with output restrictions 
        // which control hello types of outputs that hello content can be played over and 
        // any restrictions that must be put in place when using a given output.
        // For example, if hello DigitalVideoOnlyContentRestriction is enabled, 
        //then hello DRM runtime will only allow hello video toobe displayed over digital outputs 
        //(analog video outputs won’t be allowed toopass hello content).

        //IMPORTANT: These types of restrictions can be very powerful but can also affect hello consumer experience. 
        // If hello output protections are configured too restrictive, 
        // hello content might be unplayable on some clients. For more information, see hello PlayReady Compliance Rules document.

        // For example:
        //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

        responseTemplate.LicenseTemplates.Add(licenseTemplate);

        return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
    }


<span data-ttu-id="fff10-168">um token de teste com base na restrição de token de saudação que foi usada para Olá consulte de política de autorização da chave de tooget [isso](#test) seção.</span><span class="sxs-lookup"><span data-stu-id="fff10-168">tooget a test token based on hello token restriction that was used for hello key authorization policy see [this](#test) section.</span></span> 

## <span data-ttu-id="fff10-169"><a id="types"></a>Tipos usados ao definir ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="fff10-169"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="fff10-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="fff10-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="fff10-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="fff10-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <span data-ttu-id="fff10-172"><a id="TokenType"></a>TokenType</span><span class="sxs-lookup"><span data-stu-id="fff10-172"><a id="TokenType"></a>TokenType</span></span>
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="fff10-173">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="fff10-173">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fff10-174">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="fff10-174">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="fff10-175">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="fff10-175">Next step</span></span>
<span data-ttu-id="fff10-176">Agora que você configurou a diretiva de autorização da chave de conteúdo, vá toohello [como política de entrega de ativos tooconfigure](media-services-dotnet-configure-asset-delivery-policy.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="fff10-176">Now that you have configured content key's authorization policy, go toohello [How tooconfigure asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md) topic.</span></span>

