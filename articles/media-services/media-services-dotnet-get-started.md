---
title: "aaaGet iniciado com o fornecimento de conteúdo sob demanda usando .NET | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de saudação da implementação de um aplicativo de entrega de conteúdo na demanda com o Azure Media Services usando o .NET."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 388b8928-9aa9-46b1-b60a-a918da75bd7b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 4ca9394bd581e1d9062e5a008a410b2c058e017e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a>Introdução ao fornecimento de conteúdo sob demanda usando o SDK do .NET
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

Este tutorial orienta você pelas etapas de saudação da implementação de um serviço básico de fornecimento de conteúdo de vídeo sob demanda (VoD) com aplicativos de serviços de mídia do Azure (AMS) usando o SDK do Azure Media Services .NET de saudação.

## <a name="prerequisites"></a>Pré-requisitos

Olá seguem tutorial de saudação toocomplete necessária:

* Uma conta do Azure. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* Uma conta dos Serviços de Mídia. toocreate uma conta de serviços de mídia, consulte [como tooCreate uma conta do Media Services](media-services-portal-create-account.md).
* .NET Framework 4.0 ou posterior.
* Visual Studio.

Este tutorial inclui Olá tarefas a seguir:

1. Inicie o streaming de ponto de extremidade (usando Olá portal do Azure).
2. Criar e configurar um projeto do Visual Studio.
3. Conecte-se a conta de serviços de mídia toohello.
2. Carregar um arquivo de vídeo.
3. Codifica o arquivo de origem de saudação em um conjunto de arquivos MP4 com taxa de bits adaptável.
4. Publica ativo hello e get streaming e URLs de download progressivo.  
5. Reproduzir o conteúdo.

## <a name="overview"></a>Visão geral
Este tutorial orienta você pelas etapas de saudação da implementação de um aplicativo de entrega de conteúdo de vídeo sob demanda (VoD) usando os serviços de mídia do Azure (AMS) SDK para .NET.

tutorial de Olá apresenta o fluxo de trabalho de serviços de mídia básico hello e objetos de programação mais comuns hello e tarefas necessárias para o desenvolvimento de serviços de mídia. Na conclusão de saudação do tutorial Olá, você será capaz de toostream ou baixar progressivamente um arquivo de mídia de exemplo que você carregado, codificado e baixado.

### <a name="ams-model"></a>Modelo do AMS

Hello imagem a seguir mostra alguns dos objetos hello mais comumente usada ao desenvolver aplicativos VoD em modelo de mídia serviços OData hello.

Clique em Olá imagem tooview-tamanho máximo.  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

Você pode exibir uma saudação todo modelo [aqui](https://media.windows.net/API/$metadata?api-version=2.15).  

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a>Iniciar o streaming de pontos de extremidade usando Olá portal do Azure

Ao trabalhar com o Azure Media Services, um dos cenários mais comuns de saudação está entregando vídeo por meio de streaming de taxa de bits adaptável. Serviços de mídia fornecem empacotamento dinâmico, que permite que você toodeliver sua taxa de bits adaptável MP4 codificados conteúdo de streaming formatos suportados pelo Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, sem a necessidade de toostore pacote predefinido versões de cada um desses formatos de fluxo contínuo.

>[!NOTE]
>Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado. toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado.

toostart Olá ponto de extremidade de streaming, Olá a seguir:

1. Faça logon em Olá [portal do Azure](https://portal.azure.com/).
2. Na janela de configurações de saudação, clique em pontos de extremidade de Streaming.
3. Clique em padrão Olá ponto de extremidade de streaming.

    saudação padrão detalhes do ponto de EXTREMIDADE de STREAMING de janela é exibida.

4. Clique o ícone de início de saudação.
5. Clique em Olá toosave de botão de salvar suas alterações.

## <a name="create-and-configure-a-visual-studio-project"></a>Criar e configurar um projeto do Visual Studio

1. Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md). 
2. Crie uma nova pasta (pasta pode estar em qualquer lugar no disco local) e copie um arquivo. mp4 que você deseja tooencode e fluxo ou download progressivo. Neste exemplo, o caminho de "C:\VideoFiles" hello é usado.

## <a name="connect-toohello-media-services-account"></a>Conecte-se a conta de serviços de mídia toohello

Ao usar os serviços de mídia com .NET, você deve usar o hello **CloudMediaContext** classe para a maioria dos serviços de mídia tarefas de programação: conectar-se a conta de serviços tooMedia; criar, atualizar, acessar e excluir o seguinte Olá objetos: ativos, arquivos de ativos, trabalhos, políticas de acesso, os localizadores, etc.

Substitua a classe de programa padrão Olá com hello código a seguir. Olá código demonstra como conexão de saudação tooread os valores do arquivo App. config de saudação e Olá toocreate **CloudMediaContext** objeto na ordem tooconnect tooMedia de serviços. Para obter mais informações, consulte [conexão toohello API de serviços de mídia](media-services-use-aad-auth-to-access-ams-api.md).

Certifique-se de que tooupdate Olá arquivo nome e caminho toowhere que tiver seu arquivo de mídia.

Olá **principal** função chama métodos que serão definidos mais nesta seção.

> [!NOTE]
> Você obterá erros de compilação até que você adicione definições para todas as funções hello.

    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
        try
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Add calls toomethods defined in this section.
            // Make sure tooupdate hello file name and path toowhere you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse hello XML error message in hello Media Services response and create a new
            // exception with its content.
            exception = MediaServicesExceptionParser.Parse(exception);

            Console.Error.WriteLine(exception.Message);
        }
        finally
        {
            Console.ReadLine();
        }
        }
    }

