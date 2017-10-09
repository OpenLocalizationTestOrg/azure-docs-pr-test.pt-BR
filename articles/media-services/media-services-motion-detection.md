---
title: "aaaDetect movimentos com análise de mídia do Azure | Microsoft Docs"
description: "Olá habilita de processador (MP) do Detector de movimento de mídia do Azure media tooefficiently você identificar seções de interesse em um vídeo de outra forma longa e sem problemas."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: d144f813-1a55-442f-a895-5c4cb6d0aeae
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: milanga;juliako;
ms.openlocfilehash: cb431375c92222053ed2239dd4e45767524dab68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a>Detectar movimentos com o Azure Media Analytics
## <a name="overview"></a>Visão geral
Olá **Detector de movimento de mídia do Azure** habilita (MP) do processador de mídia tooefficiently você identificar seções de interesse em um vídeo de outra forma longa e sem problemas. Detecção de movimento pode ser usada em câmera estático filmagens tooidentify seções de vídeo Olá onde ocorre a animação. Ele gera um arquivo JSON que contém um metadados com carimbos de hora e hello delimitadora região em que ocorreu o evento hello.

Destinado a feeds de vídeo de segurança, essa tecnologia é capaz de toocategorize movimento em eventos relevantes e falsos positivos, como alterações de iluminação e sombras. Isso permite toogenerate alertas de segurança de feeds de câmera sem recebam eventos irrelevantes infinito, enquanto estiver sendo momentos tooextract capaz de interesse de vídeos de vigilância muito longos.

Olá **Detector de movimento de mídia do Azure** MP está atualmente em visualização.

Este tópico fornece detalhes sobre **Detector de movimento de mídia do Azure** e mostra como toouse com o SDK do Media Services para .NET

## <a name="motion-detector-input-files"></a>Arquivos de entrada do Motion Detector
Arquivos de vídeo. Atualmente, a saudação formatos a seguir têm suporte: MOV, MP4 e WMV.

## <a name="task-configuration-preset"></a>Configuração de tarefa (predefinição)
Quando você criar uma tarefa com o **Azure Media Motion Detector**, deverá especificar uma predefinição de configuração. 

### <a name="parameters"></a>parâmetros
Você pode usar o hello parâmetros a seguir:

| Nome | Opções | Descrição | Padrão |
| --- | --- | --- | --- |
| sensitivityLevel |Cadeia de caracteres: 'low', 'medium', 'high' |Define a sensibilidade de saudação nível no qual movimentos é relatado. Ajuste esta quantidade tooadjust de falsos positivos. |'medium' |
| frameSamplingValue |Número inteiro positivo |Define a frequência de saudação no qual o algoritmo é executado. 1 equivale a cada quadro, 2 significa a cada dois quadros e assim por diante. |1 |
| detectLightChange |Booliano: 'true', 'false' |Define se alterações leves são relatadas nos resultados da saudação |'False' |
| mergeTimeThreshold |Xs-time: Hh:mm:ss<br/>Exemplo: 00:00:03 |Especifica a janela de tempo de saudação entre os eventos de movimento onde 2 eventos serão combinados e relatados como 1. |00:00:00 |
| detectionZones |Uma matriz de zonas de detecção:<br/>- A Zona de Detecção é uma matriz de três ou mais pontos<br/>-Ponto é um x e y coordenada de too1 0. |Descreve a lista de saudação de detecção poligonal zonas toobe usado.<br/>Resultados serão relatados com zonas hello como uma ID, com hello primeiro sendo 'id': 0 |Zona única que abrange toda a estrutura hello. |

### <a name="json-example"></a>Exemplo de JSON
    {
      "version": "1.0",
      "options": {
        "sensitivityLevel": "medium",
        "frameSamplingValue": 1,
        "detectLightChange": "False",
        "mergeTimeThreshold":
        "00:00:02",
        "detectionZones": [
          [
            {"x": 0, "y": 0},
            {"x": 0.5, "y": 0},
            {"x": 0, "y": 1}
           ],
          [
            {"x": 0.3, "y": 0.3},
            {"x": 0.55, "y": 0.3},
            {"x": 0.8, "y": 0.3},
            {"x": 0.8, "y": 0.55},
            {"x": 0.8, "y": 0.8},
            {"x": 0.55, "y": 0.8},
            {"x": 0.3, "y": 0.8},
            {"x": 0.3, "y": 0.55}
          ]
        ]
      }
    }


## <a name="motion-detector-output-files"></a>Arquivos de saída do Motion Detector
Um trabalho de detecção de movimento retornará um arquivo JSON Olá ativo de saída que descreve os alertas de movimento hello e suas categorias, dentro de saudação vídeo. arquivo de saudação conterá informações sobre tempo de saudação e a duração da animação detectada no vídeo de saudação.

Olá API do Detector de movimento fornece indicadores quando existem objetos em movimento em um plano fixo vídeo (por exemplo, um vídeo de inspeção). Olá Detector de movimento é treinado tooreduce falsos alarmes, iluminação e as alterações de sombra. Limitações atuais dos algoritmos de saudação incluem vídeos de visão da noite, semitransparentes objetos e objetos pequenos.

### <a id="output_elements"></a>Elementos Olá JSON do arquivo de saída
> [!NOTE]
> Na versão mais recente do hello, formato da saída JSON de saudação foi alterado e pode representar uma alteração significativa para alguns clientes.
> 
> 

Olá tabela a seguir descreve os elementos Olá JSON do arquivo de saída.

