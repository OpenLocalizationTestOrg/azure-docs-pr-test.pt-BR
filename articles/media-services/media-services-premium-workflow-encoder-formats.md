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
# <a name="media-encoder-premium-workflow-formats-and-codecs"></a><span data-ttu-id="fc368-103">Codecs e formatos de fluxo de trabalho do Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="fc368-103">Media Encoder Premium Workflow formats and codecs</span></span>
> [!NOTE]
> <span data-ttu-id="fc368-104">Para solucionar dúvidas sobre o codificador premium, envie um email para o mepd em Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="fc368-104">For premium encoder questions, email mepd at Microsoft.com.</span></span>
> 
> <span data-ttu-id="fc368-105">O processador de mídia do Fluxo de Trabalho do Media Encoder Premium analisado neste tópico não está disponível na China.</span><span class="sxs-lookup"><span data-stu-id="fc368-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span> 
> 
> 

<span data-ttu-id="fc368-106">Este documento contém uma lista de formatos de arquivo de entrada e saída e codecs são suportados pela versão de visualização pública de saudação do hello **o fluxo de trabalho do Media Encoder Premium** codificador.</span><span class="sxs-lookup"><span data-stu-id="fc368-106">This document contains a list of input and output file formats and codecs that are supported by hello public preview version of hello **Media Encoder Premium Workflow** encoder.</span></span>

