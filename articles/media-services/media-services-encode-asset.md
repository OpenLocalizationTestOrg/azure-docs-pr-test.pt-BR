---
title: "aaaOverview e a comparação do Azure na demandam codificadores de mídia | Microsoft Docs"
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
ms.openlocfilehash: 24a3e0a16162b1bebfcde290b6baf2dd8dbfff17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a><span data-ttu-id="d226b-103">Visão geral e comparação de codificadores de mídia sob demanda do Azure</span><span class="sxs-lookup"><span data-stu-id="d226b-103">Overview and comparison of Azure on demand media encoders</span></span>
## <a name="encoding-overview"></a><span data-ttu-id="d226b-104">Visão Geral de Codificação</span><span class="sxs-lookup"><span data-stu-id="d226b-104">Encoding overview</span></span>
<span data-ttu-id="d226b-105">Serviços de mídia do Azure fornece várias opções para Olá codificação de mídia na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="d226b-105">Azure Media Services provides multiple options for hello encoding of media in hello cloud.</span></span>

<span data-ttu-id="d226b-106">Começando com os serviços de mídia, é importante toounderstand diferença de saudação entre codecs e formatos de arquivo.</span><span class="sxs-lookup"><span data-stu-id="d226b-106">When starting out with Media Services, it is important toounderstand hello difference between codecs and file formats.</span></span>
<span data-ttu-id="d226b-107">Codecs são Olá de software que implementa os algoritmos de compactação/descompactação Olá enquanto formatos de arquivo são contêineres que armazenam o vídeo Olá compactado.</span><span class="sxs-lookup"><span data-stu-id="d226b-107">Codecs are hello software that implements hello compression/decompression algorithms whereas file formats are containers that hold hello compressed video.</span></span>

<span data-ttu-id="d226b-108">Serviços de mídia fornecem empacotamento dinâmico que permite que você toodeliver sua taxa de bits adaptável MP4 ou Smooth Streaming codificado conteúdo de streaming formatos suportados pelo Media Services (MPEG DASH, HLS, Smooth Streaming) sem a necessidade de toore-package nesses formatos de fluxo contínuo.</span><span class="sxs-lookup"><span data-stu-id="d226b-108">Media Services provides dynamic packaging which allows you toodeliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having toore-package into these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="d226b-109">Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado.</span><span class="sxs-lookup"><span data-stu-id="d226b-109">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="d226b-110">toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado.</span><span class="sxs-lookup"><span data-stu-id="d226b-110">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> <span data-ttu-id="d226b-111">aproveitar tootake [empacotamento dinâmico](media-services-dynamic-packaging-overview.md), você precisa toodo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="d226b-111">tootake advantage of [dynamic packaging](media-services-dynamic-packaging-overview.md), you need toodo hello following:</span></span>
>
><span data-ttu-id="d226b-112">Além disso, codifica o arquivo de origem em um conjunto de arquivos MP4 de taxa de bits adaptável ou arquivos de Smooth Streaming de taxa de bits adaptável (etapas de codificação Olá são demonstradas posteriormente neste tutorial).</span><span class="sxs-lookup"><span data-stu-id="d226b-112">Also, encode your source file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files (hello encoding steps are demonstrated later in this tutorial).</span></span>

<span data-ttu-id="d226b-113">Serviços de mídia oferece suporte a seguinte Olá em codificadores de demanda que são descritos neste artigo:</span><span class="sxs-lookup"><span data-stu-id="d226b-113">Media Services supports hello following on demand encoders that are described in this article:</span></span>

