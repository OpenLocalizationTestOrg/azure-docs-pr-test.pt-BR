---
title: "Predefinições de aaaTask para MES (padrão de codificador de mídia) | Microsoft Docs"
description: "Olá tópico apresenta e visão geral das predefinições de tarefa para MES (padrão de codificador de mídia)."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: f243ed1c-ac9c-4300-a5f7-f092cf9853b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 56e098d6d8c8f84031421ec59f087f20370ba111
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="task-presets-for-mes-media-encoder-standard"></a>Predefinições de tarefa para MES (Media Encoder Standard)

O **Media Encoder Standard** define um conjunto de predefinições de codificação que pode ser usado ao criar trabalhos de codificação. É recomendável toouse hello "Streaming adaptável" predefinição se você quiser tooencode um vídeo para streaming com os serviços de mídia. Ao especificar essa predefinição, o Media Encoder Standard [gerará uma escada de taxa de bits automaticamente](media-services-autogen-bitrate-ladder-with-mes.md). 

No entanto, se você precisar toocustomize uma predefinição de codificação, você deve executar uma das Olá definidas nesta seção como um modelo para a sua configuração personalizada de predefinições de codificação. Para obter explicações de que cada elemento nessas significa predefinições, e os valores válidos Olá para cada elemento, consulte Olá [esquema padrão do Media Encoder](media-services-mes-schema.md) tópico.  
  
> [!NOTE]
>  Ao usar uma predefinição de 4K codifica, você deve obter Olá `S3` tipo de unidade reservada. Para obter mais informações, consulte [como tooScale codificação](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).  
  
