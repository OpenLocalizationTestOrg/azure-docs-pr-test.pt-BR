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
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a><span data-ttu-id="67857-103">Introdução ao fornecimento de conteúdo sob demanda usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="67857-103">Get started with delivering content on demand using .NET SDK</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="67857-104">Este tutorial orienta você pelas etapas de saudação da implementação de um serviço básico de fornecimento de conteúdo de vídeo sob demanda (VoD) com aplicativos de serviços de mídia do Azure (AMS) usando o SDK do Azure Media Services .NET de saudação.</span><span class="sxs-lookup"><span data-stu-id="67857-104">This tutorial walks you through hello steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using hello Azure Media Services .NET SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67857-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="67857-105">Prerequisites</span></span>

<span data-ttu-id="67857-106">Olá seguem tutorial de saudação toocomplete necessária:</span><span class="sxs-lookup"><span data-stu-id="67857-106">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="67857-107">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="67857-107">An Azure account.</span></span> <span data-ttu-id="67857-108">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="67857-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="67857-109">Uma conta dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="67857-109">A Media Services account.</span></span> <span data-ttu-id="67857-110">toocreate uma conta de serviços de mídia, consulte [como tooCreate uma conta do Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="67857-110">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="67857-111">.NET Framework 4.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="67857-111">.NET Framework 4.0 or later.</span></span>
* <span data-ttu-id="67857-112">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="67857-112">Visual Studio.</span></span>

<span data-ttu-id="67857-113">Este tutorial inclui Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="67857-113">This tutorial includes hello following tasks:</span></span>

1. <span data-ttu-id="67857-114">Inicie o streaming de ponto de extremidade (usando Olá portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="67857-114">Start streaming endpoint (using hello Azure portal).</span></span>
2. <span data-ttu-id="67857-115">Criar e configurar um projeto do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="67857-115">Create and configure a Visual Studio project.</span></span>
3. <span data-ttu-id="67857-116">Conecte-se a conta de serviços de mídia toohello.</span><span class="sxs-lookup"><span data-stu-id="67857-116">Connect toohello Media Services account.</span></span>
2. <span data-ttu-id="67857-117">Carregar um arquivo de vídeo.</span><span class="sxs-lookup"><span data-stu-id="67857-117">Upload a video file.</span></span>
3. <span data-ttu-id="67857-118">Codifica o arquivo de origem de saudação em um conjunto de arquivos MP4 com taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="67857-118">Encode hello source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="67857-119">Publica ativo hello e get streaming e URLs de download progressivo.</span><span class="sxs-lookup"><span data-stu-id="67857-119">Publish hello asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="67857-120">Reproduzir o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="67857-120">Play your content.</span></span>

## <a name="overview"></a><span data-ttu-id="67857-121">Visão geral</span><span class="sxs-lookup"><span data-stu-id="67857-121">Overview</span></span>
<span data-ttu-id="67857-122">Este tutorial orienta você pelas etapas de saudação da implementação de um aplicativo de entrega de conteúdo de vídeo sob demanda (VoD) usando os serviços de mídia do Azure (AMS) SDK para .NET.</span><span class="sxs-lookup"><span data-stu-id="67857-122">This tutorial walks you through hello steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) SDK for .NET.</span></span>

<span data-ttu-id="67857-123">tutorial de Olá apresenta o fluxo de trabalho de serviços de mídia básico hello e objetos de programação mais comuns hello e tarefas necessárias para o desenvolvimento de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="67857-123">hello tutorial introduces hello basic Media Services workflow and hello most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="67857-124">Na conclusão de saudação do tutorial Olá, você será capaz de toostream ou baixar progressivamente um arquivo de mídia de exemplo que você carregado, codificado e baixado.</span><span class="sxs-lookup"><span data-stu-id="67857-124">At hello completion of hello tutorial, you will be able toostream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

### <a name="ams-model"></a><span data-ttu-id="67857-125">Modelo do AMS</span><span class="sxs-lookup"><span data-stu-id="67857-125">AMS model</span></span>

<span data-ttu-id="67857-126">Hello imagem a seguir mostra alguns dos objetos hello mais comumente usada ao desenvolver aplicativos VoD em modelo de mídia serviços OData hello.</span><span class="sxs-lookup"><span data-stu-id="67857-126">hello following image shows some of hello most commonly used objects when developing VoD applications against hello Media Services OData model.</span></span>

