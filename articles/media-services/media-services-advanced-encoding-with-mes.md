---
title: "aaaPerform avançado personalizando MES predefinições de codificação | Microsoft Docs"
description: "Este tópico mostra como tooperform avançados de codificação Personalizando o codificador de mídia padrão predefinições de tarefa."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 2a4ade25-e600-4bce-a66e-e29cf4a38369
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 9caa68fafacaf51f91f0554c5bafe491928d8c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a>Executar a codificação avançada personalizando predefinições de MES 

## <a name="overview"></a>Visão geral

Este tópico mostra como predefinições de codificador de mídia padrão de toocustomize. Olá [codificação com codificador de mídia padrão usando predefinições personalizadas](media-services-custom-mes-presets-with-dotnet.md) tópico mostra como toouse .NET toocreate uma codificação de tarefas e um trabalho que executa essa tarefa. Quando você personalizar uma predefinição de tarefa de codificação do fornecimento Olá predefinições personalizadas toohello. 

>[!NOTE]
>Se usando uma predefinição XML, certifique-se de ordem de saudação toopreserve dos elementos, conforme mostrado nos exemplos XML abaixo (por exemplo, KeyFrameInterval deve preceder SceneChangeDetection).
>

Neste tópico, predefinições personalizadas de saudação que executam Olá tarefas de codificação a seguir são demonstradas.

## <a name="support-for-relative-sizes"></a>Suporte para tamanhos relativos

Ao gerar miniaturas, não é necessário tooalways especificar saída largura e altura em pixels. Você pode especificá-los em porcentagens, no intervalo de saudação [% 1, …, 100%].

### <a name="json-preset"></a>Predefinição JSON
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a>Predefinição XML
    <Width>100%</Width>
    <Height>100%</Height>

## <a id="thumbnails"></a>Gerar miniaturas

Esta seção mostra como toocustomize uma predefinição que gera miniaturas. Olá predefinição definida abaixo contém informações sobre como você deseja tooencode seu arquivo, bem como miniaturas toogenerate as informações necessárias. Você pode executar qualquer uma das predefinições MES Olá documentadas [isso](media-services-mes-presets-overview.md) seção e adicione o código que gera miniaturas.  

> [!NOTE]
> Olá **SceneChangeDetection** configuração Olá predefinidas a seguir só pode ser definida tootrue se a codificação de vídeo de taxa de bits única tooa. Se você estiver codificando tooa várias taxas de bits vídeo e defina **SceneChangeDetection** tootrue, o codificador Olá retornará um erro.  
>
>

Para obter informações sobre o esquema, consulte [este](media-services-mes-schema.md) tópico.

