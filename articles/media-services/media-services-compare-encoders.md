---
title: "aaaComparison do Azure em codificadores de mídia de demanda | Microsoft Docs"
description: "Este tópico compara recursos de codificação de saudação do * * Media Encoder padrão * * e * * Media Encoder Premium fluxo de trabalho * *."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: a79437c0-4832-423a-bca8-82632b2c47cc
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: ee04ad10d8e7c5f4f3c6e91e9b7679c2aba82c99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-of-azure-on-demand-media-encoders"></a>Comparação de codificadores de mídia sob demanda do Azure

Este tópico compara recursos de codificação de saudação do **codificador de mídia padrão** e **o fluxo de trabalho do Media Encoder Premium**.

## <a name="video-and-audio-processing-capabilities"></a>Funcionalidades de processamento de vídeo e áudio

Olá, a tabela a seguir compara a funcionalidade de saudação entre o codificador de mídia padrão (MES) e o Media Encoder Premium fluxo de trabalho (MEPW). 

|Recurso|Media Encoder Standard|Fluxo de trabalho do Media Encoder Premium|
|---|---|---|
|Aplicar a lógica condicional durante a codificação<br/>(por exemplo, se entrada hello está HD, em seguida, codificar áudio 5.1)|Não|Sim|
|Legendagem oculta|Não|[Sim](media-services-premium-workflow-encoder-formats.md#closed_captioning)|
|[Dolby® Professional Loudness Correction](http://www.dolby.com/us/en/technologies/dolby-professional-loudness-solutions.pdf)<br/> com Dialogue Intelligence™|Não|Sim|
|Desentrelaçamento, telecine inverso|Basic|Qualidade de difusão|
|Detectar e remover bordas pretas <br/>(formatos pillarbox e letterbox)|Não|Sim|
|Geração de miniaturas|[Sim](media-services-dotnet-generate-thumbnail-with-mes.md)|[Sim](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)|
|Distorção/filtragem e costura de vídeos|[Sim](media-services-advanced-encoding-with-mes.md#trim_video)|Sim|
|Sobreposições de áudio ou vídeo|[Sim](media-services-advanced-encoding-with-mes.md#overlay)|[Sim](media-services-media-encoder-premium-workflow-multiplefilesinput.md#example-1--overlay-an-image-on-top-of-the-video)|
|Sobreposições de elementos gráficos|De fontes de imagem|De fontes de imagem e texto|
|Várias faixas de idioma de áudio|Limitado|[Sim](media-services-media-encoder-premium-workflow-multiplefilesinput.md#example-2--multiple-audio-language-encoding)|

## <a id="billing"></a>Medidor de cobrança usado por cada codificador
| Nome do processador de mídia | Preços aplicáveis | Observações |
| --- | --- | --- |
| **Media Encoder Standard** |CODIFICADOR |Codificação de tarefas serão cobradas com base na duração total hello, em minutos, de todos os arquivos de mídia Olá produzidos como saída, a taxa de saudação especificada [aqui][1], na coluna de CODIFICADOR hello. |
| **Fluxo de trabalho do Media Encoder Premium** |CODIFICADOR PREMIUM |Codificação de tarefas serão cobradas com base na duração total hello, em minutos, de todos os arquivos de mídia Olá produzidos como saída, a taxa de saudação especificada [aqui][1], na coluna de CODIFICADOR PREMIUM Olá. |

## <a name="input-containerfile-formats"></a>Formatos de contêiner/arquivo de entrada
| Formatos de arquivo/contêiner de entrada | Media Encoder Standard | Fluxo de trabalho do Media Encoder Premium |
| --- | --- | --- |
| Adobe® Flash® F4V |Sim |Sim |
| MXF/SMPTE 377M |Sim |Sim |
| GXF |Sim |Sim |
| Fluxos de transporte de MPEG-2 |Sim |Sim |
| Fluxos de programa MPEG-2 |Sim |Sim |
| MPEG-4/MP4 |Sim |Sim |
| Windows Media/ASF |Sim |Sim |
| AVI (8 bits/10 bits descompactado) |Sim |Sim |
| 3GPP/3GPP2 |Sim |Não |
| Formato de arquivo do Smooth Streaming (PIFF 1.3) |Sim |Não |
| [Gravação (DVR-MS) de vídeo Digital da Microsoft](https://msdn.microsoft.com/library/windows/desktop/dd692984) |Sim |Não |
| Matroska/WebM |Sim |Não |
| QuickTime (.mov) |Sim |Não |

## <a name="input-video-codecs"></a>Codecs de vídeo de entrada
| Codecs de vídeo de entrada | Media Encoder Standard | Fluxo de trabalho do Media Encoder Premium |
| --- | --- | --- |
| AVC 8 bits/10 bits, o too4:2:2, incluindo AVCIntra |8 bits 4:2:0 e 4:2:2 |Sim |
| DNxHD ávido (em MXF) |Sim |Sim |
| DVCPro/DVCProHD (em MXF) |Sim |Sim |
| JPEG2000 |Sim |Sim |
| MPEG-2 (o perfil too422 e de alto nível, inclusive variantes como XDCAM, XDCAM HD, XDCAM IMX, CableLabs® e D10) |O perfil de too422 |Sim |
| MPEG-1 |Sim |Sim |
| Windows Media Video/VC-1 |Sim |Sim |
| Canopus HQ/HQX |Não |Não |
| MPEG-4, parte 2 |Sim |Não |
| [Theora](https://en.wikipedia.org/wiki/Theora) |Sim |Não |
| Apple ProRes 422 |Sim |Não |
| Apple ProRes 422 LT |Sim |Não |
| Apple ProRes 422 HQ |Sim |Não |
| Apple ProRes Proxy |Sim |Não |
| Apple ProRes 4444 |Sim |Não |
| Apple ProRes 4444 XQ |Sim |Não |

## <a name="input-audio-codecs"></a>Codecs de áudio de entrada
| Codecs de áudio de entrada | Media Encoder Standard | Fluxo de trabalho do Media Encoder Premium |
| --- | --- | --- |
| AES (SMPTE 331M e 302M, AES3-2003) |Não |Sim |
| Dolby® E |Não |Sim |
| Dolby® Digital (AC3) |Não |Sim |
| Dolby® Digital Plus (E-AC3) |Não |Sim |
| AAC (AAC-LC, HE-AAC e AAC-HEv2; o too5.1) |Sim |Sim |
| MPEG Layer 2 |Sim |Sim |
| MP3 (MPEG-1 Audio Layer 3) |Sim |Sim |
| Áudio do Windows Media |Sim |Sim |
| WAV/PCM |Sim |Sim |
| [FLAC](https://en.wikipedia.org/wiki/FLAC)</a> |Sim |Não |
| [Opus](https://en.wikipedia.org/wiki/Opus_\(audio_format\)) |Sim |Não |
| [Vorbis](https://en.wikipedia.org/wiki/Vorbis)</a> |Sim |Não |

## <a name="output-containerfile-formats"></a>Formatos de contêiner/arquivo de saída
| Formatos de contêiner/arquivo de saída | Media Encoder Standard | Fluxo de trabalho do Media Encoder Premium |
| --- | --- | --- |
| Adobe® Flash® F4V |Não |Sim |
| MXF (OP1a, XDCAM e AS02) |Não |Sim |
| DPP (incluindo AS11) |Não |Sim |
| GXF |Não |Sim |
| MPEG-4/MP4 |Sim |Sim |
| MPEG-TS |Sim |Sim |
| Windows Media/ASF |Não |Sim |
| AVI (8 bits/10 bits descompactado) |Não |Sim |
| Formato de arquivo do Smooth Streaming (PIFF 1.3) |Não |Sim |

## <a name="output-video-codecs"></a>Codecs de vídeo de saída
| Codecs de vídeo de saída | Media Encoder Standard | Fluxo de trabalho do Media Encoder Premium |
| --- | --- | --- |
| AVC (h. 264; 8 bits; até tooHigh perfil, nível 5.2; HD Ultra de 4K; Dentro de AVC) |Somente 8 bits 4:2:0 |Sim |
| DNxHD ávido (em MXF) |Não |Sim |
| MPEG-2 (o perfil too422 e de alto nível, inclusive variantes como XDCAM, XDCAM HD, XDCAM IMX, CableLabs® e D10) |Não |Sim |
| MPEG-1 |Não |Sim |
| Windows Media Video/VC-1 |Não |Sim |
| Criação de miniaturas JPEG |Sim |Sim |
| Criação de miniaturas PNG |Sim |Sim |
| Criação de miniaturas BMP |Sim |Não |

## <a name="output-audio-codecs"></a>Codecs de áudio de saída
| Codecs de áudio de saída | Media Encoder Standard | Fluxo de trabalho do Media Encoder Premium |
| --- | --- | --- |
| AES (SMPTE 331M e 302M, AES3-2003) |Não |Sim |
| Dolby® Digital (AC3) |Não |Sim |
| Dolby® Digital Plus (E AC3) backup too7.1 |Não |Sim |
| AAC (AAC-LC, HE-AAC e AAC-HEv2; o too5.1) |Sim |Sim |
| MPEG Layer 2 |Não |Sim |
| MP3 (MPEG-1 Audio Layer 3) |Não |Sim |
| Áudio do Windows Media |Não |Sim |

>[!NOTE]
>Se você codificar tooDolby® Digital (AC3), saída de hello só pode ser gravada em um arquivo ISO MP4.

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Artigos relacionados
* [Executar tarefas avançadas de codificação ao personalizar predefinições do Codificador de Mídia Padrão](media-services-custom-mes-presets-with-dotnet.md)
* [Cotas e limitações](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
