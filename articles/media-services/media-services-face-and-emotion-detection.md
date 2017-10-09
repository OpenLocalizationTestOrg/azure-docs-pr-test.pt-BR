---
title: "aaaDetect Face e emoção com análise de mídia do Azure | Microsoft Docs"
description: "Este tópico demonstra como toodetect faces e emoções com análise de mídia do Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5ca4692c-23f1-451d-9d82-cbc8bf0fd707
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: f58d81d82dde08a694cdb4d92c6bab6a40a9c157
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a>Detectar a face e a emoção com o Azure Media Analytics
## <a name="overview"></a>Visão geral
Olá **Detector de Face de mídia do Azure** processador de mídia (MP) permite que você toocount, acompanhar movimentos e até mesmo a participação do medidor público e reação via expressões faciais. Este serviço contém dois recursos: 

* **Detecção facial**
  
    A detecção facial localiza e acompanha as faces humanas em um vídeo. Várias faces podem ser detectadas e posteriormente ser controladas à medida que se movimentam, com metadados de hora e o local de saudação retornados em um arquivo JSON. Durante o rastreamento, ele tentará toogive um toohello ID consistente mesmo enfrentam enquanto pessoa Olá é mover-se na tela, mesmo se eles são obstruídos ou deixam brevemente quadro hello.
  
  > [!NOTE]
  > Esse serviço não realiza reconhecimento facial. Uma pessoa que sai do quadro de saudação ou se torna obstruída para muito tempo será fornecida uma nova ID quando elas retornam.
  > 
  > 
* **Detecção de emoções**
  
    Detecção de emoção é um componente opcional do hello processador de mídia de detecção de rosto que retorna análise em vários atributos emocionais de faces Olá detectadas, inclusive felicidade, tristeza, medo, irritação e muito mais. 

Olá **Detector de Face de mídia do Azure** MP está atualmente em visualização.

Este tópico fornece detalhes sobre **Detector de Face de mídia do Azure** e mostra como toouse com o SDK do Media Services para .NET.

## <a name="face-detector-input-files"></a>Arquivos de entrada do Face Detector
Arquivos de vídeo. Atualmente, a saudação formatos a seguir têm suporte: MOV, MP4 e WMV.

## <a name="face-detector-output-files"></a>Arquivos de saída do Face Detector
API de controle e detecção de face Olá fornece controle que pode detectar o too64 as faces humana em um vídeo e detecção de local de face de alta precisão. Faces frontais fornecem Olá obter melhores resultados, enquanto as faces lado e faces pequenas (menor que ou igual a too24x24 pixels) pode não ser tão precisas.

Olá faces detectadas e controladas são retornadas pelas coordenadas (esquerda, superior, largura e altura) que indica o local de saudação de faces na imagem de saudação em pixels, bem como uma face ID numérica que indica Olá controle dessa pessoa. Números de identificação de face são propensas a tooreset em circunstâncias quando face frontal Olá for perdido ou sobreposta no quadro hello, resultando em algumas pessoas ser atribuídas a várias IDs.

## <a id="output_elements"></a>Elementos Olá JSON do arquivo de saída

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

Detector de face usa técnicas de fragmentação (onde Olá metadados podem ser dividido em partes com base em hora e você pode baixar apenas o que é necessário) e segmentação (onde os eventos de saudação são divididos caso eles obtêm muito grandes). Alguns cálculos simples podem ajudá-lo a transformar dados hello. Por exemplo, se um evento tiver começado em 6300 (tiques), com uma escala de tempo de 2997 (tiques/s) e uma taxa de quadros de 29,97 (quadros/s), então:

* Início/Escala de tempo = 2,1 segundos
* Segundos x taxa de quadros = 63 quadros

