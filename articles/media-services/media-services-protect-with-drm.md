---
title: "aaaUsing PlayReady e/ou Widevine comuns criptografia dinâmica | Microsoft Docs"
description: "Serviços de mídia do Microsoft Azure permite que você toodeliver MPEG-DASH, Smooth Streaming e Http-Live-Streaming (HLS) fluxos protegidos com o Microsoft PlayReady DRM. Ele também permite que você toodelivery DASH criptografado com Widevine DRM. Este tópico mostra como toodynamically criptografar com PlayReady e Widevine DRM."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 548d1a12-e2cb-45fe-9307-4ec0320567a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 0475e6ec80dcf39eb4e5c4ad4d17f821502951bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-playready-andor-widevine-dynamic-common-encryption"></a>Usando a criptografia comum dinâmica PlayReady e/ou Widevine

> [!div class="op_single_selector"]
> * [.NET](media-services-protect-with-drm.md)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>
>

Serviços de mídia do Microsoft Azure permite que você toodeliver MPEG-DASH, Smooth Streaming e fluxos de HTTP-Live-Streaming (HLS) protegidos com [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). Ele também permite fluxos de traço toodeliver criptografado com licenças Widevine DRM. PlayReady e Widevine são criptografados por Olá especificação de criptografia comum (ISO/IEC 23001-7 CENC). Você pode usar [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (começando com a versão de hello 3.5.1) ou REST API tooconfigure seu toouse AssetDeliveryConfiguration Widevine.

Os Serviços de Mídia fornecem um serviço para entregar licenças DRM do PlayReady e do Widevine. Serviços de mídia oferecem APIs que permitem que você configure direitos hello e restrições que você deseja para Olá tooenforce de tempo de execução PlayReady ou Widevine DRM quando um usuário é reproduzido conteúdo protegido. Quando um usuário solicita um conteúdo protegido por DRM, o aplicativo de player hello solicitará uma licença do serviço de licença Olá AMS. serviço de licença AMS Olá emitirá um player de toohello de licença se ele está autorizado. Uma licença do PlayReady ou Widevine contém a chave de descriptografia de saudação que pode ser usado por Olá cliente player toodecrypt e fluxo Olá conteúdo.

Você também pode usar o hello AMS parceiros toohelp fornecer licenças Widevine a seguir: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/). Para saber mais, consulte: integração com [Axinom](media-services-axinom-integration.md) e [castLabs](media-services-castlabs-integration.md).

Os serviços de mídia oferecem suporte a várias maneiras de autorizar os usuários que fazem solicitações de chave. Olá política de autorização da chave de conteúdo pode ter uma ou mais restrições de autorização: abrir ou restrição de token. política de restrição de token de saudação deve ser acompanhada por um token emitido por um Token STS (serviço seguro). Serviços de mídia oferece suporte a tokens no hello [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) formato (SWT) e [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) formato (JWT). Para obter mais informações, consulte a política de autorização de configurar Olá da chave de conteúdo.

tootake vantagem da criptografia dinâmica, você precisa toohave um ativo que contenha um conjunto de arquivos MP4 com múltiplas taxas de bits ou arquivos de origem de Smooth Streaming de várias taxas de bits. Você também precisa políticas de entrega Olá tooconfigure ativo hello (descrita posteriormente neste tópico). Em seguida, com base no formato de saudação especificado na URL de streaming de hello, Olá Streaming sob demanda servidor garantirá que fluxo Olá é fornecido no protocolo de saudação escolhida. Como resultado, você só precisa toostore e pagamento para arquivos de saudação em um único formato de armazenamento e os serviços de mídia criará e enviará a resposta HTTP apropriada Olá com base em cada solicitação de um cliente.

Este tópico seria útil toodevelopers que funcionam em aplicativos que distribuem mídia protegida com vários DRMs, como o PlayReady e Widevine. tópico de saudação mostra como tooconfigure Olá o serviço de entrega de licenças do PlayReady com as políticas de autorização para que somente clientes autorizados recebam licenças do PlayReady ou Widevine. Ele também mostra como criptografia de criptografia dinâmica toouse com PlayReady ou Widevine DRM sobre traço.

>[!NOTE]
>Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado. toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado. 

## <a name="download-sample"></a>Baixar exemplo
Você pode baixar o exemplo hello descrito neste artigo do [aqui](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).

## <a name="configuring-dynamic-common-encryption-and-drm-license-delivery-services"></a>Configurando a Criptografia Dinâmica Comum e Serviços de Distribuição de Licenças de DRM

