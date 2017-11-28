---
title: "aaaPerform avançado personalizando MES predefinições de codificação | Microsoft Docs"
description: "Este tópico mostra como tooperform avançados de codificação Personalizando o codificador de mídia padrão predefinições de tarefa."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 2a4ade25-e600-4bce-a66e-e29cf4a38369
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 9caa68fafacaf51f91f0554c5bafe491928d8c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a><span data-ttu-id="01867-103">Executar a codificação avançada personalizando predefinições de MES</span><span class="sxs-lookup"><span data-stu-id="01867-103">Perform advanced encoding by customizing MES presets</span></span> 

## <a name="overview"></a><span data-ttu-id="01867-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="01867-104">Overview</span></span>

<span data-ttu-id="01867-105">Este tópico mostra como predefinições de codificador de mídia padrão de toocustomize.</span><span class="sxs-lookup"><span data-stu-id="01867-105">This topic shows how toocustomize Media Encoder Standard presets.</span></span> <span data-ttu-id="01867-106">Olá [codificação com codificador de mídia padrão usando predefinições personalizadas](media-services-custom-mes-presets-with-dotnet.md) tópico mostra como toouse .NET toocreate uma codificação de tarefas e um trabalho que executa essa tarefa.</span><span class="sxs-lookup"><span data-stu-id="01867-106">hello [Encoding with Media Encoder Standard using custom presets](media-services-custom-mes-presets-with-dotnet.md) topic shows how toouse .NET toocreate an encoding task and a job that executes this task.</span></span> <span data-ttu-id="01867-107">Quando você personalizar uma predefinição de tarefa de codificação do fornecimento Olá predefinições personalizadas toohello.</span><span class="sxs-lookup"><span data-stu-id="01867-107">Once you customize a preset, supply hello custom presets toohello encoding task.</span></span> 

>[!NOTE]
><span data-ttu-id="01867-108">Se usando uma predefinição XML, certifique-se de ordem de saudação toopreserve dos elementos, conforme mostrado nos exemplos XML abaixo (por exemplo, KeyFrameInterval deve preceder SceneChangeDetection).</span><span class="sxs-lookup"><span data-stu-id="01867-108">If using an XML preset, make sure toopreserve hello order of elements, as shown in XML samples below (for example, KeyFrameInterval should precede SceneChangeDetection).</span></span>
>

<span data-ttu-id="01867-109">Neste tópico, predefinições personalizadas de saudação que executam Olá tarefas de codificação a seguir são demonstradas.</span><span class="sxs-lookup"><span data-stu-id="01867-109">In this topic, hello custom presets that perform hello following encoding tasks are demonstrated.</span></span>

## <a name="support-for-relative-sizes"></a><span data-ttu-id="01867-110">Suporte para tamanhos relativos</span><span class="sxs-lookup"><span data-stu-id="01867-110">Support for relative sizes</span></span>

<span data-ttu-id="01867-111">Ao gerar miniaturas, não é necessário tooalways especificar saída largura e altura em pixels.</span><span class="sxs-lookup"><span data-stu-id="01867-111">When generating thumbnails, you do not need tooalways specify output width and height in pixels.</span></span> <span data-ttu-id="01867-112">Você pode especificá-los em porcentagens, no intervalo de saudação [% 1, …, 100%].</span><span class="sxs-lookup"><span data-stu-id="01867-112">You can specify them in percentages, in hello range [1%, …, 100%].</span></span>

### <a name="json-preset"></a><span data-ttu-id="01867-113">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="01867-113">JSON preset</span></span>
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a><span data-ttu-id="01867-114">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="01867-114">XML preset</span></span>
    <Width>100%</Width>
    <Height>100%</Height>

## <span data-ttu-id="01867-115"><a id="thumbnails"></a>Gerar miniaturas</span><span class="sxs-lookup"><span data-stu-id="01867-115"><a id="thumbnails"></a>Generate thumbnails</span></span>

<span data-ttu-id="01867-116">Esta seção mostra como toocustomize uma predefinição que gera miniaturas.</span><span class="sxs-lookup"><span data-stu-id="01867-116">This section shows how toocustomize a preset that generates thumbnails.</span></span> <span data-ttu-id="01867-117">Olá predefinição definida abaixo contém informações sobre como você deseja tooencode seu arquivo, bem como miniaturas toogenerate as informações necessárias.</span><span class="sxs-lookup"><span data-stu-id="01867-117">hello preset defined below contains information on how you want tooencode your file as well as information needed toogenerate thumbnails.</span></span> <span data-ttu-id="01867-118">Você pode executar qualquer uma das predefinições MES Olá documentadas [isso](media-services-mes-presets-overview.md) seção e adicione o código que gera miniaturas.</span><span class="sxs-lookup"><span data-stu-id="01867-118">You can take any of hello MES presets documented [this](media-services-mes-presets-overview.md) section and add code that generates thumbnails.</span></span>  

> [!NOTE]
> <span data-ttu-id="01867-119">Olá **SceneChangeDetection** configuração Olá predefinidas a seguir só pode ser definida tootrue se a codificação de vídeo de taxa de bits única tooa.</span><span class="sxs-lookup"><span data-stu-id="01867-119">hello **SceneChangeDetection** setting in hello following preset can only be set tootrue if you are encoding tooa single  bitrate video.</span></span> <span data-ttu-id="01867-120">Se você estiver codificando tooa várias taxas de bits vídeo e defina **SceneChangeDetection** tootrue, o codificador Olá retornará um erro.</span><span class="sxs-lookup"><span data-stu-id="01867-120">If you are encoding tooa multi-bitrate video and set **SceneChangeDetection** tootrue, hello encoder returns an error.</span></span>  
>
>

