---
title: "aaaUse miniaturas de vídeo de mídia do Azure tooCreate um resumo de vídeo | Microsoft Docs"
description: "Resumo de vídeo pode ajudá-lo a criar resumos dos vídeos longos selecionando automaticamente trechos interessantes de vídeo de origem hello. Isso é útil quando você deseja tooprovide uma visão rápida do que tooexpect em um vídeo longo."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: a245529f-3150-4afc-93ec-e40d8a6b761d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: 0a8f0bba6c12a948b940114fe4937e675688a8c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-video-thumbnails-toocreate-a-video-summarization"></a><span data-ttu-id="d8291-104">Use miniaturas de vídeo de mídia do Azure tooCreate um resumo de vídeo</span><span class="sxs-lookup"><span data-stu-id="d8291-104">Use Azure Media Video Thumbnails tooCreate a Video Summarization</span></span>
## <a name="overview"></a><span data-ttu-id="d8291-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d8291-105">Overview</span></span>
<span data-ttu-id="d8291-106">Olá **miniaturas de vídeo de mídia do Azure** processador de mídia (MP) permite que você toocreate um resumo de um vídeo que é útil toocustomers que desejam apenas toopreview um resumo de um vídeo longo.</span><span class="sxs-lookup"><span data-stu-id="d8291-106">hello **Azure Media Video Thumbnails** media processor (MP) enables you toocreate a summary of a video that is useful toocustomers who just want toopreview a summary of a long video.</span></span> <span data-ttu-id="d8291-107">Por exemplo, os clientes talvez queira toosee um "Resumo vídeo" ao focalizar uma miniatura.</span><span class="sxs-lookup"><span data-stu-id="d8291-107">For example, customers might want toosee a short "summary video" when they hover over a thumbnail.</span></span> <span data-ttu-id="d8291-108">Ajustando os parâmetros de saudação do **miniaturas de vídeo de mídia do Azure** por meio de uma predefinição de configuração, você pode usar a detecção de captura poderoso saudação do pacote de gerenciamento e concatenação tecnologia tooalgorithmically gerar um subclip descritivo.</span><span class="sxs-lookup"><span data-stu-id="d8291-108">By tweaking hello parameters of **Azure Media Video Thumbnails** through a configuration preset, you can use hello MP's powerful shot detection and concatenation technology tooalgorithmically generate a descriptive subclip.</span></span>  

<span data-ttu-id="d8291-109">Olá **miniatura de vídeo de mídia do Azure** MP está atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="d8291-109">hello **Azure Media Video Thumbnail** MP is currently in Preview.</span></span>

<span data-ttu-id="d8291-110">Este tópico fornece detalhes sobre **miniatura de vídeo de mídia do Azure** e mostra como toouse com o SDK do Media Services para .NET.</span><span class="sxs-lookup"><span data-stu-id="d8291-110">This topic gives details about  **Azure Media Video Thumbnail** and shows how toouse it with Media Services SDK for .NET.</span></span>

## <a name="limitations"></a><span data-ttu-id="d8291-111">Limitações</span><span class="sxs-lookup"><span data-stu-id="d8291-111">Limitations</span></span>

<span data-ttu-id="d8291-112">Em alguns casos, se o vídeo não é composto por diferentes cenas, Olá saída será apenas uma única captura.</span><span class="sxs-lookup"><span data-stu-id="d8291-112">In some cases, if your video is not comprised of different scenes, hello output will only be a single shot.</span></span>

## <a name="video-summary-example"></a><span data-ttu-id="d8291-113">Exemplo de resumo de vídeo</span><span class="sxs-lookup"><span data-stu-id="d8291-113">Video summary example</span></span>
<span data-ttu-id="d8291-114">Aqui estão alguns exemplos do que processadores de mídia Olá miniaturas de vídeo de mídia do Azure podem fazer:</span><span class="sxs-lookup"><span data-stu-id="d8291-114">Here are some examples of what hello Azure Media Video Thumbnails media processor can do:</span></span>

