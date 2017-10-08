---
title: "aaaUsing AES-128 dinâmico criptografia e a chave de serviço de entrega | Microsoft Docs"
description: "Serviços de mídia do Microsoft Azure permite que você toodeliver seu conteúdo criptografado com chaves de criptografia AES de 128 bits. Serviços de mídia também fornece o serviço de entrega de chave de saudação que oferece aos usuários tooauthorized de chaves de criptografia. Este tópico mostra como toodynamically criptografar com AES-128 e usar o serviço de distribuição de chaves de saudação."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 4d2c10af-9ee0-408f-899b-33fa4c1d89b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: cb1b413ec2ba79f7437464099cf72236ab93f312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-aes-128-dynamic-encryption-and-key-delivery-service"></a>Uso da criptografia dinâmica AES-128 e serviço de distribuição de chaves
> [!div class="op_single_selector"]
> * [.NET](media-services-protect-with-aes128.md)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Visão geral
> [!NOTE]
> Consulte [isso](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) vídeo para obter uma visão geral de como tooprotect seu conteúdo de mídia com a criptografia AES.
> 
> 

Serviços de mídia do Microsoft Azure permite que você toodeliver Http-Live-Streaming (HLS) e Smooth Streams criptografados com Advanced Encryption Standard (AES) (usando chaves de criptografia de 128 bits). Serviços de mídia também fornece o serviço de entrega de chave de saudação que oferece aos usuários tooauthorized de chaves de criptografia. Se você quiser para serviços de mídia tooencrypt um ativo, você precisa tooassociate uma chave de criptografia com ativo hello e também configurar políticas de autorização para a chave de saudação. Quando um fluxo é solicitado por um player, o Media Services usa Olá especificado toodynamically chave criptografar seu conteúdo usando a criptografia AES. fluxo de saudação toodecrypt, player Olá solicitar chave Olá do serviço de distribuição de chaves de saudação. toodecide ou não usuário Olá é autorizado chave de saudação tooget, serviço Olá avalia as políticas de autorização de saudação que você especificou para a chave de saudação.

