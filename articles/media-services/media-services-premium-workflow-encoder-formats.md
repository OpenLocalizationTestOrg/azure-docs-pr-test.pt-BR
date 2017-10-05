---
title: Codecs e formatos do Fluxo de Trabalho do Media Encoder Premium | Microsoft Docs
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
ms.openlocfilehash: e18de2adc9aac585d6890dd7b43a54f1a0ca177e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="media-encoder-premium-workflow-formats-and-codecs"></a><span data-ttu-id="cdf82-103">Codecs e formatos de fluxo de trabalho do Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="cdf82-103">Media Encoder Premium Workflow formats and codecs</span></span>
> [!NOTE]
> <span data-ttu-id="cdf82-104">Para solucionar dúvidas sobre o codificador premium, envie um email para o mepd em Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="cdf82-104">For premium encoder questions, email mepd at Microsoft.com.</span></span>
> 
> <span data-ttu-id="cdf82-105">O processador de mídia do Fluxo de Trabalho do Media Encoder Premium analisado neste tópico não está disponível na China.</span><span class="sxs-lookup"><span data-stu-id="cdf82-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span> 
> 
> 

<span data-ttu-id="cdf82-106">Este documento contém uma lista de formatos de arquivo de entrada e saída e codecs com suporte pela versão de demonstração pública do codificador de **Fluxo de trabalho do Media Encoder Premium** .</span><span class="sxs-lookup"><span data-stu-id="cdf82-106">This document contains a list of input and output file formats and codecs that are supported by the public preview version of the **Media Encoder Premium Workflow** encoder.</span></span>

