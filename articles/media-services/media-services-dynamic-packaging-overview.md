---
title: "Visão geral do empacotamento dinâmico de serviços de mídia aaaAzure | Microsoft Docs"
description: "Olá tópico apresenta e visão geral do empacotamento dinâmico."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0d9e4f54-5daa-45c1-bfaa-cf09ca89b812
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 970e24eba800e098774172c87f56629430b227a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-packaging"></a><span data-ttu-id="76357-103">Empacotamento dinâmico</span><span class="sxs-lookup"><span data-stu-id="76357-103">Dynamic packaging</span></span>
## <a name="overview"></a><span data-ttu-id="76357-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="76357-104">Overview</span></span>
<span data-ttu-id="76357-105">Serviços de mídia do Microsoft Azure pode ser usado toodeliver mídia muitos formatos de arquivo, formatos de streaming de mídia e proteção de conteúdo formatos tooa variedade de tecnologias de cliente de origem (por exemplo, iOS, XBOX, Silverlight, Windows 8).</span><span class="sxs-lookup"><span data-stu-id="76357-105">Microsoft Azure Media Services can be used toodeliver many media source file formats, media streaming formats, and content protection formats tooa variety of client technologies (for example, iOS, XBOX, Silverlight, Windows 8).</span></span> <span data-ttu-id="76357-106">Esses clientes entendem protocolos diferentes, por exemplo: o iOS requer um formato HTTP Live Streaming (HLS) V4, enquanto Silverlight e Xbox requerem Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="76357-106">These clients understand different protocols, for example iOS requires an HTTP Live Streaming (HLS) V4 format and Silverlight and Xbox require Smooth Streaming.</span></span> <span data-ttu-id="76357-107">Se você tiver um conjunto de taxa de bits adaptável (múltiplas taxas de bits) MP4 arquivos (ISO Base Media 14496-12) ou um conjunto de arquivos de Smooth Streaming de taxa de bits adaptável que você deseja tooclients tooserve que compreendam MPEG DASH, HLS ou Smooth Streaming, você deve aproveitar da mídia Serviços de empacotamento dinâmico.</span><span class="sxs-lookup"><span data-stu-id="76357-107">If you have a set of adaptive bitrate (multi-bitrate) MP4 (ISO Base Media 14496-12) files or a set of adaptive bitrate Smooth Streaming files that you want tooserve tooclients that understand MPEG DASH, HLS or Smooth Streaming, you should take advantage of Media Services dynamic packaging.</span></span>

<span data-ttu-id="76357-108">Com o empacotamento dinâmico, tudo o que você precisa é toocreate um ativo que contém um conjunto de arquivos MP4 de taxa de bits adaptável ou arquivos de Smooth Streaming de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="76357-108">With dynamic packaging all you need is toocreate an asset that contains a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="76357-109">Em seguida, com base no formato de saudação especificado no manifesto de saudação ou solicitação de fragmento, Olá sob demanda de Streaming server irá garantir que você receba o fluxo de saudação no protocolo hello escolhido.</span><span class="sxs-lookup"><span data-stu-id="76357-109">Then, based on hello specified format in hello manifest or fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="76357-110">Como resultado, você só precisa toostore e pagamento para arquivos de saudação em único formato de armazenamento e serviços de mídia criará e enviará a resposta apropriada hello, com base nas solicitações de um cliente.</span><span class="sxs-lookup"><span data-stu-id="76357-110">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="76357-111">Olá diagrama a seguir mostra Olá tradicional codificação e fluxo de trabalho de empacotamento estático.</span><span class="sxs-lookup"><span data-stu-id="76357-111">hello following diagram shows hello traditional encoding and static packaging workflow.</span></span>

