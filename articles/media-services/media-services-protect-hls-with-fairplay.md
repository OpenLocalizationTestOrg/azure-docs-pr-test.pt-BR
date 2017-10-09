---
title: "aaaProtect de conteúdo HLS com o Microsoft PlayReady ou Apple FairPlay - Azure | Microsoft Docs"
description: "Este tópico fornece uma visão geral e mostra como toouse Azure Media Services toodynamically criptografar conteúdo HTTP Live Streaming (HLS) com FairPlay da Apple. Ele também mostra toouse Olá Media Services licenciar toodeliver do serviço de entrega tooclients de licenças FairPlay."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 91ca451e3e7bf0da1d74dac4c99180f08f39e4ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a>Proteger o conteúdo do HLS com o Apple FairPlay ou Microsoft PlayReady
Habilita de serviços de mídia do Azure toodynamically você criptografar seu conteúdo HTTP Live Streaming (HLS) usando Olá formatos a seguir:  

* **Chave de limpeza do envelope AES-128**

    Olá parte inteira é criptografado usando Olá **CBC AES-128** modo. descriptografia de saudação do fluxo de saudação é suportada pelo player OS X e iOS nativamente. Para saber mais, confira [Uso da criptografia dinâmica AES-128 e serviço de distribuição de chaves](media-services-protect-with-aes128.md).
* **Apple FairPlay**

    Olá individual vídeo e áudio exemplos são criptografados usando Olá **CBC AES-128** modo. **Streaming de FairPlay** (FPS) está integrado ao Olá sistemas operacionais de dispositivos com suporte nativo no iOS e Apple TV. Safari nos X permite FPS usando o suporte à interface de extensões de mídia criptografados (EME) hello.
* **Microsoft PlayReady**

Olá, imagem a seguir mostra Olá **HLS + FairPlay ou PlayReady criptografia dinâmica** fluxo de trabalho.