<span data-ttu-id="01867-121">Para obter informações sobre o esquema, consulte [este](media-services-mes-schema.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="01867-121">For information about schema, see [this](media-services-mes-schema.md) topic.</span></span>

<span data-ttu-id="01867-122">Verifique se Olá de tooreview [considerações](#considerations) seção.</span><span class="sxs-lookup"><span data-stu-id="01867-122">Make sure tooreview hello [Considerations](#considerations) section.</span></span>

### <span data-ttu-id="01867-123"><a id="json"></a>Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="01867-123"><a id="json"></a>JSON preset</span></span>
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
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": 640,
              "Height": 360,
            }
          ],
          "Start": "00:00:01",
          "Step": "00:00:10",
          "Range": "00:00:58",
          "Type": "PngImage"
        },
        {
          "BmpLayers": [
            {
              "Type": "BmpLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "10%",
          "Step": "10%",
          "Range": "90%",
          "Type": "BmpImage"
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
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "BmpFormat"
          }
        },
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <span data-ttu-id="01867-124"><a id="xml"></a>Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="01867-124"><a id="xml"></a>XML preset</span></span>
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
              <Width>640</Width>
              <Height>360</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
        <BmpImage Start="10%" Step="10%" Range="90%">
          <BmpLayers>
            <BmpLayer>
              <Width>640</Width>
              <Height>360</Height>
            </BmpLayer>
          </BmpLayers>
        </BmpImage>
        <PngImage Start="00:00:01" Step="00:00:10" Range="00:00:58">
          <PngLayers>
            <PngLayer>
              <Width>640</Width>
              <Height>360</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <BmpFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

### <a name="considerations"></a><span data-ttu-id="01867-125">Considerações</span><span class="sxs-lookup"><span data-stu-id="01867-125">Considerations</span></span>

<span data-ttu-id="01867-126">Olá considerações a seguir se aplicam:</span><span class="sxs-lookup"><span data-stu-id="01867-126">hello following considerations apply:</span></span>

* <span data-ttu-id="01867-127">uso de saudação de carimbos de hora explícitos para etapa/intervalo de início pressupõe que dessa fonte de entrada hello é pelo menos 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="01867-127">hello use of explicit timestamps for Start/Step/Range assumes that hello input source is at least 1 minute long.</span></span>
* <span data-ttu-id="01867-128">Elementos Jpg/Png/BmpImage têm atributos de cadeia de caracteres de Início, Etapa e Intervalo que podem ser interpretados como:</span><span class="sxs-lookup"><span data-stu-id="01867-128">Jpg/Png/BmpImage elements have Start, Step, and Range string attributes – these can be interpreted as:</span></span>

  * <span data-ttu-id="01867-129">Número de quadro se eles forem números inteiros não negativos, por exemplo, "Início": "120",</span><span class="sxs-lookup"><span data-stu-id="01867-129">Frame Number if they are non-negative integers, for example "Start": "120",</span></span>
  * <span data-ttu-id="01867-130">Duração toosource relativo se expresso como sufixo %, por exemplo "início": "15%", ou</span><span class="sxs-lookup"><span data-stu-id="01867-130">Relative toosource duration if expressed as %-suffixed, for example "Start": "15%", OR</span></span>
  * <span data-ttu-id="01867-131">Carimbo de data/hora se expresso no formato HH:MM:SS…</span><span class="sxs-lookup"><span data-stu-id="01867-131">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="01867-132">formato, por exemplo "Start" : "00:01:00"</span><span class="sxs-lookup"><span data-stu-id="01867-132">format, for example "Start" : "00:01:00"</span></span>

    <span data-ttu-id="01867-133">Você pode combinar as notações como desejar.</span><span class="sxs-lookup"><span data-stu-id="01867-133">You can mix and match notations as you please.</span></span>

    <span data-ttu-id="01867-134">Além disso, início também suporta uma Macro especial: {melhor}, que tenta toodetermine Olá primeiro "interessante" quadro de conteúdo Olá Observação: (etapa e intervalo são ignorados quando iniciar está definido muito {melhor})</span><span class="sxs-lookup"><span data-stu-id="01867-134">Additionally, Start also supports a special Macro:{Best}, which attempts toodetermine hello first “interesting” frame of hello content NOTE: (Step and Range are ignored when Start is set too{Best})</span></span>
  * <span data-ttu-id="01867-135">Padrões: Start:{Best}</span><span class="sxs-lookup"><span data-stu-id="01867-135">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="01867-136">Formato de saída precisa toobe fornecido explicitamente para cada formato de imagem: Jpg/Png/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="01867-136">Output format needs toobe explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="01867-137">Quando presente, MES corresponde JpgVideo tooJpgFormat e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="01867-137">When present, MES matches JpgVideo tooJpgFormat and so on.</span></span> <span data-ttu-id="01867-138">OutputFormat apresenta uma nova Macro específico de codec de imagem: {índice}, que precisa toobe presente (uma vez e apenas uma vez) para formatos de saída de imagem.</span><span class="sxs-lookup"><span data-stu-id="01867-138">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs toobe present (once and only once) for image output formats.</span></span>

## <span data-ttu-id="01867-139"><a id="trim_video"></a>Cortar um vídeo (recorte)</span><span class="sxs-lookup"><span data-stu-id="01867-139"><a id="trim_video"></a>Trim a video (clipping)</span></span>
<span data-ttu-id="01867-140">Esta seção explica modificando codificador Olá predefinições tooclip ou cortar o vídeo de entrada hello onde Olá entrada é um arquivo de mezanino chamados ou sob demanda.</span><span class="sxs-lookup"><span data-stu-id="01867-140">This section talks about modifying hello encoder presets tooclip or trim hello input video where hello input is a so-called mezzanine file or on-demand file.</span></span> <span data-ttu-id="01867-141">Hello codificador também pode ser usado tooclip ou cortar um ativo, o que é capturado ou arquivado a partir de um fluxo ao vivo – Olá detalhes para este estão disponíveis no [este blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="01867-141">hello encoder can also be used tooclip or trim an asset, which is captured or archived from a live stream – hello details for this are available in [this blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span></span>

<span data-ttu-id="01867-142">tootrim vídeos, você pode executar qualquer uma das predefinições MES Olá documentadas [isso](media-services-mes-presets-overview.md) seção e modificar Olá **fontes** elemento (conforme mostrado abaixo).</span><span class="sxs-lookup"><span data-stu-id="01867-142">tootrim your videos, you can take any of hello MES presets documented [this](media-services-mes-presets-overview.md) section and modify hello **Sources** element (as shown below).</span></span> <span data-ttu-id="01867-143">Olá. o valor de StartTime deve toomatch Olá absoluto carimbos de hora de vídeo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="01867-143">hello value of StartTime needs toomatch hello absolute timestamps of hello input video.</span></span> <span data-ttu-id="01867-144">Por exemplo, se hello primeiro quadro de vídeo de entrada hello tem um carimbo de hora de 12:00:10.000, StartTime deve ser pelo menos 12:00:10.000 e maior.</span><span class="sxs-lookup"><span data-stu-id="01867-144">For example, if hello first frame of hello input video has a timestamp of 12:00:10.000, then StartTime should be at least 12:00:10.000 and greater.</span></span> <span data-ttu-id="01867-145">O exemplo hello abaixo, presumimos Olá vídeo de entrada tem um carimbo de hora inicial igual a zero.</span><span class="sxs-lookup"><span data-stu-id="01867-145">In hello example below, we assume that hello input video has a starting timestamp of zero.</span></span> <span data-ttu-id="01867-146">**Fontes** deve ser colocado no início de saudação do hello predefinição.</span><span class="sxs-lookup"><span data-stu-id="01867-146">**Sources** should be placed at hello beginning of hello preset.</span></span>

### <span data-ttu-id="01867-147"><a id="json"></a>Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="01867-147"><a id="json"></a>JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "StartTime": "00:00:04",
          "Duration": "00:00:16"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1500,
              "MaxBitrate": 1500,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1000,
              "MaxBitrate": 1000,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 650,
              "MaxBitrate": 650,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 400,
              "MaxBitrate": 400,
              "BufferWindow": "00:00:05",
              "Width": 320,
              "Height": 180,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="xml-preset"></a><span data-ttu-id="01867-148">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="01867-148">XML preset</span></span>
<span data-ttu-id="01867-149">tootrim vídeos, você pode executar qualquer uma das predefinições MES Olá documentadas [aqui](media-services-mes-presets-overview.md) e modificar Olá **fontes** elemento (conforme mostrado abaixo).</span><span class="sxs-lookup"><span data-stu-id="01867-149">tootrim your videos, you can take any of hello MES presets documented [here](media-services-mes-presets-overview.md) and modify hello **Sources** element (as shown below).</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source StartTime="PT4S" Duration="PT14S"/>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>3400</Bitrate>
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
              <MaxBitrate>3400</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>2250</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>2250</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1500</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1500</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1000</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1000</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>650</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>650</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>400</Bitrate>
              <Width>320</Width>
              <Height>180</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>400</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>

## <span data-ttu-id="01867-150"><a id="overlay"></a>Criar uma sobreposição</span><span class="sxs-lookup"><span data-stu-id="01867-150"><a id="overlay"></a>Create an overlay</span></span>

<span data-ttu-id="01867-151">Olá codificador de mídia padrão permite que você toooverlay uma imagem em um vídeo existente.</span><span class="sxs-lookup"><span data-stu-id="01867-151">hello Media Encoder Standard allows you toooverlay an image onto an existing video.</span></span> <span data-ttu-id="01867-152">Atualmente, a saudação formatos a seguir têm suporte: png, jpg, gif e bmp.</span><span class="sxs-lookup"><span data-stu-id="01867-152">Currently, hello following formats are supported: png, jpg, gif, and bmp.</span></span> <span data-ttu-id="01867-153">Olá predefinição definida abaixo é um exemplo básico de uma sobreposição de vídeo.</span><span class="sxs-lookup"><span data-stu-id="01867-153">hello preset defined below is a basic example  of a video overlay.</span></span>

<span data-ttu-id="01867-154">Além disso toodefining um arquivo predefinido, você também tem os serviços de mídia toolet saber qual arquivo de ativo de saudação é Olá sobreposição de imagem e qual arquivo de vídeo de origem Olá no qual você deseja toooverlay imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="01867-154">In addition toodefining a preset file, you also have toolet Media Services know which file in hello asset is hello overlay image and which file is hello source video onto which you want toooverlay hello image.</span></span> <span data-ttu-id="01867-155">arquivo de vídeo Olá tem Olá toobe **primário** arquivo.</span><span class="sxs-lookup"><span data-stu-id="01867-155">hello video file has toobe hello **primary** file.</span></span>

<span data-ttu-id="01867-156">Se você estiver usando .NET, adicione Olá após duas funções de exemplo do .NET toohello definido em [isso](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) tópico.</span><span class="sxs-lookup"><span data-stu-id="01867-156">If you are using .NET, add hello following two functions toohello .NET example defined in [this](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic.</span></span> <span data-ttu-id="01867-157">Olá **UploadMediaFilesFromFolder** função uploads de arquivos de uma pasta (por exemplo, BigBuckBunny.mp4 e Image001.png) e conjuntos de Olá arquivo toobe Olá primário arquivo mp4 no ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="01867-157">hello **UploadMediaFilesFromFolder** function uploads files from a folder (for example, BigBuckBunny.mp4 and Image001.png) and sets hello mp4 file toobe hello primary file in hello asset.</span></span> <span data-ttu-id="01867-158">Olá **EncodeWithOverlay** função usa Olá arquivo predefinido personalizado que foi passado tooit (por exemplo, Olá predefinição que segue) toocreate Olá tarefa de codificação.</span><span class="sxs-lookup"><span data-stu-id="01867-158">hello **EncodeWithOverlay** function uses hello custom preset file that was passed tooit (for example, hello preset that follows) toocreate hello encoding task.</span></span>


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // hello following code assumes 
            // you have an input folder with one MP4 and one overlay image file.
            if (af.Name.Contains(".mp4"))
                af.IsPrimary = true;
            else
                af.IsPrimary = false;
    
            af.Update();
        }
    
        return asset;
    }

    static public IAsset EncodeWithOverlay(IAsset assetSource, string customPresetFileName)
    {
        // Declare a new job.
        IJob job = _context.Jobs.Create("Media Encoder Standard Job");
        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input assets toobe encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset toocontain hello results of hello job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> <span data-ttu-id="01867-159">Limitações atuais:</span><span class="sxs-lookup"><span data-stu-id="01867-159">Current limitations:</span></span>
>
> <span data-ttu-id="01867-160">Não há suporte para a configuração de opacidade de sobreposição de saudação.</span><span class="sxs-lookup"><span data-stu-id="01867-160">hello overlay opacity setting is not supported.</span></span>
>
> <span data-ttu-id="01867-161">O arquivo de vídeo de origem e o arquivo de imagem de sobreposição de saudação têm toobe em Olá mesmo ativo e Olá conjunto do arquivo de vídeo necessidades toobe como arquivo principal de saudação nesse ativo.</span><span class="sxs-lookup"><span data-stu-id="01867-161">Your source video file and hello overlay image file have toobe in hello same asset, and hello video file needs toobe set as hello primary file in this asset.</span></span>
>
>

### <a name="json-preset"></a><span data-ttu-id="01867-162">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="01867-162">JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "VideoOverlay": {
              "Position": {
                "X": 100,
                "Y": 100,
                "Width": 100,
                "Height": 50
              },
              "AudioGainLevel": 0.0,
              "MediaParams": [
                {
                  "OverlayLoopCount": 1
                },
                {
                  "IsOverlay": true,
                  "OverlayLoopCount": 1,
                  "InputLoop": true
                }
              ],
              "Source": "Image001.png",
              "Clip": {
                "Duration": "00:00:05"
              },
              "FadeInDuration": {
                "Duration": "00:00:01"
              },
              "FadeOutDuration": {
                "StartTime": "00:00:03",
                "Duration": "00:00:04"
              }
            }
          },
          "Pad": true
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1045,
              "MaxBitrate": 1045,
              "BufferWindow": "00:00:05",
              "ReferenceFrames": 3,
              "EntropyMode": "Cavlc",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Type": "CopyAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}{Extension}",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a name="xml-preset"></a><span data-ttu-id="01867-163">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="01867-163">XML preset</span></span>
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source>
          <Streams />
          <Filters>
            <VideoOverlay>
              <Source>Image001.png</Source>
              <Clip Duration="PT5S" />
              <FadeInDuration Duration="PT1S" />
              <FadeOutDuration StartTime="PT3S" Duration="PT4S" />
              <Position X="100" Y="100" Width="100" Height="50" />
              <Opacity>0</Opacity>
              <AudioGainLevel>0</AudioGainLevel>
              <MediaParams>
                <MediaParam>
                  <IsOverlay>false</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>false</InputLoop>
                </MediaParam>
                <MediaParam>
                  <IsOverlay>true</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>true</InputLoop>
                </MediaParam>
              </MediaParams>
            </VideoOverlay>
          </Filters>
          <Pad>true</Pad>
        </Source>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>1045</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>0</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cavlc</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1045</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <CopyAudio />
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}{Extension}">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>


