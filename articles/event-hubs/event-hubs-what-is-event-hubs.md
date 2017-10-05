---
title: "O que é o Hub de Eventos do Azure e por que usá-lo | Microsoft Docs"
description: "Visão geral e introdução aos Hubs de Eventos do Azure - ingestão de telemetria da escala de nuvem de sites, aplicativos e dispositivos"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm; babanisa
ms.openlocfilehash: 1a6bf0a0352e6d9e3a22586ac825558d12e1307a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-event-hubs"></a><span data-ttu-id="4e3f1-103">O que são Hubs de Eventos?</span><span class="sxs-lookup"><span data-stu-id="4e3f1-103">What is Event Hubs?</span></span>

<span data-ttu-id="4e3f1-104">Os Hubs de Evento do Azure são um plataforma de transmissão de dados altamente dimensionável e um serviço de ingestão de dados capaz de receber e processar milhões de eventos por segundo.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-104">Azure Event Hubs is a highly scalable data streaming platform and event ingestion service capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="4e3f1-105">Os Hubs de Eventos podem processar e armazenar eventos, dados ou telemetria produzidos pelos dispositivos e software distribuídos.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-105">Event Hubs can process and store events, data, or telemetry produced by distributed software and devices.</span></span> <span data-ttu-id="4e3f1-106">Os dados enviados para um Hub de Eventos podem ser transformados e armazenados usando qualquer provedor de análise em tempo real ou adaptadores de envio em lote/armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-106">Data sent to an event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="4e3f1-107">Com a capacidade de fornecer [recursos de publicação/assinatura](https://msdn.microsoft.com/library/aa560414.aspx) com baixa latência e em grande escala, os Hubs de Eventos servem como uma "subida" para Big Data.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-107">With the ability to provide [publish-subscribe capabilities](https://msdn.microsoft.com/library/aa560414.aspx) with low latency and at massive scale, Event Hubs serves as the "on ramp" for Big Data.</span></span>

## <a name="why-use-event-hubs"></a><span data-ttu-id="4e3f1-108">Por que usar Hubs de Eventos?</span><span class="sxs-lookup"><span data-stu-id="4e3f1-108">Why use Event Hubs?</span></span>

<span data-ttu-id="4e3f1-109">Os eventos de Hubs de Eventos e os recursos de manipulação de telemetria o tornam especialmente útil para:</span><span class="sxs-lookup"><span data-stu-id="4e3f1-109">Event Hubs event and telemetry handling capabilities make it especially useful for:</span></span>

* <span data-ttu-id="4e3f1-110">Instrumentação de aplicativos</span><span class="sxs-lookup"><span data-stu-id="4e3f1-110">Application instrumentation</span></span>
* <span data-ttu-id="4e3f1-111">Experiência do usuário ou o processamento de fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="4e3f1-111">User experience or workflow processing</span></span>
* <span data-ttu-id="4e3f1-112">Cenários de IoT (Internet das coisas)</span><span class="sxs-lookup"><span data-stu-id="4e3f1-112">Internet of Things (IoT) scenarios</span></span>

<span data-ttu-id="4e3f1-113">Por exemplo, os Hubs de Eventos habilitam o rastreamento de comportamentos em aplicativos móveis, informações do tráfego de web farms, captura de eventos de jogos em jogos de console ou telemetria coletada de máquinas industriais, veículos conectados ou outros dispositivos.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-113">For example, Event Hubs enables behavior tracking in mobile apps, traffic information from web farms, in-game event capture in console games, or telemetry collected from industrial machines, connected vehicles, or other devices.</span></span>

## <a name="azure-event-hubs-overview"></a><span data-ttu-id="4e3f1-114">Visão geral dos Hubs de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="4e3f1-114">Azure Event Hubs overview</span></span>

<span data-ttu-id="4e3f1-115">A função comum que os Hubs de Evento desempenham em arquiteturas de solução é ser a "porta da frente" de um pipeline de evento, geralmente chamado de *ingestor de eventos*.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-115">The common role that Event Hubs plays in solution architectures is the "front door" for an event pipeline, often called an *event ingestor*.</span></span> <span data-ttu-id="4e3f1-116">Um ingestor de eventos é um componente ou serviço que fica entre os editores de eventos e consumidores de eventos para desacoplar a produção de uma transmissão de eventos do consumo desses eventos.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-116">An event ingestor is a component or service that sits between event publishers and event consumers to decouple the production of an event stream from the consumption of those events.</span></span> <span data-ttu-id="4e3f1-117">A figura a seguir ilustra essa arquitetura:</span><span class="sxs-lookup"><span data-stu-id="4e3f1-117">The following figure depicts this architecture:</span></span>

![Hubs de Eventos](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

<span data-ttu-id="4e3f1-119">Os Hubs de Eventos fornecem recurso de manipulação de fluxo de mensagens, mas têm características que são diferentes das mensagens corporativas tradicionais.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-119">Event Hubs provides message stream handling capability but has characteristics that are different from traditional enterprise messaging.</span></span> <span data-ttu-id="4e3f1-120">Os recursos de Hubs de Eventos são criados em torno de cenários de alta produtividade e de processamento de eventos.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-120">Event Hubs capabilities are built around high throughput and event processing scenarios.</span></span> <span data-ttu-id="4e3f1-121">Assim, os Hubs de Eventos são diferentes das mensagens do [Barramento de Serviço do Azure](https://azure.microsoft.com/services/service-bus/) e não implementam alguns dos recursos que estão disponíveis para entidades de [mensagens do Barramento de Serviço](/azure/service-bus-messaging/), por exemplo, tópicos.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-121">As such, Event Hubs is different from [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) messaging, and does not implement some of the capabilities that are available for [Service Bus messaging](/azure/service-bus-messaging/) entities, such as topics.</span></span>

## <a name="event-hubs-features"></a><span data-ttu-id="4e3f1-122">Recursos de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="4e3f1-122">Event Hubs features</span></span>

<span data-ttu-id="4e3f1-123">Os Hubs de Eventos contêm os seguintes elementos principais:</span><span class="sxs-lookup"><span data-stu-id="4e3f1-123">Event Hubs contains the following key elements:</span></span>

- <span data-ttu-id="4e3f1-124">[**Editores/produtores de eventos**](event-hubs-features.md#event-publishers): uma entidade que envia dados para um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-124">[**Event producers/publishers**](event-hubs-features.md#event-publishers): An entity that sends data to an event hub.</span></span> <span data-ttu-id="4e3f1-125">Um evento é publicado por meio de AMQP 1.0 ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-125">An event is published via AMQP 1.0 or HTTPS.</span></span>
- <span data-ttu-id="4e3f1-126">[**Capturar**](event-hubs-features.md#capture): habilita a captura de dados de transmissão de Hubs de Eventos e o armazenamento em uma conta de armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-126">[**Capture**](event-hubs-features.md#capture): Enables you to capture Event Hubs streaming data and store it in an Azure Blob storage account.</span></span>
- <span data-ttu-id="4e3f1-127">[**Partições**](event-hubs-features.md#partitions): permite que cada consumidor leia apenas um subconjunto específico, ou uma partição, do fluxo de eventos.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-127">[**Partitions**](event-hubs-features.md#partitions): Enables each consumer to only read a specific subset, or partition, of the event stream.</span></span>
- <span data-ttu-id="4e3f1-128">[**Tokens SAS**](event-hubs-features.md#sas-tokens): identifica e autentica o editor do evento.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-128">[**SAS tokens**](event-hubs-features.md#sas-tokens): Identifies and authenticates the event publisher.</span></span>
- <span data-ttu-id="4e3f1-129">[**Consumidores de evento**](event-hubs-features.md#event-consumers): qualquer entidade que leia dados de evento de um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-129">[**Event consumers**](event-hubs-features.md#event-consumers): An entity that reads event data from an event hub.</span></span> <span data-ttu-id="4e3f1-130">Os consumidores do evento se conectam por meio de AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-130">Event consumers connect via AMQP 1.0.</span></span> 
- <span data-ttu-id="4e3f1-131">[**Grupos de consumidores**](event-hubs-features.md#consumer-groups): fornece a cada aplicativo com consumo múltiplo uma exibição separada do fluxo de eventos, permitindo que os consumidores ajam independentemente.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-131">[**Consumer groups**](event-hubs-features.md#consumer-groups): Provides each multiple consuming application with a separate view of the event stream, enabling those consumers to act independently.</span></span>
- <span data-ttu-id="4e3f1-132">[**Unidades de produtividade**](event-hubs-features.md#capacity): unidades de capacidade pré-adquiridas.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-132">[**Throughput units**](event-hubs-features.md#capacity): Pre-purchased units of capacity.</span></span> <span data-ttu-id="4e3f1-133">Uma única partição tem uma escala máxima de 1 unidade de transferência.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-133">A single partition has a maximum scale of 1 throughput unit.</span></span>

<span data-ttu-id="4e3f1-134">Para obter detalhes técnicos sobre esses e outros recursos dos Hubs de Eventos, consulte a [Visão geral dos recursos de Hubs de Eventos](event-hubs-features.md).</span><span class="sxs-lookup"><span data-stu-id="4e3f1-134">For technical details about these and other Event Hubs features, see the [Event Hubs features overview](event-hubs-features.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4e3f1-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4e3f1-135">Next steps</span></span>

<span data-ttu-id="4e3f1-136">Para obter informações sobre preços de Hubs de Evento, consulte [Preços de Hubs de Evento](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="4e3f1-136">For detailed Event Hubs pricing information, see [Event Hubs Pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span>

<span data-ttu-id="4e3f1-137">Para saber mais sobre os Hubs de Eventos, visite os seguintes links:</span><span class="sxs-lookup"><span data-stu-id="4e3f1-137">For more information about Event Hubs, visit the following links:</span></span>

* <span data-ttu-id="4e3f1-138">Introdução com um [Tutorial de Hubs de Eventos](event-hubs-dotnet-standard-getstarted-send.md)</span><span class="sxs-lookup"><span data-stu-id="4e3f1-138">Get started with an [Event Hubs tutorial](event-hubs-dotnet-standard-getstarted-send.md)</span></span>
* [<span data-ttu-id="4e3f1-139">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="4e3f1-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)
* [<span data-ttu-id="4e3f1-140">Aplicativos de exemplo que usam Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="4e3f1-140">Sample applications that use Event Hubs</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

