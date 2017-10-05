---
title: "Visão geral do empacotamento dinâmico dos Serviços de Mídia do Azure | Microsoft Docs"
description: "O tópico apresenta uma visão geral do empacotamento dinâmico."
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
ms.openlocfilehash: 2d212599302fced3f60085ab30cdeaefc1ee2e6a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="dynamic-packaging"></a><span data-ttu-id="91f46-103">Empacotamento dinâmico</span><span class="sxs-lookup"><span data-stu-id="91f46-103">Dynamic packaging</span></span>
## <a name="overview"></a><span data-ttu-id="91f46-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="91f46-104">Overview</span></span>
<span data-ttu-id="91f46-105">Os Serviços de Mídia do Microsoft Azure podem ser usados para fornecer vários formatos de arquivos de mídia de origem, formatos de streaming de mídia e formatos de proteção de conteúdo para uma variedade de tecnologias de cliente (por exemplo, iOS, XBOX, Silverlight, Windows 8).</span><span class="sxs-lookup"><span data-stu-id="91f46-105">Microsoft Azure Media Services can be used to deliver many media source file formats, media streaming formats, and content protection formats to a variety of client technologies (for example, iOS, XBOX, Silverlight, Windows 8).</span></span> <span data-ttu-id="91f46-106">Esses clientes entendem protocolos diferentes, por exemplo: o iOS requer um formato HTTP Live Streaming (HLS) V4, enquanto Silverlight e Xbox requerem Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="91f46-106">These clients understand different protocols, for example iOS requires an HTTP Live Streaming (HLS) V4 format and Silverlight and Xbox require Smooth Streaming.</span></span> <span data-ttu-id="91f46-107">Se você tiver um conjunto de arquivos MP4 (mídia base ISO 14496-12) de taxa de bits adaptável (múltiplas taxas de bits), ou um conjunto de arquivos Smooth Streaming de taxa de bits adaptável que você deseja fornecer a clientes que entendam MPEG DASH, HLS ou Smooth Streaming, você deve tirar proveito do empacotamento dinâmico dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="91f46-107">If you have a set of adaptive bitrate (multi-bitrate) MP4 (ISO Base Media 14496-12) files or a set of adaptive bitrate Smooth Streaming files that you want to serve to clients that understand MPEG DASH, HLS or Smooth Streaming, you should take advantage of Media Services dynamic packaging.</span></span>

<span data-ttu-id="91f46-108">Com o empacotamento dinâmico, tudo o que você precisa é criar um ativo que contenha um conjunto de arquivos MP4 de taxa de bits adaptável ou arquivos de Smooth Streaming de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="91f46-108">With dynamic packaging all you need is to create an asset that contains a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="91f46-109">Em seguida, com base no formato especificado na solicitação de fragmento ou manifesto, o servidor de Streaming OnDemand garantirá que você receba o fluxo no protocolo escolhido por você.</span><span class="sxs-lookup"><span data-stu-id="91f46-109">Then, based on the specified format in the manifest or fragment request, the On-Demand Streaming server will ensure that you receive the stream in the protocol you have chosen.</span></span> <span data-ttu-id="91f46-110">Como resultado você só precisa armazenar e pagar pelos arquivos em um único formato de armazenamento, e os Serviços de Mídia vão criar e fornecer a resposta apropriada com base nas solicitações de um cliente.</span><span class="sxs-lookup"><span data-stu-id="91f46-110">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="91f46-111">O diagrama a seguir mostra a codificação tradicional e o fluxo de trabalho de empacotamento estático.</span><span class="sxs-lookup"><span data-stu-id="91f46-111">The following diagram shows the traditional encoding and static packaging workflow.</span></span>