Olá seguem etapas gerais que você precisaria tooperform para proteger seus ativos com o PlayReady, usando o serviço de entrega de licença de serviços de mídia hello e também usando criptografia dinâmica.

1. Criar um ativo e carregar arquivos no ativo de saudação.
2. Codifica Olá ativo contendo Olá arquivo toohello taxa de bits adaptável que MP4 definido.
3. Criar uma chave de conteúdo e associá-lo com ativo Olá codificado. Nos serviços de mídia, a chave de conteúdo de saudação contém chave de criptografia do ativo hello.
4. Configure a política de autorização da chave de saudação conteúdo. política de autorização da chave de conteúdo Olá deve ser configurada por você e cliente Olá para Olá conteúdo toobe chave toohello entregue cliente.

    Ao criar a política de autorização da chave de conteúdo hello, você precisa fazer toospecify Olá seguinte: método (PlayReady ou Widevine), restrições de entrega (abertas ou token) e tipo de entrega de chave de toohello específicos de informações que define como chave Olá é entregue cliente de toohello ([PlayReady](media-services-playready-license-template-overview.md) ou [Widevine](media-services-widevine-license-template-overview.md) modelo de licença).

5. Configure a política de distribuição de saudação para um ativo. configuração de política de entrega de saudação inclui: Olá de protocolo de entrega (por exemplo, MPEG DASH, HLS, Smooth Streaming ou todos), tipo de criptografia dinâmica (por exemplo, criptografia comum), PlayReady ou URL de aquisição de licenças Widevine.

    Você pode aplicar o protocolo de tooeach política diferente em Olá mesmo ativo. Por exemplo, você pode aplicar PlayReady criptografia tooSmooth/DASH e Envelope AES tooHLS. Todos os protocolos que não estão definidos em uma política de entrega (por exemplo, você adiciona uma única política que só especifica HLS como protocolo de saudação) serão impedidos de streaming. Olá toothis de exceção é se você não tiver nenhuma política de entrega de ativo definida. Em seguida, todos os protocolos poderão ser em Olá clara.

6. Crie um localizador OnDemand em ordem tooget uma URL de streaming.

Você encontrará um exemplo completo de .NET final Olá Olá tópico.

Olá a imagem a seguir demonstra o fluxo de trabalho de saudação descrito acima. Aqui o token de saudação é usado para autenticação.

![Proteger com o PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

restante deste tópico Olá fornece explicações detalhadas, exemplos de código e tootopics links que mostram como tooachieve Olá as tarefas descritas acima.

## <a name="current-limitations"></a>Limitações atuais
Se você adicionar ou atualizar uma política de entrega de ativos, você deve excluir o localizador de saudação associada (se houver) e criar um novo.

Limitação ao criptografar com o Widevine com os Serviços de Mídia do Azure: atualmente, não há suporte para várias chaves de conteúdo.

## <a name="create-an-asset-and-upload-files-into-hello-asset"></a>Criar um ativo e carregar arquivos no ativo de saudação
Em ordem toomanage, codificar e transmitir seus vídeos, primeiro você deve carregar o conteúdo nos serviços de mídia do Microsoft Azure. Uma vez carregado, seu conteúdo é armazenado com segurança na nuvem Olá para processamento e streaming.

Para obter informações detalhadas, consulte [Carregar arquivos em uma conta dos Serviços de Mídia](media-services-dotnet-upload-files.md).

## <a name="encode-hello-asset-containing-hello-file-toohello-adaptive-bitrate-mp4-set"></a>Codificar Olá ativo contendo Olá arquivo toohello taxa de bits adaptável que MP4 set
Com criptografia dinâmica, tudo o que você precisa é toocreate um ativo que contenha um conjunto de arquivos MP4 com múltiplas taxas de bits ou arquivos de origem de Smooth Streaming de várias taxas de bits. Em seguida, com base no formato de saudação especificado no manifesto de saudação e solicitação de fragmento, Olá sob demanda de Streaming server irá garantir que você receba o fluxo de saudação no protocolo hello escolhido. Como resultado, você só precisa toostore e pagamento para arquivos de saudação em único formato de armazenamento e serviços de mídia criará e enviará a resposta apropriada hello, com base nas solicitações de um cliente. Para obter mais informações, consulte Olá [visão geral do empacotamento dinâmico](media-services-dynamic-packaging-overview.md) tópico.

Para obter instruções sobre como tooencode, consulte [como tooencode um ativo usando o codificador de mídia padrão](media-services-dotnet-encode-with-media-encoder-standard.md).

## <a id="create_contentkey"></a>Criar uma chave de conteúdo e associá-lo com ativo Olá codificado
Nos serviços de mídia, a chave de conteúdo de saudação contém chave Olá que você deseja tooencrypt um ativo com.

Para obter informações detalhadas, consulte [Criar chave de conteúdo](media-services-dotnet-create-contentkey.md).

## <a id="configure_key_auth_policy"></a>Configurar política de autorização da chave de saudação conteúdo
Os serviços de mídia oferecem suporte a várias maneiras de autenticar os usuários que fazem solicitações de chave. política de autorização da chave de conteúdo Olá deve ser configurada por você e Olá cliente (player) em ordem para Olá toobe chave entregue toohello cliente. Olá política de autorização da chave de conteúdo pode ter uma ou mais restrições de autorização: abrir ou restrição de token.

Para obter informações detalhadas, consulte [Configurar política de autorização de chave de conteúdo](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).

## <a id="configure_asset_delivery_policy"></a>Configurar política de entrega de ativos
Configure a política de distribuição de saudação para seu ativo. Algumas coisas que Olá a configuração de política de entrega de ativos inclui:

* Olá DRM URL de aquisição de licença.
* Olá ativo protocolo de entrega (por exemplo, MPEG DASH, HLS, Smooth Streaming ou todos).
* tipo de saudação de criptografia dinâmica (neste caso, criptografia comum).

Para obter informações detalhadas, consulte [Configurar política de entrega de ativos ](media-services-rest-configure-asset-delivery-policy.md).

## <a id="create_locator"></a>Criar um OnDemand streaming localizador de ordem tooget uma URL de streaming
Você precisará tooprovide seu usuário com hello streaming URL para Smooth, DASH ou HLS.

> [!NOTE]
> Se você adicionar ou atualizar a política de fornecimento do ativo, você deve excluir um localizador existente (se houver) e criar um novo localizador.
>
>

Para obter instruções sobre como toopublish um ativo e compilar uma URL de streaming, consulte [construir uma URL de streaming](media-services-deliver-streaming-content.md).

## <a name="get-a-test-token"></a>Obter um token de teste
Obtenha um teste de token com base na restrição de token de saudação que foi usada para a política de autorização da chave de saudação.

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string.
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);