## <a name="create-a-new-asset-and-upload-a-video-file"></a>Criar um novo ativo e carregar um arquivo de vídeo

No Serviços de Mídia, você carrega (ou ingere) seus arquivos digitais em um ativo. Olá **ativo** entidade pode conter vídeo, áudio, imagens, coleções de miniaturas, texto faixas e legenda codificada arquivos (e Olá metadados sobre esses arquivos.)  Depois que forem carregados arquivos hello, seu conteúdo é armazenado com segurança na nuvem de saudação para processamento adicional e streaming. Olá arquivos no ativo de saudação são chamados **arquivos de ativo**.

Olá **UploadFile** definido abaixo chamadas de método **CreateFromFile** (definido em extensões do SDK do .NET). **CreateFromFile** cria um novo ativo em qual Olá o arquivo de origem especificado é carregado.

Olá **CreateFromFile** leva **AssetCreationOptions** que permite que você especifique uma saudação seguindo as opções de criação de ativo:

* **None** - nenhuma criptografia é usada. Este é o valor padrão de saudação. Observe que, ao usar essa opção, seu conteúdo não será protegido quando estiver em trânsito ou em repouso no armazenamento.
  Se você planejar toodeliver um MP4 usando o download progressivo, use essa opção.
* **StorageEncrypted** -Use essa opção tooencrypt o conteúdo limpo localmente usando a criptografia de-256 bits (AES padrão), que carrega tooAzure armazenamento onde ele está armazenado criptografado em repouso. Ativos protegidos pela criptografia de armazenamento são descriptografados automaticamente e posicionados em um tooencoding anterior do sistema de arquivos criptografados e, opcionalmente, criptografada novamente toouploading anterior como um novo ativo de saída. caso de uso primário Olá para criptografia de armazenamento é quando você deseja toosecure seus arquivos de mídia de entrada de alta qualidade com criptografia forte em rest no disco.
* **CommonEncryptionProtected** — use esta opção se você estiver carregando conteúdo que já foi criptografado e protegido com criptografia comum ou DRM PlayReady (por exemplo, Smooth Streaming protegido com DRM PlayReady).
* **EnvelopeEncryptionProtected** – use esta opção se você estiver carregando HLS criptografado com AES. Observe que arquivos Olá devem ter sido codificados e criptografados pelo Transform Manager.

Olá **CreateFromFile** método também permite especificar um retorno de chamada em andamento do upload ordem tooreport saudação do arquivo hello.

Saudação de exemplo a seguir, especificamos **nenhum** para opções de ativo de saudação.

Adicione Olá classe do método toohello programa a seguir.

    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }


## <a name="encode-hello-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a>Codificar o arquivo de origem de saudação em um conjunto de arquivos MP4 com taxa de bits adaptável
Após a ingestão de ativos nos serviços de mídia, a mídia pode ser codificado, transmultiplexar, marca d'água e assim por diante, antes de entregar tooclients. Essas atividades são agendadas e executadas várias em segundo plano função instâncias tooensure alto desempenho e disponibilidade. Essas atividades são chamadas de trabalhos, e cada trabalho é composto de tarefas atômicas que Olá real trabalho no arquivo de ativo de saudação.

Como foi mencionado anteriormente, ao trabalhar com os serviços de mídia do Azure, um dos cenários mais comuns de saudação está entregando tooyour clientes de streaming de taxa de bits adaptável. Serviços de mídia pode empacotar dinamicamente um conjunto de arquivos MP4 com taxa de bits adaptável em uma saudação formatos a seguir: HTTP Live Streaming (HLS), Smooth Streaming e MPEG DASH.

tootake proveito do empacotamento dinâmico, você precisa tooencode ou transcodificar o arquivo de mezanino (origem) em um conjunto de arquivos MP4 de taxa de bits adaptável ou arquivos de Smooth Streaming de taxa de bits adaptável.  

