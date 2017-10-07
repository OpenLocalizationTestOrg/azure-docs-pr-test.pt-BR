---
title: "licenças DRM aaaUse Azure Media Services toodeliver ou chaves AES"
description: "Este artigo descreve como você pode usar licenças de PlayReady e/ou Widevine toodeliver serviços de mídia do Azure (AMS) e chaves AES, mas Olá rest (codificação, criptografando, streaming) usando os servidores no local."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 8546c2c1-430b-4254-a88d-4436a83f9192
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: a81da2973c79e5182ae58aeca7a0f14f3fc7c9ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-services-toodeliver-drm-licenses-or-aes-keys"></a>Usar licenças dos serviços de mídia do Azure toodeliver DRM ou chaves AES
Serviços de mídia do Azure (AMS) permite que você tooingest, codificar, adicionar proteção de conteúdo e transmitir o conteúdo (consulte [isso](media-services-protect-with-drm.md) artigo para obter detalhes). No entanto, há os clientes que apenas deseja licenças de toodeliver AMS toouse e/ou chaves e fazem a codificação, criptografia e streaming usando seus servidores locais. Este artigo descreve como você pode usar AMS toodeliver PlayReady e/ou licenças Widevine mas Olá rest com os servidores no local. 

## <a name="overview"></a>Visão geral
Os Serviços de Mídia fornecem um serviço para entregar licenças DRM do PlayReady e do Widevine e chaves AES-128. Serviços de mídia oferecem APIs que permitem que você configure direitos hello e restrições que você deseja para tooenforce de tempo de execução do DRM hello quando um usuário é reproduzido Olá DRM o conteúdo protegido. Quando o conteúdo protegido de uma saudação de solicitações do usuário, aplicativo de player hello solicita uma licença do serviço de licença Olá AMS. serviço de licença Olá AMS emitirá player do hello licença toohello (se ele está autorizado). licenças do PlayReady e Widevine Olá contém a chave de descriptografia de saudação que pode ser usado por Olá cliente player toodecrypt fluxo Olá conteúdo e.

Os Serviços de Mídia dão suporte a várias maneiras de autorizar os usuários que fazem solicitações de chave ou de licença. Configurar política de autorização da chave de saudação conteúdo e política de saudação pode ter uma ou mais restrições: abrir ou restrição de token. política de restrição de token de saudação deve ser acompanhada por um token emitido por um Token STS (serviço seguro). Serviços de mídia oferece suporte a tokens no formato do Simple Web Tokens (SWT) hello e JSON Web Token (JWT).

Hello diagrama a seguir mostra as principais etapas de saudação necessário tootake toouse AMS toodeliver PlayReady e/ou licenças Widevine mas Olá rest com os servidores no local.

![Proteger com o PlayReady](./media/media-services-deliver-keys-and-licenses/media-services-diagram1.png)

## <a name="download-sample"></a>Baixar exemplo
Você pode baixar o exemplo hello descrito neste artigo do [aqui](https://github.com/Azure/media-services-dotnet-deliver-drm-licenses).

## <a name="create-and-configure-a-visual-studio-project"></a>Criar e configurar um projeto do Visual Studio

1. Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md). 
2. Adicionar Olá elementos a seguir muito**appSettings** definido no seu arquivo App. config:

    <add key="Issuer" value="http://testacs.com"/> <add key="Audience" value="urn:test"/>

## <a name="net-code-example"></a>Exemplo de código do .NET