### <a name="original-video"></a><span data-ttu-id="d8291-115">Vídeo original</span><span class="sxs-lookup"><span data-stu-id="d8291-115">Original video</span></span>
[<span data-ttu-id="d8291-116">Vídeo original</span><span class="sxs-lookup"><span data-stu-id="d8291-116">Original video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a><span data-ttu-id="d8291-117">Resultado da miniatura de vídeo</span><span class="sxs-lookup"><span data-stu-id="d8291-117">Video thumbnail result</span></span>
[<span data-ttu-id="d8291-118">Resultado da miniatura de vídeo</span><span class="sxs-lookup"><span data-stu-id="d8291-118">Video thumbnail result</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a><span data-ttu-id="d8291-119">Configuração de tarefa (predefinição)</span><span class="sxs-lookup"><span data-stu-id="d8291-119">Task configuration (preset)</span></span>
<span data-ttu-id="d8291-120">Ao criar uma tarefa de miniatura de vídeo com as **Miniaturas de Vídeo de Mídia do Azure**, é necessário especificar uma predefinição de configuração.</span><span class="sxs-lookup"><span data-stu-id="d8291-120">When creating a video thumbnail task with **Azure Media Video Thumbnails**, you must specify a configuration preset.</span></span> <span data-ttu-id="d8291-121">Olá acima em miniatura exemplo foi criado com hello básicas de configuração JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="d8291-121">hello above thumbnail sample was created with hello following basic JSON configuration:</span></span>

    {"version":"1.0"}

<span data-ttu-id="d8291-122">No momento, você pode alterar Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="d8291-122">Currently, you can change hello following parameters:</span></span>

| <span data-ttu-id="d8291-123">Param</span><span class="sxs-lookup"><span data-stu-id="d8291-123">Param</span></span> | <span data-ttu-id="d8291-124">Descrição</span><span class="sxs-lookup"><span data-stu-id="d8291-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d8291-125">outputAudio</span><span class="sxs-lookup"><span data-stu-id="d8291-125">outputAudio</span></span> |<span data-ttu-id="d8291-126">Especifica se ou não o vídeo resultante Olá contém áudio.</span><span class="sxs-lookup"><span data-stu-id="d8291-126">Specifies whether or not hello resultant video contains any audio.</span></span> <br/><span data-ttu-id="d8291-127">Valores permitidos: True ou False.</span><span class="sxs-lookup"><span data-stu-id="d8291-127">Allowed values are: True or False.</span></span> <span data-ttu-id="d8291-128">Padrão: True.</span><span class="sxs-lookup"><span data-stu-id="d8291-128">Default is True.</span></span> |
| <span data-ttu-id="d8291-129">fadeInFadeOut</span><span class="sxs-lookup"><span data-stu-id="d8291-129">fadeInFadeOut</span></span> |<span data-ttu-id="d8291-130">Especifica se transições de esmaecimento usados entre miniaturas de movimento separadas Olá.</span><span class="sxs-lookup"><span data-stu-id="d8291-130">Specifies whether or not fade transitions are used between hello separate motion thumbnails.</span></span>  <br/><span data-ttu-id="d8291-131">Valores permitidos: True ou False.</span><span class="sxs-lookup"><span data-stu-id="d8291-131">Allowed values are: True or False.</span></span>  <span data-ttu-id="d8291-132">Padrão: True.</span><span class="sxs-lookup"><span data-stu-id="d8291-132">Default is True.</span></span> |
| <span data-ttu-id="d8291-133">maxMotionThumbnailDurationInSecs</span><span class="sxs-lookup"><span data-stu-id="d8291-133">maxMotionThumbnailDurationInSecs</span></span> |<span data-ttu-id="d8291-134">Inteiro que especifica quanto tempo Olá todo resultante vídeo deve ser.</span><span class="sxs-lookup"><span data-stu-id="d8291-134">Integer that specifies how long hello entire resultant video shall be.</span></span>  <span data-ttu-id="d8291-135">O padrão depende da duração do vídeo original.</span><span class="sxs-lookup"><span data-stu-id="d8291-135">Default depends on original video duration.</span></span> |

<span data-ttu-id="d8291-136">Olá, tabela a seguir descreve saudação padrão duração, quando **maxMotionThumbnailInSecs** não é usado.</span><span class="sxs-lookup"><span data-stu-id="d8291-136">hello following table describes hello default duration, when **maxMotionThumbnailInSecs** is not used.</span></span>

|  |  |  |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="d8291-137">Duração do vídeo</span><span class="sxs-lookup"><span data-stu-id="d8291-137">Video duration</span></span> |<span data-ttu-id="d8291-138">d < 3 min</span><span class="sxs-lookup"><span data-stu-id="d8291-138">d < 3 min</span></span> |<span data-ttu-id="d8291-139">3 min < d < 15 min</span><span class="sxs-lookup"><span data-stu-id="d8291-139">3 min < d < 15 min</span></span> |
| <span data-ttu-id="d8291-140">Duração da miniatura</span><span class="sxs-lookup"><span data-stu-id="d8291-140">Thumbnail duration</span></span> |<span data-ttu-id="d8291-141">15 s (2 a 3 cenas)</span><span class="sxs-lookup"><span data-stu-id="d8291-141">15 sec (2-3 scenes)</span></span> |<span data-ttu-id="d8291-142">30 s (3 a 5 cenas)</span><span class="sxs-lookup"><span data-stu-id="d8291-142">30 sec (3-5 scenes)</span></span> |

<span data-ttu-id="d8291-143">Olá JSON a seguir define parâmetros disponíveis.</span><span class="sxs-lookup"><span data-stu-id="d8291-143">hello following JSON sets available parameters.</span></span>

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a><span data-ttu-id="d8291-144">Código de exemplo do .NET</span><span class="sxs-lookup"><span data-stu-id="d8291-144">.NET sample code</span></span>

<span data-ttu-id="d8291-145">a seguir Olá programa mostra como:</span><span class="sxs-lookup"><span data-stu-id="d8291-145">hello following program shows how to:</span></span>

1. <span data-ttu-id="d8291-146">Criar um ativo e carregar um arquivo de mídia no ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8291-146">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="d8291-147">Cria um trabalho com uma tarefa em miniatura de vídeo com base em um arquivo de configuração que contém Olá predefinição json a seguir.</span><span class="sxs-lookup"><span data-stu-id="d8291-147">Creates a job with a video thumbnail task based on a configuration file that contains hello following json preset.</span></span> 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. <span data-ttu-id="d8291-148">Baixa os arquivos de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="d8291-148">Downloads hello output files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="d8291-149">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d8291-149">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="d8291-150">Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="d8291-150">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="d8291-151">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d8291-151">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoSummarization
    {
        class Program
        {
            // Read values from hello App.config file.
            private static readonly string _AADTenantDomain =
                ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
                ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);


                // Run hello thumbnail job.
                var asset = RunVideoThumbnailJob(@"C:\supportFiles\VideoThumbnail\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoThumbnail\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoThumbnail\Output");
            }

            static IAsset RunVideoThumbnailJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Thumbnail Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Thumbnail Job");

                // Get a reference tooAzure Media Video Thumbnails.
                string MediaProcessorName = "Azure Media Video Thumbnails";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Thumbnail Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Thumbnail Output Asset", AssetCreationOptions.None);

                // Use hello following event handler toocheck job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch hello job.
                job.Submit();

                // Check job execution and wait for job toofinish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, hello event handling
                // method for job progress should log errors.  Here we check
                // for error state and exit if needed.
                if (job.State == JobState.Error)
                {
                    ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                    Console.WriteLine(string.Format("Error: {0}. {1}",
                                                    error.Code,
                                                    error.Message));
                    return null;
                }

                return job.OutputMediaAssets[0];
            }

            static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
            {
                IAsset asset = _context.Assets.Create(assetName, options);

                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                assetFile.Upload(filePath);

                return asset;
            }

            static void DownloadAsset(IAsset asset, string outputDirectory)
            {
                foreach (IAssetFile file in asset.AssetFiles)
                {
                    file.Download(Path.Combine(outputDirectory, file.Name));
                }
            }

            static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
                var processor = _context.MediaProcessors
                    .Where(p => p.Name == mediaProcessorName)
                    .ToList()
                    .OrderBy(p => new Version(p.Version))
                    .LastOrDefault();

                if (processor == null)
                    throw new ArgumentException(string.Format("Unknown media processor",
                                                               mediaProcessorName));

                return processor;
            }

            static private void StateChanged(object sender, JobStateChangedEventArgs e)
            {
                Console.WriteLine("Job state changed event:");
                Console.WriteLine("  Previous state: " + e.PreviousState);
                Console.WriteLine("  Current state: " + e.CurrentState);

                switch (e.CurrentState)
                {
                    case JobState.Finished:
                        Console.WriteLine();
                        Console.WriteLine("Job is finished.");
                        Console.WriteLine();
                        break;
                    case JobState.Canceling:
                    case JobState.Queued:
                    case JobState.Scheduled:
                    case JobState.Processing:
                        Console.WriteLine("Please wait...\n");
                        break;
                    case JobState.Canceled:
                    case JobState.Error:
                        // Cast sender as a job.
                        IJob job = (IJob)sender;
                        // Display or log error details as needed.
                        // LogJobStop(job.Id);
                        break;
                    default:
                        break;
                }
            }

        }
    }

### <a name="video-thumbnail-output"></a><span data-ttu-id="d8291-152">Saída da miniatura de vídeo</span><span class="sxs-lookup"><span data-stu-id="d8291-152">Video thumbnail output</span></span>
[<span data-ttu-id="d8291-153">Saída da miniatura de vídeo</span><span class="sxs-lookup"><span data-stu-id="d8291-153">Video thumbnail output</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a><span data-ttu-id="d8291-154">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="d8291-154">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d8291-155">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="d8291-155">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="d8291-156">Links relacionados</span><span class="sxs-lookup"><span data-stu-id="d8291-156">Related links</span></span>
[<span data-ttu-id="d8291-157">Visão geral do Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="d8291-157">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="d8291-158">Demonstrações do Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="d8291-158">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