## <span data-ttu-id="01867-164"><a id="silent_audio"></a>Inserir uma faixa de áudio silenciosa quando a entrada não tiver áudio</span><span class="sxs-lookup"><span data-stu-id="01867-164"><a id="silent_audio"></a>Insert a silent audio track when input has no audio</span></span>
<span data-ttu-id="01867-165">Por padrão, se você enviar um codificador de toohello de entrada que contenha apenas vídeo e nenhum áudio, em seguida, Olá ativo de saída contém de arquivos que contêm dados de apenas vídeo.</span><span class="sxs-lookup"><span data-stu-id="01867-165">By default, if you send an input toohello encoder that contains only video, and no audio, then hello output asset contains files that contain only video data.</span></span> <span data-ttu-id="01867-166">Alguns players podem não ser capazes de toohandle tal fluxos de saída.</span><span class="sxs-lookup"><span data-stu-id="01867-166">Some players may not be able toohandle such output streams.</span></span> <span data-ttu-id="01867-167">Você pode usar essa configuração tooforce Olá codificador tooadd uma saída de toohello silenciosa faixa de áudio nesse cenário.</span><span class="sxs-lookup"><span data-stu-id="01867-167">You can use this setting tooforce hello encoder tooadd a silent audio track toohello output in that scenario.</span></span>

