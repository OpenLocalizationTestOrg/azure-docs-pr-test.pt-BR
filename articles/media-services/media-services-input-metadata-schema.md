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
# <a name="input-metadata"></a><span data-ttu-id="2ab58-103">Metadados de entrada</span><span class="sxs-lookup"><span data-stu-id="2ab58-103">Input Metadata</span></span>
<span data-ttu-id="2ab58-104">Um trabalho de codificação está associado um ativo de entrada (ou ativos) no qual você deseja tooperform algumas tarefas de codificação.</span><span class="sxs-lookup"><span data-stu-id="2ab58-104">An encoding job is associated with an input asset (or assets) on which you want tooperform some encoding tasks.</span></span>  <span data-ttu-id="2ab58-105">Após a conclusão de uma tarefa, um ativo de saída é produzido.</span><span class="sxs-lookup"><span data-stu-id="2ab58-105">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="2ab58-106">Olá ativo de saída contém vídeo, áudio, miniaturas manifestos, etc. Olá também contém um arquivo com metadados sobre o ativo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="2ab58-106">hello output asset contains video, audio, thumbnails, manifest, etc. hello output asset also contains a file with metadata about hello input asset.</span></span> <span data-ttu-id="2ab58-107">nome do arquivo XML de metadados Olá Olá tem Olá formato a seguir: &lt;asset_id&gt;<asset_id>_metadata.XML (por exemplo, 41114ad3-eb5e - 4c 57 8d 92-5354e2b7d4a4_metadata.xml), onde &lt;asset_id&gt; é hello AssetId valor do ativo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="2ab58-107">hello name of hello metadata XML file has hello following format: &lt;asset_id&gt;_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where &lt;asset_id&gt; is hello AssetId value of hello input asset.</span></span>  

