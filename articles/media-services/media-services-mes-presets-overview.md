---
title: "Predefinições de tarefa para MES (Media Encoder Standard) | Microsoft Docs"
description: "Este tópico apresenta uma visão geral das Predefinições de tarefa para MES (Media Encoder Standard)."
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
ms.openlocfilehash: 6fcdd361b7725b1a5136828cede24cdaac5dacc1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="task-presets-for-mes-media-encoder-standard"></a>Predefinições de tarefa para MES (Media Encoder Standard)

O **Media Encoder Standard** define um conjunto de predefinições de codificação que pode ser usado ao criar trabalhos de codificação. Será recomendável usar a predefinição “Transmissão Adaptável” se você desejar codificar um vídeo para transmissão com os Serviços de Mídia. Ao especificar essa predefinição, o Media Encoder Standard [gerará uma escada de taxa de bits automaticamente](media-services-autogen-bitrate-ladder-with-mes.md). 

No entanto, se precisar personalizar uma predefinição de codificação, use uma das predefinições de codificação definidas nesta seção como um modelo para a configuração personalizada. Para obter explicações sobre o significado de cada elemento nessas predefinições, e os valores válidos para cada elemento, veja o tópico [Esquema do Media Encoder Standard](media-services-mes-schema.md).  
  
> [!NOTE]
>  Ao usar uma predefinição para codificações 4k, você deverá adquirir o tipo de unidade reservada `S3`. Para saber mais, confira [Como dimensionar a codificação](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).  
  
Ao trabalhar com o Media Encoder Standard, a rotação é habilitada por padrão. Se o vídeo foi gravado em um smartphone ou em outro dispositivo móvel no modo Retrato, essas predefinições o girarão por padrão para modo Paisagem antes da codificação (ao contrário de quando você trabalha com o Codificador de Mídia do Azure, no qual a rotação do vídeo é uma operação manual, conforme documentado [neste](http://azure.microsoft.com/blog/2014/08/21/advanced-encoding-features-in-azure-media-encoder/) blog, em "Video Rotation" [Rotação do vídeo]).  
  
Predefinições disponíveis:  
  
 [H264 Taxas de Bits Múltiplas 1080p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-1080p-Audio-5.1.md) produz um conjunto de 8 arquivos MP4 alinhados a GOP, variando de 6000 kbps a 400 kbps, e áudio AAC 5.1.  
  
 [H264 Taxas de Bits Múltiplas 1080p](media-services-mes-preset-H264-Multiple-Bitrate-1080p.md) produz um conjunto de 8 arquivos MP4 alinhados a GOP, variando de 6000 kbps a 400 kbps, e áudio AAC estéreo.  
  
 [H264 Taxas de Bits Múltiplas 16x9 para iOS](media-services-mes-preset-H264-Multiple-Bitrate-16x9-for-iOS.md) produz um conjunto de 8 arquivos MP4 alinhados a GOP, variando de 8500 kbps a 200 kbps, e áudio AAC estéreo.  
  
 [H264 Taxas de Bits Múltiplas 16x9 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD-Audio-5.1.md) produz um conjunto de 5 arquivos MP4 alinhados a GOP, variando de 1900 kbps a 400 kbps, e áudio AAC 5.1.  
  
 [H264 Taxas de Bits Múltiplas 16x9 SD](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD.md) produz um conjunto de 5 arquivos MP4 alinhados a GOP, variando de 1900 kbps a 400 kbps, e áudio AAC estéreo.  
  
 [H264 Taxas de Bits Múltiplas 4K Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4K-Audio-5.1.md) produz um conjunto de 12 arquivos MP4 alinhados a GOP, variando de 20000 kbps a 1000 kbps, e áudio AAC 5.1.  
  
 [H264 Taxas de Bits Múltiplas 4K](media-services-mes-preset-H264-Multiple-Bitrate-4K.md) produz um conjunto de 12 arquivos MP4 alinhados a GOP, variando de 20000 kbps a 1000 kbps, e áudio AAC estéreo.  
  
 [H264 Taxas de Bits Múltiplas 4x3 para iOS](media-services-mes-preset-H264-Multiple-Bitrate-4x3-for-iOS.md) produz um conjunto de 8 arquivos MP4 alinhados a GOP, variando de 8500 kbps a 200 kbps, e áudio AAC estéreo.  
  
 [H264 Taxas de Bits Múltiplas 4x3 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD-Audio-5.1.md) produz um conjunto de 5 arquivos MP4 alinhados a GOP, variando de 1600 kbps a 400 kbps, e áudio AAC 5.1.  
  
 [H264 Taxas de Bits Múltiplas 4x3 SD](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD.md) produz um conjunto de 5 arquivos MP4 alinhados a GOP, variando de 1600 kbps a 400 kbps, e áudio AAC estéreo.  
  
 [H264 Taxas de Bits Múltiplas 720p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-720p-Audio-5.1.md) produz um conjunto de 6 arquivos MP4 alinhados a GOP, variando de 3400 kbps a 400 kbps, e áudio AAC 5.1.  
  
 [H264 Taxas de Bits Múltiplas 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) produz um conjunto de 6 arquivos MP4 alinhados a GOP, variando de 3400 kbps a 400 kbps, e áudio AAC estéreo.  
  
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
  
 Para saber mais sobre os codificadores dos Serviços de Mídia, veja [Codificação sob demanda com os Serviços de Mídia do Azure](https://azure.microsoft.com/en-us/documentation/articles/media-services-encode-asset/).
