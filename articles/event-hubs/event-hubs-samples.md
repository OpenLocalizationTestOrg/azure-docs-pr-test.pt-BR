---
title: Exemplos de Hubs de Eventos do Azure | Microsoft Docs
description: Exemplos de Hubs de Eventos do Azure
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: ae9fbd97a1747d8f14c561f247a0973bb11fd039
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-samples"></a><span data-ttu-id="93c9b-103">Exemplos de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="93c9b-103">Event Hubs samples</span></span> 

<span data-ttu-id="93c9b-104">O conjunto de exemplos de Hubs de Eventos do Azure demonstra os principais recursos nos [Hubs de Eventos do Azure](/azure/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="93c9b-104">The set of Azure Event Hubs samples demonstrates key features in [Azure Event Hubs](/azure/event-hubs/).</span></span> <span data-ttu-id="93c9b-105">Este tópico categoriza e descreve os exemplos disponíveis, com links para cada um.</span><span class="sxs-lookup"><span data-stu-id="93c9b-105">This article categorizes and describes the samples available, with links to each.</span></span>

<span data-ttu-id="93c9b-106">No momento da redação deste artigo, exemplos de Hubs de Eventos estão localizados em vários lugares diferentes:</span><span class="sxs-lookup"><span data-stu-id="93c9b-106">At the time of this writing, Event Hubs samples are located in several different places:</span></span>

- [<span data-ttu-id="93c9b-107">Exemplos de código do desenvolvedor do MSDN</span><span class="sxs-lookup"><span data-stu-id="93c9b-107">MSDN developer code samples</span></span>](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [<span data-ttu-id="93c9b-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="93c9b-108">GitHub</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="93c9b-109">Para saber mais sobre as diferentes versões do .NET Framework, veja [estruturas e destinos](/dotnet/articles/standard/frameworks).</span><span class="sxs-lookup"><span data-stu-id="93c9b-109">For more information about different versions of the .NET Framework, see [Frameworks and Targets](/dotnet/articles/standard/frameworks).</span></span>

<span data-ttu-id="93c9b-110">Mais exemplos será adicionado ao longo do tempo, então verifique novamente com frequência para atualizações.</span><span class="sxs-lookup"><span data-stu-id="93c9b-110">More samples will be added over time, so check back here frequently for updates.</span></span>

## <a name="net-standard"></a><span data-ttu-id="93c9b-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="93c9b-111">.NET Standard</span></span>

<span data-ttu-id="93c9b-112">Os exemplos a seguir demonstram como enviar e receber eventos usando o [cliente dos Hubs de Eventos](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) para a [biblioteca do .NET Standard](/dotnet/articles/standard/library).</span><span class="sxs-lookup"><span data-stu-id="93c9b-112">The following samples demonstrate how to send and receive events using the [Event Hubs client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) for the [.NET Standard library](/dotnet/articles/standard/library).</span></span>

### <a name="send-events"></a><span data-ttu-id="93c9b-113">Enviar eventos</span><span class="sxs-lookup"><span data-stu-id="93c9b-113">Send events</span></span> 

<span data-ttu-id="93c9b-114">O exemplo de [Introdução ao envio](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) mostra como escrever um aplicativo de console do .NET Core que envia eventos para um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="93c9b-114">The [Get started sending](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) sample shows how to write a .NET Core console application that sends events to an event hub.</span></span>

### <a name="receive-events"></a><span data-ttu-id="93c9b-115">Receber eventos</span><span class="sxs-lookup"><span data-stu-id="93c9b-115">Receive events</span></span> 

<span data-ttu-id="93c9b-116">O exemplo [Introdução ao recebimento com o Host do Processador de Eventos](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) é um aplicativo de console .NET Core que recebe mensagens de um hub de eventos usando o Host do Processador de Eventos.</span><span class="sxs-lookup"><span data-stu-id="93c9b-116">The [Get started receiving with the Event Processor Host](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) sample is a .NET Core console application that receives messages from an event hub using the Event Processor Host.</span></span>

## <a name="net-framework"></a><span data-ttu-id="93c9b-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="93c9b-117">.NET Framework</span></span>   

<span data-ttu-id="93c9b-118">Estes exemplos demonstram vários outros recursos dos Hubs de Eventos do Azure, direcionados para a [biblioteca do .NET Framework](/dotnet/framework/index).</span><span class="sxs-lookup"><span data-stu-id="93c9b-118">These samples demonstrate various other features of Azure Event Hubs, targeting the [.NET Framework library](/dotnet/framework/index).</span></span>
 
### <a name="notify-users-of-events-received"></a><span data-ttu-id="93c9b-119">Notificar os usuários de eventos recebidos</span><span class="sxs-lookup"><span data-stu-id="93c9b-119">Notify users of events received</span></span>

<span data-ttu-id="93c9b-120">O [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) exemplo notifica os usuários de dados recebidos de sensores ou outros sistemas.</span><span class="sxs-lookup"><span data-stu-id="93c9b-120">The [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) sample notifies users of data received from sensors or other systems.</span></span>

### <a name="get-started-with-event-hubs"></a><span data-ttu-id="93c9b-121">Introdução aos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="93c9b-121">Get started with Event Hubs</span></span> 

<span data-ttu-id="93c9b-122">O exemplo de [Introdução aos Hubs de Eventos](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) demonstra os recursos básicos de Hubs de Eventos, por exemplo, como criar um hub de eventos, enviar eventos a um hub de eventos e consumir eventos usando o [Host do Processador de Eventos](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="93c9b-122">The [Event Hubs Getting Started](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) sample demonstrates the basic capabilities of Event Hubs, such as how to create an event hub, send events to an event hub, and consume events using the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>

### <a name="scale-out-event-processing"></a><span data-ttu-id="93c9b-123">Processamento de eventos de escala horizontal</span><span class="sxs-lookup"><span data-stu-id="93c9b-123">Scale out event processing</span></span> 

<span data-ttu-id="93c9b-124">O exemplo de [Expandir o processamento de eventos](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) demonstra como usar o [Host do Processador de Eventos](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) para distribuir a carga de trabalho de consumo de fluxo de Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="93c9b-124">The [Scale out event processing](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) sample demonstrates how to use the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) to distribute the workload of Event Hubs stream consumption.</span></span> <span data-ttu-id="93c9b-125">Ele mostra como implementar a **EventProcessor** e **EventProcessorFactory** objetos para gerenciar o fluxo de eventos.</span><span class="sxs-lookup"><span data-stu-id="93c9b-125">It shows how to implement the **EventProcessor** and **EventProcessorFactory** objects to manage the event stream.</span></span> 

###  <a name="pull-data-from-sql-into-an-event-hub"></a><span data-ttu-id="93c9b-126">Efetuar pull de dados do SQL para um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="93c9b-126">Pull data from SQL into an event hub</span></span>

<span data-ttu-id="93c9b-127">O exemplo de [Efetuar pull de dados do SQL](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) mostra como efetuar pull de dados de uma tabela SQL e enviá-los por push a um hub de eventos para serem usado como uma entrada em aplicativos analíticos de downstream.</span><span class="sxs-lookup"><span data-stu-id="93c9b-127">The [Pulling SQL data](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) sample shows how to pull data from a SQL table and push it to an event hub, to use as an input in downstream analytical applications.</span></span>

### <a name="pull-web-data-into-an-event-hub"></a><span data-ttu-id="93c9b-128">Efetuar pull de dados da Web para um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="93c9b-128">Pull web data into an event hub</span></span> 

<span data-ttu-id="93c9b-129">O exemplo de [Importar dados da Web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) mostra como efetuar pull de dados de feeds públicos (como o feed de informações de tráfego do Departamento de Transportes) e enviá-los por push para um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="93c9b-129">The [Import data from the web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) sample shows how to pull data from public feeds (such as the Department of Transportation's traffic information feed) and push it to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93c9b-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="93c9b-130">Next steps</span></span>

<span data-ttu-id="93c9b-131">Saiba mais sobre as versões do .NET Framework visitando os links a seguir:</span><span class="sxs-lookup"><span data-stu-id="93c9b-131">Learn more about .NET Framework versions by visiting the following links:</span></span>

- [<span data-ttu-id="93c9b-132">Estruturas e destinos</span><span class="sxs-lookup"><span data-stu-id="93c9b-132">Frameworks and targets</span></span>](/dotnet/articles/standard/frameworks)
- [<span data-ttu-id="93c9b-133">.NET Framework 4.6 e 4.5</span><span class="sxs-lookup"><span data-stu-id="93c9b-133">.NET Framework 4.6 and 4.5</span></span>](/dotnet/framework/index)

<span data-ttu-id="93c9b-134">Você pode saber mais sobre os Hubs de Eventos nestes artigos:</span><span class="sxs-lookup"><span data-stu-id="93c9b-134">You can learn more about Event Hubs in the following articles:</span></span>

- [<span data-ttu-id="93c9b-135">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="93c9b-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="93c9b-136">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="93c9b-136">Create an event hub</span></span>](event-hubs-create.md)
- [<span data-ttu-id="93c9b-137">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="93c9b-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)