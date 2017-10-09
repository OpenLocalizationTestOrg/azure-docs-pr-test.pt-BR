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
# <a name="how-toogenerate-thumbnails-using-media-encoder-standard-with-net"></a><span data-ttu-id="03c08-103">Como miniaturas toogenerate usando o codificador de mídia padrão com .NET</span><span class="sxs-lookup"><span data-stu-id="03c08-103">How toogenerate thumbnails using Media Encoder Standard with .NET</span></span>

<span data-ttu-id="03c08-104">Você pode usar uma ou mais miniaturas de toogenerate codificador de mídia padrão de sua entrada de vídeo de [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), ou [BMP](https://en.wikipedia.org/wiki/BMP_file_format) formatos de arquivo de imagem.</span><span class="sxs-lookup"><span data-stu-id="03c08-104">You can use Media Encoder Standard toogenerate one or more thumbnails from your input video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), or [BMP](https://en.wikipedia.org/wiki/BMP_file_format) image file formats.</span></span> <span data-ttu-id="03c08-105">Você pode enviar Tarefas que geram somente imagens ou pode combinar a geração de miniaturas com codificação.</span><span class="sxs-lookup"><span data-stu-id="03c08-105">You can submit Tasks that produce only images, or you can combine thumbnail generation with encoding.</span></span> <span data-ttu-id="03c08-106">Este tópico apresenta alguns exemplo de predefinições de miniatura em XML e JSON para esses cenários.</span><span class="sxs-lookup"><span data-stu-id="03c08-106">This topic provides a few sample XML and JSON thumbnail presets for such scenarios.</span></span> <span data-ttu-id="03c08-107">Final Olá Olá tópico, há um [código de exemplo](#code_sample) que mostra como toouse Olá SDK do Media Services .NET tooaccomplish Olá tarefa de codificação.</span><span class="sxs-lookup"><span data-stu-id="03c08-107">At hello end of hello topic, there is a [sample code](#code_sample) that shows how toouse hello Media Services .NET SDK tooaccomplish hello encoding task.</span></span>

<span data-ttu-id="03c08-108">Para obter mais detalhes sobre os elementos de saudação que são usados nas predefinições de exemplo, você deve examinar [esquema padrão do Media Encoder](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="03c08-108">For more details on hello elements that are used in sample presets, you should review [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>

<span data-ttu-id="03c08-109">Verifique se Olá de tooreview [considerações](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) seção.</span><span class="sxs-lookup"><span data-stu-id="03c08-109">Make sure tooreview hello [Considerations](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) section.</span></span>

## <a name="example--single-png-file"></a><span data-ttu-id="03c08-110">Exemplo – arquivo PNG único</span><span class="sxs-lookup"><span data-stu-id="03c08-110">Example – single PNG file</span></span>

<span data-ttu-id="03c08-111">Olá JSON a seguir e predefinição XML pode ser usado tooproduce uma única saída PNG arquivo fora do hello primeiro alguns segundos de vídeo de entrada hello, em que o codificador Olá faz uma tentativa de melhor esforço na localização de um quadro "interessante".</span><span class="sxs-lookup"><span data-stu-id="03c08-111">hello following JSON and XML preset can be used tooproduce a single output PNG file out of hello first few seconds of hello input video, where hello encoder makes a best-effort attempt at finding an “interesting” frame.</span></span> <span data-ttu-id="03c08-112">Observe que Olá dimensões da imagem de saída foram definidas too100%, que significa que essas dimensões de saudação do vídeo de entrada hello fará a correspondência.</span><span class="sxs-lookup"><span data-stu-id="03c08-112">Note that hello output image dimensions have been set too100%, meaning these will match hello dimensions of hello input video.</span></span> <span data-ttu-id="03c08-113">Observe também como a configuração de "Format" Olá "Saídas" é necessária toomatch uso hello "PngLayers" na seção de "Codecs" hello.</span><span class="sxs-lookup"><span data-stu-id="03c08-113">Note also how hello “Format” setting in “Outputs” is required toomatch hello use of “PngLayers” in hello “Codecs” section.</span></span> 

### <a name="json-preset"></a><span data-ttu-id="03c08-114">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="03c08-114">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="03c08-115">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="03c08-115">XML preset</span></span>

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

## <a name="example--a-series-of-jpeg-images"></a><span data-ttu-id="03c08-116">Exemplo – uma série de imagens JPEG</span><span class="sxs-lookup"><span data-stu-id="03c08-116">Example – a series of JPEG images</span></span>

<span data-ttu-id="03c08-117">Olá JSON a seguir e predefinição XML pode ser usado tooproduce um conjunto de 10 imagens em carimbos de hora de 5% 15%,..., 95% da saudação entrada da linha do tempo, em que o tamanho da imagem Olá é toobe especificado um quarto que Olá vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="03c08-117">hello following JSON and XML preset can be used tooproduce a set of 10 images at timestamps of 5%, 15%, …, 95% of hello input timeline, where hello image size is specified toobe one quarter that of hello input video.</span></span>

### <a name="json-preset"></a><span data-ttu-id="03c08-118">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="03c08-118">JSON preset</span></span>

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

### <a name="xml-preset"></a><span data-ttu-id="03c08-119">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="03c08-119">XML preset</span></span>
    
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

## <a name="example--one-image-at-a-specific-timestamp"></a><span data-ttu-id="03c08-120">Exemplo – uma imagem em um carimbo de data/hora específico</span><span class="sxs-lookup"><span data-stu-id="03c08-120">Example – one image at a specific timestamp</span></span>

<span data-ttu-id="03c08-121">Olá predefinição JSON e XML a seguir pode ser usado tooproduce 30 segundos de uma única imagem JPEG Olá marcar de vídeo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="03c08-121">hello following JSON and XML preset can be used tooproduce a single JPEG image at hello 30 second mark of hello input video.</span></span> <span data-ttu-id="03c08-122">Essa predefinição espera toobe entrada hello mais de 30 segundos de duração (else hello haverá falha).</span><span class="sxs-lookup"><span data-stu-id="03c08-122">This preset expects hello input toobe more than 30 seconds in duration (else hello job will fail).</span></span>

### <a name="json-preset"></a><span data-ttu-id="03c08-123">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="03c08-123">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="03c08-124">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="03c08-124">XML preset</span></span>
    
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

## <span data-ttu-id="03c08-125"><a id="code_sample"></a>Exemplo – codificar o vídeo e gerar a miniatura</span><span class="sxs-lookup"><span data-stu-id="03c08-125"><a id="code_sample"></a>Example – encode video and generate thumbnail</span></span>

<span data-ttu-id="03c08-126">saudação de exemplo de código a seguir usa saudação do SDK do Media Services .NET tooperform tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="03c08-126">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

* <span data-ttu-id="03c08-127">Crie um trabalho de codificação.</span><span class="sxs-lookup"><span data-stu-id="03c08-127">Create an encoding job.</span></span>
* <span data-ttu-id="03c08-128">Obtém um codificador de mídia codificador padrão de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="03c08-128">Get a reference toohello Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="03c08-129">Saudação de carga predefinição [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) ou [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) que contêm Olá codificação predefinidos, bem como miniaturas toogenerate as informações necessárias.</span><span class="sxs-lookup"><span data-stu-id="03c08-129">Load hello preset [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) that contain hello encoding preset as well as information needed toogenerate thumbnails.</span></span> <span data-ttu-id="03c08-130">Você pode salvar esse [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) ou [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) em uma saudação de arquivo e usar arquivo de saudação do tooload de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="03c08-130">You can save this  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in a file and use hello following code tooload hello file.</span></span>
  
        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(fileName);  
* <span data-ttu-id="03c08-131">Adicione um único trabalho de toohello de tarefa de codificação.</span><span class="sxs-lookup"><span data-stu-id="03c08-131">Add a single encoding task toohello job.</span></span> 
* <span data-ttu-id="03c08-132">Especifique a entrada hello toobe ativo codificado.</span><span class="sxs-lookup"><span data-stu-id="03c08-132">Specify hello input asset toobe encoded.</span></span>
* <span data-ttu-id="03c08-133">Crie um ativo de saída que conterá o ativo de saudação codificado.</span><span class="sxs-lookup"><span data-stu-id="03c08-133">Create an output asset that will contain hello encoded asset.</span></span>
* <span data-ttu-id="03c08-134">Adicione o andamento do trabalho um evento manipulador toocheck hello.</span><span class="sxs-lookup"><span data-stu-id="03c08-134">Add an event handler toocheck hello job progress.</span></span>
* <span data-ttu-id="03c08-135">Envie trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="03c08-135">Submit hello job.</span></span>

<span data-ttu-id="03c08-136">Consulte Olá [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md) tópico para obter instruções sobre como tooset o seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="03c08-136">See hello [Media Services development with .NET](media-services-dotnet-how-to-use.md) topic for directions on how tooset up your dev environment.</span></span>

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

## <span data-ttu-id="03c08-137"><a id="json"></a>Predefinição JSON em miniatura</span><span class="sxs-lookup"><span data-stu-id="03c08-137"><a id="json"></a>Thumbnail JSON preset</span></span>
<span data-ttu-id="03c08-138">Para obter informações sobre o esquema, consulte [este](https://msdn.microsoft.com/library/mt269962.aspx) tópico.</span><span class="sxs-lookup"><span data-stu-id="03c08-138">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>

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

## <span data-ttu-id="03c08-139"><a id="xml"></a>Predefinição XML em miniatura</span><span class="sxs-lookup"><span data-stu-id="03c08-139"><a id="xml"></a>Thumbnail XML preset</span></span>
<span data-ttu-id="03c08-140">Para obter informações sobre o esquema, consulte [este](https://msdn.microsoft.com/library/mt269962.aspx) tópico.</span><span class="sxs-lookup"><span data-stu-id="03c08-140">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>
    
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

## <a name="considerations"></a><span data-ttu-id="03c08-141">Considerações</span><span class="sxs-lookup"><span data-stu-id="03c08-141">Considerations</span></span>
<span data-ttu-id="03c08-142">Olá considerações a seguir se aplicam:</span><span class="sxs-lookup"><span data-stu-id="03c08-142">hello following considerations apply:</span></span>

* <span data-ttu-id="03c08-143">uso de saudação de carimbos de hora explícitos para etapa/intervalo de início pressupõe que dessa fonte de entrada hello é pelo menos 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="03c08-143">hello use of explicit timestamps for Start/Step/Range assumes that hello input source is at least 1 minute long.</span></span>
* <span data-ttu-id="03c08-144">Elementos Jpg/Png/BmpImage têm atributos de cadeia de caracteres de Início, Etapa e Intervalo que podem ser interpretados como:</span><span class="sxs-lookup"><span data-stu-id="03c08-144">Jpg/Png/BmpImage elements have Start, Step and Range string attributes – these can be interpreted as:</span></span>
  
  * <span data-ttu-id="03c08-145">Número de quadro se eles forem números inteiros não negativos, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="03c08-145">Frame Number if they are non-negative integers, eg.</span></span> <span data-ttu-id="03c08-146">"Start": "120",</span><span class="sxs-lookup"><span data-stu-id="03c08-146">"Start": "120",</span></span>
  * <span data-ttu-id="03c08-147">Se expresso como sufixo %, por exemplo, a duração do toosource relativo.</span><span class="sxs-lookup"><span data-stu-id="03c08-147">Relative toosource duration if expressed as %-suffixed, eg.</span></span> <span data-ttu-id="03c08-148">"Start": "15%" OU</span><span class="sxs-lookup"><span data-stu-id="03c08-148">"Start": "15%", OR</span></span>
  * <span data-ttu-id="03c08-149">Carimbo de data/hora se expresso no formato HH:MM:SS…</span><span class="sxs-lookup"><span data-stu-id="03c08-149">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="03c08-150">.</span><span class="sxs-lookup"><span data-stu-id="03c08-150">format.</span></span> <span data-ttu-id="03c08-151">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="03c08-151">Eg.</span></span> <span data-ttu-id="03c08-152">"Start": "00:01:00"</span><span class="sxs-lookup"><span data-stu-id="03c08-152">"Start" : "00:01:00"</span></span>
    
    <span data-ttu-id="03c08-153">Você pode combinar as notações como desejar.</span><span class="sxs-lookup"><span data-stu-id="03c08-153">You can mix and match notations as you please.</span></span>
    
    <span data-ttu-id="03c08-154">Além disso, início também suporta uma Macro especial: {melhor}, que tenta toodetermine Olá primeiro "interessante" quadro de conteúdo Olá Observação: (etapa e intervalo são ignorados quando iniciar está definido muito {melhor})</span><span class="sxs-lookup"><span data-stu-id="03c08-154">Additionally, Start also supports a special Macro:{Best}, which attempts toodetermine hello first “interesting” frame of hello content NOTE: (Step and Range are ignored when Start is set too{Best})</span></span>
  * <span data-ttu-id="03c08-155">Padrões: Start:{Best}</span><span class="sxs-lookup"><span data-stu-id="03c08-155">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="03c08-156">Formato de saída precisa toobe fornecido explicitamente para cada formato de imagem: Jpg/Png/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="03c08-156">Output format needs toobe explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="03c08-157">Quando presente, MES corresponderá JpgVideo tooJpgFormat e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="03c08-157">When present, MES will match JpgVideo tooJpgFormat and so on.</span></span> <span data-ttu-id="03c08-158">OutputFormat apresenta uma nova Macro específico de codec de imagem: {índice}, que precisa toobe presente (uma vez e apenas uma vez) para formatos de saída de imagem.</span><span class="sxs-lookup"><span data-stu-id="03c08-158">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs toobe present (once and only once) for image output formats.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03c08-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="03c08-159">Next steps</span></span>

<span data-ttu-id="03c08-160">Você pode verificar Olá [andamento do trabalho](media-services-check-job-progress.md) durante a saudação trabalho de codificação está pendente.</span><span class="sxs-lookup"><span data-stu-id="03c08-160">You can check hello [job progress](media-services-check-job-progress.md) while hello encoding job is pending.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="03c08-161">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="03c08-161">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="03c08-162">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="03c08-162">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="03c08-163">Consulte também</span><span class="sxs-lookup"><span data-stu-id="03c08-163">See Also</span></span>
[<span data-ttu-id="03c08-164">Visão geral da codificação de serviços de mídia</span><span class="sxs-lookup"><span data-stu-id="03c08-164">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

