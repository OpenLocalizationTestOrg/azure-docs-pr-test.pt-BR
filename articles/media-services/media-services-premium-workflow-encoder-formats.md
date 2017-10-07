---
title: aaaMedia o fluxo de trabalho do codificador Premium codecs e formatos | Microsoft Docs
description: "Este tópico fornece uma visão geral dos codecs e formatos do Fluxo de Trabalho do Media Encoder Premium"
services: media-services
documentationcenter: 
author: juliako
manager: erik43
editor: 
ms.assetid: b197fce8-3b9b-4189-8d08-486810c0426f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;anilmur
ms.openlocfilehash: e781384ca8f08926f00c83b6710fd413ce2a3e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-premium-workflow-formats-and-codecs"></a>Codecs e formatos de fluxo de trabalho do Media Encoder Premium
> [!NOTE]
> Para solucionar dúvidas sobre o codificador premium, envie um email para o mepd em Microsoft.com.
> 
> O processador de mídia do Fluxo de Trabalho do Media Encoder Premium analisado neste tópico não está disponível na China. 
> 
> 

Este documento contém uma lista de formatos de arquivo de entrada e saída e codecs são suportados pela versão de visualização pública de saudação do hello **o fluxo de trabalho do Media Encoder Premium** codificador.

[Codecs e formatos de entrada de fluxo de trabalho do Media Encoder Premium](#input_formats)

[Codecs e formatos de saída de fluxo de trabalho do Media Encoder Premium](#output_formats)

**Fluxo de trabalho do Media Encoder Premium** dá suporte a legendas codificadas descritas [nesta](#closed_captioning) seção 

## <a id="input_formats"></a>Codecs e formatos de entrada de fluxo de trabalho do Media Encoder Premium
Olá seção a seguir lista Olá codecs e formatos de arquivo que oferece suporte a este processador de mídia como entrada.

### <a name="input-containerfile-formats"></a>Formatos de arquivo/contêiner de entrada
* Adobe® Flash® F4V
* MXF/SMPTE 377M
* GXF
* Fluxos de transporte de MPEG-2
* Fluxos de programa MPEG-2
* MPEG-4/MP4
* Windows Media/ASF
* AVI (8 bits/10 bits descompactado)

### <a name="input-video-codecs"></a>Codecs de vídeo de entrada
* AVC 8 bits/10 bits, o too4:2:2, incluindo AVCIntra
* DNxHD ávido (em MXF)
* DVCPro/DVCProHD (em MXF)
* JPEG2000
* MPEG-2 (o perfil too422 e de alto nível, inclusive variantes como XDCAM, XDCAM HD, XDCAM IMX, CableLabs® e D10)
* MPEG-1
* Windows Media Video/VC-1

### <a name="input-audio-codecs"></a>Codecs de áudio de entrada
* AES (SMPTE 331M e 302M, AES3-2003)
* Dolby® E
* Dolby® Digital (AC3)
* AAC (AAC-LC, HE-AAC e AAC-HEv2; o too5.1)
* MPEG Layer 2
* MP3 (MPEG-1 Audio Layer 3)
* Áudio do Windows Media
* WAV/PCM

## <a id="output_format"></a>Codecs e formatos de saída de fluxo de trabalho do Media Encoder Premium
Olá, seção a seguir lista Olá codecs e formatos de arquivo que têm suporte como a saída deste processador de mídia.

### <a name="output-containerfile-formats"></a>Formatos de contêiner/arquivo de saída
* Adobe® Flash® F4V
* MXF (OP1a, XDCAM e AS02)
* DPP (incluindo AS11)
* GXF
* MPEG-4/MP4
* Windows Media/ASF
* AVI (8 bits/10 bits descompactado)
* Formato de arquivo do Smooth Streaming (PIFF 1.3)
* MPEG-TS 

### <a name="output-video-codecs"></a>Codecs de vídeo de saída
* AVC (h. 264; 8 bits; até tooHigh perfil, nível 5.2; HD Ultra de 4K; Dentro de AVC)
* DNxHD ávido (em MXF)
* DVCPro/DVCProHD (em MXF)
* MPEG-2 (o perfil too422 e de alto nível, inclusive variantes como XDCAM, XDCAM HD, XDCAM IMX, CableLabs® e D10)
* MPEG-1
* Windows Media Video/VC-1
* Criação de miniaturas JPEG

### <a name="output-audio-codecs"></a>Codecs de áudio de saída
* AES (SMPTE 331M e 302M, AES3-2003)
* Dolby® Digital (AC3)
* Dolby® Digital Plus (E AC3) backup too7.1
* AAC (AAC-LC, HE-AAC e AAC-HEv2; o too5.1)
* MPEG Layer 2
* MP3 (MPEG-1 Audio Layer 3)
* Áudio do Windows Media

>[!NOTE]
>Se você codificar tooDolby® Digital (AC3), saída de hello só pode ser gravada em um arquivo ISO MP4.

## <a id="closed_captioning"></a>Suporte a legenda codificada
Na ingestão, o **fluxo de trabalho do Media Encoder Premium** dá suporte a:

1. Arquivos SCC
2. Arquivos SMPTE-TT
3. CEA-608/CEA-708 – transportados como dados de usuário (mensagens SEI de fluxos elementares H.264, ATSC/53, SCTE20) ou executados como dados complementares em arquivos MXF/GXF
4. Arquivos de legenda STL

Na saída, Olá as opções a seguir está disponível:

1. 608 CEA 708 tooCEA tradução
2. Transmissão CEA-608/CEA-708 (integrada em mensagens SEI para fluxos elementares H.264, ou carregada como dados auxiliares nos arquivos MXF)
3. SCC
4. Texto cronometrado de SMPTE (de origem CEA-608 por SMPTE RP2052, inclusive criação de arquivo DFXP)
5. Arquivo de legenda SRT
6. Fluxos de legenda DVB

Observação: nem todos os Olá acima formatos de saída são suportados para fornecimento por meio de streaming nos serviços de mídia do Azure.

## <a name="known-issues"></a>Problemas conhecidos
Se o vídeo de entrada não contém a legenda codificada, Olá saída que ativo ainda conterá um arquivo TTML vazio. 

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