<span data-ttu-id="01867-168">tooforce Olá codificador tooproduce um ativo que contenha uma faixa de áudio silenciosa quando a entrada não tem áudio, especifique o valor de "InsertSilenceIfNoAudio" hello.</span><span class="sxs-lookup"><span data-stu-id="01867-168">tooforce hello encoder tooproduce an asset that contains a silent audio track when input has no audio, specify hello "InsertSilenceIfNoAudio" value.</span></span>

<span data-ttu-id="01867-169">Você pode executar qualquer Olá MES predefinições documentadas em [isso](media-services-mes-presets-overview.md) seção e fazer Olá modificações a seguir:</span><span class="sxs-lookup"><span data-stu-id="01867-169">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

### <a name="json-preset"></a><span data-ttu-id="01867-170">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="01867-170">JSON preset</span></span>
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a><span data-ttu-id="01867-171">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="01867-171">XML preset</span></span>
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <span data-ttu-id="01867-172"><a id="deinterlacing"></a>Desabilitar desentrelaçamento automático</span><span class="sxs-lookup"><span data-stu-id="01867-172"><a id="deinterlacing"></a>Disable auto de-interlacing</span></span>
<span data-ttu-id="01867-173">Os clientes não precisam toodo nada se eles como Olá entrelaçamento toobe conteúdo automaticamente eliminação entrelaçada.</span><span class="sxs-lookup"><span data-stu-id="01867-173">Customers don’t need toodo anything if they like hello interlace contents toobe automatically de-interlaced.</span></span> <span data-ttu-id="01867-174">Quando Olá automática de entrelaçamento está na saudação (padrão) MES Olá auto detecção de quadros entrelaçadas e somente eliminação as interfaces quadros marcados como entrelaçada.</span><span class="sxs-lookup"><span data-stu-id="01867-174">When hello auto de-interlacing is on (default) hello MES does hello auto detection of interlaced frames and only de-interlaces frames marked as interlaced.</span></span>

