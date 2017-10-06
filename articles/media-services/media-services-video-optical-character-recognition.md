---
title: "texto aaaDigitize com OCR de análise de mídia do Azure | Microsoft Docs"
description: "OCR de análise de mídia do Azure (reconhecimento óptico de caracteres) permite que você tooconvert o conteúdo de texto em arquivos de vídeo em texto digital editável e pesquisável.  Isso permite a extração de saudação tooautomate de metadados significativo de sinal de vídeo de saudação da sua mídia."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 307c196e-3a50-4f4b-b982-51585448ffc6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 0476c3ba3942b2c5182a34a429909adbf5c75ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-analytics-tooconvert-text-content-in-video-files-into-digital-text"></a>Usar o conteúdo de texto de tooconvert de análise de mídia do Azure em arquivos de vídeo em texto digital
## <a name="overview"></a>Visão geral
Se você precisa texto tooextract conteúdo de seus arquivos de vídeo e gerar um texto editável, pesquisável digital, você deve usar OCR de análise de mídia do Azure (reconhecimento óptico de caracteres). Esse Processador de Mídia do Azure detecta o conteúdo de texto em seus arquivos de vídeo e gera arquivos de texto para seu uso. OCR permite que você tooautomate Olá extração de metadados significativo de sinal de vídeo de saudação da sua mídia.

Quando usado em conjunto com um mecanismo de pesquisa, pode facilmente sua mídia de índice de texto e aumentar a capacidade de descoberta de saudação do seu conteúdo. Isso é extremamente útil em vídeo altamente textual, como uma gravação de vídeo ou captura de tela de uma apresentação de slides. Olá processador de mídia do Azure OCR é otimizado para texto digital.

Olá **OCR de mídia do Azure** processador de mídia está atualmente em visualização.

Este tópico fornece detalhes sobre **OCR de mídia do Azure** e mostra como toouse com o SDK do Media Services para .NET. Para obter informações e exemplos adicionais, consulte [este blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).

## <a name="ocr-input-files"></a>Arquivos de entrada de OCR
Arquivos de vídeo. Atualmente, a saudação formatos a seguir têm suporte: MOV, MP4 e WMV.

## <a name="task-configuration"></a>Configuração de tarefa
Configuração de tarefa (predefinição). Ao criar uma tarefa com o **OCR de Mídia do Azure**, é necessário especificar uma predefinição de configuração usando JSON ou XML. 

>[!NOTE]
>o mecanismo de OCR Olá tem apenas uma região da imagem com pixels de toomaximum 32000 40 pixels mínima como uma entrada válida em ambos os altura/largura.
>

### <a name="attribute-descriptions"></a>Descrições de atributos
| Nome do atributo | Descrição |
| --- | --- |
|AdvancedOutput| Se você definir AdvancedOutput tootrue, a saída JSON de saudação conterá dados posicionais para cada palavra única (em adição toophrases e regiões). Se você não quiser toosee esses detalhes, defina Olá sinalizador toofalse. valor padrão de saudação é false. Para saber mais, confira [este blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).|
| idioma |(opcional) descreve a linguagem de saudação do texto para o qual toolook. Um dos seguintes Olá: detecção automática (padrão), árabe, ChineseSimplified, chinês tradicional, dinamarquês tcheco, holandês, inglês, finlandês, francês, alemão, grego, húngaro, italiano, japonês, coreano, norueguês, polonês, português, romeno, russo, SerbianCyrillic, SerbianLatin, eslovaco, espanhol, sueco, turco. |
| TextOrientation |(opcional) descreve a orientação de saudação do texto para o qual toolook.  "Esquerda" significa que Olá superior de todas as letras é apontada para a esquerda hello.  O texto padrão (como aquele que pode ser encontrado em um livro), tem a orientação “Up”.  Um dos seguintes Olá: detecção automática (padrão), para cima, à direita, à esquerda. |
| TimeInterval |(opcional) descreve a taxa de amostragem de saudação.  O padrão é a cada 1/2 segundo.<br/>Formato JSON – HH:mm:ss.SSS (padrão 00:00:00.500)<br/>Formato XML: duração primitiva do W3C XSD (padrão PT0.5) |
| DetectRegions |(opcional) Uma matriz de objetos DetectRegion especificando regiões dentro de quadros do vídeo Olá na qual o texto toodetect.<br/>Um objeto DetectRegion é composto de saudação quatro valores de inteiro a seguir:<br/>Esquerda – pixels da margem esquerda Olá<br/>Principais – pixels da margem superior Olá<br/>Largura – largura da região de saudação em pixels<br/>Altura – altura da região de saudação em pixels |

