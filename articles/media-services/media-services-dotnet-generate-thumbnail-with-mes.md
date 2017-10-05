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
# <a name="how-to-generate-thumbnails-using-media-encoder-standard-with-net"></a><span data-ttu-id="6c936-103">Como gerar miniaturas usando o Codificador de Mídia Padrão com o .NET</span><span class="sxs-lookup"><span data-stu-id="6c936-103">How to generate thumbnails using Media Encoder Standard with .NET</span></span>

<span data-ttu-id="6c936-104">Você pode usar o Media Encoder Standard para gerar uma ou mais miniaturas de sua entrada de vídeo nos formatos de arquivo de imagem [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics) ou [BMP](https://en.wikipedia.org/wiki/BMP_file_format).</span><span class="sxs-lookup"><span data-stu-id="6c936-104">You can use Media Encoder Standard to generate one or more thumbnails from your input video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), or [BMP](https://en.wikipedia.org/wiki/BMP_file_format) image file formats.</span></span> <span data-ttu-id="6c936-105">Você pode enviar Tarefas que geram somente imagens ou pode combinar a geração de miniaturas com codificação.</span><span class="sxs-lookup"><span data-stu-id="6c936-105">You can submit Tasks that produce only images, or you can combine thumbnail generation with encoding.</span></span> <span data-ttu-id="6c936-106">Este tópico apresenta alguns exemplo de predefinições de miniatura em XML e JSON para esses cenários.</span><span class="sxs-lookup"><span data-stu-id="6c936-106">This topic provides a few sample XML and JSON thumbnail presets for such scenarios.</span></span> <span data-ttu-id="6c936-107">No final do tópico, há um [código de exemplo](#code_sample) que mostra como usar o SDK .NET dos Serviços de Mídia para realizar a tarefa de codificação.</span><span class="sxs-lookup"><span data-stu-id="6c936-107">At the end of the topic, there is a [sample code](#code_sample) that shows how to use the Media Services .NET SDK to accomplish the encoding task.</span></span>

<span data-ttu-id="6c936-108">Para obter mais detalhes sobre os elementos usados nas predefinições de exemplo, examine o [esquema do Media Encoder Standard](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="6c936-108">For more details on the elements that are used in sample presets, you should review [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>

<span data-ttu-id="6c936-109">Certifique-se de examinar a seção [Considerações](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) .</span><span class="sxs-lookup"><span data-stu-id="6c936-109">Make sure to review the [Considerations](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) section.</span></span>

## <a name="example--single-png-file"></a><span data-ttu-id="6c936-110">Exemplo – arquivo PNG único</span><span class="sxs-lookup"><span data-stu-id="6c936-110">Example – single PNG file</span></span>

<span data-ttu-id="6c936-111">As predefinições JSON e XML a seguir podem ser usadas para produzir um único arquivo PNG de saída para os primeiros segundos da entrada vídeo, em que o codificador faz uma tentativa de melhor esforço na localização de um quadro "interessante".</span><span class="sxs-lookup"><span data-stu-id="6c936-111">The following JSON and XML preset can be used to produce a single output PNG file out of the first few seconds of the input video, where the encoder makes a best-effort attempt at finding an “interesting” frame.</span></span> <span data-ttu-id="6c936-112">Observe que as dimensões da imagem de saída foram definidas como 100%, o que significa que corresponderão às dimensões do vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="6c936-112">Note that the output image dimensions have been set to 100%, meaning these will match the dimensions of the input video.</span></span> <span data-ttu-id="6c936-113">Observe também como a configuração de "Formato" em "Saídas" deve coincidir com o uso de "PngLayers" na seção "Codecs".</span><span class="sxs-lookup"><span data-stu-id="6c936-113">Note also how the “Format” setting in “Outputs” is required to match the use of “PngLayers” in the “Codecs” section.</span></span> 

### <a name="json-preset"></a><span data-ttu-id="6c936-114">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="6c936-114">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="6c936-115">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="6c936-115">XML preset</span></span>

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

## <a name="example--a-series-of-jpeg-images"></a><span data-ttu-id="6c936-116">Exemplo – uma série de imagens JPEG</span><span class="sxs-lookup"><span data-stu-id="6c936-116">Example – a series of JPEG images</span></span>

<span data-ttu-id="6c936-117">As predefinições JSON e XML a seguir podem ser usadas para produzir um conjunto de 10 imagens em carimbos de data/hora de 5%, 15%, …, 95% da entrada da linha do tempo, em que o tamanho da imagem é especificado como sendo de um quarto daquele do vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="6c936-117">The following JSON and XML preset can be used to produce a set of 10 images at timestamps of 5%, 15%, …, 95% of the input timeline, where the image size is specified to be one quarter that of the input video.</span></span>

### <a name="json-preset"></a><span data-ttu-id="6c936-118">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="6c936-118">JSON preset</span></span>

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

### <a name="xml-preset"></a><span data-ttu-id="6c936-119">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="6c936-119">XML preset</span></span>
    
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

## <a name="example--one-image-at-a-specific-timestamp"></a><span data-ttu-id="6c936-120">Exemplo – uma imagem em um carimbo de data/hora específico</span><span class="sxs-lookup"><span data-stu-id="6c936-120">Example – one image at a specific timestamp</span></span>

<span data-ttu-id="6c936-121">A predefinição JSON e XML a seguir pode ser usada para produzir uma única imagem JPEG na marca de 30 segunda do vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="6c936-121">The following JSON and XML preset can be used to produce a single JPEG image at the 30 second mark of the input video.</span></span> <span data-ttu-id="6c936-122">Essa predefinição espera que a entrada tenha mais de 30 segundos de duração (caso contrário, haverá falha no trabalho).</span><span class="sxs-lookup"><span data-stu-id="6c936-122">This preset expects the input to be more than 30 seconds in duration (else the job will fail).</span></span>

### <a name="json-preset"></a><span data-ttu-id="6c936-123">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="6c936-123">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="6c936-124">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="6c936-124">XML preset</span></span>
    
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

## <span data-ttu-id="6c936-125"><a id="code_sample"></a>Exemplo – codificar o vídeo e gerar a miniatura</span><span class="sxs-lookup"><span data-stu-id="6c936-125"><a id="code_sample"></a>Example – encode video and generate thumbnail</span></span>

<span data-ttu-id="6c936-126">O exemplo de código a seguir usa o SDK .NET dos Serviços de Mídia para executar as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="6c936-126">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

* <span data-ttu-id="6c936-127">Crie um trabalho de codificação.</span><span class="sxs-lookup"><span data-stu-id="6c936-127">Create an encoding job.</span></span>
* <span data-ttu-id="6c936-128">Obtenha uma referência para o Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="6c936-128">Get a reference to the Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="6c936-129">Carregue a predefinição [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) ou [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) que contém a codificação predefinida, assim como as informações necessárias para gerar miniaturas.</span><span class="sxs-lookup"><span data-stu-id="6c936-129">Load the preset [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) that contain the encoding preset as well as information needed to generate thumbnails.</span></span> <span data-ttu-id="6c936-130">Você pode salvar esse [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) ou [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) em um arquivo e usar o código a seguir para carregar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="6c936-130">You can save this  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in a file and use the following code to load the file.</span></span>
  
        // Load the XML (or JSON) from the local file.
        string configuration = File.ReadAllText(fileName);  
* <span data-ttu-id="6c936-131">Adicione uma única tarefa de codificação para o trabalho.</span><span class="sxs-lookup"><span data-stu-id="6c936-131">Add a single encoding task to the job.</span></span> 
* <span data-ttu-id="6c936-132">Especifique o ativo de entrada a ser codificado.</span><span class="sxs-lookup"><span data-stu-id="6c936-132">Specify the input asset to be encoded.</span></span>
* <span data-ttu-id="6c936-133">Crie um ativo de saída que conterá o ativo codificado.</span><span class="sxs-lookup"><span data-stu-id="6c936-133">Create an output asset that will contain the encoded asset.</span></span>
* <span data-ttu-id="6c936-134">Adicione um manipulador de eventos para verificar o progresso do trabalho.</span><span class="sxs-lookup"><span data-stu-id="6c936-134">Add an event handler to check the job progress.</span></span>
* <span data-ttu-id="6c936-135">Enviar o trabalho.</span><span class="sxs-lookup"><span data-stu-id="6c936-135">Submit the job.</span></span>

<span data-ttu-id="6c936-136">Consulte o tópico [Desenvolvimento de Serviços de Mídia com .NET](media-services-dotnet-how-to-use.md) para obter instruções sobre como configurar seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="6c936-136">See the [Media Services development with .NET](media-services-dotnet-how-to-use.md) topic for directions on how to set up your dev environment.</span></span>

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

## <span data-ttu-id="6c936-137"><a id="json"></a>Predefinição JSON em miniatura</span><span class="sxs-lookup"><span data-stu-id="6c936-137"><a id="json"></a>Thumbnail JSON preset</span></span>
<span data-ttu-id="6c936-138">Para obter informações sobre o esquema, consulte [este](https://msdn.microsoft.com/library/mt269962.aspx) tópico.</span><span class="sxs-lookup"><span data-stu-id="6c936-138">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>

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

## <span data-ttu-id="6c936-139"><a id="xml"></a>Predefinição XML em miniatura</span><span class="sxs-lookup"><span data-stu-id="6c936-139"><a id="xml"></a>Thumbnail XML preset</span></span>
<span data-ttu-id="6c936-140">Para obter informações sobre o esquema, consulte [este](https://msdn.microsoft.com/library/mt269962.aspx) tópico.</span><span class="sxs-lookup"><span data-stu-id="6c936-140">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>
    
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

## <a name="considerations"></a><span data-ttu-id="6c936-141">Considerações</span><span class="sxs-lookup"><span data-stu-id="6c936-141">Considerations</span></span>
<span data-ttu-id="6c936-142">As seguintes considerações se aplicam:</span><span class="sxs-lookup"><span data-stu-id="6c936-142">The following considerations apply:</span></span>

* <span data-ttu-id="6c936-143">O uso de carimbos explícitos para Início/Etapa/Intervalo pressupõe que a fonte de entrada tem duração de pelo menos 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="6c936-143">The use of explicit timestamps for Start/Step/Range assumes that the input source is at least 1 minute long.</span></span>
* <span data-ttu-id="6c936-144">Elementos Jpg/Png/BmpImage têm atributos de cadeia de caracteres de Início, Etapa e Intervalo que podem ser interpretados como:</span><span class="sxs-lookup"><span data-stu-id="6c936-144">Jpg/Png/BmpImage elements have Start, Step and Range string attributes – these can be interpreted as:</span></span>
  
  * <span data-ttu-id="6c936-145">Número de quadro se eles forem números inteiros não negativos, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6c936-145">Frame Number if they are non-negative integers, eg.</span></span> <span data-ttu-id="6c936-146">"Start": "120",</span><span class="sxs-lookup"><span data-stu-id="6c936-146">"Start": "120",</span></span>
  * <span data-ttu-id="6c936-147">Relativos à duração da origem se expressos com sufixo %, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6c936-147">Relative to source duration if expressed as %-suffixed, eg.</span></span> <span data-ttu-id="6c936-148">"Start": "15%" OU</span><span class="sxs-lookup"><span data-stu-id="6c936-148">"Start": "15%", OR</span></span>
  * <span data-ttu-id="6c936-149">Carimbo de data/hora se expresso no formato HH:MM:SS…</span><span class="sxs-lookup"><span data-stu-id="6c936-149">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="6c936-150">.</span><span class="sxs-lookup"><span data-stu-id="6c936-150">format.</span></span> <span data-ttu-id="6c936-151">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="6c936-151">Eg.</span></span> <span data-ttu-id="6c936-152">"Start": "00:01:00"</span><span class="sxs-lookup"><span data-stu-id="6c936-152">"Start" : "00:01:00"</span></span>
    
    <span data-ttu-id="6c936-153">Você pode combinar as notações como desejar.</span><span class="sxs-lookup"><span data-stu-id="6c936-153">You can mix and match notations as you please.</span></span>
    
    <span data-ttu-id="6c936-154">Além disso, o Início também dá suporte a uma Macro especial: {Best}, que tenta determinar o primeiro quadro "interessante" da NOTA de conteúdo: (Etapa e Intervalo são ignorados quando Início é definido como {Best})</span><span class="sxs-lookup"><span data-stu-id="6c936-154">Additionally, Start also supports a special Macro:{Best}, which attempts to determine the first “interesting” frame of the content NOTE: (Step and Range are ignored when Start is set to {Best})</span></span>
  * <span data-ttu-id="6c936-155">Padrões: Start:{Best}</span><span class="sxs-lookup"><span data-stu-id="6c936-155">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="6c936-156">O formato de saída precisa ser fornecido explicitamente para cada formato de Imagem: Jpg/Png/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="6c936-156">Output format needs to be explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="6c936-157">Quando presente, o MES corresponderá JpgVideo a JpgFormat e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="6c936-157">When present, MES will match JpgVideo to JpgFormat and so on.</span></span> <span data-ttu-id="6c936-158">OutputFormat introduz uma nova Macro específica do codec de imagem: {Index}, que precisa estar presente (apenas uma vez) para formatos de saída de imagem.</span><span class="sxs-lookup"><span data-stu-id="6c936-158">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs to be present (once and only once) for image output formats.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c936-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6c936-159">Next steps</span></span>

<span data-ttu-id="6c936-160">Você pode verificar o [andamento do trabalho](media-services-check-job-progress.md) enquanto o trabalho de codificação está pendente.</span><span class="sxs-lookup"><span data-stu-id="6c936-160">You can check the [job progress](media-services-check-job-progress.md) while the encoding job is pending.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="6c936-161">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="6c936-161">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6c936-162">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="6c936-162">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="6c936-163">Consulte também</span><span class="sxs-lookup"><span data-stu-id="6c936-163">See Also</span></span>
[<span data-ttu-id="6c936-164">Visão geral da codificação de serviços de mídia</span><span class="sxs-lookup"><span data-stu-id="6c936-164">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

