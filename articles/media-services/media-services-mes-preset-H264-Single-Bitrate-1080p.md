---
title: "taxa de bits aaaH264 única 1080p predefinição padrão de codificador de mídia - Azure | Microsoft Docs"
description: "tópico de saudação fornece uma visão geral de saudação * * H264 taxas de bits única 1080 p * * predefinição de tarefa."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0951fea8-15af-420b-9648-8c5c1abf8173
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: e06c68e3372c7f1e5903413840c118e2c3426168
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="h264-single-bitrate-1080p"></a>H264 Taxa de Bits Única 1080p
`Media Encoder Standard` define um conjunto de predefinições de codificação que pode ser usado ao criar trabalhos de codificação. Você pode usar um `preset name` toospecify em qual formato você deseja que tooencode seu arquivo de mídia. Ou, pode criar suas próprias predefinições com base em JSON ou XML (usando a codificação UTF-8 ou UTF-16). Em seguida, transmita codificador do hello toohello predefinição personalizada. Para obter lista de saudação de saudação todos os predefinição nomes compatíveis com esta `Media Encoder Standard` codificador, consulte [predefinições de tarefa para o codificador de mídia padrão](media-services-mes-presets-overview.md).  
  
 Este tópico mostra Olá `H264 Single Bitrate 1080p` predefinido no formato XML e JSON.  
  
 Essa predefinição produz um único arquivo MP4 com uma taxa de bits de 6750 kbps e áudio AAC estéreo. Para obter informações detalhadas sobre o perfil, taxa de bits, taxa de amostragem etc. Isso predefinido, examine Olá XML ou JSON definido abaixo. Para obter explicações de que cada elemento nessas significa predefinições, e os valores válidos Olá para cada elemento, consulte Olá [esquema padrão do Media Encoder](media-services-mes-schema.md) tópico.  
  
 XML  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>6750</Bitrate>  
          <Width>1920</Width>  
          <Height>1080</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>6750</MaxBitrate>  
        </H264Layer>  
      </H264Layers>  
      <Chapters />  
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
```  
  
 JSON  
  
```  
{  
  "Version": 1.0,  
  "Codecs": [  
    {  
      "KeyFrameInterval": "00:00:02",  
      "SceneChangeDetection": true,  
      "H264Layers": [  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 6750,  
          "MaxBitrate": 6750,  
          "BufferWindow": "00:00:05",  
          "Width": 1920,  
          "Height": 1080,  
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
```
