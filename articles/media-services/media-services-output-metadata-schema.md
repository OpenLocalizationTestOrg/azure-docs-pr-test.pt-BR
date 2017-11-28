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
# <a name="output-metadata"></a><span data-ttu-id="5a192-103">Metadados de saída</span><span class="sxs-lookup"><span data-stu-id="5a192-103">Output Metadata</span></span>
## <a name="overview"></a><span data-ttu-id="5a192-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="5a192-104">Overview</span></span>
<span data-ttu-id="5a192-105">Um trabalho de codificação está associado um ativo de entrada (ou ativos) no qual você deseja tooperform algumas tarefas de codificação.</span><span class="sxs-lookup"><span data-stu-id="5a192-105">An encoding job is associated with an input asset (or assets) on which you want tooperform some encoding tasks.</span></span> <span data-ttu-id="5a192-106">Por exemplo, codificar uma MP4 arquivo tooH.264 MP4 taxa de bits adaptável define; criar uma miniatura. Crie sobreposições.</span><span class="sxs-lookup"><span data-stu-id="5a192-106">For example, encode an MP4 file tooH.264 MP4 adaptive bitrate sets; create a thumbnail; create overlays.</span></span> <span data-ttu-id="5a192-107">Após a conclusão de uma tarefa, um ativo de saída é produzido.</span><span class="sxs-lookup"><span data-stu-id="5a192-107">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="5a192-108">Olá ativo de saída contém vídeo, áudio, miniaturas, etc. Olá também contém um arquivo com metadados sobre o ativo de saída hello.</span><span class="sxs-lookup"><span data-stu-id="5a192-108">hello output asset contains video, audio, thumbnails, etc. hello output asset also contains a file with metadata about hello output asset.</span></span> <span data-ttu-id="5a192-109">nome do arquivo XML de metadados Olá Olá tem Olá formato a seguir: &lt;source_file_name>_manifest.XML&gt;<nome_do_arquivo_de_origem>_manifest.XML (por exemplo, BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="5a192-109">hello name of hello metadata XML file has hello following format: &lt;source_file_name&gt;_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span>  

<span data-ttu-id="5a192-110">Se desejar que o arquivo de metadados de saudação tooexamine, você pode criar um **SAS** localizador e download Olá computador local do arquivo tooyour.</span><span class="sxs-lookup"><span data-stu-id="5a192-110">If you want tooexamine hello metadata file, you can create a **SAS** locator and download hello file tooyour local computer.</span></span>  

<span data-ttu-id="5a192-111">Este tópico discute elementos hello e tipos de esquema XML, Olá em quais metadados de saída hello (&lt;source_file_name>_manifest.XML&gt;<nome_do_arquivo_de_origem>_manifest.xml) é baseado.</span><span class="sxs-lookup"><span data-stu-id="5a192-111">This topic discusses hello elements and types of hello XML schema on which hello output metada (&lt;source_file_name&gt;_manifest.xml) is based.</span></span> <span data-ttu-id="5a192-112">Para obter informações sobre o arquivo hello que contém metadados sobre o ativo de entrada hello, consulte [metadados de entrada](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="5a192-112">For information about hello file that contains metadata about hello input asset, see [Input Metadata](media-services-input-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="5a192-113">Você pode encontrar o código de esquema completo hello e exemplo XML no final deste tópico hello.</span><span class="sxs-lookup"><span data-stu-id="5a192-113">You can find hello complete schema code and XML example at hello end of this topic.</span></span>  
>
>

## <span data-ttu-id="5a192-114"><a name="AssetFiles "></a> Elemento raiz AssetFiles</span><span class="sxs-lookup"><span data-stu-id="5a192-114"><a name="AssetFiles "></a> AssetFiles root element</span></span>
<span data-ttu-id="5a192-115">Coleção de entradas AssetFile para o trabalho de codificação hello.</span><span class="sxs-lookup"><span data-stu-id="5a192-115">Collection of AssetFile entries for hello encoding job.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="5a192-116">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="5a192-116">Child elements</span></span>
| <span data-ttu-id="5a192-117">Nome</span><span class="sxs-lookup"><span data-stu-id="5a192-117">Name</span></span> | <span data-ttu-id="5a192-118">Descrição</span><span class="sxs-lookup"><span data-stu-id="5a192-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5a192-119">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="5a192-119">**AssetFile**</span></span><br/><br/> <span data-ttu-id="5a192-120">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="5a192-120">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="5a192-121">Um [elemento AssetFile](media-services-output-metadata-schema.md) que faz parte da coleção de AssetFiles de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a192-121">An [AssetFile element](media-services-output-metadata-schema.md) that is part of hello AssetFiles collection.</span></span> |

## <span data-ttu-id="5a192-122"><a name="AssetFile "></a> Elemento AssetFile</span><span class="sxs-lookup"><span data-stu-id="5a192-122"><a name="AssetFile "></a> AssetFile element</span></span>
<span data-ttu-id="5a192-123">Você pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="5a192-123">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="5a192-124">Atributos</span><span class="sxs-lookup"><span data-stu-id="5a192-124">Attributes</span></span>
| <span data-ttu-id="5a192-125">Nome</span><span class="sxs-lookup"><span data-stu-id="5a192-125">Name</span></span> | <span data-ttu-id="5a192-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="5a192-126">Type</span></span> | <span data-ttu-id="5a192-127">Descrição</span><span class="sxs-lookup"><span data-stu-id="5a192-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a192-128">**Nome**</span><span class="sxs-lookup"><span data-stu-id="5a192-128">**Name**</span></span><br/><br/> <span data-ttu-id="5a192-129">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-129">Required</span></span> |<span data-ttu-id="5a192-130">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="5a192-130">**xs:string**</span></span> |<span data-ttu-id="5a192-131">nome do arquivo de ativo de mídia de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a192-131">hello media asset file name.</span></span> |
| <span data-ttu-id="5a192-132">**Tamanho**</span><span class="sxs-lookup"><span data-stu-id="5a192-132">**Size**</span></span><br/><br/> <span data-ttu-id="5a192-133">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="5a192-133">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="5a192-134">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-134">Required</span></span> |<span data-ttu-id="5a192-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="5a192-135">**xs:long**</span></span> |<span data-ttu-id="5a192-136">Tamanho do arquivo de ativo de saudação em bytes.</span><span class="sxs-lookup"><span data-stu-id="5a192-136">Size of hello asset file in bytes.</span></span> |
| <span data-ttu-id="5a192-137">**Duração**</span><span class="sxs-lookup"><span data-stu-id="5a192-137">**Duration**</span></span><br/><br/> <span data-ttu-id="5a192-138">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-138">Required</span></span> |<span data-ttu-id="5a192-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="5a192-139">**xs:duration**</span></span> |<span data-ttu-id="5a192-140">Duração de reprodução de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="5a192-140">Content play back duration.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="5a192-141">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="5a192-141">Child elements</span></span>
| <span data-ttu-id="5a192-142">Nome</span><span class="sxs-lookup"><span data-stu-id="5a192-142">Name</span></span> | <span data-ttu-id="5a192-143">Descrição</span><span class="sxs-lookup"><span data-stu-id="5a192-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5a192-144">**Fontes**</span><span class="sxs-lookup"><span data-stu-id="5a192-144">**Sources**</span></span> |<span data-ttu-id="5a192-145">Coleção de arquivos de mídia de entrada/origem, que foi processada em ordem tooproduce esse AssetFile.</span><span class="sxs-lookup"><span data-stu-id="5a192-145">Collection of input/source media files, that was processed in order tooproduce this AssetFile.</span></span> <span data-ttu-id="5a192-146">Para obter mais informações, veja [Elemento Origem](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="5a192-146">For more information, see [Source element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="5a192-147">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="5a192-147">**VideoTracks**</span></span><br/><br/> <span data-ttu-id="5a192-148">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="5a192-148">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="5a192-149">Cada AssetFile físico pode conter zero ou mais faixas de vídeo intercaladas em um formato de contêiner apropriado.</span><span class="sxs-lookup"><span data-stu-id="5a192-149">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="5a192-150">Esta é a coleção de saudação de todas essas faixas de vídeos.</span><span class="sxs-lookup"><span data-stu-id="5a192-150">This is hello collection of all those video tracks.</span></span> <span data-ttu-id="5a192-151">Para obter mais informações, veja [Elemento VideoTracks](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="5a192-151">For more information, see [VideoTracks element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="5a192-152">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="5a192-152">**AudioTracks**</span></span><br/><br/> <span data-ttu-id="5a192-153">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="5a192-153">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="5a192-154">Cada AssetFile físico pode conter zero ou mais faixas de áudio intercaladas em um formato de contêiner apropriado.</span><span class="sxs-lookup"><span data-stu-id="5a192-154">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="5a192-155">Esta é a coleção de saudação de todas essas faixas de áudio.</span><span class="sxs-lookup"><span data-stu-id="5a192-155">This is hello collection of all those audio tracks.</span></span> <span data-ttu-id="5a192-156">Para obter mais informações, veja [Elemento AudioTracks](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="5a192-156">For more information, see [AudioTracks element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="5a192-157"><a name="Sources "></a> Elemento Origens</span><span class="sxs-lookup"><span data-stu-id="5a192-157"><a name="Sources "></a> Sources element</span></span>
<span data-ttu-id="5a192-158">Coleção de arquivos de mídia de entrada/origem, que foi processada em ordem tooproduce esse AssetFile.</span><span class="sxs-lookup"><span data-stu-id="5a192-158">Collection of input/source media files, that was processed in order tooproduce this AssetFile.</span></span>  

<span data-ttu-id="5a192-159">Você pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="5a192-159">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="5a192-160">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="5a192-160">Child elements</span></span>
| <span data-ttu-id="5a192-161">Nome</span><span class="sxs-lookup"><span data-stu-id="5a192-161">Name</span></span> | <span data-ttu-id="5a192-162">Descrição</span><span class="sxs-lookup"><span data-stu-id="5a192-162">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5a192-163">**Fonte**</span><span class="sxs-lookup"><span data-stu-id="5a192-163">**Source**</span></span><br/><br/> <span data-ttu-id="5a192-164">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="5a192-164">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="5a192-165">Um arquivo de entrada/origem usado ao gerar esse ativo.</span><span class="sxs-lookup"><span data-stu-id="5a192-165">An input/source file used when generating this asset.</span></span> <span data-ttu-id="5a192-166">Para obter mais informações, veja [Elemento Origem](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="5a192-166">For more information see [Source element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="5a192-167"><a name="Source "></a> Elemento Origem</span><span class="sxs-lookup"><span data-stu-id="5a192-167"><a name="Source "></a> Source element</span></span>
<span data-ttu-id="5a192-168">Um arquivo de entrada/origem usado ao gerar esse ativo.</span><span class="sxs-lookup"><span data-stu-id="5a192-168">An input/source file used when generating this asset.</span></span>  

<span data-ttu-id="5a192-169">Você pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="5a192-169">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="5a192-170">Atributos</span><span class="sxs-lookup"><span data-stu-id="5a192-170">Attributes</span></span>
| <span data-ttu-id="5a192-171">Nome</span><span class="sxs-lookup"><span data-stu-id="5a192-171">Name</span></span> | <span data-ttu-id="5a192-172">Tipo</span><span class="sxs-lookup"><span data-stu-id="5a192-172">Type</span></span> | <span data-ttu-id="5a192-173">Descrição</span><span class="sxs-lookup"><span data-stu-id="5a192-173">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a192-174">**Nome**</span><span class="sxs-lookup"><span data-stu-id="5a192-174">**Name**</span></span><br/><br/> <span data-ttu-id="5a192-175">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-175">Required</span></span> |<span data-ttu-id="5a192-176">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="5a192-176">**xs:string**</span></span> |<span data-ttu-id="5a192-177">Nome do arquivo de fonte de entrada.</span><span class="sxs-lookup"><span data-stu-id="5a192-177">Input source file name.</span></span> |

## <span data-ttu-id="5a192-178"><a name="VideoTracks "></a> Elemento VideoTracks</span><span class="sxs-lookup"><span data-stu-id="5a192-178"><a name="VideoTracks "></a> VideoTracks element</span></span>
<span data-ttu-id="5a192-179">Cada AssetFile físico pode conter zero ou mais faixas de vídeo intercaladas em um formato de contêiner apropriado.</span><span class="sxs-lookup"><span data-stu-id="5a192-179">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="5a192-180">Esta é a coleção de saudação de todas essas faixas de vídeos.</span><span class="sxs-lookup"><span data-stu-id="5a192-180">This is hello collection of all those video tracks.</span></span>  

<span data-ttu-id="5a192-181">Você pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="5a192-181">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="5a192-182">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="5a192-182">Child elements</span></span>
| <span data-ttu-id="5a192-183">Nome</span><span class="sxs-lookup"><span data-stu-id="5a192-183">Name</span></span> | <span data-ttu-id="5a192-184">Descrição</span><span class="sxs-lookup"><span data-stu-id="5a192-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5a192-185">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="5a192-185">**VideoTrack**</span></span><br/><br/> <span data-ttu-id="5a192-186">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="5a192-186">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="5a192-187">Uma faixa de vídeo específica no AssetFile pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a192-187">A specific video track in hello parent AssetFile.</span></span> <span data-ttu-id="5a192-188">Para obter mais informações, veja [Elemento VideoTrack](media-services-output-metadata-schema.md#VideoTrack).</span><span class="sxs-lookup"><span data-stu-id="5a192-188">For more information, see [VideoTrack element](media-services-output-metadata-schema.md#VideoTrack).</span></span> |

## <span data-ttu-id="5a192-189"><a name="VideoTrack"></a> Elemento VideoTrack</span><span class="sxs-lookup"><span data-stu-id="5a192-189"><a name="VideoTrack"></a> VideoTrack element</span></span>
<span data-ttu-id="5a192-190">Uma faixa de vídeo específica no AssetFile pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a192-190">A specific video track in hello parent AssetFile.</span></span>  

<span data-ttu-id="5a192-191">Você pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="5a192-191">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="5a192-192">Atributos</span><span class="sxs-lookup"><span data-stu-id="5a192-192">Attributes</span></span>
| <span data-ttu-id="5a192-193">Nome</span><span class="sxs-lookup"><span data-stu-id="5a192-193">Name</span></span> | <span data-ttu-id="5a192-194">Tipo</span><span class="sxs-lookup"><span data-stu-id="5a192-194">Type</span></span> | <span data-ttu-id="5a192-195">Descrição</span><span class="sxs-lookup"><span data-stu-id="5a192-195">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a192-196">**Id**</span><span class="sxs-lookup"><span data-stu-id="5a192-196">**Id**</span></span><br/><br/> <span data-ttu-id="5a192-197">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="5a192-197">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="5a192-198">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-198">Required</span></span> |<span data-ttu-id="5a192-199">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="5a192-199">**xs:int**</span></span> |<span data-ttu-id="5a192-200">Índice baseado em zero dessa faixa de vídeo. **Observação:** não é necessariamente Olá TrackID como utilizado em um arquivo MP4.</span><span class="sxs-lookup"><span data-stu-id="5a192-200">Zero-based index of this video track. **Note:**  This is not necessarily hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="5a192-201">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="5a192-201">**FourCC**</span></span><br/><br/> <span data-ttu-id="5a192-202">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-202">Required</span></span> |<span data-ttu-id="5a192-203">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="5a192-203">**xs:string**</span></span> |<span data-ttu-id="5a192-204">Código FourCC de codec de vídeo.</span><span class="sxs-lookup"><span data-stu-id="5a192-204">Video codec FourCC code.</span></span> |
| <span data-ttu-id="5a192-205">**Perfil**</span><span class="sxs-lookup"><span data-stu-id="5a192-205">**Profile**</span></span> |<span data-ttu-id="5a192-206">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="5a192-206">**xs:string**</span></span> |<span data-ttu-id="5a192-207">Perfil H264 (somente aplicável tooH264 codec).</span><span class="sxs-lookup"><span data-stu-id="5a192-207">H264 profile (only applicable tooH264 codec).</span></span> |
| <span data-ttu-id="5a192-208">**Level**</span><span class="sxs-lookup"><span data-stu-id="5a192-208">**Level**</span></span> |<span data-ttu-id="5a192-209">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="5a192-209">**xs:string**</span></span> |<span data-ttu-id="5a192-210">Nível H264 (somente aplicável tooH264 codec).</span><span class="sxs-lookup"><span data-stu-id="5a192-210">H264 level (only applicable tooH264 codec).</span></span> |
| <span data-ttu-id="5a192-211">**Width**</span><span class="sxs-lookup"><span data-stu-id="5a192-211">**Width**</span></span><br/><br/> <span data-ttu-id="5a192-212">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="5a192-212">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="5a192-213">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-213">Required</span></span> |<span data-ttu-id="5a192-214">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="5a192-214">**xs:int**</span></span> |<span data-ttu-id="5a192-215">Largura do vídeo codificado em pixels.</span><span class="sxs-lookup"><span data-stu-id="5a192-215">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="5a192-216">**Height**</span><span class="sxs-lookup"><span data-stu-id="5a192-216">**Height**</span></span><br/><br/> <span data-ttu-id="5a192-217">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="5a192-217">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="5a192-218">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-218">Required</span></span> |<span data-ttu-id="5a192-219">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="5a192-219">**xs:int**</span></span> |<span data-ttu-id="5a192-220">Altura do vídeo codificado em pixels.</span><span class="sxs-lookup"><span data-stu-id="5a192-220">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="5a192-221">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="5a192-221">**DisplayAspectRatioNumerator**</span></span><br/><br/> <span data-ttu-id="5a192-222">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="5a192-222">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="5a192-223">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-223">Required</span></span> |<span data-ttu-id="5a192-224">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="5a192-224">**xs:double**</span></span> |<span data-ttu-id="5a192-225">Numerador de taxa de proporção de exibição do vídeo.</span><span class="sxs-lookup"><span data-stu-id="5a192-225">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="5a192-226">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="5a192-226">**DisplayAspectRatioDenominator**</span></span><br/><br/> <span data-ttu-id="5a192-227">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="5a192-227">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="5a192-228">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-228">Required</span></span> |<span data-ttu-id="5a192-229">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="5a192-229">**xs:double**</span></span> |<span data-ttu-id="5a192-230">Denominador de taxa de proporção de exibição do vídeo.</span><span class="sxs-lookup"><span data-stu-id="5a192-230">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="5a192-231">**Framerate**</span><span class="sxs-lookup"><span data-stu-id="5a192-231">**Framerate**</span></span><br/><br/> <span data-ttu-id="5a192-232">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="5a192-232">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="5a192-233">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-233">Required</span></span> |<span data-ttu-id="5a192-234">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="5a192-234">**xs:decimal**</span></span> |<span data-ttu-id="5a192-235">Medida de taxa de quadros de vídeo em formato .3f.</span><span class="sxs-lookup"><span data-stu-id="5a192-235">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="5a192-236">**TargetFramerate**</span><span class="sxs-lookup"><span data-stu-id="5a192-236">**TargetFramerate**</span></span><br/><br/> <span data-ttu-id="5a192-237">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="5a192-237">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="5a192-238">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-238">Required</span></span> |<span data-ttu-id="5a192-239">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="5a192-239">**xs:decimal**</span></span> |<span data-ttu-id="5a192-240">Taxa de quadros de vídeo de destino predefinida em formato .3f.</span><span class="sxs-lookup"><span data-stu-id="5a192-240">Preset target video frame rate in .3f format.</span></span> |
| <span data-ttu-id="5a192-241">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="5a192-241">**Bitrate**</span></span><br/><br/> <span data-ttu-id="5a192-242">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="5a192-242">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="5a192-243">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-243">Required</span></span> |<span data-ttu-id="5a192-244">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="5a192-244">**xs:int**</span></span> |<span data-ttu-id="5a192-245">Taxa média de bits de vídeo em quilobits por segundo, calculada a partir Olá AssetFile.</span><span class="sxs-lookup"><span data-stu-id="5a192-245">Average video bit rate in kilobits per second, as calculated from hello AssetFile.</span></span> <span data-ttu-id="5a192-246">Contagens somente Olá corrente de carga elementar e não inclui a sobrecarga de embalagem hello.</span><span class="sxs-lookup"><span data-stu-id="5a192-246">Counts only hello elementary stream payload, and does not include hello packaging overhead.</span></span> |
| <span data-ttu-id="5a192-247">**TargetBitrate**</span><span class="sxs-lookup"><span data-stu-id="5a192-247">**TargetBitrate**</span></span><br/><br/> <span data-ttu-id="5a192-248">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="5a192-248">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="5a192-249">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-249">Required</span></span> |<span data-ttu-id="5a192-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="5a192-250">**xs:int**</span></span> |<span data-ttu-id="5a192-251">Taxa de bits média para esta faixa de vídeo de destino conforme solicitado através da predefinição de codificação hello, em quilobits por segundo.</span><span class="sxs-lookup"><span data-stu-id="5a192-251">Target average bitrate for this video track, as requested via hello encoding preset, in kilobits per second.</span></span> |
| <span data-ttu-id="5a192-252">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="5a192-252">**MaxGOPBitrate**</span></span><br/><br/> <span data-ttu-id="5a192-253">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="5a192-253">minInclusive ="0"</span></span> |<span data-ttu-id="5a192-254">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="5a192-254">**xs:int**</span></span> |<span data-ttu-id="5a192-255">Taxa de bits média do GOP máximo para esta faixa de vídeo em quilobits por segundo.</span><span class="sxs-lookup"><span data-stu-id="5a192-255">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |

## <span data-ttu-id="5a192-256"><a name="AudioTracks "></a> Elemento AudioTracks</span><span class="sxs-lookup"><span data-stu-id="5a192-256"><a name="AudioTracks "></a> AudioTracks element</span></span>
<span data-ttu-id="5a192-257">Cada AssetFile físico pode conter zero ou mais faixas de áudio intercaladas em um formato de contêiner apropriado.</span><span class="sxs-lookup"><span data-stu-id="5a192-257">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="5a192-258">Esta é a coleção de saudação de todas essas faixas de áudio.</span><span class="sxs-lookup"><span data-stu-id="5a192-258">This is hello collection of all those audio tracks.</span></span>  

<span data-ttu-id="5a192-259">Você pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="5a192-259">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="5a192-260">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="5a192-260">Child elements</span></span>
| <span data-ttu-id="5a192-261">Nome</span><span class="sxs-lookup"><span data-stu-id="5a192-261">Name</span></span> | <span data-ttu-id="5a192-262">Descrição</span><span class="sxs-lookup"><span data-stu-id="5a192-262">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5a192-263">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="5a192-263">**AudioTrack**</span></span><br/><br/> <span data-ttu-id="5a192-264">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="5a192-264">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="5a192-265">Uma faixa de áudio específica no AssetFile pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a192-265">A specific audio track in hello parent AssetFile.</span></span> <span data-ttu-id="5a192-266">Para obter mais informações, veja [Elemento AudioTrack](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="5a192-266">For more information, see [AudioTrack element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="5a192-267"><a name="AudioTrack "></a> Elemento AudioTrack</span><span class="sxs-lookup"><span data-stu-id="5a192-267"><a name="AudioTrack "></a> AudioTrack element</span></span>
<span data-ttu-id="5a192-268">Uma faixa de áudio específica no AssetFile pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a192-268">A specific audio track in hello parent AssetFile.</span></span>  

<span data-ttu-id="5a192-269">Você pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="5a192-269">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="5a192-270">Atributos</span><span class="sxs-lookup"><span data-stu-id="5a192-270">Attributes</span></span>
| <span data-ttu-id="5a192-271">Nome</span><span class="sxs-lookup"><span data-stu-id="5a192-271">Name</span></span> | <span data-ttu-id="5a192-272">Tipo</span><span class="sxs-lookup"><span data-stu-id="5a192-272">Type</span></span> | <span data-ttu-id="5a192-273">Descrição</span><span class="sxs-lookup"><span data-stu-id="5a192-273">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a192-274">**Id**</span><span class="sxs-lookup"><span data-stu-id="5a192-274">**Id**</span></span><br/><br/> <span data-ttu-id="5a192-275">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="5a192-275">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="5a192-276">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-276">Required</span></span> |<span data-ttu-id="5a192-277">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="5a192-277">**xs:int**</span></span> |<span data-ttu-id="5a192-278">Índice baseado em zero dessa faixa de áudio. **Observação:** não é necessariamente Olá TrackID como utilizado em um arquivo MP4.</span><span class="sxs-lookup"><span data-stu-id="5a192-278">Zero-based index of this audio track. **Note:**  This is not necessarily hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="5a192-279">**Codec**</span><span class="sxs-lookup"><span data-stu-id="5a192-279">**Codec**</span></span> |<span data-ttu-id="5a192-280">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="5a192-280">**xs:string**</span></span> |<span data-ttu-id="5a192-281">Cadeia de caracteres de codec de faixa de áudio.</span><span class="sxs-lookup"><span data-stu-id="5a192-281">Audio track codec string.</span></span> |
| <span data-ttu-id="5a192-282">**EncoderVersion**</span><span class="sxs-lookup"><span data-stu-id="5a192-282">**EncoderVersion**</span></span> |<span data-ttu-id="5a192-283">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="5a192-283">**xs:string**</span></span> |<span data-ttu-id="5a192-284">Cadeia de caracteres da versão de codificador opcional, exigida para EAC3.</span><span class="sxs-lookup"><span data-stu-id="5a192-284">Optional encoder version string, required for EAC3.</span></span> |
| <span data-ttu-id="5a192-285">**Channels**</span><span class="sxs-lookup"><span data-stu-id="5a192-285">**Channels**</span></span><br/><br/> <span data-ttu-id="5a192-286">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="5a192-286">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="5a192-287">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-287">Required</span></span> |<span data-ttu-id="5a192-288">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="5a192-288">**xs:int**</span></span> |<span data-ttu-id="5a192-289">Número de canais de áudio.</span><span class="sxs-lookup"><span data-stu-id="5a192-289">Number of audio channels.</span></span> |
| <span data-ttu-id="5a192-290">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="5a192-290">**SamplingRate**</span></span><br/><br/> <span data-ttu-id="5a192-291">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="5a192-291">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="5a192-292">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-292">Required</span></span> |<span data-ttu-id="5a192-293">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="5a192-293">**xs:int**</span></span> |<span data-ttu-id="5a192-294">Taxa de amostragem de áudio em amostras/s ou Hz.</span><span class="sxs-lookup"><span data-stu-id="5a192-294">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="5a192-295">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="5a192-295">**Bitrate**</span></span><br/><br/> <span data-ttu-id="5a192-296">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="5a192-296">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="5a192-297">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-297">Required</span></span> |<span data-ttu-id="5a192-298">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="5a192-298">**xs:int**</span></span> |<span data-ttu-id="5a192-299">Taxa média de bits de áudio em bits por segundo, calculada a partir Olá AssetFile.</span><span class="sxs-lookup"><span data-stu-id="5a192-299">Average audio bit rate in bits per second, as calculated from hello AssetFile.</span></span> <span data-ttu-id="5a192-300">Contagens somente Olá corrente de carga elementar e não inclui a sobrecarga de embalagem hello.</span><span class="sxs-lookup"><span data-stu-id="5a192-300">Counts only hello elementary stream payload, and does not include hello packaging overhead.</span></span> |
| <span data-ttu-id="5a192-301">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="5a192-301">**BitsPerSample**</span></span><br/><br/> <span data-ttu-id="5a192-302">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="5a192-302">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="5a192-303">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-303">Required</span></span> |<span data-ttu-id="5a192-304">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="5a192-304">**xs:int**</span></span> |<span data-ttu-id="5a192-305">Bits por amostra para o formato wFormatTag Olá tipo.</span><span class="sxs-lookup"><span data-stu-id="5a192-305">Bits per sample for hello wFormatTag format type.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="5a192-306">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="5a192-306">Child elements</span></span>
| <span data-ttu-id="5a192-307">Nome</span><span class="sxs-lookup"><span data-stu-id="5a192-307">Name</span></span> | <span data-ttu-id="5a192-308">Descrição</span><span class="sxs-lookup"><span data-stu-id="5a192-308">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5a192-309">**LoudnessMeteringResultParameters**</span><span class="sxs-lookup"><span data-stu-id="5a192-309">**LoudnessMeteringResultParameters**</span></span><br/><br/> <span data-ttu-id="5a192-310">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="5a192-310">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="5a192-311">Parâmetros de resultado de medição de intensidade.</span><span class="sxs-lookup"><span data-stu-id="5a192-311">Loudness metering result parameters.</span></span> <span data-ttu-id="5a192-312">Para obter mais informações, veja [Elemento LoudnessMeteringResultParameters](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="5a192-312">For more information, see [LoudnessMeteringResultParameters element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="5a192-313"><a name="LoudnessMeteringResultParameters "></a> Elemento LoudnessMeteringResultParameters</span><span class="sxs-lookup"><span data-stu-id="5a192-313"><a name="LoudnessMeteringResultParameters "></a> LoudnessMeteringResultParameters element</span></span>
<span data-ttu-id="5a192-314">Parâmetros de resultado de medição de intensidade.</span><span class="sxs-lookup"><span data-stu-id="5a192-314">Loudness metering result parameters.</span></span>  

<span data-ttu-id="5a192-315">Você pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="5a192-315">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="5a192-316">Atributos</span><span class="sxs-lookup"><span data-stu-id="5a192-316">Attributes</span></span>
| <span data-ttu-id="5a192-317">Nome</span><span class="sxs-lookup"><span data-stu-id="5a192-317">Name</span></span> | <span data-ttu-id="5a192-318">Tipo</span><span class="sxs-lookup"><span data-stu-id="5a192-318">Type</span></span> | <span data-ttu-id="5a192-319">Descrição</span><span class="sxs-lookup"><span data-stu-id="5a192-319">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a192-320">**DPLMVersionInformation**</span><span class="sxs-lookup"><span data-stu-id="5a192-320">**DPLMVersionInformation**</span></span> |<span data-ttu-id="5a192-321">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="5a192-321">**xs:string**</span></span> |<span data-ttu-id="5a192-322">Versão do kit de desenvolvimento de medição de intensidade profissional **Dolby**.</span><span class="sxs-lookup"><span data-stu-id="5a192-322">**Dolby** professional loudness metering development kit version.</span></span> |
| <span data-ttu-id="5a192-323">**DialogNormalization**</span><span class="sxs-lookup"><span data-stu-id="5a192-323">**DialogNormalization**</span></span><br/><br/> <span data-ttu-id="5a192-324">minInclusive="-31" maxInclusive="-1"</span><span class="sxs-lookup"><span data-stu-id="5a192-324">minInclusive="-31" maxInclusive="-1"</span></span><br/><br/> <span data-ttu-id="5a192-325">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-325">Required</span></span> |<span data-ttu-id="5a192-326">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="5a192-326">**xs:int**</span></span> |<span data-ttu-id="5a192-327">DialogNormalization gerado através de DPLM, necessário quando LoudnessMetering é definido</span><span class="sxs-lookup"><span data-stu-id="5a192-327">DialogNormalization generated through DPLM, required when LoudnessMetering is set</span></span> |
| <span data-ttu-id="5a192-328">**IntegratedLoudness**</span><span class="sxs-lookup"><span data-stu-id="5a192-328">**IntegratedLoudness**</span></span><br/><br/> <span data-ttu-id="5a192-329">minInclusive="-70" maxInclusive="10"</span><span class="sxs-lookup"><span data-stu-id="5a192-329">minInclusive="-70" maxInclusive="10"</span></span><br/><br/> <span data-ttu-id="5a192-330">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-330">Required</span></span> |<span data-ttu-id="5a192-331">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="5a192-331">**xs:float**</span></span> |<span data-ttu-id="5a192-332">Intensidade integrada</span><span class="sxs-lookup"><span data-stu-id="5a192-332">Integrated loudness</span></span> |
| <span data-ttu-id="5a192-333">**IntegratedLoudnessUnit**</span><span class="sxs-lookup"><span data-stu-id="5a192-333">**IntegratedLoudnessUnit**</span></span><br/><br/> <span data-ttu-id="5a192-334">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-334">Required</span></span> |<span data-ttu-id="5a192-335">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="5a192-335">**xs:string**</span></span> |<span data-ttu-id="5a192-336">Unidade de intensidade integrada.</span><span class="sxs-lookup"><span data-stu-id="5a192-336">Integrated loudness unit.</span></span> |
| <span data-ttu-id="5a192-337">**IntegratedLoudnessGatingMethod**</span><span class="sxs-lookup"><span data-stu-id="5a192-337">**IntegratedLoudnessGatingMethod**</span></span><br/><br/> <span data-ttu-id="5a192-338">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-338">Required</span></span> |<span data-ttu-id="5a192-339">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="5a192-339">**xs:string**</span></span> |<span data-ttu-id="5a192-340">Identificador de controle</span><span class="sxs-lookup"><span data-stu-id="5a192-340">Gating identifier</span></span> |
| <span data-ttu-id="5a192-341">**IntegratedLoudnessSpeechPercentage**</span><span class="sxs-lookup"><span data-stu-id="5a192-341">**IntegratedLoudnessSpeechPercentage**</span></span><br/><br/> <span data-ttu-id="5a192-342">minInclusive ="0" maxInclusive="100"</span><span class="sxs-lookup"><span data-stu-id="5a192-342">minInclusive ="0" maxInclusive="100"</span></span> |<span data-ttu-id="5a192-343">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="5a192-343">**xs:float**</span></span> |<span data-ttu-id="5a192-344">Conteúdo de fala sobre programa hello, como uma porcentagem.</span><span class="sxs-lookup"><span data-stu-id="5a192-344">Speech content over hello program, as a percentage.</span></span> |
| <span data-ttu-id="5a192-345">**SamplePeak**</span><span class="sxs-lookup"><span data-stu-id="5a192-345">**SamplePeak**</span></span><br/><br/> <span data-ttu-id="5a192-346">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-346">Required</span></span> |<span data-ttu-id="5a192-347">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="5a192-347">**xs:float**</span></span> |<span data-ttu-id="5a192-348">Valor de pico absoluto de amostra, desde a redefinição ou desde a última limpeza, por canal.</span><span class="sxs-lookup"><span data-stu-id="5a192-348">Peak absolute sample value, since reset or since it was last cleared, per channel.</span></span>  <span data-ttu-id="5a192-349">As unidades são dBFS.</span><span class="sxs-lookup"><span data-stu-id="5a192-349">Units are dBFS.</span></span> |
| <span data-ttu-id="5a192-350">**SamplePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="5a192-350">**SamplePeakUnit**</span></span><br/><br/> <span data-ttu-id="5a192-351">fixed="dBFS"</span><span class="sxs-lookup"><span data-stu-id="5a192-351">fixed="dBFS"</span></span><br/><br/> <span data-ttu-id="5a192-352">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-352">Required</span></span> |<span data-ttu-id="5a192-353">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="5a192-353">**xs:anySimpleType**</span></span> |<span data-ttu-id="5a192-354">Unidade de pico de amostra.</span><span class="sxs-lookup"><span data-stu-id="5a192-354">Sample peak unit.</span></span> |
| <span data-ttu-id="5a192-355">**TruePeak**</span><span class="sxs-lookup"><span data-stu-id="5a192-355">**TruePeak**</span></span><br/><br/> <span data-ttu-id="5a192-356">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-356">Required</span></span> |<span data-ttu-id="5a192-357">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="5a192-357">**xs:float**</span></span> |<span data-ttu-id="5a192-358">Valor do pico real máximo, de acordo com ITU-R BS.1770-2, desde a redefinição ou desde a última limpeza, por canal.</span><span class="sxs-lookup"><span data-stu-id="5a192-358">Maximum true peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.</span></span> <span data-ttu-id="5a192-359">As unidades são dBTP.</span><span class="sxs-lookup"><span data-stu-id="5a192-359">Units are dBTP.</span></span> |
| <span data-ttu-id="5a192-360">**TruePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="5a192-360">**TruePeakUnit**</span></span><br/><br/> <span data-ttu-id="5a192-361">fixed="dBTP"</span><span class="sxs-lookup"><span data-stu-id="5a192-361">fixed="dBTP"</span></span><br/><br/> <span data-ttu-id="5a192-362">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a192-362">Required</span></span> |<span data-ttu-id="5a192-363">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="5a192-363">**xs:anySimpleType**</span></span> |<span data-ttu-id="5a192-364">Unidade de pico real.</span><span class="sxs-lookup"><span data-stu-id="5a192-364">True peak unit.</span></span> |

## <a name="schema-code"></a><span data-ttu-id="5a192-365">Código de Esquema</span><span class="sxs-lookup"><span data-stu-id="5a192-365">Schema Code</span></span>
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



## <span data-ttu-id="5a192-366"><a name="xml"></a> Exemplo de XML</span><span class="sxs-lookup"><span data-stu-id="5a192-366"><a name="xml"></a> XML example</span></span>
 <span data-ttu-id="5a192-367">a seguir Olá é um exemplo hello metadados do arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="5a192-367">hello following is an example of hello Output metadata file.</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="5a192-368">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5a192-368">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5a192-369">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="5a192-369">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
