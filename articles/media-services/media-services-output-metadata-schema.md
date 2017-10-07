---
title: "esquema de metadados de saída de serviços de mídia aaaAzure | Microsoft Docs"
description: "tópico de saudação fornece uma visão geral do esquema de metadados de saída de serviços de mídia do Azure."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 1ed84c88-eea5-4a24-9c4f-f2428157d08a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 7f07d6accbe0b171d0408b15d5e1e6b5afd6c367
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="output-metadata"></a>Metadados de saída
## <a name="overview"></a>Visão geral
Um trabalho de codificação está associado um ativo de entrada (ou ativos) no qual você deseja tooperform algumas tarefas de codificação. Por exemplo, codificar uma MP4 arquivo tooH.264 MP4 taxa de bits adaptável define; criar uma miniatura. Crie sobreposições. Após a conclusão de uma tarefa, um ativo de saída é produzido.  Olá ativo de saída contém vídeo, áudio, miniaturas, etc. Olá também contém um arquivo com metadados sobre o ativo de saída hello. nome do arquivo XML de metadados Olá Olá tem Olá formato a seguir: &lt;source_file_name>_manifest.XML&gt;<nome_do_arquivo_de_origem>_manifest.XML (por exemplo, BigBuckBunny_manifest.xml).  

Se desejar que o arquivo de metadados de saudação tooexamine, você pode criar um **SAS** localizador e download Olá computador local do arquivo tooyour.  

Este tópico discute elementos hello e tipos de esquema XML, Olá em quais metadados de saída hello (&lt;source_file_name>_manifest.XML&gt;<nome_do_arquivo_de_origem>_manifest.xml) é baseado. Para obter informações sobre o arquivo hello que contém metadados sobre o ativo de entrada hello, consulte [metadados de entrada](media-services-input-metadata-schema.md).  

> [!NOTE]
> Você pode encontrar o código de esquema completo hello e exemplo XML no final deste tópico hello.  
>
>

## <a name="AssetFiles "></a> Elemento raiz AssetFiles
Coleção de entradas AssetFile para o trabalho de codificação hello.  

### <a name="child-elements"></a>Elementos filho
| Nome | Descrição |
| --- | --- |
| **AssetFile**<br/><br/> minOccurs="0" maxOccurs="1" |Um [elemento AssetFile](media-services-output-metadata-schema.md) que faz parte da coleção de AssetFiles de saudação. |

## <a name="AssetFile "></a> Elemento AssetFile
Você pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).  

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Nome**<br/><br/> Obrigatório |**xs:string** |nome do arquivo de ativo de mídia de saudação. |
| **Tamanho**<br/><br/> minInclusive ="0"<br/><br/> Obrigatório |**xs:long** |Tamanho do arquivo de ativo de saudação em bytes. |
| **Duração**<br/><br/> Obrigatório |**xs:duration** |Duração de reprodução de conteúdo. |

### <a name="child-elements"></a>Elementos filho
| Nome | Descrição |
| --- | --- |
| **Fontes** |Coleção de arquivos de mídia de entrada/origem, que foi processada em ordem tooproduce esse AssetFile. Para obter mais informações, veja [Elemento Origem](media-services-output-metadata-schema.md). |
| **VideoTracks**<br/><br/> minOccurs="0" maxOccurs="1" |Cada AssetFile físico pode conter zero ou mais faixas de vídeo intercaladas em um formato de contêiner apropriado. Esta é a coleção de saudação de todas essas faixas de vídeos. Para obter mais informações, veja [Elemento VideoTracks](media-services-output-metadata-schema.md). |
| **AudioTracks**<br/><br/> minOccurs="0" maxOccurs="1" |Cada AssetFile físico pode conter zero ou mais faixas de áudio intercaladas em um formato de contêiner apropriado. Esta é a coleção de saudação de todas essas faixas de áudio. Para obter mais informações, veja [Elemento AudioTracks](media-services-output-metadata-schema.md). |

