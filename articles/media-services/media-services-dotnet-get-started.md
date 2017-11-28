---
title: "Introdução ao fornecimento de conteúdo sob demanda usando o .NET | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de implementação de um aplicativo de fornecimento de conteúdo sob demanda com os Serviços de Mídia do Azure usando .NET."
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
ms.openlocfilehash: f0be787ba1ccee067fb1d7e6a6554be32f886089
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a><span data-ttu-id="ddd0e-103">Introdução ao fornecimento de conteúdo sob demanda usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="ddd0e-103">Get started with delivering content on demand using .NET SDK</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="ddd0e-104">Este tutorial o orienta ao longo das etapas de implementação de um serviço básico de fornecimento de conteúdo de VoD (Vídeo sob Demanda) com o aplicativo AMS (Serviços de Mídia do Azure) usando o SDK .NET dos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-104">This tutorial walks you through the steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using the Azure Media Services .NET SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddd0e-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ddd0e-105">Prerequisites</span></span>

<span data-ttu-id="ddd0e-106">Os itens a seguir são necessários para concluir o tutorial:</span><span class="sxs-lookup"><span data-stu-id="ddd0e-106">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="ddd0e-107">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-107">An Azure account.</span></span> <span data-ttu-id="ddd0e-108">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ddd0e-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ddd0e-109">Uma conta dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-109">A Media Services account.</span></span> <span data-ttu-id="ddd0e-110">Para criar uma conta de Serviços de Mídia, consulte [Como criar uma conta de Serviços de Mídia](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="ddd0e-110">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="ddd0e-111">.NET Framework 4.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-111">.NET Framework 4.0 or later.</span></span>
* <span data-ttu-id="ddd0e-112">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-112">Visual Studio.</span></span>

<span data-ttu-id="ddd0e-113">Este tutorial inclui as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="ddd0e-113">This tutorial includes the following tasks:</span></span>