![Codificação estática](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

<span data-ttu-id="91f46-113">O diagrama a seguir mostra o fluxo de trabalho de empacotamento dinâmico.</span><span class="sxs-lookup"><span data-stu-id="91f46-113">The following diagram shows the dynamic packaging workflow.</span></span>

![Codificação dinâmica](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a><span data-ttu-id="91f46-115">Cenário comum</span><span class="sxs-lookup"><span data-stu-id="91f46-115">Common scenario</span></span>
1. <span data-ttu-id="91f46-116">Carrega um arquivo de entrada (chamado de arquivo de mezanino).</span><span class="sxs-lookup"><span data-stu-id="91f46-116">Upload an input file (called a mezzanine file).</span></span> <span data-ttu-id="91f46-117">Por exemplo, H.264, MP4 ou WMV (para obter a lista de formatos com suporte, consulte [Formatos com suporte do Codificador de Mídia Padrão](media-services-media-encoder-standard-formats.md)).</span><span class="sxs-lookup"><span data-stu-id="91f46-117">For example, H.264, MP4, or WMV (for the list of supported formats see [Formats Supported by the Media Encoder Standard](media-services-media-encoder-standard-formats.md).</span></span>
2. <span data-ttu-id="91f46-118">Codifique o arquivo de mezanino para conjuntos de taxa de bits adaptável MP4 H.264.</span><span class="sxs-lookup"><span data-stu-id="91f46-118">Encode your mezzanine file to H.264 MP4 adaptive bitrate sets.</span></span>
3. <span data-ttu-id="91f46-119">Publique o ativo que contém a taxa de bits adaptável MP4 definida ao criar o localizador OnDemand.</span><span class="sxs-lookup"><span data-stu-id="91f46-119">Publish the asset that contains the adaptive bitrate MP4 set by creating the On-Demand Locator.</span></span>
4. <span data-ttu-id="91f46-120">Crie as URLs de streaming para acessar e transmitir seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="91f46-120">Build the streaming URLs to access and stream your content.</span></span>

## <a name="preparing-assets-for-dynamic-streaming"></a><span data-ttu-id="91f46-121">Preparação de ativos para streaming dinâmico</span><span class="sxs-lookup"><span data-stu-id="91f46-121">Preparing assets for dynamic streaming</span></span>
<span data-ttu-id="91f46-122">Para preparar o ativo de streaming dinâmico você tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="91f46-122">To prepare your asset for dynamic streaming you have two options:</span></span>

1. <span data-ttu-id="91f46-123">[Carregue um arquivo mestre](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="91f46-123">[Upload a master file](media-services-dotnet-upload-files.md).</span></span>
2. <span data-ttu-id="91f46-124">[Use o Codificador de Mídia Padrão para produzir conjuntos de taxa de bits adaptáveis MP4 H.264](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="91f46-124">[Use the Media Encoder Standard encoder to produce H.264 MP4 adaptive bitrate sets](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>
3. <span data-ttu-id="91f46-125">[Transmita seu conteúdo](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="91f46-125">[Stream your content](media-services-deliver-content-overview.md).</span></span>

## <span data-ttu-id="91f46-126"><a id="unsupported_formats"></a>Formatos sem suporte pelo empacotamento dinâmico</span><span class="sxs-lookup"><span data-stu-id="91f46-126"><a id="unsupported_formats"></a>Formats that are not supported by dynamic packaging</span></span>
<span data-ttu-id="91f46-127">Os formatos de arquivo de origem a seguir não têm suporte pelo empacotamento dinâmico.</span><span class="sxs-lookup"><span data-stu-id="91f46-127">The following source file formats are not supported by dynamic packaging.</span></span>

* <span data-ttu-id="91f46-128">Arquivos mp4 Dolby digital.</span><span class="sxs-lookup"><span data-stu-id="91f46-128">Dolby digital mp4 files.</span></span>
* <span data-ttu-id="91f46-129">Arquivos suaves Dolby digital.</span><span class="sxs-lookup"><span data-stu-id="91f46-129">Dolby digital smooth files.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="91f46-130">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="91f46-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="91f46-131">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="91f46-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