## <a name="Sources "></a> Elemento Origens
Coleção de arquivos de mídia de entrada/origem, que foi processada em ordem tooproduce esse AssetFile.  

Você pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).  

### <a name="child-elements"></a>Elementos filho
| Nome | Descrição |
| --- | --- |
| **Fonte**<br/><br/> minOccurs="1" maxOccurs="unbounded" |Um arquivo de entrada/origem usado ao gerar esse ativo. Para obter mais informações, veja [Elemento Origem](media-services-output-metadata-schema.md). |

## <a name="Source "></a> Elemento Origem
Um arquivo de entrada/origem usado ao gerar esse ativo.  

Você pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).  

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Nome**<br/><br/> Obrigatório |**xs:string** |Nome do arquivo de fonte de entrada. |

## <a name="VideoTracks "></a> Elemento VideoTracks
Cada AssetFile físico pode conter zero ou mais faixas de vídeo intercaladas em um formato de contêiner apropriado. Esta é a coleção de saudação de todas essas faixas de vídeos.  

Você pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).  

### <a name="child-elements"></a>Elementos filho
| Nome | Descrição |
| --- | --- |
| **VideoTrack**<br/><br/> minOccurs="1" maxOccurs="unbounded" |Uma faixa de vídeo específica no AssetFile pai de saudação. Para obter mais informações, veja [Elemento VideoTrack](media-services-output-metadata-schema.md#VideoTrack). |

## <a name="VideoTrack"></a> Elemento VideoTrack
Uma faixa de vídeo específica no AssetFile pai de saudação.  

Você pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).  

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Id**<br/><br/> minInclusive ="0"<br/><br/> Obrigatório |**xs:int** |Índice baseado em zero dessa faixa de vídeo. **Observação:** não é necessariamente Olá TrackID como utilizado em um arquivo MP4. |
| **FourCC**<br/><br/> Obrigatório |**xs:string** |Código FourCC de codec de vídeo. |
| **Perfil** |**xs:string** |Perfil H264 (somente aplicável tooH264 codec). |
| **Level** |**xs:string** |Nível H264 (somente aplicável tooH264 codec). |
| **Width**<br/><br/> minInclusive ="0"<br/><br/> Obrigatório |**xs:int** |Largura do vídeo codificado em pixels. |
| **Height**<br/><br/> minInclusive ="0"<br/><br/> Obrigatório |**xs:int** |Altura do vídeo codificado em pixels. |
| **DisplayAspectRatioNumerator**<br/><br/> minInclusive ="0"<br/><br/> Obrigatório |**xs:double** |Numerador de taxa de proporção de exibição do vídeo. |
| **DisplayAspectRatioDenominator**<br/><br/> minInclusive ="0"<br/><br/> Obrigatório |**xs:double** |Denominador de taxa de proporção de exibição do vídeo. |
| **Framerate**<br/><br/> minInclusive ="0"<br/><br/> Obrigatório |**xs:decimal** |Medida de taxa de quadros de vídeo em formato .3f. |
| **TargetFramerate**<br/><br/> minInclusive ="0"<br/><br/> Obrigatório |**xs:decimal** |Taxa de quadros de vídeo de destino predefinida em formato .3f. |
| **Bitrate**<br/><br/> minInclusive ="0"<br/><br/> Obrigatório |**xs:int** |Taxa média de bits de vídeo em quilobits por segundo, calculada a partir Olá AssetFile. Contagens somente Olá corrente de carga elementar e não inclui a sobrecarga de embalagem hello. |
| **TargetBitrate**<br/><br/> minInclusive ="0"<br/><br/> Obrigatório |**xs:int** |Taxa de bits média para esta faixa de vídeo de destino conforme solicitado através da predefinição de codificação hello, em quilobits por segundo. |
| **MaxGOPBitrate**<br/><br/> minInclusive ="0" |**xs:int** |Taxa de bits média do GOP máximo para esta faixa de vídeo em quilobits por segundo. |

