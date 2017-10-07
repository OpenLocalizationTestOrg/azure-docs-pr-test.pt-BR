---
title: "Visão geral dos serviços de mídia de aaaAzure | Microsoft Docs"
description: "Este tópico oferece uma visão geral dos Serviços de Mídia do Azure"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7a5e9723-c379-446b-b4d6-d0e41bd7d31f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/04/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 81f9f4d9ff75effea30c10fd09449e9d2025f377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-overview"></a><span data-ttu-id="94ad4-103">Visão geral dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="94ad4-103">Azure Media Services overview</span></span> 

<span data-ttu-id="94ad4-104">Serviços de mídia do Microsoft Azure é uma plataforma extensível baseada em nuvem que permite que os desenvolvedores toobuild mídia escalonável gerenciamento e entrega de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="94ad4-104">Microsoft Azure Media Services is an extensible cloud-based platform that enables developers toobuild scalable media management and delivery applications.</span></span> <span data-ttu-id="94ad4-105">Serviços de mídia baseia-se nas APIs de REST que permitem que você toosecurely carregar, armazenar, codificar e empacotar conteúdo de áudio ou vídeo sob demanda e ao vivo streaming entrega toovarious clientes (por exemplo, TV, PC e dispositivos móveis).</span><span class="sxs-lookup"><span data-stu-id="94ad4-105">Media Services is based on REST APIs that enable you toosecurely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery toovarious clients (for example, TV, PC, and mobile devices).</span></span>

<span data-ttu-id="94ad4-106">Você pode compilar fluxos de trabalho de ponta a ponta usando totalmente os serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="94ad4-106">You can build end-to-end workflows using entirely Media Services.</span></span> <span data-ttu-id="94ad4-107">Você também pode escolher toouse componentes de terceiros para algumas partes do fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="94ad4-107">You can also choose toouse third-party components for some parts of your workflow.</span></span> <span data-ttu-id="94ad4-108">Por exemplo, codifique usando um codificador de terceiros.</span><span class="sxs-lookup"><span data-stu-id="94ad4-108">For example, encode using a third-party encoder.</span></span> <span data-ttu-id="94ad4-109">Em seguida, carregue, proteja, empacote e entregue usando os serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="94ad4-109">Then, upload, protect, package, deliver using Media Services.</span></span>

<span data-ttu-id="94ad4-110">Você pode escolher toostream seu conteúdo ao vivo ou fornecer conteúda sob demanda.</span><span class="sxs-lookup"><span data-stu-id="94ad4-110">You can choose toostream your content live or deliver content on-demand.</span></span> <span data-ttu-id="94ad4-111">tópico de saudação também vincula a tópicos relevantes tooother.</span><span class="sxs-lookup"><span data-stu-id="94ad4-111">hello topic also links tooother relevant topics.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="94ad4-112">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="94ad4-112">Media Services learning paths</span></span>
<span data-ttu-id="94ad4-113">Você pode exibir os roteiros de aprendizagem do AMS aqui:</span><span class="sxs-lookup"><span data-stu-id="94ad4-113">You can view AMS learning paths here:</span></span>