<span data-ttu-id="01867-175">Você pode desativar Olá automática de entrelaçamento.</span><span class="sxs-lookup"><span data-stu-id="01867-175">You can turn hello auto de-interlacing off.</span></span> <span data-ttu-id="01867-176">No entanto, isso não é recomendado.</span><span class="sxs-lookup"><span data-stu-id="01867-176">This option is not recommended.</span></span>

### <a name="json-preset"></a><span data-ttu-id="01867-177">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="01867-177">JSON preset</span></span>
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a><span data-ttu-id="01867-178">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="01867-178">XML preset</span></span>
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <span data-ttu-id="01867-179"><a id="audio_only"></a>Predefinições somente de áudio</span><span class="sxs-lookup"><span data-stu-id="01867-179"><a id="audio_only"></a>Audio-only presets</span></span>
<span data-ttu-id="01867-180">Esta seção demonstra duas predefinições MES somente de áudio: áudio AAC e Áudio de Boa Qualidade AAC.</span><span class="sxs-lookup"><span data-stu-id="01867-180">This section demonstrates two audio-only MES presets: AAC Audio and AAC Good Quality Audio.</span></span>

### <a name="aac-audio"></a><span data-ttu-id="01867-181">Áudio AAC</span><span class="sxs-lookup"><span data-stu-id="01867-181">AAC Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="aac-good-quality-audio"></a><span data-ttu-id="01867-182">Áudio de Boa Qualidade AAC</span><span class="sxs-lookup"><span data-stu-id="01867-182">AAC Good Quality Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 192,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="01867-183"><a id="concatenate"></a>Concatenar dois ou mais arquivos de vídeo</span><span class="sxs-lookup"><span data-stu-id="01867-183"><a id="concatenate"></a>Concatenate two or more video files</span></span>

<span data-ttu-id="01867-184">Olá exemplo a seguir ilustra como você pode gerar uma predefinição tooconcatenate dois ou mais arquivos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="01867-184">hello following example illustrates how you can generate a preset tooconcatenate two or more video files.</span></span> <span data-ttu-id="01867-185">cenário mais comum de saudação é quando você deseja tooadd um cabeçalho ou um vídeo principal de toohello do marcador.</span><span class="sxs-lookup"><span data-stu-id="01867-185">hello most common scenario is when you want tooadd a header or a trailer toohello main video.</span></span> <span data-ttu-id="01867-186">Olá destinado a uso é quando (resolução de vídeo, taxa de quadros, contagem de faixa de áudio, etc.) de propriedades de compartilhamento de arquivos de vídeo hello está sendo editados juntos.</span><span class="sxs-lookup"><span data-stu-id="01867-186">hello intended use is when hello video files being edited together share  properties (video resolution, frame rate, audio track count, etc.).</span></span> <span data-ttu-id="01867-187">Você deve tomar cuidado para não toomix vídeos de taxas de quadros diferentes ou com números diferentes de faixas de áudio.</span><span class="sxs-lookup"><span data-stu-id="01867-187">You should take care not toomix videos of different frame rates, or with different number of audio tracks.</span></span>