1. <span data-ttu-id="ddd0e-114">Iniciar pontos de extremidade de streaming (usando o portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="ddd0e-114">Start streaming endpoint (using the Azure portal).</span></span>
2. <span data-ttu-id="ddd0e-115">Criar e configurar um projeto do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-115">Create and configure a Visual Studio project.</span></span>
3. <span data-ttu-id="ddd0e-116">Conectar-se à conta dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-116">Connect to the Media Services account.</span></span>
2. <span data-ttu-id="ddd0e-117">Carregar um arquivo de vídeo.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-117">Upload a video file.</span></span>
3. <span data-ttu-id="ddd0e-118">Codificar o arquivo de origem em um conjunto de arquivos MP4 com taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-118">Encode the source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="ddd0e-119">Publicar o ativo e obter URLs de download progressivo e streaming.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-119">Publish the asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="ddd0e-120">Reproduzir o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-120">Play your content.</span></span>

## <a name="overview"></a><span data-ttu-id="ddd0e-121">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ddd0e-121">Overview</span></span>
<span data-ttu-id="ddd0e-122">Este tutorial orienta você pelas etapas de implementação de um aplicativo de entrega de conteúdo de vídeo sob demanda (VoD) com os Serviços de Mídia do Azure (AMS) para .NET.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-122">This tutorial walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) SDK for .NET.</span></span>

<span data-ttu-id="ddd0e-123">O tutorial apresenta o fluxo de trabalho básico dos Serviços de Mídia e os objetos e as tarefas de programação mais comuns necessárias para o desenvolvimento dos Serviços de Mídia do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-123">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="ddd0e-124">No final do tutorial, você poderá transmitir ou baixar progressivamente um arquivo de mídia de exemplo que você carregou, codificou e baixou.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-124">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

### <a name="ams-model"></a><span data-ttu-id="ddd0e-125">Modelo do AMS</span><span class="sxs-lookup"><span data-stu-id="ddd0e-125">AMS model</span></span>

<span data-ttu-id="ddd0e-126">A imagem a seguir mostra alguns dos objetos mais usados ao desenvolver aplicativos VoD em relação ao modelo de OData de Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-126">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span></span>

<span data-ttu-id="ddd0e-127">Clique na imagem para exibi-la em tamanho normal.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-127">Click the image to view it full size.</span></span>  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="ddd0e-128">Você pode exibir todo o modelo [aqui](https://media.windows.net/API/$metadata?api-version=2.15).</span><span class="sxs-lookup"><span data-stu-id="ddd0e-128">You can view the whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="start-streaming-endpoints-using-the-azure-portal"></a><span data-ttu-id="ddd0e-129">Iniciar pontos de extremidade de streaming usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ddd0e-129">Start streaming endpoints using the Azure portal</span></span>

<span data-ttu-id="ddd0e-130">Ao trabalhar com os Serviços de Mídia do Azure, um dos cenários mais comuns o fornecimento de vídeo via streaming de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-130">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="ddd0e-131">Os Serviços de Mídia fornecem um empacotamento dinâmico que permite a você enviar o conteúdo codificado para MP4 da taxa de bits adaptável nos formatos de transmissão suportados pelos Serviços de Mídia (MPEG DASH, HLS, Smooth Streaming) just-in-time, sem ter que armazenar as versões recolocadas de cada um dos formatos de transmissão.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-131">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="ddd0e-132">Quando sua conta AMS é criada, um ponto de extremidade de streaming **padrão** é adicionado à sua conta em estado **Parado**.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-132">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="ddd0e-133">Para iniciar seu conteúdo de streaming e tirar proveito do empacotamento dinâmico e da criptografia dinâmica, o ponto de extremidade de streaming do qual você deseja transmitir o conteúdo deve estar em estado **Executando**.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-133">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="ddd0e-134">Para iniciar o ponto de extremidade de streaming, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ddd0e-134">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="ddd0e-135">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ddd0e-135">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ddd0e-136">Na janela Configurações, clique em Pontos de extremidade de streaming.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-136">In the Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="ddd0e-137">Clique no ponto de extremidade de streaming padrão.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-137">Click the default streaming endpoint.</span></span>

    <span data-ttu-id="ddd0e-138">A janela DETALHES DO PONTO DE EXTREMIDADE DE STREAMING PADRÃO é exibida.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-138">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="ddd0e-139">Clique no ícone Iniciar.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-139">Click the Start icon.</span></span>
5. <span data-ttu-id="ddd0e-140">Clique no botão Salvar para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-140">Click the Save button to save your changes.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="ddd0e-141">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ddd0e-141">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="ddd0e-142">Configure seu ambiente de desenvolvimento e preencha o arquivo de configuração app.config com as informações de conexão, conforme descrito em [Desenvolvimento de Serviços de Mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="ddd0e-142">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="ddd0e-143">Crie uma nova pasta (a pasta pode estar em qualquer lugar na unidade local) e copie um arquivo .mp4 que você deseja codificar e transmitir ou baixar progressivamente.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-143">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want to encode and stream or progressively download.</span></span> <span data-ttu-id="ddd0e-144">Este exemplo usa o caminho "C:\VideoFiles".</span><span class="sxs-lookup"><span data-stu-id="ddd0e-144">In this example, the "C:\VideoFiles" path is used.</span></span>

## <a name="connect-to-the-media-services-account"></a><span data-ttu-id="ddd0e-145">Conectar-se à conta dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="ddd0e-145">Connect to the Media Services account</span></span>

<span data-ttu-id="ddd0e-146">Ao usar os serviços de mídia com o .NET, você deve usar a classe **CloudMediaContext** para a maioria das tarefas de programação dos Serviços de Mídia: conectar-se à conta de Serviços de Mídia; criar, atualizar, acessar e excluir os seguintes objetos: ativos, arquivos de ativos, trabalhos, políticas de acesso, localizadores, etc.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-146">When using Media Services with .NET, you must use the **CloudMediaContext** class for most Media Services programming tasks: connecting to Media Services account; creating, updating, accessing, and deleting the following objects: assets, asset files, jobs, access policies, locators, etc.</span></span>

<span data-ttu-id="ddd0e-147">Substitua a classe Program padrão pelo código a seguir.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-147">Overwrite the default Program class with the following code.</span></span> <span data-ttu-id="ddd0e-148">O código demonstra como ler os valores de conexão por meio do arquivo App.config e como criar o objeto **CloudMediaContext** para poder se conectar aos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-148">The code demonstrates how to read the connection values from the App.config file and how to create the **CloudMediaContext** object in order to connect to Media Services.</span></span> <span data-ttu-id="ddd0e-149">Para saber mais, consulte [Conectar-se à API dos Serviços de Mídia](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="ddd0e-149">For more information, see [connecting to the Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

<span data-ttu-id="ddd0e-150">Atualize o nome do arquivo e o caminho onde está o arquivo de mídia.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-150">Make sure to update the file name and path to where you have your media file.</span></span>

<span data-ttu-id="ddd0e-151">A função **Main** chama métodos que serão definidos posteriormente nesta seção.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-151">The **Main** function calls methods that will be defined further in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="ddd0e-152">Você receberá erros de compilação até que adicione definições a todas as funções.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-152">You will be getting compilation errors until you add definitions for all the functions.</span></span>

    class Program
    {
        // Read values from the App.config file.
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

            // Add calls to methods defined in this section.
            // Make sure to update the file name and path to where you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse the XML error message in the Media Services response and create a new
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

## <a name="create-a-new-asset-and-upload-a-video-file"></a><span data-ttu-id="ddd0e-153">Criar um novo ativo e carregar um arquivo de vídeo</span><span class="sxs-lookup"><span data-stu-id="ddd0e-153">Create a new asset and upload a video file</span></span>

<span data-ttu-id="ddd0e-154">No Serviços de Mídia, você carrega (ou ingere) seus arquivos digitais em um ativo.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-154">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="ddd0e-155">A entidade **Asset** pode conter vídeo, áudio, imagens, coleções de miniaturas, sequências de texto e arquivos de legendas (e os metadados sobre esses arquivos).  Depois que os arquivos são carregados, o conteúdo é armazenado com segurança na nuvem para processamento adicional e transmissão.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-155">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and the metadata about these files.)  Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span> <span data-ttu-id="ddd0e-156">Os arquivos no ativo são chamados **Arquivos de Ativo**.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-156">The files in the asset are called **Asset Files**.</span></span>

<span data-ttu-id="ddd0e-157">O método **UploadFile** definido abaixo chama **CreateFromFile** (definido em extensões do SDK .NET).</span><span class="sxs-lookup"><span data-stu-id="ddd0e-157">The **UploadFile** method defined below calls **CreateFromFile** (defined in .NET SDK Extensions).</span></span> <span data-ttu-id="ddd0e-158">**CreateFromFile** cria um novo ativo no qual o arquivo de origem especificado é carregado.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-158">**CreateFromFile** creates a new asset into which the specified source file is uploaded.</span></span>

<span data-ttu-id="ddd0e-159">O método **CreateFromFile** contém **AssetCreationOptions**, que permite especificar uma das seguintes opções de criação de ativos:</span><span class="sxs-lookup"><span data-stu-id="ddd0e-159">The **CreateFromFile** method takes **AssetCreationOptions** which lets you specify one of the following asset creation options:</span></span>

* <span data-ttu-id="ddd0e-160">**None** - nenhuma criptografia é usada.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-160">**None** - No encryption is used.</span></span> <span data-ttu-id="ddd0e-161">Esse é o valor padrão.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-161">This is the default value.</span></span> <span data-ttu-id="ddd0e-162">Observe que, ao usar essa opção, seu conteúdo não será protegido quando estiver em trânsito ou em repouso no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-162">Note that when using this option, your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="ddd0e-163">Se você pretende enviar um MP4 usando o download progressivo, use essa opção.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-163">If you plan to deliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="ddd0e-164">**StorageEncrypted** – use essa opção para criptografar seu conteúdo limpo localmente usando a criptografia AES de 256 bits e, em seguida, carregá-lo para o armazenamento do Azure, onde ele é armazenado, criptografado em repouso.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-164">**StorageEncrypted** - Use this option to encrypt your clear content locally using Advanced Encryption Standard (AES)-256 bit encryption, which then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="ddd0e-165">Ativos protegidos pela criptografia de armazenamento são descriptografados automaticamente e posicionados em um sistema de arquivos criptografado antes da codificação, então opcionalmente criptografados novamente antes do carregamento como um novo ativo de saída.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-165">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="ddd0e-166">O caso de uso primário para criptografia de armazenamento é quando você deseja proteger seus arquivos de mídia de entrada de alta qualidade com criptografia forte em repouso no disco.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-166">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="ddd0e-167">**CommonEncryptionProtected** — use esta opção se você estiver carregando conteúdo que já foi criptografado e protegido com criptografia comum ou DRM PlayReady (por exemplo, Smooth Streaming protegido com DRM PlayReady).</span><span class="sxs-lookup"><span data-stu-id="ddd0e-167">**CommonEncryptionProtected** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="ddd0e-168">**EnvelopeEncryptionProtected** – use esta opção se você estiver carregando HLS criptografado com AES.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-168">**EnvelopeEncryptionProtected** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="ddd0e-169">Observe que os arquivos devem ter sido codificados e criptografados pelo Gerenciador de Transformação.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-169">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>

<span data-ttu-id="ddd0e-170">O método **CreateFromFile** também permite especificar um retorno de chamada para relatar o progresso do upload do arquivo.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-170">The **CreateFromFile** method also lets you specify a callback in order to report the upload progress of the file.</span></span>

<span data-ttu-id="ddd0e-171">No exemplo a seguir, podemos especificar **Nenhum** para as opções de ativo.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-171">In the following example, we specify **None** for the asset options.</span></span>

<span data-ttu-id="ddd0e-172">Adicionar o método a seguir à classe do programa.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-172">Add the following method to the Program class.</span></span>

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


## <a name="encode-the-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a><span data-ttu-id="ddd0e-173">Codificar o arquivo de origem em um conjunto de arquivos MP4 com taxa de bits adaptável</span><span class="sxs-lookup"><span data-stu-id="ddd0e-173">Encode the source file into a set of adaptive bitrate MP4 files</span></span>
<span data-ttu-id="ddd0e-174">Após a inserção de Ativos nos Serviços de Mídia, a mídia poderá ser codificada, transmultiplexada, marcada com marca d'água e assim por diante antes que seja entregue aos clientes.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-174">After ingesting assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span></span> <span data-ttu-id="ddd0e-175">Essas atividades são agendadas e executadas em contraste com várias instâncias de função de plano de fundo para garantir a disponibilidade e desempenho elevados.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-175">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span></span> <span data-ttu-id="ddd0e-176">Essas atividades são chamadas de Trabalhos, e cada Trabalho é composto por Tarefas atômicas, que fazem o trabalho real no arquivo do Ativo.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-176">These activities are called Jobs, and each Job is composed of atomic Tasks that do the actual work on the Asset file.</span></span>

<span data-ttu-id="ddd0e-177">Como mencionado anteriormente, ao trabalhar com os Serviços de Mídia do Azure, um dos cenários mais comuns é fornecer streaming com uma taxa de bits adaptável aos clientes.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-177">As was mentioned earlier, when working with Azure Media Services, one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="ddd0e-178">Os serviços de mídia podem empacotar dinamicamente um conjunto de arquivos MP4 com taxas de bit adaptável: HTTP Live Streaming (HLS), Smooth Streaming e MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-178">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span>

<span data-ttu-id="ddd0e-179">Para tirar proveito do empacotamento dinâmico, você precisa codificar ou transcodificar seu arquivo mezanino (fonte) em um conjunto de arquivos MP4 de taxa de bits adaptável ou arquivos Smooth Streaming de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-179">To take advantage of dynamic packaging, you need to encode or transcode your mezzanine (source) file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>  

<span data-ttu-id="ddd0e-180">O código a seguir mostra como enviar um trabalho de codificação.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-180">The following code shows how to submit an encoding job.</span></span> <span data-ttu-id="ddd0e-181">O trabalho contém uma tarefa que determina a transcodificação do arquivo de mezanino em um conjunto de MP4s de taxa de bits adaptável usando o **Codificador de Mídia Standard**.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-181">The job contains one task that specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="ddd0e-182">O código envia o trabalho e aguarda até que ele seja concluído.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-182">The code submits the job and waits until it is completed.</span></span>

<span data-ttu-id="ddd0e-183">Depois que o trabalho for concluído, você poderá transmitir seu ativo ou baixar progressivamente arquivos MP4 criados como resultado de transcodificação.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-183">Once the job is completed, you would be able to stream your asset or progressively download MP4 files that were created as a result of transcoding.</span></span>

<span data-ttu-id="ddd0e-184">Adicionar o método a seguir à classe do programa.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-184">Add the following method to the Program class.</span></span>

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task to transcode the specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit the job and wait until it is completed.
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

## <a name="publish-the-asset-and-get-urls-for-streaming-and-progressive-download"></a><span data-ttu-id="ddd0e-185">Publicar o ativo e obter URLs para streaming e download progressivo</span><span class="sxs-lookup"><span data-stu-id="ddd0e-185">Publish the asset and get URLs for streaming and progressive download</span></span>

<span data-ttu-id="ddd0e-186">Para transmitir ou baixar um ativo, primeiro você precisa "publicá-lo" criando um localizador.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-186">To stream or download an asset, you first need to "publish" it by creating a locator.</span></span> <span data-ttu-id="ddd0e-187">Os localizadores fornecem acesso aos arquivos contidos no ativo.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-187">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="ddd0e-188">Os Serviços de Mídia oferecem suporte a dois tipos de localizador: OnDemandOrigin, usados para transmitir mídia por streaming (por exemplo, MPEG DASH, HLS ou Smooth Streaming) e SAS (Assinatura de Acesso), usados para baixar arquivos de mídia (Para saber mais sobre localizadores SAS, confira [este](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span><span class="sxs-lookup"><span data-stu-id="ddd0e-188">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files (for more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span></span>

### <a name="some-details-about-url-formats"></a><span data-ttu-id="ddd0e-189">Alguns detalhes sobre os formatos de URL</span><span class="sxs-lookup"><span data-stu-id="ddd0e-189">Some details about URL formats</span></span>

<span data-ttu-id="ddd0e-190">Depois de criar os localizadores, você pode criar as URLs que seriam usadas para transmitir ou baixar os arquivos.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-190">After you create the locators, you can build the URLs that would be used to stream or download your files.</span></span> <span data-ttu-id="ddd0e-191">O exemplo neste tutorial produzirá URLs que podem ser coladas em navegadores apropriados.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-191">The sample in this tutorial will output URLs that you can paste in appropriate browsers.</span></span> <span data-ttu-id="ddd0e-192">Esta seção fornece apenas breves exemplos da aparência de formatos diferentes.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-192">This section just gives short examples of what different formats look like.</span></span>

#### <a name="a-streaming-url-for-mpeg-dash-has-the-following-format"></a><span data-ttu-id="ddd0e-193">Uma URL de streaming para MPEG DASH tem o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="ddd0e-193">A streaming URL for MPEG DASH has the following format:</span></span>

<span data-ttu-id="ddd0e-194">{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span><span class="sxs-lookup"><span data-stu-id="ddd0e-194">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span></span>

#### <a name="a-streaming-url-for-hls-has-the-following-format"></a><span data-ttu-id="ddd0e-195">Uma URL de streaming para HLS tem o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="ddd0e-195">A streaming URL for HLS has the following format:</span></span>

<span data-ttu-id="ddd0e-196">{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span><span class="sxs-lookup"><span data-stu-id="ddd0e-196">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span></span>

#### <a name="a-streaming-url-for-smooth-streaming-has-the-following-format"></a><span data-ttu-id="ddd0e-197">Uma URL de streaming para Smooth Streaming tem o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="ddd0e-197">A streaming URL for Smooth Streaming has the following format:</span></span>

<span data-ttu-id="ddd0e-198">{nome do ponto de extremidade de streaming - nome de conta do dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arqui}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="ddd0e-198">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>


#### <a name="a-sas-url-used-to-download-files-has-the-following-format"></a><span data-ttu-id="ddd0e-199">Uma URL SAS usada para baixar arquivos tem o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="ddd0e-199">A SAS URL used to download files has the following format:</span></span>

<span data-ttu-id="ddd0e-200">{nome do contêiner de blob}/{nome do ativo}/{nome do arquivo}/{assinatura SAS}</span><span class="sxs-lookup"><span data-stu-id="ddd0e-200">{blob container name}/{asset name}/{file name}/{SAS signature}</span></span>

<span data-ttu-id="ddd0e-201">Extensões do SDK do .NET dos Serviços de Mídia fornecem métodos auxiliares práticos, que retornam URLs formatadas para o ativo publicado.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-201">Media Services .NET SDK extensions provide convenient helper methods that return formatted URLs for the published asset.</span></span>

<span data-ttu-id="ddd0e-202">O código a seguir usa extensões do SDK .NET para criar os localizadores e obter streaming e URLs de download progressivo.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-202">The following code uses .NET SDK Extensions to create locators and to get streaming and progressive download URLs.</span></span> <span data-ttu-id="ddd0e-203">O código também mostra como baixar os arquivos em uma pasta local.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-203">The code also shows how to download files to a local folder.</span></span>

<span data-ttu-id="ddd0e-204">Adicionar o método a seguir à classe do programa.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-204">Add the following method to the Program class.</span></span>

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish the output asset by creating an Origin locator for adaptive streaming,
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

        // Get the Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and the Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get the URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  the streaming URLs.
        Console.WriteLine("Use the following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display the URLs for progressive download.
        Console.WriteLine("Use the following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download the output asset to a local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files to a local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a><span data-ttu-id="ddd0e-205">Testar ao reproduzir o conteúdo</span><span class="sxs-lookup"><span data-stu-id="ddd0e-205">Test by playing your content</span></span>

<span data-ttu-id="ddd0e-206">Depois que você executar o programa definido na seção anterior, as URLs semelhantes à seguinte serão exibidas na janela do console.</span><span class="sxs-lookup"><span data-stu-id="ddd0e-206">Once you run the program defined in the previous section, the URLs similar to the following will be displayed in the console window.</span></span>

<span data-ttu-id="ddd0e-207">URLs de streaming adaptáveis:</span><span class="sxs-lookup"><span data-stu-id="ddd0e-207">Adaptive streaming URLs:</span></span>

<span data-ttu-id="ddd0e-208">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="ddd0e-208">Smooth Streaming</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="ddd0e-209">HLS</span><span class="sxs-lookup"><span data-stu-id="ddd0e-209">HLS</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="ddd0e-210">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="ddd0e-210">MPEG DASH</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

<span data-ttu-id="ddd0e-211">URLs de download progressivo (áudio e vídeo).</span><span class="sxs-lookup"><span data-stu-id="ddd0e-211">Progressive download URLs (audio and video).</span></span>

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


<span data-ttu-id="ddd0e-212">Para transmitir o vídeo, cole a URL na caixa de texto de URL no [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="ddd0e-212">To stream your video, paste your URL in the URL textbox in the [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="ddd0e-213">Para testar o download progressivo, cole uma URL em um navegador (por exemplo, Internet Explorer, Chrome ou Safari).</span><span class="sxs-lookup"><span data-stu-id="ddd0e-213">To test progressive download, paste a URL into a browser (for example, Internet Explorer, Chrome, or Safari).</span></span>

<span data-ttu-id="ddd0e-214">Para saber mais, consulte os tópicos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ddd0e-214">For more information, see the following topics:</span></span>

- [<span data-ttu-id="ddd0e-215">Reprodução de seu conteúdo com players existentes</span><span class="sxs-lookup"><span data-stu-id="ddd0e-215">Playing your content with existing players</span></span>](media-services-playback-content-with-existing-players.md)
- [<span data-ttu-id="ddd0e-216">Desenvolver aplicativos de player de vídeo</span><span class="sxs-lookup"><span data-stu-id="ddd0e-216">Develop video player applications</span></span>](media-services-develop-video-players.md)
- [<span data-ttu-id="ddd0e-217">Inserindo um vídeo de streaming adaptável MPEG-DASH em um aplicativo HTML5 com DASH.js</span><span class="sxs-lookup"><span data-stu-id="ddd0e-217">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a><span data-ttu-id="ddd0e-218">Baixar exemplo</span><span class="sxs-lookup"><span data-stu-id="ddd0e-218">Download sample</span></span>
<span data-ttu-id="ddd0e-219">O exemplo de código a seguir contém o código que você criou neste tutorial: [exemplo](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="ddd0e-219">The following code sample contains the code that you created in this tutorial: [sample](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddd0e-220">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ddd0e-220">Next Steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ddd0e-221">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="ddd0e-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
