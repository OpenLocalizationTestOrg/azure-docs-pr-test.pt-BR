---
title: "Como cortar vídeos com o Media Encoder Standard - Azure | Microsoft Docs"
description: "Este artigo mostra como cortar vídeos com o Codificador de Mídia Padrão."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 7628f674-2005-4531-8b61-d7a4f53e46ba
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/09/2017
ms.author: anilmur;juliako;
ms.openlocfilehash: 60d0ce14a271fcbe698559da95ca011cb888b221
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="crop-videos-with-media-encoder-standard"></a><span data-ttu-id="30728-103">Cortar vídeos com o Codificador de Mídia Padrão</span><span class="sxs-lookup"><span data-stu-id="30728-103">Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="30728-104">Você pode usar o MES (Codificador de Mídia Padrão) para cortar a entrada de seu vídeo.</span><span class="sxs-lookup"><span data-stu-id="30728-104">You can use Media Encoder Standard (MES) to crop your input video.</span></span> <span data-ttu-id="30728-105">Corte é o processo de seleção de uma janela retangular no quadro de vídeo e codificação apenas dos pixels nessa janela.</span><span class="sxs-lookup"><span data-stu-id="30728-105">Cropping is the process of selecting a rectangular window within the video frame, and encoding just the pixels within that window.</span></span> <span data-ttu-id="30728-106">O diagrama a seguir ajuda a ilustrar o processo.</span><span class="sxs-lookup"><span data-stu-id="30728-106">The following diagram helps illustrate the process.</span></span>

![Cortar um vídeo](./media/media-services-crop-video/media-services-crop-video01.png)

<span data-ttu-id="30728-108">Suponha que você tenha como entrada um vídeo que tem uma resolução de 1920 x 1080 pixels (taxa de proporção de 16:9), mas tem barras pretas (formatos pillarbox) à esquerda e direita e, portanto, apenas uma janela de 4:3 ou 1440 x 1080 pixels contém vídeo ativo.</span><span class="sxs-lookup"><span data-stu-id="30728-108">Suppose you have as input a video that has a resolution of 1920x1080 pixels (16:9 aspect ratio), but has black bars (pillar boxes) at the left and right, so that only a 4:3 window or 1440x1080 pixels contains active video.</span></span> <span data-ttu-id="30728-109">Você pode usar o MES para cortar ou editar as barras pretas e codificar a região 1440 x 1080.</span><span class="sxs-lookup"><span data-stu-id="30728-109">You can use MES to crop or edit out the black bars, and encode the 1440x1080 region.</span></span>

<span data-ttu-id="30728-110">O corte no MES é uma fase de pré-processamento e, portanto, os parâmetros de corte na predefinição de codificação se aplicam ao vídeo de entrada original.</span><span class="sxs-lookup"><span data-stu-id="30728-110">Cropping in MES is a pre-processing stage, so the cropping parameters in the encoding preset apply to the original input video.</span></span> <span data-ttu-id="30728-111">A codificação é um estágio posterior, e as configurações de largura/altura se aplicam ao vídeo *pré-processado* , não ao vídeo original.</span><span class="sxs-lookup"><span data-stu-id="30728-111">Encoding is a subsequent stage, and the width/height settings apply to the *pre-processed* video, and not to the original video.</span></span> <span data-ttu-id="30728-112">Ao projetar a predefinição, você precisa fazer o seguinte: (a) selecionar os parâmetros de corte com base no vídeo de entrada original e (b) selecionar as configurações de codificação com base no vídeo cortado.</span><span class="sxs-lookup"><span data-stu-id="30728-112">When designing your preset you need to do the following: (a) select the crop parameters based on the original input video, and (b) select your encode settings based on the cropped video.</span></span> <span data-ttu-id="30728-113">Se as configurações de codificação não forem correspondentes ao vídeo cortado, a saída não será como esperado.</span><span class="sxs-lookup"><span data-stu-id="30728-113">If you do not match your encode settings to the cropped video, the output will not be as you expect.</span></span>