<span data-ttu-id="2ab58-108">Se desejar que o arquivo de metadados de saudação tooexamine, você pode criar um **SAS** localizador e download Olá computador local do arquivo tooyour.</span><span class="sxs-lookup"><span data-stu-id="2ab58-108">If you want tooexamine hello metadata file, you can create a **SAS** locator and download hello file tooyour local computer.</span></span> <span data-ttu-id="2ab58-109">Você pode encontrar um exemplo sobre como toocreate um localizador SAS e baixar um arquivo [usando extensões de SDK .NET do serviços de mídia Olá](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2ab58-109">You can find an example on how toocreate a SAS locator and download a file  [Using hello Media Services .NET SDK Extensions](media-services-dotnet-get-started.md).</span></span>  

<span data-ttu-id="2ab58-110">Este tópico discute elementos hello e tipos de esquema XML, Olá em quais metadados de entrada hello (&lt;asset_id&gt;<asset_id>_metadata.xml) é baseado.</span><span class="sxs-lookup"><span data-stu-id="2ab58-110">This topic discusses hello elements and types of hello XML schema on which hello input metada (&lt;asset_id&gt;_metadata.xml) is based.</span></span>  <span data-ttu-id="2ab58-111">Para obter informações sobre o arquivo hello que contém metadados sobre o ativo de saída de hello, consulte [metadados de saída](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="2ab58-111">For information about hello file that contains metadata about hello output asset, see [Output Metadata](media-services-output-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="2ab58-112">Você pode encontrar hello [código de esquema](media-services-input-metadata-schema.md#code) um [exemplo XML](media-services-input-metadata-schema.md#xml) final Olá deste tópico.</span><span class="sxs-lookup"><span data-stu-id="2ab58-112">You can find hello [Schema Code](media-services-input-metadata-schema.md#code) an [XML example](media-services-input-metadata-schema.md#xml) at hello end of this topic.</span></span>  
> 
> 

## <span data-ttu-id="2ab58-113"><a name="AssetFiles"></a> Elemento AssetFiles (elemento raiz)</span><span class="sxs-lookup"><span data-stu-id="2ab58-113"><a name="AssetFiles"></a> AssetFiles element (root element)</span></span>
<span data-ttu-id="2ab58-114">Contém uma coleção de [elemento AssetFile](media-services-input-metadata-schema.md#AssetFile)s para o trabalho de codificação hello.</span><span class="sxs-lookup"><span data-stu-id="2ab58-114">Contains a collection of [AssetFile element](media-services-input-metadata-schema.md#AssetFile)s for hello encoding job.</span></span>  

<span data-ttu-id="2ab58-115">Veja um exemplo XML no final deste tópico Olá: [exemplo XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="2ab58-115">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

| <span data-ttu-id="2ab58-116">Nome</span><span class="sxs-lookup"><span data-stu-id="2ab58-116">Name</span></span> | <span data-ttu-id="2ab58-117">Descrição</span><span class="sxs-lookup"><span data-stu-id="2ab58-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2ab58-118">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="2ab58-118">**AssetFile**</span></span><br /><br /> <span data-ttu-id="2ab58-119">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="2ab58-119">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="2ab58-120">Um único elemento filho.</span><span class="sxs-lookup"><span data-stu-id="2ab58-120">A single child element.</span></span> <span data-ttu-id="2ab58-121">Para saber mais, veja [Elemento AssetFile](media-services-input-metadata-schema.md#AssetFile).</span><span class="sxs-lookup"><span data-stu-id="2ab58-121">For more information, see [AssetFile element](media-services-input-metadata-schema.md#AssetFile).</span></span> |

## <span data-ttu-id="2ab58-122"><a name="AssetFile"></a> Elemento AssetFile</span><span class="sxs-lookup"><span data-stu-id="2ab58-122"><a name="AssetFile"></a> AssetFile element</span></span>
 <span data-ttu-id="2ab58-123">Contém atributos e elementos que descrevem um arquivo de ativo.</span><span class="sxs-lookup"><span data-stu-id="2ab58-123">Contains attributes and elements that describe an asset file.</span></span>  

 <span data-ttu-id="2ab58-124">Veja um exemplo XML no final deste tópico Olá: [exemplo XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="2ab58-124">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="2ab58-125">Atributos</span><span class="sxs-lookup"><span data-stu-id="2ab58-125">Attributes</span></span>
| <span data-ttu-id="2ab58-126">Nome</span><span class="sxs-lookup"><span data-stu-id="2ab58-126">Name</span></span> | <span data-ttu-id="2ab58-127">Tipo</span><span class="sxs-lookup"><span data-stu-id="2ab58-127">Type</span></span> | <span data-ttu-id="2ab58-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="2ab58-128">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ab58-129">**Nome**</span><span class="sxs-lookup"><span data-stu-id="2ab58-129">**Name**</span></span><br /><br /> <span data-ttu-id="2ab58-130">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-130">Required</span></span> |<span data-ttu-id="2ab58-131">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2ab58-131">**xs:string**</span></span> |<span data-ttu-id="2ab58-132">Nome do arquivo de ativo.</span><span class="sxs-lookup"><span data-stu-id="2ab58-132">Asset file name.</span></span> |
| <span data-ttu-id="2ab58-133">**Tamanho**</span><span class="sxs-lookup"><span data-stu-id="2ab58-133">**Size**</span></span><br /><br /> <span data-ttu-id="2ab58-134">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-134">Required</span></span> |<span data-ttu-id="2ab58-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="2ab58-135">**xs:long**</span></span> |<span data-ttu-id="2ab58-136">Tamanho do arquivo de ativo de saudação em bytes.</span><span class="sxs-lookup"><span data-stu-id="2ab58-136">Size of hello asset file in bytes.</span></span> |
| <span data-ttu-id="2ab58-137">**Duração**</span><span class="sxs-lookup"><span data-stu-id="2ab58-137">**Duration**</span></span><br /><br /> <span data-ttu-id="2ab58-138">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-138">Required</span></span> |<span data-ttu-id="2ab58-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="2ab58-139">**xs:duration**</span></span> |<span data-ttu-id="2ab58-140">Duração da reprodução de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="2ab58-140">Content play back duration.</span></span> <span data-ttu-id="2ab58-141">Exemplo: Duration="PT25M37.757S".</span><span class="sxs-lookup"><span data-stu-id="2ab58-141">Example: Duration="PT25M37.757S".</span></span> |
| <span data-ttu-id="2ab58-142">**NumberOfStreams**</span><span class="sxs-lookup"><span data-stu-id="2ab58-142">**NumberOfStreams**</span></span><br /><br /> <span data-ttu-id="2ab58-143">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-143">Required</span></span> |<span data-ttu-id="2ab58-144">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-144">**xs:int**</span></span> |<span data-ttu-id="2ab58-145">Número de fluxos no arquivo de ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab58-145">Number of streams in hello asset file.</span></span> |
| <span data-ttu-id="2ab58-146">**FormatNames**</span><span class="sxs-lookup"><span data-stu-id="2ab58-146">**FormatNames**</span></span><br /><br /> <span data-ttu-id="2ab58-147">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-147">Required</span></span> |<span data-ttu-id="2ab58-148">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2ab58-148">**xs:string**</span></span> |<span data-ttu-id="2ab58-149">Nomes de formato.</span><span class="sxs-lookup"><span data-stu-id="2ab58-149">Format names.</span></span> |
| <span data-ttu-id="2ab58-150">**FormatVerboseNames**</span><span class="sxs-lookup"><span data-stu-id="2ab58-150">**FormatVerboseNames**</span></span><br /><br /> <span data-ttu-id="2ab58-151">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-151">Required</span></span> |<span data-ttu-id="2ab58-152">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2ab58-152">**xs:string**</span></span> |<span data-ttu-id="2ab58-153">Nomes detalhados de formato.</span><span class="sxs-lookup"><span data-stu-id="2ab58-153">Format verbose names.</span></span> |
| <span data-ttu-id="2ab58-154">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="2ab58-154">**StartTime**</span></span> |<span data-ttu-id="2ab58-155">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="2ab58-155">**xs:duration**</span></span> |<span data-ttu-id="2ab58-156">Hora de início do conteúdo.</span><span class="sxs-lookup"><span data-stu-id="2ab58-156">Content start time.</span></span> <span data-ttu-id="2ab58-157">Exemplo: StartTime = "PT2.669S".</span><span class="sxs-lookup"><span data-stu-id="2ab58-157">Example: StartTime="PT2.669S".</span></span> |
| <span data-ttu-id="2ab58-158">**OverallBitRate**</span><span class="sxs-lookup"><span data-stu-id="2ab58-158">**OverallBitRate**</span></span> |<span data-ttu-id="2ab58-159">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-159">**xs:int**</span></span> |<span data-ttu-id="2ab58-160">Taxa de bits média do arquivo de ativo de saudação em kbps.</span><span class="sxs-lookup"><span data-stu-id="2ab58-160">Average bitrate of hello asset file in kbps.</span></span> |

> [!NOTE]
> <span data-ttu-id="2ab58-161">Olá 4 elementos filhos a seguir deve aparecer em uma sequência.</span><span class="sxs-lookup"><span data-stu-id="2ab58-161">hello following 4 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="2ab58-162">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="2ab58-162">Child elements</span></span>
| <span data-ttu-id="2ab58-163">Nome</span><span class="sxs-lookup"><span data-stu-id="2ab58-163">Name</span></span> | <span data-ttu-id="2ab58-164">Tipo</span><span class="sxs-lookup"><span data-stu-id="2ab58-164">Type</span></span> | <span data-ttu-id="2ab58-165">Descrição</span><span class="sxs-lookup"><span data-stu-id="2ab58-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ab58-166">**Programas**</span><span class="sxs-lookup"><span data-stu-id="2ab58-166">**Programs**</span></span><br /><br /> <span data-ttu-id="2ab58-167">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="2ab58-167">minOccurs="0"</span></span> | |<span data-ttu-id="2ab58-168">Coleção de todos os [elemento programas](media-services-input-metadata-schema.md#Programs) quando o arquivo de ativo hello está em formato MPEG-TS.</span><span class="sxs-lookup"><span data-stu-id="2ab58-168">Collection of all [Programs element](media-services-input-metadata-schema.md#Programs) when hello asset file is in MPEG-TS format.</span></span> |
| <span data-ttu-id="2ab58-169">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="2ab58-169">**VideoTracks**</span></span><br /><br /> <span data-ttu-id="2ab58-170">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="2ab58-170">minOccurs="0"</span></span> | |<span data-ttu-id="2ab58-171">Cada arquivo de ativo físico pode conter nenhuma ou mais faixas de vídeo intercaladas em um formato de contêiner apropriado.</span><span class="sxs-lookup"><span data-stu-id="2ab58-171">Each physical asset file can contain zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="2ab58-172">Esse elemento contém uma coleção de todos os [elemento VideoTracks](media-services-input-metadata-schema.md#VideoTracks) que fazem parte do arquivo de ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab58-172">This element contains a collection of all [VideoTracks element](media-services-input-metadata-schema.md#VideoTracks) that are part of hello asset file.</span></span> |
| <span data-ttu-id="2ab58-173">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="2ab58-173">**AudioTracks**</span></span><br /><br /> <span data-ttu-id="2ab58-174">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="2ab58-174">minOccurs="0"</span></span> | |<span data-ttu-id="2ab58-175">Cada arquivo de ativo físico pode conter nenhuma ou mais faixas de áudio intercaladas em um formato de contêiner apropriado.</span><span class="sxs-lookup"><span data-stu-id="2ab58-175">Each physical asset file can contain zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="2ab58-176">Esse elemento contém uma coleção de todos os [elemento AudioTracks](media-services-input-metadata-schema.md#AudioTracks) que fazem parte do arquivo de ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab58-176">This element contains a collection of all [AudioTracks element](media-services-input-metadata-schema.md#AudioTracks) that are part of hello asset file.</span></span> |
| <span data-ttu-id="2ab58-177">**Metadados**</span><span class="sxs-lookup"><span data-stu-id="2ab58-177">**Metadata**</span></span><br /><br /> <span data-ttu-id="2ab58-178">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="2ab58-178">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="2ab58-179">MetadataType</span><span class="sxs-lookup"><span data-stu-id="2ab58-179">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="2ab58-180">Metadados do arquivo de ativo representados como cadeias de caracteres de chave\valor.</span><span class="sxs-lookup"><span data-stu-id="2ab58-180">Asset file’s metadata represented as key\value strings.</span></span> <span data-ttu-id="2ab58-181">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2ab58-181">For example:</span></span><br /><br /> <span data-ttu-id="2ab58-182">**&lt;Metadata key="language" value="eng" /&gt;**</span><span class="sxs-lookup"><span data-stu-id="2ab58-182">**&lt;Metadata key="language" value="eng" /&gt;**</span></span> |

## <span data-ttu-id="2ab58-183"><a name="TrackType"></a> TrackType</span><span class="sxs-lookup"><span data-stu-id="2ab58-183"><a name="TrackType"></a> TrackType</span></span>
<span data-ttu-id="2ab58-184">Veja um exemplo XML no final deste tópico Olá: [exemplo XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="2ab58-184">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="2ab58-185">Atributos</span><span class="sxs-lookup"><span data-stu-id="2ab58-185">Attributes</span></span>
| <span data-ttu-id="2ab58-186">Nome</span><span class="sxs-lookup"><span data-stu-id="2ab58-186">Name</span></span> | <span data-ttu-id="2ab58-187">Tipo</span><span class="sxs-lookup"><span data-stu-id="2ab58-187">Type</span></span> | <span data-ttu-id="2ab58-188">Descrição</span><span class="sxs-lookup"><span data-stu-id="2ab58-188">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ab58-189">**Id**</span><span class="sxs-lookup"><span data-stu-id="2ab58-189">**Id**</span></span><br /><br /> <span data-ttu-id="2ab58-190">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-190">Required</span></span> |<span data-ttu-id="2ab58-191">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-191">**xs:int**</span></span> |<span data-ttu-id="2ab58-192">Índice baseado em zero da faixa de áudio ou de vídeo.</span><span class="sxs-lookup"><span data-stu-id="2ab58-192">Zero-based index of this audio or video track.</span></span><br /><br /> <span data-ttu-id="2ab58-193">Isso não é necessariamente que Olá TrackID como utilizado em um arquivo MP4.</span><span class="sxs-lookup"><span data-stu-id="2ab58-193">This is not necessarily that hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="2ab58-194">**Codec**</span><span class="sxs-lookup"><span data-stu-id="2ab58-194">**Codec**</span></span> |<span data-ttu-id="2ab58-195">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2ab58-195">**xs:string**</span></span> |<span data-ttu-id="2ab58-196">Cadeia de caracteres de codec de faixa de vídeo.</span><span class="sxs-lookup"><span data-stu-id="2ab58-196">Video track codec string.</span></span> |
| <span data-ttu-id="2ab58-197">**CodecLongName**</span><span class="sxs-lookup"><span data-stu-id="2ab58-197">**CodecLongName**</span></span> |<span data-ttu-id="2ab58-198">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2ab58-198">**xs:string**</span></span> |<span data-ttu-id="2ab58-199">Nome longo de codec de faixa de áudio ou vídeo.</span><span class="sxs-lookup"><span data-stu-id="2ab58-199">Audio or video track codec long name.</span></span> |
| <span data-ttu-id="2ab58-200">**TimeBase**</span><span class="sxs-lookup"><span data-stu-id="2ab58-200">**TimeBase**</span></span><br /><br /> <span data-ttu-id="2ab58-201">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-201">Required</span></span> |<span data-ttu-id="2ab58-202">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2ab58-202">**xs:string**</span></span> |<span data-ttu-id="2ab58-203">Base de tempo.</span><span class="sxs-lookup"><span data-stu-id="2ab58-203">Time base.</span></span> <span data-ttu-id="2ab58-204">Exemplo: TimeBase="1/48000"</span><span class="sxs-lookup"><span data-stu-id="2ab58-204">Example: TimeBase="1/48000"</span></span> |
| <span data-ttu-id="2ab58-205">**NumberOfFrames**</span><span class="sxs-lookup"><span data-stu-id="2ab58-205">**NumberOfFrames**</span></span> |<span data-ttu-id="2ab58-206">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-206">**xs:int**</span></span> |<span data-ttu-id="2ab58-207">Número de quadros (presentes em faixas de vídeo).</span><span class="sxs-lookup"><span data-stu-id="2ab58-207">Number of frames (present for video tracks).</span></span> |
| <span data-ttu-id="2ab58-208">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="2ab58-208">**StartTime**</span></span> |<span data-ttu-id="2ab58-209">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="2ab58-209">**xs:duration**</span></span> |<span data-ttu-id="2ab58-210">Hora de início da faixa.</span><span class="sxs-lookup"><span data-stu-id="2ab58-210">Track start time.</span></span> <span data-ttu-id="2ab58-211">Exemplo: StartTime="PT2.669S"</span><span class="sxs-lookup"><span data-stu-id="2ab58-211">Example: StartTime="PT2.669S"</span></span> |
| <span data-ttu-id="2ab58-212">**Duração**</span><span class="sxs-lookup"><span data-stu-id="2ab58-212">**Duration**</span></span> |<span data-ttu-id="2ab58-213">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="2ab58-213">**xs:duration**</span></span> |<span data-ttu-id="2ab58-214">Duração da faixa.</span><span class="sxs-lookup"><span data-stu-id="2ab58-214">Track duration.</span></span> <span data-ttu-id="2ab58-215">Exemplo: Duration="PTSampleFormat M37.757S".</span><span class="sxs-lookup"><span data-stu-id="2ab58-215">Example: Duration="PTSampleFormat M37.757S".</span></span> |

> [!NOTE]
> <span data-ttu-id="2ab58-216">Olá 2 elementos filho a seguir deve aparecer em uma sequência.</span><span class="sxs-lookup"><span data-stu-id="2ab58-216">hello following 2 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="2ab58-217">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="2ab58-217">Child elements</span></span>
| <span data-ttu-id="2ab58-218">Nome</span><span class="sxs-lookup"><span data-stu-id="2ab58-218">Name</span></span> | <span data-ttu-id="2ab58-219">Tipo</span><span class="sxs-lookup"><span data-stu-id="2ab58-219">Type</span></span> | <span data-ttu-id="2ab58-220">Descrição</span><span class="sxs-lookup"><span data-stu-id="2ab58-220">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ab58-221">**Disposição**</span><span class="sxs-lookup"><span data-stu-id="2ab58-221">**Disposition**</span></span><br /><br /> <span data-ttu-id="2ab58-222">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="2ab58-222">minOccurs="0" maxOccurs="1"</span></span> |[<span data-ttu-id="2ab58-223">StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="2ab58-223">StreamDispositionType</span></span>](media-services-input-metadata-schema.md#StreamDispositionType) |<span data-ttu-id="2ab58-224">Contém informações de apresentação (por exemplo, se uma determinada faixa de áudio for para usuários com deficiência visual).</span><span class="sxs-lookup"><span data-stu-id="2ab58-224">Contains presentation information (for example, whether a particular audio track is for visually impaired viewers).</span></span> |
| <span data-ttu-id="2ab58-225">**Metadados**</span><span class="sxs-lookup"><span data-stu-id="2ab58-225">**Metadata**</span></span><br /><br /> <span data-ttu-id="2ab58-226">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="2ab58-226">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="2ab58-227">MetadataType</span><span class="sxs-lookup"><span data-stu-id="2ab58-227">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="2ab58-228">Cadeias de caracteres de chave/valor genérico que podem ser usado toohold uma variedade de informações.</span><span class="sxs-lookup"><span data-stu-id="2ab58-228">Generic key/value strings that can be used toohold a variety of information.</span></span> <span data-ttu-id="2ab58-229">Por exemplo, key=”language” e value=”eng”.</span><span class="sxs-lookup"><span data-stu-id="2ab58-229">For example, key=”language”, and value=”eng”.</span></span> |

## <span data-ttu-id="2ab58-230"><a name="AudioTrackType"></a> AudioTrackType (herda de TrackType)</span><span class="sxs-lookup"><span data-stu-id="2ab58-230"><a name="AudioTrackType"></a> AudioTrackType (inherits from TrackType)</span></span>
 <span data-ttu-id="2ab58-231">**AudioTrackType** é um tipo complexo global que herda de [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="2ab58-231">**AudioTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

 <span data-ttu-id="2ab58-232">tipo de saudação representa uma faixa de áudio específica no arquivo de ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab58-232">hello type represents a specific audio track in hello asset file.</span></span>  

 <span data-ttu-id="2ab58-233">Veja um exemplo XML no final deste tópico Olá: [exemplo XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="2ab58-233">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="2ab58-234">Atributos</span><span class="sxs-lookup"><span data-stu-id="2ab58-234">Attributes</span></span>
| <span data-ttu-id="2ab58-235">Nome</span><span class="sxs-lookup"><span data-stu-id="2ab58-235">Name</span></span> | <span data-ttu-id="2ab58-236">Tipo</span><span class="sxs-lookup"><span data-stu-id="2ab58-236">Type</span></span> | <span data-ttu-id="2ab58-237">Descrição</span><span class="sxs-lookup"><span data-stu-id="2ab58-237">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ab58-238">**SampleFormat**</span><span class="sxs-lookup"><span data-stu-id="2ab58-238">**SampleFormat**</span></span> |<span data-ttu-id="2ab58-239">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2ab58-239">**xs:string**</span></span> |<span data-ttu-id="2ab58-240">Formato de exemplo.</span><span class="sxs-lookup"><span data-stu-id="2ab58-240">Sample format.</span></span> |
| <span data-ttu-id="2ab58-241">**ChannelLayout**</span><span class="sxs-lookup"><span data-stu-id="2ab58-241">**ChannelLayout**</span></span> |<span data-ttu-id="2ab58-242">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2ab58-242">**xs:string**</span></span> |<span data-ttu-id="2ab58-243">Layout do canal.</span><span class="sxs-lookup"><span data-stu-id="2ab58-243">Channel layout.</span></span> |
| <span data-ttu-id="2ab58-244">**Canais**</span><span class="sxs-lookup"><span data-stu-id="2ab58-244">**Channels**</span></span><br /><br /> <span data-ttu-id="2ab58-245">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-245">Required</span></span> |<span data-ttu-id="2ab58-246">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-246">**xs:int**</span></span> |<span data-ttu-id="2ab58-247">Número (0 ou mais) de canais de áudio.</span><span class="sxs-lookup"><span data-stu-id="2ab58-247">Number (0 or more) of audio channels.</span></span> |
| <span data-ttu-id="2ab58-248">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="2ab58-248">**SamplingRate**</span></span><br /><br /> <span data-ttu-id="2ab58-249">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-249">Required</span></span> |<span data-ttu-id="2ab58-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-250">**xs:int**</span></span> |<span data-ttu-id="2ab58-251">Taxa de amostragem de áudio em amostras/s ou Hz.</span><span class="sxs-lookup"><span data-stu-id="2ab58-251">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="2ab58-252">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="2ab58-252">**Bitrate**</span></span> |<span data-ttu-id="2ab58-253">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-253">**xs:int**</span></span> |<span data-ttu-id="2ab58-254">Taxa média de bits de áudio em bits por segundo, calculada a partir do arquivo de ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab58-254">Average audio bit rate in bits per second, as calculated from hello asset file.</span></span> <span data-ttu-id="2ab58-255">Somente Olá corrente de carga elementar é contada e sobrecarga de embalagem Olá não está incluída nesta contagem.</span><span class="sxs-lookup"><span data-stu-id="2ab58-255">Only hello elementary stream payload is counted, and hello packaging overhead is not included in this count.</span></span> |
| <span data-ttu-id="2ab58-256">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="2ab58-256">**BitsPerSample**</span></span> |<span data-ttu-id="2ab58-257">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-257">**xs:int**</span></span> |<span data-ttu-id="2ab58-258">Bits por amostra para o formato wFormatTag Olá tipo.</span><span class="sxs-lookup"><span data-stu-id="2ab58-258">Bits per sample for hello wFormatTag format type.</span></span> |

## <span data-ttu-id="2ab58-259"><a name="VideoTrackType"></a> VideoTrackType (herda de TrackType)</span><span class="sxs-lookup"><span data-stu-id="2ab58-259"><a name="VideoTrackType"></a> VideoTrackType (inherits from TrackType)</span></span>
<span data-ttu-id="2ab58-260">**VideoTrackType** é um tipo complexo global que herda de [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="2ab58-260">**VideoTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

<span data-ttu-id="2ab58-261">tipo de saudação representa uma faixa de vídeo específica no arquivo de ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab58-261">hello type represents a specific video track in hello asset file.</span></span>  

<span data-ttu-id="2ab58-262">Veja um exemplo XML no final deste tópico Olá: [exemplo XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="2ab58-262">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="2ab58-263">Atributos</span><span class="sxs-lookup"><span data-stu-id="2ab58-263">Attributes</span></span>
| <span data-ttu-id="2ab58-264">Nome</span><span class="sxs-lookup"><span data-stu-id="2ab58-264">Name</span></span> | <span data-ttu-id="2ab58-265">Tipo</span><span class="sxs-lookup"><span data-stu-id="2ab58-265">Type</span></span> | <span data-ttu-id="2ab58-266">Descrição</span><span class="sxs-lookup"><span data-stu-id="2ab58-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ab58-267">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="2ab58-267">**FourCC**</span></span><br /><br /> <span data-ttu-id="2ab58-268">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-268">Required</span></span> |<span data-ttu-id="2ab58-269">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2ab58-269">**xs:string**</span></span> |<span data-ttu-id="2ab58-270">Código FourCC de codec de vídeo.</span><span class="sxs-lookup"><span data-stu-id="2ab58-270">Video codec FourCC code.</span></span> |
| <span data-ttu-id="2ab58-271">**Perfil**</span><span class="sxs-lookup"><span data-stu-id="2ab58-271">**Profile**</span></span> |<span data-ttu-id="2ab58-272">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2ab58-272">**xs:string**</span></span> |<span data-ttu-id="2ab58-273">Perfil da faixa de vídeo.</span><span class="sxs-lookup"><span data-stu-id="2ab58-273">Video track's profile.</span></span> |
| <span data-ttu-id="2ab58-274">**Nível**</span><span class="sxs-lookup"><span data-stu-id="2ab58-274">**Level**</span></span> |<span data-ttu-id="2ab58-275">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2ab58-275">**xs:string**</span></span> |<span data-ttu-id="2ab58-276">Nível da faixa de vídeo.</span><span class="sxs-lookup"><span data-stu-id="2ab58-276">Video track's level.</span></span> |
| <span data-ttu-id="2ab58-277">**PixelFormat**</span><span class="sxs-lookup"><span data-stu-id="2ab58-277">**PixelFormat**</span></span> |<span data-ttu-id="2ab58-278">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2ab58-278">**xs:string**</span></span> |<span data-ttu-id="2ab58-279">Formato de pixel da faixa de vídeo.</span><span class="sxs-lookup"><span data-stu-id="2ab58-279">Video track's pixel format.</span></span> |
| <span data-ttu-id="2ab58-280">**Largura**</span><span class="sxs-lookup"><span data-stu-id="2ab58-280">**Width**</span></span><br /><br /> <span data-ttu-id="2ab58-281">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-281">Required</span></span> |<span data-ttu-id="2ab58-282">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-282">**xs:int**</span></span> |<span data-ttu-id="2ab58-283">Largura do vídeo codificado em pixels.</span><span class="sxs-lookup"><span data-stu-id="2ab58-283">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="2ab58-284">**Altura**</span><span class="sxs-lookup"><span data-stu-id="2ab58-284">**Height**</span></span><br /><br /> <span data-ttu-id="2ab58-285">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-285">Required</span></span> |<span data-ttu-id="2ab58-286">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-286">**xs:int**</span></span> |<span data-ttu-id="2ab58-287">Altura do vídeo codificado em pixels.</span><span class="sxs-lookup"><span data-stu-id="2ab58-287">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="2ab58-288">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="2ab58-288">**DisplayAspectRatioNumerator**</span></span><br /><br /> <span data-ttu-id="2ab58-289">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-289">Required</span></span> |<span data-ttu-id="2ab58-290">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="2ab58-290">**xs:double**</span></span> |<span data-ttu-id="2ab58-291">Numerador de taxa de proporção de exibição do vídeo.</span><span class="sxs-lookup"><span data-stu-id="2ab58-291">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="2ab58-292">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="2ab58-292">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="2ab58-293">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-293">Required</span></span> |<span data-ttu-id="2ab58-294">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="2ab58-294">**xs:double**</span></span> |<span data-ttu-id="2ab58-295">Denominador de taxa de proporção de exibição do vídeo.</span><span class="sxs-lookup"><span data-stu-id="2ab58-295">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="2ab58-296">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="2ab58-296">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="2ab58-297">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-297">Required</span></span> |<span data-ttu-id="2ab58-298">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="2ab58-298">**xs:double**</span></span> |<span data-ttu-id="2ab58-299">Numerador de proporção de amostra de vídeo.</span><span class="sxs-lookup"><span data-stu-id="2ab58-299">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="2ab58-300">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="2ab58-300">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="2ab58-301">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="2ab58-301">**xs:double**</span></span> |<span data-ttu-id="2ab58-302">Numerador de proporção de amostra de vídeo.</span><span class="sxs-lookup"><span data-stu-id="2ab58-302">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="2ab58-303">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="2ab58-303">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="2ab58-304">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="2ab58-304">**xs:double**</span></span> |<span data-ttu-id="2ab58-305">Denominador de proporção de amostra de vídeo.</span><span class="sxs-lookup"><span data-stu-id="2ab58-305">Video sample aspect ratio denominator.</span></span> |
| <span data-ttu-id="2ab58-306">**FrameRate**</span><span class="sxs-lookup"><span data-stu-id="2ab58-306">**FrameRate**</span></span><br /><br /> <span data-ttu-id="2ab58-307">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-307">Required</span></span> |<span data-ttu-id="2ab58-308">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="2ab58-308">**xs:decimal**</span></span> |<span data-ttu-id="2ab58-309">Medida de taxa de quadros de vídeo em formato .3f.</span><span class="sxs-lookup"><span data-stu-id="2ab58-309">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="2ab58-310">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="2ab58-310">**Bitrate**</span></span> |<span data-ttu-id="2ab58-311">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-311">**xs:int**</span></span> |<span data-ttu-id="2ab58-312">Taxa média de bits de vídeo em quilobits por segundo, calculada a partir do arquivo de ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab58-312">Average video bit rate in kilobits per second, as calculated from hello asset file.</span></span> <span data-ttu-id="2ab58-313">Somente Olá corrente de carga elementar é contada e não há sobrecarga de embalagem hello.</span><span class="sxs-lookup"><span data-stu-id="2ab58-313">Only hello elementary stream payload is counted, and hello packaging overhead is not included.</span></span> |
| <span data-ttu-id="2ab58-314">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="2ab58-314">**MaxGOPBitrate**</span></span> |<span data-ttu-id="2ab58-315">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-315">**xs:int**</span></span> |<span data-ttu-id="2ab58-316">Taxa de bits média do GOP máximo para esta faixa de vídeo em quilobits por segundo.</span><span class="sxs-lookup"><span data-stu-id="2ab58-316">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |
| <span data-ttu-id="2ab58-317">**HasBFrames**</span><span class="sxs-lookup"><span data-stu-id="2ab58-317">**HasBFrames**</span></span> |<span data-ttu-id="2ab58-318">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-318">**xs:int**</span></span> |<span data-ttu-id="2ab58-319">Número de faixas de vídeo de quadros B.</span><span class="sxs-lookup"><span data-stu-id="2ab58-319">Video track number of B frames.</span></span> |

## <span data-ttu-id="2ab58-320"><a name="MetadataType"></a> MetadataType</span><span class="sxs-lookup"><span data-stu-id="2ab58-320"><a name="MetadataType"></a> MetadataType</span></span>
<span data-ttu-id="2ab58-321">**MetadataType** é um tipo global complexo que descreve os metadados de um arquivo de ativo como cadeias de caracteres de chave/valor.</span><span class="sxs-lookup"><span data-stu-id="2ab58-321">**MetadataType** is a global complex type that describes metadata of an asset file as key/value strings.</span></span> <span data-ttu-id="2ab58-322">Por exemplo, key=”language” e value=”eng”.</span><span class="sxs-lookup"><span data-stu-id="2ab58-322">For example, key=”language”, and value=”eng”.</span></span>  

<span data-ttu-id="2ab58-323">Veja um exemplo XML no final deste tópico Olá: [exemplo XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="2ab58-323">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="2ab58-324">Atributos</span><span class="sxs-lookup"><span data-stu-id="2ab58-324">Attributes</span></span>
| <span data-ttu-id="2ab58-325">Nome</span><span class="sxs-lookup"><span data-stu-id="2ab58-325">Name</span></span> | <span data-ttu-id="2ab58-326">Tipo</span><span class="sxs-lookup"><span data-stu-id="2ab58-326">Type</span></span> | <span data-ttu-id="2ab58-327">Descrição</span><span class="sxs-lookup"><span data-stu-id="2ab58-327">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ab58-328">**chave**</span><span class="sxs-lookup"><span data-stu-id="2ab58-328">**key**</span></span><br /><br /> <span data-ttu-id="2ab58-329">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-329">Required</span></span> |<span data-ttu-id="2ab58-330">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2ab58-330">**xs:string**</span></span> |<span data-ttu-id="2ab58-331">chave de saudação no par chave/valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab58-331">hello key in hello key/value pair.</span></span> |
| <span data-ttu-id="2ab58-332">**valor**</span><span class="sxs-lookup"><span data-stu-id="2ab58-332">**value**</span></span><br /><br /> <span data-ttu-id="2ab58-333">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-333">Required</span></span> |<span data-ttu-id="2ab58-334">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2ab58-334">**xs:string**</span></span> |<span data-ttu-id="2ab58-335">valor de saudação no par chave/valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab58-335">hello value in hello key/value pair.</span></span> |

## <span data-ttu-id="2ab58-336"><a name="ProgramType"></a> ProgramType</span><span class="sxs-lookup"><span data-stu-id="2ab58-336"><a name="ProgramType"></a> ProgramType</span></span>
<span data-ttu-id="2ab58-337">**ProgramType** é um tipo global complexo que descreve um programa.</span><span class="sxs-lookup"><span data-stu-id="2ab58-337">**ProgramType** is a global complex type that describes a program.</span></span>  

### <a name="attributes"></a><span data-ttu-id="2ab58-338">Atributos</span><span class="sxs-lookup"><span data-stu-id="2ab58-338">Attributes</span></span>
| <span data-ttu-id="2ab58-339">Nome</span><span class="sxs-lookup"><span data-stu-id="2ab58-339">Name</span></span> | <span data-ttu-id="2ab58-340">Tipo</span><span class="sxs-lookup"><span data-stu-id="2ab58-340">Type</span></span> | <span data-ttu-id="2ab58-341">Descrição</span><span class="sxs-lookup"><span data-stu-id="2ab58-341">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ab58-342">**ProgramId**</span><span class="sxs-lookup"><span data-stu-id="2ab58-342">**ProgramId**</span></span><br /><br /> <span data-ttu-id="2ab58-343">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-343">Required</span></span> |<span data-ttu-id="2ab58-344">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-344">**xs:int**</span></span> |<span data-ttu-id="2ab58-345">Id do Programa</span><span class="sxs-lookup"><span data-stu-id="2ab58-345">Program Id</span></span> |
| <span data-ttu-id="2ab58-346">**NumberOfPrograms**</span><span class="sxs-lookup"><span data-stu-id="2ab58-346">**NumberOfPrograms**</span></span><br /><br /> <span data-ttu-id="2ab58-347">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-347">Required</span></span> |<span data-ttu-id="2ab58-348">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-348">**xs:int**</span></span> |<span data-ttu-id="2ab58-349">Número de programas.</span><span class="sxs-lookup"><span data-stu-id="2ab58-349">Number of programs.</span></span> |
| <span data-ttu-id="2ab58-350">**PmtPid**</span><span class="sxs-lookup"><span data-stu-id="2ab58-350">**PmtPid**</span></span><br /><br /> <span data-ttu-id="2ab58-351">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-351">Required</span></span> |<span data-ttu-id="2ab58-352">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-352">**xs:int**</span></span> |<span data-ttu-id="2ab58-353">As PMTs (Tabelas de Mapa de Programa) contêm informações sobre programas.</span><span class="sxs-lookup"><span data-stu-id="2ab58-353">Program Map Tables (PMTs) contain information about programs.</span></span>  <span data-ttu-id="2ab58-354">Para saber mais, confira [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span><span class="sxs-lookup"><span data-stu-id="2ab58-354">For more information, see [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span></span> |
| <span data-ttu-id="2ab58-355">**PcrPid**</span><span class="sxs-lookup"><span data-stu-id="2ab58-355">**PcrPid**</span></span><br /><br /> <span data-ttu-id="2ab58-356">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-356">Required</span></span> |<span data-ttu-id="2ab58-357">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-357">**xs:int**</span></span> |<span data-ttu-id="2ab58-358">Usado pelo decodificador.</span><span class="sxs-lookup"><span data-stu-id="2ab58-358">Used by decoder.</span></span> <span data-ttu-id="2ab58-359">Para saber mais, confira [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span><span class="sxs-lookup"><span data-stu-id="2ab58-359">For more information, see [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span></span> |
| <span data-ttu-id="2ab58-360">**StartPTS**</span><span class="sxs-lookup"><span data-stu-id="2ab58-360">**StartPTS**</span></span> |<span data-ttu-id="2ab58-361">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="2ab58-361">**xs: long**</span></span> |<span data-ttu-id="2ab58-362">Iniciando o carimbo de data/hora de apresentação.</span><span class="sxs-lookup"><span data-stu-id="2ab58-362">Starting presentation time stamp.</span></span> |
| <span data-ttu-id="2ab58-363">**EndPTS**</span><span class="sxs-lookup"><span data-stu-id="2ab58-363">**EndPTS**</span></span> |<span data-ttu-id="2ab58-364">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="2ab58-364">**xs: long**</span></span> |<span data-ttu-id="2ab58-365">Hora de término do carimbo de data/hora de apresentação.</span><span class="sxs-lookup"><span data-stu-id="2ab58-365">Ending presentation time stamp.</span></span> |

## <span data-ttu-id="2ab58-366"><a name="StreamDispositionType"></a> StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="2ab58-366"><a name="StreamDispositionType"></a> StreamDispositionType</span></span>
<span data-ttu-id="2ab58-367">**StreamDispositionType** é um tipo de complexo global que descreve o fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab58-367">**StreamDispositionType** is a global complex type that describes hello stream.</span></span>  

<span data-ttu-id="2ab58-368">Veja um exemplo XML no final deste tópico Olá: [exemplo XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="2ab58-368">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="2ab58-369">Atributos</span><span class="sxs-lookup"><span data-stu-id="2ab58-369">Attributes</span></span>
| <span data-ttu-id="2ab58-370">Nome</span><span class="sxs-lookup"><span data-stu-id="2ab58-370">Name</span></span> | <span data-ttu-id="2ab58-371">Tipo</span><span class="sxs-lookup"><span data-stu-id="2ab58-371">Type</span></span> | <span data-ttu-id="2ab58-372">Descrição</span><span class="sxs-lookup"><span data-stu-id="2ab58-372">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ab58-373">**Padrão**</span><span class="sxs-lookup"><span data-stu-id="2ab58-373">**Default**</span></span><br /><br /> <span data-ttu-id="2ab58-374">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-374">Required</span></span> |<span data-ttu-id="2ab58-375">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-375">**xs:int**</span></span> |<span data-ttu-id="2ab58-376">Defina tooindicate de too1 este atributo trata de apresentação de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab58-376">Set this attribute too1 tooindicate this is hello default presentation.</span></span> |
| <span data-ttu-id="2ab58-377">**Dub**</span><span class="sxs-lookup"><span data-stu-id="2ab58-377">**Dub**</span></span><br /><br /> <span data-ttu-id="2ab58-378">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-378">Required</span></span> |<span data-ttu-id="2ab58-379">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-379">**xs:int**</span></span> |<span data-ttu-id="2ab58-380">Defina tooindicate de too1 esse atributo é Olá apelidado de apresentação.</span><span class="sxs-lookup"><span data-stu-id="2ab58-380">Set this attribute too1 tooindicate this is hello dubbed presentation.</span></span> |
| <span data-ttu-id="2ab58-381">**Original**</span><span class="sxs-lookup"><span data-stu-id="2ab58-381">**Original**</span></span><br /><br /> <span data-ttu-id="2ab58-382">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-382">Required</span></span> |<span data-ttu-id="2ab58-383">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-383">**xs:int**</span></span> |<span data-ttu-id="2ab58-384">Defina tooindicate de too1 este atributo trata apresentação original hello.</span><span class="sxs-lookup"><span data-stu-id="2ab58-384">Set this attribute too1 tooindicate this is hello original presentation.</span></span> |
| <span data-ttu-id="2ab58-385">**Comentário**</span><span class="sxs-lookup"><span data-stu-id="2ab58-385">**Comment**</span></span><br /><br /> <span data-ttu-id="2ab58-386">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-386">Required</span></span> |<span data-ttu-id="2ab58-387">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-387">**xs:int**</span></span> |<span data-ttu-id="2ab58-388">Defina este tooindicate too1 de atributo faixa contém comentários.</span><span class="sxs-lookup"><span data-stu-id="2ab58-388">Set this attribute too1 tooindicate this track contains commentary.</span></span> |
| <span data-ttu-id="2ab58-389">**Lyrics**</span><span class="sxs-lookup"><span data-stu-id="2ab58-389">**Lyrics**</span></span><br /><br /> <span data-ttu-id="2ab58-390">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-390">Required</span></span> |<span data-ttu-id="2ab58-391">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-391">**xs:int**</span></span> |<span data-ttu-id="2ab58-392">Defina este tooindicate too1 de atributo faixa contém letras.</span><span class="sxs-lookup"><span data-stu-id="2ab58-392">Set this attribute too1 tooindicate this track contains lyrics.</span></span> |
| <span data-ttu-id="2ab58-393">**Karaoke**</span><span class="sxs-lookup"><span data-stu-id="2ab58-393">**Karaoke**</span></span><br /><br /> <span data-ttu-id="2ab58-394">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-394">Required</span></span> |<span data-ttu-id="2ab58-395">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-395">**xs:int**</span></span> |<span data-ttu-id="2ab58-396">Defina este tooindicate too1 de atributo representa Olá faixa Karaoke (música de fundo, sem vocais).</span><span class="sxs-lookup"><span data-stu-id="2ab58-396">Set this attribute too1 tooindicate this represents hello karaoke track (background music, no vocals).</span></span> |
| <span data-ttu-id="2ab58-397">**Forced**</span><span class="sxs-lookup"><span data-stu-id="2ab58-397">**Forced**</span></span><br /><br /> <span data-ttu-id="2ab58-398">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-398">Required</span></span> |<span data-ttu-id="2ab58-399">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-399">**xs:int**</span></span> |<span data-ttu-id="2ab58-400">Defina tooindicate de too1 este atributo trata apresentação Olá forçado.</span><span class="sxs-lookup"><span data-stu-id="2ab58-400">Set this attribute too1 tooindicate this is hello forced presentation.</span></span> |
| <span data-ttu-id="2ab58-401">**HearingImpaired**</span><span class="sxs-lookup"><span data-stu-id="2ab58-401">**HearingImpaired**</span></span><br /><br /> <span data-ttu-id="2ab58-402">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-402">Required</span></span> |<span data-ttu-id="2ab58-403">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-403">**xs:int**</span></span> |<span data-ttu-id="2ab58-404">Defina este tooindicate too1 de atributo que esta faixa é para deficiência auditiva de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab58-404">Set this attribute too1 tooindicate this track is for hello hearing impaired.</span></span> |
| <span data-ttu-id="2ab58-405">**VisualImpaired**</span><span class="sxs-lookup"><span data-stu-id="2ab58-405">**VisualImpaired**</span></span><br /><br /> <span data-ttu-id="2ab58-406">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-406">Required</span></span> |<span data-ttu-id="2ab58-407">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-407">**xs:int**</span></span> |<span data-ttu-id="2ab58-408">Defina este tooindicate too1 de atributo que esta faixa é para Olá pessoas com deficiências visuais.</span><span class="sxs-lookup"><span data-stu-id="2ab58-408">Set this attribute too1 tooindicate this track is for hello visually impaired.</span></span> |
| <span data-ttu-id="2ab58-409">**CleanEffects**</span><span class="sxs-lookup"><span data-stu-id="2ab58-409">**CleanEffects**</span></span><br /><br /> <span data-ttu-id="2ab58-410">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-410">Required</span></span> |<span data-ttu-id="2ab58-411">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-411">**xs:int**</span></span> |<span data-ttu-id="2ab58-412">Defina este tooindicate too1 de atributo que esta faixa tem efeitos limpos.</span><span class="sxs-lookup"><span data-stu-id="2ab58-412">Set this attribute too1 tooindicate this track has clean effects.</span></span> |
| <span data-ttu-id="2ab58-413">**AttachedPic**</span><span class="sxs-lookup"><span data-stu-id="2ab58-413">**AttachedPic**</span></span><br /><br /> <span data-ttu-id="2ab58-414">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2ab58-414">Required</span></span> |<span data-ttu-id="2ab58-415">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2ab58-415">**xs:int**</span></span> |<span data-ttu-id="2ab58-416">Defina este tooindicate too1 de atributo que esta faixa contém imagens.</span><span class="sxs-lookup"><span data-stu-id="2ab58-416">Set this attribute too1 tooindicate this track has pictures.</span></span> |

## <span data-ttu-id="2ab58-417"><a name="Programs"></a> Elemento Programs</span><span class="sxs-lookup"><span data-stu-id="2ab58-417"><a name="Programs"></a> Programs element</span></span>
<span data-ttu-id="2ab58-418">Elemento de wrapper que contém vários elementos **Program**.</span><span class="sxs-lookup"><span data-stu-id="2ab58-418">Wrapper element holding multiple **Program** elements.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="2ab58-419">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="2ab58-419">Child elements</span></span>
| <span data-ttu-id="2ab58-420">Nome</span><span class="sxs-lookup"><span data-stu-id="2ab58-420">Name</span></span> | <span data-ttu-id="2ab58-421">Tipo</span><span class="sxs-lookup"><span data-stu-id="2ab58-421">Type</span></span> | <span data-ttu-id="2ab58-422">Descrição</span><span class="sxs-lookup"><span data-stu-id="2ab58-422">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ab58-423">**Programa**</span><span class="sxs-lookup"><span data-stu-id="2ab58-423">**Program**</span></span><br /><br /> <span data-ttu-id="2ab58-424">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="2ab58-424">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="2ab58-425">ProgramType</span><span class="sxs-lookup"><span data-stu-id="2ab58-425">ProgramType</span></span>](media-services-input-metadata-schema.md#ProgramType) |<span data-ttu-id="2ab58-426">Para arquivos de ativos que estão no formato MPEG-TS, contém informações sobre programas no arquivo de ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab58-426">For asset files that are in MPEG-TS format, contains information about programs in hello asset file.</span></span> |

## <span data-ttu-id="2ab58-427"><a name="VideoTracks"></a> Elemento VideoTracks</span><span class="sxs-lookup"><span data-stu-id="2ab58-427"><a name="VideoTracks"></a> VideoTracks element</span></span>
 <span data-ttu-id="2ab58-428">Elemento de wrapper que contém vários elementos **VideoTrack**.</span><span class="sxs-lookup"><span data-stu-id="2ab58-428">Wrapper element holding multiple **VideoTrack** elements.</span></span>  

 <span data-ttu-id="2ab58-429">Veja um exemplo XML no final deste tópico Olá: [exemplo XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="2ab58-429">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="2ab58-430">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="2ab58-430">Child elements</span></span>
| <span data-ttu-id="2ab58-431">Nome</span><span class="sxs-lookup"><span data-stu-id="2ab58-431">Name</span></span> | <span data-ttu-id="2ab58-432">Tipo</span><span class="sxs-lookup"><span data-stu-id="2ab58-432">Type</span></span> | <span data-ttu-id="2ab58-433">Descrição</span><span class="sxs-lookup"><span data-stu-id="2ab58-433">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ab58-434">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="2ab58-434">**VideoTrack**</span></span><br /><br /> <span data-ttu-id="2ab58-435">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="2ab58-435">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="2ab58-436">VideoTrackType (herdado de TrackType)</span><span class="sxs-lookup"><span data-stu-id="2ab58-436">VideoTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#VideoTrackType) |<span data-ttu-id="2ab58-437">Contém informações sobre as faixas de vídeos no arquivo de ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab58-437">Contains information about video tracks in hello asset file.</span></span> |

## <span data-ttu-id="2ab58-438"><a name="AudioTracks"></a> Elemento AudioTracks</span><span class="sxs-lookup"><span data-stu-id="2ab58-438"><a name="AudioTracks"></a> AudioTracks element</span></span>
 <span data-ttu-id="2ab58-439">Elemento de wrapper que contém vários elementos **AudioTrack**.</span><span class="sxs-lookup"><span data-stu-id="2ab58-439">Wrapper element holding multiple **AudioTrack** elements.</span></span>  

 <span data-ttu-id="2ab58-440">Veja um exemplo XML no final deste tópico Olá: [exemplo XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="2ab58-440">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="elements"></a><span data-ttu-id="2ab58-441">elementos</span><span class="sxs-lookup"><span data-stu-id="2ab58-441">elements</span></span>
| <span data-ttu-id="2ab58-442">Nome</span><span class="sxs-lookup"><span data-stu-id="2ab58-442">Name</span></span> | <span data-ttu-id="2ab58-443">Tipo</span><span class="sxs-lookup"><span data-stu-id="2ab58-443">Type</span></span> | <span data-ttu-id="2ab58-444">Descrição</span><span class="sxs-lookup"><span data-stu-id="2ab58-444">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ab58-445">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="2ab58-445">**AudioTrack**</span></span><br /><br /> <span data-ttu-id="2ab58-446">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="2ab58-446">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="2ab58-447">AudioTrackType (herdado de TrackType)</span><span class="sxs-lookup"><span data-stu-id="2ab58-447">AudioTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#AudioTrackType) |<span data-ttu-id="2ab58-448">Contém informações sobre as faixas de áudio no arquivo de ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab58-448">Contains information about audio tracks in hello asset file.</span></span> |

## <span data-ttu-id="2ab58-449"><a name="code"></a> Código de Esquema</span><span class="sxs-lookup"><span data-stu-id="2ab58-449"><a name="code"></a> Schema Code</span></span>
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


## <span data-ttu-id="2ab58-450"><a name="xml"></a> Exemplo de XML</span><span class="sxs-lookup"><span data-stu-id="2ab58-450"><a name="xml"></a> XML example</span></span>
<span data-ttu-id="2ab58-451">a seguir Olá é um exemplo de arquivo de metadados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="2ab58-451">hello following is an example of hello Input metadata file.</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="2ab58-452">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2ab58-452">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2ab58-453">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="2ab58-453">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

