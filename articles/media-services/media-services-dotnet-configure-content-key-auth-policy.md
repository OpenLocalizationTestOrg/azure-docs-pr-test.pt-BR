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
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a>Criptografia dinâmica: configurar a política de autorização de chave de conteúdo
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a>Visão geral
Serviços de mídia do Microsoft Azure permite que você toodeliver MPEG-DASH, Smooth Streaming e fluxos de HTTP-Live-Streaming (HLS) protegidos com Advanced Encryption Standard (AES) (usando chaves de criptografia de 128 bits) ou [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). AMS também permite que você toodeliver DASH streams criptografados com Widevine DRM. PlayReady e Widevine são criptografados por Olá especificação de criptografia comum (ISO/IEC 23001-7 CENC).

Serviços de mídia também fornecem um **serviço de entrega de chave ou a licença** dos quais os clientes podem obter chaves AES ou tooplay de licenças do PlayReady/Widevine Olá conteúdo criptografado.

Se você quiser para serviços de mídia tooencrypt um ativo, você precisa tooassociate uma chave de criptografia (**CommonEncryption** ou **EnvelopeEncryption**) com o ativo de saudação (conforme descrito [aqui](media-services-dotnet-create-contentkey.md)) e também configurar políticas de autorização para a chave de saudação (conforme descrito neste artigo).

Quando um fluxo é solicitado por um player, o Media Services usa Olá especificado toodynamically chave criptografar seu conteúdo usando a criptografia AES ou DRM. fluxo de saudação toodecrypt, player Olá solicitar chave Olá do serviço de distribuição de chaves de saudação. toodecide ou não usuário Olá é autorizado chave de saudação tooget, serviço Olá avalia as políticas de autorização de saudação que você especificou para a chave de saudação.

Os serviços de mídia oferecem suporte a várias maneiras de autenticar os usuários que fazem solicitações de chave. Olá política de autorização da chave de conteúdo pode ter uma ou mais restrições de autorização: **abrir** ou **token** restrição. política de restrição de token de saudação deve ser acompanhada por um token emitido por um Token STS (serviço seguro). Serviços de mídia oferece suporte a tokens no hello **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) formato e **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) formato.

Os serviços de mídia não fornecem Secure Token Services. Você pode criar um STS personalizado ou utilizar a tokens de tooissue ACS do Microsoft Azure. Olá STS deve ser configurado toocreate um token assinado com a chave especificada hello e problema declarações que você especificou na configuração de restrição de token da saudação (conforme descrito neste artigo). Olá serviço de distribuição de chaves de serviços de mídia retornará cliente de toohello chave de criptografia de saudação se Olá token é válido e hello declarações no token Olá correspondam às configuradas para chave de conteúdo de saudação.

Para obter mais informações, consulte

