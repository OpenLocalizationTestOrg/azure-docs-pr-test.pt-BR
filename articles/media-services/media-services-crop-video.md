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
# <a name="crop-videos-with-media-encoder-standard"></a>Cortar vídeos com o Codificador de Mídia Padrão
Você pode usar o codificador de mídia padrão (MES) toocrop o vídeo de entrada. Corte é o processo de saudação de seleção de uma janela retangular dentro do quadro de vídeo hello e codificação apenas os pixels hello dentro dessa janela. Olá diagrama a seguir ajudam a ilustrar o processo de saudação.

![Cortar um vídeo](./media/media-services-crop-video/media-services-crop-video01.png)

Suponha que você tenha como entrada um vídeo que tem uma resolução de 1920 x 1080 pixels (taxa de proporção de 16:9), mas tem barras pretas (pilar caixas) no hello esquerda e direita, para que somente uma janela de 4:3 ou 1440 x 1080 pixels contém vídeo ativo. Você pode usar MES toocrop ou editar limite barras Olá preto e codificar a região de 1440 x 1080 hello.

Corte em MES é uma fase de pré-processamento para que parâmetros de corte Olá na predefinição de codificação Olá aplicam toohello vídeo de entrada original. A codificação é um estágio subsequente, e as configurações de largura/altura do hello aplicam toohello *pré-processado* vídeo e não toohello original. Ao projetar sua predefinição você precisa fazer toodo Olá seguinte: (a) Selecione parâmetros de corte de saudação com base no vídeo de entrada original hello e (b), selecione seu codificar configurações com base em Olá cortada vídeo. Se você não corresponder a codificar configurações toohello cortada vídeo, saída de hello não estará conforme o esperado.

Olá [seguir](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) tópico mostra como toocreate um trabalho de codificação com MES e como toospecify um personalizado predefinido para Olá tarefa de codificação. 

## <a name="creating-a-custom-preset"></a>Criando uma predefinição personalizada
O exemplo hello mostrado no diagrama de saudação:

1. A entrada original é 1920 x 1080
2. Ele precisa toobe cortada saída tooan de 1440 x 1080, que é centralizada no quadro de entrada hello
3. Isso significa um deslocamento de X de (1920 – 1440)/2 = 240 e um deslocamento de Y de zero
4. Olá largura e altura do retângulo de corte de saudação são 1440 e 1080, respectivamente
5. Em Olá codificar estágio, hello pedir é tooproduce três camadas, são resoluções 1440 x 1080, 960 x 720 e 480 x 360, respectivamente

### <a name="json-preset"></a>Predefinição JSON
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


## <a name="restrictions-on-cropping"></a>Restrições de corte
Olá corte recurso destina-se toobe manual. Você precisaria tooload sua entrada de vídeo em uma ferramenta de edição adequada que permite que você selecione quadros de interesse, posicione Olá cursor toodetermine deslocamentos Olá corte retângulo, toodetermine Olá predefinição de codificação é ajustada para que determinado vídeo, etc. Este recurso não é tooenable coisas como: detecção automática e remoção das bordas pretas letterbox/pillarbox no vídeo de entrada.

As seguintes restrições se aplicam a toohello cortar o recurso. Se eles não forem atendidos, Olá codificar tarefas podem falhar ou produzir uma saída inesperada.

1. Olá coordenadas e o tamanho do retângulo de corte Olá tem toofit no vídeo de entrada hello
2. Conforme mencionado acima, Olá largura e altura em Olá codificar configurações têm toohello toocorrespond cortada vídeo
3. Recortando aplica toovideos capturados no modo paisagem (ou seja, não aplicável toovideos registrado com um smartphone mantidos verticalmente ou no modo retrato)
4. Funciona melhor com vídeo progressivo capturado com pixels quadrados

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Próxima etapa
Consulte toohelp caminhos que você conheça ótimos recursos oferecidos pelo AMS de aprendizado do Azure Media Services.  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