![Diagrama do fluxo de trabalho de criptografia dinâmica](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

Este tópico demonstra como toouse os serviços de mídia toodynamically criptografar o conteúdo HLS com FairPlay da Apple. Ele também mostra toouse Olá Media Services licenciar toodeliver do serviço de entrega tooclients de licenças FairPlay.

> [!NOTE]
> Se também desejar tooencrypt o HLS conteúdo com PlayReady, você precisa toocreate uma chave de conteúdo comum e associá-lo com seu ativo. Você também precisa política de autorização tooconfigure Olá da chave de conteúdo, conforme descrito em [criptografia comum dinâmica do PlayReady usando](media-services-protect-with-drm.md).
>
>

## <a name="requirements-and-considerations"></a>Requisitos e considerações

a seguir Olá é necessária ao usar os serviços de mídia toodeliver que HLS criptografado com FairPlay e toodeliver FairPlay licenças:

  * Uma conta do Azure. Para obter detalhes, confira [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
  * Uma conta dos Serviços de Mídia. toocreate um, consulte [criar uma conta de serviços de mídia do Azure usando o portal do Azure de saudação](media-services-portal-create-account.md).
  * Inscreva-se no [Programa de Desenvolvimento da Apple](https://developer.apple.com/).
  * Apple requer saudação do hello proprietário do conteúdo tooobtain [pacote de implantação](https://developer.apple.com/contact/fps/). Estado que você já implementou módulo de segurança de chave (KSM) com os serviços de mídia, e que você está solicitando o pacote FPS final hello. Há instruções Olá FPS final toogenerate certificação do pacote e obter Olá chave de segredo do aplicativo (SOLICITAR). Use o peça tooconfigure FairPlay.
  * SDK do .NET dos Serviços de Mídia do Azure na versão **3.6.0** ou posterior.

Olá coisas a seguir deve ser definido no lado de distribuição de chaves dos serviços de mídia:

  * **Certificado do aplicativo (AC)**: Este é um arquivo. pfx que contém a chave privada hello. Você cria esse arquivo e o criptografa com uma senha.

       Quando você configurar uma política de distribuição de chaves, você deve fornecer esse arquivo. pfx hello e a senha no formato Base64.

      Olá, as etapas a seguir descreve como toogenerate um certificado. pfx do arquivo para FairPlay:

    1. Instale o OpenSSL de https://slproweb.com/products/Win32OpenSSL.html.

        Vá toohello pasta onde estão os certificados de FairPlay hello e outros arquivos fornecidos pela Apple.
    2. Execute Olá comando a seguir na linha de comando hello. Isso converte hello. cer tooa. PEM arquivo.

        "C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem
    3. Execute Olá comando a seguir na linha de comando hello. Isso converte hello. PEM tooa. pfx arquivo com a chave privada hello. senha Olá para o arquivo. pfx de hello, em seguida, é solicitada pelo OpenSSL.

        "C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt
  * **Senha do certificado do aplicativo**: senha Olá para criar o arquivo. pfx de saudação.
  * **ID da senha de aplicativo Cert**: você deve carregar senha hello, semelhante toohow carregar outras chaves de serviços de mídia. Saudação de uso **ContentKeyType.FairPlayPfxPassword** Olá de tooget valor de enum ID de serviços de mídia Este é o que precisam toouse dentro de opção de política de distribuição de chaves de saudação.
  * **iv**: é um valor aleatório de 16 bytes. Ele deve corresponder Olá iv na política de entrega de ativos de saudação. Gerar Olá iv e colocá-la em dois lugares: política de distribuição Olá ativo e opção de política de distribuição de chaves de saudação.
  * **Peça**: essa chave é recebida quando você gerar certificação Olá usando o portal do desenvolvedor Apple Olá. Cada equipe de desenvolvimento receberá uma ASK exclusiva. Salvar uma cópia do hello peça e armazená-lo em um local seguro. Você precisará tooconfigure peça como FairPlayAsk tooMedia serviços mais tarde.
  * **ID da ASK**: essa ID é obtida quando você faz upload da ASK nos Serviços de Mídia. Você deve carregar peça usando Olá **ContentKeyType.FairPlayAsk** valor de enumeração. Como resultado de Olá Olá ID de serviços de mídia será retornado e isso é o que deve ser usado ao configurar a opção de política de distribuição de chaves de saudação.

Olá itens a seguir devem ser definidos por saudação do lado do cliente FPS:

  * **Certificado do aplicativo (AC)**: Este é um arquivo de.cer/.der que contém a chave pública do hello, sistema operacional no qual Olá usa tooencrypt alguns carga. Serviços de mídia precisa tooknow sobre ele porque ela é necessária pelo player hello. serviço de distribuição de chaves Olá descriptografa usando a chave privada correspondente do hello.

tooplay um fluxo criptografado FairPlay, obter uma peça real primeiro e, em seguida, gerar um certificado real. Esse processo cria três partes:

  * arquivo .der
  * arquivo .pfx
  * senha para. Olá pfx

os seguintes clientes Hello suportam HLS com **CBC AES-128** criptografia: Safari nos X, Apple TV, iOS.

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a>Configurar a criptografia dinâmica do FairPlay e os serviços de distribuição de licenças
Olá seguem etapas gerais para proteger seus ativos com FairPlay usando o serviço de entrega de licença de serviços de mídia Olá e também com o uso de criptografia dinâmica.

1. Criar um ativo e carregar arquivos no ativo de saudação.
2. Codifica o ativo de saudação que contenha Olá arquivo toohello taxa de bits adaptável que MP4 definido.
3. Criar uma chave de conteúdo e associá-lo com ativo Olá codificado.  
4. Configure a política de autorização da chave de saudação conteúdo. Especifique Olá seguinte:

   * método de entrega da saudação (nesse caso, FairPlay).
   * a configuração de opções de política do FairPlay. Para obter detalhes sobre como tooconfigure FairPlay, consulte Olá **ConfigureFairPlayPolicyOptions()** método no exemplo hello abaixo.

     > [!NOTE]
     > Normalmente, você desejaria tooconfigure FairPlay política opções apenas uma vez, porque você terá apenas um conjunto de uma certificação e uma peça.
     >
     >
   * Restrições (abertas ou token).
   * Informações específicas toohello entrega de chave tipo que define como chave Olá é entregue toohello cliente.
5. Configure a política de distribuição de ativos de saudação. configuração de política de distribuição de saudação inclui:

   * protocolo de entrega da saudação (HLS).
   * tipo de saudação de criptografia dinâmica (criptografia CBC comum).
   * Olá URL de aquisição de licença.

     > [!NOTE]
     > Se você quiser toodeliver um fluxo que é criptografado com FairPlay e outro sistema de gerenciamento de direitos digitais (DRM), você tem políticas de entrega separada tooconfigure:
     >
     > * Um tooconfigure IAssetDeliveryPolicy Streaming adaptável dinâmico sobre HTTP (traço) com o Common Encryption (CENC) (PlayReady + Widevine) e Smooth com PlayReady
     > * Outro IAssetDeliveryPolicy tooconfigure FairPlay para HLS
     >
     >
6. Crie um tooget de localizador OnDemand uma URL de streaming.

## <a name="use-fairplay-key-delivery-by-player-apps"></a>Usar a distribuição de chaves do FairPlay para aplicativos de player
Você pode desenvolver aplicativos player usando o SDK do iOS hello. toobe capaz de tooplay FairPlay conteúdo, você tem protocolo de intercâmbio de licença tooimplement hello. Esse protocolo não é especificado pela Apple. É o aplicativo tooeach como entrega de chave toosend solicitações. Olá serviço de entrega de chave do Media Services FairPlay espera Olá SPC toocome como uma mensagem de post codificados www-form-url, em Olá formulário a seguir:

    spc=<Base64 encoded SPC>

> [!NOTE]
> Player de mídia do Azure não dá suporte a reprodução FairPlay imediato saudação. tooget FairPlay reprodução no MAC OS X, obter reprodutor da amostra de saudação do hello conta de desenvolvedor da Apple.
>
>

## <a name="streaming-urls"></a>URLs de streaming
Se seu ativo foi criptografado com DRM de mais de um, você deve usar uma marca de criptografia na URL de streaming de saudação: (formato = 'm3u8-aapl', criptografia = 'xxx').

Olá considerações a seguir se aplicam:

* Pode ser especificado apenas zero ou um tipo de criptografia.
* tipo de criptografia de saudação não tem toobe especificado na URL de saudação se apenas uma criptografia foi aplicada toohello ativo.
* tipo de criptografia Olá diferencia maiusculas de minúsculas.
* Olá seguintes tipos de criptografia pode ser especificada:  
  * **cenc**: criptografia comum (PlayReady ou Widevine)
  * **cbcs-aapl**: FairPlay
  * **cbc**: criptografia de envelope AES

## <a name="create-and-configure-a-visual-studio-project"></a>Criar e configurar um projeto do Visual Studio

1. Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md). 
2. Adicionar Olá elementos a seguir muito**appSettings** definido no seu arquivo App. config:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a>Exemplo

saudação de exemplo a seguir demonstra Olá capacidade toouse toodeliver de serviços de mídia seu conteúdo criptografado com FairPlay. Essa funcionalidade foi introduzida no hello Azure Media Services SDK para .NET versão 3.6.0. 

Substitua o código de saudação no arquivo Program.cs pelo código Olá mostrado nesta seção.

>[!NOTE]
>Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy). Você deve usar Olá Olá a mesma ID de política se você estiver usando sempre mesmo dias acesso permissões, por exemplo, as políticas para localizadores são tooremain desejado no local por um longo período (políticas de carregamento não). Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.

Certifique-se de que variáveis de tooupdate toopoint toofolders onde se encontram os arquivos de entrada.

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.FairPlay;
    using Newtonsoft.Json;
    using System.Security.Cryptography.X509Certificates;

    namespace DynamicEncryptionWithFairPlay
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

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonCBCTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("FairPlay License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay));
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted HLS URL: {0}/manifest(format=m3u8-aapl)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding {0}", inputAsset.Name));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        static public IContentKey CreateCommonCBCTypeContentKey(IAsset asset)
        {
            // Create HLS SAMPLE AES encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryptionCbcs);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }


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


            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();

            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
            ContentKeyDeliveryType.FairPlay,
            restrictions,
            FairPlayConfiguration);


            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with no restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                    {
                    new ContentKeyAuthorizationPolicyRestriction
                    {
                        Name = "Token Authorization Policy",
                        KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                        Requirements = tokenTemplateString,
                    }
                    };

            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();


            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                   ContentKeyDeliveryType.FairPlay,
                   restrictions,
                   FairPlayConfiguration);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with hello cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound tooa real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key toogenerate hello response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating hello .pfx file.
            string pfxPassword = "<customer password for creating hello .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key toogenerate hello response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match hello iv in hello asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify hello .pfx file created by hello customer.
            var appCert = new X509Certificate2("path toohello .pfx file created by hello customer", pfxPassword, X509KeyStorageFlags.Exportable);

            string FairPlayConfiguration =
            Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
                appCert,
                pfxPassword,
                pfxPasswordId,
                askId,
                iv);

            return FairPlayConfiguration;
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

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            var kdPolicy = _context.ContentKeyAuthorizationPolicies.Where(p => p.Id == key.AuthorizationPolicyId).Single();

            var kdOption = kdPolicy.Options.Single(o => o.KeyDeliveryType == ContentKeyDeliveryType.FairPlay);

            FairPlayConfiguration configFP = JsonConvert.DeserializeObject<FairPlayConfiguration>(kdOption.KeyDeliveryConfiguration);

            // Get hello FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // hello reason hello below code replaces "https://" with "skd://" is because
            // in hello IOS player sample code which you obtained in Apple developer account,
            // hello player only recognizes a Key URL that starts with skd://.
            // However, if you are using a customized player,
            // you can choose whatever protocol you want.
            // For example, "https".

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, acquisitionUrl.ToString().Replace("https://", "skd://")},
                    {AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs, configFP.ContentEncryptionIV}
            };

            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
            AssetDeliveryProtocol.HLS,
            assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }


        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
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


## <a name="next-steps-media-services-learning-paths"></a>Próximas etapas: roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