## <a name="AudioTracks "></a> Elemento AudioTracks
Cada AssetFile físico pode conter zero ou mais faixas de áudio intercaladas em um formato de contêiner apropriado. Esta é a coleção de saudação de todas essas faixas de áudio.  

Você pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).  

### <a name="child-elements"></a>Elementos filho
| Nome | Descrição |
| --- | --- |
| **AudioTrack**<br/><br/> minOccurs="1" maxOccurs="unbounded" |Uma faixa de áudio específica no AssetFile pai de saudação. Para obter mais informações, veja [Elemento AudioTrack](media-services-output-metadata-schema.md). |

## <a name="AudioTrack "></a> Elemento AudioTrack
Uma faixa de áudio específica no AssetFile pai de saudação.  

Você pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).  

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Id**<br/><br/> minInclusive ="0"<br/><br/> Obrigatório |**xs:int** |Índice baseado em zero dessa faixa de áudio. **Observação:** não é necessariamente Olá TrackID como utilizado em um arquivo MP4. |
| **Codec** |**xs:string** |Cadeia de caracteres de codec de faixa de áudio. |
| **EncoderVersion** |**xs:string** |Cadeia de caracteres da versão de codificador opcional, exigida para EAC3. |
| **Channels**<br/><br/> minInclusive ="0"<br/><br/> Obrigatório |**xs:int** |Número de canais de áudio. |
| **SamplingRate**<br/><br/> minInclusive ="0"<br/><br/> Obrigatório |**xs:int** |Taxa de amostragem de áudio em amostras/s ou Hz. |
| **Bitrate**<br/><br/> minInclusive ="0"<br/><br/> Obrigatório |**xs:int** |Taxa média de bits de áudio em bits por segundo, calculada a partir Olá AssetFile. Contagens somente Olá corrente de carga elementar e não inclui a sobrecarga de embalagem hello. |
| **BitsPerSample**<br/><br/> minInclusive ="0"<br/><br/> Obrigatório |**xs:int** |Bits por amostra para o formato wFormatTag Olá tipo. |

### <a name="child-elements"></a>Elementos filho
| Nome | Descrição |
| --- | --- |
| **LoudnessMeteringResultParameters**<br/><br/> minOccurs="0" maxOccurs="1" |Parâmetros de resultado de medição de intensidade. Para obter mais informações, veja [Elemento LoudnessMeteringResultParameters](media-services-output-metadata-schema.md). |

## <a name="LoudnessMeteringResultParameters "></a> Elemento LoudnessMeteringResultParameters
Parâmetros de resultado de medição de intensidade.  

Você pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).  

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **DPLMVersionInformation** |**xs:string** |Versão do kit de desenvolvimento de medição de intensidade profissional **Dolby**. |
| **DialogNormalization**<br/><br/> minInclusive="-31" maxInclusive="-1"<br/><br/> Obrigatório |**xs:int** |DialogNormalization gerado através de DPLM, necessário quando LoudnessMetering é definido |
| **IntegratedLoudness**<br/><br/> minInclusive="-70" maxInclusive="10"<br/><br/> Obrigatório |**xs:float** |Intensidade integrada |
| **IntegratedLoudnessUnit**<br/><br/> Obrigatório |**xs:string** |Unidade de intensidade integrada. |
| **IntegratedLoudnessGatingMethod**<br/><br/> Obrigatório |**xs:string** |Identificador de controle |
| **IntegratedLoudnessSpeechPercentage**<br/><br/> minInclusive ="0" maxInclusive="100" |**xs:float** |Conteúdo de fala sobre programa hello, como uma porcentagem. |
| **SamplePeak**<br/><br/> Obrigatório |**xs:float** |Valor de pico absoluto de amostra, desde a redefinição ou desde a última limpeza, por canal.  As unidades são dBFS. |
| **SamplePeakUnit**<br/><br/> fixed="dBFS"<br/><br/> Obrigatório |**xs:anySimpleType** |Unidade de pico de amostra. |
| **TruePeak**<br/><br/> Obrigatório |**xs:float** |Valor do pico real máximo, de acordo com ITU-R BS.1770-2, desde a redefinição ou desde a última limpeza, por canal. As unidades são dBTP. |
| **TruePeakUnit**<br/><br/> fixed="dBTP"<br/><br/> Obrigatório |**xs:anySimpleType** |Unidade de pico real. |

