---
title: "aaaHow toogenerate miniaturas usando o codificador de mídia padrão com .NET"
description: "Este tópico mostra como toouse .NET tooencode um ativo e gerem miniaturas no hello mesmo tempo usando o codificador de mídia padrão."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: b8dab73a-1d91-4b6d-9741-a92ad39fc3f7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: juliako
ms.openlocfilehash: 23d3e4d9bf64a688d45499c045f19d2792167990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-thumbnails-using-media-encoder-standard-with-net"></a>Como miniaturas toogenerate usando o codificador de mídia padrão com .NET

Você pode usar uma ou mais miniaturas de toogenerate codificador de mídia padrão de sua entrada de vídeo de [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), ou [BMP](https://en.wikipedia.org/wiki/BMP_file_format) formatos de arquivo de imagem. Você pode enviar Tarefas que geram somente imagens ou pode combinar a geração de miniaturas com codificação. Este tópico apresenta alguns exemplo de predefinições de miniatura em XML e JSON para esses cenários. Final Olá Olá tópico, há um [código de exemplo](#code_sample) que mostra como toouse Olá SDK do Media Services .NET tooaccomplish Olá tarefa de codificação.

Para obter mais detalhes sobre os elementos de saudação que são usados nas predefinições de exemplo, você deve examinar [esquema padrão do Media Encoder](media-services-mes-schema.md).

Verifique se Olá de tooreview [considerações](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) seção.

## <a name="example--single-png-file"></a>Exemplo – arquivo PNG único

Olá JSON a seguir e predefinição XML pode ser usado tooproduce uma única saída PNG arquivo fora do hello primeiro alguns segundos de vídeo de entrada hello, em que o codificador Olá faz uma tentativa de melhor esforço na localização de um quadro "interessante". Observe que Olá dimensões da imagem de saída foram definidas too100%, que significa que essas dimensões de saudação do vídeo de entrada hello fará a correspondência. Observe também como a configuração de "Format" Olá "Saídas" é necessária toomatch uso hello "PngLayers" na seção de "Codecs" hello. 

### <a name="json-preset"></a>Predefinição JSON

    {
      "Version": 1.0,
      "Codecs": [
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "PngImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a>Predefinição XML

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <PngImage Start="{Best}">
          <PngLayers>
            <PngLayer>
              <Width>100%</Width>
              <Height>100%</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--a-series-of-jpeg-images"></a>Exemplo – uma série de imagens JPEG

Olá JSON a seguir e predefinição XML pode ser usado tooproduce um conjunto de 10 imagens em carimbos de hora de 5% 15%,..., 95% da saudação entrada da linha do tempo, em que o tamanho da imagem Olá é toobe especificado um quarto que Olá vídeo de entrada.

### <a name="json-preset"></a>Predefinição JSON

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "5%",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }

### <a name="xml-preset"></a>Predefinição XML
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="5%" Step="10%" Range="96%">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--one-image-at-a-specific-timestamp"></a>Exemplo – uma imagem em um carimbo de data/hora específico

Olá predefinição JSON e XML a seguir pode ser usado tooproduce 30 segundos de uma única imagem JPEG Olá marcar de vídeo de entrada hello. Essa predefinição espera toobe entrada hello mais de 30 segundos de duração (else hello haverá falha).

### <a name="json-preset"></a>Predefinição JSON

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "00:00:30",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a>Predefinição XML
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="00:00:30" Step="00:00:02" Range="00:00:01">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a id="code_sample"></a>Exemplo – codificar o vídeo e gerar a miniatura

saudação de exemplo de código a seguir usa saudação do SDK do Media Services .NET tooperform tarefas a seguir:

* Crie um trabalho de codificação.
* Obtém um codificador de mídia codificador padrão de toohello de referência.
* Saudação de carga predefinição [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) ou [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) que contêm Olá codificação predefinidos, bem como miniaturas toogenerate as informações necessárias. Você pode salvar esse [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) ou [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) em uma saudação de arquivo e usar arquivo de saudação do tooload de código a seguir.
  
        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(fileName);  
* Adicione um único trabalho de toohello de tarefa de codificação. 
* Especifique a entrada hello toobe ativo codificado.
* Crie um ativo de saída que conterá o ativo de saudação codificado.
* Adicione o andamento do trabalho um evento manipulador toocheck hello.
* Envie trabalho de saudação.

Consulte Olá [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md) tópico para obter instruções sobre como tooset o seu ambiente de desenvolvimento.

        using System;
        using System.Configuration;
        using System.IO;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;

        namespace EncodeAndGenerateThumbnails
        {
        class Program
        {
            // Read values from hello App.config file.
            private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            private static CloudMediaContext _context = null;

            private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

            static void Main(string[] args)
            {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate hello thumbnails.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
            }

            static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
            {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Load hello XML (or JSON) from hello local file.
            string configuration = File.ReadAllText("ThumbnailPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
                processor,
                configuration,
                TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
            }

            private static void JobStateChanged(object sender, JobStateChangedEventArgs e)
            {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);
            switch (e.CurrentState)
            {
                case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("Job is finished. Please wait while local tasks or downloads complete...");
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
                break;
                default:
                break;
            }
            }

            private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
            }
        }
        }

## <a id="json"></a>Predefinição JSON em miniatura
Para obter informações sobre o esquema, consulte [este](https://msdn.microsoft.com/library/mt269962.aspx) tópico.

    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
    
            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Resolution}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <a id="xml"></a>Predefinição XML em miniatura
Para obter informações sobre o esquema, consulte [este](https://msdn.microsoft.com/library/mt269962.aspx) tópico.
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <SceneChangeDetection>true</SceneChangeDetection>
          <H264Layers>
            <H264Layer>
              <Bitrate>4500</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>4500</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>100%</Width>
              <Height>100%/Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Resolution}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="considerations"></a>Considerações
Olá considerações a seguir se aplicam:

* uso de saudação de carimbos de hora explícitos para etapa/intervalo de início pressupõe que dessa fonte de entrada hello é pelo menos 1 minuto.
* Elementos Jpg/Png/BmpImage têm atributos de cadeia de caracteres de Início, Etapa e Intervalo que podem ser interpretados como:
  
  * Número de quadro se eles forem números inteiros não negativos, por exemplo: "Start": "120",
  * Se expresso como sufixo %, por exemplo, a duração do toosource relativo. "Start": "15%" OU
  * Carimbo de data/hora se expresso no formato HH:MM:SS… . Por exemplo, "Start": "00:01:00"
    
    Você pode combinar as notações como desejar.
    
    Além disso, início também suporta uma Macro especial: {melhor}, que tenta toodetermine Olá primeiro "interessante" quadro de conteúdo Olá Observação: (etapa e intervalo são ignorados quando iniciar está definido muito {melhor})
  * Padrões: Start:{Best}
* Formato de saída precisa toobe fornecido explicitamente para cada formato de imagem: Jpg/Png/BmpFormat. Quando presente, MES corresponderá JpgVideo tooJpgFormat e assim por diante. OutputFormat apresenta uma nova Macro específico de codec de imagem: {índice}, que precisa toobe presente (uma vez e apenas uma vez) para formatos de saída de imagem.

## <a name="next-steps"></a>Próximas etapas

Você pode verificar Olá [andamento do trabalho](media-services-check-job-progress.md) durante a saudação trabalho de codificação está pendente.

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Consulte também
[Visão geral da codificação de serviços de mídia](media-services-encode-asset.md)

