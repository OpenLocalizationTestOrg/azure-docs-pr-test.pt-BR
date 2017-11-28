---
title: "aaaWhat Hubs de eventos do Azure e usá-lo por | Microsoft Docs"
description: "Visão geral e introdução tooAzure Hubs de eventos - inclusão de telemetria de escala de nuvem de sites, aplicativos e dispositivos"
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
ms.openlocfilehash: f6199a2e5bee8506f529b6f561234d79f9c8d465
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-event-hubs"></a><span data-ttu-id="ebe5e-103">O que são Hubs de Eventos?</span><span class="sxs-lookup"><span data-stu-id="ebe5e-103">What is Event Hubs?</span></span>

<span data-ttu-id="ebe5e-104">Os Hubs de Evento do Azure são um plataforma de transmissão de dados altamente dimensionável e um serviço de ingestão de dados capaz de receber e processar milhões de eventos por segundo.</span><span class="sxs-lookup"><span data-stu-id="ebe5e-104">Azure Event Hubs is a highly scalable data streaming platform and event ingestion service capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="ebe5e-105">Os Hubs de Eventos podem processar e armazenar eventos, dados ou telemetria produzidos pelos dispositivos e software distribuídos.</span><span class="sxs-lookup"><span data-stu-id="ebe5e-105">Event Hubs can process and store events, data, or telemetry produced by distributed software and devices.</span></span> <span data-ttu-id="ebe5e-106">Os dados enviados tooan hub de eventos pode ser transformado e armazenados usando qualquer provedor de análise em tempo real ou adaptadores de envio em lote/armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ebe5e-106">Data sent tooan event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="ebe5e-107">Com hello capacidade tooprovide [recursos de publicação / assinatura](https://msdn.microsoft.com/library/aa560414.aspx) com baixa latência e em grande escala, Hubs de eventos serve como Olá "no painel" para dados grandes.</span><span class="sxs-lookup"><span data-stu-id="ebe5e-107">With hello ability tooprovide [publish-subscribe capabilities](https://msdn.microsoft.com/library/aa560414.aspx) with low latency and at massive scale, Event Hubs serves as hello "on ramp" for Big Data.</span></span>

## <a name="why-use-event-hubs"></a><span data-ttu-id="ebe5e-108">Por que usar Hubs de Eventos?</span><span class="sxs-lookup"><span data-stu-id="ebe5e-108">Why use Event Hubs?</span></span>

<span data-ttu-id="ebe5e-109">Os eventos de Hubs de Eventos e os recursos de manipulação de telemetria o tornam especialmente útil para:</span><span class="sxs-lookup"><span data-stu-id="ebe5e-109">Event Hubs event and telemetry handling capabilities make it especially useful for:</span></span>

* <span data-ttu-id="ebe5e-110">Instrumentação de aplicativos</span><span class="sxs-lookup"><span data-stu-id="ebe5e-110">Application instrumentation</span></span>
* <span data-ttu-id="ebe5e-111">Experiência do usuário ou o processamento de fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="ebe5e-111">User experience or workflow processing</span></span>
* <span data-ttu-id="ebe5e-112">Cenários de IoT (Internet das coisas)</span><span class="sxs-lookup"><span data-stu-id="ebe5e-112">Internet of Things (IoT) scenarios</span></span>

<span data-ttu-id="ebe5e-113">Por exemplo, os Hubs de Eventos habilitam o rastreamento de comportamentos em aplicativos móveis, informações do tráfego de web farms, captura de eventos de jogos em jogos de console ou telemetria coletada de máquinas industriais, veículos conectados ou outros dispositivos.</span><span class="sxs-lookup"><span data-stu-id="ebe5e-113">For example, Event Hubs enables behavior tracking in mobile apps, traffic information from web farms, in-game event capture in console games, or telemetry collected from industrial machines, connected vehicles, or other devices.</span></span>

## <a name="azure-event-hubs-overview"></a><span data-ttu-id="ebe5e-114">Visão geral dos Hubs de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="ebe5e-114">Azure Event Hubs overview</span></span>

<span data-ttu-id="ebe5e-115">função comum que os Hubs de eventos desempenham em arquiteturas de solução Hello é hello "porta da frente" para um pipeline de eventos, geralmente chamada um *ingestor de eventos*.</span><span class="sxs-lookup"><span data-stu-id="ebe5e-115">hello common role that Event Hubs plays in solution architectures is hello "front door" for an event pipeline, often called an *event ingestor*.</span></span> <span data-ttu-id="ebe5e-116">Um ingestor de eventos é um componente ou serviço que fica entre a produção de hello do evento consumidores toodecouple de um fluxo de eventos do consumo Olá desses eventos e editores de eventos.</span><span class="sxs-lookup"><span data-stu-id="ebe5e-116">An event ingestor is a component or service that sits between event publishers and event consumers toodecouple hello production of an event stream from hello consumption of those events.</span></span> <span data-ttu-id="ebe5e-117">Olá figura a seguir ilustra essa arquitetura:</span><span class="sxs-lookup"><span data-stu-id="ebe5e-117">hello following figure depicts this architecture:</span></span>

