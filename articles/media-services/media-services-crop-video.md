---
title: "aaaHow toocrop vídeos com Media Encoder Standard - Azure | Microsoft Docs"
description: "Este artigo mostra como toocrop vídeos com o codificador de mídia padrão."
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
ms.openlocfilehash: 2b4ac3d96228b93c890a38c57c4913988de1e8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="crop-videos-with-media-encoder-standard"></a><span data-ttu-id="f3db7-103">Cortar vídeos com o Codificador de Mídia Padrão</span><span class="sxs-lookup"><span data-stu-id="f3db7-103">Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="f3db7-104">Você pode usar o codificador de mídia padrão (MES) toocrop o vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="f3db7-104">You can use Media Encoder Standard (MES) toocrop your input video.</span></span> <span data-ttu-id="f3db7-105">Corte é o processo de saudação de seleção de uma janela retangular dentro do quadro de vídeo hello e codificação apenas os pixels hello dentro dessa janela.</span><span class="sxs-lookup"><span data-stu-id="f3db7-105">Cropping is hello process of selecting a rectangular window within hello video frame, and encoding just hello pixels within that window.</span></span> <span data-ttu-id="f3db7-106">Olá diagrama a seguir ajudam a ilustrar o processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f3db7-106">hello following diagram helps illustrate hello process.</span></span>

![Cortar um vídeo](./media/media-services-crop-video/media-services-crop-video01.png)

<span data-ttu-id="f3db7-108">Suponha que você tenha como entrada um vídeo que tem uma resolução de 1920 x 1080 pixels (taxa de proporção de 16:9), mas tem barras pretas (pilar caixas) no hello esquerda e direita, para que somente uma janela de 4:3 ou 1440 x 1080 pixels contém vídeo ativo.</span><span class="sxs-lookup"><span data-stu-id="f3db7-108">Suppose you have as input a video that has a resolution of 1920x1080 pixels (16:9 aspect ratio), but has black bars (pillar boxes) at hello left and right, so that only a 4:3 window or 1440x1080 pixels contains active video.</span></span> <span data-ttu-id="f3db7-109">Você pode usar MES toocrop ou editar limite barras Olá preto e codificar a região de 1440 x 1080 hello.</span><span class="sxs-lookup"><span data-stu-id="f3db7-109">You can use MES toocrop or edit out hello black bars, and encode hello 1440x1080 region.</span></span>

<span data-ttu-id="f3db7-110">Corte em MES é uma fase de pré-processamento para que parâmetros de corte Olá na predefinição de codificação Olá aplicam toohello vídeo de entrada original.</span><span class="sxs-lookup"><span data-stu-id="f3db7-110">Cropping in MES is a pre-processing stage, so hello cropping parameters in hello encoding preset apply toohello original input video.</span></span> <span data-ttu-id="f3db7-111">A codificação é um estágio subsequente, e as configurações de largura/altura do hello aplicam toohello *pré-processado* vídeo e não toohello original.</span><span class="sxs-lookup"><span data-stu-id="f3db7-111">Encoding is a subsequent stage, and hello width/height settings apply toohello *pre-processed* video, and not toohello original video.</span></span> <span data-ttu-id="f3db7-112">Ao projetar sua predefinição você precisa fazer toodo Olá seguinte: (a) Selecione parâmetros de corte de saudação com base no vídeo de entrada original hello e (b), selecione seu codificar configurações com base em Olá cortada vídeo.</span><span class="sxs-lookup"><span data-stu-id="f3db7-112">When designing your preset you need toodo hello following: (a) select hello crop parameters based on hello original input video, and (b) select your encode settings based on hello cropped video.</span></span> <span data-ttu-id="f3db7-113">Se você não corresponder a codificar configurações toohello cortada vídeo, saída de hello não estará conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="f3db7-113">If you do not match your encode settings toohello cropped video, hello output will not be as you expect.</span></span>

