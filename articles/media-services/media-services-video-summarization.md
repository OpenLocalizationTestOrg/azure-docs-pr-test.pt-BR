---
title: "Usar o Azure Media Video Thumbnails para Criar um Resumo de vídeo | Microsoft Docs"
description: "O resumo de vídeo pode ajudá-lo a criar resumos de vídeos de longa duração com a seleção automática de trechos interessantes do vídeo de origem. Isso será útil quando você desejar fornecer uma visão geral rápida do que esperar de um vídeo de longa duração."
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
ms.openlocfilehash: 5d5afdaf22ffea8f3b77a154acb5d0a8dda74405
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-media-video-thumbnails-to-create-a-video-summarization"></a><span data-ttu-id="c5621-104">Usar as Miniaturas de Vídeo de Mídia do Azure para criar um resumo de vídeo</span><span class="sxs-lookup"><span data-stu-id="c5621-104">Use Azure Media Video Thumbnails to Create a Video Summarization</span></span>
## <a name="overview"></a><span data-ttu-id="c5621-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c5621-105">Overview</span></span>
<span data-ttu-id="c5621-106">O MP (processador de mídia) das **Miniaturas de Vídeo de Mídia do Azure** permite criar o resumo de um vídeo que é grande utilidade para clientes que desejam apenas visualizar um resumo de um vídeo de longa duração.</span><span class="sxs-lookup"><span data-stu-id="c5621-106">The **Azure Media Video Thumbnails** media processor (MP) enables you to create a summary of a video that is useful to customers who just want to preview a summary of a long video.</span></span> <span data-ttu-id="c5621-107">Por exemplo, os clientes talvez queiram ver um breve “vídeo resumido” ao focalizar uma miniatura.</span><span class="sxs-lookup"><span data-stu-id="c5621-107">For example, customers might want to see a short "summary video" when they hover over a thumbnail.</span></span> <span data-ttu-id="c5621-108">Ao ajustar os parâmetros das **Miniaturas de Vídeo de Mídia do Azure** por meio de uma predefinição de configuração, é possível usar a avançada tecnologia de detecção de captura e concatenação do MP para gerar de forma algorítmica um subclipe descritivo.</span><span class="sxs-lookup"><span data-stu-id="c5621-108">By tweaking the parameters of **Azure Media Video Thumbnails** through a configuration preset, you can use the MP's powerful shot detection and concatenation technology to algorithmically generate a descriptive subclip.</span></span>  

<span data-ttu-id="c5621-109">No momento, o MP da **Miniatura de Vídeo de Mídia do Azure** está em Preview.</span><span class="sxs-lookup"><span data-stu-id="c5621-109">The **Azure Media Video Thumbnail** MP is currently in Preview.</span></span>

<span data-ttu-id="c5621-110">Este tópico fornece detalhes sobre a **Miniatura de Vídeo de Mídia do Azure** e mostra como usá-la com o SDK dos Serviços de Mídia para .NET.</span><span class="sxs-lookup"><span data-stu-id="c5621-110">This topic gives details about  **Azure Media Video Thumbnail** and shows how to use it with Media Services SDK for .NET.</span></span>

## <a name="limitations"></a><span data-ttu-id="c5621-111">Limitações</span><span class="sxs-lookup"><span data-stu-id="c5621-111">Limitations</span></span>

<span data-ttu-id="c5621-112">Em alguns casos, se o vídeo não for composto de cenas diferentes, a saída será apenas uma única captura.</span><span class="sxs-lookup"><span data-stu-id="c5621-112">In some cases, if your video is not comprised of different scenes, the output will only be a single shot.</span></span>

## <a name="video-summary-example"></a><span data-ttu-id="c5621-113">Exemplo de resumo de vídeo</span><span class="sxs-lookup"><span data-stu-id="c5621-113">Video summary example</span></span>
<span data-ttu-id="c5621-114">Apresentamos abaixo alguns exemplos do que o processador de mídia das Miniaturas de Vídeo de Mídia do Azure é capaz de fazer:</span><span class="sxs-lookup"><span data-stu-id="c5621-114">Here are some examples of what the Azure Media Video Thumbnails media processor can do:</span></span>