#### <a name="json-preset-example"></a>Exemplo de predefinição JSON

    {
        "Version":1.0, 
        "Options": 
        {
            "AdvancedOutput":"true",
            "Language":"English", 
            "TimeInterval":"00:00:01.5",
            "TextOrientation":"Up",
            "DetectRegions": [
                    {
                       "Left": 10,
                       "Top": 10,
                       "Width": 100,
                       "Height": 50
                    }
             ]
        }
    }


#### <a name="xml-preset-example"></a>Exemplo de predefinição XML
    <?xml version=""1.0"" encoding=""utf-16""?>
    <VideoOcrPreset xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" Version=""1.0"" xmlns=""http://www.windowsazure.com/media/encoding/Preset/2014/03"">
      <Options>
         <AdvancedOutput>true</AdvancedOutput>
         <Language>English</Language>
         <TimeInterval>PT1.5S</TimeInterval>
         <DetectRegions>
             <DetectRegion>
                   <Left>10</Left>
                   <Top>10</Top>
                   <Width>100</Width>
                   <Height>50</Height>
            </DetectRegion>
       </DetectRegions>
       <TextOrientation>Up</TextOrientation>
      </Options>
    </VideoOcrPreset>

## <a name="ocr-output-files"></a>Arquivos de saída de OCR
saída de saudação do processador de mídia Olá OCR é um arquivo JSON.

### <a name="elements-of-hello-output-json-file"></a>Elementos Olá JSON do arquivo de saída
saída de vídeo OCR Hello fornece dados segmentados de tempo em caracteres hello encontrados no vídeo.  Você pode usar atributos como o idioma ou orientação toohone no exatamente palavras Olá que você está interessado na análise. 

saída de Hello contém Olá seguintes atributos:

| Elemento | Descrição |
| --- | --- |
| Escala de tempo |"tiques" por segundo de vídeo Olá |
| Deslocamento |diferença de tempo para carimbos de data/hora. Na versão 1.0 das APIs de Vídeo, sempre será 0. |
| Taxa de quadros |Quadros por segundo do hello vídeo |
| width |largura da saudação vídeo em pixels |
| height |altura do vídeo em pixels da saudação |
| Fragmentos |matriz de blocos com base em tempo de vídeo no qual Olá metadados está em bloco |
| iniciar |hora de início de um fragmento em "tiques" |
| duration |duração de um fragmento em "tiques" |
| intervalo |intervalo de cada evento no hello determinado por fragmento |
| events |matriz que contém regiões |
| region |objeto representando palavras ou frases detectadas |
| Linguagem |idioma do texto de saudação detectado dentro de uma região |
| orientation |orientação do texto de saudação detectado dentro de uma região |
| lines |matriz de linhas de texto detectadas em uma região |
| texto |texto real da saudação |

### <a name="json-output-example"></a>Exemplo de saída JSON
Olá saída exemplo a seguir contém informações gerais de vídeo hello e vários fragmentos de vídeo. Em cada fragmento do vídeo, ele contém todas as regiões que é detectada pelo OCR MP com idioma hello e sua orientação de texto. região Olá também contém todas as linhas word nesta região com o texto da linha hello, posição da linha hello e todas as informações de palavra (conteúdo do word, posição e confiança) nesta linha. Olá seguinte é um exemplo e coloquei embutido alguns comentários.

    {
        "version": 1, 
        "timescale": 90000, 
        "offset": 0, 
        "framerate": 30, 
        "width": 640, 
        "height": 480,  // general video information
        "fragments": [
            {
                "start": 0, 
                "duration": 180000, 
                "interval": 90000,  // hello time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // hello detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including hello text and hello position
                                    {
                                        "text": "One Two", 
                                        "left": 10, 
                                        "top": 10, 
                                        "right": 210, 
                                        "bottom": 110, 
                                        "word": [  // word information array in this line
                                            {
                                                "text": "One", 
                                                "left": 10, 
                                                "top": 10, 
                                                "right": 110, 
                                                "bottom": 110, 
                                                "confidence": 900
                                            }, 
                                            {
                                                "text": "Two", 
                                                "left": 110, 
                                                "top": 10, 
                                                "right": 210, 
                                                "bottom": 110, 
                                                "confidence": 910
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                ]
            }
        ]
    }

## <a name="net-sample-code"></a>Código de exemplo do .NET

a seguir Olá programa mostra como:

1. Criar um ativo e carregar um arquivo de mídia no ativo de saudação.
2. Crie um trabalho com um arquivo de configuração/predefinição de OCR.
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

    namespace OCR
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

                // Run hello OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference tooAzure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

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