Você pode usar o hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest seu fluxo.

## <a name="create-and-configure-a-visual-studio-project"></a>Criar e configurar um projeto do Visual Studio

1. Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md). 
2. Adicionar Olá elementos a seguir muito**appSettings** definido no seu arquivo App. config:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a>Exemplo

Olá exemplo a seguir demonstra a funcionalidade que foi introduzida no SDK de serviços de mídia do Azure para .net-versão 3.5.2 (especificamente, Olá capacidade toodefine um Widevine modelo de licença e solicitam uma licença de Widevine dos serviços de mídia do Azure).

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
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DynamicEncryptionWithDRM
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

            IContentKey key = CreateCommonTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("PlayReady License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));
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

            // You can use hello http://amsplayer.azurewebsites.net/azuremediaplayer.html player tootest streams.
            // Note that DASH works on IE 11 (via PlayReady), Edge (via PlayReady), Chrome (via Widevine).

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted DASH URL: {0}/manifest(format=mpd-time-csf)", url);

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

            IJob job = _context.Jobs.Create(String.Format("Encoding into Mp4 {0} too{1}",
                        inputAsset.Name,
                        encodingPreset));

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


        static public IContentKey CreateCommonTypeContentKey(IAsset asset)
        {

            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryption);

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

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
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

        private static string ConfigureWidevineLicenseTemplate()
        {
            var template = new WidevineMessage
            {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                    new ContentKeySpecs
                    {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
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

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            // Get hello PlayReady license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

            // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
            // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
            // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption
            // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
            // As a result Widevine license acquisition URL will have KID appended twice,
            // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

            Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
            UriBuilder uriBuilder = new UriBuilder(widevineUrl);
            uriBuilder.Query = String.Empty;
            widevineUrl = uriBuilder.Uri;

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
                    {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl, widevineUrl.ToString()}

            };

            // In this case we only specify Dash streaming protocol in hello delivery policy,
            // All other protocols will be blocked from streaming.
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
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


## <a name="next-step"></a>Próxima etapa
Revise os roteiros de aprendizagem dos Serviços de Mídia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Confira também
[CENC com DRM múltiplo e controle de acesso](media-services-cenc-with-multidrm-access-control.md)

[Configurar o empacotamento Widevine com AMS](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)

[Anunciando os serviços de entrega de licenças do Google Widevine nos Serviços de Mídia do Azure](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)
