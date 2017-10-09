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
# <a name="use-azure-media-video-thumbnails-toocreate-a-video-summarization"></a>Use miniaturas de vídeo de mídia do Azure tooCreate um resumo de vídeo
## <a name="overview"></a>Visão geral
Olá **miniaturas de vídeo de mídia do Azure** processador de mídia (MP) permite que você toocreate um resumo de um vídeo que é útil toocustomers que desejam apenas toopreview um resumo de um vídeo longo. Por exemplo, os clientes talvez queira toosee um "Resumo vídeo" ao focalizar uma miniatura. Ajustando os parâmetros de saudação do **miniaturas de vídeo de mídia do Azure** por meio de uma predefinição de configuração, você pode usar a detecção de captura poderoso saudação do pacote de gerenciamento e concatenação tecnologia tooalgorithmically gerar um subclip descritivo.  

Olá **miniatura de vídeo de mídia do Azure** MP está atualmente em visualização.

Este tópico fornece detalhes sobre **miniatura de vídeo de mídia do Azure** e mostra como toouse com o SDK do Media Services para .NET.

## <a name="limitations"></a>Limitações

Em alguns casos, se o vídeo não é composto por diferentes cenas, Olá saída será apenas uma única captura.

## <a name="video-summary-example"></a>Exemplo de resumo de vídeo
Aqui estão alguns exemplos do que processadores de mídia Olá miniaturas de vídeo de mídia do Azure podem fazer:

### <a name="original-video"></a>Vídeo original
[Vídeo original](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a>Resultado da miniatura de vídeo
[Resultado da miniatura de vídeo](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a>Configuração de tarefa (predefinição)
Ao criar uma tarefa de miniatura de vídeo com as **Miniaturas de Vídeo de Mídia do Azure**, é necessário especificar uma predefinição de configuração. Olá acima em miniatura exemplo foi criado com hello básicas de configuração JSON a seguir:

    {"version":"1.0"}

No momento, você pode alterar Olá parâmetros a seguir:

| Param | Descrição |
| --- | --- |
| outputAudio |Especifica se ou não o vídeo resultante Olá contém áudio. <br/>Valores permitidos: True ou False. Padrão: True. |
| fadeInFadeOut |Especifica se transições de esmaecimento usados entre miniaturas de movimento separadas Olá.  <br/>Valores permitidos: True ou False.  Padrão: True. |
| maxMotionThumbnailDurationInSecs |Inteiro que especifica quanto tempo Olá todo resultante vídeo deve ser.  O padrão depende da duração do vídeo original. |

Olá, tabela a seguir descreve saudação padrão duração, quando **maxMotionThumbnailInSecs** não é usado.

|  |  |  |
| --- | --- | --- | --- | --- |
| Duração do vídeo |d < 3 min |3 min < d < 15 min |
| Duração da miniatura |15 s (2 a 3 cenas) |30 s (3 a 5 cenas) |

Olá JSON a seguir define parâmetros disponíveis.

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a>Código de exemplo do .NET

a seguir Olá programa mostra como:

1. Criar um ativo e carregar um arquivo de mídia no ativo de saudação.
2. Cria um trabalho com uma tarefa em miniatura de vídeo com base em um arquivo de configuração que contém Olá predefinição json a seguir. 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. Baixa os arquivos de saída de hello. 

#### <a name="create-and-configure-a-visual-studio-project"></a>Criar e configurar um projeto do Visual Studio

Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Exemplo

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

### <a name="video-thumbnail-output"></a>Saída da miniatura de vídeo
[Saída da miniatura de vídeo](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Links relacionados
[Visão geral do Azure Media Services Analytics](media-services-analytics-overview.md)

[Demonstrações do Azure Media Analytics](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