| Elemento | Descrição |
| --- | --- |
| Versão |Isso se refere a versão toohello de saudação API de vídeo. versão atual do Hello é 2. |
| Escala de tempo |"Tiques" por segundo de vídeo hello. |
| Deslocamento |deslocamento de horário de saudação de carimbos de hora em "tiques". Na versão 1.0 das APIs de Vídeo, sempre será 0. Em cenários futuro para os quais oferecemos suporte, esse valor poderá ser alterado. |
| Taxa de quadros |Quadros por segundo do hello vídeo. |
| Largura, Altura |Refere-se toohello largura e altura da saudação vídeo em pixels. |
| Iniciar |Olá iniciar carimbo de hora "tiques". |
| Duration |comprimento de saudação do evento hello, em "tiques". |
| Intervalo |intervalo de saudação de cada entrada no evento hello, em "tiques". |
| Eventos |Cada fragmento do evento contém movimento Olá detectado dentro desse tempo de duração. |
| Tipo |Na versão atual do hello, isso é sempre '2' para o movimento genérico. Este rótulo fornece toocategorize movimento por vídeo APIs Olá flexibilidade em versões futuras. |
| RegionID |Conforme explicado acima, isso sempre será 0 nesta versão. Este rótulo fornece movimento por vídeo API Olá flexibilidade toofind em várias regiões em versões futuras. |
| Regiões |Refere-se a área de toohello no vídeo onde você se preocupa movimento. <br/><br/>-"id" representa a área da região hello – nesta versão há apenas um, ID de 0. <br/>-"type" representa a forma de saudação da região Olá importantes para você por movimento. Atualmente, "retângulo" e "polígono" têm suporte.<br/> Se você especificou "retângulo", a região Olá tem dimensões em X, Y, largura e altura. Hello X e Y coordenadas representam as coordenadas XY Olá superior esquerdo da região de saudação em uma escala normalizada de 0.0 too1.0. altura e largura de saudação representam o tamanho de saudação da região de saudação em uma escala normalizada de too1.0 0.0. Na versão atual do hello, X, Y, largura e altura sempre são corrigidas em 0, 0 e 1, 1. <br/>Se você especificou "polígono", a região Olá tem dimensões em pontos. <br/> |
| Fragmentos |Olá metadados está em bloco para cima em diferentes segmentos de chamadas de fragmentos. Cada fragmento contém um início, uma duração, um número de intervalo e evento(s). Um fragmento sem eventos significa que nenhum movimento foi detectado durante essa hora de início e duração. |
| Colchetes [] |Cada colchete representa um intervalo em eventos de saudação. Colchetes vazios para esse intervalo significam que nenhum movimento foi detectado. |
| locais |Essa nova entrada em eventos lista local de saudação onde ocorreu o movimento de saudação. Isso é mais específico que zonas de detecção de saudação. |

a seguir Olá é um exemplo de saída JSON

    {
      "version": 2,
      "timescale": 23976,
      "offset": 0,
      "framerate": 24,
      "width": 1280,
      "height": 720,
      "regions": [
        {
          "id": 0,
          "type": "polygon",
          "points": [{'x': 0, 'y': 0},
            {'x': 0.5, 'y': 0},
            {'x': 0, 'y': 1}]
        }
      ],
      "fragments": [
        {
          "start": 0,
          "duration": 226765
        },
        {
          "start": 226765,
          "duration": 47952,
          "interval": 999,
          "events": [
            [
              {
                "type": 2,
                "typeName": "motion",
                "locations": [
                  {
                    "x": 0.004184,
                    "y": 0.007463,
                    "width": 0.991667,
                    "height": 0.985185
                  }
                ],
                "regionId": 0
              }
            ],

    …
## <a name="limitations"></a>Limitações
* formatos de vídeo entrada Hello com suporte incluem MP4, MOV e WMV.
* A detecção de movimento é otimizada para vídeos estáticos em segundo plano. algoritmo de saudação se concentra na redução alarmes falsos, como alterações de iluminação e sombras.
* Alguns movimento não pode ser detectado devido tootechnical desafios; Por exemplo, vídeos de visão da noite, semitransparentes objetos e objetos pequenos.

## <a name="net-sample-code"></a>Código de exemplo do .NET

a seguir Olá programa mostra como:

1. Criar um ativo e carregar um arquivo de mídia no ativo de saudação.
2. Crie um trabalho com uma tarefa de detecção de movimento por vídeo com base em um arquivo de configuração que contém Olá predefinição json a seguir. 
   
        {
          "Version": "1.0",
          "Options": {
            "SensitivityLevel": "medium",
            "FrameSamplingValue": 1,
            "DetectLightChange": "False",
            "MergeTimeThreshold":
            "00:00:02",
            "DetectionZones": [
              [
                {"x": 0, "y": 0},
                {"x": 0.5, "y": 0},
                {"x": 0, "y": 1}
               ],
              [
                {"x": 0.3, "y": 0.3},
                {"x": 0.55, "y": 0.3},
                {"x": 0.8, "y": 0.3},
                {"x": 0.8, "y": 0.55},
                {"x": 0.8, "y": 0.8},
                {"x": 0.55, "y": 0.8},
                {"x": 0.3, "y": 0.8},
                {"x": 0.3, "y": 0.55}
              ]
            ]
          }
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

    namespace VideoMotionDetection
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

                // Run hello VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference tooAzure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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
[Blog do Detector de movimento dos Serviços de Mídia do Azure](https://azure.microsoft.com/blog/motion-detector-update/)

[Visão geral do Azure Media Services Analytics](media-services-analytics-overview.md)

[Demonstrações do Azure Media Analytics](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