* [<span data-ttu-id="94ad4-114">Fluxo de trabalho do streaming ao vivo do AMS</span><span class="sxs-lookup"><span data-stu-id="94ad4-114">AMS Live Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [<span data-ttu-id="94ad4-115">Fluxo de trabalho do streaming sob demanda do AMS</span><span class="sxs-lookup"><span data-stu-id="94ad4-115">AMS on-Demand Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a><span data-ttu-id="94ad4-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="94ad4-116">Prerequisites</span></span>

<span data-ttu-id="94ad4-117">toostart usando serviços de mídia do Azure, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="94ad4-117">toostart using Azure Media Services, you should have hello following:</span></span>

* <span data-ttu-id="94ad4-118">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="94ad4-118">An Azure account.</span></span> <span data-ttu-id="94ad4-119">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="94ad4-119">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="94ad4-120">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="94ad4-120">For details, see [Azure Free Trial](https://azure.microsoft.com).</span></span>
* <span data-ttu-id="94ad4-121">Uma conta de Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="94ad4-121">An Azure Media Services account.</span></span> <span data-ttu-id="94ad4-122">Para obter mais informações, veja [Criar conta](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="94ad4-122">For more information, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="94ad4-123">(Opcional) Configure o ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="94ad4-123">(Optional) Set up development environment.</span></span> <span data-ttu-id="94ad4-124">Escolha .NET ou API REST para seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="94ad4-124">Choose .NET or REST API for your development environment.</span></span> <span data-ttu-id="94ad4-125">Para obter mais informações, veja [Configurar ambiente](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="94ad4-125">For more information, see [Set up environment](media-services-dotnet-how-to-use.md).</span></span>

    <span data-ttu-id="94ad4-126">Além disso, saiba como muito[conectar programaticamente tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="94ad4-126">Also, learn how too[connect  programmatically tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
* <span data-ttu-id="94ad4-127">Um ponto de extremidade de streaming padrão ou premium em estado iniciado.</span><span class="sxs-lookup"><span data-stu-id="94ad4-127">A standard or premium streaming endpoint in started state.</span></span>  <span data-ttu-id="94ad4-128">Para obter mais informações, consulte [Gerenciando pontos de extremidade de streaming](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="94ad4-128">For more information, see [Managing streaming endpoints](media-services-portal-manage-streaming-endpoints.md)</span></span>

## <a name="sdks-and-tools"></a><span data-ttu-id="94ad4-129">SDKs e ferramentas</span><span class="sxs-lookup"><span data-stu-id="94ad4-129">SDKs and tools</span></span>

<span data-ttu-id="94ad4-130">soluções de serviços de mídia toobuild, você pode usar:</span><span class="sxs-lookup"><span data-stu-id="94ad4-130">toobuild Media Services solutions, you can use:</span></span>

* [<span data-ttu-id="94ad4-131">API REST dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="94ad4-131">Media Services REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* <span data-ttu-id="94ad4-132">Um dos clientes disponíveis da saudação SDKs:</span><span class="sxs-lookup"><span data-stu-id="94ad4-132">One of hello available client SDKs:</span></span>
    * <span data-ttu-id="94ad4-133">[SDK dos Serviços de Mídia do Azure para .NET](https://github.com/Azure/azure-sdk-for-media-services),</span><span class="sxs-lookup"><span data-stu-id="94ad4-133">[Azure Media Services SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services),</span></span>
    * <span data-ttu-id="94ad4-134">[SDK do Azure para Java](https://github.com/Azure/azure-sdk-for-java),</span><span class="sxs-lookup"><span data-stu-id="94ad4-134">[Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java),</span></span>
    * <span data-ttu-id="94ad4-135">[SDK do PHP do Azure](https://github.com/Azure/azure-sdk-for-php),</span><span class="sxs-lookup"><span data-stu-id="94ad4-135">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),</span></span>
    * <span data-ttu-id="94ad4-136">[Serviços de Mídia do Azure para Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (esta é uma versão de um SDK do Node.js que não foi criada pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="94ad4-136">[Azure Media Services for Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (This is a non-Microsoft version of a Node.js SDK.</span></span> <span data-ttu-id="94ad4-137">É mantido por uma comunidade e atualmente não tem 100% de cobertura de saudação AMS APIs).</span><span class="sxs-lookup"><span data-stu-id="94ad4-137">It is maintained by a community and currently does not have a 100% coverage of hello AMS APIs).</span></span>
* <span data-ttu-id="94ad4-138">Ferramentas existentes:</span><span class="sxs-lookup"><span data-stu-id="94ad4-138">Existing tools:</span></span>
    * [<span data-ttu-id="94ad4-139">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="94ad4-139">Azure portal</span></span>](https://portal.azure.com/)
    * <span data-ttu-id="94ad4-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) ([AMSE] Gerenciador de Serviços de Mídia do Azure é um aplicativo Winforms/C# para Windows)</span><span class="sxs-lookup"><span data-stu-id="94ad4-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) is a Winforms/C# application for Windows)</span></span>

## <a name="concepts-and-overview"></a><span data-ttu-id="94ad4-141">Visão geral e conceitos</span><span class="sxs-lookup"><span data-stu-id="94ad4-141">Concepts and overview</span></span>
<span data-ttu-id="94ad4-142">Para conferir os conceitos dos Serviços de Mídia do Azure, confira [Conceitos](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="94ad4-142">For Azure Media Services concepts, see [Concepts](media-services-concepts.md).</span></span>

<span data-ttu-id="94ad4-143">Para um como-tooseries que apresenta a você tooall Olá principais componentes de serviços de mídia do Azure, consulte [tutoriais passo a passo de serviços de mídia do Azure](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span><span class="sxs-lookup"><span data-stu-id="94ad4-143">For a how-tooseries that introduces you tooall hello main components of Azure Media Services, see [Azure Media Services Step-by-Step tutorials](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span></span> <span data-ttu-id="94ad4-144">Esta série tem uma visão geral de conceitos e usa tarefas de toodemonstrate AMS Olá AMSE ferramenta.</span><span class="sxs-lookup"><span data-stu-id="94ad4-144">This series has a great overview of concepts and it uses hello AMSE tool toodemonstrate AMS tasks.</span></span> <span data-ttu-id="94ad4-145">A ferramenta AMSE é uma ferramenta do Windows.</span><span class="sxs-lookup"><span data-stu-id="94ad4-145">AMSE tool is a Windows tool.</span></span> <span data-ttu-id="94ad4-146">Essa ferramenta oferece suporte à maioria das tarefas de saudação, você pode obter por meio de programação com [AMS SDK para .NET](https://github.com/Azure/azure-sdk-for-media-services), [SDK do Azure para Java](https://github.com/Azure/azure-sdk-for-java), ou [SDK PHP do Azure](https://github.com/Azure/azure-sdk-for-php).</span><span class="sxs-lookup"><span data-stu-id="94ad4-146">This tool supports most of hello tasks you can achieve programmatically with [AMS SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java), or  [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).</span></span>

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a><span data-ttu-id="94ad4-147">Cenários com suporte e disponibilidade dos Serviços de Mídia em data centers</span><span class="sxs-lookup"><span data-stu-id="94ad4-147">Supported scenarios and availability of Media Services across data centers</span></span>

<span data-ttu-id="94ad4-148">Para obter informações detalhadas, veja [Cenários do AMS e disponibilidade de recursos e serviços nos data centers](scenarios-and-availability.md).</span><span class="sxs-lookup"><span data-stu-id="94ad4-148">For detailed information, see [AMS scenarios and availability of features and services across data centers](scenarios-and-availability.md).</span></span>

## <a name="service-level-agreement-sla"></a><span data-ttu-id="94ad4-149">Contrato de nível de serviço (SLA)</span><span class="sxs-lookup"><span data-stu-id="94ad4-149">Service Level Agreement (SLA)</span></span>

* <span data-ttu-id="94ad4-150">Para a Codificação dos Serviços de mídia, garantimos a disponibilidade de 99,9% de transações de API REST.</span><span class="sxs-lookup"><span data-stu-id="94ad4-150">For Media Services Encoding, we guarantee 99.9% availability of REST API transactions.</span></span>
* <span data-ttu-id="94ad4-151">Para streaming, atenderemos com êxito a solicitações com uma garantia de disponibilidade de 99,9% para conteúdos de mídia existentes quando um ponto de extremidade de streaming padrão ou premium for adquirido.</span><span class="sxs-lookup"><span data-stu-id="94ad4-151">For Streaming, we will successfully service requests with a 99.9% availability guarantee for existing media content when a standard or premium streaming endpoint is purchased.</span></span>
* <span data-ttu-id="94ad4-152">Para canais ao vivo, garantimos que executar canais terão conectividade externa pelo menos 99,9% de tempo de saudação.</span><span class="sxs-lookup"><span data-stu-id="94ad4-152">For Live Channels, we guarantee that running Channels will have external connectivity at least 99.9% of hello time.</span></span>
* <span data-ttu-id="94ad4-153">Para proteção de conteúdo, garantimos que podemos com êxito atenderá solicitações de chave pelo menos 99,9% de tempo de saudação.</span><span class="sxs-lookup"><span data-stu-id="94ad4-153">For Content Protection, we guarantee that we will successfully fulfill key requests at least 99.9% of hello time.</span></span>
* <span data-ttu-id="94ad4-154">Para o indexador, podemos com êxito atenderá solicitações de tarefa do indexador processadas com um codificação reservado unidade 99,9% de tempo de saudação.</span><span class="sxs-lookup"><span data-stu-id="94ad4-154">For Indexer, we will successfully service Indexer Task requests processed with an Encoding Reserved Unit 99.9% of hello time.</span></span>

<span data-ttu-id="94ad4-155">Para obter mais informações, veja [SLA do Microsoft Azure](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="94ad4-155">For more information, see [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/).</span></span>

<span data-ttu-id="94ad4-156">Para obter informações sobre a disponibilidade em data centers, consulte Olá [Avaiability](scenarios-and-availability.md#availability) seção.</span><span class="sxs-lookup"><span data-stu-id="94ad4-156">For information about availability in datacenters, see hello [Avaiability](scenarios-and-availability.md#availability) section.</span></span>

## <a name="support"></a><span data-ttu-id="94ad4-157">Suporte</span><span class="sxs-lookup"><span data-stu-id="94ad4-157">Support</span></span>

<span data-ttu-id="94ad4-158">[Suporte do Azure](https://azure.microsoft.com/support/options/) fornece opções de suporte do Azure, incluindo os Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="94ad4-158">[Azure Support](https://azure.microsoft.com/support/options/) provides support options for Azure, including Media Services.</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="94ad4-159">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="94ad4-159">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