<span data-ttu-id="30728-114">O tópico [a seguir](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) mostra como criar um trabalho de codificação com o MES e especificar uma predefinição personalizada para a tarefa de codificação.</span><span class="sxs-lookup"><span data-stu-id="30728-114">The [following](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic shows how to create an encoding job with MES and how to specify a custom preset for the encoding task.</span></span> 

## <a name="creating-a-custom-preset"></a><span data-ttu-id="30728-115">Criando uma predefinição personalizada</span><span class="sxs-lookup"><span data-stu-id="30728-115">Creating a custom preset</span></span>
<span data-ttu-id="30728-116">No exemplo mostrado no diagrama:</span><span class="sxs-lookup"><span data-stu-id="30728-116">In the example shown in the diagram:</span></span>

1. <span data-ttu-id="30728-117">A entrada original é 1920 x 1080</span><span class="sxs-lookup"><span data-stu-id="30728-117">Original input is 1920x1080</span></span>
2. <span data-ttu-id="30728-118">Ela precisa ser recortada para uma saída de 1440 x 1080, que é centralizada no quadro de entrada</span><span class="sxs-lookup"><span data-stu-id="30728-118">It needs to be cropped to an output of 1440x1080, which is centered in the input frame</span></span>
3. <span data-ttu-id="30728-119">Isso significa um deslocamento de X de (1920 – 1440)/2 = 240 e um deslocamento de Y de zero</span><span class="sxs-lookup"><span data-stu-id="30728-119">This means an X offset of (1920 – 1440)/2 = 240, and a Y offset of zero</span></span>
4. <span data-ttu-id="30728-120">A Largura e a Altura do retângulo de Corte são 1440 e 1080, respectivamente</span><span class="sxs-lookup"><span data-stu-id="30728-120">The Width and Height of the Crop rectangle are 1440 and 1080, respectively</span></span>
5. <span data-ttu-id="30728-121">No estágio de codificação, a tarefa é produzir três camadas com as resoluções 1440 x 1080, 960 x 720 e 480 x 360, respectivamente</span><span class="sxs-lookup"><span data-stu-id="30728-121">In the encode stage, the ask is to produce three layers, are resolutions 1440x1080, 960x720 and 480x360, respectively</span></span>

### <a name="json-preset"></a><span data-ttu-id="30728-122">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="30728-122">JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "Crop": {
                "X": 240,
                "Y": 0,
                "Width": 1440,
                "Height": 1080
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
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1440,
              "Height": 1080,
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
              "Bitrate": 1250,
              "MaxBitrate": 1250,
              "BufferWindow": "00:00:05",
              "Width": 480,
              "Height": 360,
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


## <a name="restrictions-on-cropping"></a><span data-ttu-id="30728-123">Restrições de corte</span><span class="sxs-lookup"><span data-stu-id="30728-123">Restrictions on cropping</span></span>
<span data-ttu-id="30728-124">O recurso de corte deve ser manual.</span><span class="sxs-lookup"><span data-stu-id="30728-124">The cropping feature is meant to be manual.</span></span> <span data-ttu-id="30728-125">Você precisa carregar o vídeo de entrada em uma ferramenta de edição adequada que permite selecionar quadros de interesse, posicionar o cursor para determinar os deslocamentos do retângulo de corte, determinar a predefinição de codificação ajustada para esse vídeo específico, etc. Esse recurso não se destina a habilitar opções como: detecção automática e remoção de bordas pretas no formato letterbox/pillarbox no vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="30728-125">You would need to load your input video into a suitable editing tool that lets you select frames of interest, position the cursor to determine offsets for the cropping rectangle, to determine the encoding preset that is tuned for that particular video, etc. This feature is not meant to enable things like: automatic detection and removal of black letterbox/pillarbox borders in your input video.</span></span>

<span data-ttu-id="30728-126">As restrições a seguir se aplicam ao recurso de corte.</span><span class="sxs-lookup"><span data-stu-id="30728-126">Following constraints apply to the cropping feature.</span></span> <span data-ttu-id="30728-127">Se elas não forem atendidas, a Tarefa de codificação poderá falhar ou produzir uma saída inesperada.</span><span class="sxs-lookup"><span data-stu-id="30728-127">If these are not met, the encode Task can fail, or produce an unexpected output.</span></span>

1. <span data-ttu-id="30728-128">As coordenadas e o tamanho do retângulo de Corte deverão se ajustar ao vídeo de entrada</span><span class="sxs-lookup"><span data-stu-id="30728-128">The co-ordinates and size of the Crop rectangle have to fit within the input video</span></span>
2. <span data-ttu-id="30728-129">Conforme mencionado acima, a Largura e a Altura nas configurações de codificação precisam corresponder ao vídeo cortado</span><span class="sxs-lookup"><span data-stu-id="30728-129">As mentioned above, the Width & Height in the encode settings have to correspond to the cropped video</span></span>
3. <span data-ttu-id="30728-130">O corte se aplica aos vídeos capturados no modo paisagem (ou seja, não se aplica aos vídeos gravados com um smartphone mantido verticalmente ou no modo retrato)</span><span class="sxs-lookup"><span data-stu-id="30728-130">Cropping applies to videos captured in landscape mode (i.e. not applicable to videos recorded with a smartphone held vertically or in portrait mode)</span></span>
4. <span data-ttu-id="30728-131">Funciona melhor com vídeo progressivo capturado com pixels quadrados</span><span class="sxs-lookup"><span data-stu-id="30728-131">Works best with progressive video captured with square pixels</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="30728-132">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="30728-132">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="30728-133">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="30728-133">Next step</span></span>
<span data-ttu-id="30728-134">Veja os roteiros de aprendizagem dos Serviços de Mídia do Azure para ajudá-lo a saber mais sobre os excelentes recursos oferecidos pelo AMS.</span><span class="sxs-lookup"><span data-stu-id="30728-134">See Azure Media Services learning paths to help you learn about great features offered by AMS.</span></span>  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
