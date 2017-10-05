---
title: "Esquema de metadados de entrada dos Serviços de Mídia do Azure | Microsoft Docs"
description: "O tópico oferece uma visão geral do estema de metadados de entrada dos Serviços de Mídia do Azure."
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
ms.openlocfilehash: 4787e4033e1afda6339b0b917263ecc165e400ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="input-metadata"></a><span data-ttu-id="71312-103">Metadados de entrada</span><span class="sxs-lookup"><span data-stu-id="71312-103">Input Metadata</span></span>
<span data-ttu-id="71312-104">Um trabalho de codificação é associado um ativo (ou ativos) de entrada no qual você deseja executar algumas tarefas de codificação.</span><span class="sxs-lookup"><span data-stu-id="71312-104">An encoding job is associated with an input asset (or assets) on which you want to perform some encoding tasks.</span></span>  <span data-ttu-id="71312-105">Após a conclusão de uma tarefa, um ativo de saída é produzido.</span><span class="sxs-lookup"><span data-stu-id="71312-105">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="71312-106">O ativo de saída contém vídeo, áudio, miniaturas, manifesto etc. O ativo de saída também contém um arquivo com metadados sobre o ativo de entrada.</span><span class="sxs-lookup"><span data-stu-id="71312-106">The output asset contains video, audio, thumbnails, manifest, etc. The output asset also contains a file with metadata about the input asset.</span></span> <span data-ttu-id="71312-107">O nome do arquivo XML de metadados tem o seguinte formato: &lt;asset_id&gt;_metadata.xml (por exemplo, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), onde &lt;asset_id&gt; é o valor de AssetId do ativo de entrada.</span><span class="sxs-lookup"><span data-stu-id="71312-107">The name of the metadata XML file has the following format: &lt;asset_id&gt;_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where &lt;asset_id&gt; is the AssetId value of the input asset.</span></span>  