>[!NOTE]
><span data-ttu-id="01867-188">Olá design atual do recurso de concatenação de saudação espera que Olá entrada videoclipes são consistentes em termos de resolução, taxa de quadros etc.</span><span class="sxs-lookup"><span data-stu-id="01867-188">hello current design of hello concatenation feature expects that hello input video clips are consistent in terms of resolution, frame rate etc.</span></span> 

### <a name="requirements-and-considerations"></a><span data-ttu-id="01867-189">Requisitos e considerações</span><span class="sxs-lookup"><span data-stu-id="01867-189">Requirements and considerations</span></span>

* <span data-ttu-id="01867-190">Vídeos de entrada devem ter apenas uma faixa de áudio.</span><span class="sxs-lookup"><span data-stu-id="01867-190">Input videos should only have one audio track.</span></span>
* <span data-ttu-id="01867-191">Vídeos de entrada devem ter Olá mesma taxa de quadros.</span><span class="sxs-lookup"><span data-stu-id="01867-191">Input videos should all have hello same frame rate.</span></span>
* <span data-ttu-id="01867-192">Você deve carregar seus vídeos em ativos separados e definir vídeos hello como arquivo principal de saudação em cada ativo.</span><span class="sxs-lookup"><span data-stu-id="01867-192">You must upload your videos into separate assets and set hello videos as hello primary file in each asset.</span></span>
* <span data-ttu-id="01867-193">Você precisa de duração de saudação tooknow de vídeos.</span><span class="sxs-lookup"><span data-stu-id="01867-193">You need tooknow hello duration of your videos.</span></span>
* <span data-ttu-id="01867-194">Olá predefinidos exemplos a seguir presume que todos os vídeos de entrada hello começam com um carimbo de hora de zero.</span><span class="sxs-lookup"><span data-stu-id="01867-194">hello preset examples below assumes that all hello input videos start with a timestamp of zero.</span></span> <span data-ttu-id="01867-195">Você precisar de toomodify Olá StartTime valores se vídeos Olá tem o carimbo de hora de início diferente, como normalmente Olá caso com arquivos mortos ao vivo.</span><span class="sxs-lookup"><span data-stu-id="01867-195">You need toomodify hello StartTime values if hello videos have different starting timestamp, as is typically hello case with live archives.</span></span>
* <span data-ttu-id="01867-196">Olá predefinição JSON faz referências explícitas toohello AssetID valores de ativos de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="01867-196">hello JSON preset makes explicit references toohello AssetID values of hello input assets.</span></span>
* <span data-ttu-id="01867-197">o código de exemplo Hello pressupõe que Olá que JSON predefinição tiver sido salvo como arquivo local tooa, como "C:\supportFiles\preset.json".</span><span class="sxs-lookup"><span data-stu-id="01867-197">hello sample code assumes that hello JSON preset has been saved tooa local file, such as "C:\supportFiles\preset.json".</span></span> <span data-ttu-id="01867-198">Ele também pressupõe que foram criados dois ativos Carregando dois arquivos de vídeos e que você sabe Olá AssetID os valores resultantes.</span><span class="sxs-lookup"><span data-stu-id="01867-198">It also assumes that two assets have been created by uploading two video files, and that you know hello resultant AssetID values.</span></span>
* <span data-ttu-id="01867-199">Olá trecho de código e JSON predefinição mostra um exemplo de concatenação de dois arquivos de vídeos.</span><span class="sxs-lookup"><span data-stu-id="01867-199">hello code snippet and JSON preset shows an example of concatenating two video files.</span></span> <span data-ttu-id="01867-200">Você pode estendê-lo toomore que dois vídeos por:</span><span class="sxs-lookup"><span data-stu-id="01867-200">You can extend it toomore than two videos by:</span></span>

  1. <span data-ttu-id="01867-201">Tarefa de chamada. InputAssets.Add() repetidamente tooadd mais vídeos, na ordem.</span><span class="sxs-lookup"><span data-stu-id="01867-201">Calling task.InputAssets.Add() repeatedly tooadd more videos, in order.</span></span>
  2. <span data-ttu-id="01867-202">Tornar correspondente edita o elemento toohello "fontes" hello JSON, adicionando mais entradas, Olá mesma ordem.</span><span class="sxs-lookup"><span data-stu-id="01867-202">Making corresponding edits toohello "Sources" element in hello JSON, by adding more entries, in hello same order.</span></span>

### <a name="net-code"></a><span data-ttu-id="01867-203">Código do .NET</span><span class="sxs-lookup"><span data-stu-id="01867-203">.NET code</span></span>

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass tooit hello name of the
    // processor toouse for hello specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load hello XML (or JSON) from hello local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify hello input videos toobe concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset toocontain hello results of hello job.
    // This output is specified as AssetCreationOptions.None, which
    // means hello output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a><span data-ttu-id="01867-204">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="01867-204">JSON preset</span></span>

