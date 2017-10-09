---
title: "as faces aaaRedact com análise de mídia do Azure | Microsoft Docs"
description: "Este tópico demonstra como tooredact faces com análise de mídia do Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5b6d8b8c-5f4d-4fef-b3d6-dc22c6b5a0f5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;
ms.openlocfilehash: 1f5688a8c6374151c526a9c702b904d8c3e46164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a>Edição facial com o Azure Media Analytics
## <a name="overview"></a>Visão geral
**Redactor de mídia do Azure** é um [análise de mídia do Azure](media-services-analytics-overview.md) processador de mídia (MP) que oferece redação face escalonável na nuvem hello. Redação da face permite que você toomodify o vídeo em faces de tooblur de ordem de pessoas selecionadas. Talvez você queira serviço de redação de face toouse Olá em cenários de segurança e mídia públicos. Alguns minutos do que contém várias faces podem levar horas tooredact manualmente, mas com esta face de saudação do serviço redação processo requer apenas algumas etapas simples. Para saber mais, confira [este](https://azure.microsoft.com/blog/azure-media-redactor/)blog.

Este tópico fornece detalhes sobre **Redactor de mídia do Azure** e mostra como toouse com o SDK do Media Services para .NET.

Olá **Redactor de mídia do Azure** MP está atualmente em visualização. Ele está disponível em todas as regiões públicas do Azure, bem como em data centers do Governo dos EUA e da China. Esta visualização está disponível gratuitamente no momento. 

## <a name="face-redaction-modes"></a>Modos de edição facial
Redação facial funciona Detectando as faces em cada quadro de vídeo e controle face Olá objeto ambos frente e para trás no tempo, para que hello mesma pessoa pode ser indefinida de outros ângulos também. Olá processo automatizado de redação é muito complexo e não produzir sempre 100% de saída desejada, por esse motivo, que análise de mídia oferece duas maneiras saída final de saudação toomodify.

No modo totalmente automático de tooa de adição, há um fluxo de trabalho de dois passos que permite Olá seleção de/de-selection de faces encontradas por meio de uma lista de IDs. Além disso, toomake arbitrário por saudação ajustes de quadro MP usa um arquivo de metadados no formato JSON. Esse fluxo de trabalho é dividido nos modos **Analisar** e **Editar**. Você pode combinar dois modos de saudação em uma única passagem que executa ambas as tarefas em um trabalho; Esse modo é chamado **combinada**.

### <a name="combined-mode"></a>Modo Combinado
Esse procedimento produzirá um mp4 editado automaticamente sem qualquer entrada manual.

| Estágio | Nome do Arquivo | Observações |
| --- | --- | --- |
| Ativo de entrada |foo.bar |Vídeo em formato WMV, MOV ou MP4 |
| Configuração de entrada |Predefinição de configuração de tarefa |{'version':'1.0', 'options': {'mode':'combined'}} |
| Ativo de saída |foo_redacted.mp4 |Vídeo com desfoque aplicado |

#### <a name="input-example"></a>Exemplo de entrada:
[veja este vídeo](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a>Exemplo de saída:
[veja este vídeo](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a>Modo Analisar
Olá **analisar** passagem de fluxo de trabalho de dois passos Olá utiliza uma entrada de vídeo e produz um arquivo JSON de locais de face e jpg imagens de cada detectado face.

| Estágio | Nome do Arquivo | Observações |
| --- | --- | --- |
| Ativo de entrada |foo.bar |Vídeo em formato WMV, MPV ou MP4 |
| Configuração de entrada |Predefinição de configuração de tarefa |{'version':'1.0', 'options': {'mode':'analyze'}} |
| Ativo de saída |foo_annotations.json |Dados de anotação da localização dos rostos no formato JSON. Isso pode ser editado por obscurecendo no saudação do toomodify de usuário Olá caixas delimitadoras. Confira o exemplo abaixo. |
| Ativo de saída |foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg] |Jpg cortada de cada detectado face, onde o número de saudação indica labelId Olá da face Olá |

#### <a name="output-example"></a>Exemplo de saída:

    {
      "version": 1,
      "timescale": 24000,
      "offset": 0,
      "framerate": 23.976,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 48048,
          "interval": 1001,
          "events": [
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [
              {
                "index": 13,
                "id": 1138,
                "x": 0.29537,
                "y": -0.18987,
                "width": 0.36239,
                "height": 0.80335
              },
              {
                "index": 13,
                "id": 2028,
                "x": 0.60427,
                "y": 0.16098,
                "width": 0.26958,
                "height": 0.57943
              }
            ],

    … truncated

### <a name="redact-mode"></a>Modo de edição
segundo de aprovação de fluxo de trabalho Olá Olá entra em um grande número de entradas que devem ser combinados em um único ativo.

Isso inclui uma lista de IDs tooblur vídeo original hello e anotações Olá JSON. Esse modo usa Olá anotações tooapply obscurecendo no vídeo de entrada hello.

Hello saída da passagem de analisar Olá não incluir vídeo original hello. Olá vídeo precisa toobe carregado no ativo de entrada hello para tarefas de modo Redact hello e marcada como arquivo principal hello.

| Estágio | Nome do Arquivo | Observações |
| --- | --- | --- |
| Ativo de entrada |foo.bar |Vídeo em formato WMV, MPV ou MP4. O mesmo vídeo da etapa 1. |
| Ativo de entrada |foo_annotations.json |arquivo de metadados de anotações da fase 1, com modificações opcionais. |
| Ativo de entrada |foo_IDList.txt (opcional) |Nova linha opcional lista separada de face tooredact IDs. Se deixado em branco, todas as faces são desfocadas. |
| Configuração de entrada |Predefinição de configuração de tarefa |{'version':'1.0', 'options': {'mode':'redact'}} |
| Ativo de saída |foo_redacted.mp4 |Vídeo com desfoque aplicado com base nas anotações |

#### <a name="example-output"></a>Saída de exemplo
Esta é a saída de saudação de um IDList com uma ID de selecionada.

[veja este vídeo](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

foo_IDList.txt de exemplo
 
     1
     2
     3

## <a name="blur-types"></a>Tipos de desfoque

Em Olá **combinada** ou **Redact** modo, há 5 modos de desfoque diferentes, você pode escolher por meio da configuração de entrada hello JSON: **baixo**, **Med**, **Alta**, **depurar**, e **preto**. Por padrão, **Med** é usado.

Você pode encontrar exemplos de saudação desfoque tipos abaixo.

### <a name="example-json"></a>Exemplo de JSON:

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a>Baixo

![Baixo](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a>Med

![Med](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a>Alto

![Alto](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a>Depurar

![Depurar](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a>Preto

![Preto](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-hello-output-json-file"></a>Elementos Olá JSON do arquivo de saída

Olá MP de redação fornece controle que pode detectar o too64 as faces humana em um quadro de vídeo e detecção de local de face de alta precisão. Faces frontais fornecem Olá obter melhores resultados, enquanto as faces lado e faces pequenas (menor que ou igual a too24x24 pixels) são um desafio.

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a>Código de exemplo do .NET

a seguir Olá programa mostra como:

1. Criar um ativo e carregar um arquivo de mídia no ativo de saudação.
2. Crie um trabalho com uma tarefa de redação de face com base em um arquivo de configuração que contém Olá predefinição json a seguir. 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
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

    namespace FaceRedaction
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

            // Run hello FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download hello job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload hello input media file toostorage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference tooAzure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from hello specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify hello input asset.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

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

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Links relacionados
[Visão geral do Azure Media Services Analytics](media-services-analytics-overview.md)

[Demonstrações do Azure Media Analytics](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