Os serviços de mídia oferecem suporte a várias maneiras de autenticar os usuários que fazem solicitações de chave. Olá política de autorização da chave de conteúdo pode ter uma ou mais restrições de autorização: abrir ou restrição de token. política de restrição de token de saudação deve ser acompanhada por um token emitido por um Token STS (serviço seguro). Serviços de mídia oferece suporte a tokens no hello [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) formato (SWT) e [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) formato (JWT). Para obter mais informações, consulte [configurar política de autorização da chave de saudação conteúdo](media-services-protect-with-aes128.md#configure_key_auth_policy).

tootake vantagem da criptografia dinâmica, você precisa toohave um ativo que contenha um conjunto de arquivos MP4 com múltiplas taxas de bits ou arquivos de origem de Smooth Streaming de várias taxas de bits. Você também precisa tooconfigure política de entrega de saudação para ativo hello (descrito posteriormente neste tópico). Em seguida, com base no formato de saudação especificado na URL de streaming de hello, Olá Streaming sob demanda servidor garantirá que fluxo Olá é fornecido no protocolo de saudação escolhida. Como resultado, você só precisa toostore e pagamento para arquivos de saudação em único formato de armazenamento e serviços de mídia criará e enviará a resposta apropriada hello, com base nas solicitações de um cliente.

Este tópico seria útil toodevelopers que trabalham em aplicativos que distribuem mídia protegida. tópico de saudação mostra como tooconfigure Olá o serviço de entrega de chave com políticas de autorização para que somente clientes autorizados recebam as chaves de criptografia de saudação. Ele também mostra como criptografia dinâmica toouse.


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a>Criptografia dinâmica AES-128 e fluxo de trabalho de serviço de distribuição de chaves

Olá seguem etapas gerais que você precisaria tooperform ao criptografar seus ativos com AES, usando o serviço de distribuição de chaves de serviços de mídia hello e também usar criptografia dinâmica.

1. [Criar um ativo e carregar arquivos no ativo Olá](media-services-protect-with-aes128.md#create_asset).
2. [Codificar Olá ativo que contém a saudação arquivo toohello taxa de bits adaptável MP4 conjunto](media-services-protect-with-aes128.md#encode_asset).
3. [Criar uma chave de conteúdo e associá-lo com ativo Olá codificado](media-services-protect-with-aes128.md#create_contentkey). Nos serviços de mídia, a chave de conteúdo de saudação contém chave de criptografia do ativo hello.
4. [Configurar política de autorização da chave de saudação conteúdo](media-services-protect-with-aes128.md#configure_key_auth_policy). política de autorização da chave de conteúdo Olá deve ser configurada por você e cliente Olá para Olá conteúdo toobe chave toohello entregue cliente.
5. [Configurar a política de entrega Olá para um ativo](media-services-protect-with-aes128.md#configure_asset_delivery_policy). configuração de política de entrega de saudação inclui: URL de aquisição e o vetor de inicialização (IV) de chave (AES 128 exigem hello mesmo toobe de IV fornecido ao criptografar e descriptografar), protocolo de entrega (por exemplo, MPEG DASH, HLS, Smooth Streaming ou todos), Olá tipo de criptografia dinâmica (por exemplo, envelope ou nenhuma criptografia dinâmica).

    Você pode aplicar o protocolo de tooeach política diferente em Olá mesmo ativo. Por exemplo, você pode aplicar PlayReady criptografia tooSmooth/DASH e Envelope AES tooHLS. Todos os protocolos que não estão definidos em uma política de entrega (por exemplo, você adiciona uma única política que só especifica HLS como protocolo de saudação) serão impedidos de streaming. Olá toothis de exceção é se você não tiver nenhuma política de entrega de ativo definida. Em seguida, todos os protocolos poderão ser em Olá clara.

6. [Criar um localizador OnDemand](media-services-protect-with-aes128.md#create_locator) em ordem tooget uma URL de streaming.

Olá tópico também mostra [como um aplicativo cliente pode solicitar uma chave de serviço de distribuição de chaves Olá](media-services-protect-with-aes128.md#client_request).

Você encontrará um .NET completo [exemplo](media-services-protect-with-aes128.md#example) final Olá Olá tópico.

Olá a imagem a seguir demonstra o fluxo de trabalho de saudação descrito acima. Aqui o token de saudação é usado para autenticação.

![Proteger com o AES-128](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

restante deste tópico Olá fornece explicações detalhadas, exemplos de código e tootopics links que mostram como tooachieve Olá as tarefas descritas acima.

## <a name="current-limitations"></a>Limitações atuais
Se você adicionar ou atualizar a política de fornecimento do ativo, você deve excluir um localizador existente (se houver) e criar um novo localizador.

## <a id="create_asset"></a>Criar um ativo e carregar arquivos no ativo de saudação
Em ordem toomanage, codificar e transmitir seus vídeos, primeiro você deve carregar o conteúdo nos serviços de mídia do Microsoft Azure. Uma vez carregado, seu conteúdo é armazenado com segurança na nuvem Olá para processamento e streaming. 

Para obter informações detalhadas, consulte [Carregar arquivos em uma conta dos Serviços de Mídia](media-services-dotnet-upload-files.md).

## <a id="encode_asset"></a>Codificar Olá ativo contendo Olá arquivo toohello taxa de bits adaptável que MP4 set
Com criptografia dinâmica, tudo o que você precisa é toocreate um ativo que contenha um conjunto de arquivos MP4 com múltiplas taxas de bits ou arquivos de origem de Smooth Streaming de várias taxas de bits. Em seguida, com base no formato de saudação especificado no manifesto de saudação ou solicitação de fragmento, Olá sob demanda de Streaming server irá garantir que você receba o fluxo de saudação no protocolo hello escolhido. Como resultado, você só precisa toostore e pagamento para arquivos de saudação em único formato de armazenamento e serviços de mídia criará e enviará a resposta apropriada hello, com base nas solicitações de um cliente. Para obter mais informações, consulte Olá [visão geral do empacotamento dinâmico](media-services-dynamic-packaging-overview.md) tópico.

>[!NOTE]
>Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado. toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado. 
>
>Além disso, o empacotamento dinâmico capaz de toouse toobe e criptografia dinâmica seu ativo deve conter um conjunto de MP4s de taxa de bits adaptável ou arquivos de Smooth Streaming de taxa de bits adaptável.

Para obter instruções sobre como tooencode, consulte [como tooencode um ativo usando o codificador de mídia padrão](media-services-dotnet-encode-with-media-encoder-standard.md).

## <a id="create_contentkey"></a>Criar uma chave de conteúdo e associá-lo com ativo Olá codificado
Nos serviços de mídia, a chave de conteúdo de saudação contém chave Olá que você deseja tooencrypt um ativo com.

Para obter informações detalhadas, consulte [Criar chave de conteúdo](media-services-dotnet-create-contentkey.md).

## <a id="configure_key_auth_policy"></a>Configurar política de autorização da chave de saudação conteúdo
Os serviços de mídia oferecem suporte a várias maneiras de autenticar os usuários que fazem solicitações de chave. política de autorização da chave de conteúdo Olá deve ser configurada por você e Olá cliente (player) em ordem para Olá toobe chave entregue toohello cliente. Olá política de autorização da chave de conteúdo pode ter uma ou mais restrições de autorização: aberta, restrição de token ou restrição de IP.

Para obter informações detalhadas, consulte [Configurar política de autorização de chave de conteúdo](media-services-dotnet-configure-content-key-auth-policy.md).

## <a id="configure_asset_delivery_policy"></a>Configurar política de entrega de ativos
Configure a política de distribuição de saudação para seu ativo. Algumas coisas que Olá a configuração de política de entrega de ativos inclui:

* Olá URL de aquisição de chave. 
* Olá toouse de vetor de inicialização (IV) para criptografia de envelope hello. AES 128 exigem Olá mesmo toobe de IV fornecido ao criptografar e descriptografar. 
* Olá ativo protocolo de entrega (por exemplo, MPEG DASH, HLS, Smooth Streaming ou todos).
* tipo de saudação de criptografia dinâmica (por exemplo, envelope AES) ou nenhuma criptografia dinâmica. 

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

## <a id="client_request"></a>Como o seu cliente pode solicitar uma chave de serviço de distribuição de chaves Olá?
Na etapa anterior de saudação, é construída Olá URL que aponta o arquivo de manifesto tooa. Seu cliente precisa tooextract Olá informações necessárias Olá streaming de arquivos de manifesto na ordem toomake um serviço de entrega de chave de toohello de solicitação.

### <a name="manifest-files"></a>Arquivos de manifesto
cliente de saudação precisa tooextract Olá URL (que também contém a chave de conteúdo Id (kid)) valor do arquivo de manifesto hello. cliente Olá tente tooget chave de criptografia de saudação do serviço de distribuição de chaves de saudação. Olá cliente também precisa tooextract Olá IV valor e use-lo para descriptografar stream.hello Olá trecho de código a seguir mostra Olá <Protection> elemento do manifesto de Smooth Streaming hello.

    <Protection>
      <ProtectionHeader SystemID="B47B251A-2409-4B42-958E-08DBAE7B4EE9">
        <ContentProtection xmlns:sea="urn:mpeg:dash:schema:sea:2012" schemeIdUri="urn:mpeg:dash:sea:2012">
          <sea:SegmentEncryption schemeIdUri="urn:mpeg:dash:sea:aes128-cbc:2013"/>
          <sea:KeySystem keySystemUri="urn:mpeg:dash:sea:keysys:http:2013"/>
          <sea:CryptoPeriod IV="0xD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7" 
                            keyUriTemplate="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
                                            kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d"/>
        </ContentProtection>
      </ProtectionHeader>
    </Protection>

No caso de saudação do HLS, o manifesto de raiz de saudação é dividido em arquivos de segmento. 

Por exemplo, o manifesto de raiz de saudação é: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) que contém uma lista de nomes de arquivo de segmento.

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

Se você abrir um dos arquivos de segmento Olá no editor de texto (por exemplo, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should conter #EXT-X-chave que indica que esse arquivo hello está criptografado.

    #EXTM3U
    #EXT-X-VERSION:4
    #EXT-X-ALLOW-CACHE:NO
    #EXT-X-MEDIA-SEQUENCE:0
    #EXT-X-TARGETDURATION:9
    #EXT-X-KEY:METHOD=AES-128,
    URI="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
         kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d",
            IV=0XD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7
    #EXT-X-PROGRAM-DATE-TIME:1970-01-01T00:00:00.000+00:00
    #EXTINF:8.425708,no-desc
    Fragments(video=0,format=m3u8-aapl)
    #EXT-X-ENDLIST

>[!NOTE] 
>Se você estiver planejando tooplay um AES criptografado HLS no Safari, consulte [este blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).

### <a name="request-hello-key-from-hello-key-delivery-service"></a>Solicitar a chave de saudação do serviço de distribuição de chaves Olá

Olá código a seguir mostra como toosend toohello uma solicitação do Media Services chave de serviço de entrega usando uma Uri (que foi extraído do manifesto de saudação) de entrega de chave e um token (Este tópico não fala sobre como tooget Simple Web Tokens de um serviço de Token seguro).

    private byte[] GetDeliveryKey(Uri keyDeliveryUri, string token)
    {
        HttpWebRequest request = (HttpWebRequest)WebRequest.Create(keyDeliveryUri);

        request.Method = "POST";
        request.ContentType = "text/xml";
        if (!string.IsNullOrEmpty(token))
        {
            request.Headers[AuthorizationHeader] = token;
        }
        request.ContentLength = 0;

        var response = request.GetResponse();

        var stream = response.GetResponseStream();
        if (stream == null)
        {
            throw new NullReferenceException("Response stream is null");
        }

        var buffer = new byte[256];
        var length = 0;
        while (stream.CanRead && length <= buffer.Length)
        {
            var nexByte = stream.ReadByte();
            if (nexByte == -1)
            {
                break;
            }
            buffer[length] = (byte)nexByte;
            length++;
        }
        response.Close();

        // AES keys must be exactly 16 bytes (128 bits).
        var key = new byte[length];
        Array.Copy(buffer, key, length);
        return key;
    }

## <a name="protect-your-content-with-aes-128-using-net"></a>Proteger o conteúdo com o AES-128 usando o .NET

### <a name="create-and-configure-a-visual-studio-project"></a>Criar e configurar um projeto do Visual Studio

1. Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md). 
2. Adicionar Olá elementos a seguir muito**appSettings** definido no seu arquivo App. config:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

### <a id="example"></a>Exemplo

Substitua o código de saudação no arquivo Program.cs pelo código Olá mostrado nesta seção.
 
>[!NOTE]
>Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy). Você deve usar Olá Olá a mesma ID de política se você estiver usando sempre mesmo dias acesso permissões, por exemplo, as políticas para localizadores são tooremain desejado no local por um longo período (políticas de carregamento não). Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.

Certifique-se de que variáveis de tooupdate toopoint toofolders onde se encontram os arquivos de entrada.

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace AESDynamicEncryptionAndKeyDeliverySvc
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // A Uri describing hello issuer of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        // hello Audience or Scope of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
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

            IContentKey key = CreateEnvelopeTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified 
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

            //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
            //so you have tooadd it in front of hello token string. 
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello bit.ly/aesplayer Flash player tootest hello URL 
            // (with open authorization policy). 
            // Paste hello URL and click hello Update button tooplay hello video. 
            //
            string URL = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Smooth Streaming Url: {0}/manifest", URL);
            Console.WriteLine();
            Console.WriteLine("HLS Url: {0}/manifest(format=m3u8-aapl)", URL);
            Console.WriteLine();

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
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.StorageEncrypted);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);


            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
        {
            // Create envelope encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                keyId,
                contentKey,
                "ContentKey",
                ContentKeyType.EnvelopeEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

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

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);

            string envelopeEncryptionIV = Convert.ToBase64String(GetRandomBuffer(16));

            // When configuring delivery policy, you can choose tooassociate it
            // with a key acquisition URL that has a KID appended or
            // or a key acquisition URL that does not have a KID appended  
            // in which case a content key can be reused. 

            // EnvelopeKeyAcquisitionUrl:  contains a key ID in hello key URL.
            // EnvelopeBaseKeyAcquisitionUrl:  hello URL does not contains a key ID

            // hello following policy configuration specifies: 
            // key url that will have KID=<Guid> appended toohello envelope and
            // hello Initialization Vector (IV) toouse for hello envelope encryption.

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeKeyAcquisitionUrl, keyAcquisitionUri.ToString()}
            };

            IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
            assetDeliveryPolicy.AssetDeliveryPolicyType);
        }

        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset. 

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
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

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int size)
        {
            byte[] randomBytes = new byte[size];
            using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(randomBytes);
            }

            return randomBytes;
        }
        }
    }


## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