Verifique se Olá de tooreview [considerações](#considerations) seção.

### <a id="json"></a>Predefinição JSON
    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"

            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": 640,
              "Height": 360,
            }
          ],
          "Start": "00:00:01",
          "Step": "00:00:10",
          "Range": "00:00:58",
          "Type": "PngImage"
        },
        {
          "BmpLayers": [
            {
              "Type": "BmpLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "10%",
          "Step": "10%",
          "Range": "90%",
          "Type": "BmpImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "BmpFormat"
          }
        },
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a id="xml"></a>Predefinição XML
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <SceneChangeDetection>true</SceneChangeDetection>
          <H264Layers>
            <H264Layer>
              <Bitrate>4500</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>4500</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>640</Width>
              <Height>360</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
        <BmpImage Start="10%" Step="10%" Range="90%">
          <BmpLayers>
            <BmpLayer>
              <Width>640</Width>
              <Height>360</Height>
            </BmpLayer>
          </BmpLayers>
        </BmpImage>
        <PngImage Start="00:00:01" Step="00:00:10" Range="00:00:58">
          <PngLayers>
            <PngLayer>
              <Width>640</Width>
              <Height>360</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <BmpFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

### <a name="considerations"></a>Considerações

Olá considerações a seguir se aplicam:

* uso de saudação de carimbos de hora explícitos para etapa/intervalo de início pressupõe que dessa fonte de entrada hello é pelo menos 1 minuto.
* Elementos Jpg/Png/BmpImage têm atributos de cadeia de caracteres de Início, Etapa e Intervalo que podem ser interpretados como:

  * Número de quadro se eles forem números inteiros não negativos, por exemplo, "Início": "120",
  * Duração toosource relativo se expresso como sufixo %, por exemplo "início": "15%", ou
  * Carimbo de data/hora se expresso no formato HH:MM:SS… formato, por exemplo "Start" : "00:01:00"

    Você pode combinar as notações como desejar.

    Além disso, início também suporta uma Macro especial: {melhor}, que tenta toodetermine Olá primeiro "interessante" quadro de conteúdo Olá Observação: (etapa e intervalo são ignorados quando iniciar está definido muito {melhor})
  * Padrões: Start:{Best}
* Formato de saída precisa toobe fornecido explicitamente para cada formato de imagem: Jpg/Png/BmpFormat. Quando presente, MES corresponde JpgVideo tooJpgFormat e assim por diante. OutputFormat apresenta uma nova Macro específico de codec de imagem: {índice}, que precisa toobe presente (uma vez e apenas uma vez) para formatos de saída de imagem.

## <a id="trim_video"></a>Cortar um vídeo (recorte)
Esta seção explica modificando codificador Olá predefinições tooclip ou cortar o vídeo de entrada hello onde Olá entrada é um arquivo de mezanino chamados ou sob demanda. Hello codificador também pode ser usado tooclip ou cortar um ativo, o que é capturado ou arquivado a partir de um fluxo ao vivo – Olá detalhes para este estão disponíveis no [este blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).

tootrim vídeos, você pode executar qualquer uma das predefinições MES Olá documentadas [isso](media-services-mes-presets-overview.md) seção e modificar Olá **fontes** elemento (conforme mostrado abaixo). Olá. o valor de StartTime deve toomatch Olá absoluto carimbos de hora de vídeo de entrada hello. Por exemplo, se hello primeiro quadro de vídeo de entrada hello tem um carimbo de hora de 12:00:10.000, StartTime deve ser pelo menos 12:00:10.000 e maior. O exemplo hello abaixo, presumimos Olá vídeo de entrada tem um carimbo de hora inicial igual a zero. **Fontes** deve ser colocado no início de saudação do hello predefinição.

### <a id="json"></a>Predefinição JSON
    {
      "Version": 1.0,
      "Sources": [
        {
          "StartTime": "00:00:04",
          "Duration": "00:00:16"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1280,
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
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1500,
              "MaxBitrate": 1500,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1000,
              "MaxBitrate": 1000,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 650,
              "MaxBitrate": 650,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 400,
              "MaxBitrate": 400,
              "BufferWindow": "00:00:05",
              "Width": 320,
              "Height": 180,
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

### <a name="xml-preset"></a>Predefinição XML
tootrim vídeos, você pode executar qualquer uma das predefinições MES Olá documentadas [aqui](media-services-mes-presets-overview.md) e modificar Olá **fontes** elemento (conforme mostrado abaixo).

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source StartTime="PT4S" Duration="PT14S"/>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>3400</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>3400</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>2250</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>2250</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1500</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1500</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1000</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1000</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>650</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>650</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>400</Bitrate>
              <Width>320</Width>
              <Height>180</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>400</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>

## <a id="overlay"></a>Criar uma sobreposição

Olá codificador de mídia padrão permite que você toooverlay uma imagem em um vídeo existente. Atualmente, a saudação formatos a seguir têm suporte: png, jpg, gif e bmp. Olá predefinição definida abaixo é um exemplo básico de uma sobreposição de vídeo.

Além disso toodefining um arquivo predefinido, você também tem os serviços de mídia toolet saber qual arquivo de ativo de saudação é Olá sobreposição de imagem e qual arquivo de vídeo de origem Olá no qual você deseja toooverlay imagem de saudação. arquivo de vídeo Olá tem Olá toobe **primário** arquivo.

Se você estiver usando .NET, adicione Olá após duas funções de exemplo do .NET toohello definido em [isso](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) tópico. Olá **UploadMediaFilesFromFolder** função uploads de arquivos de uma pasta (por exemplo, BigBuckBunny.mp4 e Image001.png) e conjuntos de Olá arquivo toobe Olá primário arquivo mp4 no ativo de saudação. Olá **EncodeWithOverlay** função usa Olá arquivo predefinido personalizado que foi passado tooit (por exemplo, Olá predefinição que segue) toocreate Olá tarefa de codificação.


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // hello following code assumes 
            // you have an input folder with one MP4 and one overlay image file.
            if (af.Name.Contains(".mp4"))
                af.IsPrimary = true;
            else
                af.IsPrimary = false;
    
            af.Update();
        }
    
        return asset;
    }

    static public IAsset EncodeWithOverlay(IAsset assetSource, string customPresetFileName)
    {
        // Declare a new job.
        IJob job = _context.Jobs.Create("Media Encoder Standard Job");
        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input assets toobe encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset toocontain hello results of hello job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> Limitações atuais:
>
> Não há suporte para a configuração de opacidade de sobreposição de saudação.
>
> O arquivo de vídeo de origem e o arquivo de imagem de sobreposição de saudação têm toobe em Olá mesmo ativo e Olá conjunto do arquivo de vídeo necessidades toobe como arquivo principal de saudação nesse ativo.
>
>

### <a name="json-preset"></a>Predefinição JSON
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "VideoOverlay": {
              "Position": {
                "X": 100,
                "Y": 100,
                "Width": 100,
                "Height": 50
              },
              "AudioGainLevel": 0.0,
              "MediaParams": [
                {
                  "OverlayLoopCount": 1
                },
                {
                  "IsOverlay": true,
                  "OverlayLoopCount": 1,
                  "InputLoop": true
                }
              ],
              "Source": "Image001.png",
              "Clip": {
                "Duration": "00:00:05"
              },
              "FadeInDuration": {
                "Duration": "00:00:01"
              },
              "FadeOutDuration": {
                "StartTime": "00:00:03",
                "Duration": "00:00:04"
              }
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
              "Bitrate": 1045,
              "MaxBitrate": 1045,
              "BufferWindow": "00:00:05",
              "ReferenceFrames": 3,
              "EntropyMode": "Cavlc",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Type": "CopyAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}{Extension}",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a name="xml-preset"></a>Predefinição XML
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source>
          <Streams />
          <Filters>
            <VideoOverlay>
              <Source>Image001.png</Source>
              <Clip Duration="PT5S" />
              <FadeInDuration Duration="PT1S" />
              <FadeOutDuration StartTime="PT3S" Duration="PT4S" />
              <Position X="100" Y="100" Width="100" Height="50" />
              <Opacity>0</Opacity>
              <AudioGainLevel>0</AudioGainLevel>
              <MediaParams>
                <MediaParam>
                  <IsOverlay>false</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>false</InputLoop>
                </MediaParam>
                <MediaParam>
                  <IsOverlay>true</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>true</InputLoop>
                </MediaParam>
              </MediaParams>
            </VideoOverlay>
          </Filters>
          <Pad>true</Pad>
        </Source>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>1045</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>0</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cavlc</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1045</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <CopyAudio />
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}{Extension}">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>


## <a id="silent_audio"></a>Inserir uma faixa de áudio silenciosa quando a entrada não tiver áudio
Por padrão, se você enviar um codificador de toohello de entrada que contenha apenas vídeo e nenhum áudio, em seguida, Olá ativo de saída contém de arquivos que contêm dados de apenas vídeo. Alguns players podem não ser capazes de toohandle tal fluxos de saída. Você pode usar essa configuração tooforce Olá codificador tooadd uma saída de toohello silenciosa faixa de áudio nesse cenário.

tooforce Olá codificador tooproduce um ativo que contenha uma faixa de áudio silenciosa quando a entrada não tem áudio, especifique o valor de "InsertSilenceIfNoAudio" hello.

Você pode executar qualquer Olá MES predefinições documentadas em [isso](media-services-mes-presets-overview.md) seção e fazer Olá modificações a seguir:

### <a name="json-preset"></a>Predefinição JSON
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a>Predefinição XML
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <a id="deinterlacing"></a>Desabilitar desentrelaçamento automático
Os clientes não precisam toodo nada se eles como Olá entrelaçamento toobe conteúdo automaticamente eliminação entrelaçada. Quando Olá automática de entrelaçamento está na saudação (padrão) MES Olá auto detecção de quadros entrelaçadas e somente eliminação as interfaces quadros marcados como entrelaçada.

Você pode desativar Olá automática de entrelaçamento. No entanto, isso não é recomendado.

### <a name="json-preset"></a>Predefinição JSON
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a>Predefinição XML
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <a id="audio_only"></a>Predefinições somente de áudio
Esta seção demonstra duas predefinições MES somente de áudio: áudio AAC e Áudio de Boa Qualidade AAC.

### <a name="aac-audio"></a>Áudio AAC
    {
      "Version": 1.0,
      "Codecs": [
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
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="aac-good-quality-audio"></a>Áudio de Boa Qualidade AAC
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 192,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <a id="concatenate"></a>Concatenar dois ou mais arquivos de vídeo

Olá exemplo a seguir ilustra como você pode gerar uma predefinição tooconcatenate dois ou mais arquivos de vídeo. cenário mais comum de saudação é quando você deseja tooadd um cabeçalho ou um vídeo principal de toohello do marcador. Olá destinado a uso é quando (resolução de vídeo, taxa de quadros, contagem de faixa de áudio, etc.) de propriedades de compartilhamento de arquivos de vídeo hello está sendo editados juntos. Você deve tomar cuidado para não toomix vídeos de taxas de quadros diferentes ou com números diferentes de faixas de áudio.

>[!NOTE]
>Olá design atual do recurso de concatenação de saudação espera que Olá entrada videoclipes são consistentes em termos de resolução, taxa de quadros etc. 

### <a name="requirements-and-considerations"></a>Requisitos e considerações

* Vídeos de entrada devem ter apenas uma faixa de áudio.
* Vídeos de entrada devem ter Olá mesma taxa de quadros.
* Você deve carregar seus vídeos em ativos separados e definir vídeos hello como arquivo principal de saudação em cada ativo.
* Você precisa de duração de saudação tooknow de vídeos.
* Olá predefinidos exemplos a seguir presume que todos os vídeos de entrada hello começam com um carimbo de hora de zero. Você precisar de toomodify Olá StartTime valores se vídeos Olá tem o carimbo de hora de início diferente, como normalmente Olá caso com arquivos mortos ao vivo.
* Olá predefinição JSON faz referências explícitas toohello AssetID valores de ativos de entrada hello.
* o código de exemplo Hello pressupõe que Olá que JSON predefinição tiver sido salvo como arquivo local tooa, como "C:\supportFiles\preset.json". Ele também pressupõe que foram criados dois ativos Carregando dois arquivos de vídeos e que você sabe Olá AssetID os valores resultantes.
* Olá trecho de código e JSON predefinição mostra um exemplo de concatenação de dois arquivos de vídeos. Você pode estendê-lo toomore que dois vídeos por:

  1. Tarefa de chamada. InputAssets.Add() repetidamente tooadd mais vídeos, na ordem.
  2. Tornar correspondente edita o elemento toohello "fontes" hello JSON, adicionando mais entradas, Olá mesma ordem.

### <a name="net-code"></a>Código do .NET

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass tooit hello name of the
    // processor toouse for hello specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load hello XML (or JSON) from hello local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify hello input videos toobe concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset toocontain hello results of hello job.
    // This output is specified as AssetCreationOptions.None, which
    // means hello output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a>Predefinição JSON

Atualize personalizados predefinidos com ids de ativos de saudação que você deseja tooconcatenate e com o segmento de tempo apropriado Olá para cada vídeo.

    {
      "Version": 1.0,
      "Sources": [
        {
          "AssetID": "606db602-efd7-4436-97b4-c0b867ba195b",
          "StartTime": "00:00:01",
          "Duration": "00:00:15"
        },
        {
          "AssetID": "a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e",
          "StartTime": "00:00:02",
          "Duration": "00:00:05"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": true,
          "H264Layers": [
            {
              "Level": "auto",
              "Bitrate": 1800,
              "MaxBitrate": 1800,
              "BufferWindow": "00:00:05",
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
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

## <a id="crop"></a>Cortar vídeos com o Codificador de Mídia Padrão
Consulte Olá [cortar vídeos com o codificador de mídia padrão](media-services-crop-video.md) tópico.

## <a id="no_video"></a>Inserir uma faixa de vídeo quando a entrada não tiver vídeo

Por padrão, se você enviar um codificador de toohello de entrada que contenha apenas áudio e sem vídeo, em seguida, Olá ativo de saída contém de arquivos que contêm dados somente de áudio. Alguns players, incluindo o Azure Media Player (consulte [isso](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) pode não ser capaz de toohandle tais fluxos. Você pode usar este tooadd de codificador Olá configuração tooforce uma saída de toohello da faixa de vídeo monocromático nesse cenário.

> [!NOTE]
> Forçar Olá codificador tooinsert um tamanho saída faixa de vídeo aumenta Olá Olá ativo de saída e Olá assim o custo incorrido para tarefas de codificação de saudação. Você deve executar testes tooverify que esse aumento resultante tem apenas um impacto modesto sobre os encargos mensais.
>

### <a name="inserting-video-at-only-hello-lowest-bitrate"></a>Inserindo vídeo em apenas hello mais baixa taxa de bits

Suponha que você está usando uma codificação de taxa de bits vários, como predefinição ["H264 taxas de bits múltiplas 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode toda entrada de catálogo para streaming, que contém uma mistura de arquivos de vídeo e arquivos de áudio. Nesse cenário, quando a entrada de saudação não tem vídeo, convém tooforce Olá codificador tooinsert uma monocromática vídeo controlar apenas Olá taxas de bits menores, como tooinserting contrário vídeo em cada taxa de bits de saída. tooachieve isso, você precisa Olá toouse **InsertBlackIfNoVideoBottomLayerOnly** sinalizador.

Você pode executar qualquer Olá MES predefinições documentadas em [isso](media-services-mes-presets-overview.md) seção e fazer Olá modificações a seguir:

#### <a name="json-preset"></a>Predefinição JSON
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a>Predefinição XML

Ao usar o XML, use a condição = "InsertBlackIfNoVideoBottomLayerOnly" como um atributo toohello **H264Video** elemento e a condição = "InsertSilenceIfNoAudio" como um atributo muito**AACAudio**.

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideoBottomLayerOnly">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .
```

### <a name="inserting-video-at-all-output-bitrates"></a>Inserindo vídeo em todas as taxas de bits de saída
Suponha que você está usando uma codificação de taxa de bits vários, como predefinição ["H264 taxas de bits múltiplas 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode toda entrada de catálogo para streaming, que contém uma mistura de arquivos de vídeo e arquivos de áudio. Nesse cenário, quando a entrada de saudação não tem vídeo, convém tooforce Olá codificador tooinsert um vídeo monocromático acompanhar a todas as taxas de bits de saída de hello. Isso garante que a saída ativos são todos homogêneos com respeito toonumber de faixas de vídeo e faixas de áudio. tooachieve isso, é necessário toospecify Olá sinalizador "InsertBlackIfNoVideo".

Você pode executar qualquer Olá MES predefinições documentadas em [isso](media-services-mes-presets-overview.md) seção e fazer Olá modificações a seguir:

#### <a name="json-preset"></a>Predefinição JSON
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a>Predefinição XML

Ao usar o XML, use a condição = "InsertBlackIfNoVideo" como um atributo toohello **H264Video** elemento e a condição = "InsertSilenceIfNoAudio" como um atributo muito**AACAudio**.

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideo">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .  
```

## <a id="rotate_video"></a>Girar um vídeo
Olá [codificador de mídia padrão](media-services-dotnet-encode-with-media-encoder-standard.md) dá suporte a rotação de ângulos de 0/90/180/270. comportamento padrão de saudação é "Auto", onde ele tenta toodetect Olá rotação metadados no arquivo de vídeo entrada hello e compensar a ele. Incluem hello seguinte **fontes** tooone de elemento de predefinições de saudação definido em [isso](media-services-mes-presets-overview.md) seção:

### <a name="json-preset"></a>Predefinição JSON
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...
### <a name="xml-preset"></a>Predefinição XML
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

Além disso, consulte [isso](media-services-mes-schema.md#PreserveResolutionAfterRotation) tópico para obter mais informações sobre como o codificador Olá interpreta configurações de largura e altura de saudação em hello predefinidos, quando a compensação de rotação é disparada.

Você pode usar metadados da rotação do tooignore de codificador da toohello do tooindicate de valor "0" Olá, se presente, vídeo de entrada hello.

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Consulte também
[Visão geral da codificação de serviços de mídia](media-services-encode-asset.md)
