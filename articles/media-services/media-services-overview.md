---
title: "Visão geral dos Serviços de Mídia do Azure | Microsoft Docs"
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
ms.openlocfilehash: 2a175aed40b9775d9a4de6877eb3467b43819568
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-media-services-overview"></a><span data-ttu-id="9e9f0-103">Visão geral dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="9e9f0-103">Azure Media Services overview</span></span> 

<span data-ttu-id="9e9f0-104">Os Serviços de Mídia do Microsoft Azure tratam-se de uma plataforma extensível baseada em nuvem que permite aos desenvolvedores compilar aplicativos de gerenciamento e entrega de mídia escalonável.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-104">Microsoft Azure Media Services is an extensible cloud-based platform that enables developers to build scalable media management and delivery applications.</span></span> <span data-ttu-id="9e9f0-105">Os serviços de mídia se baseiam em APIs REST que permitem que você carregue com segurança, armazene, codifique e empacote o conteúdo de áudio ou vídeo para entrega de streaming sob demanda e ao vivo para vários clientes (por exemplo, TV, PCs e dispositivos móveis).</span><span class="sxs-lookup"><span data-stu-id="9e9f0-105">Media Services is based on REST APIs that enable you to securely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery to various clients (for example, TV, PC, and mobile devices).</span></span>

<span data-ttu-id="9e9f0-106">Você pode compilar fluxos de trabalho de ponta a ponta usando totalmente os serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-106">You can build end-to-end workflows using entirely Media Services.</span></span> <span data-ttu-id="9e9f0-107">Você também pode optar por usar componentes de terceiros para algumas partes do seu fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-107">You can also choose to use third-party components for some parts of your workflow.</span></span> <span data-ttu-id="9e9f0-108">Por exemplo, codifique usando um codificador de terceiros.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-108">For example, encode using a third-party encoder.</span></span> <span data-ttu-id="9e9f0-109">Em seguida, carregue, proteja, empacote e entregue usando os serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-109">Then, upload, protect, package, deliver using Media Services.</span></span>

<span data-ttu-id="9e9f0-110">Você pode optar por transmitir seu conteúdo ao vivo ou fornecer conteúdo sob demanda.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-110">You can choose to stream your content live or deliver content on-demand.</span></span> <span data-ttu-id="9e9f0-111">O tópico também está vinculado a outros tópicos relevantes.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-111">The topic also links to other relevant topics.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="9e9f0-112">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="9e9f0-112">Media Services learning paths</span></span>
<span data-ttu-id="9e9f0-113">Você pode exibir os roteiros de aprendizagem do AMS aqui:</span><span class="sxs-lookup"><span data-stu-id="9e9f0-113">You can view AMS learning paths here:</span></span>