<span data-ttu-id="01867-205">Atualize personalizados predefinidos com ids de ativos de saudação que você deseja tooconcatenate e com o segmento de tempo apropriado Olá para cada vídeo.</span><span class="sxs-lookup"><span data-stu-id="01867-205">Update your custom preset with ids of hello assets that you want tooconcatenate, and with hello appropriate time segment for each video.</span></span>

    {
      "Version": 1.0,
      "Sources": [
        {
          "AssetID": "606db602-efd7-4436-97b4-c0b867ba195b",
          "StartTime": "00:00:01",
          "Duration": "00:00:15"
        },
        {
          "AssetID": "a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e",
          "StartTime": "00:00:02",
          "Duration": "00:00:05"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": true,
          "H264Layers": [
            {
              "Level": "auto",
              "Bitrate": 1800,
              "MaxBitrate": 1800,
              "BufferWindow": "00:00:05",
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
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
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="01867-206"><a id="crop"></a>Cortar vídeos com o Codificador de Mídia Padrão</span><span class="sxs-lookup"><span data-stu-id="01867-206"><a id="crop"></a>Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="01867-207">Consulte Olá [cortar vídeos com o codificador de mídia padrão](media-services-crop-video.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="01867-207">See hello [Crop videos with Media Encoder Standard](media-services-crop-video.md) topic.</span></span>

## <span data-ttu-id="01867-208"><a id="no_video"></a>Inserir uma faixa de vídeo quando a entrada não tiver vídeo</span><span class="sxs-lookup"><span data-stu-id="01867-208"><a id="no_video"></a>Insert a video track when input has no video</span></span>

<span data-ttu-id="01867-209">Por padrão, se você enviar um codificador de toohello de entrada que contenha apenas áudio e sem vídeo, em seguida, Olá ativo de saída contém de arquivos que contêm dados somente de áudio.</span><span class="sxs-lookup"><span data-stu-id="01867-209">By default, if you send an input toohello encoder that contains only audio, and no video, then hello output asset contains files that contain only audio data.</span></span> <span data-ttu-id="01867-210">Alguns players, incluindo o Azure Media Player (consulte [isso](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) pode não ser capaz de toohandle tais fluxos.</span><span class="sxs-lookup"><span data-stu-id="01867-210">Some players, including Azure Media Player (see [this](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) may not be able toohandle such streams.</span></span> <span data-ttu-id="01867-211">Você pode usar este tooadd de codificador Olá configuração tooforce uma saída de toohello da faixa de vídeo monocromático nesse cenário.</span><span class="sxs-lookup"><span data-stu-id="01867-211">You can use this setting tooforce hello encoder tooadd a monochrome video track toohello output in that scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="01867-212">Forçar Olá codificador tooinsert um tamanho saída faixa de vídeo aumenta Olá Olá ativo de saída e Olá assim o custo incorrido para tarefas de codificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="01867-212">Forcing hello encoder tooinsert an output video track increases hello size of hello output Asset, and thereby hello cost incurred for hello encoding Task.</span></span> <span data-ttu-id="01867-213">Você deve executar testes tooverify que esse aumento resultante tem apenas um impacto modesto sobre os encargos mensais.</span><span class="sxs-lookup"><span data-stu-id="01867-213">You should run tests tooverify that this resultant increase has only a modest impact on your monthly charges.</span></span>
>

### <a name="inserting-video-at-only-hello-lowest-bitrate"></a><span data-ttu-id="01867-214">Inserindo vídeo em apenas hello mais baixa taxa de bits</span><span class="sxs-lookup"><span data-stu-id="01867-214">Inserting video at only hello lowest bitrate</span></span>

<span data-ttu-id="01867-215">Suponha que você está usando uma codificação de taxa de bits vários, como predefinição ["H264 taxas de bits múltiplas 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode toda entrada de catálogo para streaming, que contém uma mistura de arquivos de vídeo e arquivos de áudio.</span><span class="sxs-lookup"><span data-stu-id="01867-215">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="01867-216">Nesse cenário, quando a entrada de saudação não tem vídeo, convém tooforce Olá codificador tooinsert uma monocromática vídeo controlar apenas Olá taxas de bits menores, como tooinserting contrário vídeo em cada taxa de bits de saída.</span><span class="sxs-lookup"><span data-stu-id="01867-216">In this scenario, when hello input has no video, you may want tooforce hello encoder tooinsert a monochrome video track at just hello lowest bitrate, as opposed tooinserting video at every output bitrate.</span></span> <span data-ttu-id="01867-217">tooachieve isso, você precisa Olá toouse **InsertBlackIfNoVideoBottomLayerOnly** sinalizador.</span><span class="sxs-lookup"><span data-stu-id="01867-217">tooachieve this, you need toouse hello **InsertBlackIfNoVideoBottomLayerOnly** flag.</span></span>

<span data-ttu-id="01867-218">Você pode executar qualquer Olá MES predefinições documentadas em [isso](media-services-mes-presets-overview.md) seção e fazer Olá modificações a seguir:</span><span class="sxs-lookup"><span data-stu-id="01867-218">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="01867-219">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="01867-219">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="01867-220">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="01867-220">XML preset</span></span>

<span data-ttu-id="01867-221">Ao usar o XML, use a condição = "InsertBlackIfNoVideoBottomLayerOnly" como um atributo toohello **H264Video** elemento e a condição = "InsertSilenceIfNoAudio" como um atributo muito**AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="01867-221">When using XML, use Condition="InsertBlackIfNoVideoBottomLayerOnly" as an attribute toohello **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute too**AACAudio**.</span></span>

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideoBottomLayerOnly">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .
```

### <a name="inserting-video-at-all-output-bitrates"></a><span data-ttu-id="01867-222">Inserindo vídeo em todas as taxas de bits de saída</span><span class="sxs-lookup"><span data-stu-id="01867-222">Inserting video at all output bitrates</span></span>
<span data-ttu-id="01867-223">Suponha que você está usando uma codificação de taxa de bits vários, como predefinição ["H264 taxas de bits múltiplas 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode toda entrada de catálogo para streaming, que contém uma mistura de arquivos de vídeo e arquivos de áudio.</span><span class="sxs-lookup"><span data-stu-id="01867-223">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="01867-224">Nesse cenário, quando a entrada de saudação não tem vídeo, convém tooforce Olá codificador tooinsert um vídeo monocromático acompanhar a todas as taxas de bits de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="01867-224">In this scenario, when hello input has no video, you may want tooforce hello encoder tooinsert a monochrome video track at all hello output bitrates.</span></span> <span data-ttu-id="01867-225">Isso garante que a saída ativos são todos homogêneos com respeito toonumber de faixas de vídeo e faixas de áudio.</span><span class="sxs-lookup"><span data-stu-id="01867-225">This ensures that your output Assets are all homogenous with respect toonumber of video tracks and audio tracks.</span></span> <span data-ttu-id="01867-226">tooachieve isso, é necessário toospecify Olá sinalizador "InsertBlackIfNoVideo".</span><span class="sxs-lookup"><span data-stu-id="01867-226">tooachieve this, you need toospecify hello "InsertBlackIfNoVideo" flag.</span></span>

<span data-ttu-id="01867-227">Você pode executar qualquer Olá MES predefinições documentadas em [isso](media-services-mes-presets-overview.md) seção e fazer Olá modificações a seguir:</span><span class="sxs-lookup"><span data-stu-id="01867-227">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="01867-228">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="01867-228">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="01867-229">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="01867-229">XML preset</span></span>

<span data-ttu-id="01867-230">Ao usar o XML, use a condição = "InsertBlackIfNoVideo" como um atributo toohello **H264Video** elemento e a condição = "InsertSilenceIfNoAudio" como um atributo muito**AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="01867-230">When using XML, use Condition="InsertBlackIfNoVideo" as an attribute toohello **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute too**AACAudio**.</span></span>

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideo">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .  
```

## <span data-ttu-id="01867-231"><a id="rotate_video"></a>Girar um vídeo</span><span class="sxs-lookup"><span data-stu-id="01867-231"><a id="rotate_video"></a>Rotate a video</span></span>
<span data-ttu-id="01867-232">Olá [codificador de mídia padrão](media-services-dotnet-encode-with-media-encoder-standard.md) dá suporte a rotação de ângulos de 0/90/180/270.</span><span class="sxs-lookup"><span data-stu-id="01867-232">hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 0/90/180/270.</span></span> <span data-ttu-id="01867-233">comportamento padrão de saudação é "Auto", onde ele tenta toodetect Olá rotação metadados no arquivo de vídeo entrada hello e compensar a ele.</span><span class="sxs-lookup"><span data-stu-id="01867-233">hello default behavior is "Auto", where it tries toodetect hello rotation metadata in hello incoming video file and compensate for it.</span></span> <span data-ttu-id="01867-234">Incluem hello seguinte **fontes** tooone de elemento de predefinições de saudação definido em [isso](media-services-mes-presets-overview.md) seção:</span><span class="sxs-lookup"><span data-stu-id="01867-234">Include hello following **Sources** element tooone of hello presets defined in [this](media-services-mes-presets-overview.md) section:</span></span>

### <a name="json-preset"></a><span data-ttu-id="01867-235">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="01867-235">JSON preset</span></span>
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...
### <a name="xml-preset"></a><span data-ttu-id="01867-236">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="01867-236">XML preset</span></span>
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

<span data-ttu-id="01867-237">Além disso, consulte [isso](media-services-mes-schema.md#PreserveResolutionAfterRotation) tópico para obter mais informações sobre como o codificador Olá interpreta configurações de largura e altura de saudação em hello predefinidos, quando a compensação de rotação é disparada.</span><span class="sxs-lookup"><span data-stu-id="01867-237">Also, see [this](media-services-mes-schema.md#PreserveResolutionAfterRotation) topic for more information on how hello encoder interprets hello Width and Height settings in hello preset, when rotation compensation is triggered.</span></span>

<span data-ttu-id="01867-238">Você pode usar metadados da rotação do tooignore de codificador da toohello do tooindicate de valor "0" Olá, se presente, vídeo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="01867-238">You can use hello value "0" tooindicate toohello encoder tooignore rotation metadata, if present, in hello input video.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="01867-239">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="01867-239">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="01867-240">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="01867-240">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="01867-241">Consulte também</span><span class="sxs-lookup"><span data-stu-id="01867-241">See Also</span></span>
[<span data-ttu-id="01867-242">Visão geral da codificação de serviços de mídia</span><span class="sxs-lookup"><span data-stu-id="01867-242">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)