<span data-ttu-id="f3db7-114">Olá [seguir](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) tópico mostra como toocreate um trabalho de codificação com MES e como toospecify um personalizado predefinido para Olá tarefa de codificação.</span><span class="sxs-lookup"><span data-stu-id="f3db7-114">hello [following](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic shows how toocreate an encoding job with MES and how toospecify a custom preset for hello encoding task.</span></span> 

## <a name="creating-a-custom-preset"></a><span data-ttu-id="f3db7-115">Criando uma predefinição personalizada</span><span class="sxs-lookup"><span data-stu-id="f3db7-115">Creating a custom preset</span></span>
<span data-ttu-id="f3db7-116">O exemplo hello mostrado no diagrama de saudação:</span><span class="sxs-lookup"><span data-stu-id="f3db7-116">In hello example shown in hello diagram:</span></span>

1. <span data-ttu-id="f3db7-117">A entrada original é 1920 x 1080</span><span class="sxs-lookup"><span data-stu-id="f3db7-117">Original input is 1920x1080</span></span>
2. <span data-ttu-id="f3db7-118">Ele precisa toobe cortada saída tooan de 1440 x 1080, que é centralizada no quadro de entrada hello</span><span class="sxs-lookup"><span data-stu-id="f3db7-118">It needs toobe cropped tooan output of 1440x1080, which is centered in hello input frame</span></span>
3. <span data-ttu-id="f3db7-119">Isso significa um deslocamento de X de (1920 – 1440)/2 = 240 e um deslocamento de Y de zero</span><span class="sxs-lookup"><span data-stu-id="f3db7-119">This means an X offset of (1920 – 1440)/2 = 240, and a Y offset of zero</span></span>
4. <span data-ttu-id="f3db7-120">Olá largura e altura do retângulo de corte de saudação são 1440 e 1080, respectivamente</span><span class="sxs-lookup"><span data-stu-id="f3db7-120">hello Width and Height of hello Crop rectangle are 1440 and 1080, respectively</span></span>
5. <span data-ttu-id="f3db7-121">Em Olá codificar estágio, hello pedir é tooproduce três camadas, são resoluções 1440 x 1080, 960 x 720 e 480 x 360, respectivamente</span><span class="sxs-lookup"><span data-stu-id="f3db7-121">In hello encode stage, hello ask is tooproduce three layers, are resolutions 1440x1080, 960x720 and 480x360, respectively</span></span>

### <a name="json-preset"></a><span data-ttu-id="f3db7-122">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="f3db7-122">JSON preset</span></span>
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


## <a name="restrictions-on-cropping"></a><span data-ttu-id="f3db7-123">Restrições de corte</span><span class="sxs-lookup"><span data-stu-id="f3db7-123">Restrictions on cropping</span></span>
<span data-ttu-id="f3db7-124">Olá corte recurso destina-se toobe manual.</span><span class="sxs-lookup"><span data-stu-id="f3db7-124">hello cropping feature is meant toobe manual.</span></span> <span data-ttu-id="f3db7-125">Você precisaria tooload sua entrada de vídeo em uma ferramenta de edição adequada que permite que você selecione quadros de interesse, posicione Olá cursor toodetermine deslocamentos Olá corte retângulo, toodetermine Olá predefinição de codificação é ajustada para que determinado vídeo, etc. Este recurso não é tooenable coisas como: detecção automática e remoção das bordas pretas letterbox/pillarbox no vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="f3db7-125">You would need tooload your input video into a suitable editing tool that lets you select frames of interest, position hello cursor toodetermine offsets for hello cropping rectangle, toodetermine hello encoding preset that is tuned for that particular video, etc. This feature is not meant tooenable things like: automatic detection and removal of black letterbox/pillarbox borders in your input video.</span></span>

<span data-ttu-id="f3db7-126">As seguintes restrições se aplicam a toohello cortar o recurso.</span><span class="sxs-lookup"><span data-stu-id="f3db7-126">Following constraints apply toohello cropping feature.</span></span> <span data-ttu-id="f3db7-127">Se eles não forem atendidos, Olá codificar tarefas podem falhar ou produzir uma saída inesperada.</span><span class="sxs-lookup"><span data-stu-id="f3db7-127">If these are not met, hello encode Task can fail, or produce an unexpected output.</span></span>

1. <span data-ttu-id="f3db7-128">Olá coordenadas e o tamanho do retângulo de corte Olá tem toofit no vídeo de entrada hello</span><span class="sxs-lookup"><span data-stu-id="f3db7-128">hello co-ordinates and size of hello Crop rectangle have toofit within hello input video</span></span>
2. <span data-ttu-id="f3db7-129">Conforme mencionado acima, Olá largura e altura em Olá codificar configurações têm toohello toocorrespond cortada vídeo</span><span class="sxs-lookup"><span data-stu-id="f3db7-129">As mentioned above, hello Width & Height in hello encode settings have toocorrespond toohello cropped video</span></span>
3. <span data-ttu-id="f3db7-130">Recortando aplica toovideos capturados no modo paisagem (ou seja, não aplicável toovideos registrado com um smartphone mantidos verticalmente ou no modo retrato)</span><span class="sxs-lookup"><span data-stu-id="f3db7-130">Cropping applies toovideos captured in landscape mode (i.e. not applicable toovideos recorded with a smartphone held vertically or in portrait mode)</span></span>
4. <span data-ttu-id="f3db7-131">Funciona melhor com vídeo progressivo capturado com pixels quadrados</span><span class="sxs-lookup"><span data-stu-id="f3db7-131">Works best with progressive video captured with square pixels</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="f3db7-132">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="f3db7-132">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="f3db7-133">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="f3db7-133">Next step</span></span>
<span data-ttu-id="f3db7-134">Consulte toohelp caminhos que você conheça ótimos recursos oferecidos pelo AMS de aprendizado do Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="f3db7-134">See Azure Media Services learning paths toohelp you learn about great features offered by AMS.</span></span>  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
