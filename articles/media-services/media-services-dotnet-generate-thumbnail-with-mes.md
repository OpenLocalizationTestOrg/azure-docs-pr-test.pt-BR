---
title: "Como gerar miniaturas usando o Codificador de Mídia Padrão com o .NET"
description: "Este tópico mostra como usar o .NET para codificar um ativo e gerar miniaturas simultaneamente usando o Media Encoder Standard."
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
ms.openlocfilehash: 89d15cbdf71a140e78f34e07ff208776b7d4cab3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-generate-thumbnails-using-media-encoder-standard-with-net"></a>Como gerar miniaturas usando o Codificador de Mídia Padrão com o .NET

Você pode usar o Media Encoder Standard para gerar uma ou mais miniaturas de sua entrada de vídeo nos formatos de arquivo de imagem [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics) ou [BMP](https://en.wikipedia.org/wiki/BMP_file_format). Você pode enviar Tarefas que geram somente imagens ou pode combinar a geração de miniaturas com codificação. Este tópico apresenta alguns exemplo de predefinições de miniatura em XML e JSON para esses cenários. No final do tópico, há um [código de exemplo](#code_sample) que mostra como usar o SDK .NET dos Serviços de Mídia para realizar a tarefa de codificação.

Para obter mais detalhes sobre os elementos usados nas predefinições de exemplo, examine o [esquema do Media Encoder Standard](media-services-mes-schema.md).

Certifique-se de examinar a seção [Considerações](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) .

## <a name="example--single-png-file"></a>Exemplo – arquivo PNG único

As predefinições JSON e XML a seguir podem ser usadas para produzir um único arquivo PNG de saída para os primeiros segundos da entrada vídeo, em que o codificador faz uma tentativa de melhor esforço na localização de um quadro "interessante". Observe que as dimensões da imagem de saída foram definidas como 100%, o que significa que corresponderão às dimensões do vídeo de entrada. Observe também como a configuração de "Formato" em "Saídas" deve coincidir com o uso de "PngLayers" na seção "Codecs". 

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

As predefinições JSON e XML a seguir podem ser usadas para produzir um conjunto de 10 imagens em carimbos de data/hora de 5%, 15%, …, 95% da entrada da linha do tempo, em que o tamanho da imagem é especificado como sendo de um quarto daquele do vídeo de entrada.

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

A predefinição JSON e XML a seguir pode ser usada para produzir uma única imagem JPEG na marca de 30 segunda do vídeo de entrada. Essa predefinição espera que a entrada tenha mais de 30 segundos de duração (caso contrário, haverá falha no trabalho).

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

O exemplo de código a seguir usa o SDK .NET dos Serviços de Mídia para executar as seguintes tarefas:

* Crie um trabalho de codificação.
* Obtenha uma referência para o Media Encoder Standard.
* Carregue a predefinição [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) ou [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) que contém a codificação predefinida, assim como as informações necessárias para gerar miniaturas. Você pode salvar esse [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) ou [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) em um arquivo e usar o código a seguir para carregar o arquivo.
  
        // Load the XML (or JSON) from the local file.
        string configuration = File.ReadAllText(fileName);  
* Adicione uma única tarefa de codificação para o trabalho. 
* Especifique o ativo de entrada a ser codificado.
* Crie um ativo de saída que conterá o ativo codificado.
* Adicione um manipulador de eventos para verificar o progresso do trabalho.
* Enviar o trabalho.

Consulte o tópico [Desenvolvimento de Serviços de Mídia com .NET](media-services-dotnet-how-to-use.md) para obter instruções sobre como configurar seu ambiente de desenvolvimento.

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
            // Read values from the App.config file.
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

            // Encode and generate the thumbnails.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
            }

            static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
            {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Load the XML (or JSON) from the local file.
            string configuration = File.ReadAllText("ThumbnailPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
                processor,
                configuration,
                TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
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
As seguintes considerações se aplicam:

* O uso de carimbos explícitos para Início/Etapa/Intervalo pressupõe que a fonte de entrada tem duração de pelo menos 1 minuto.
* Elementos Jpg/Png/BmpImage têm atributos de cadeia de caracteres de Início, Etapa e Intervalo que podem ser interpretados como:
  
  * Número de quadro se eles forem números inteiros não negativos, por exemplo: "Start": "120",
  * Relativos à duração da origem se expressos com sufixo %, por exemplo: "Start": "15%" OU
  * Carimbo de data/hora se expresso no formato HH:MM:SS… . Por exemplo, "Start": "00:01:00"
    
    Você pode combinar as notações como desejar.
    
    Além disso, o Início também dá suporte a uma Macro especial: {Best}, que tenta determinar o primeiro quadro "interessante" da NOTA de conteúdo: (Etapa e Intervalo são ignorados quando Início é definido como {Best})
  * Padrões: Start:{Best}
* O formato de saída precisa ser fornecido explicitamente para cada formato de Imagem: Jpg/Png/BmpFormat. Quando presente, o MES corresponderá JpgVideo a JpgFormat e assim por diante. OutputFormat introduz uma nova Macro específica do codec de imagem: {Index}, que precisa estar presente (apenas uma vez) para formatos de saída de imagem.

## <a name="next-steps"></a>Próximas etapas

Você pode verificar o [andamento do trabalho](media-services-check-job-progress.md) enquanto o trabalho de codificação está pendente.

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Consulte também
[Visão geral da codificação de serviços de mídia](media-services-encode-asset.md)