![Codificação estática](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

<span data-ttu-id="76357-113">Olá diagrama a seguir mostra o fluxo de trabalho do hello empacotamento dinâmico.</span><span class="sxs-lookup"><span data-stu-id="76357-113">hello following diagram shows hello dynamic packaging workflow.</span></span>

![Codificação dinâmica](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a><span data-ttu-id="76357-115">Cenário comum</span><span class="sxs-lookup"><span data-stu-id="76357-115">Common scenario</span></span>
1. <span data-ttu-id="76357-116">Carrega um arquivo de entrada (chamado de arquivo de mezanino).</span><span class="sxs-lookup"><span data-stu-id="76357-116">Upload an input file (called a mezzanine file).</span></span> <span data-ttu-id="76357-117">Por exemplo, h. 264, MP4 ou WMV (para obter lista de saudação de formatos com suporte, consulte [formatos suportados pelo codificador de mídia padrão da saudação](media-services-media-encoder-standard-formats.md).</span><span class="sxs-lookup"><span data-stu-id="76357-117">For example, H.264, MP4, or WMV (for hello list of supported formats see [Formats Supported by hello Media Encoder Standard](media-services-media-encoder-standard-formats.md).</span></span>
2. <span data-ttu-id="76357-118">Codifica seus conjuntos de taxa de bits adaptável mezanino arquivo tooH.264 MP4.</span><span class="sxs-lookup"><span data-stu-id="76357-118">Encode your mezzanine file tooH.264 MP4 adaptive bitrate sets.</span></span>
3. <span data-ttu-id="76357-119">Publica o ativo de saudação que contém a taxa de bits adaptável Olá MP4 set criando Olá localizador sob demanda.</span><span class="sxs-lookup"><span data-stu-id="76357-119">Publish hello asset that contains hello adaptive bitrate MP4 set by creating hello On-Demand Locator.</span></span>
4. <span data-ttu-id="76357-120">Criar hello tooaccess URLs de streaming e transmitir o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="76357-120">Build hello streaming URLs tooaccess and stream your content.</span></span>

## <a name="preparing-assets-for-dynamic-streaming"></a><span data-ttu-id="76357-121">Preparação de ativos para streaming dinâmico</span><span class="sxs-lookup"><span data-stu-id="76357-121">Preparing assets for dynamic streaming</span></span>
<span data-ttu-id="76357-122">tooprepare seu ativo para dinâmico streaming, você tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="76357-122">tooprepare your asset for dynamic streaming you have two options:</span></span>

1. <span data-ttu-id="76357-123">[Carregue um arquivo mestre](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="76357-123">[Upload a master file](media-services-dotnet-upload-files.md).</span></span>
2. <span data-ttu-id="76357-124">[Usar conjuntos de taxa de bits adaptável para Olá codificador de mídia padrão codificador tooproduce MP4 h. 264](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="76357-124">[Use hello Media Encoder Standard encoder tooproduce H.264 MP4 adaptive bitrate sets](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>
3. <span data-ttu-id="76357-125">[Transmita seu conteúdo](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="76357-125">[Stream your content](media-services-deliver-content-overview.md).</span></span>

## <span data-ttu-id="76357-126"><a id="unsupported_formats"></a>Formatos sem suporte pelo empacotamento dinâmico</span><span class="sxs-lookup"><span data-stu-id="76357-126"><a id="unsupported_formats"></a>Formats that are not supported by dynamic packaging</span></span>
<span data-ttu-id="76357-127">Olá seguintes formatos de arquivo de origem não há suporte para empacotamento dinâmico.</span><span class="sxs-lookup"><span data-stu-id="76357-127">hello following source file formats are not supported by dynamic packaging.</span></span>

* <span data-ttu-id="76357-128">Arquivos mp4 Dolby digital.</span><span class="sxs-lookup"><span data-stu-id="76357-128">Dolby digital mp4 files.</span></span>
* <span data-ttu-id="76357-129">Arquivos suaves Dolby digital.</span><span class="sxs-lookup"><span data-stu-id="76357-129">Dolby digital smooth files.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="76357-130">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="76357-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="76357-131">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="76357-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