saudação de código a seguir mostra como toosubmit uma codificação de trabalho. trabalho Hello contém uma tarefa que especifica o arquivo de mezanino Olá tootranscode em um conjunto de MP4s de taxa de bits adaptável usando **codificador de mídia padrão**. código de saudação envia trabalho hello e aguarda até que ela seja concluída.

Após a conclusão do trabalho hello, deve ser capaz de toostream seu ativo ou download progressivo de arquivos MP4 que foram criados como resultado de transcodificação.

Adicione Olá classe do método toohello programa a seguir.

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task tootranscode hello specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit hello job and wait until it is completed.
        job.Submit();

        job = job.StartExecutionProgressTask(
            j =>
            {
                Console.WriteLine("Job state: {0}", j.State);
                Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
            },
            CancellationToken.None).Result;

        Console.WriteLine("Transcoding job finished.");

        IAsset outputAsset = job.OutputMediaAssets[0];

        return outputAsset;
    }

## <a name="publish-hello-asset-and-get-urls-for-streaming-and-progressive-download"></a>Publicar Olá ativo e obter URLs de download progressivo e streaming

toostream ou baixar um ativo, você primeiro precisa muito "Publicar"-lo criando um localizador. Os localizadores fornecem acesso toofiles contidos em Olá ativo. Serviços de mídia oferece suporte a dois tipos de localizadores: OnDemandOrigin localizadores, mídia toostream usado (por exemplo, MPEG DASH, HLS ou Smooth Streaming) e localizadores da assinatura de acesso (SAS), usados arquivos de mídia toodownload (para obter mais informações sobre consulte localizadores SAS [isso](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).

### <a name="some-details-about-url-formats"></a>Alguns detalhes sobre os formatos de URL

Depois de criar localizadores hello, você pode criar URLs Olá que deve ser usado toostream ou baixar os arquivos. exemplo Hello neste tutorial mostrará as URLs que você pode colar em navegadores apropriados. Esta seção fornece apenas breves exemplos da aparência de formatos diferentes.

#### <a name="a-streaming-url-for-mpeg-dash-has-hello-following-format"></a>Uma URL de streaming MPEG DASH tem Olá formato a seguir:

{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**

#### <a name="a-streaming-url-for-hls-has-hello-following-format"></a>Uma URL de streaming para HLS tem Olá formato a seguir:

{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**

#### <a name="a-streaming-url-for-smooth-streaming-has-hello-following-format"></a>Uma URL de streaming para Smooth Streaming tem Olá formato a seguir:

{nome do ponto de extremidade de streaming - nome de conta do dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arqui}.ism/Manifest


#### <a name="a-sas-url-used-toodownload-files-has-hello-following-format"></a>Arquivos de toodownload uma URL SAS usada tem Olá formato a seguir:

{nome do contêiner de blob}/{nome do ativo}/{nome do arquivo}/{assinatura SAS}

Extensões do SDK do Media Services .NET fornecem métodos auxiliares conveniente que retornam formatada URLs para Olá publicado ativo.

Olá, código a seguir usa os localizadores toocreate de extensões do SDK do .NET e URLs de download progressivo e streaming tooget. código de saudação também mostra como toodownload arquivos de pasta local tooa.

Adicione Olá classe do método toohello programa a seguir.

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish hello output asset by creating an Origin locator for adaptive streaming,
        // and a SAS locator for progressive download.

        _context.Locators.Create(
            LocatorType.OnDemandOrigin,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));

        _context.Locators.Create(
            LocatorType.Sas,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));


        IEnumerable<IAssetFile> mp4AssetFiles = asset
                .AssetFiles
                .ToList()
                .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Get hello Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and hello Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get hello URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  hello streaming URLs.
        Console.WriteLine("Use hello following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display hello URLs for progressive download.
        Console.WriteLine("Use hello following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download hello output asset tooa local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files tooa local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a>Testar ao reproduzir o conteúdo

Quando você executar o programa de saudação definido na seção anterior hello, Olá URLs a seguir toohello semelhante será exibida na janela de console hello.

URLs de streaming adaptáveis:

Smooth Streaming

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

HLS

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

MPEG DASH

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

URLs de download progressivo (áudio e vídeo).

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


toostream seu vídeo, cole a URL na caixa de texto Olá URL no hello [Player de serviços de mídia do Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

tootest progressivo baixar, cole uma URL em um navegador (por exemplo, Internet Explorer, Chrome ou Safari).

Para obter mais informações, consulte Olá seguintes tópicos:

- [Reprodução de seu conteúdo com players existentes](media-services-playback-content-with-existing-players.md)
- [Desenvolver aplicativos de player de vídeo](media-services-develop-video-players.md)
- [Inserindo um vídeo de streaming adaptável MPEG-DASH em um aplicativo HTML5 com DASH.js](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a>Baixar exemplo
exemplo de código a seguir Hello contém código Olá criado neste tutorial: [exemplo](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
