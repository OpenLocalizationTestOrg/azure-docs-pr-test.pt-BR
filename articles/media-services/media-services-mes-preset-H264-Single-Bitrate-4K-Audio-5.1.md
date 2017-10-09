---
title: "aaaH264 taxa de bits única 4K Audio 5.1 | Microsoft Docs"
description: "tópico de saudação fornece uma visão geral de saudação * * taxas de bits H264 única 4K Audio 5.1* * predefinição de tarefa."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 72cb95ac-2cd6-4ef4-9938-8f22cea04920
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 8ed5d85a0c58eaa9b076be667f4499659d90b19e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="h264-single-bitrate-4k-audio-51"></a><span data-ttu-id="5a75b-103">H264 Taxa de Bits Única 4K Audio 5.1</span><span class="sxs-lookup"><span data-stu-id="5a75b-103">H264 Single Bitrate 4K Audio 5.1</span></span>
<span data-ttu-id="5a75b-104">`Media Encoder Standard` define um conjunto de predefinições de codificação que pode ser usado ao criar trabalhos de codificação.</span><span class="sxs-lookup"><span data-stu-id="5a75b-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="5a75b-105">Você pode usar um `preset name` toospecify em qual formato você deseja que tooencode seu arquivo de mídia.</span><span class="sxs-lookup"><span data-stu-id="5a75b-105">You can either use a `preset name` toospecify into which format you would like tooencode your media file.</span></span> <span data-ttu-id="5a75b-106">Ou, pode criar suas próprias predefinições com base em JSON ou XML (usando a codificação UTF-8 ou UTF-16).</span><span class="sxs-lookup"><span data-stu-id="5a75b-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="5a75b-107">Em seguida, transmita codificador do hello toohello predefinição personalizada.</span><span class="sxs-lookup"><span data-stu-id="5a75b-107">You would then pass hello custom preset toohello encoder.</span></span> <span data-ttu-id="5a75b-108">Para obter lista de saudação de saudação todos os predefinição nomes compatíveis com esta `Media Encoder Standard` codificador, consulte [predefinições de tarefa para o codificador de mídia padrão](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5a75b-108">For hello list of all hello preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="5a75b-109">Este tópico mostra Olá `H264 Single Bitrate 4K Audio 5.1` predefinido (em formato XML e JSON).</span><span class="sxs-lookup"><span data-stu-id="5a75b-109">This topic shows hello `H264 Single Bitrate 4K Audio 5.1` preset (in XML and JSON format).</span></span>  
  
 <span data-ttu-id="5a75b-110">Essa predefinição produz um único arquivo MP4 com uma taxa de bits de 18000 kbps e áudio AAC 5.1.</span><span class="sxs-lookup"><span data-stu-id="5a75b-110">This preset produces a single MP4 file with a bitrate of 18000 kbps, and AAC 5.1 audio.</span></span> <span data-ttu-id="5a75b-111">Para obter informações detalhadas sobre o perfil, taxa de bits, taxa de amostragem etc. Isso predefinido, examine Olá XML ou JSON definido abaixo.</span><span class="sxs-lookup"><span data-stu-id="5a75b-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine hello XML or JSON defined below.</span></span> <span data-ttu-id="5a75b-112">Para explicações significa que cada elemento e os valores válidos Olá para cada elemento, consulte Olá [esquema padrão do Media Encoder](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="5a75b-112">For explanations of what each element means, and hello valid values for each element, see hello [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5a75b-113">Você deve obter Olá Premium reservado codifica o tipo de unidade com 4K.</span><span class="sxs-lookup"><span data-stu-id="5a75b-113">You should get hello Premium reserved unit type with 4K encodes.</span></span> <span data-ttu-id="5a75b-114">Para obter mais informações, consulte [como tooScale codificação](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).</span><span class="sxs-lookup"><span data-stu-id="5a75b-114">For more information, see [How tooScale Encoding](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).</span></span>  
  
 <span data-ttu-id="5a75b-115">XML</span><span class="sxs-lookup"><span data-stu-id="5a75b-115">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>18000</Bitrate>  
          <Width>3840</Width>  
          <Height>2160</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>18000</MaxBitrate>  
        </H264Layer>  
      </H264Layers>  
      <Chapters />  
    </H264Video>  
    <AACAudio>  
      <Profile>AACLC</Profile>  
      <Channels>6</Channels>  
      <SamplingRate>48000</SamplingRate>  
      <Bitrate>384</Bitrate>  
    </AACAudio>  
  </Encoding>  
  <Outputs>  
    <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">  
      <MP4Format />  
    </Output>  
  </Outputs>  
</Preset>  
```  
  
 <span data-ttu-id="5a75b-116">JSON</span><span class="sxs-lookup"><span data-stu-id="5a75b-116">JSON</span></span>  
  
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
          "Bitrate": 18000,  
          "MaxBitrate": 18000,  
          "BufferWindow": "00:00:05",  
          "Width": 3840,  
          "Height": 2160,  
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
      "Channels": 6,  
      "SamplingRate": 48000,  
      "Bitrate": 384,  
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