### <a name="original-video"></a><span data-ttu-id="c5621-115">Vídeo original</span><span class="sxs-lookup"><span data-stu-id="c5621-115">Original video</span></span>
[<span data-ttu-id="c5621-116">Vídeo original</span><span class="sxs-lookup"><span data-stu-id="c5621-116">Original video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a><span data-ttu-id="c5621-117">Resultado da miniatura de vídeo</span><span class="sxs-lookup"><span data-stu-id="c5621-117">Video thumbnail result</span></span>
[<span data-ttu-id="c5621-118">Resultado da miniatura de vídeo</span><span class="sxs-lookup"><span data-stu-id="c5621-118">Video thumbnail result</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a><span data-ttu-id="c5621-119">Configuração de tarefa (predefinição)</span><span class="sxs-lookup"><span data-stu-id="c5621-119">Task configuration (preset)</span></span>
<span data-ttu-id="c5621-120">Ao criar uma tarefa de miniatura de vídeo com as **Miniaturas de Vídeo de Mídia do Azure**, é necessário especificar uma predefinição de configuração.</span><span class="sxs-lookup"><span data-stu-id="c5621-120">When creating a video thumbnail task with **Azure Media Video Thumbnails**, you must specify a configuration preset.</span></span> <span data-ttu-id="c5621-121">O exemplo de miniatura acima foi criado com a seguinte configuração básica do JSON:</span><span class="sxs-lookup"><span data-stu-id="c5621-121">The above thumbnail sample was created with the following basic JSON configuration:</span></span>

    {"version":"1.0"}

<span data-ttu-id="c5621-122">No momento, é possível alterar os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="c5621-122">Currently, you can change the following parameters:</span></span>

| <span data-ttu-id="c5621-123">Param</span><span class="sxs-lookup"><span data-stu-id="c5621-123">Param</span></span> | <span data-ttu-id="c5621-124">Descrição</span><span class="sxs-lookup"><span data-stu-id="c5621-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c5621-125">outputAudio</span><span class="sxs-lookup"><span data-stu-id="c5621-125">outputAudio</span></span> |<span data-ttu-id="c5621-126">Especifica se o vídeo resultante conterá áudio.</span><span class="sxs-lookup"><span data-stu-id="c5621-126">Specifies whether or not the resultant video contains any audio.</span></span> <br/><span data-ttu-id="c5621-127">Valores permitidos: True ou False.</span><span class="sxs-lookup"><span data-stu-id="c5621-127">Allowed values are: True or False.</span></span> <span data-ttu-id="c5621-128">Padrão: True.</span><span class="sxs-lookup"><span data-stu-id="c5621-128">Default is True.</span></span> |
| <span data-ttu-id="c5621-129">fadeInFadeOut</span><span class="sxs-lookup"><span data-stu-id="c5621-129">fadeInFadeOut</span></span> |<span data-ttu-id="c5621-130">Especifica se as transições de esmaecimento serão usadas entre as miniaturas de movimento separadas.</span><span class="sxs-lookup"><span data-stu-id="c5621-130">Specifies whether or not fade transitions are used between the separate motion thumbnails.</span></span>  <br/><span data-ttu-id="c5621-131">Valores permitidos: True ou False.</span><span class="sxs-lookup"><span data-stu-id="c5621-131">Allowed values are: True or False.</span></span>  <span data-ttu-id="c5621-132">Padrão: True.</span><span class="sxs-lookup"><span data-stu-id="c5621-132">Default is True.</span></span> |
| <span data-ttu-id="c5621-133">maxMotionThumbnailDurationInSecs</span><span class="sxs-lookup"><span data-stu-id="c5621-133">maxMotionThumbnailDurationInSecs</span></span> |<span data-ttu-id="c5621-134">Inteiro que especifica qual será a duração de todo o vídeo resultante.</span><span class="sxs-lookup"><span data-stu-id="c5621-134">Integer that specifies how long the entire resultant video shall be.</span></span>  <span data-ttu-id="c5621-135">O padrão depende da duração do vídeo original.</span><span class="sxs-lookup"><span data-stu-id="c5621-135">Default depends on original video duration.</span></span> |

<span data-ttu-id="c5621-136">A tabela a seguir descreve a duração padrão, quando **maxMotionThumbnailInSecs** não é usado.</span><span class="sxs-lookup"><span data-stu-id="c5621-136">The following table describes the default duration, when **maxMotionThumbnailInSecs** is not used.</span></span>

|  |  |  |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="c5621-137">Duração do vídeo</span><span class="sxs-lookup"><span data-stu-id="c5621-137">Video duration</span></span> |<span data-ttu-id="c5621-138">d < 3 min</span><span class="sxs-lookup"><span data-stu-id="c5621-138">d < 3 min</span></span> |<span data-ttu-id="c5621-139">3 min < d < 15 min</span><span class="sxs-lookup"><span data-stu-id="c5621-139">3 min < d < 15 min</span></span> |
| <span data-ttu-id="c5621-140">Duração da miniatura</span><span class="sxs-lookup"><span data-stu-id="c5621-140">Thumbnail duration</span></span> |<span data-ttu-id="c5621-141">15 s (2 a 3 cenas)</span><span class="sxs-lookup"><span data-stu-id="c5621-141">15 sec (2-3 scenes)</span></span> |<span data-ttu-id="c5621-142">30 s (3 a 5 cenas)</span><span class="sxs-lookup"><span data-stu-id="c5621-142">30 sec (3-5 scenes)</span></span> |

<span data-ttu-id="c5621-143">O JSON a seguir define os parâmetros disponíveis.</span><span class="sxs-lookup"><span data-stu-id="c5621-143">The following JSON sets available parameters.</span></span>

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a><span data-ttu-id="c5621-144">Código de exemplo do .NET</span><span class="sxs-lookup"><span data-stu-id="c5621-144">.NET sample code</span></span>

<span data-ttu-id="c5621-145">O programa a seguir mostra como:</span><span class="sxs-lookup"><span data-stu-id="c5621-145">The following program shows how to:</span></span>

1. <span data-ttu-id="c5621-146">Criar um ativo e carregar um arquivo de mídia nesse ativo.</span><span class="sxs-lookup"><span data-stu-id="c5621-146">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="c5621-147">Criar um trabalho com uma miniatura de vídeo baseada em um arquivo de configuração que contém a predefinição de JSON a seguir.</span><span class="sxs-lookup"><span data-stu-id="c5621-147">Creates a job with a video thumbnail task based on a configuration file that contains the following json preset.</span></span> 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. <span data-ttu-id="c5621-148">Baixar os arquivos de saída.</span><span class="sxs-lookup"><span data-stu-id="c5621-148">Downloads the output files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="c5621-149">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c5621-149">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="c5621-150">Configure seu ambiente de desenvolvimento e preencha o arquivo de configuração app.config com as informações de conexão, conforme descrito em [Desenvolvimento de Serviços de Mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="c5621-150">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="c5621-151">Exemplo</span><span class="sxs-lookup"><span data-stu-id="c5621-151">Example</span></span>

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
            // Read values from the App.config file.
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


                // Run the thumbnail job.
                var asset = RunVideoThumbnailJob(@"C:\supportFiles\VideoThumbnail\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoThumbnail\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoThumbnail\Output");
            }

            static IAsset RunVideoThumbnailJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Thumbnail Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Thumbnail Job");

                // Get a reference to Azure Media Video Thumbnails.
                string MediaProcessorName = "Azure Media Video Thumbnails";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Thumbnail Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Video Thumbnail Output Asset", AssetCreationOptions.None);

                // Use the following event handler to check job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch the job.
                job.Submit();

                // Check job execution and wait for job to finish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, the event handling
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

### <a name="video-thumbnail-output"></a><span data-ttu-id="c5621-152">Saída da miniatura de vídeo</span><span class="sxs-lookup"><span data-stu-id="c5621-152">Video thumbnail output</span></span>
[<span data-ttu-id="c5621-153">Saída da miniatura de vídeo</span><span class="sxs-lookup"><span data-stu-id="c5621-153">Video thumbnail output</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a><span data-ttu-id="c5621-154">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="c5621-154">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c5621-155">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="c5621-155">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="c5621-156">Links relacionados</span><span class="sxs-lookup"><span data-stu-id="c5621-156">Related links</span></span>
[<span data-ttu-id="c5621-157">Visão geral do Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="c5621-157">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="c5621-158">Demonstrações do Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="c5621-158">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

