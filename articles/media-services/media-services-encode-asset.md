---
title: "Visão geral e comparação de codificadores de mídia sob demanda do Azure | Microsoft Docs"
description: "Este tópico fornece uma visão geral e uma comparação dos codificadores de mídia sob demanda do Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 538a6ab60168735c2626a93cdeedd8d4999a6efc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a><span data-ttu-id="559b9-103">Visão geral e comparação de codificadores de mídia sob demanda do Azure</span><span class="sxs-lookup"><span data-stu-id="559b9-103">Overview and comparison of Azure on demand media encoders</span></span>
## <a name="encoding-overview"></a><span data-ttu-id="559b9-104">Visão Geral de Codificação</span><span class="sxs-lookup"><span data-stu-id="559b9-104">Encoding overview</span></span>
<span data-ttu-id="559b9-105">Os Serviços de Mídia do Azure fornecem várias opções para a codificação de mídia na nuvem.</span><span class="sxs-lookup"><span data-stu-id="559b9-105">Azure Media Services provides multiple options for the encoding of media in the cloud.</span></span>

<span data-ttu-id="559b9-106">Ao começar a usar os Serviços de Mídia é importante compreender a diferença entre codecs e formatos de arquivo.</span><span class="sxs-lookup"><span data-stu-id="559b9-106">When starting out with Media Services, it is important to understand the difference between codecs and file formats.</span></span>
<span data-ttu-id="559b9-107">Codecs são o software que implementa os algoritmos de compactação/descompactação. Já os formatos de arquivo são contêineres que armazenam o vídeo compactado.</span><span class="sxs-lookup"><span data-stu-id="559b9-107">Codecs are the software that implements the compression/decompression algorithms whereas file formats are containers that hold the compressed video.</span></span>

<span data-ttu-id="559b9-108">Os Serviços de Mídia fornecem empacotamento dinâmico, o que permite distribuir seu conteúdo codificado em Smooth Streaming ou MP4 com taxa de bits adaptável em formatos de streaming com suporte dos Serviços de Mídia (MPEG DASH, HLS, Smooth Streaming), sem a necessidade de empacotar novamente nesses formatos de streaming.</span><span class="sxs-lookup"><span data-stu-id="559b9-108">Media Services provides dynamic packaging which allows you to deliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having to re-package into these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="559b9-109">Quando sua conta AMS é criada, um ponto de extremidade de streaming **padrão** é adicionado à sua conta em estado **Parado**.</span><span class="sxs-lookup"><span data-stu-id="559b9-109">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="559b9-110">Para iniciar seu conteúdo de streaming e tirar proveito do empacotamento dinâmico e da criptografia dinâmica, o ponto de extremidade de streaming do qual você deseja transmitir o conteúdo deve estar em estado **Executando**.</span><span class="sxs-lookup"><span data-stu-id="559b9-110">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> <span data-ttu-id="559b9-111">Para aproveitar os benefícios do [empacotamento dinâmico](media-services-dynamic-packaging-overview.md), você precisa fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="559b9-111">To take advantage of [dynamic packaging](media-services-dynamic-packaging-overview.md), you need to do the following:</span></span>
>
><span data-ttu-id="559b9-112">Além disso, codifique seu arquivo de origem em um conjunto de arquivos MP4 de taxa de bits adaptável ou arquivos Smooth Streaming de taxa de bits adaptável (as etapas de codificação são demonstradas mais adiante neste tutorial).</span><span class="sxs-lookup"><span data-stu-id="559b9-112">Also, encode your source file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files (the encoding steps are demonstrated later in this tutorial).</span></span>

<span data-ttu-id="559b9-113">Os Serviços de Mídia são compatíveis com os seguintes codificadores sob demanda descritos neste artigo:</span><span class="sxs-lookup"><span data-stu-id="559b9-113">Media Services supports the following on demand encoders that are described in this article:</span></span>