<span data-ttu-id="71312-108">Se desejar examinar o arquivo de metadados, você poderá criar um localizador **SAS** e baixar o arquivo em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="71312-108">If you want to examine the metadata file, you can create a **SAS** locator and download the file to your local computer.</span></span> <span data-ttu-id="71312-109">É possível encontrar um exemplo de como criar um localizador SAS e baixar um arquivo em [Usando as Extensões do SDK do .NET para os Serviços de Mídia](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="71312-109">You can find an example on how to create a SAS locator and download a file  [Using the Media Services .NET SDK Extensions](media-services-dotnet-get-started.md).</span></span>  

<span data-ttu-id="71312-110">Este tópico discute os elementos e os tipos do esquema XML no qual os metadados de entrada (&lt;asset_id&gt;_metadata.xml) se baseiam.</span><span class="sxs-lookup"><span data-stu-id="71312-110">This topic discusses the elements and types of the XML schema on which the input metada (&lt;asset_id&gt;_metadata.xml) is based.</span></span>  <span data-ttu-id="71312-111">Para saber mais sobre o arquivo que contém metadados sobre o ativo de saída, veja [Metadados de saída](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="71312-111">For information about the file that contains metadata about the output asset, see [Output Metadata](media-services-output-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="71312-112">Você pode encontrar o [Código de Esquema](media-services-input-metadata-schema.md#code) e um [Exemplo de XML](media-services-input-metadata-schema.md#xml) no final deste tópico.</span><span class="sxs-lookup"><span data-stu-id="71312-112">You can find the [Schema Code](media-services-input-metadata-schema.md#code) an [XML example](media-services-input-metadata-schema.md#xml) at the end of this topic.</span></span>  
> 
> 

## <span data-ttu-id="71312-113"><a name="AssetFiles"></a> Elemento AssetFiles (elemento raiz)</span><span class="sxs-lookup"><span data-stu-id="71312-113"><a name="AssetFiles"></a> AssetFiles element (root element)</span></span>
<span data-ttu-id="71312-114">Contém uma coleção de [elementos AssetFile](media-services-input-metadata-schema.md#AssetFile) para o trabalho de codificação.</span><span class="sxs-lookup"><span data-stu-id="71312-114">Contains a collection of [AssetFile element](media-services-input-metadata-schema.md#AssetFile)s for the encoding job.</span></span>  

<span data-ttu-id="71312-115">Veja um exemplo de XML no final deste tópico: [Exemplo de XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="71312-115">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

| <span data-ttu-id="71312-116">Nome</span><span class="sxs-lookup"><span data-stu-id="71312-116">Name</span></span> | <span data-ttu-id="71312-117">Descrição</span><span class="sxs-lookup"><span data-stu-id="71312-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="71312-118">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="71312-118">**AssetFile**</span></span><br /><br /> <span data-ttu-id="71312-119">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="71312-119">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="71312-120">Um único elemento filho.</span><span class="sxs-lookup"><span data-stu-id="71312-120">A single child element.</span></span> <span data-ttu-id="71312-121">Para saber mais, veja [Elemento AssetFile](media-services-input-metadata-schema.md#AssetFile).</span><span class="sxs-lookup"><span data-stu-id="71312-121">For more information, see [AssetFile element](media-services-input-metadata-schema.md#AssetFile).</span></span> |

## <span data-ttu-id="71312-122"><a name="AssetFile"></a> Elemento AssetFile</span><span class="sxs-lookup"><span data-stu-id="71312-122"><a name="AssetFile"></a> AssetFile element</span></span>
 <span data-ttu-id="71312-123">Contém atributos e elementos que descrevem um arquivo de ativo.</span><span class="sxs-lookup"><span data-stu-id="71312-123">Contains attributes and elements that describe an asset file.</span></span>  

 <span data-ttu-id="71312-124">Veja um exemplo de XML no final deste tópico: [Exemplo de XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="71312-124">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="71312-125">Atributos</span><span class="sxs-lookup"><span data-stu-id="71312-125">Attributes</span></span>
| <span data-ttu-id="71312-126">Nome</span><span class="sxs-lookup"><span data-stu-id="71312-126">Name</span></span> | <span data-ttu-id="71312-127">Tipo</span><span class="sxs-lookup"><span data-stu-id="71312-127">Type</span></span> | <span data-ttu-id="71312-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="71312-128">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="71312-129">**Nome**</span><span class="sxs-lookup"><span data-stu-id="71312-129">**Name**</span></span><br /><br /> <span data-ttu-id="71312-130">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-130">Required</span></span> |<span data-ttu-id="71312-131">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="71312-131">**xs:string**</span></span> |<span data-ttu-id="71312-132">Nome do arquivo de ativo.</span><span class="sxs-lookup"><span data-stu-id="71312-132">Asset file name.</span></span> |
| <span data-ttu-id="71312-133">**Tamanho**</span><span class="sxs-lookup"><span data-stu-id="71312-133">**Size**</span></span><br /><br /> <span data-ttu-id="71312-134">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-134">Required</span></span> |<span data-ttu-id="71312-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="71312-135">**xs:long**</span></span> |<span data-ttu-id="71312-136">Tamanho do arquivo de ativo em bytes.</span><span class="sxs-lookup"><span data-stu-id="71312-136">Size of the asset file in bytes.</span></span> |
| <span data-ttu-id="71312-137">**Duração**</span><span class="sxs-lookup"><span data-stu-id="71312-137">**Duration**</span></span><br /><br /> <span data-ttu-id="71312-138">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-138">Required</span></span> |<span data-ttu-id="71312-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="71312-139">**xs:duration**</span></span> |<span data-ttu-id="71312-140">Duração da reprodução de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="71312-140">Content play back duration.</span></span> <span data-ttu-id="71312-141">Exemplo: Duration="PT25M37.757S".</span><span class="sxs-lookup"><span data-stu-id="71312-141">Example: Duration="PT25M37.757S".</span></span> |
| <span data-ttu-id="71312-142">**NumberOfStreams**</span><span class="sxs-lookup"><span data-stu-id="71312-142">**NumberOfStreams**</span></span><br /><br /> <span data-ttu-id="71312-143">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-143">Required</span></span> |<span data-ttu-id="71312-144">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-144">**xs:int**</span></span> |<span data-ttu-id="71312-145">Número de fluxos no arquivo de ativo.</span><span class="sxs-lookup"><span data-stu-id="71312-145">Number of streams in the asset file.</span></span> |
| <span data-ttu-id="71312-146">**FormatNames**</span><span class="sxs-lookup"><span data-stu-id="71312-146">**FormatNames**</span></span><br /><br /> <span data-ttu-id="71312-147">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-147">Required</span></span> |<span data-ttu-id="71312-148">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="71312-148">**xs:string**</span></span> |<span data-ttu-id="71312-149">Nomes de formato.</span><span class="sxs-lookup"><span data-stu-id="71312-149">Format names.</span></span> |
| <span data-ttu-id="71312-150">**FormatVerboseNames**</span><span class="sxs-lookup"><span data-stu-id="71312-150">**FormatVerboseNames**</span></span><br /><br /> <span data-ttu-id="71312-151">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-151">Required</span></span> |<span data-ttu-id="71312-152">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="71312-152">**xs:string**</span></span> |<span data-ttu-id="71312-153">Nomes detalhados de formato.</span><span class="sxs-lookup"><span data-stu-id="71312-153">Format verbose names.</span></span> |
| <span data-ttu-id="71312-154">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="71312-154">**StartTime**</span></span> |<span data-ttu-id="71312-155">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="71312-155">**xs:duration**</span></span> |<span data-ttu-id="71312-156">Hora de início do conteúdo.</span><span class="sxs-lookup"><span data-stu-id="71312-156">Content start time.</span></span> <span data-ttu-id="71312-157">Exemplo: StartTime = "PT2.669S".</span><span class="sxs-lookup"><span data-stu-id="71312-157">Example: StartTime="PT2.669S".</span></span> |
| <span data-ttu-id="71312-158">**OverallBitRate**</span><span class="sxs-lookup"><span data-stu-id="71312-158">**OverallBitRate**</span></span> |<span data-ttu-id="71312-159">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-159">**xs:int**</span></span> |<span data-ttu-id="71312-160">Taxa de bits média do arquivo de ativo em kbps.</span><span class="sxs-lookup"><span data-stu-id="71312-160">Average bitrate of the asset file in kbps.</span></span> |

> [!NOTE]
> <span data-ttu-id="71312-161">Os quatro elementos filhos a seguir devem aparecer em uma sequência.</span><span class="sxs-lookup"><span data-stu-id="71312-161">The following 4 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="71312-162">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="71312-162">Child elements</span></span>
| <span data-ttu-id="71312-163">Nome</span><span class="sxs-lookup"><span data-stu-id="71312-163">Name</span></span> | <span data-ttu-id="71312-164">Tipo</span><span class="sxs-lookup"><span data-stu-id="71312-164">Type</span></span> | <span data-ttu-id="71312-165">Descrição</span><span class="sxs-lookup"><span data-stu-id="71312-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="71312-166">**Programas**</span><span class="sxs-lookup"><span data-stu-id="71312-166">**Programs**</span></span><br /><br /> <span data-ttu-id="71312-167">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="71312-167">minOccurs="0"</span></span> | |<span data-ttu-id="71312-168">A coleção de todos os [elementos Programs](media-services-input-metadata-schema.md#Programs) quando o arquivo de ativo está no formato MPEG-TS.</span><span class="sxs-lookup"><span data-stu-id="71312-168">Collection of all [Programs element](media-services-input-metadata-schema.md#Programs) when the asset file is in MPEG-TS format.</span></span> |
| <span data-ttu-id="71312-169">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="71312-169">**VideoTracks**</span></span><br /><br /> <span data-ttu-id="71312-170">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="71312-170">minOccurs="0"</span></span> | |<span data-ttu-id="71312-171">Cada arquivo de ativo físico pode conter nenhuma ou mais faixas de vídeo intercaladas em um formato de contêiner apropriado.</span><span class="sxs-lookup"><span data-stu-id="71312-171">Each physical asset file can contain zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="71312-172">Esse elemento contém uma coleção de todos os [elementos VideoTracks](media-services-input-metadata-schema.md#VideoTracks) que fazem parte do arquivo de ativo.</span><span class="sxs-lookup"><span data-stu-id="71312-172">This element contains a collection of all [VideoTracks element](media-services-input-metadata-schema.md#VideoTracks) that are part of the asset file.</span></span> |
| <span data-ttu-id="71312-173">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="71312-173">**AudioTracks**</span></span><br /><br /> <span data-ttu-id="71312-174">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="71312-174">minOccurs="0"</span></span> | |<span data-ttu-id="71312-175">Cada arquivo de ativo físico pode conter nenhuma ou mais faixas de áudio intercaladas em um formato de contêiner apropriado.</span><span class="sxs-lookup"><span data-stu-id="71312-175">Each physical asset file can contain zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="71312-176">Esse elemento contém uma coleção de todos os [elementos AudioTracks](media-services-input-metadata-schema.md#AudioTracks) que fazem parte do arquivo de ativo.</span><span class="sxs-lookup"><span data-stu-id="71312-176">This element contains a collection of all [AudioTracks element](media-services-input-metadata-schema.md#AudioTracks) that are part of the asset file.</span></span> |
| <span data-ttu-id="71312-177">**Metadados**</span><span class="sxs-lookup"><span data-stu-id="71312-177">**Metadata**</span></span><br /><br /> <span data-ttu-id="71312-178">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="71312-178">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="71312-179">MetadataType</span><span class="sxs-lookup"><span data-stu-id="71312-179">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="71312-180">Metadados do arquivo de ativo representados como cadeias de caracteres de chave\valor.</span><span class="sxs-lookup"><span data-stu-id="71312-180">Asset file’s metadata represented as key\value strings.</span></span> <span data-ttu-id="71312-181">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="71312-181">For example:</span></span><br /><br /> <span data-ttu-id="71312-182">**&lt;Metadata key="language" value="eng" /&gt;**</span><span class="sxs-lookup"><span data-stu-id="71312-182">**&lt;Metadata key="language" value="eng" /&gt;**</span></span> |

## <span data-ttu-id="71312-183"><a name="TrackType"></a> TrackType</span><span class="sxs-lookup"><span data-stu-id="71312-183"><a name="TrackType"></a> TrackType</span></span>
<span data-ttu-id="71312-184">Veja um exemplo de XML no final deste tópico: [Exemplo de XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="71312-184">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="71312-185">Atributos</span><span class="sxs-lookup"><span data-stu-id="71312-185">Attributes</span></span>
| <span data-ttu-id="71312-186">Nome</span><span class="sxs-lookup"><span data-stu-id="71312-186">Name</span></span> | <span data-ttu-id="71312-187">Tipo</span><span class="sxs-lookup"><span data-stu-id="71312-187">Type</span></span> | <span data-ttu-id="71312-188">Descrição</span><span class="sxs-lookup"><span data-stu-id="71312-188">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="71312-189">**Id**</span><span class="sxs-lookup"><span data-stu-id="71312-189">**Id**</span></span><br /><br /> <span data-ttu-id="71312-190">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-190">Required</span></span> |<span data-ttu-id="71312-191">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-191">**xs:int**</span></span> |<span data-ttu-id="71312-192">Índice baseado em zero da faixa de áudio ou de vídeo.</span><span class="sxs-lookup"><span data-stu-id="71312-192">Zero-based index of this audio or video track.</span></span><br /><br /> <span data-ttu-id="71312-193">Essa não é necessariamente a TrackID como usada em um arquivo MP4.</span><span class="sxs-lookup"><span data-stu-id="71312-193">This is not necessarily that the TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="71312-194">**Codec**</span><span class="sxs-lookup"><span data-stu-id="71312-194">**Codec**</span></span> |<span data-ttu-id="71312-195">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="71312-195">**xs:string**</span></span> |<span data-ttu-id="71312-196">Cadeia de caracteres de codec de faixa de vídeo.</span><span class="sxs-lookup"><span data-stu-id="71312-196">Video track codec string.</span></span> |
| <span data-ttu-id="71312-197">**CodecLongName**</span><span class="sxs-lookup"><span data-stu-id="71312-197">**CodecLongName**</span></span> |<span data-ttu-id="71312-198">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="71312-198">**xs:string**</span></span> |<span data-ttu-id="71312-199">Nome longo de codec de faixa de áudio ou vídeo.</span><span class="sxs-lookup"><span data-stu-id="71312-199">Audio or video track codec long name.</span></span> |
| <span data-ttu-id="71312-200">**TimeBase**</span><span class="sxs-lookup"><span data-stu-id="71312-200">**TimeBase**</span></span><br /><br /> <span data-ttu-id="71312-201">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-201">Required</span></span> |<span data-ttu-id="71312-202">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="71312-202">**xs:string**</span></span> |<span data-ttu-id="71312-203">Base de tempo.</span><span class="sxs-lookup"><span data-stu-id="71312-203">Time base.</span></span> <span data-ttu-id="71312-204">Exemplo: TimeBase="1/48000"</span><span class="sxs-lookup"><span data-stu-id="71312-204">Example: TimeBase="1/48000"</span></span> |
| <span data-ttu-id="71312-205">**NumberOfFrames**</span><span class="sxs-lookup"><span data-stu-id="71312-205">**NumberOfFrames**</span></span> |<span data-ttu-id="71312-206">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-206">**xs:int**</span></span> |<span data-ttu-id="71312-207">Número de quadros (presentes em faixas de vídeo).</span><span class="sxs-lookup"><span data-stu-id="71312-207">Number of frames (present for video tracks).</span></span> |
| <span data-ttu-id="71312-208">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="71312-208">**StartTime**</span></span> |<span data-ttu-id="71312-209">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="71312-209">**xs:duration**</span></span> |<span data-ttu-id="71312-210">Hora de início da faixa.</span><span class="sxs-lookup"><span data-stu-id="71312-210">Track start time.</span></span> <span data-ttu-id="71312-211">Exemplo: StartTime="PT2.669S"</span><span class="sxs-lookup"><span data-stu-id="71312-211">Example: StartTime="PT2.669S"</span></span> |
| <span data-ttu-id="71312-212">**Duração**</span><span class="sxs-lookup"><span data-stu-id="71312-212">**Duration**</span></span> |<span data-ttu-id="71312-213">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="71312-213">**xs:duration**</span></span> |<span data-ttu-id="71312-214">Duração da faixa.</span><span class="sxs-lookup"><span data-stu-id="71312-214">Track duration.</span></span> <span data-ttu-id="71312-215">Exemplo: Duration="PTSampleFormat M37.757S".</span><span class="sxs-lookup"><span data-stu-id="71312-215">Example: Duration="PTSampleFormat M37.757S".</span></span> |

> [!NOTE]
> <span data-ttu-id="71312-216">Os dois elementos filhos a seguir devem aparecer em uma sequência.</span><span class="sxs-lookup"><span data-stu-id="71312-216">The following 2 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="71312-217">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="71312-217">Child elements</span></span>
| <span data-ttu-id="71312-218">Nome</span><span class="sxs-lookup"><span data-stu-id="71312-218">Name</span></span> | <span data-ttu-id="71312-219">Tipo</span><span class="sxs-lookup"><span data-stu-id="71312-219">Type</span></span> | <span data-ttu-id="71312-220">Descrição</span><span class="sxs-lookup"><span data-stu-id="71312-220">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="71312-221">**Disposição**</span><span class="sxs-lookup"><span data-stu-id="71312-221">**Disposition**</span></span><br /><br /> <span data-ttu-id="71312-222">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="71312-222">minOccurs="0" maxOccurs="1"</span></span> |[<span data-ttu-id="71312-223">StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="71312-223">StreamDispositionType</span></span>](media-services-input-metadata-schema.md#StreamDispositionType) |<span data-ttu-id="71312-224">Contém informações de apresentação (por exemplo, se uma determinada faixa de áudio for para usuários com deficiência visual).</span><span class="sxs-lookup"><span data-stu-id="71312-224">Contains presentation information (for example, whether a particular audio track is for visually impaired viewers).</span></span> |
| <span data-ttu-id="71312-225">**Metadados**</span><span class="sxs-lookup"><span data-stu-id="71312-225">**Metadata**</span></span><br /><br /> <span data-ttu-id="71312-226">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="71312-226">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="71312-227">MetadataType</span><span class="sxs-lookup"><span data-stu-id="71312-227">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="71312-228">As cadeias de caracteres de chave/valor genéricas que podem ser usadas para armazenar uma variedade de informações.</span><span class="sxs-lookup"><span data-stu-id="71312-228">Generic key/value strings that can be used to hold a variety of information.</span></span> <span data-ttu-id="71312-229">Por exemplo, key=”language” e value=”eng”.</span><span class="sxs-lookup"><span data-stu-id="71312-229">For example, key=”language”, and value=”eng”.</span></span> |

## <span data-ttu-id="71312-230"><a name="AudioTrackType"></a> AudioTrackType (herda de TrackType)</span><span class="sxs-lookup"><span data-stu-id="71312-230"><a name="AudioTrackType"></a> AudioTrackType (inherits from TrackType)</span></span>
 <span data-ttu-id="71312-231">**AudioTrackType** é um tipo complexo global que herda de [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="71312-231">**AudioTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

 <span data-ttu-id="71312-232">O tipo representa uma faixa de áudio específica no arquivo de ativo.</span><span class="sxs-lookup"><span data-stu-id="71312-232">The type represents a specific audio track in the asset file.</span></span>  

 <span data-ttu-id="71312-233">Veja um exemplo de XML no final deste tópico: [Exemplo de XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="71312-233">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="71312-234">Atributos</span><span class="sxs-lookup"><span data-stu-id="71312-234">Attributes</span></span>
| <span data-ttu-id="71312-235">Nome</span><span class="sxs-lookup"><span data-stu-id="71312-235">Name</span></span> | <span data-ttu-id="71312-236">Tipo</span><span class="sxs-lookup"><span data-stu-id="71312-236">Type</span></span> | <span data-ttu-id="71312-237">Descrição</span><span class="sxs-lookup"><span data-stu-id="71312-237">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="71312-238">**SampleFormat**</span><span class="sxs-lookup"><span data-stu-id="71312-238">**SampleFormat**</span></span> |<span data-ttu-id="71312-239">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="71312-239">**xs:string**</span></span> |<span data-ttu-id="71312-240">Formato de exemplo.</span><span class="sxs-lookup"><span data-stu-id="71312-240">Sample format.</span></span> |
| <span data-ttu-id="71312-241">**ChannelLayout**</span><span class="sxs-lookup"><span data-stu-id="71312-241">**ChannelLayout**</span></span> |<span data-ttu-id="71312-242">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="71312-242">**xs:string**</span></span> |<span data-ttu-id="71312-243">Layout do canal.</span><span class="sxs-lookup"><span data-stu-id="71312-243">Channel layout.</span></span> |
| <span data-ttu-id="71312-244">**Canais**</span><span class="sxs-lookup"><span data-stu-id="71312-244">**Channels**</span></span><br /><br /> <span data-ttu-id="71312-245">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-245">Required</span></span> |<span data-ttu-id="71312-246">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-246">**xs:int**</span></span> |<span data-ttu-id="71312-247">Número (0 ou mais) de canais de áudio.</span><span class="sxs-lookup"><span data-stu-id="71312-247">Number (0 or more) of audio channels.</span></span> |
| <span data-ttu-id="71312-248">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="71312-248">**SamplingRate**</span></span><br /><br /> <span data-ttu-id="71312-249">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-249">Required</span></span> |<span data-ttu-id="71312-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-250">**xs:int**</span></span> |<span data-ttu-id="71312-251">Taxa de amostragem de áudio em amostras/s ou Hz.</span><span class="sxs-lookup"><span data-stu-id="71312-251">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="71312-252">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="71312-252">**Bitrate**</span></span> |<span data-ttu-id="71312-253">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-253">**xs:int**</span></span> |<span data-ttu-id="71312-254">Taxa média de bits de áudio em bits por segundo, calculada com base no arquivo de ativo.</span><span class="sxs-lookup"><span data-stu-id="71312-254">Average audio bit rate in bits per second, as calculated from the asset file.</span></span> <span data-ttu-id="71312-255">Apenas a carga de fluxo elementar é contada, e a sobrecarga de empacotamento não está incluída nesta contagem.</span><span class="sxs-lookup"><span data-stu-id="71312-255">Only the elementary stream payload is counted, and the packaging overhead is not included in this count.</span></span> |
| <span data-ttu-id="71312-256">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="71312-256">**BitsPerSample**</span></span> |<span data-ttu-id="71312-257">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-257">**xs:int**</span></span> |<span data-ttu-id="71312-258">Bits por amostra para o tipo de formato wFormatTag.</span><span class="sxs-lookup"><span data-stu-id="71312-258">Bits per sample for the wFormatTag format type.</span></span> |

## <span data-ttu-id="71312-259"><a name="VideoTrackType"></a> VideoTrackType (herda de TrackType)</span><span class="sxs-lookup"><span data-stu-id="71312-259"><a name="VideoTrackType"></a> VideoTrackType (inherits from TrackType)</span></span>
<span data-ttu-id="71312-260">**VideoTrackType** é um tipo complexo global que herda de [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="71312-260">**VideoTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

<span data-ttu-id="71312-261">O tipo representa uma faixa de vídeo específica no arquivo de ativo.</span><span class="sxs-lookup"><span data-stu-id="71312-261">The type represents a specific video track in the asset file.</span></span>  

<span data-ttu-id="71312-262">Veja um exemplo de XML no final deste tópico: [Exemplo de XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="71312-262">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="71312-263">Atributos</span><span class="sxs-lookup"><span data-stu-id="71312-263">Attributes</span></span>
| <span data-ttu-id="71312-264">Nome</span><span class="sxs-lookup"><span data-stu-id="71312-264">Name</span></span> | <span data-ttu-id="71312-265">Tipo</span><span class="sxs-lookup"><span data-stu-id="71312-265">Type</span></span> | <span data-ttu-id="71312-266">Descrição</span><span class="sxs-lookup"><span data-stu-id="71312-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="71312-267">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="71312-267">**FourCC**</span></span><br /><br /> <span data-ttu-id="71312-268">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-268">Required</span></span> |<span data-ttu-id="71312-269">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="71312-269">**xs:string**</span></span> |<span data-ttu-id="71312-270">Código FourCC de codec de vídeo.</span><span class="sxs-lookup"><span data-stu-id="71312-270">Video codec FourCC code.</span></span> |
| <span data-ttu-id="71312-271">**Perfil**</span><span class="sxs-lookup"><span data-stu-id="71312-271">**Profile**</span></span> |<span data-ttu-id="71312-272">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="71312-272">**xs:string**</span></span> |<span data-ttu-id="71312-273">Perfil da faixa de vídeo.</span><span class="sxs-lookup"><span data-stu-id="71312-273">Video track's profile.</span></span> |
| <span data-ttu-id="71312-274">**Nível**</span><span class="sxs-lookup"><span data-stu-id="71312-274">**Level**</span></span> |<span data-ttu-id="71312-275">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="71312-275">**xs:string**</span></span> |<span data-ttu-id="71312-276">Nível da faixa de vídeo.</span><span class="sxs-lookup"><span data-stu-id="71312-276">Video track's level.</span></span> |
| <span data-ttu-id="71312-277">**PixelFormat**</span><span class="sxs-lookup"><span data-stu-id="71312-277">**PixelFormat**</span></span> |<span data-ttu-id="71312-278">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="71312-278">**xs:string**</span></span> |<span data-ttu-id="71312-279">Formato de pixel da faixa de vídeo.</span><span class="sxs-lookup"><span data-stu-id="71312-279">Video track's pixel format.</span></span> |
| <span data-ttu-id="71312-280">**Largura**</span><span class="sxs-lookup"><span data-stu-id="71312-280">**Width**</span></span><br /><br /> <span data-ttu-id="71312-281">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-281">Required</span></span> |<span data-ttu-id="71312-282">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-282">**xs:int**</span></span> |<span data-ttu-id="71312-283">Largura do vídeo codificado em pixels.</span><span class="sxs-lookup"><span data-stu-id="71312-283">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="71312-284">**Altura**</span><span class="sxs-lookup"><span data-stu-id="71312-284">**Height**</span></span><br /><br /> <span data-ttu-id="71312-285">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-285">Required</span></span> |<span data-ttu-id="71312-286">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-286">**xs:int**</span></span> |<span data-ttu-id="71312-287">Altura do vídeo codificado em pixels.</span><span class="sxs-lookup"><span data-stu-id="71312-287">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="71312-288">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="71312-288">**DisplayAspectRatioNumerator**</span></span><br /><br /> <span data-ttu-id="71312-289">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-289">Required</span></span> |<span data-ttu-id="71312-290">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="71312-290">**xs:double**</span></span> |<span data-ttu-id="71312-291">Numerador de taxa de proporção de exibição do vídeo.</span><span class="sxs-lookup"><span data-stu-id="71312-291">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="71312-292">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="71312-292">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="71312-293">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-293">Required</span></span> |<span data-ttu-id="71312-294">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="71312-294">**xs:double**</span></span> |<span data-ttu-id="71312-295">Denominador de taxa de proporção de exibição do vídeo.</span><span class="sxs-lookup"><span data-stu-id="71312-295">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="71312-296">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="71312-296">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="71312-297">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-297">Required</span></span> |<span data-ttu-id="71312-298">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="71312-298">**xs:double**</span></span> |<span data-ttu-id="71312-299">Numerador de proporção de amostra de vídeo.</span><span class="sxs-lookup"><span data-stu-id="71312-299">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="71312-300">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="71312-300">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="71312-301">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="71312-301">**xs:double**</span></span> |<span data-ttu-id="71312-302">Numerador de proporção de amostra de vídeo.</span><span class="sxs-lookup"><span data-stu-id="71312-302">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="71312-303">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="71312-303">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="71312-304">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="71312-304">**xs:double**</span></span> |<span data-ttu-id="71312-305">Denominador de proporção de amostra de vídeo.</span><span class="sxs-lookup"><span data-stu-id="71312-305">Video sample aspect ratio denominator.</span></span> |
| <span data-ttu-id="71312-306">**FrameRate**</span><span class="sxs-lookup"><span data-stu-id="71312-306">**FrameRate**</span></span><br /><br /> <span data-ttu-id="71312-307">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-307">Required</span></span> |<span data-ttu-id="71312-308">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="71312-308">**xs:decimal**</span></span> |<span data-ttu-id="71312-309">Medida de taxa de quadros de vídeo em formato .3f.</span><span class="sxs-lookup"><span data-stu-id="71312-309">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="71312-310">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="71312-310">**Bitrate**</span></span> |<span data-ttu-id="71312-311">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-311">**xs:int**</span></span> |<span data-ttu-id="71312-312">Taxa média de bits de vídeo em quilobits por segundo, calculada desde o arquivo de ativo.</span><span class="sxs-lookup"><span data-stu-id="71312-312">Average video bit rate in kilobits per second, as calculated from the asset file.</span></span> <span data-ttu-id="71312-313">Apenas a carga de fluxo elementar é contada, e a sobrecarga de empacotamento não está incluída.</span><span class="sxs-lookup"><span data-stu-id="71312-313">Only the elementary stream payload is counted, and the packaging overhead is not included.</span></span> |
| <span data-ttu-id="71312-314">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="71312-314">**MaxGOPBitrate**</span></span> |<span data-ttu-id="71312-315">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-315">**xs:int**</span></span> |<span data-ttu-id="71312-316">Taxa de bits média do GOP máximo para esta faixa de vídeo em quilobits por segundo.</span><span class="sxs-lookup"><span data-stu-id="71312-316">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |
| <span data-ttu-id="71312-317">**HasBFrames**</span><span class="sxs-lookup"><span data-stu-id="71312-317">**HasBFrames**</span></span> |<span data-ttu-id="71312-318">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-318">**xs:int**</span></span> |<span data-ttu-id="71312-319">Número de faixas de vídeo de quadros B.</span><span class="sxs-lookup"><span data-stu-id="71312-319">Video track number of B frames.</span></span> |

## <span data-ttu-id="71312-320"><a name="MetadataType"></a> MetadataType</span><span class="sxs-lookup"><span data-stu-id="71312-320"><a name="MetadataType"></a> MetadataType</span></span>
<span data-ttu-id="71312-321">**MetadataType** é um tipo global complexo que descreve os metadados de um arquivo de ativo como cadeias de caracteres de chave/valor.</span><span class="sxs-lookup"><span data-stu-id="71312-321">**MetadataType** is a global complex type that describes metadata of an asset file as key/value strings.</span></span> <span data-ttu-id="71312-322">Por exemplo, key=”language” e value=”eng”.</span><span class="sxs-lookup"><span data-stu-id="71312-322">For example, key=”language”, and value=”eng”.</span></span>  

<span data-ttu-id="71312-323">Veja um exemplo de XML no final deste tópico: [Exemplo de XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="71312-323">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="71312-324">Atributos</span><span class="sxs-lookup"><span data-stu-id="71312-324">Attributes</span></span>
| <span data-ttu-id="71312-325">Nome</span><span class="sxs-lookup"><span data-stu-id="71312-325">Name</span></span> | <span data-ttu-id="71312-326">Tipo</span><span class="sxs-lookup"><span data-stu-id="71312-326">Type</span></span> | <span data-ttu-id="71312-327">Descrição</span><span class="sxs-lookup"><span data-stu-id="71312-327">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="71312-328">**chave**</span><span class="sxs-lookup"><span data-stu-id="71312-328">**key**</span></span><br /><br /> <span data-ttu-id="71312-329">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-329">Required</span></span> |<span data-ttu-id="71312-330">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="71312-330">**xs:string**</span></span> |<span data-ttu-id="71312-331">A chave no par chave/valor.</span><span class="sxs-lookup"><span data-stu-id="71312-331">The key in the key/value pair.</span></span> |
| <span data-ttu-id="71312-332">**valor**</span><span class="sxs-lookup"><span data-stu-id="71312-332">**value**</span></span><br /><br /> <span data-ttu-id="71312-333">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-333">Required</span></span> |<span data-ttu-id="71312-334">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="71312-334">**xs:string**</span></span> |<span data-ttu-id="71312-335">O valor do par chave/valor.</span><span class="sxs-lookup"><span data-stu-id="71312-335">The value in the key/value pair.</span></span> |

## <span data-ttu-id="71312-336"><a name="ProgramType"></a> ProgramType</span><span class="sxs-lookup"><span data-stu-id="71312-336"><a name="ProgramType"></a> ProgramType</span></span>
<span data-ttu-id="71312-337">**ProgramType** é um tipo global complexo que descreve um programa.</span><span class="sxs-lookup"><span data-stu-id="71312-337">**ProgramType** is a global complex type that describes a program.</span></span>  

### <a name="attributes"></a><span data-ttu-id="71312-338">Atributos</span><span class="sxs-lookup"><span data-stu-id="71312-338">Attributes</span></span>
| <span data-ttu-id="71312-339">Nome</span><span class="sxs-lookup"><span data-stu-id="71312-339">Name</span></span> | <span data-ttu-id="71312-340">Tipo</span><span class="sxs-lookup"><span data-stu-id="71312-340">Type</span></span> | <span data-ttu-id="71312-341">Descrição</span><span class="sxs-lookup"><span data-stu-id="71312-341">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="71312-342">**ProgramId**</span><span class="sxs-lookup"><span data-stu-id="71312-342">**ProgramId**</span></span><br /><br /> <span data-ttu-id="71312-343">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-343">Required</span></span> |<span data-ttu-id="71312-344">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-344">**xs:int**</span></span> |<span data-ttu-id="71312-345">Id do Programa</span><span class="sxs-lookup"><span data-stu-id="71312-345">Program Id</span></span> |
| <span data-ttu-id="71312-346">**NumberOfPrograms**</span><span class="sxs-lookup"><span data-stu-id="71312-346">**NumberOfPrograms**</span></span><br /><br /> <span data-ttu-id="71312-347">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-347">Required</span></span> |<span data-ttu-id="71312-348">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-348">**xs:int**</span></span> |<span data-ttu-id="71312-349">Número de programas.</span><span class="sxs-lookup"><span data-stu-id="71312-349">Number of programs.</span></span> |
| <span data-ttu-id="71312-350">**PmtPid**</span><span class="sxs-lookup"><span data-stu-id="71312-350">**PmtPid**</span></span><br /><br /> <span data-ttu-id="71312-351">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-351">Required</span></span> |<span data-ttu-id="71312-352">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-352">**xs:int**</span></span> |<span data-ttu-id="71312-353">As PMTs (Tabelas de Mapa de Programa) contêm informações sobre programas.</span><span class="sxs-lookup"><span data-stu-id="71312-353">Program Map Tables (PMTs) contain information about programs.</span></span>  <span data-ttu-id="71312-354">Para saber mais, confira [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span><span class="sxs-lookup"><span data-stu-id="71312-354">For more information, see [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span></span> |
| <span data-ttu-id="71312-355">**PcrPid**</span><span class="sxs-lookup"><span data-stu-id="71312-355">**PcrPid**</span></span><br /><br /> <span data-ttu-id="71312-356">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-356">Required</span></span> |<span data-ttu-id="71312-357">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-357">**xs:int**</span></span> |<span data-ttu-id="71312-358">Usado pelo decodificador.</span><span class="sxs-lookup"><span data-stu-id="71312-358">Used by decoder.</span></span> <span data-ttu-id="71312-359">Para saber mais, confira [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span><span class="sxs-lookup"><span data-stu-id="71312-359">For more information, see [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span></span> |
| <span data-ttu-id="71312-360">**StartPTS**</span><span class="sxs-lookup"><span data-stu-id="71312-360">**StartPTS**</span></span> |<span data-ttu-id="71312-361">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="71312-361">**xs: long**</span></span> |<span data-ttu-id="71312-362">Iniciando o carimbo de data/hora de apresentação.</span><span class="sxs-lookup"><span data-stu-id="71312-362">Starting presentation time stamp.</span></span> |
| <span data-ttu-id="71312-363">**EndPTS**</span><span class="sxs-lookup"><span data-stu-id="71312-363">**EndPTS**</span></span> |<span data-ttu-id="71312-364">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="71312-364">**xs: long**</span></span> |<span data-ttu-id="71312-365">Hora de término do carimbo de data/hora de apresentação.</span><span class="sxs-lookup"><span data-stu-id="71312-365">Ending presentation time stamp.</span></span> |

## <span data-ttu-id="71312-366"><a name="StreamDispositionType"></a> StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="71312-366"><a name="StreamDispositionType"></a> StreamDispositionType</span></span>
<span data-ttu-id="71312-367">**StreamDispositionType** é um tipo global complexo que descreve o fluxo.</span><span class="sxs-lookup"><span data-stu-id="71312-367">**StreamDispositionType** is a global complex type that describes the stream.</span></span>  

<span data-ttu-id="71312-368">Veja um exemplo de XML no final deste tópico: [Exemplo de XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="71312-368">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="71312-369">Atributos</span><span class="sxs-lookup"><span data-stu-id="71312-369">Attributes</span></span>
| <span data-ttu-id="71312-370">Nome</span><span class="sxs-lookup"><span data-stu-id="71312-370">Name</span></span> | <span data-ttu-id="71312-371">Tipo</span><span class="sxs-lookup"><span data-stu-id="71312-371">Type</span></span> | <span data-ttu-id="71312-372">Descrição</span><span class="sxs-lookup"><span data-stu-id="71312-372">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="71312-373">**Padrão**</span><span class="sxs-lookup"><span data-stu-id="71312-373">**Default**</span></span><br /><br /> <span data-ttu-id="71312-374">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-374">Required</span></span> |<span data-ttu-id="71312-375">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-375">**xs:int**</span></span> |<span data-ttu-id="71312-376">Defina esse atributo como 1 para indicar que esta é a apresentação padrão.</span><span class="sxs-lookup"><span data-stu-id="71312-376">Set this attribute to 1 to indicate this is the default presentation.</span></span> |
| <span data-ttu-id="71312-377">**Dub**</span><span class="sxs-lookup"><span data-stu-id="71312-377">**Dub**</span></span><br /><br /> <span data-ttu-id="71312-378">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-378">Required</span></span> |<span data-ttu-id="71312-379">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-379">**xs:int**</span></span> |<span data-ttu-id="71312-380">Defina esse atributo como 1 para indicar que esta é a apresentação dublada.</span><span class="sxs-lookup"><span data-stu-id="71312-380">Set this attribute to 1 to indicate this is the dubbed presentation.</span></span> |
| <span data-ttu-id="71312-381">**Original**</span><span class="sxs-lookup"><span data-stu-id="71312-381">**Original**</span></span><br /><br /> <span data-ttu-id="71312-382">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-382">Required</span></span> |<span data-ttu-id="71312-383">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-383">**xs:int**</span></span> |<span data-ttu-id="71312-384">Defina esse atributo como 1 para indicar que esta é a apresentação original.</span><span class="sxs-lookup"><span data-stu-id="71312-384">Set this attribute to 1 to indicate this is the original presentation.</span></span> |
| <span data-ttu-id="71312-385">**Comentário**</span><span class="sxs-lookup"><span data-stu-id="71312-385">**Comment**</span></span><br /><br /> <span data-ttu-id="71312-386">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-386">Required</span></span> |<span data-ttu-id="71312-387">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-387">**xs:int**</span></span> |<span data-ttu-id="71312-388">Defina esse atributo como 1 para indicar que esta faixa contém comentários.</span><span class="sxs-lookup"><span data-stu-id="71312-388">Set this attribute to 1 to indicate this track contains commentary.</span></span> |
| <span data-ttu-id="71312-389">**Lyrics**</span><span class="sxs-lookup"><span data-stu-id="71312-389">**Lyrics**</span></span><br /><br /> <span data-ttu-id="71312-390">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-390">Required</span></span> |<span data-ttu-id="71312-391">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-391">**xs:int**</span></span> |<span data-ttu-id="71312-392">Defina esse atributo como 1 para indicar que esta faixa contém letras.</span><span class="sxs-lookup"><span data-stu-id="71312-392">Set this attribute to 1 to indicate this track contains lyrics.</span></span> |
| <span data-ttu-id="71312-393">**Karaoke**</span><span class="sxs-lookup"><span data-stu-id="71312-393">**Karaoke**</span></span><br /><br /> <span data-ttu-id="71312-394">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-394">Required</span></span> |<span data-ttu-id="71312-395">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-395">**xs:int**</span></span> |<span data-ttu-id="71312-396">Defina esse atributo como 1 para indicar que ele representa a faixa de karaokê (música em segundo plano, sem vocais).</span><span class="sxs-lookup"><span data-stu-id="71312-396">Set this attribute to 1 to indicate this represents the karaoke track (background music, no vocals).</span></span> |
| <span data-ttu-id="71312-397">**Forced**</span><span class="sxs-lookup"><span data-stu-id="71312-397">**Forced**</span></span><br /><br /> <span data-ttu-id="71312-398">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-398">Required</span></span> |<span data-ttu-id="71312-399">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-399">**xs:int**</span></span> |<span data-ttu-id="71312-400">Defina esse atributo como 1 para indicar que esta é a apresentação forçada.</span><span class="sxs-lookup"><span data-stu-id="71312-400">Set this attribute to 1 to indicate this is the forced presentation.</span></span> |
| <span data-ttu-id="71312-401">**HearingImpaired**</span><span class="sxs-lookup"><span data-stu-id="71312-401">**HearingImpaired**</span></span><br /><br /> <span data-ttu-id="71312-402">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-402">Required</span></span> |<span data-ttu-id="71312-403">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-403">**xs:int**</span></span> |<span data-ttu-id="71312-404">Defina esse atributo como 1 para indicar que esta faixa é para os deficientes auditivos.</span><span class="sxs-lookup"><span data-stu-id="71312-404">Set this attribute to 1 to indicate this track is for the hearing impaired.</span></span> |
| <span data-ttu-id="71312-405">**VisualImpaired**</span><span class="sxs-lookup"><span data-stu-id="71312-405">**VisualImpaired**</span></span><br /><br /> <span data-ttu-id="71312-406">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-406">Required</span></span> |<span data-ttu-id="71312-407">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-407">**xs:int**</span></span> |<span data-ttu-id="71312-408">Defina esse atributo como 1 para indicar que esta faixa é para os deficientes visuais.</span><span class="sxs-lookup"><span data-stu-id="71312-408">Set this attribute to 1 to indicate this track is for the visually impaired.</span></span> |
| <span data-ttu-id="71312-409">**CleanEffects**</span><span class="sxs-lookup"><span data-stu-id="71312-409">**CleanEffects**</span></span><br /><br /> <span data-ttu-id="71312-410">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-410">Required</span></span> |<span data-ttu-id="71312-411">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-411">**xs:int**</span></span> |<span data-ttu-id="71312-412">Defina esse atributo como 1 para indicar que esta faixa tem efeitos limpos.</span><span class="sxs-lookup"><span data-stu-id="71312-412">Set this attribute to 1 to indicate this track has clean effects.</span></span> |
| <span data-ttu-id="71312-413">**AttachedPic**</span><span class="sxs-lookup"><span data-stu-id="71312-413">**AttachedPic**</span></span><br /><br /> <span data-ttu-id="71312-414">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="71312-414">Required</span></span> |<span data-ttu-id="71312-415">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="71312-415">**xs:int**</span></span> |<span data-ttu-id="71312-416">Defina esse atributo como 1 para indicar que esta faixa contém fotos.</span><span class="sxs-lookup"><span data-stu-id="71312-416">Set this attribute to 1 to indicate this track has pictures.</span></span> |

## <span data-ttu-id="71312-417"><a name="Programs"></a> Elemento Programs</span><span class="sxs-lookup"><span data-stu-id="71312-417"><a name="Programs"></a> Programs element</span></span>
<span data-ttu-id="71312-418">Elemento de wrapper que contém vários elementos **Program**.</span><span class="sxs-lookup"><span data-stu-id="71312-418">Wrapper element holding multiple **Program** elements.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="71312-419">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="71312-419">Child elements</span></span>
| <span data-ttu-id="71312-420">Nome</span><span class="sxs-lookup"><span data-stu-id="71312-420">Name</span></span> | <span data-ttu-id="71312-421">Tipo</span><span class="sxs-lookup"><span data-stu-id="71312-421">Type</span></span> | <span data-ttu-id="71312-422">Descrição</span><span class="sxs-lookup"><span data-stu-id="71312-422">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="71312-423">**Programa**</span><span class="sxs-lookup"><span data-stu-id="71312-423">**Program**</span></span><br /><br /> <span data-ttu-id="71312-424">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="71312-424">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="71312-425">ProgramType</span><span class="sxs-lookup"><span data-stu-id="71312-425">ProgramType</span></span>](media-services-input-metadata-schema.md#ProgramType) |<span data-ttu-id="71312-426">Para os arquivos de ativo no formato MPEG-TS, eles contêm informações sobre os programas no arquivo de ativo.</span><span class="sxs-lookup"><span data-stu-id="71312-426">For asset files that are in MPEG-TS format, contains information about programs in the asset file.</span></span> |

## <span data-ttu-id="71312-427"><a name="VideoTracks"></a> Elemento VideoTracks</span><span class="sxs-lookup"><span data-stu-id="71312-427"><a name="VideoTracks"></a> VideoTracks element</span></span>
 <span data-ttu-id="71312-428">Elemento de wrapper que contém vários elementos **VideoTrack**.</span><span class="sxs-lookup"><span data-stu-id="71312-428">Wrapper element holding multiple **VideoTrack** elements.</span></span>  

 <span data-ttu-id="71312-429">Veja um exemplo de XML no final deste tópico: [Exemplo de XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="71312-429">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="71312-430">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="71312-430">Child elements</span></span>
| <span data-ttu-id="71312-431">Nome</span><span class="sxs-lookup"><span data-stu-id="71312-431">Name</span></span> | <span data-ttu-id="71312-432">Tipo</span><span class="sxs-lookup"><span data-stu-id="71312-432">Type</span></span> | <span data-ttu-id="71312-433">Descrição</span><span class="sxs-lookup"><span data-stu-id="71312-433">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="71312-434">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="71312-434">**VideoTrack**</span></span><br /><br /> <span data-ttu-id="71312-435">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="71312-435">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="71312-436">VideoTrackType (herdado de TrackType)</span><span class="sxs-lookup"><span data-stu-id="71312-436">VideoTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#VideoTrackType) |<span data-ttu-id="71312-437">Contém informações sobre as faixas de vídeo no arquivo de ativo.</span><span class="sxs-lookup"><span data-stu-id="71312-437">Contains information about video tracks in the asset file.</span></span> |

## <span data-ttu-id="71312-438"><a name="AudioTracks"></a> Elemento AudioTracks</span><span class="sxs-lookup"><span data-stu-id="71312-438"><a name="AudioTracks"></a> AudioTracks element</span></span>
 <span data-ttu-id="71312-439">Elemento de wrapper que contém vários elementos **AudioTrack**.</span><span class="sxs-lookup"><span data-stu-id="71312-439">Wrapper element holding multiple **AudioTrack** elements.</span></span>  

 <span data-ttu-id="71312-440">Veja um exemplo de XML no final deste tópico: [Exemplo de XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="71312-440">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="elements"></a><span data-ttu-id="71312-441">elementos</span><span class="sxs-lookup"><span data-stu-id="71312-441">elements</span></span>
| <span data-ttu-id="71312-442">Nome</span><span class="sxs-lookup"><span data-stu-id="71312-442">Name</span></span> | <span data-ttu-id="71312-443">Tipo</span><span class="sxs-lookup"><span data-stu-id="71312-443">Type</span></span> | <span data-ttu-id="71312-444">Descrição</span><span class="sxs-lookup"><span data-stu-id="71312-444">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="71312-445">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="71312-445">**AudioTrack**</span></span><br /><br /> <span data-ttu-id="71312-446">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="71312-446">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="71312-447">AudioTrackType (herdado de TrackType)</span><span class="sxs-lookup"><span data-stu-id="71312-447">AudioTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#AudioTrackType) |<span data-ttu-id="71312-448">Contém informações sobre as faixas de áudios no arquivo de ativo.</span><span class="sxs-lookup"><span data-stu-id="71312-448">Contains information about audio tracks in the asset file.</span></span> |

## <span data-ttu-id="71312-449"><a name="code"></a> Código de Esquema</span><span class="sxs-lookup"><span data-stu-id="71312-449"><a name="code"></a> Schema Code</span></span>
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
            <xs:documentation>zero-based index of this video track. Note: this is not necessarily the TrackID as used in an MP4 file</xs:documentation>  
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
          <xs:documentation>A specific video track in the parent AssetFile</xs:documentation>  
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
                <xs:documentation>average video bit rate in kilobits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
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
          <xs:documentation>a specific audio track in the parent AssetFile</xs:documentation>  
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
                <xs:documentation>average audio bit rate in bits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for the wFormatTag format type</xs:documentation>  
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
          <xs:documentation>Collection of AssetFile entries for the encoding job</xs:documentation>  
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
                      <xs:documentation>This is the collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is the collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is the collection of all those audio tracks</xs:documentation>  
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
                    <xs:documentation>the media asset file name</xs:documentation>  
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
                    <xs:documentation>average bitrate of the asset file in kbps</xs:documentation>  
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


## <span data-ttu-id="71312-450"><a name="xml"></a> Exemplo de XML</span><span class="sxs-lookup"><span data-stu-id="71312-450"><a name="xml"></a> XML example</span></span>
<span data-ttu-id="71312-451">Este é um exemplo do arquivo de metadados de entrada.</span><span class="sxs-lookup"><span data-stu-id="71312-451">The following is an example of the Input metadata file.</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="71312-452">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="71312-452">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="71312-453">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="71312-453">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