<span data-ttu-id="67857-127">Clique em Olá imagem tooview-tamanho máximo.</span><span class="sxs-lookup"><span data-stu-id="67857-127">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="67857-128">Você pode exibir uma saudação todo modelo [aqui](https://media.windows.net/API/$metadata?api-version=2.15).</span><span class="sxs-lookup"><span data-stu-id="67857-128">You can view hello whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a><span data-ttu-id="67857-129">Iniciar o streaming de pontos de extremidade usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="67857-129">Start streaming endpoints using hello Azure portal</span></span>

<span data-ttu-id="67857-130">Ao trabalhar com o Azure Media Services, um dos cenários mais comuns de saudação está entregando vídeo por meio de streaming de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="67857-130">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="67857-131">Serviços de mídia fornecem empacotamento dinâmico, que permite que você toodeliver sua taxa de bits adaptável MP4 codificados conteúdo de streaming formatos suportados pelo Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, sem a necessidade de toostore pacote predefinido versões de cada um desses formatos de fluxo contínuo.</span><span class="sxs-lookup"><span data-stu-id="67857-131">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="67857-132">Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado.</span><span class="sxs-lookup"><span data-stu-id="67857-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="67857-133">toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado.</span><span class="sxs-lookup"><span data-stu-id="67857-133">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="67857-134">toostart Olá ponto de extremidade de streaming, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="67857-134">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="67857-135">Faça logon em Olá [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="67857-135">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="67857-136">Na janela de configurações de saudação, clique em pontos de extremidade de Streaming.</span><span class="sxs-lookup"><span data-stu-id="67857-136">In hello Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="67857-137">Clique em padrão Olá ponto de extremidade de streaming.</span><span class="sxs-lookup"><span data-stu-id="67857-137">Click hello default streaming endpoint.</span></span>

    <span data-ttu-id="67857-138">saudação padrão detalhes do ponto de EXTREMIDADE de STREAMING de janela é exibida.</span><span class="sxs-lookup"><span data-stu-id="67857-138">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="67857-139">Clique o ícone de início de saudação.</span><span class="sxs-lookup"><span data-stu-id="67857-139">Click hello Start icon.</span></span>
5. <span data-ttu-id="67857-140">Clique em Olá toosave de botão de salvar suas alterações.</span><span class="sxs-lookup"><span data-stu-id="67857-140">Click hello Save button toosave your changes.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="67857-141">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="67857-141">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="67857-142">Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="67857-142">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="67857-143">Crie uma nova pasta (pasta pode estar em qualquer lugar no disco local) e copie um arquivo. mp4 que você deseja tooencode e fluxo ou download progressivo.</span><span class="sxs-lookup"><span data-stu-id="67857-143">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want tooencode and stream or progressively download.</span></span> <span data-ttu-id="67857-144">Neste exemplo, o caminho de "C:\VideoFiles" hello é usado.</span><span class="sxs-lookup"><span data-stu-id="67857-144">In this example, hello "C:\VideoFiles" path is used.</span></span>

## <a name="connect-toohello-media-services-account"></a><span data-ttu-id="67857-145">Conecte-se a conta de serviços de mídia toohello</span><span class="sxs-lookup"><span data-stu-id="67857-145">Connect toohello Media Services account</span></span>

<span data-ttu-id="67857-146">Ao usar os serviços de mídia com .NET, você deve usar o hello **CloudMediaContext** classe para a maioria dos serviços de mídia tarefas de programação: conectar-se a conta de serviços tooMedia; criar, atualizar, acessar e excluir o seguinte Olá objetos: ativos, arquivos de ativos, trabalhos, políticas de acesso, os localizadores, etc.</span><span class="sxs-lookup"><span data-stu-id="67857-146">When using Media Services with .NET, you must use hello **CloudMediaContext** class for most Media Services programming tasks: connecting tooMedia Services account; creating, updating, accessing, and deleting hello following objects: assets, asset files, jobs, access policies, locators, etc.</span></span>

<span data-ttu-id="67857-147">Substitua a classe de programa padrão Olá com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="67857-147">Overwrite hello default Program class with hello following code.</span></span> <span data-ttu-id="67857-148">Olá código demonstra como conexão de saudação tooread os valores do arquivo App. config de saudação e Olá toocreate **CloudMediaContext** objeto na ordem tooconnect tooMedia de serviços.</span><span class="sxs-lookup"><span data-stu-id="67857-148">hello code demonstrates how tooread hello connection values from hello App.config file and how toocreate hello **CloudMediaContext** object in order tooconnect tooMedia Services.</span></span> <span data-ttu-id="67857-149">Para obter mais informações, consulte [conexão toohello API de serviços de mídia](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="67857-149">For more information, see [connecting toohello Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

<span data-ttu-id="67857-150">Certifique-se de que tooupdate Olá arquivo nome e caminho toowhere que tiver seu arquivo de mídia.</span><span class="sxs-lookup"><span data-stu-id="67857-150">Make sure tooupdate hello file name and path toowhere you have your media file.</span></span>

<span data-ttu-id="67857-151">Olá **principal** função chama métodos que serão definidos mais nesta seção.</span><span class="sxs-lookup"><span data-stu-id="67857-151">hello **Main** function calls methods that will be defined further in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="67857-152">Você obterá erros de compilação até que você adicione definições para todas as funções hello.</span><span class="sxs-lookup"><span data-stu-id="67857-152">You will be getting compilation errors until you add definitions for all hello functions.</span></span>

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

## <a name="create-a-new-asset-and-upload-a-video-file"></a><span data-ttu-id="67857-153">Criar um novo ativo e carregar um arquivo de vídeo</span><span class="sxs-lookup"><span data-stu-id="67857-153">Create a new asset and upload a video file</span></span>

<span data-ttu-id="67857-154">No Serviços de Mídia, você carrega (ou ingere) seus arquivos digitais em um ativo.</span><span class="sxs-lookup"><span data-stu-id="67857-154">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="67857-155">Olá **ativo** entidade pode conter vídeo, áudio, imagens, coleções de miniaturas, texto faixas e legenda codificada arquivos (e Olá metadados sobre esses arquivos.)  Depois que forem carregados arquivos hello, seu conteúdo é armazenado com segurança na nuvem de saudação para processamento adicional e streaming.</span><span class="sxs-lookup"><span data-stu-id="67857-155">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and hello metadata about these files.)  Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span> <span data-ttu-id="67857-156">Olá arquivos no ativo de saudação são chamados **arquivos de ativo**.</span><span class="sxs-lookup"><span data-stu-id="67857-156">hello files in hello asset are called **Asset Files**.</span></span>

<span data-ttu-id="67857-157">Olá **UploadFile** definido abaixo chamadas de método **CreateFromFile** (definido em extensões do SDK do .NET).</span><span class="sxs-lookup"><span data-stu-id="67857-157">hello **UploadFile** method defined below calls **CreateFromFile** (defined in .NET SDK Extensions).</span></span> <span data-ttu-id="67857-158">**CreateFromFile** cria um novo ativo em qual Olá o arquivo de origem especificado é carregado.</span><span class="sxs-lookup"><span data-stu-id="67857-158">**CreateFromFile** creates a new asset into which hello specified source file is uploaded.</span></span>

<span data-ttu-id="67857-159">Olá **CreateFromFile** leva **AssetCreationOptions** que permite que você especifique uma saudação seguindo as opções de criação de ativo:</span><span class="sxs-lookup"><span data-stu-id="67857-159">hello **CreateFromFile** method takes **AssetCreationOptions** which lets you specify one of hello following asset creation options:</span></span>

* <span data-ttu-id="67857-160">**None** - nenhuma criptografia é usada.</span><span class="sxs-lookup"><span data-stu-id="67857-160">**None** - No encryption is used.</span></span> <span data-ttu-id="67857-161">Este é o valor padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="67857-161">This is hello default value.</span></span> <span data-ttu-id="67857-162">Observe que, ao usar essa opção, seu conteúdo não será protegido quando estiver em trânsito ou em repouso no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="67857-162">Note that when using this option, your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="67857-163">Se você planejar toodeliver um MP4 usando o download progressivo, use essa opção.</span><span class="sxs-lookup"><span data-stu-id="67857-163">If you plan toodeliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="67857-164">**StorageEncrypted** -Use essa opção tooencrypt o conteúdo limpo localmente usando a criptografia de-256 bits (AES padrão), que carrega tooAzure armazenamento onde ele está armazenado criptografado em repouso.</span><span class="sxs-lookup"><span data-stu-id="67857-164">**StorageEncrypted** - Use this option tooencrypt your clear content locally using Advanced Encryption Standard (AES)-256 bit encryption, which then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="67857-165">Ativos protegidos pela criptografia de armazenamento são descriptografados automaticamente e posicionados em um tooencoding anterior do sistema de arquivos criptografados e, opcionalmente, criptografada novamente toouploading anterior como um novo ativo de saída.</span><span class="sxs-lookup"><span data-stu-id="67857-165">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="67857-166">caso de uso primário Olá para criptografia de armazenamento é quando você deseja toosecure seus arquivos de mídia de entrada de alta qualidade com criptografia forte em rest no disco.</span><span class="sxs-lookup"><span data-stu-id="67857-166">hello primary use case for Storage Encryption is when you want toosecure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="67857-167">**CommonEncryptionProtected** — use esta opção se você estiver carregando conteúdo que já foi criptografado e protegido com criptografia comum ou DRM PlayReady (por exemplo, Smooth Streaming protegido com DRM PlayReady).</span><span class="sxs-lookup"><span data-stu-id="67857-167">**CommonEncryptionProtected** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="67857-168">**EnvelopeEncryptionProtected** – use esta opção se você estiver carregando HLS criptografado com AES.</span><span class="sxs-lookup"><span data-stu-id="67857-168">**EnvelopeEncryptionProtected** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="67857-169">Observe que arquivos Olá devem ter sido codificados e criptografados pelo Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="67857-169">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>

<span data-ttu-id="67857-170">Olá **CreateFromFile** método também permite especificar um retorno de chamada em andamento do upload ordem tooreport saudação do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="67857-170">hello **CreateFromFile** method also lets you specify a callback in order tooreport hello upload progress of hello file.</span></span>

<span data-ttu-id="67857-171">Saudação de exemplo a seguir, especificamos **nenhum** para opções de ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="67857-171">In hello following example, we specify **None** for hello asset options.</span></span>

<span data-ttu-id="67857-172">Adicione Olá classe do método toohello programa a seguir.</span><span class="sxs-lookup"><span data-stu-id="67857-172">Add hello following method toohello Program class.</span></span>

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


## <a name="encode-hello-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a><span data-ttu-id="67857-173">Codificar o arquivo de origem de saudação em um conjunto de arquivos MP4 com taxa de bits adaptável</span><span class="sxs-lookup"><span data-stu-id="67857-173">Encode hello source file into a set of adaptive bitrate MP4 files</span></span>
<span data-ttu-id="67857-174">Após a ingestão de ativos nos serviços de mídia, a mídia pode ser codificado, transmultiplexar, marca d'água e assim por diante, antes de entregar tooclients.</span><span class="sxs-lookup"><span data-stu-id="67857-174">After ingesting assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered tooclients.</span></span> <span data-ttu-id="67857-175">Essas atividades são agendadas e executadas várias em segundo plano função instâncias tooensure alto desempenho e disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="67857-175">These activities are scheduled and run against multiple background role instances tooensure high performance and availability.</span></span> <span data-ttu-id="67857-176">Essas atividades são chamadas de trabalhos, e cada trabalho é composto de tarefas atômicas que Olá real trabalho no arquivo de ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="67857-176">These activities are called Jobs, and each Job is composed of atomic Tasks that do hello actual work on hello Asset file.</span></span>

<span data-ttu-id="67857-177">Como foi mencionado anteriormente, ao trabalhar com os serviços de mídia do Azure, um dos cenários mais comuns de saudação está entregando tooyour clientes de streaming de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="67857-177">As was mentioned earlier, when working with Azure Media Services, one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="67857-178">Serviços de mídia pode empacotar dinamicamente um conjunto de arquivos MP4 com taxa de bits adaptável em uma saudação formatos a seguir: HTTP Live Streaming (HLS), Smooth Streaming e MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="67857-178">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of hello following formats: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span>

<span data-ttu-id="67857-179">tootake proveito do empacotamento dinâmico, você precisa tooencode ou transcodificar o arquivo de mezanino (origem) em um conjunto de arquivos MP4 de taxa de bits adaptável ou arquivos de Smooth Streaming de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="67857-179">tootake advantage of dynamic packaging, you need tooencode or transcode your mezzanine (source) file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>  

<span data-ttu-id="67857-180">saudação de código a seguir mostra como toosubmit uma codificação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="67857-180">hello following code shows how toosubmit an encoding job.</span></span> <span data-ttu-id="67857-181">trabalho Hello contém uma tarefa que especifica o arquivo de mezanino Olá tootranscode em um conjunto de MP4s de taxa de bits adaptável usando **codificador de mídia padrão**.</span><span class="sxs-lookup"><span data-stu-id="67857-181">hello job contains one task that specifies tootranscode hello mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="67857-182">código de saudação envia trabalho hello e aguarda até que ela seja concluída.</span><span class="sxs-lookup"><span data-stu-id="67857-182">hello code submits hello job and waits until it is completed.</span></span>

<span data-ttu-id="67857-183">Após a conclusão do trabalho hello, deve ser capaz de toostream seu ativo ou download progressivo de arquivos MP4 que foram criados como resultado de transcodificação.</span><span class="sxs-lookup"><span data-stu-id="67857-183">Once hello job is completed, you would be able toostream your asset or progressively download MP4 files that were created as a result of transcoding.</span></span>

<span data-ttu-id="67857-184">Adicione Olá classe do método toohello programa a seguir.</span><span class="sxs-lookup"><span data-stu-id="67857-184">Add hello following method toohello Program class.</span></span>

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

## <a name="publish-hello-asset-and-get-urls-for-streaming-and-progressive-download"></a><span data-ttu-id="67857-185">Publicar Olá ativo e obter URLs de download progressivo e streaming</span><span class="sxs-lookup"><span data-stu-id="67857-185">Publish hello asset and get URLs for streaming and progressive download</span></span>

<span data-ttu-id="67857-186">toostream ou baixar um ativo, você primeiro precisa muito "Publicar"-lo criando um localizador.</span><span class="sxs-lookup"><span data-stu-id="67857-186">toostream or download an asset, you first need too"publish" it by creating a locator.</span></span> <span data-ttu-id="67857-187">Os localizadores fornecem acesso toofiles contidos em Olá ativo.</span><span class="sxs-lookup"><span data-stu-id="67857-187">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="67857-188">Serviços de mídia oferece suporte a dois tipos de localizadores: OnDemandOrigin localizadores, mídia toostream usado (por exemplo, MPEG DASH, HLS ou Smooth Streaming) e localizadores da assinatura de acesso (SAS), usados arquivos de mídia toodownload (para obter mais informações sobre consulte localizadores SAS [isso](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span><span class="sxs-lookup"><span data-stu-id="67857-188">Media Services supports two types of locators: OnDemandOrigin locators, used toostream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used toodownload media files (for more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span></span>

### <a name="some-details-about-url-formats"></a><span data-ttu-id="67857-189">Alguns detalhes sobre os formatos de URL</span><span class="sxs-lookup"><span data-stu-id="67857-189">Some details about URL formats</span></span>

<span data-ttu-id="67857-190">Depois de criar localizadores hello, você pode criar URLs Olá que deve ser usado toostream ou baixar os arquivos.</span><span class="sxs-lookup"><span data-stu-id="67857-190">After you create hello locators, you can build hello URLs that would be used toostream or download your files.</span></span> <span data-ttu-id="67857-191">exemplo Hello neste tutorial mostrará as URLs que você pode colar em navegadores apropriados.</span><span class="sxs-lookup"><span data-stu-id="67857-191">hello sample in this tutorial will output URLs that you can paste in appropriate browsers.</span></span> <span data-ttu-id="67857-192">Esta seção fornece apenas breves exemplos da aparência de formatos diferentes.</span><span class="sxs-lookup"><span data-stu-id="67857-192">This section just gives short examples of what different formats look like.</span></span>

#### <a name="a-streaming-url-for-mpeg-dash-has-hello-following-format"></a><span data-ttu-id="67857-193">Uma URL de streaming MPEG DASH tem Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="67857-193">A streaming URL for MPEG DASH has hello following format:</span></span>

<span data-ttu-id="67857-194">{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span><span class="sxs-lookup"><span data-stu-id="67857-194">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span></span>

#### <a name="a-streaming-url-for-hls-has-hello-following-format"></a><span data-ttu-id="67857-195">Uma URL de streaming para HLS tem Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="67857-195">A streaming URL for HLS has hello following format:</span></span>

<span data-ttu-id="67857-196">{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span><span class="sxs-lookup"><span data-stu-id="67857-196">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span></span>

#### <a name="a-streaming-url-for-smooth-streaming-has-hello-following-format"></a><span data-ttu-id="67857-197">Uma URL de streaming para Smooth Streaming tem Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="67857-197">A streaming URL for Smooth Streaming has hello following format:</span></span>

<span data-ttu-id="67857-198">{nome do ponto de extremidade de streaming - nome de conta do dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arqui}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="67857-198">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>


#### <a name="a-sas-url-used-toodownload-files-has-hello-following-format"></a><span data-ttu-id="67857-199">Arquivos de toodownload uma URL SAS usada tem Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="67857-199">A SAS URL used toodownload files has hello following format:</span></span>

<span data-ttu-id="67857-200">{nome do contêiner de blob}/{nome do ativo}/{nome do arquivo}/{assinatura SAS}</span><span class="sxs-lookup"><span data-stu-id="67857-200">{blob container name}/{asset name}/{file name}/{SAS signature}</span></span>

<span data-ttu-id="67857-201">Extensões do SDK do Media Services .NET fornecem métodos auxiliares conveniente que retornam formatada URLs para Olá publicado ativo.</span><span class="sxs-lookup"><span data-stu-id="67857-201">Media Services .NET SDK extensions provide convenient helper methods that return formatted URLs for hello published asset.</span></span>

<span data-ttu-id="67857-202">Olá, código a seguir usa os localizadores toocreate de extensões do SDK do .NET e URLs de download progressivo e streaming tooget.</span><span class="sxs-lookup"><span data-stu-id="67857-202">hello following code uses .NET SDK Extensions toocreate locators and tooget streaming and progressive download URLs.</span></span> <span data-ttu-id="67857-203">código de saudação também mostra como toodownload arquivos de pasta local tooa.</span><span class="sxs-lookup"><span data-stu-id="67857-203">hello code also shows how toodownload files tooa local folder.</span></span>

<span data-ttu-id="67857-204">Adicione Olá classe do método toohello programa a seguir.</span><span class="sxs-lookup"><span data-stu-id="67857-204">Add hello following method toohello Program class.</span></span>

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

## <a name="test-by-playing-your-content"></a><span data-ttu-id="67857-205">Testar ao reproduzir o conteúdo</span><span class="sxs-lookup"><span data-stu-id="67857-205">Test by playing your content</span></span>

<span data-ttu-id="67857-206">Quando você executar o programa de saudação definido na seção anterior hello, Olá URLs a seguir toohello semelhante será exibida na janela de console hello.</span><span class="sxs-lookup"><span data-stu-id="67857-206">Once you run hello program defined in hello previous section, hello URLs similar toohello following will be displayed in hello console window.</span></span>

<span data-ttu-id="67857-207">URLs de streaming adaptáveis:</span><span class="sxs-lookup"><span data-stu-id="67857-207">Adaptive streaming URLs:</span></span>

<span data-ttu-id="67857-208">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="67857-208">Smooth Streaming</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="67857-209">HLS</span><span class="sxs-lookup"><span data-stu-id="67857-209">HLS</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="67857-210">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="67857-210">MPEG DASH</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

<span data-ttu-id="67857-211">URLs de download progressivo (áudio e vídeo).</span><span class="sxs-lookup"><span data-stu-id="67857-211">Progressive download URLs (audio and video).</span></span>

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


<span data-ttu-id="67857-212">toostream seu vídeo, cole a URL na caixa de texto Olá URL no hello [Player de serviços de mídia do Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="67857-212">toostream your video, paste your URL in hello URL textbox in hello [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="67857-213">tootest progressivo baixar, cole uma URL em um navegador (por exemplo, Internet Explorer, Chrome ou Safari).</span><span class="sxs-lookup"><span data-stu-id="67857-213">tootest progressive download, paste a URL into a browser (for example, Internet Explorer, Chrome, or Safari).</span></span>

<span data-ttu-id="67857-214">Para obter mais informações, consulte Olá seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="67857-214">For more information, see hello following topics:</span></span>

- [<span data-ttu-id="67857-215">Reprodução de seu conteúdo com players existentes</span><span class="sxs-lookup"><span data-stu-id="67857-215">Playing your content with existing players</span></span>](media-services-playback-content-with-existing-players.md)
- [<span data-ttu-id="67857-216">Desenvolver aplicativos de player de vídeo</span><span class="sxs-lookup"><span data-stu-id="67857-216">Develop video player applications</span></span>](media-services-develop-video-players.md)
- [<span data-ttu-id="67857-217">Inserindo um vídeo de streaming adaptável MPEG-DASH em um aplicativo HTML5 com DASH.js</span><span class="sxs-lookup"><span data-stu-id="67857-217">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a><span data-ttu-id="67857-218">Baixar exemplo</span><span class="sxs-lookup"><span data-stu-id="67857-218">Download sample</span></span>
<span data-ttu-id="67857-219">exemplo de código a seguir Hello contém código Olá criado neste tutorial: [exemplo](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="67857-219">hello following code sample contains hello code that you created in this tutorial: [sample](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="67857-220">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="67857-220">Next Steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="67857-221">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="67857-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