* [<span data-ttu-id="559b9-114">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="559b9-114">Media Encoder Standard</span></span>](media-services-encode-asset.md#media-encoder-standard)
* [<span data-ttu-id="559b9-115">Fluxo de trabalho do Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="559b9-115">Media Encoder Premium Workflow</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

<span data-ttu-id="559b9-116">Este artigo fornece uma breve visão geral dos codificadores de mídia sob demanda e fornece links para artigos que oferecem informações mais detalhadas.</span><span class="sxs-lookup"><span data-stu-id="559b9-116">This article gives a brief overview of on demand media encoders and provides links to articles that give more detailed information.</span></span> <span data-ttu-id="559b9-117">O tópico também fornece uma comparação entre os codificadores.</span><span class="sxs-lookup"><span data-stu-id="559b9-117">The topic also provides comparison of the encoders.</span></span>

>[!NOTE]
><span data-ttu-id="559b9-118">Por padrão, cada conta dos Serviços de Mídia pode ter uma tarefa de codificação ativa por vez.</span><span class="sxs-lookup"><span data-stu-id="559b9-118">By default each Media Services account can have one active encoding task at a time.</span></span> <span data-ttu-id="559b9-119">Você pode reservar unidades de codificação que permitem ter várias tarefas de codificação em execução simultaneamente, uma para cada unidade reservada de codificação que você comprar.</span><span class="sxs-lookup"><span data-stu-id="559b9-119">You can reserve encoding units that allow you to have multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span></span> <span data-ttu-id="559b9-120">Para saber mais, consulte [Dimensionamento das unidades de codificação](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="559b9-120">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span></span>

## <a name="media-encoder-standard"></a><span data-ttu-id="559b9-121">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="559b9-121">Media Encoder Standard</span></span>
### <a name="how-to-use"></a><span data-ttu-id="559b9-122">Como usar</span><span class="sxs-lookup"><span data-stu-id="559b9-122">How to use</span></span>
[<span data-ttu-id="559b9-123">Como codificar com o Codificador de Mídia Padrão</span><span class="sxs-lookup"><span data-stu-id="559b9-123">How to encode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a><span data-ttu-id="559b9-124">Formatos</span><span class="sxs-lookup"><span data-stu-id="559b9-124">Formats</span></span>
[<span data-ttu-id="559b9-125">Formatos e codecs</span><span class="sxs-lookup"><span data-stu-id="559b9-125">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a><span data-ttu-id="559b9-126">Predefinições</span><span class="sxs-lookup"><span data-stu-id="559b9-126">Presets</span></span>
<span data-ttu-id="559b9-127">O Media Encoder Standard é configurado usando um dos codificadores predefinidos descritos [aqui](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="559b9-127">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="559b9-128">Metadados de entrada e saída</span><span class="sxs-lookup"><span data-stu-id="559b9-128">Input and output metadata</span></span>
<span data-ttu-id="559b9-129">Os metadados de entrada dos codificadores estão descritos [aqui](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="559b9-129">The encoders input metadata is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="559b9-130">Os metadados de saída dos codificadores estão descritos [aqui](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="559b9-130">The encoders output metadata is described [here](media-services-output-metadata-schema.md).</span></span>

### <a name="generate-thumbnails"></a><span data-ttu-id="559b9-131">Gerar miniaturas</span><span class="sxs-lookup"><span data-stu-id="559b9-131">Generate thumbnails</span></span>
<span data-ttu-id="559b9-132">Para obter informações, veja [Como gerar miniaturas usando o Codificador de Mídia Padrão](media-services-advanced-encoding-with-mes.md#thumbnails).</span><span class="sxs-lookup"><span data-stu-id="559b9-132">For information, see [How to generate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span></span>

### <a name="trim-videos-clipping"></a><span data-ttu-id="559b9-133">Cortar vídeos (recorte)</span><span class="sxs-lookup"><span data-stu-id="559b9-133">Trim videos (clipping)</span></span>
<span data-ttu-id="559b9-134">Para obter informações, veja [Como cortar vídeos usando o Codificador de Mídia Padrão](media-services-advanced-encoding-with-mes.md#trim_video).</span><span class="sxs-lookup"><span data-stu-id="559b9-134">For information, see [How to trim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span></span>

### <a name="create-overlays"></a><span data-ttu-id="559b9-135">Criar sobreposições</span><span class="sxs-lookup"><span data-stu-id="559b9-135">Create overlays</span></span>
<span data-ttu-id="559b9-136">Para obter informações, veja [Como criar sobreposições usando o Codificador de Mídia Padrão](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="559b9-136">For information, see [How to create overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

### <a name="see-also"></a><span data-ttu-id="559b9-137">Confira também</span><span class="sxs-lookup"><span data-stu-id="559b9-137">See also</span></span>
[<span data-ttu-id="559b9-138">O blog Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="559b9-138">The Media Services blog</span></span>](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a><span data-ttu-id="559b9-139">Fluxo de trabalho do Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="559b9-139">Media Encoder Premium Workflow</span></span>
### <a name="overview"></a><span data-ttu-id="559b9-140">Visão geral</span><span class="sxs-lookup"><span data-stu-id="559b9-140">Overview</span></span>
[<span data-ttu-id="559b9-141">Apresentando a codificação Premium nos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="559b9-141">Introducing Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-to-use"></a><span data-ttu-id="559b9-142">Como usar</span><span class="sxs-lookup"><span data-stu-id="559b9-142">How to use</span></span>
<span data-ttu-id="559b9-143">O fluxo de trabalho do Media Encoder Premium é configurado usando fluxos de trabalho complexos.</span><span class="sxs-lookup"><span data-stu-id="559b9-143">Media Encoder Premium Workflow is configured using complex workflows.</span></span> <span data-ttu-id="559b9-144">Os arquivos de fluxo de trabalho podem ser criados e atualizados usando a ferramenta [Designer de Fluxo de Trabalho](media-services-workflow-designer.md) .</span><span class="sxs-lookup"><span data-stu-id="559b9-144">Workflow files could be created and updated using the [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

[<span data-ttu-id="559b9-145">Como usar a codificação Premium nos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="559b9-145">How to Use Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a><span data-ttu-id="559b9-146">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="559b9-146">Known issues</span></span>
<span data-ttu-id="559b9-147">Se o vídeo de entrada não contiver a legendagem oculta, o ativo de saída ainda conterá um arquivo TTML vazio.</span><span class="sxs-lookup"><span data-stu-id="559b9-147">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="559b9-148">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="559b9-148">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="559b9-149">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="559b9-149">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="559b9-150">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="559b9-150">Related articles</span></span>
* [<span data-ttu-id="559b9-151">Executar tarefas avançadas de codificação ao personalizar predefinições do Codificador de Mídia Padrão</span><span class="sxs-lookup"><span data-stu-id="559b9-151">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="559b9-152">Cotas e limitações</span><span class="sxs-lookup"><span data-stu-id="559b9-152">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
