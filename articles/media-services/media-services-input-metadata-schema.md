---
title: esquema de entrada de metadados do Media Services aaaAzure | Microsoft Docs
description: "tópico de saudação fornece uma visão geral do esquema de entrada de metadados de serviços de mídia do Azure."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d72848e2-4b65-4c84-94bc-e2a90a6e7f47
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 9b72c6ff317aa98451ea75548465dc6023b44a55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="input-metadata"></a>Metadados de entrada
Um trabalho de codificação está associado um ativo de entrada (ou ativos) no qual você deseja tooperform algumas tarefas de codificação.  Após a conclusão de uma tarefa, um ativo de saída é produzido.  Olá ativo de saída contém vídeo, áudio, miniaturas manifestos, etc. Olá também contém um arquivo com metadados sobre o ativo de entrada hello. nome do arquivo XML de metadados Olá Olá tem Olá formato a seguir: &lt;asset_id&gt;<asset_id>_metadata.XML (por exemplo, 41114ad3-eb5e - 4c 57 8d 92-5354e2b7d4a4_metadata.xml), onde &lt;asset_id&gt; é hello AssetId valor do ativo de entrada hello.  

Se desejar que o arquivo de metadados de saudação tooexamine, você pode criar um **SAS** localizador e download Olá computador local do arquivo tooyour. Você pode encontrar um exemplo sobre como toocreate um localizador SAS e baixar um arquivo [usando extensões de SDK .NET do serviços de mídia Olá](media-services-dotnet-get-started.md).  

Este tópico discute elementos hello e tipos de esquema XML, Olá em quais metadados de entrada hello (&lt;asset_id&gt;<asset_id>_metadata.xml) é baseado.  Para obter informações sobre o arquivo hello que contém metadados sobre o ativo de saída de hello, consulte [metadados de saída](media-services-output-metadata-schema.md).  