saudação de exemplo de código a seguir mostra como toocreate um comum chave de conteúdo e obter URLs de aquisição de licença PlayReady ou Widevine. Você precisa tooget Olá seguintes informações de AMS e configure o servidor local: **chave de conteúdo**, **id da chave**, **URL de aquisição de licença**. Após configurar seu servidor local, você poderá transmitir a partir de seu próprio servidor de transmissão. Desde que o servidor de licença do hello fluxo criptografado tooAMS pontos, o player solicitará uma licença do AMS. Se você escolher autenticação de token, o servidor de licença Olá AMS validará token Olá enviados por meio de HTTPS e (se válida) fornecerá player do hello licença tooyour back. (o exemplo de código Olá apenas mostra como toocreate um comum chave de conteúdo e obter URLs de aquisição de licença PlayReady ou Widevine. Se você quiser chaves toodelivery AES-128, você precisa toocreate uma chave de conteúdo do envelope e obter uma URL de aquisição de chave e [isso](media-services-protect-with-aes128.md) artigo mostra como toodo-lo).

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DeliverDRMLicenses
    {
        class Program
        {
            // Read values from hello App.config file.
            private static readonly string _AADTenantDomain =
                ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
                ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            private static readonly Uri _sampleIssuer =
                new Uri(ConfigurationManager.AppSettings["Issuer"]);
            private static readonly Uri _sampleAudience =
                new Uri(ConfigurationManager.AppSettings["Audience"]);

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                bool tokenRestriction = true;
                string tokenTemplateString = null;


                IContentKey key = CreateCommonTypeContentKey();

                // Print out hello key ID and Key in base64 string format
                Console.WriteLine("Created key {0} with key value {1} ",
                    key.Id, System.Convert.ToBase64String(key.GetClearKeyValue()));

                Console.WriteLine("PlayReady License Key delivery URL: {0}",
                    key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));

                Console.WriteLine("Widevine License Key delivery URL: {0}",
                    key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine));

                if (tokenRestriction)
                    tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
                else
                    AddOpenAuthorizationPolicy(key);

                Console.WriteLine("Added authorization policy: {0}",
                    key.AuthorizationPolicyId);
                Console.WriteLine();
                Console.ReadLine();
            }

            static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
            {

                // Create ContentKeyAuthorizationPolicy with Open restrictions 
                // and create authorization policy          

                List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                    new List<ContentKeyAuthorizationPolicyRestriction>
                {
                        new ContentKeyAuthorizationPolicyRestriction
                        {
                            Name = "Open",
                            KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                            Requirements = null
                        }
                };

                // Configure PlayReady and Widevine license templates.
                string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

                IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, PlayReadyLicenseTemplate);

                IContentKeyAuthorizationPolicyOption WidevinePolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.Widevine,
                        restrictions, WidevineLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with no restrictions").
                            Result;


                contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
                contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);
                // Associate hello content key authorization policy with hello content key.
                contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
                contentKey = contentKey.UpdateAsync().Result;
            }

            public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
            {
                string tokenTemplateString = GenerateTokenRequirements();

                List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                    new List<ContentKeyAuthorizationPolicyRestriction>
                {
                        new ContentKeyAuthorizationPolicyRestriction
                        {
                            Name = "Token Authorization Policy",
                            KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                            Requirements = tokenTemplateString,
                        }
                };

                // Configure PlayReady and Widevine license templates.
                string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

                IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, PlayReadyLicenseTemplate);

                IContentKeyAuthorizationPolicyOption WidevinePolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                        ContentKeyDeliveryType.Widevine,
                            restrictions, WidevineLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with token restrictions").
                            Result;

                contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
                contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);

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

                //hello PlayReadyLicenseResponseTemplate class represents hello template 
                //for hello response sent back toohello end user. 
                //It contains a field for a custom data string between hello license server 
                //and hello application (may be useful for custom app logic) 
                //as well as a list of one or more license templates.

                PlayReadyLicenseResponseTemplate responseTemplate =
                    new PlayReadyLicenseResponseTemplate();

                // hello PlayReadyLicenseTemplate class represents a license template 
                // for creating PlayReady licenses
                // toobe returned toohello end users. 
                // It contains hello data on hello content key in hello license 
                // and any rights or restrictions toobe 
                // enforced by hello PlayReady DRM runtime when using hello content key.
                PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();

                // Configure whether hello license is persistent 
                // (saved in persistent storage on hello client) 
                // or non-persistent (only held in memory while hello player is using hello license).  
                licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

                // AllowTestDevices controls whether test devices can use hello license or not.  
                // If true, hello MinimumSecurityLevel property of hello license
                // is set too150.  If false (hello default), 
                // hello MinimumSecurityLevel property of hello license is set too2000.
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

                // IMPORTANT: These types of restrictions can be very powerful 
                // but can also affect hello consumer experience. 
                // If hello output protections are configured too restrictive, 
                // hello content might be unplayable on some clients. 
                // For more information, see hello PlayReady Compliance Rules document.

                // For example:
                //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

                responseTemplate.LicenseTemplates.Add(licenseTemplate);

                return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
            }


            private static string ConfigureWidevineLicenseTemplate()
            {
                var template = new WidevineMessage
                {
                    allowed_track_types = AllowedTrackTypes.SD_HD,
                    content_key_specs = new[]
                    {
                            new ContentKeySpecs
                            {
                                required_output_protection =
                                    new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                                security_level = 1,
                                track_type = "SD"
                            }
                        },
                    policy_overrides = new
                    {
                        can_play = true,
                        can_persist = true,
                        can_renew = false
                    }
                };

                string configuration = JsonConvert.SerializeObject(template);
                return configuration;
            }


            static public IContentKey CreateCommonTypeContentKey()
            {
                // Create envelope encryption content key
                Guid keyId = Guid.NewGuid();
                byte[] contentKey = GetRandomBuffer(16);

                IContentKey key = _context.ContentKeys.Create(
                                        keyId,
                                        contentKey,
                                        "ContentKey",
                                        ContentKeyType.CommonEncryption);

                return key;
            }

            static private byte[] GetRandomBuffer(int length)
            {
                var returnValue = new byte[length];

                using (var rng =
                    new System.Security.Cryptography.RNGCryptoServiceProvider())
                {
                    rng.GetBytes(returnValue);
                }

                return returnValue;
            }
        }
    }

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Consulte também
[Usando a PlayReady e/ou a Criptografia Comum Dinâmica Widevine](media-services-protect-with-drm.md)

[Usando o serviço de entrega de chave e criptografia dinâmica do AES-128](media-services-protect-with-aes128.md)

[Usando parceiros toodeliver Widevine licenças tooAzure serviços de mídia](media-services-licenses-partner-integration.md)

