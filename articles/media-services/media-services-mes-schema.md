---
title: "esquema padrão do codificador aaaMedia | Microsoft Docs"
description: "tópico de saudação fornece uma visão geral do esquema padrão do Media Encoder hello."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 4c060062-8ef2-41d9-834e-e81e8eafcf2e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 82bad27b9546f75557ac691ff148b46990647632
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-standard-schema"></a>Esquema do Media Encoder Standard
Este tópico descreve alguns dos elementos de saudação e tipos de esquema XML, Olá no qual [predefinições de codificador de mídia padrão](media-services-mes-presets-overview.md) se baseiam. tópico de saudação fornece uma explicação das elementos e seus valores válidos. o esquema completo Hello será publicado em uma data posterior.  

## <a name="Preset"></a> Predefinição (elemento raiz)
Define uma predefinição de codificação.  

### <a name="elements"></a>Elementos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Codificação** |[Codificação](media-services-mes-schema.md#Encoding) |Elemento raiz, indica que as fontes de entrada hello toobe codificado. |
| **Saídas** |[Saídas](media-services-mes-schema.md#Output) |Coleção dos arquivos de saída desejados. |

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Versão**<br/><br/> Obrigatório |**xs:decimal** |Olá predefinição versão. Olá seguintes restrições se aplicam: valor xs:fractionDigits = "1" e xs:minInclusive value = "1" por exemplo, **versão = "1.0"**. |

## <a name="Encoding"></a> Codificação
Contém uma sequência de saudação elementos a seguir.  

### <a name="elements"></a>Elementos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **H264Video** |[H264Video](media-services-mes-schema.md#H264Video) |Configurações de codificação de vídeo H.264. |
| **AACAudio** |[AACAudio](media-services-mes-schema.md#AACAudio) |Configurações de codificação de áudio AAC. |
| **BmpImage** |[BmpImage](media-services-mes-schema.md#BmpImage) |Configurações de imagem Bmp. |
| **PngImage** |[PngImage](media-services-mes-schema.md#PngImage) |Configurações de imagem Png. |
| **JpgImage** |[JpgImage](media-services-mes-schema.md#JpgImage) |Configurações de imagem Jpg. |

## <a name="H264Video"></a> H264Video
### <a name="elements"></a>Elementos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **TwoPass**<br/><br/> minOccurs="0" |**xs:boolean** |Atualmente, há suporte apenas para a codificação em uma passo. |
| **KeyFrameInterval**<br/><br/> minOccurs="0"<br/><br/> **default="00:00:02"** |**xs:time** |Determina a saudação fixada espaçamento entre quadros IDR em unidades de segundos. Também chamado de duração de GOP tooas hello. Consulte **SceneChangeDetection** (abaixo) para controlar se hello codificador pode desviar desse valor. |
| **SceneChangeDetection**<br/><br/> minOccurs="0"<br/><br/> default=”false” |**xs:boolean** |Se set tootrue, tentativas de codificador cena toodetect alterar vídeo hello e insere um quadro IDR. |
| **Complexity**<br/><br/> minOccurs="0"<br/><br/> default="Balanced" |**xs:string** |Controles Olá compensação entre a codificar a qualidade de vídeo e de velocidade. Pode ser uma saudação valores a seguir: **velocidade**, **equilibrado**, ou **qualidade**<br/><br/> Padrão: **Balanced** |
| **SyncMode**<br/><br/> minOccurs="0" | |O recurso será exposto em versões futuras. |
| **H264Layers**<br/><br/> minOccurs="0" |[H264Layers](media-services-mes-schema.md#H264Layers) |Coleção de camadas de vídeo de saída. |

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Condição** |**xs:string** | Quando a entrada de saudação não tem vídeo, talvez você queira tooforce Olá codificador tooinsert uma faixa de vídeo monocromática. toodo que usar condição = "InsertBlackIfNoVideoBottomLayerOnly" (tooinsert um vídeo em apenas hello mais baixa taxa de bits) ou condição = "InsertBlackIfNoVideo" (tooinsert um vídeo em todas as taxas de bits de saída). Para obter mais informações, consulte [este](media-services-advanced-encoding-with-mes.md#no_video) tópico.|

## <a name="H264Layers"></a> H264Layers

Por padrão, se você enviar um codificador de toohello de entrada que contenha apenas áudio e nenhum vídeo, Olá ativo de saída conterá arquivos com apenas os dados de áudio. Alguns players podem não ser capazes de toohandle tal fluxos de saída. Você pode usar do hello H264Video **InsertBlackIfNoVideo** atributo definindo uma saída de toohello da faixa de vídeo de tooforce Olá codificador tooadd nesse cenário. Para obter mais informações, consulte [este](media-services-advanced-encoding-with-mes.md#no_video) tópico.
              
### <a name="elements"></a>Elementos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **H264Layer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[H264Layer](media-services-mes-schema.md#H264Layer) |Uma coleção de camadas de H264. |

## <a name="H264Layer"></a> H264Layer
> [!NOTE]
> Limites de vídeo são baseados nos valores de saudação descritos em Olá [H264 níveis](https://en.wikipedia.org/wiki/H.264/MPEG-4_AVC#Levels) tabela.  
> 
> 

### <a name="elements"></a>Elementos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Perfil**<br/><br/> minOccurs="0"<br/><br/> default=”Auto” |**xs:string** |Pode ser de um dos seguintes Olá **xs: string** valores: **automática**, **Baseline**, **principal**, **alta**. |
| **Level**<br/><br/> minOccurs="0"<br/><br/> default=”Auto” |**xs:string** | |
| **Bitrate**<br/><br/> minOccurs="0" |**xs:int** |taxa de bits Olá usada para esta camada de vídeo, especificada em kbps. |
| **MaxBitrate**<br/><br/> minOccurs="0" |**xs:int** |Olá taxa de bits máxima usada para esta camada de vídeo, especificada em kbps. |
| **BufferWindow**<br/><br/> minOccurs="0"<br/><br/> default="00:00:05" |**xs:time** |Comprimento do buffer de vídeo de saudação. |
| **Width**<br/><br/> minOccurs="0" |**xs:int** |Largura da saudação saída quadros do vídeo, em pixels.<br/><br/> Observe que, no momento, você deve especificar ambos Width e Height. Olá largura e altura necessário toobe os números pares. |
| **Height**<br/><br/> minOccurs="0" |**xs:int** |Altura da saudação saída quadros do vídeo, em pixels.<br/><br/> Observe que, no momento, você deve especificar ambos Width e Height. Olá largura e altura necessário toobe os números pares.|
| **BFrames**<br/><br/> minOccurs="0" |**xs:int** |Número de quadros B entre quadros de referência. |
| **ReferenceFrames**<br/><br/> minOccurs="0"<br/><br/> default=”3” |**xs:int** |Número de quadros de referência em um GOP. |
| **EntropyMode**<br/><br/> minOccurs="0"<br/><br/> default=”Cabac” |**xs:string** |Pode ser uma saudação valores a seguir: **Cabac** e **Cavlc**. |
| **FrameRate**<br/><br/> minOccurs="0" |número racional |Determina a taxa de quadros de saudação do vídeo de saída de hello. Use padrão de "1/0" toolet Olá codificador use Olá mesmo quadro taxa como saudação de entrada de vídeo. Valores permitidos são toobe esperado comuns taxas de quadros do vídeo, conforme mostrado abaixo. No entanto, qualquer valor racional é permitido. Por exemplo, 1/1 seria 1 fps e é válido.<br/><br/> -12/1 (12 fps)<br/><br/> -15/1 (15 fps)<br/><br/> -24/1 (24 fps)<br/><br/> -24.000/1.001 (23.976 fps)<br/><br/> - 25/1 (25 fps)<br/><br/>  - 30/1 (30 fps)<br/><br/> - 30.000/1.001 (29,97 fps) <br/> <br/>**Observação** se você estiver criando uma predefinição de codificação de várias taxas de bits personalizada, predefinição de todas as camadas de hello, em seguida, **deve** use Olá mesmo valor de taxa de quadros.|
| **AdaptiveBFrame**<br/><br/> minOccurs="0" |**xs:boolean** |Cópia do Codificador de Mídia do Azure |
| **Slices**<br/><br/> minOccurs="0"<br/><br/> default="0" |**xs:int** |Determina em quantas fatias um quadro é dividido. É recomendável usar o padrão. |

## <a name="AACAudio"></a> AACAudio
 Contém uma sequência de saudação elementos a seguir e grupos.  

 Para saber mais sobre AAC, veja [AAC](https://en.wikipedia.org/wiki/Advanced_Audio_Coding).  

### <a name="elements"></a>Elementos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Perfil**<br/><br/> minOccurs="0 "<br/><br/> default="AACLC" |**xs:string** |Pode ser uma saudação valores a seguir: **AACLC**, **HEAACV1**, ou **HEAACV2**. |

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Condição** |**xs:string** |tooforce Olá codificador tooproduce um ativo que contenha uma faixa de áudio silenciosa quando a entrada não tem áudio, especifique o valor de "InsertSilenceIfNoAudio" hello.<br/><br/> Por padrão, se você enviar um codificador de toohello de entrada que contenha apenas vídeo e nenhum áudio, Olá ativo de saída conterá os arquivos que contêm dados de apenas vídeo. Alguns players podem não ser capazes de toohandle tal fluxos de saída. Você pode usar essa configuração tooforce Olá codificador tooadd uma saída de toohello silenciosa faixa de áudio nesse cenário. |

### <a name="groups"></a>Grupos
| Referência | Descrição |
| --- | --- |
| [AudioGroup](media-services-mes-schema.md#AudioGroup)<br/><br/> minOccurs="0" |Consulte a descrição do [AudioGroup](media-services-mes-schema.md#AudioGroup) tooknow Olá número apropriado de canais, taxa de amostragem e a taxa de bits que pode ser definida para cada perfil. |

## <a name="AudioGroup"></a> AudioGroup
Para obter detalhes sobre quais valores são válidos para cada perfil, consulte a tabela a "Detalhes de codec de áudio" hello que segue.  

### <a name="elements"></a>Elementos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Channels**<br/><br/> minOccurs="0" |**xs:int** |número de saudação de canais de áudio codificado. Olá, estes são opções válidas: 1, 2, 5, 6, 8.<br/><br/> Padrão: 2. |
| **SamplingRate**<br/><br/> minOccurs="0" |**xs:int** |taxa de amostragem de áudio Hello, especificada em Hz. |
| **Bitrate**<br/><br/> minOccurs="0" |**xs:int** |taxa de bits de saudação usada quando a codificação de áudio hello, especificada em kbps. |

### <a name="audio-codec-details"></a>Detalhes do codec de áudio
Codec de áudio|Detalhes  
-----------------|---  
**AACLC**|1:<br/><br/> - 11025 : 8 &lt;= taxa de bits &lt; 16<br/><br/> - 12000 : 8 &lt;= taxa de bits &lt; 16<br/><br/> - 16000 : 8 &lt;= taxa de bits &lt;32<br/><br/>- 22050 : 24 &lt;= taxa de bits &lt; 32<br/><br/> - 24000 : 24 &lt;= taxa de bits &lt; 32<br/><br/> - 32000 : 32 &lt;= taxa de bits &lt;= 192<br/><br/> - 44100 : 56 &lt;= taxa de bits &lt;= 288<br/><br/> - 48000 : 56 &lt;= taxa de bits &lt;= 288<br/><br/> - 88200 : 128 &lt;= taxa de bits &lt;= 288<br/><br/> - 96000 : 128 &lt;= taxa de bits &lt;= 288<br/><br/> 2:<br/><br/> - 11025 : 16 &lt;= taxa de bits &lt; 24<br/><br/> - 12000 : 16 &lt;= taxa de bits &lt; 24<br/><br/> - 16000 : 16 &lt;= taxa de bits &lt; 40<br/><br/> - 22050 : 32 &lt;= taxa de bits &lt; 40<br/><br/> - 24000 : 32 &lt;= taxa de bits &lt; 40<br/><br/> - 32000 : 40 &lt;= taxa de bits &lt;= 384<br/><br/> - 44100 : 96 &lt;= taxa de bits &lt;= 576<br/><br/> - 48000 : 96 &lt;= taxa de bits &lt;= 576<br/><br/> - 88200 : 256 &lt;= taxa de bits &lt;= 576<br/><br/> - 96000 : 256 &lt;= taxa de bits &lt;= 576<br/><br/> 5/6:<br/><br/> - 32000 : 160 &lt;= taxa de bits &lt;= 896<br/><br/> - 44100 : 240 &lt;= taxa de bits &lt;= 1024<br/><br/> - 48000 : 240 &lt;= taxa de bits &lt;= 1024<br/><br/> - 88200 : 640 &lt;= taxa de bits &lt;= 1024<br/><br/> - 96000 : 640 &lt;= taxa de bits &lt;= 1024<br/><br/> 8:<br/><br/> - 32000 : 224 &lt;= taxa de bits &lt;= 1024<br/><br/> - 44100 : 384 &lt;= taxa de bits &lt;= 1024<br/><br/> - 48000 : 384 &lt;= taxa de bits &lt;= 1024<br/><br/> - 88200 : 896 &lt;= taxa de bits &lt;= 1024<br/><br/> - 96000 : 896 &lt;= taxa de bits &lt;= 1024  
**HEAACV1**|1:<br/><br/> - 22050 : taxa de bits = 8<br/><br/> - 24000 : 8 &lt;= taxa de bits &lt;= 10<br/><br/> - 32000 : 12 &lt;= taxa de bits &lt;= 64<br/><br/> - 44100 : 20 &lt;= taxa de bits &lt;= 64<br/><br/> - 48000 : 20 &lt;= taxa de bits &lt;= 64<br/><br/> - 88200 : taxa de bits = 64<br/><br/> 2:<br/><br/> - 32000 : 16 &lt;= taxa de bits &lt;= 128<br/><br/> - 44100 : 16 &lt;= taxa de bits &lt;= 128<br/><br/> - 48000 : 16 &lt;= taxa de bits &lt;= 128<br/><br/> - 88200 : 96 &lt;= taxa de bits &lt;= 128<br/><br/> - 96000 : 96 &lt;= taxa de bits &lt;= 128<br/><br/> 5/6:<br/><br/> - 32000 : 64 &lt;= taxa de bits &lt;= 320<br/><br/> - 44100 : 64 &lt;= taxa de bits &lt;= 320<br/><br/> - 48000 : 64 &lt;= taxa de bits &lt;= 320<br/><br/> - 88200 : 256 &lt;= taxa de bits &lt;= 320<br/><br/> - 96000 : 256 &lt;= taxa de bits &lt;= 320<br/><br/> 8:<br/><br/> - 32000 : 96 &lt;= taxa de bits &lt;= 448<br/><br/> - 44100 : 96 &lt;= taxa de bits &lt;= 448<br/><br/> - 48000 : 96 &lt;= taxa de bits &lt;= 448<br/><br/> - 88200 : 384 &lt;= taxa de bits &lt;= 448<br/><br/> - 96000 : 384 &lt;= taxa de bits &lt;= 448  
**HEAACV2**|2:<br/><br/> - 22050 : 8 &lt;= taxa de bits &lt;= 10<br/><br/> - 24000 : 8 &lt;= taxa de bits &lt;= 10<br/><br/> - 32000 : 12 &lt;= taxa de bits &lt;= 64<br/><br/> - 44100 : 20 &lt;= taxa de bits &lt;= 64<br/><br/> - 48000 : 20 &lt;= taxa de bits &lt;= 64<br/><br/> - 88200 : 64 &lt;= taxa de bits &lt;= 64  
  

## <a name="Clip"></a> Clip
### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **StartTime** |**xs:duration** |Especifica a hora de início de saudação de uma apresentação. Olá. o valor de StartTime deve toomatch Olá absoluto carimbos de hora de vídeo de entrada hello. Por exemplo, se hello primeiro quadro de vídeo de entrada hello tem um carimbo de hora de 12:00:10.000, StartTime deve ser pelo menos 12:00:10.000 ou superior. |
| **Duração** |**xs:duration** |Especifica a duração de saudação de uma apresentação (por exemplo, a aparência de uma sobreposição de vídeo Olá). |

## <a name="Output"></a> Output
### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **FileName** |**xs:string** |nome de Olá Olá do arquivo de saída.<br/><br/> Você pode usar macros descritas em Olá nomes de arquivo de saída do tabela toobuild Olá a seguir. Por exemplo:<br/><br/> **"Outputs": [      {       "FileName": "{Basename}*{Resolution}*{Bitrate}.mp4",       "Format": {         "Type": "MP4Format"       }     }   ]** |

### <a name="macros"></a>Macros
| Macro | Descrição |
| --- | --- |
| **{Basename}** |Se você estiver fazendo VoD codificação, Olá {nome base} é Olá primeiros 32 caracteres da propriedade de AssetFile.Name de saudação do arquivo primário de saudação no ativo de entrada hello.<br/><br/> Se o ativo de entrada hello é um arquivo em tempo real, em seguida, Olá {nome base} é derivado do atributos de trackName Olá no manifesto do servidor de saudação. Se você estiver enviando um trabalho de subclip usando Olá TopBitrate, como em: "< VideoStream\>TopBitrate < / VideoStream\>" e arquivo de saída de hello contém vídeo, Olá {nome base} é Olá primeiros 32 caracteres da saudação trackName de saudação camada de vídeo com taxa de bits máxima hello.<br/><br/> Se, em vez disso, você está enviando um trabalho subclip usando todas as taxas de bits entrada hello, como "< VideoStream\>* < / VideoStream\>" e Olá arquivo de saída contém vídeo, {nome base} é hello primeiro 32 caracteres da saudação trackName de camada de vídeo de saudação correspondente. |
| **{Codec}** |Mapeia muito "H264" para vídeo e áudio "AAC". |
| **{Bitrate}** |Olá destino vídeo com taxa de bits se Olá arquivo de saída contém áudio e vídeo ou áudio taxas de bits de destino se o arquivo de saída de hello somente de áudio. valor de saudação usado é a taxa de bits de saudação em kbps. |
| **{Channel}** |Contagem de canais de áudio se o arquivo hello contém áudio. |
| **{Width}** |Largura da saudação vídeo, em pixels, no arquivo de saída de hello, se o arquivo hello contém vídeo. |
| **{Height}** |Altura do vídeo, em pixels, no arquivo de saída de hello, se o arquivo hello contém vídeo de saudação. |
| **{Extension}** |Herda de Olá propriedade "Type" hello arquivo de saída. nome do arquivo de saída de Hello terá uma extensão que é um de: "mp4", "ts", "jpg", "png" ou "bmp". |
| **{Index}** |Obrigatório para a miniatura. Deve estar presente apenas uma vez. |

## <a name="Video"></a> Video (o tipo complexo herda do Codec)
### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Iniciar** |**xs:string** | |
| **Step** |**xs:string** | |
| **Range** |**xs:string** | |
| **PreserveResolutionAfterRotation** |**xs:boolean** |Para uma explicação detalhada, consulte Olá seção a seguir: [PreserveResolutionAfterRotation](media-services-mes-schema.md#PreserveResolutionAfterRotation) |

### <a name="PreserveResolutionAfterRotation"></a> PreserveResolutionAfterRotation
É recomendável sinalizador de PreserveResolutionAfterRotation toouse Olá em combinação com os valores de resolução expressados em termos percentuais (Width = "100%" Height = "100%").  

Por padrão, Olá codificar as configurações de resolução (largura, altura) em Olá predefinições de codificador de mídia padrão (MES) são destinadas a vídeos com 0 grau de rotação. Por exemplo, se o vídeo de entrada for 1280x720 com zero grau de rotação, a saudação padrão predefinições Verifique se saída Olá tem Olá mesma resolução. Ver a figura abaixo.  

![MESRoation1](./media/media-services-shemas/media-services-mes-roation1.png) 

No entanto, isso significa que, se o vídeo de entrada hello foi capturado com rotação diferente de zero (por exemplo. um smartphone ou tablet mantido verticalmente), e em seguida, MES por padrão se aplicará Olá codificar resolução configurações (largura, altura) toohello vídeo de entrada e, em seguida, compensar a rotação de saudação. Por exemplo, consulte a imagem de saudação abaixo. predefinição Hello usa largura = "100%" Height = "100%", que MES interpreta como exigir Olá saída toobe 1280 pixels ampla e 720 pixels de altura. Após girar vídeo Olá, em seguida, reduz Olá imagem toofit essa janela, líderes áreas toopillar caixa Olá para esquerda e direita.  

![MESRoation2](./media/media-services-shemas/media-services-mes-roation2.png) 

Se Olá acima não é o comportamento de saudação desejado, você pode fazer uso de saudação PreserveResolutionAfterRotation sinalizador e defini-lo muito "true" (o padrão é "false"). Então se seu predefinido tem largura = "100%" Height = "100%" e PreserveResolutionAfterRotation definido muito "verdadeiro", um vídeo de entrada que é 1280 pixels de largura e 720 pixels de altura com rotação de 90 graus produzirá uma saída com rotação zero grau, mas 720 pixels de largura e 1280 pixels de altura. Consulte a imagem de saudação abaixo.  

![MESRoation3](./media/media-services-shemas/media-services-mes-roation3.png) 

## <a name="FormatGroup"></a> FormatGroup (grupo)
### <a name="elements"></a>Elementos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **BmpFormat** |**BmpFormat** | |
| **PngFormat** |**PngFormat** | |
| **JpgFormat** |**JpgFormat** | |

## <a name="BmpLayer"></a> BmpLayer
### <a name="element"></a>Elemento
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Width**<br/><br/> minOccurs="0" |**xs:int** | |
| **Height**<br/><br/> minOccurs="0" |**xs:int** | |

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Condição** |**xs:string** | |

## <a name="PngLayer"></a> PngLayer
### <a name="element"></a>Elemento
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Width**<br/><br/> minOccurs="0" |**xs:int** | |
| **Height**<br/><br/> minOccurs="0" |**xs:int** | |

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Condição** |**xs:string** | |

## <a name="JpgLayer"></a> JpgLayer
### <a name="element"></a>Elemento
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Width**<br/><br/> minOccurs="0" |**xs:int** | |
| **Height**<br/><br/> minOccurs="0" |**xs:int** | |
| **Quality**<br/><br/> minOccurs="0" |**xs:int** |Valores válidos: 1 (pior) – 100 (melhor) |

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Condição** |**xs:string** | |

## <a name="PngLayers"></a> PngLayers
### <a name="elements"></a>Elementos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **PngLayer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[PngLayer](media-services-mes-schema.md#PngLayer) | |

## <a name="BmpLayers"></a> BmpLayers
### <a name="elements"></a>Elementos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **BmpLayer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[BmpLayer](media-services-mes-schema.md#BmpLayer) | |

## <a name="JpgLayers"></a> JpgLayers
### <a name="elements"></a>Elementos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **JpgLayer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[JpgLayer](media-services-mes-schema.md#JpgLayer) | |

## <a name="BmpImage"></a> BmpImage (o tipo complexo herda do Vídeo)
### <a name="elements"></a>Elementos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs="0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Camadas de Png |

## <a name="JpgImage"></a> JpgImage (o tipo complexo herda do Vídeo)
### <a name="elements"></a>Elementos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs="0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Camadas de Png |

## <a name="PngImage"></a> PngImage (o tipo complexo herda do Vídeo)
### <a name="elements"></a>Elementos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs="0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Camadas de Png |

## <a name="examples"></a>Exemplos
Consulte exemplos de predefinições XML que são criadas com base neste esquema, veja [Predefinições de tarefa para MES (Media Encoder Standard)](media-services-mes-presets-overview.md).

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