[<span data-ttu-id="cdf82-107">Codecs e formatos de entrada de fluxo de trabalho do Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="cdf82-107">Media Encoder Premium Worflow Input Formats and Codecs</span></span>](#input_formats)

[<span data-ttu-id="cdf82-108">Codecs e formatos de saída de fluxo de trabalho do Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="cdf82-108">Media Encoder Premium Worflow Output Formats and Codecs</span></span>](#output_formats)

<span data-ttu-id="cdf82-109">**Fluxo de trabalho do Media Encoder Premium** dá suporte a legendas codificadas descritas [nesta](#closed_captioning) seção</span><span class="sxs-lookup"><span data-stu-id="cdf82-109">**Media Encoder Premium Workflow** supports closed captioning described in [this](#closed_captioning) section.</span></span> 

## <span data-ttu-id="cdf82-110"><a id="input_formats"></a>Codecs e formatos de entrada de fluxo de trabalho do Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="cdf82-110"><a id="input_formats"></a>Media Encoder Premium Workflow Input Formats and Codecs</span></span>
<span data-ttu-id="cdf82-111">A seção a seguir lista os codecs e formatos de arquivo aos quais esse processador de mídia dá suporte como entrada.</span><span class="sxs-lookup"><span data-stu-id="cdf82-111">The following section lists the codecs and file formats that this media processor supports as input.</span></span>

### <a name="input-containerfile-formats"></a><span data-ttu-id="cdf82-112">Formatos de arquivo/contêiner de entrada</span><span class="sxs-lookup"><span data-stu-id="cdf82-112">Input Container/File Formats</span></span>
* <span data-ttu-id="cdf82-113">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="cdf82-113">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="cdf82-114">MXF/SMPTE 377M</span><span class="sxs-lookup"><span data-stu-id="cdf82-114">MXF/SMPTE 377M</span></span>
* <span data-ttu-id="cdf82-115">GXF</span><span class="sxs-lookup"><span data-stu-id="cdf82-115">GXF</span></span>
* <span data-ttu-id="cdf82-116">Fluxos de transporte de MPEG-2</span><span class="sxs-lookup"><span data-stu-id="cdf82-116">MPEG-2 Transport Streams</span></span>
* <span data-ttu-id="cdf82-117">Fluxos de programa MPEG-2</span><span class="sxs-lookup"><span data-stu-id="cdf82-117">MPEG-2 Program Streams</span></span>
* <span data-ttu-id="cdf82-118">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="cdf82-118">MPEG-4/MP4</span></span>
* <span data-ttu-id="cdf82-119">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="cdf82-119">Windows Media/ASF</span></span>
* <span data-ttu-id="cdf82-120">AVI (8 bits/10 bits descompactado)</span><span class="sxs-lookup"><span data-stu-id="cdf82-120">AVI (Uncompressed 8bit/10bit)</span></span>

### <a name="input-video-codecs"></a><span data-ttu-id="cdf82-121">Codecs de vídeo de entrada</span><span class="sxs-lookup"><span data-stu-id="cdf82-121">Input Video Codecs</span></span>
* <span data-ttu-id="cdf82-122">AVC de 8 bits/10 bits até 4:2:2, incluindo AVCIntra</span><span class="sxs-lookup"><span data-stu-id="cdf82-122">AVC 8-bit/10-bit, up to 4:2:2, including AVCIntra</span></span>
* <span data-ttu-id="cdf82-123">DNxHD ávido (em MXF)</span><span class="sxs-lookup"><span data-stu-id="cdf82-123">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="cdf82-124">DVCPro/DVCProHD (em MXF)</span><span class="sxs-lookup"><span data-stu-id="cdf82-124">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="cdf82-125">JPEG2000</span><span class="sxs-lookup"><span data-stu-id="cdf82-125">JPEG2000</span></span>
* <span data-ttu-id="cdf82-126">MPEG-2 (até perfil e de alto nível 422; incluindo variantes como XDCAM, XDCAM HD, XDCAM IMX, CableLabs ® e D10)</span><span class="sxs-lookup"><span data-stu-id="cdf82-126">MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="cdf82-127">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="cdf82-127">MPEG-1</span></span>
* <span data-ttu-id="cdf82-128">Windows Media Video/VC-1</span><span class="sxs-lookup"><span data-stu-id="cdf82-128">Windows Media Video/VC-1</span></span>

### <a name="input-audio-codecs"></a><span data-ttu-id="cdf82-129">Codecs de áudio de entrada</span><span class="sxs-lookup"><span data-stu-id="cdf82-129">Input Audio Codecs</span></span>
* <span data-ttu-id="cdf82-130">AES (SMPTE 331M e 302M, AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="cdf82-130">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="cdf82-131">Dolby® E</span><span class="sxs-lookup"><span data-stu-id="cdf82-131">Dolby® E</span></span>
* <span data-ttu-id="cdf82-132">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="cdf82-132">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="cdf82-133">AAC (AAC-LC, AAC-HE e AAC-HEv2; até 5.1)</span><span class="sxs-lookup"><span data-stu-id="cdf82-133">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1)</span></span>
* <span data-ttu-id="cdf82-134">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="cdf82-134">MPEG Layer 2</span></span>
* <span data-ttu-id="cdf82-135">MP3 (MPEG-1 Audio Layer 3)</span><span class="sxs-lookup"><span data-stu-id="cdf82-135">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="cdf82-136">Áudio do Windows Media</span><span class="sxs-lookup"><span data-stu-id="cdf82-136">Windows Media Audio</span></span>
* <span data-ttu-id="cdf82-137">WAV/PCM</span><span class="sxs-lookup"><span data-stu-id="cdf82-137">WAV/PCM</span></span>

## <span data-ttu-id="cdf82-138"><a id="output_format"></a>Codecs e formatos de saída de fluxo de trabalho do Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="cdf82-138"><a id="output_format"></a>Media Encoder Premium Workflow Output Formats and Codecs</span></span>
<span data-ttu-id="cdf82-139">A seção a seguir lista os codecs e formatos de arquivo com suporte como a saída desse processador de mídia.</span><span class="sxs-lookup"><span data-stu-id="cdf82-139">The following section lists the codecs and file formats that are supported as output from this media processor.</span></span>

### <a name="output-containerfile-formats"></a><span data-ttu-id="cdf82-140">Formatos de contêiner/arquivo de saída</span><span class="sxs-lookup"><span data-stu-id="cdf82-140">Output Container/File Formats</span></span>
* <span data-ttu-id="cdf82-141">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="cdf82-141">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="cdf82-142">MXF (OP1a, XDCAM e AS02)</span><span class="sxs-lookup"><span data-stu-id="cdf82-142">MXF (OP1a, XDCAM and AS02)</span></span>
* <span data-ttu-id="cdf82-143">DPP (incluindo AS11)</span><span class="sxs-lookup"><span data-stu-id="cdf82-143">DPP (including AS11)</span></span>
* <span data-ttu-id="cdf82-144">GXF</span><span class="sxs-lookup"><span data-stu-id="cdf82-144">GXF</span></span>
* <span data-ttu-id="cdf82-145">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="cdf82-145">MPEG-4/MP4</span></span>
* <span data-ttu-id="cdf82-146">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="cdf82-146">Windows Media/ASF</span></span>
* <span data-ttu-id="cdf82-147">AVI (8 bits/10 bits descompactado)</span><span class="sxs-lookup"><span data-stu-id="cdf82-147">AVI (Uncompressed 8bit/10bit)</span></span>
* <span data-ttu-id="cdf82-148">Formato de arquivo do Smooth Streaming (PIFF 1.3)</span><span class="sxs-lookup"><span data-stu-id="cdf82-148">Smooth Streaming File Format (PIFF 1.3)</span></span>
* <span data-ttu-id="cdf82-149">MPEG-TS</span><span class="sxs-lookup"><span data-stu-id="cdf82-149">MPEG-TS</span></span> 

### <a name="output-video-codecs"></a><span data-ttu-id="cdf82-150">Codecs de vídeo de saída</span><span class="sxs-lookup"><span data-stu-id="cdf82-150">Output Video Codecs</span></span>
* <span data-ttu-id="cdf82-151">AVC (H. 264; 8 bits; até perfil, nível elevado 5.2; 4K Ultra HD; Intra AVC)</span><span class="sxs-lookup"><span data-stu-id="cdf82-151">AVC (H.264; 8-bit; up to High Profile, Level 5.2; 4K Ultra HD; AVC Intra)</span></span>
* <span data-ttu-id="cdf82-152">DNxHD ávido (em MXF)</span><span class="sxs-lookup"><span data-stu-id="cdf82-152">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="cdf82-153">DVCPro/DVCProHD (em MXF)</span><span class="sxs-lookup"><span data-stu-id="cdf82-153">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="cdf82-154">MPEG-2 (até perfil e de alto nível 422; incluindo variantes como XDCAM, XDCAM HD, XDCAM IMX, CableLabs ® e D10)</span><span class="sxs-lookup"><span data-stu-id="cdf82-154">MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="cdf82-155">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="cdf82-155">MPEG-1</span></span>
* <span data-ttu-id="cdf82-156">Windows Media Video/VC-1</span><span class="sxs-lookup"><span data-stu-id="cdf82-156">Windows Media Video/VC-1</span></span>
* <span data-ttu-id="cdf82-157">Criação de miniaturas JPEG</span><span class="sxs-lookup"><span data-stu-id="cdf82-157">JPEG thumbnail creation</span></span>

### <a name="output-audio-codecs"></a><span data-ttu-id="cdf82-158">Codecs de áudio de saída</span><span class="sxs-lookup"><span data-stu-id="cdf82-158">Output Audio Codecs</span></span>
* <span data-ttu-id="cdf82-159">AES (SMPTE 331M e 302M, AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="cdf82-159">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="cdf82-160">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="cdf82-160">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="cdf82-161">Dolby ® Digital Plus (E-AC3) até 7.1</span><span class="sxs-lookup"><span data-stu-id="cdf82-161">Dolby® Digital Plus (E-AC3) up to 7.1</span></span>
* <span data-ttu-id="cdf82-162">AAC (AAC-LC, AAC-HE e AAC-HEv2; até 5.1)</span><span class="sxs-lookup"><span data-stu-id="cdf82-162">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1)</span></span>
* <span data-ttu-id="cdf82-163">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="cdf82-163">MPEG Layer 2</span></span>
* <span data-ttu-id="cdf82-164">MP3 (MPEG-1 Audio Layer 3)</span><span class="sxs-lookup"><span data-stu-id="cdf82-164">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="cdf82-165">Áudio do Windows Media</span><span class="sxs-lookup"><span data-stu-id="cdf82-165">Windows Media Audio</span></span>

>[!NOTE]
><span data-ttu-id="cdf82-166">Se você codificar para Dolby® Digital (AC3), a saída só poderá ser gravada em um arquivo ISO MP4.</span><span class="sxs-lookup"><span data-stu-id="cdf82-166">If you encode to Dolby® Digital (AC3), the output can only be written into an ISO MP4 file.</span></span>

## <span data-ttu-id="cdf82-167"><a id="closed_captioning"></a>Suporte a legenda codificada</span><span class="sxs-lookup"><span data-stu-id="cdf82-167"><a id="closed_captioning"></a>Support for Closed Captioning</span></span>
<span data-ttu-id="cdf82-168">Na ingestão, o **fluxo de trabalho do Media Encoder Premium** dá suporte a:</span><span class="sxs-lookup"><span data-stu-id="cdf82-168">On ingest, **Media Encoder Premium Workflow** supports:</span></span>

1. <span data-ttu-id="cdf82-169">Arquivos SCC</span><span class="sxs-lookup"><span data-stu-id="cdf82-169">SCC files</span></span>
2. <span data-ttu-id="cdf82-170">Arquivos SMPTE-TT</span><span class="sxs-lookup"><span data-stu-id="cdf82-170">SMPTE-TT files</span></span>
3. <span data-ttu-id="cdf82-171">CEA-608/CEA-708 – transportados como dados de usuário (mensagens SEI de fluxos elementares H.264, ATSC/53, SCTE20) ou executados como dados complementares em arquivos MXF/GXF</span><span class="sxs-lookup"><span data-stu-id="cdf82-171">CEA-608/CEA-708 – carried as user data (SEI messages of H.264 elementary streams, ATSC/53, SCTE20) or carried as ancillary data in MXF/GXF files</span></span>
4. <span data-ttu-id="cdf82-172">Arquivos de legenda STL</span><span class="sxs-lookup"><span data-stu-id="cdf82-172">STL subtitle files</span></span>

<span data-ttu-id="cdf82-173">Na saída, as seguintes opções estão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="cdf82-173">On output, the following options are available:</span></span>

1. <span data-ttu-id="cdf82-174">Tradução de CEA-608 para CEA-708</span><span class="sxs-lookup"><span data-stu-id="cdf82-174">CEA-608 to CEA-708 translation</span></span>
2. <span data-ttu-id="cdf82-175">Transmissão CEA-608/CEA-708 (integrada em mensagens SEI para fluxos elementares H.264, ou carregada como dados auxiliares nos arquivos MXF)</span><span class="sxs-lookup"><span data-stu-id="cdf82-175">CEA-608/CEA-708 pass through (embedded in SEI messages of H.264 elementary streams, or carried as ancillary data in MXF files)</span></span>
3. <span data-ttu-id="cdf82-176">SCC</span><span class="sxs-lookup"><span data-stu-id="cdf82-176">SCC</span></span>
4. <span data-ttu-id="cdf82-177">Texto cronometrado de SMPTE (de origem CEA-608 por SMPTE RP2052, inclusive criação de arquivo DFXP)</span><span class="sxs-lookup"><span data-stu-id="cdf82-177">SMPTE Timed Text (from source CEA-608 per SMPTE RP2052; including DFXP file creation)</span></span>
5. <span data-ttu-id="cdf82-178">Arquivo de legenda SRT</span><span class="sxs-lookup"><span data-stu-id="cdf82-178">SRT Subtitle file</span></span>
6. <span data-ttu-id="cdf82-179">Fluxos de legenda DVB</span><span class="sxs-lookup"><span data-stu-id="cdf82-179">DVB subtitle streams</span></span>

<span data-ttu-id="cdf82-180">Observação: nem todos os formatos de saída acima têm suporte para fornecimento por meio de streaming nos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdf82-180">Note: not all of the above output formats are supported for delivery via streaming in Azure Media Services.</span></span>

## <a name="known-issues"></a><span data-ttu-id="cdf82-181">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="cdf82-181">Known issues</span></span>
<span data-ttu-id="cdf82-182">Se o vídeo de entrada não contiver a legendagem oculta, o ativo de saída ainda conterá um arquivo TTML vazio.</span><span class="sxs-lookup"><span data-stu-id="cdf82-182">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="cdf82-183">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="cdf82-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cdf82-184">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="cdf82-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