[Autenticação do token JWT](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<seg>
  [Integrar o aplicativo do MVC OWIN dos serviços de mídia do Azure com base no aplicativo com Active Directory do Azure e restringir o fornecimento da chave de conteúdo com base em declarações JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</seg>

[Usar tokens do Azure ACS tooissue](http://mingfeiy.com/acs-with-key-services).

### <a name="some-considerations-apply"></a>Algumas considerações se aplicam:
* Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado. toostart seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, o ponto de extremidade de streaming de streaming tem toobe em Olá **executando** estado. 
* O ativo deve conter um conjunto de MP4s de taxa de bits adaptável ou arquivos de Smooth Streaming de taxa de bits adaptável. Para obter mais informações, consulte [Codificar um ativo](media-services-encode-asset.md).
* Carregar e codificar seus ativos usando a opção **AssetCreationOptions.StorageEncrypted** .
* Se você planejar toohave várias chaves de conteúdo que exigem Olá mesma configuração de política, é altamente recomendável toocreate uma única política de autorização e reutilizá-la com várias chaves de conteúdo.
* Olá serviço de entrega de chave armazena ContentKeyAuthorizationPolicy e seus objetos relacionados (restrições e opções de política) por 15 minutos.  Se você criar um ContentKeyAuthorizationPolicy e especifica toouse uma restrição por "Token", em seguida, testá-lo e, em seguida, atualizar a política de saudação muito "abrir" restrição, levará aproximadamente 15 minutos antes de saudação política comutadores toohello versão "Aberta da política de saudação".
* Se você adicionar ou atualizar a política de fornecimento do ativo, você deve excluir um localizador existente (se houver) e criar um novo localizador.
* No momento, não é possível criptografar downloads progressivos.

## <a name="aes-128-dynamic-encryption"></a>Criptografia dinâmica AES-128
### <a name="open-restriction"></a>Restrição aberta
Restrição aberta significa sistema Olá fornecerá Olá tooanyone chave que faz uma solicitação de chave. Essa restrição pode ser útil para fins de teste.

saudação de exemplo a seguir cria uma política de autorização aberta e o adiciona toohello chave de conteúdo.

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


### <a name="token-restriction"></a>Restrição de token
Esta seção descreve como toocreate um conteúdo de diretiva de autorização de chave e associá-lo a chave de conteúdo de saudação. política de autorização Olá descreve quais requisitos de autorização devem ser atendido toodetermine se usuário Olá tooreceive autorizados Olá chave (por exemplo, lista de "chave de verificação" hello contêm chave Olá que Olá token foi assinado com).

opção de restrição de token de saudação tooconfigure, você precisa toouse XML requisitos de autorização do token de saudação toodescribe. XML de configuração de restrição de token Olá deve estar de acordo com toohello esquema XML a seguir.

#### <a id="schema"></a>Esquema de restrição de token
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

Ao configurar Olá **token** restrito a política, você deve especificar Olá primário * * verificação chave * *, **emissor** e **público** parâmetros. Olá * * chave de verificação primária * * contém chave Olá Olá token foi assinado, **emissor** é o serviço de token seguro Olá esse token de saudação de problemas. Olá **público** (às vezes chamado de **escopo**) descreve a intenção de saudação do token de saudação ou recurso de saudação token Olá autoriza o acesso ao. Olá serviço de distribuição de chaves de serviços de mídia valida que esses valores no token Olá correspondem a valores de saudação no modelo de saudação. 

Ao usar **SDK de serviços de mídia para .NET**, você pode usar o hello **TokenRestrictionTemplate** token de restrição classe toogenerate hello.
saudação de exemplo a seguir cria uma política de autorização com uma restrição de token. Neste exemplo, Olá cliente terá toopresent um token que contém: assinatura de chave (VerificationKey), um emissor de token e as declarações necessárias.

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

#### <a id="test"></a>Token de teste
tooget um token de teste com base na restrição de token de saudação que foi usada para a política de autorização da chave hello, Olá a seguir.

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


## <a name="playready-dynamic-encryption"></a>Criptografia dinâmica do PlayReady
Serviços de mídia permite que você tooconfigure direitos de saudação e restrições que você deseja para Olá tooenforce de tempo de execução do PlayReady DRM quando um usuário está tentando tooplay novamente o conteúdo protegido. 

Ao proteger o conteúdo com PlayReady, uma das coisas Olá precisar toospecify em sua política de autorização é uma cadeia de caracteres XML que define Olá [modelo de licença do PlayReady](media-services-playready-license-template-overview.md). No SDK do Media Services para .NET, Olá **PlayReadyLicenseResponseTemplate** e **PlayReadyLicenseTemplate** classes ajudará você a definir Olá modelo de licença do PlayReady.

[Este tópico](media-services-protect-with-drm.md) mostra como tooencrypt seu conteúdo com **PlayReady** e **Widevine**.

### <a name="open-restriction"></a>Restrição aberta
Restrição aberta significa sistema Olá fornecerá Olá tooanyone chave que faz uma solicitação de chave. Essa restrição pode ser útil para fins de teste.

saudação de exemplo a seguir cria uma política de autorização aberta e o adiciona toohello chave de conteúdo.

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

### <a name="token-restriction"></a>Restrição de token
opção de restrição de token de saudação tooconfigure, você precisa toouse XML requisitos de autorização do token de saudação toodescribe. XML de configuração de restrição de token Olá deve estar de acordo com toohello esquema XML mostrada no [isso](#schema) seção.

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


um token de teste com base na restrição de token de saudação que foi usada para Olá consulte de política de autorização da chave de tooget [isso](#test) seção. 

## <a id="types"></a>Tipos usados ao definir ContentKeyAuthorizationPolicy
### <a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <a id="TokenType"></a>TokenType
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Próxima etapa
Agora que você configurou a diretiva de autorização da chave de conteúdo, vá toohello [como política de entrega de ativos tooconfigure](media-services-dotnet-configure-asset-delivery-policy.md) tópico.