> [!NOTE]
> Você pode encontrar hello [código de esquema](media-services-input-metadata-schema.md#code) um [exemplo XML](media-services-input-metadata-schema.md#xml) final Olá deste tópico.  
> 
> 

## <a name="AssetFiles"></a> Elemento AssetFiles (elemento raiz)
Contém uma coleção de [elemento AssetFile](media-services-input-metadata-schema.md#AssetFile)s para o trabalho de codificação hello.  

Veja um exemplo XML no final deste tópico Olá: [exemplo XML](media-services-input-metadata-schema.md#xml).  

| Nome | Descrição |
| --- | --- |
| **AssetFile**<br /><br /> minOccurs="1" maxOccurs="unbounded" |Um único elemento filho. Para saber mais, veja [Elemento AssetFile](media-services-input-metadata-schema.md#AssetFile). |

## <a name="AssetFile"></a> Elemento AssetFile
 Contém atributos e elementos que descrevem um arquivo de ativo.  

 Veja um exemplo XML no final deste tópico Olá: [exemplo XML](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Nome**<br /><br /> Obrigatório |**xs:string** |Nome do arquivo de ativo. |
| **Tamanho**<br /><br /> Obrigatório |**xs:long** |Tamanho do arquivo de ativo de saudação em bytes. |
| **Duração**<br /><br /> Obrigatório |**xs:duration** |Duração da reprodução de conteúdo. Exemplo: Duration="PT25M37.757S". |
| **NumberOfStreams**<br /><br /> Obrigatório |**xs:int** |Número de fluxos no arquivo de ativo de saudação. |
| **FormatNames**<br /><br /> Obrigatório |**xs:string** |Nomes de formato. |
| **FormatVerboseNames**<br /><br /> Obrigatório |**xs:string** |Nomes detalhados de formato. |
| **StartTime** |**xs:duration** |Hora de início do conteúdo. Exemplo: StartTime = "PT2.669S". |
| **OverallBitRate** |**xs:int** |Taxa de bits média do arquivo de ativo de saudação em kbps. |

> [!NOTE]
> Olá 4 elementos filhos a seguir deve aparecer em uma sequência.  
> 
> 

### <a name="child-elements"></a>Elementos filho
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Programas**<br /><br /> minOccurs="0" | |Coleção de todos os [elemento programas](media-services-input-metadata-schema.md#Programs) quando o arquivo de ativo hello está em formato MPEG-TS. |
| **VideoTracks**<br /><br /> minOccurs="0" | |Cada arquivo de ativo físico pode conter nenhuma ou mais faixas de vídeo intercaladas em um formato de contêiner apropriado. Esse elemento contém uma coleção de todos os [elemento VideoTracks](media-services-input-metadata-schema.md#VideoTracks) que fazem parte do arquivo de ativo de saudação. |
| **AudioTracks**<br /><br /> minOccurs="0" | |Cada arquivo de ativo físico pode conter nenhuma ou mais faixas de áudio intercaladas em um formato de contêiner apropriado. Esse elemento contém uma coleção de todos os [elemento AudioTracks](media-services-input-metadata-schema.md#AudioTracks) que fazem parte do arquivo de ativo de saudação. |
| **Metadados**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[MetadataType](media-services-input-metadata-schema.md#MetadataType) |Metadados do arquivo de ativo representados como cadeias de caracteres de chave\valor. Por exemplo:<br /><br /> **&lt;Metadata key="language" value="eng" /&gt;** |

## <a name="TrackType"></a> TrackType
Veja um exemplo XML no final deste tópico Olá: [exemplo XML](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Id**<br /><br /> Obrigatório |**xs:int** |Índice baseado em zero da faixa de áudio ou de vídeo.<br /><br /> Isso não é necessariamente que Olá TrackID como utilizado em um arquivo MP4. |
| **Codec** |**xs:string** |Cadeia de caracteres de codec de faixa de vídeo. |
| **CodecLongName** |**xs:string** |Nome longo de codec de faixa de áudio ou vídeo. |
| **TimeBase**<br /><br /> Obrigatório |**xs:string** |Base de tempo. Exemplo: TimeBase="1/48000" |
| **NumberOfFrames** |**xs:int** |Número de quadros (presentes em faixas de vídeo). |
| **StartTime** |**xs:duration** |Hora de início da faixa. Exemplo: StartTime="PT2.669S" |
| **Duração** |**xs:duration** |Duração da faixa. Exemplo: Duration="PTSampleFormat M37.757S". |

> [!NOTE]
> Olá 2 elementos filho a seguir deve aparecer em uma sequência.  
> 
> 

### <a name="child-elements"></a>Elementos filho
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Disposição**<br /><br /> minOccurs="0" maxOccurs="1" |[StreamDispositionType](media-services-input-metadata-schema.md#StreamDispositionType) |Contém informações de apresentação (por exemplo, se uma determinada faixa de áudio for para usuários com deficiência visual). |
| **Metadados**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[MetadataType](media-services-input-metadata-schema.md#MetadataType) |Cadeias de caracteres de chave/valor genérico que podem ser usado toohold uma variedade de informações. Por exemplo, key=”language” e value=”eng”. |

## <a name="AudioTrackType"></a> AudioTrackType (herda de TrackType)
 **AudioTrackType** é um tipo complexo global que herda de [TrackType](media-services-input-metadata-schema.md#TrackType).  

 tipo de saudação representa uma faixa de áudio específica no arquivo de ativo de saudação.  

 Veja um exemplo XML no final deste tópico Olá: [exemplo XML](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **SampleFormat** |**xs:string** |Formato de exemplo. |
| **ChannelLayout** |**xs:string** |Layout do canal. |
| **Canais**<br /><br /> Obrigatório |**xs:int** |Número (0 ou mais) de canais de áudio. |
| **SamplingRate**<br /><br /> Obrigatório |**xs:int** |Taxa de amostragem de áudio em amostras/s ou Hz. |
| **Bitrate** |**xs:int** |Taxa média de bits de áudio em bits por segundo, calculada a partir do arquivo de ativo de saudação. Somente Olá corrente de carga elementar é contada e sobrecarga de embalagem Olá não está incluída nesta contagem. |
| **BitsPerSample** |**xs:int** |Bits por amostra para o formato wFormatTag Olá tipo. |

## <a name="VideoTrackType"></a> VideoTrackType (herda de TrackType)
**VideoTrackType** é um tipo complexo global que herda de [TrackType](media-services-input-metadata-schema.md#TrackType).  

tipo de saudação representa uma faixa de vídeo específica no arquivo de ativo de saudação.  

Veja um exemplo XML no final deste tópico Olá: [exemplo XML](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **FourCC**<br /><br /> Obrigatório |**xs:string** |Código FourCC de codec de vídeo. |
| **Perfil** |**xs:string** |Perfil da faixa de vídeo. |
| **Nível** |**xs:string** |Nível da faixa de vídeo. |
| **PixelFormat** |**xs:string** |Formato de pixel da faixa de vídeo. |
| **Largura**<br /><br /> Obrigatório |**xs:int** |Largura do vídeo codificado em pixels. |
| **Altura**<br /><br /> Obrigatório |**xs:int** |Altura do vídeo codificado em pixels. |
| **DisplayAspectRatioNumerator**<br /><br /> Obrigatório |**xs:double** |Numerador de taxa de proporção de exibição do vídeo. |
| **DisplayAspectRatioDenominator**<br /><br /> Obrigatório |**xs:double** |Denominador de taxa de proporção de exibição do vídeo. |
| **DisplayAspectRatioDenominator**<br /><br /> Obrigatório |**xs:double** |Numerador de proporção de amostra de vídeo. |
| **SampleAspectRatioNumerator** |**xs:double** |Numerador de proporção de amostra de vídeo. |
| **SampleAspectRatioNumerator** |**xs:double** |Denominador de proporção de amostra de vídeo. |
| **FrameRate**<br /><br /> Obrigatório |**xs:decimal** |Medida de taxa de quadros de vídeo em formato .3f. |
| **Bitrate** |**xs:int** |Taxa média de bits de vídeo em quilobits por segundo, calculada a partir do arquivo de ativo de saudação. Somente Olá corrente de carga elementar é contada e não há sobrecarga de embalagem hello. |
| **MaxGOPBitrate** |**xs:int** |Taxa de bits média do GOP máximo para esta faixa de vídeo em quilobits por segundo. |
| **HasBFrames** |**xs:int** |Número de faixas de vídeo de quadros B. |

## <a name="MetadataType"></a> MetadataType
**MetadataType** é um tipo global complexo que descreve os metadados de um arquivo de ativo como cadeias de caracteres de chave/valor. Por exemplo, key=”language” e value=”eng”.  

Veja um exemplo XML no final deste tópico Olá: [exemplo XML](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **chave**<br /><br /> Obrigatório |**xs:string** |chave de saudação no par chave/valor de saudação. |
| **valor**<br /><br /> Obrigatório |**xs:string** |valor de saudação no par chave/valor de saudação. |

## <a name="ProgramType"></a> ProgramType
**ProgramType** é um tipo global complexo que descreve um programa.  

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **ProgramId**<br /><br /> Obrigatório |**xs:int** |Id do Programa |
| **NumberOfPrograms**<br /><br /> Obrigatório |**xs:int** |Número de programas. |
| **PmtPid**<br /><br /> Obrigatório |**xs:int** |As PMTs (Tabelas de Mapa de Programa) contêm informações sobre programas.  Para saber mais, confira [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT). |
| **PcrPid**<br /><br /> Obrigatório |**xs:int** |Usado pelo decodificador. Para saber mais, confira [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR) |
| **StartPTS** |**xs: long** |Iniciando o carimbo de data/hora de apresentação. |
| **EndPTS** |**xs: long** |Hora de término do carimbo de data/hora de apresentação. |

## <a name="StreamDispositionType"></a> StreamDispositionType
**StreamDispositionType** é um tipo de complexo global que descreve o fluxo de saudação.  

Veja um exemplo XML no final deste tópico Olá: [exemplo XML](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Padrão**<br /><br /> Obrigatório |**xs:int** |Defina tooindicate de too1 este atributo trata de apresentação de padrão de saudação. |
| **Dub**<br /><br /> Obrigatório |**xs:int** |Defina tooindicate de too1 esse atributo é Olá apelidado de apresentação. |
| **Original**<br /><br /> Obrigatório |**xs:int** |Defina tooindicate de too1 este atributo trata apresentação original hello. |
| **Comentário**<br /><br /> Obrigatório |**xs:int** |Defina este tooindicate too1 de atributo faixa contém comentários. |
| **Lyrics**<br /><br /> Obrigatório |**xs:int** |Defina este tooindicate too1 de atributo faixa contém letras. |
| **Karaoke**<br /><br /> Obrigatório |**xs:int** |Defina este tooindicate too1 de atributo representa Olá faixa Karaoke (música de fundo, sem vocais). |
| **Forced**<br /><br /> Obrigatório |**xs:int** |Defina tooindicate de too1 este atributo trata apresentação Olá forçado. |
| **HearingImpaired**<br /><br /> Obrigatório |**xs:int** |Defina este tooindicate too1 de atributo que esta faixa é para deficiência auditiva de saudação. |
| **VisualImpaired**<br /><br /> Obrigatório |**xs:int** |Defina este tooindicate too1 de atributo que esta faixa é para Olá pessoas com deficiências visuais. |
| **CleanEffects**<br /><br /> Obrigatório |**xs:int** |Defina este tooindicate too1 de atributo que esta faixa tem efeitos limpos. |
| **AttachedPic**<br /><br /> Obrigatório |**xs:int** |Defina este tooindicate too1 de atributo que esta faixa contém imagens. |

## <a name="Programs"></a> Elemento Programs
Elemento de wrapper que contém vários elementos **Program**.  

### <a name="child-elements"></a>Elementos filho
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Programa**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[ProgramType](media-services-input-metadata-schema.md#ProgramType) |Para arquivos de ativos que estão no formato MPEG-TS, contém informações sobre programas no arquivo de ativo de saudação. |

## <a name="VideoTracks"></a> Elemento VideoTracks
 Elemento de wrapper que contém vários elementos **VideoTrack**.  

 Veja um exemplo XML no final deste tópico Olá: [exemplo XML](media-services-input-metadata-schema.md#xml).  

### <a name="child-elements"></a>Elementos filho
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **VideoTrack**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[VideoTrackType (herdado de TrackType)](media-services-input-metadata-schema.md#VideoTrackType) |Contém informações sobre as faixas de vídeos no arquivo de ativo de saudação. |

## <a name="AudioTracks"></a> Elemento AudioTracks
 Elemento de wrapper que contém vários elementos **AudioTrack**.  

 Veja um exemplo XML no final deste tópico Olá: [exemplo XML](media-services-input-metadata-schema.md#xml).  

### <a name="elements"></a>elementos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **AudioTrack**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[AudioTrackType (herdado de TrackType)](media-services-input-metadata-schema.md#AudioTrackType) |Contém informações sobre as faixas de áudio no arquivo de ativo de saudação. |

## <a name="code"></a> Código de Esquema
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.0"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               elementFormDefault="qualified">  

      <xs:complexType name="MetadataType">  
        <xs:attribute name="key"   type="xs:string" use="required"/>  
        <xs:attribute name="value" type="xs:string" use="required"/>  
      </xs:complexType>  

      <xs:complexType name="ProgramType">  
        <xs:attribute name="ProgramId" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Program Id</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfPrograms" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Number of programs</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PmtPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pmt pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PcrPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pcr pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="StartPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>start pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="EndPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>end pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="StreamDispositionType">  
        <xs:attribute name="Default"          type="xs:int" use="required" />  
        <xs:attribute name="Dub"              type="xs:int" use="required" />  
        <xs:attribute name="Original"         type="xs:int" use="required" />  
        <xs:attribute name="Comment"          type="xs:int" use="required" />  
        <xs:attribute name="Lyrics"           type="xs:int" use="required" />  
        <xs:attribute name="Karaoke"          type="xs:int" use="required" />  
        <xs:attribute name="Forced"           type="xs:int" use="required" />  
        <xs:attribute name="HearingImpaired"  type="xs:int" use="required" />  
        <xs:attribute name="VisualImpaired"   type="xs:int" use="required" />  
        <xs:attribute name="CleanEffects"     type="xs:int" use="required" />  
        <xs:attribute name="AttachedPic"      type="xs:int" use="required" />  
      </xs:complexType>  

      <xs:complexType name="TrackType" abstract="true">  
        <xs:sequence>  
          <xs:element name="Disposition" type="StreamDispositionType" minOccurs="0" maxOccurs="1"/>  
          <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded"/>  
        </xs:sequence>  
        <xs:attribute name="Id" use="required">  
          <xs:annotation>  
            <xs:documentation>zero-based index of this video track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="Codec" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec string</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="CodecLongName" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec long name</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="TimeBase"  type="xs:string" use="required">  
          <xs:annotation>  
            <xs:documentation>Time base. Example: TimeBase="1/48000"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfFrames">  
          <xs:annotation>  
            <xs:documentation>number of frames</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="StartTime" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track start time. Example: StartTime="PT2.669S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="Duration" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track duration. Example: Duration="PT25M37.757S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="VideoTrackType">  
        <xs:annotation>  
          <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="FourCC" type="xs:string" use="required">  
              <xs:annotation>  
                <xs:documentation>video codec FourCC code</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Profile" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>profile</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Level" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>level</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="PixelFormat" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>Video track's pixel format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Width" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video width in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Height" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video height in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioNumerator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioDenominator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioNumerator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioDenominator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="FrameRate" use="required">  
              <xs:annotation>  
                <xs:documentation>measured video frame rate in .3f format</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:decimal">  
                  <xs:minInclusive value="0"/>  
                  <xs:fractionDigits value="3"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="MaxGOPBitrate">  
              <xs:annotation>  
                <xs:documentation>Max GOP average bitrate for this video track, in kilobits per second</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="HasBFrames" type="xs:int">  
              <xs:annotation>  
                <xs:documentation>video track number of B frames</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:complexType name="AudioTrackType">  
        <xs:annotation>  
          <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="SampleFormat"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>sample format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="ChannelLayout"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>channel layout</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Channels" use="required">  
              <xs:annotation>  
                <xs:documentation>number of audio channels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SamplingRate" use="required">  
              <xs:annotation>  
                <xs:documentation>audio sampling rate in samples/sec or Hz</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for hello encoding job</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="AssetFile" minOccurs="1" maxOccurs="unbounded">  
              <xs:annotation>  
                <xs:documentation>asset file</xs:documentation>  
              </xs:annotation>  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="Programs" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>This is hello collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" type="AudioTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded" />  
                </xs:sequence>  
                <xs:attribute name="Name" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>hello media asset file name</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Size" use="required">  
                  <xs:annotation>  
                    <xs:documentation>size of file in bytes</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:long">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
                <xs:attribute name="Duration" type="xs:duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration. Example: Duration="PT25M37.757S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="NumberOfStreams" type="xs:int" use="required">  
                  <xs:annotation>  
                    <xs:documentation>number of streams in asset file</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatNames" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatVerboseName" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format verbose names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="StartTime" type="xs:duration">  
                  <xs:annotation>  
                    <xs:documentation>content start time. Example: StartTime="PT2.669S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="OverallBitRate">  
                  <xs:annotation>  
                    <xs:documentation>average bitrate of hello asset file in kbps</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:int">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  


## <a name="xml"></a> Exemplo de XML
a seguir Olá é um exemplo de arquivo de metadados de entrada hello.  

    <?xml version="1.0" encoding="utf-8"?>  
    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata">  
      <AssetFile Name="bear.mp4" Size="1973733" Duration="PT12.678S" NumberOfStreams="2" FormatNames="mov,mp4,m4a,3gp,3g2,mj2" FormatVerboseName="QuickTime / MOV" StartTime="PT0S" OverallBitRate="1245">  
        <VideoTracks>  
          <VideoTrack Id="1" Codec="h264" CodecLongName="H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10" TimeBase="1/29970" NumberOfFrames="375" StartTime="PT0.034S" Duration="PT12.645S" FourCC="avc1" Profile="High" Level="4.1" PixelFormat="yuv420p" Width="512" Height="384" DisplayAspectRatioNumerator="4" DisplayAspectRatioDenominator="3" SampleAspectRatioNumerator="1" SampleAspectRatioDenominator="1" FrameRate="29.656" Bitrate="1043" HasBFrames="1">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Video Media Handler" />  
          </VideoTrack>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="aac" CodecLongName="AAC (Advanced Audio Coding)" TimeBase="1/44100" NumberOfFrames="546" StartTime="PT0S" Duration="PT12.678S" SampleFormat="fltp" ChannelLayout="stereo" Channels="2" SamplingRate="44100" Bitrate="156" BitsPerSample="0">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Sound Media Handler" />  
          </AudioTrack>  
        </AudioTracks>  
        <Metadata key="major_brand" value="mp42" />  
        <Metadata key="minor_version" value="0" />  
        <Metadata key="compatible_brands" value="mp42mp41" />  
        <Metadata key="creation_time" value="2010-03-10 16:11:53" />  
        <Metadata key="comment" value="Courtesy of National Geographic.  Used by Permission." />  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

