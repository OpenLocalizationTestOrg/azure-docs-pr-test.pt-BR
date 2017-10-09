---
title: "aaaIndexing arquivos de mídia com a visualização de 2 do indexador de mídia do Azure | Microsoft Docs"
description: "Indexador de mídia do Azure permite que você toomake conteúdo de seus arquivos de mídia pesquisáveis e toogenerate uma transcrição de texto completo para legendas e palavras-chave. Este tópico mostra como toouse indexador de mídia 2 visualizar."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 85d25525-a498-44eb-ae3a-2ca5ceb8e53d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: f83fa0db58b828ffa29933d68ce108b4906dcd78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-media-files-with-azure-media-indexer-2-preview"></a>Indexando arquivos de mídia com a Preview do Azure Media Indexer 2
## <a name="overview"></a>Visão geral
Olá **visualização de 2 do indexador de mídia do Azure** processador de mídia (MP) permite que você toomake arquivos de mídia e conteúdo pesquisável, bem como gerar faixas de legendas fechadas. Toohello em comparação com a versão anterior do [Azure Media Indexer](media-services-index-content.md), **visualização de 2 do indexador de mídia do Azure** executa a indexação mais rápida e oferece maior suporte a idiomas. Os idiomas com suporte incluem o inglês, espanhol, francês, alemão, italiano, chinês (mandarim, simplificado), português, árabe e japonês.

Olá **visualização de 2 do indexador de mídia do Azure** MP está atualmente em visualização.

Este tópico mostra como trabalhos de indexação toocreate com **visualização de 2 do indexador de mídia do Azure**.

> [!NOTE]
> Olá considerações a seguir se aplicam:
> 
> Não há suporte para o Indexador 2 no Azure China e no Azure Governamental.
> 
> Quando a indexação de conteúdo, verifique se toouse arquivos de mídia com fala muito clara (sem música em segundo plano, ruído, efeitos ou assovio de microfone). Alguns exemplos de conteúdo apropriado são: reuniões, palestras e apresentações registradas. Olá seguinte conteúdo pode não ser adequado para indexação: filmes, programas de TV, tudo com misto de áudio e efeitos sonoros, conteúdo mal registrado com ruídos de fundo (assovio).
> 
> 

Este tópico fornece detalhes sobre **visualização de 2 do indexador de mídia do Azure** e mostra como toouse com o SDK do Media Services para .NET

## <a name="input-and-output-files"></a>Arquivos de entrada e saída
### <a name="input-files"></a>Arquivos de entrada
Arquivos de áudio ou vídeo

### <a name="output-files"></a>Arquivos de saída
Um trabalho de indexação pode gerar arquivos de legenda codificada Olá formatos a seguir:  

* **SAMI**
* **TTML**
* **WebVTT**

Arquivos fechados de legenda (CC) nos seguintes formatos podem ser usados toomake áudio e vídeo arquivos toopeople acessível com deficiência auditiva.

## <a name="task-configuration-preset"></a>Configuração de tarefa (predefinição)
Ao criar uma tarefa de indexação com a **Preview do Azure Media Indexer 2**, é necessário especificar uma predefinição de configuração.

Olá JSON a seguir define parâmetros disponíveis.

    {
      "version":"1.0",
      "Features":
        [
           {
           "Options": {
                "Formats":["WebVtt","ttml"],
                "Language":"enUs",
                "Type":"RecoOptions"
           },
           "Type":"SpReco"
        }]
    }

## <a name="supported-languages"></a>Idiomas com suporte
Visualização 2 de indexador de mídia do Azure suporta fala em texto de saudação idiomas a seguir (ao especificar o nome do idioma Olá na configuração da tarefa hello, use o código de 4 caracteres entre colchetes, conforme mostrado abaixo):

* Inglês [EnUs]
* Espanhol [EsEs]
* Chinês (mandarim, simplificado) [ZhCn]
* Francês [FrFr]
* Alemão [DeDe]
* Italiano [ItIt]
* Português [PtBr]
* Árabe (Egípcio) [ArEg]
* Japonês [JaJp]
* Russo [RuRu]
* Inglês britânico [EnGb]
* Espanhol do México [EsMx] 

## <a name="supported-file-types"></a>Tipos de arquivo com suporte

Para obter informações sobre os tipos de arquivos com suporte, consulte Olá [codecs/formatos com suporte](media-services-media-encoder-standard-formats.md#input-containerfile-formats) seção.

## <a name="net-sample-code"></a>Código de exemplo do .NET

a seguir Olá programa mostra como:

1. Criar um ativo e carregar um arquivo de mídia no ativo de saudação.
2. Crie um trabalho com uma tarefa de indexação com base em um arquivo de configuração que contém Olá predefinição json a seguir.
   
        {
          "version":"1.0",
          "Features":
            [
               {
               "Options": {
                    "Formats":["WebVtt","ttml"],
                    "Language":"enUs",
                    "Type":"RecoOptions"
               },
               "Type":"SpReco"
            }]
        }
3. Baixe arquivos de saída de hello. 
   
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

    namespace IndexContent
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

                // Run indexing job.
                var asset = RunIndexingJob(@"C:\supportFiles\Indexer\BigBuckBunny.mp4",
                                            @"C:\supportFiles\Indexer\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\Indexer\Output");
            }

            static IAsset RunIndexingJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Indexing Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Indexing Job");

                // Get a reference tooAzure Media Indexer 2 Preview.
                string MediaProcessorName = "Azure Media Indexer 2 Preview";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Indexing Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset toobe indexed.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Indexing Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Links relacionados
[Visão geral do Azure Media Services Analytics](media-services-analytics-overview.md)

[Demonstrações do Azure Media Analytics](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