## <a name="face-detection-input-and-output-example"></a>Exemplo de entrada e saída da detecção facial
### <a name="input-video"></a>Vídeo de entrada
[Vídeo de Entrada](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a>Configuração de tarefa (predefinição)
Ao criar uma tarefa com o **Azure Media Face Detector**, é necessário especificar uma predefinição de configuração. Olá predefinição de configuração a seguir é apenas para detecção de rosto.

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a>Descrições de atributos
| Nome do atributo | Descrição |
| --- | --- |
| Mode |Mais rápido: maior velocidade de processamento, mas menos precisão (padrão).|

### <a name="json-output"></a>Saída em JSON
saudação de exemplo da saída JSON a seguir foi truncada.

    {
    "version": 1,
    "timescale": 30000,
    "offset": 0,
    "framerate": 29.97,
    "width": 1280,
    "height": 720,
    "fragments": [
        {
        "start": 0,
        "duration": 60060
        },
        {
        "start": 60060,
        "duration": 60060,
        "interval": 1001,
        "events": [
            [
            {
                "id": 0,
                "x": 0.519531,
                "y": 0.180556,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517969,
                "y": 0.181944,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517187,
                "y": 0.183333,
                "width": 0.0851562,
                "height": 0.151389
            }
            ],

        . . . 

## <a name="emotion-detection-input-and-output-example"></a>Exemplo de entrada e saída da detecção de emoção
### <a name="input-video"></a>Vídeo de entrada
[Vídeo de Entrada](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a>Configuração de tarefa (predefinição)
Ao criar uma tarefa com o **Azure Media Face Detector**, é necessário especificar uma predefinição de configuração. Olá predefinição de configuração a seguir especifica toocreate que JSON com base na detecção de emoção hello.

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a>Descrições de atributos
| Nome do atributo | Descrição |
| --- | --- |
| Modo |Faces: somente detecção facial.<br/>PerFaceEmotion: retornar emoção independentemente de cada detecção facial.<br/>AggregateEmotion: retorna uma média dos valores de emoção para todas as faces no quadro. |
| AggregateEmotionWindowMs |Use se o modo AggregateEmotion for selecionado. Especifica o comprimento de saudação do vídeo tooproduce usado cada resultado da agregação, em milissegundos. |
| AggregateEmotionIntervalMs |Use se o modo AggregateEmotion for selecionado. Especifica com resultados de agregação de tooproduce que frequência. |

#### <a name="aggregate-defaults"></a>Padrões de agregação
Abaixo são recomendados para a janela de agregação hello e as configurações de intervalo. AggregateEmotionWindowMs deve ser maior que AggregateEmotionIntervalMs.

|| Padrões | Mín. | Máx. |
|--- | --- | --- | --- |
| AggregateEmotionWindowMs |0,5 |2 |0,25|
| AggregateEmotionIntervalMs |0,5 |1 |0,25|

### <a name="json-output"></a>Saída em JSON
Saída em JSON para agregação de emoção (truncada):

    {
     "version": 1,
     "timescale": 30000,
     "offset": 0,
     "framerate": 29.97,
     "width": 1280,
     "height": 720,
     "fragments": [
       {
         "start": 0,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ]
         ]
       },
       {
         "start": 60060,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0.688541,
                 "happiness": 0.0586323,
                 "surprise": 0.227184,
                 "sadness": 0.00945675,
                 "anger": 0.00592107,
                 "disgust": 0.00154993,
                 "fear": 0.00450447,
                 "contempt": 0.0042109
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,

## <a name="limitations"></a>Limitações
* formatos de vídeo entrada Hello com suporte incluem MP4, MOV e WMV.
* intervalo de tamanho de face detectáveis Olá é 24 x 24 pixels de too2048x2048. Olá faces fora desse intervalo não serão detectadas.
* Para cada vídeo, o número máximo de saudação de faces retornado é 64.
* Algumas faces podem não ser detectadas devido tootechnical desafios; Por exemplo, é muito grandes ângulos de face (pose head) e oclusão grande. Faces frontais e próximo frontal tem os melhores resultados de saudação.

## <a name="net-sample-code"></a>Código de exemplo do .NET

a seguir Olá programa mostra como:

1. Criar um ativo e carregar um arquivo de mídia no ativo de saudação.
2. Crie um trabalho com uma tarefa de detecção de rosto com base em um arquivo de configuração que contém Olá predefinição json a seguir. 
   
        {
            "version": "1.0"
        }
3. Baixe os arquivos de saída do JSON hello. 

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

    namespace FaceDetection
    {
        class Program
        {
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

                // Run hello FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference tooAzure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

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

[Demonstrações do Azure Media Analytics](http://amslabs.azurewebsites.net/demos/Analytics.html)