## <a name="schema-code"></a>Código de Esquema
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.2"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               elementFormDefault="qualified">  
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
                  <xs:element name="Sources">  
                    <xs:annotation>  
                      <xs:documentation>Collection of input/source media files, that was processed in order tooproduce this AssetFile</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Source" minOccurs="1" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>An input/source file used when generating this asset</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:attribute name="Name" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>input source file name</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
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
                            <xs:attribute name="FourCC" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>video codec FourCC code</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Profile" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 profile (only appliable for H264 codec)</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Level" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 level (only appliable for H264 codec)</xs:documentation>  
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
                            <xs:attribute name="Framerate" use="required">  
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
                            <xs:attribute name="TargetFramerate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>preset target video frame rate in .3f format</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:decimal">  
                                  <xs:minInclusive value="0"/>  
                                  <xs:fractionDigits value="3"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="TargetBitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>target average bitrate for this video track, as requested via hello encoding preset, in kilobits per second</xs:documentation>  
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
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:sequence>  
                              <xs:element name="LoudnessMeteringResultParameters" minOccurs="0" maxOccurs="1">  
                                <xs:annotation>  
                                  <xs:documentation>Loudness Metering Result Parameters</xs:documentation>  
                                </xs:annotation>  
                                <xs:complexType>  
                                  <xs:attribute name="DPLMVersionInformation" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Dolby Professional Loudness Metering Development Kit Version</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="DialogNormalization" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation> DialogNormalization generated through DPLM, required when LoudnessMetering is set</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:int">  
                                        <xs:minInclusive value="-31"/>  
                                        <xs:maxInclusive value="-1"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudness" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation>Integrated loudness</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="-70"/>  
                                        <xs:maxInclusive value="10"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessUnit" use="required" type="xs:string">  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessGatingMethod" use="required" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Gating identifier</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessSpeechPercentage">  
                                    <xs:annotation>  
                                      <xs:documentation>Speech content over hello program, as a percentage.</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="0"/>  
                                        <xs:maxInclusive value="100"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Peak absolute sample value, since reset or since it was last cleared, per channel.  Units are dBFS.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeakUnit" use="required" fixed="dBFS">  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Maximum True Peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.  Units are dBTP.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeakUnit" use="required" fixed="dBTP">  
                                  </xs:attribute>  
                                </xs:complexType>  
                              </xs:element>  
                            </xs:sequence>  
                            <xs:attribute name="Id" use="required">  
                              <xs:annotation>  
                                <xs:documentation>zero-based index of this audio track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Codec" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>audio track codec string</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="EncoderVersion" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>optional encoder version string, required for EAC3</xs:documentation>  
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
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="BitsPerSample" use="required">  
                              <xs:annotation>  
                                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
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
                <xs:attribute name="Duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:duration"/>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  



## <a name="xml"></a> Exemplo de XML
 a seguir Olá é um exemplo hello metadados do arquivo de saída.  

    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
                xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata">  
      <AssetFile Name="BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4" Size="4646283" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.2" Width="1280" Height="720" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="4250" TargetBitrate="3400" MaxGOPBitrate="5514"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4" Size="3166728" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="2846" TargetBitrate="2250" MaxGOPBitrate="3630"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4" Size="2205095" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1932" TargetBitrate="1500" MaxGOPBitrate="2513"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4" Size="1508567" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1271" TargetBitrate="1000" MaxGOPBitrate="1527"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4" Size="1057155" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="843" TargetBitrate="650" MaxGOPBitrate="1086"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4" Size="699262" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="1.3" Width="320" Height="180" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="503" TargetBitrate="400" MaxGOPBitrate="661"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_96kbps.mp4" Size="166780" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_56kbps.mp4" Size="124576" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="53" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