![Hubs de Eventos](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

<span data-ttu-id="ebe5e-119">Os Hubs de Eventos fornecem recurso de manipulação de fluxo de mensagens, mas têm características que são diferentes das mensagens corporativas tradicionais.</span><span class="sxs-lookup"><span data-stu-id="ebe5e-119">Event Hubs provides message stream handling capability but has characteristics that are different from traditional enterprise messaging.</span></span> <span data-ttu-id="ebe5e-120">Os recursos de Hubs de Eventos são criados em torno de cenários de alta produtividade e de processamento de eventos.</span><span class="sxs-lookup"><span data-stu-id="ebe5e-120">Event Hubs capabilities are built around high throughput and event processing scenarios.</span></span> <span data-ttu-id="ebe5e-121">Como tal, os Hubs de eventos é diferente do [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) mensagens e não implementa alguns dos recursos de saudação que estão disponíveis para [mensagens do barramento de serviço](/azure/service-bus-messaging/) entidades, como tópicos.</span><span class="sxs-lookup"><span data-stu-id="ebe5e-121">As such, Event Hubs is different from [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) messaging, and does not implement some of hello capabilities that are available for [Service Bus messaging](/azure/service-bus-messaging/) entities, such as topics.</span></span>

## <a name="event-hubs-features"></a><span data-ttu-id="ebe5e-122">Recursos de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="ebe5e-122">Event Hubs features</span></span>

<span data-ttu-id="ebe5e-123">Hubs de eventos contém Olá principais elementos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ebe5e-123">Event Hubs contains hello following key elements:</span></span>

- <span data-ttu-id="ebe5e-124">[**Editores/produtores de eventos**](event-hubs-features.md#event-publishers): uma entidade que envia o hub de eventos de tooan de dados.</span><span class="sxs-lookup"><span data-stu-id="ebe5e-124">[**Event producers/publishers**](event-hubs-features.md#event-publishers): An entity that sends data tooan event hub.</span></span> <span data-ttu-id="ebe5e-125">Um evento é publicado por meio de AMQP 1.0 ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ebe5e-125">An event is published via AMQP 1.0 or HTTPS.</span></span>
- <span data-ttu-id="ebe5e-126">[**Capturar**](event-hubs-features.md#capture): permite que os Hubs de eventos toocapture fluxo de dados e armazená-lo em uma conta de armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="ebe5e-126">[**Capture**](event-hubs-features.md#capture): Enables you toocapture Event Hubs streaming data and store it in an Azure Blob storage account.</span></span>
- <span data-ttu-id="ebe5e-127">[**Partições**](event-hubs-features.md#partitions): permite que cada consumidor tooonly ler um subconjunto específico ou partição, de Olá fluxo de eventos.</span><span class="sxs-lookup"><span data-stu-id="ebe5e-127">[**Partitions**](event-hubs-features.md#partitions): Enables each consumer tooonly read a specific subset, or partition, of hello event stream.</span></span>
- <span data-ttu-id="ebe5e-128">[**Tokens SAS**](event-hubs-features.md#sas-tokens): identifica e autentica o publicador do evento hello.</span><span class="sxs-lookup"><span data-stu-id="ebe5e-128">[**SAS tokens**](event-hubs-features.md#sas-tokens): Identifies and authenticates hello event publisher.</span></span>
- <span data-ttu-id="ebe5e-129">[**Consumidores de evento**](event-hubs-features.md#event-consumers): qualquer entidade que leia dados de evento de um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="ebe5e-129">[**Event consumers**](event-hubs-features.md#event-consumers): An entity that reads event data from an event hub.</span></span> <span data-ttu-id="ebe5e-130">Os consumidores do evento se conectam por meio de AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="ebe5e-130">Event consumers connect via AMQP 1.0.</span></span> 
- <span data-ttu-id="ebe5e-131">[**Grupos de consumidores**](event-hubs-features.md#consumer-groups): fornece cada múltiplo consumindo o aplicativo com uma exibição separada saudação do fluxo de eventos, permitindo que os consumidores tooact independentemente.</span><span class="sxs-lookup"><span data-stu-id="ebe5e-131">[**Consumer groups**](event-hubs-features.md#consumer-groups): Provides each multiple consuming application with a separate view of hello event stream, enabling those consumers tooact independently.</span></span>
- <span data-ttu-id="ebe5e-132">[**Unidades de produtividade**](event-hubs-features.md#capacity): unidades de capacidade pré-adquiridas.</span><span class="sxs-lookup"><span data-stu-id="ebe5e-132">[**Throughput units**](event-hubs-features.md#capacity): Pre-purchased units of capacity.</span></span> <span data-ttu-id="ebe5e-133">Uma única partição tem uma escala máxima de 1 unidade de transferência.</span><span class="sxs-lookup"><span data-stu-id="ebe5e-133">A single partition has a maximum scale of 1 throughput unit.</span></span>

<span data-ttu-id="ebe5e-134">Para obter detalhes técnicos sobre esses e outros recursos de Hubs de eventos, consulte Olá [visão geral dos recursos de Hubs de eventos](event-hubs-features.md).</span><span class="sxs-lookup"><span data-stu-id="ebe5e-134">For technical details about these and other Event Hubs features, see hello [Event Hubs features overview](event-hubs-features.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ebe5e-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ebe5e-135">Next steps</span></span>

<span data-ttu-id="ebe5e-136">Para obter informações sobre preços de Hubs de Evento, consulte [Preços de Hubs de Evento](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="ebe5e-136">For detailed Event Hubs pricing information, see [Event Hubs Pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span>

<span data-ttu-id="ebe5e-137">Para obter mais informações sobre Hubs de eventos, visite Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="ebe5e-137">For more information about Event Hubs, visit hello following links:</span></span>

* <span data-ttu-id="ebe5e-138">Introdução com um [Tutorial de Hubs de Eventos](event-hubs-dotnet-standard-getstarted-send.md)</span><span class="sxs-lookup"><span data-stu-id="ebe5e-138">Get started with an [Event Hubs tutorial](event-hubs-dotnet-standard-getstarted-send.md)</span></span>
* [<span data-ttu-id="ebe5e-139">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="ebe5e-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)
* [<span data-ttu-id="ebe5e-140">Aplicativos de exemplo que usam Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="ebe5e-140">Sample applications that use Event Hubs</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

