---
title: "codecs e formatos de codificador padrão aaaMedia"
description: "Este tópico oferece uma visão geral dos codecs e dos formatos do Codificador de Mídia Padrão."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: f334b1ce-2f56-4968-a019-f0a2b0016d9f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 51a67f372dff579383ffcfa988e8f4d38ad44a72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-standard-formats-and-codecs"></a>Codecs e formatos padrão do codificador de mídia
Este documento contém uma lista de importação de hello mais comuns e formatos de arquivo de exportação que você pode usar com o codificador de mídia padrão.

## <a name="input-containerfile-formats"></a>Formatos de arquivo/contêiner de entrada
| Formatos de arquivo (extensões de arquivo) | Suportado |
| --- | --- | --- | --- |
| FLV (com codecs H.264 e AAC) (.flv) |sim |
| MXF    (.mxf) |sim |
| GXF    (.gxf) |Sim |
| MPEG2-PS, MPEG2-TS, 3GP (.ts, .ps, .3gp, .3gpp, .mpg) |Sim |
| Vídeo do Windows Media (WMV)/ASF (.wmv, .asf) |Sim |
| AVI (8 bits/10 bits descompactado) (.avi) |Sim |
| MP4 (.mp4, .m4a, .m4v)/ISMV (.isma, .ismv) |Sim |
| [Gravação (DVR-MS) de vídeo Digital da Microsoft](https://msdn.microsoft.com/library/windows/desktop/dd692984) (.dvr-ms) |Sim |
| Matroska/WebM (.mkv) |Sim |
| WAVE/WAV (.wav) |Sim |
| QuickTime (.mov) |Sim |

> [!NOTE]
> Acima é uma lista de extensões de arquivo hello mais comumente encontrado. O Media Encoder Standard dá suporte a muitos outros (por exemplo: .m2ts, .mpeg2video, .qt). Se você tentar tooencode um arquivo e você receber uma mensagem de erro sobre o formato de saudação não tem suporte, forneça um feedback [aqui](https://feedback.azure.com/forums/169396-media-services/category/144411-encoding-and-processing/).
> 
> 

### <a name="audio-formats-in-input-containers"></a>Formatos de áudio em contêineres de entrada
Codificador de mídia padrão oferece suporte a transporte Olá formatos de áudio em contêineres de entrada a seguir:

* Arquivos do MXF, GXF e QuickTime que têm faixas de áudio com exemplos em estéreo intercalado ou de 5.1

ou o

* Arquivos MXF, GXF e QuickTime onde áudio Olá é executado como mapeamento de canal hello, mas faixas separadas de PCM (toostereo ou 5.1) pode ser deduzido dos metadados do arquivo hello

Observe que oferecem suporte para mapeamento de canal explícita/fornecido pelo usuário será fornecido no hello futuro próximo.

## <a name="input-video-codecs"></a>Codecs de vídeo de entrada
| Codecs de vídeo de entrada | Suportado |
| --- | --- | --- | --- |
| AVC 8 bits/10 bits, o too4:2:2, incluindo AVCIntra |8 bits 4:2:0 e 4:2:2 |
| DNxHD ávido (em MXF) |Sim |
| DVCPro/DVCProHD (em MXF) |Sim |
| Vídeo digital (VD) (em arquivos AVI) |Sim |
| JPEG 2000 |Sim |
| MPEG-2 (o perfil too422 e de alto nível, inclusive variantes como XDCAM, XDCAM HD, XDCAM IMX, CableLabs® e D10) |O perfil de too422 |
| MPEG-1 |Sim |
| VC-1/WMV9 |Sim |
| Canopus HQ/HQX |Não |
| MPEG-4, parte 2 |Sim |
| [Theora](https://en.wikipedia.org/wiki/Theora) |Sim |
| YUV420 descompactado, ou mezzanine |Sim |
| Apple ProRes 422 |Sim |
| Apple ProRes 422 LT |Sim |
| Apple ProRes 422 HQ |Sim |
| Apple ProRes Proxy |Sim |
| Apple ProRes 4444 |Sim |
| Apple ProRes 4444 XQ |Sim |

## <a name="input-audio-codecs"></a>Codecs de áudio de entrada
| Codecs de áudio de entrada | Suportado |
| --- | --- | --- | --- |
| AAC (AAC-LC, HE-AAC e AAC-HEv2; o too5.1) |Sim |
| MPEG Layer 2 |Sim |
| MP3 (MPEG-1 Audio Layer 3) |Sim |
| Áudio do Windows Media |Sim |
| WAV/PCM |Sim |
| [FLAC](https://en.wikipedia.org/wiki/FLAC)</a> |Sim |
| [Opus](http://go.microsoft.com/fwlink/?LinkId=822667) |Sim |
| [Vorbis](https://en.wikipedia.org/wiki/Vorbis)</a> |Sim |
| AMR (multitaxa adaptável) |Sim |
| AES (SMPTE 331M e 302M, AES3-2003) |Não |
| Dolby® E |Não |
| Dolby® Digital (AC3) |Não |
| Dolby® Digital Plus (E-AC3) |Não |

## <a name="output-formats-and-codecs"></a>Formatos e codecs de saída
Olá, a tabela a seguir lista Olá codecs e formatos de arquivo com suporte para exportação.

| Formato de arquivo | Codec de vídeo | Codec de áudio |
| --- | --- | --- |
| MP4  <br/><br/>(incluindo contêineres MP4 de múltiplas taxas de bits) |H.264 (Perfis Alto, Principal e Linha de base) |AAC-LC, HE-AAC v1, HE-AAC v2 |
| MPEG2-TS |H.264 (Perfis Alto, Principal e Linha de base) |AAC-LC, HE-AAC v1, HE-AAC v2 |

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Consulte também
[Codificando conteúdo sob demanda com os Serviços de Mídia do Azure](media-services-encode-asset.md)

[Como tooencode com o codificador de mídia padrão](media-services-dotnet-encode-with-media-encoder-standard.md)