* [<span data-ttu-id="9e9f0-114">Fluxo de trabalho do streaming ao vivo do AMS</span><span class="sxs-lookup"><span data-stu-id="9e9f0-114">AMS Live Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [<span data-ttu-id="9e9f0-115">Fluxo de trabalho do streaming sob demanda do AMS</span><span class="sxs-lookup"><span data-stu-id="9e9f0-115">AMS on-Demand Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a><span data-ttu-id="9e9f0-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9e9f0-116">Prerequisites</span></span>

<span data-ttu-id="9e9f0-117">Para começar a usar o Azure Media Services, você deve possuir o seguinte:</span><span class="sxs-lookup"><span data-stu-id="9e9f0-117">To start using Azure Media Services, you should have the following:</span></span>

* <span data-ttu-id="9e9f0-118">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-118">An Azure account.</span></span> <span data-ttu-id="9e9f0-119">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-119">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9e9f0-120">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="9e9f0-120">For details, see [Azure Free Trial](https://azure.microsoft.com).</span></span>
* <span data-ttu-id="9e9f0-121">Uma conta de Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-121">An Azure Media Services account.</span></span> <span data-ttu-id="9e9f0-122">Para obter mais informações, veja [Criar conta](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="9e9f0-122">For more information, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="9e9f0-123">(Opcional) Configure o ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-123">(Optional) Set up development environment.</span></span> <span data-ttu-id="9e9f0-124">Escolha .NET ou API REST para seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-124">Choose .NET or REST API for your development environment.</span></span> <span data-ttu-id="9e9f0-125">Para obter mais informações, veja [Configurar ambiente](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="9e9f0-125">For more information, see [Set up environment](media-services-dotnet-how-to-use.md).</span></span>

    <span data-ttu-id="9e9f0-126">Além disso, saiba como [conectar-se programaticamente à API do AMS](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="9e9f0-126">Also, learn how to [connect  programmatically to AMS API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
* <span data-ttu-id="9e9f0-127">Um ponto de extremidade de streaming padrão ou premium em estado iniciado.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-127">A standard or premium streaming endpoint in started state.</span></span>  <span data-ttu-id="9e9f0-128">Para obter mais informações, consulte [Gerenciando pontos de extremidade de streaming](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="9e9f0-128">For more information, see [Managing streaming endpoints](media-services-portal-manage-streaming-endpoints.md)</span></span>

## <a name="sdks-and-tools"></a><span data-ttu-id="9e9f0-129">SDKs e ferramentas</span><span class="sxs-lookup"><span data-stu-id="9e9f0-129">SDKs and tools</span></span>

<span data-ttu-id="9e9f0-130">Para compilar soluções de serviços de mídia, você pode usar:</span><span class="sxs-lookup"><span data-stu-id="9e9f0-130">To build Media Services solutions, you can use:</span></span>

* [<span data-ttu-id="9e9f0-131">API REST dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="9e9f0-131">Media Services REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* <span data-ttu-id="9e9f0-132">Um dos SDKs de cliente disponíveis:</span><span class="sxs-lookup"><span data-stu-id="9e9f0-132">One of the available client SDKs:</span></span>
    * <span data-ttu-id="9e9f0-133">[SDK dos Serviços de Mídia do Azure para .NET](https://github.com/Azure/azure-sdk-for-media-services),</span><span class="sxs-lookup"><span data-stu-id="9e9f0-133">[Azure Media Services SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services),</span></span>
    * <span data-ttu-id="9e9f0-134">[SDK do Azure para Java](https://github.com/Azure/azure-sdk-for-java),</span><span class="sxs-lookup"><span data-stu-id="9e9f0-134">[Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java),</span></span>
    * <span data-ttu-id="9e9f0-135">[SDK do PHP do Azure](https://github.com/Azure/azure-sdk-for-php),</span><span class="sxs-lookup"><span data-stu-id="9e9f0-135">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),</span></span>
    * <span data-ttu-id="9e9f0-136">[Serviços de Mídia do Azure para Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (esta é uma versão de um SDK do Node.js que não foi criada pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-136">[Azure Media Services for Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (This is a non-Microsoft version of a Node.js SDK.</span></span> <span data-ttu-id="9e9f0-137">Ele é mantido por uma comunidade e atualmente não tem cobertura de 100% das APIs do AMS).</span><span class="sxs-lookup"><span data-stu-id="9e9f0-137">It is maintained by a community and currently does not have a 100% coverage of the AMS APIs).</span></span>
* <span data-ttu-id="9e9f0-138">Ferramentas existentes:</span><span class="sxs-lookup"><span data-stu-id="9e9f0-138">Existing tools:</span></span>
    * [<span data-ttu-id="9e9f0-139">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9e9f0-139">Azure portal</span></span>](https://portal.azure.com/)
    * <span data-ttu-id="9e9f0-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) ([AMSE] Gerenciador de Serviços de Mídia do Azure é um aplicativo Winforms/C# para Windows)</span><span class="sxs-lookup"><span data-stu-id="9e9f0-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) is a Winforms/C# application for Windows)</span></span>

## <a name="concepts-and-overview"></a><span data-ttu-id="9e9f0-141">Visão geral e conceitos</span><span class="sxs-lookup"><span data-stu-id="9e9f0-141">Concepts and overview</span></span>
<span data-ttu-id="9e9f0-142">Para conferir os conceitos dos Serviços de Mídia do Azure, confira [Conceitos](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="9e9f0-142">For Azure Media Services concepts, see [Concepts](media-services-concepts.md).</span></span>

<span data-ttu-id="9e9f0-143">Para uma série de instruções que apresenta a todos os componentes principais dos Serviços de Mídia do Azure, confira [Tutoriais passo a passo dos Serviços de Mídia do Azure](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span><span class="sxs-lookup"><span data-stu-id="9e9f0-143">For a how-to series that introduces you to all the main components of Azure Media Services, see [Azure Media Services Step-by-Step tutorials](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span></span> <span data-ttu-id="9e9f0-144">Este série apresenta uma ótima visão geral dos conceitos e usa a ferramenta AMSE para demonstrar as tarefas de AMS.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-144">This series has a great overview of concepts and it uses the AMSE tool to demonstrate AMS tasks.</span></span> <span data-ttu-id="9e9f0-145">A ferramenta AMSE é uma ferramenta do Windows.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-145">AMSE tool is a Windows tool.</span></span> <span data-ttu-id="9e9f0-146">Essa ferramenta dá suporte à maioria das tarefas que você pode obter programaticamente com o [SDK do AMS para .NET](https://github.com/Azure/azure-sdk-for-media-services), [SDK do Azure para Java](https://github.com/Azure/azure-sdk-for-java) ou [SDK do PHP do Azure](https://github.com/Azure/azure-sdk-for-php).</span><span class="sxs-lookup"><span data-stu-id="9e9f0-146">This tool supports most of the tasks you can achieve programmatically with [AMS SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java), or  [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).</span></span>

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a><span data-ttu-id="9e9f0-147">Cenários com suporte e disponibilidade dos Serviços de Mídia em data centers</span><span class="sxs-lookup"><span data-stu-id="9e9f0-147">Supported scenarios and availability of Media Services across data centers</span></span>

<span data-ttu-id="9e9f0-148">Para obter informações detalhadas, veja [Cenários do AMS e disponibilidade de recursos e serviços nos data centers](scenarios-and-availability.md).</span><span class="sxs-lookup"><span data-stu-id="9e9f0-148">For detailed information, see [AMS scenarios and availability of features and services across data centers](scenarios-and-availability.md).</span></span>

## <a name="service-level-agreement-sla"></a><span data-ttu-id="9e9f0-149">Contrato de nível de serviço (SLA)</span><span class="sxs-lookup"><span data-stu-id="9e9f0-149">Service Level Agreement (SLA)</span></span>

* <span data-ttu-id="9e9f0-150">Para a Codificação dos Serviços de mídia, garantimos a disponibilidade de 99,9% de transações de API REST.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-150">For Media Services Encoding, we guarantee 99.9% availability of REST API transactions.</span></span>
* <span data-ttu-id="9e9f0-151">Para streaming, atenderemos com êxito a solicitações com uma garantia de disponibilidade de 99,9% para conteúdos de mídia existentes quando um ponto de extremidade de streaming padrão ou premium for adquirido.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-151">For Streaming, we will successfully service requests with a 99.9% availability guarantee for existing media content when a standard or premium streaming endpoint is purchased.</span></span>
* <span data-ttu-id="9e9f0-152">Para canais ao vivo, garantimos que os canais em execução terão conectividade externa em, no mínimo, 99,9% do tempo.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-152">For Live Channels, we guarantee that running Channels will have external connectivity at least 99.9% of the time.</span></span>
* <span data-ttu-id="9e9f0-153">Para proteção de conteúdo, garantimos que atenderemos com êxito a solicitações de chave em, no mínimo, 99,9% do tempo.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-153">For Content Protection, we guarantee that we will successfully fulfill key requests at least 99.9% of the time.</span></span>
* <span data-ttu-id="9e9f0-154">Para o indexador, podemos atenderemos com êxito às solicitações de tarefa do indexador processadas com uma unidade reservada para codificação em 99,9% do tempo.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-154">For Indexer, we will successfully service Indexer Task requests processed with an Encoding Reserved Unit 99.9% of the time.</span></span>

<span data-ttu-id="9e9f0-155">Para obter mais informações, veja [SLA do Microsoft Azure](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="9e9f0-155">For more information, see [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/).</span></span>

<span data-ttu-id="9e9f0-156">Para saber mais sobre a disponibilidade em data centers, veja a seção [Disponibilidade](scenarios-and-availability.md#availability).</span><span class="sxs-lookup"><span data-stu-id="9e9f0-156">For information about availability in datacenters, see the [Avaiability](scenarios-and-availability.md#availability) section.</span></span>

## <a name="support"></a><span data-ttu-id="9e9f0-157">Suporte</span><span class="sxs-lookup"><span data-stu-id="9e9f0-157">Support</span></span>

<span data-ttu-id="9e9f0-158">[Suporte do Azure](https://azure.microsoft.com/support/options/) fornece opções de suporte do Azure, incluindo os Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="9e9f0-158">[Azure Support](https://azure.microsoft.com/support/options/) provides support options for Azure, including Media Services.</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="9e9f0-159">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="9e9f0-159">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