* [<span data-ttu-id="d226b-114">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="d226b-114">Media Encoder Standard</span></span>](media-services-encode-asset.md#media-encoder-standard)
* [<span data-ttu-id="d226b-115">Fluxo de trabalho do Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="d226b-115">Media Encoder Premium Workflow</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

<span data-ttu-id="d226b-116">Este artigo fornece uma visão geral de sob demanda codificadores de mídia e fornece links tooarticles que fornecem informações mais detalhadas.</span><span class="sxs-lookup"><span data-stu-id="d226b-116">This article gives a brief overview of on demand media encoders and provides links tooarticles that give more detailed information.</span></span> <span data-ttu-id="d226b-117">tópico de Olá também fornece a comparação de codificadores hello.</span><span class="sxs-lookup"><span data-stu-id="d226b-117">hello topic also provides comparison of hello encoders.</span></span>

>[!NOTE]
><span data-ttu-id="d226b-118">Por padrão, cada conta dos Serviços de Mídia pode ter uma tarefa de codificação ativa por vez.</span><span class="sxs-lookup"><span data-stu-id="d226b-118">By default each Media Services account can have one active encoding task at a time.</span></span> <span data-ttu-id="d226b-119">Você pode reservar unidades de codificação que permitem que você toohave várias tarefas de codificação em execução simultaneamente, uma para cada unidade reservada de codificação que comprar.</span><span class="sxs-lookup"><span data-stu-id="d226b-119">You can reserve encoding units that allow you toohave multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span></span> <span data-ttu-id="d226b-120">Para saber mais, consulte [Dimensionamento das unidades de codificação](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d226b-120">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span></span>

## <a name="media-encoder-standard"></a><span data-ttu-id="d226b-121">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="d226b-121">Media Encoder Standard</span></span>
### <a name="how-toouse"></a><span data-ttu-id="d226b-122">Como toouse</span><span class="sxs-lookup"><span data-stu-id="d226b-122">How toouse</span></span>
[<span data-ttu-id="d226b-123">Como tooencode com o codificador de mídia padrão</span><span class="sxs-lookup"><span data-stu-id="d226b-123">How tooencode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a><span data-ttu-id="d226b-124">Formatos</span><span class="sxs-lookup"><span data-stu-id="d226b-124">Formats</span></span>
[<span data-ttu-id="d226b-125">Formatos e codecs</span><span class="sxs-lookup"><span data-stu-id="d226b-125">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a><span data-ttu-id="d226b-126">Predefinições</span><span class="sxs-lookup"><span data-stu-id="d226b-126">Presets</span></span>
<span data-ttu-id="d226b-127">Codificador de mídia padrão é configurado usando uma das predefinições de codificador Olá descritas [aqui](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="d226b-127">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="d226b-128">Metadados de entrada e saída</span><span class="sxs-lookup"><span data-stu-id="d226b-128">Input and output metadata</span></span>
<span data-ttu-id="d226b-129">Olá codificadores metadados de entrada é descrito [aqui](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="d226b-129">hello encoders input metadata is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="d226b-130">Olá codificadores metadados de saída é descrito [aqui](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="d226b-130">hello encoders output metadata is described [here](media-services-output-metadata-schema.md).</span></span>

### <a name="generate-thumbnails"></a><span data-ttu-id="d226b-131">Gerar miniaturas</span><span class="sxs-lookup"><span data-stu-id="d226b-131">Generate thumbnails</span></span>
<span data-ttu-id="d226b-132">Para obter informações, consulte [como miniaturas toogenerate usando o codificador de mídia padrão](media-services-advanced-encoding-with-mes.md#thumbnails).</span><span class="sxs-lookup"><span data-stu-id="d226b-132">For information, see [How toogenerate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span></span>

### <a name="trim-videos-clipping"></a><span data-ttu-id="d226b-133">Cortar vídeos (recorte)</span><span class="sxs-lookup"><span data-stu-id="d226b-133">Trim videos (clipping)</span></span>
<span data-ttu-id="d226b-134">Para obter informações, consulte [como vídeos tootrim usando o codificador de mídia padrão](media-services-advanced-encoding-with-mes.md#trim_video).</span><span class="sxs-lookup"><span data-stu-id="d226b-134">For information, see [How tootrim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span></span>

### <a name="create-overlays"></a><span data-ttu-id="d226b-135">Criar sobreposições</span><span class="sxs-lookup"><span data-stu-id="d226b-135">Create overlays</span></span>
<span data-ttu-id="d226b-136">Para obter informações, consulte [como sobreposições toocreate usando o codificador de mídia padrão](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="d226b-136">For information, see [How toocreate overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

### <a name="see-also"></a><span data-ttu-id="d226b-137">Consulte também</span><span class="sxs-lookup"><span data-stu-id="d226b-137">See also</span></span>
[<span data-ttu-id="d226b-138">blog de serviços de mídia Olá</span><span class="sxs-lookup"><span data-stu-id="d226b-138">hello Media Services blog</span></span>](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a><span data-ttu-id="d226b-139">Fluxo de trabalho do Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="d226b-139">Media Encoder Premium Workflow</span></span>
### <a name="overview"></a><span data-ttu-id="d226b-140">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d226b-140">Overview</span></span>
[<span data-ttu-id="d226b-141">Apresentando a codificação Premium nos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="d226b-141">Introducing Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-toouse"></a><span data-ttu-id="d226b-142">Como toouse</span><span class="sxs-lookup"><span data-stu-id="d226b-142">How toouse</span></span>
<span data-ttu-id="d226b-143">O fluxo de trabalho do Media Encoder Premium é configurado usando fluxos de trabalho complexos.</span><span class="sxs-lookup"><span data-stu-id="d226b-143">Media Encoder Premium Workflow is configured using complex workflows.</span></span> <span data-ttu-id="d226b-144">Arquivos de fluxo de trabalho pode ser criados e atualizado com hello [Designer de fluxo de trabalho](media-services-workflow-designer.md) ferramenta.</span><span class="sxs-lookup"><span data-stu-id="d226b-144">Workflow files could be created and updated using hello [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

[<span data-ttu-id="d226b-145">Como tooUse Premium de codificação no Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="d226b-145">How tooUse Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a><span data-ttu-id="d226b-146">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="d226b-146">Known issues</span></span>
<span data-ttu-id="d226b-147">Se o vídeo de entrada não contém a legenda codificada, Olá saída que ativo ainda conterá um arquivo TTML vazio.</span><span class="sxs-lookup"><span data-stu-id="d226b-147">If your input video does not contain closed captioning, hello output Asset will still contain an empty TTML file.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="d226b-148">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="d226b-148">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d226b-149">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="d226b-149">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="d226b-150">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="d226b-150">Related articles</span></span>
* [<span data-ttu-id="d226b-151">Executar tarefas avançadas de codificação ao personalizar predefinições do Codificador de Mídia Padrão</span><span class="sxs-lookup"><span data-stu-id="d226b-151">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="d226b-152">Cotas e limitações</span><span class="sxs-lookup"><span data-stu-id="d226b-152">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