Ao trabalhar com o Media Encoder Standard, a rotação é habilitada por padrão. Se o vídeo foi registrado em um smartphone ou outro dispositivo móvel no modo retrato, em seguida, essas predefinições, por padrão, gira-los tooLandscape modo anterior tooencoding (ao contrário, quando você trabalha com o codificador de mídia do Azure, onde a rotação do vídeo é uma operação manual, conforme documentado no [isso](http://azure.microsoft.com/blog/2014/08/21/advanced-encoding-features-in-azure-media-encoder/) blog em "Vídeo rotação").  
  
Predefinições disponíveis:  
  
 [H264 taxas de bits múltiplas 1080p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-1080p-Audio-5.1.md) produz um conjunto de 8 arquivos MP4 com alinhamento GOP, variando de 6000 kbps too400 kbps e áudio 5.1 AAC.  
  
 [H264 várias taxas de bits 1080p](media-services-mes-preset-H264-Multiple-Bitrate-1080p.md) produz um conjunto de 8 arquivos MP4 com alinhamento GOP, variando de 6000 kbps too400 kbps e de áudio estéreo AAC.  
  
 [H264 taxas de bits múltiplas 16X9 para iOS](media-services-mes-preset-H264-Multiple-Bitrate-16x9-for-iOS.md) produz um conjunto de 8 arquivos MP4 com alinhamento GOP, variando de 8500 kbps too200 kbps e de áudio estéreo AAC.  
  
 [Taxa de bits H264 múltiplas 16X9 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD-Audio-5.1.md) produz um conjunto de 5 arquivos MP4 com alinhamento GOP, variando de 1900 kbps too400 kbps e áudio 5.1 AAC.  
  
 [Taxas de bits H264 múltiplas 16X9 SD](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD.md) produz um conjunto de 5 arquivos MP4 com alinhamento GOP, variando de 1900 kbps too400 kbps e de áudio estéreo AAC.  
  
 [Taxa de bits H264 múltiplas 4K Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4K-Audio-5.1.md) produz um conjunto de 12 arquivos MP4 com alinhamento GOP, variando de 20.000 kbps too1000 kbps e áudio 5.1 AAC.  
  
 [H264 várias taxas de bits 4K](media-services-mes-preset-H264-Multiple-Bitrate-4K.md) produz um conjunto de 12 arquivos MP4 com alinhamento GOP, variando de 20.000 kbps too1000 kbps e de áudio estéreo AAC.  
  
 [H264 taxas de bits múltiplas 4x3 para iOS](media-services-mes-preset-H264-Multiple-Bitrate-4x3-for-iOS.md) produz um conjunto de 8 arquivos MP4 com alinhamento GOP, variando de 8500 kbps too200 kbps e de áudio estéreo AAC.  
  
 [H264 múltiplas 4x3 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD-Audio-5.1.md) produz um conjunto de 5 arquivos MP4 com alinhamento GOP, variando de 1600 kbps too400 kbps e áudio 5.1 AAC.  
  
 [H264 múltiplas 4x3 SD](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD.md) produz um conjunto de 5 arquivos MP4 com alinhamento GOP, variando de 1600 kbps too400 kbps e de áudio estéreo AAC.  
  
 [H264 taxas de bits múltiplas 720p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-720p-Audio-5.1.md) produz um conjunto de 6 arquivos MP4 com alinhamento GOP, variando de 3400 kbps too400 kbps e áudio 5.1 AAC.  
  
 [H264 várias taxas de bits 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) produz um conjunto de 6 arquivos MP4 com alinhamento GOP, variando de 3400 kbps too400 kbps e de áudio estéreo AAC.  
  
 [H264 Taxa de Bits Única 1080p Áudio 5.1](media-services-mes-preset-H264-Single-Bitrate-1080p-Audio-5.1.md) produz um único arquivo MP4 com uma taxa de bits de 6750 kbps e áudio AAC 5.1.  
  
 [H264 Taxa de Bits Única 1080p](media-services-mes-preset-H264-Single-Bitrate-1080p.md) produz um único arquivo MP4 com uma taxa de bits de 6750 kbps e áudio AAC estéreo.  
  
 [H264 Taxa de Bits Única 4K Áudio 5.1](media-services-mes-preset-H264-Single-Bitrate-4K-Audio-5.1.md) produz um único arquivo MP4 com uma taxa de bits de 18000 kbps e áudio AAC 5.1.  
  
 [H264 Taxa de Bits Única 4K](media-services-mes-preset-H264-Single-Bitrate-4K.md) produz um único arquivo MP4 com uma taxa de bits de 18000 kbps e áudio AAC estéreo.  
  
 [H264 Taxa de Bits Única 4x3 SD Áudio 5.1](media-services-mes-preset-H264-Single-Bitrate-4x3-SD-Audio-5.1.md) produz um único arquivo MP4 com uma taxa de bits de 1800 kbps e áudio AAC 5.1.  
  
 [H264 Taxa de Bits Única 4x3 SD](media-services-mes-preset-H264-Single-Bitrate-4x3-SD.md) produz um único arquivo MP4 com uma taxa de bits de 1800 kbps e áudio AAC estéreo.  
  
 [H264 Taxa de Bits Única 16x9 SD Áudio 5.1](media-services-mes-preset-H264-Single-Bitrate-16x9-SD-Audio-5.1.md) produz um único arquivo MP4 com uma taxa de bits de 2200 kbps e áudio AAC 5.1.  
  
 [H264 Taxa de Bits Única 16x9 SD](media-services-mes-preset-H264-Single-Bitrate-16x9-SD.md) produz um único arquivo MP4 com uma taxa de bits de 2200 kbps e áudio AAC estéreo.  
  
 [H264 Taxa de Bits Única 720p Áudio 5.1](media-services-mes-preset-H264-Single-Bitrate-720p-Audio-5.1.md) produz um único arquivo MP4 com uma taxa de bits de 4500 kbps e áudio AAC 5.1.  
  
 [H264 Taxa de Bits Única 720p para Android](media-services-mes-preset-H264-Single-Bitrate-720p-for-Android.md) produz um único arquivo MP4 com uma taxa de bits de 2000 kbps e AAC estéreo.  
  
 [H264 Taxa de Bits Única 720p](media-services-mes-preset-H264-Single-Bitrate-720p.md) produz um único arquivo MP4 com uma taxa de bits de 4500 kbps e áudio AAC estéreo.  
  
 [H264 Taxa de Bits Única SD de Alta Qualidade para Android](media-services-mes-preset-H264-Single-Bitrate-High-Quality-SD-for-Android.md) produz um único arquivo MP4 com uma taxa de bits de 500 kbps e áudio AAC estéreo.  
  
 [H264 Taxa de Bits Única SD de Baixa Qualidade para Android](media-services-mes-preset-H264-Single-Bitrate-Low-Quality-SD-for-Android.md) produz um único arquivo MP4 com uma taxa de bits de 56 kbps e áudio AAC estéreo.  
  
 Para obter mais informações relacionadas tooMedia serviços codificadores, consulte [codificação sob demanda com o Azure Media Services](https://azure.microsoft.com/en-us/documentation/articles/media-services-encode-asset/).