[<span data-ttu-id="fc368-107">Codecs e formatos de entrada de fluxo de trabalho do Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="fc368-107">Media Encoder Premium Worflow Input Formats and Codecs</span></span>](#input_formats)

[<span data-ttu-id="fc368-108">Codecs e formatos de saída de fluxo de trabalho do Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="fc368-108">Media Encoder Premium Worflow Output Formats and Codecs</span></span>](#output_formats)

<span data-ttu-id="fc368-109">**Fluxo de trabalho do Media Encoder Premium** dá suporte a legendas codificadas descritas [nesta](#closed_captioning) seção</span><span class="sxs-lookup"><span data-stu-id="fc368-109">**Media Encoder Premium Workflow** supports closed captioning described in [this](#closed_captioning) section.</span></span> 

## <span data-ttu-id="fc368-110"><a id="input_formats"></a>Codecs e formatos de entrada de fluxo de trabalho do Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="fc368-110"><a id="input_formats"></a>Media Encoder Premium Workflow Input Formats and Codecs</span></span>
<span data-ttu-id="fc368-111">Olá seção a seguir lista Olá codecs e formatos de arquivo que oferece suporte a este processador de mídia como entrada.</span><span class="sxs-lookup"><span data-stu-id="fc368-111">hello following section lists hello codecs and file formats that this media processor supports as input.</span></span>

### <a name="input-containerfile-formats"></a><span data-ttu-id="fc368-112">Formatos de arquivo/contêiner de entrada</span><span class="sxs-lookup"><span data-stu-id="fc368-112">Input Container/File Formats</span></span>
* <span data-ttu-id="fc368-113">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="fc368-113">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="fc368-114">MXF/SMPTE 377M</span><span class="sxs-lookup"><span data-stu-id="fc368-114">MXF/SMPTE 377M</span></span>
* <span data-ttu-id="fc368-115">GXF</span><span class="sxs-lookup"><span data-stu-id="fc368-115">GXF</span></span>
* <span data-ttu-id="fc368-116">Fluxos de transporte de MPEG-2</span><span class="sxs-lookup"><span data-stu-id="fc368-116">MPEG-2 Transport Streams</span></span>
* <span data-ttu-id="fc368-117">Fluxos de programa MPEG-2</span><span class="sxs-lookup"><span data-stu-id="fc368-117">MPEG-2 Program Streams</span></span>
* <span data-ttu-id="fc368-118">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="fc368-118">MPEG-4/MP4</span></span>
* <span data-ttu-id="fc368-119">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="fc368-119">Windows Media/ASF</span></span>
* <span data-ttu-id="fc368-120">AVI (8 bits/10 bits descompactado)</span><span class="sxs-lookup"><span data-stu-id="fc368-120">AVI (Uncompressed 8bit/10bit)</span></span>

### <a name="input-video-codecs"></a><span data-ttu-id="fc368-121">Codecs de vídeo de entrada</span><span class="sxs-lookup"><span data-stu-id="fc368-121">Input Video Codecs</span></span>
* <span data-ttu-id="fc368-122">AVC 8 bits/10 bits, o too4:2:2, incluindo AVCIntra</span><span class="sxs-lookup"><span data-stu-id="fc368-122">AVC 8-bit/10-bit, up too4:2:2, including AVCIntra</span></span>
* <span data-ttu-id="fc368-123">DNxHD ávido (em MXF)</span><span class="sxs-lookup"><span data-stu-id="fc368-123">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="fc368-124">DVCPro/DVCProHD (em MXF)</span><span class="sxs-lookup"><span data-stu-id="fc368-124">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="fc368-125">JPEG2000</span><span class="sxs-lookup"><span data-stu-id="fc368-125">JPEG2000</span></span>
* <span data-ttu-id="fc368-126">MPEG-2 (o perfil too422 e de alto nível, inclusive variantes como XDCAM, XDCAM HD, XDCAM IMX, CableLabs® e D10)</span><span class="sxs-lookup"><span data-stu-id="fc368-126">MPEG-2 (up too422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="fc368-127">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="fc368-127">MPEG-1</span></span>
* <span data-ttu-id="fc368-128">Windows Media Video/VC-1</span><span class="sxs-lookup"><span data-stu-id="fc368-128">Windows Media Video/VC-1</span></span>

### <a name="input-audio-codecs"></a><span data-ttu-id="fc368-129">Codecs de áudio de entrada</span><span class="sxs-lookup"><span data-stu-id="fc368-129">Input Audio Codecs</span></span>
* <span data-ttu-id="fc368-130">AES (SMPTE 331M e 302M, AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="fc368-130">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="fc368-131">Dolby® E</span><span class="sxs-lookup"><span data-stu-id="fc368-131">Dolby® E</span></span>
* <span data-ttu-id="fc368-132">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="fc368-132">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="fc368-133">AAC (AAC-LC, HE-AAC e AAC-HEv2; o too5.1)</span><span class="sxs-lookup"><span data-stu-id="fc368-133">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up too5.1)</span></span>
* <span data-ttu-id="fc368-134">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="fc368-134">MPEG Layer 2</span></span>
* <span data-ttu-id="fc368-135">MP3 (MPEG-1 Audio Layer 3)</span><span class="sxs-lookup"><span data-stu-id="fc368-135">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="fc368-136">Áudio do Windows Media</span><span class="sxs-lookup"><span data-stu-id="fc368-136">Windows Media Audio</span></span>
* <span data-ttu-id="fc368-137">WAV/PCM</span><span class="sxs-lookup"><span data-stu-id="fc368-137">WAV/PCM</span></span>

## <span data-ttu-id="fc368-138"><a id="output_format"></a>Codecs e formatos de saída de fluxo de trabalho do Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="fc368-138"><a id="output_format"></a>Media Encoder Premium Workflow Output Formats and Codecs</span></span>
<span data-ttu-id="fc368-139">Olá, seção a seguir lista Olá codecs e formatos de arquivo que têm suporte como a saída deste processador de mídia.</span><span class="sxs-lookup"><span data-stu-id="fc368-139">hello following section lists hello codecs and file formats that are supported as output from this media processor.</span></span>

### <a name="output-containerfile-formats"></a><span data-ttu-id="fc368-140">Formatos de contêiner/arquivo de saída</span><span class="sxs-lookup"><span data-stu-id="fc368-140">Output Container/File Formats</span></span>
* <span data-ttu-id="fc368-141">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="fc368-141">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="fc368-142">MXF (OP1a, XDCAM e AS02)</span><span class="sxs-lookup"><span data-stu-id="fc368-142">MXF (OP1a, XDCAM and AS02)</span></span>
* <span data-ttu-id="fc368-143">DPP (incluindo AS11)</span><span class="sxs-lookup"><span data-stu-id="fc368-143">DPP (including AS11)</span></span>
* <span data-ttu-id="fc368-144">GXF</span><span class="sxs-lookup"><span data-stu-id="fc368-144">GXF</span></span>
* <span data-ttu-id="fc368-145">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="fc368-145">MPEG-4/MP4</span></span>
* <span data-ttu-id="fc368-146">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="fc368-146">Windows Media/ASF</span></span>
* <span data-ttu-id="fc368-147">AVI (8 bits/10 bits descompactado)</span><span class="sxs-lookup"><span data-stu-id="fc368-147">AVI (Uncompressed 8bit/10bit)</span></span>
* <span data-ttu-id="fc368-148">Formato de arquivo do Smooth Streaming (PIFF 1.3)</span><span class="sxs-lookup"><span data-stu-id="fc368-148">Smooth Streaming File Format (PIFF 1.3)</span></span>
* <span data-ttu-id="fc368-149">MPEG-TS</span><span class="sxs-lookup"><span data-stu-id="fc368-149">MPEG-TS</span></span> 

### <a name="output-video-codecs"></a><span data-ttu-id="fc368-150">Codecs de vídeo de saída</span><span class="sxs-lookup"><span data-stu-id="fc368-150">Output Video Codecs</span></span>
* <span data-ttu-id="fc368-151">AVC (h. 264; 8 bits; até tooHigh perfil, nível 5.2; HD Ultra de 4K; Dentro de AVC)</span><span class="sxs-lookup"><span data-stu-id="fc368-151">AVC (H.264; 8-bit; up tooHigh Profile, Level 5.2; 4K Ultra HD; AVC Intra)</span></span>
* <span data-ttu-id="fc368-152">DNxHD ávido (em MXF)</span><span class="sxs-lookup"><span data-stu-id="fc368-152">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="fc368-153">DVCPro/DVCProHD (em MXF)</span><span class="sxs-lookup"><span data-stu-id="fc368-153">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="fc368-154">MPEG-2 (o perfil too422 e de alto nível, inclusive variantes como XDCAM, XDCAM HD, XDCAM IMX, CableLabs® e D10)</span><span class="sxs-lookup"><span data-stu-id="fc368-154">MPEG-2 (up too422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="fc368-155">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="fc368-155">MPEG-1</span></span>
* <span data-ttu-id="fc368-156">Windows Media Video/VC-1</span><span class="sxs-lookup"><span data-stu-id="fc368-156">Windows Media Video/VC-1</span></span>
* <span data-ttu-id="fc368-157">Criação de miniaturas JPEG</span><span class="sxs-lookup"><span data-stu-id="fc368-157">JPEG thumbnail creation</span></span>

### <a name="output-audio-codecs"></a><span data-ttu-id="fc368-158">Codecs de áudio de saída</span><span class="sxs-lookup"><span data-stu-id="fc368-158">Output Audio Codecs</span></span>
* <span data-ttu-id="fc368-159">AES (SMPTE 331M e 302M, AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="fc368-159">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="fc368-160">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="fc368-160">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="fc368-161">Dolby® Digital Plus (E AC3) backup too7.1</span><span class="sxs-lookup"><span data-stu-id="fc368-161">Dolby® Digital Plus (E-AC3) up too7.1</span></span>
* <span data-ttu-id="fc368-162">AAC (AAC-LC, HE-AAC e AAC-HEv2; o too5.1)</span><span class="sxs-lookup"><span data-stu-id="fc368-162">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up too5.1)</span></span>
* <span data-ttu-id="fc368-163">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="fc368-163">MPEG Layer 2</span></span>
* <span data-ttu-id="fc368-164">MP3 (MPEG-1 Audio Layer 3)</span><span class="sxs-lookup"><span data-stu-id="fc368-164">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="fc368-165">Áudio do Windows Media</span><span class="sxs-lookup"><span data-stu-id="fc368-165">Windows Media Audio</span></span>

>[!NOTE]
><span data-ttu-id="fc368-166">Se você codificar tooDolby® Digital (AC3), saída de hello só pode ser gravada em um arquivo ISO MP4.</span><span class="sxs-lookup"><span data-stu-id="fc368-166">If you encode tooDolby® Digital (AC3), hello output can only be written into an ISO MP4 file.</span></span>

## <span data-ttu-id="fc368-167"><a id="closed_captioning"></a>Suporte a legenda codificada</span><span class="sxs-lookup"><span data-stu-id="fc368-167"><a id="closed_captioning"></a>Support for Closed Captioning</span></span>
<span data-ttu-id="fc368-168">Na ingestão, o **fluxo de trabalho do Media Encoder Premium** dá suporte a:</span><span class="sxs-lookup"><span data-stu-id="fc368-168">On ingest, **Media Encoder Premium Workflow** supports:</span></span>

1. <span data-ttu-id="fc368-169">Arquivos SCC</span><span class="sxs-lookup"><span data-stu-id="fc368-169">SCC files</span></span>
2. <span data-ttu-id="fc368-170">Arquivos SMPTE-TT</span><span class="sxs-lookup"><span data-stu-id="fc368-170">SMPTE-TT files</span></span>
3. <span data-ttu-id="fc368-171">CEA-608/CEA-708 – transportados como dados de usuário (mensagens SEI de fluxos elementares H.264, ATSC/53, SCTE20) ou executados como dados complementares em arquivos MXF/GXF</span><span class="sxs-lookup"><span data-stu-id="fc368-171">CEA-608/CEA-708 – carried as user data (SEI messages of H.264 elementary streams, ATSC/53, SCTE20) or carried as ancillary data in MXF/GXF files</span></span>
4. <span data-ttu-id="fc368-172">Arquivos de legenda STL</span><span class="sxs-lookup"><span data-stu-id="fc368-172">STL subtitle files</span></span>

<span data-ttu-id="fc368-173">Na saída, Olá as opções a seguir está disponível:</span><span class="sxs-lookup"><span data-stu-id="fc368-173">On output, hello following options are available:</span></span>

1. <span data-ttu-id="fc368-174">608 CEA 708 tooCEA tradução</span><span class="sxs-lookup"><span data-stu-id="fc368-174">CEA-608 tooCEA-708 translation</span></span>
2. <span data-ttu-id="fc368-175">Transmissão CEA-608/CEA-708 (integrada em mensagens SEI para fluxos elementares H.264, ou carregada como dados auxiliares nos arquivos MXF)</span><span class="sxs-lookup"><span data-stu-id="fc368-175">CEA-608/CEA-708 pass through (embedded in SEI messages of H.264 elementary streams, or carried as ancillary data in MXF files)</span></span>
3. <span data-ttu-id="fc368-176">SCC</span><span class="sxs-lookup"><span data-stu-id="fc368-176">SCC</span></span>
4. <span data-ttu-id="fc368-177">Texto cronometrado de SMPTE (de origem CEA-608 por SMPTE RP2052, inclusive criação de arquivo DFXP)</span><span class="sxs-lookup"><span data-stu-id="fc368-177">SMPTE Timed Text (from source CEA-608 per SMPTE RP2052; including DFXP file creation)</span></span>
5. <span data-ttu-id="fc368-178">Arquivo de legenda SRT</span><span class="sxs-lookup"><span data-stu-id="fc368-178">SRT Subtitle file</span></span>
6. <span data-ttu-id="fc368-179">Fluxos de legenda DVB</span><span class="sxs-lookup"><span data-stu-id="fc368-179">DVB subtitle streams</span></span>

<span data-ttu-id="fc368-180">Observação: nem todos os Olá acima formatos de saída são suportados para fornecimento por meio de streaming nos serviços de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc368-180">Note: not all of hello above output formats are supported for delivery via streaming in Azure Media Services.</span></span>

## <a name="known-issues"></a><span data-ttu-id="fc368-181">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="fc368-181">Known issues</span></span>
<span data-ttu-id="fc368-182">Se o vídeo de entrada não contém a legenda codificada, Olá saída que ativo ainda conterá um arquivo TTML vazio.</span><span class="sxs-lookup"><span data-stu-id="fc368-182">If your input video does not contain closed captioning, hello output Asset will still contain an empty TTML file.</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="fc368-183">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="fc368-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fc368-184">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="fc368-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

