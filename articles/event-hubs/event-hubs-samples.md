---
title: exemplos de Hubs de eventos aaaAzure | Microsoft Docs
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
ms.openlocfilehash: f01f52e6c13f9e885999a6726143440bbc70446d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-samples"></a><span data-ttu-id="550be-103">Exemplos de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="550be-103">Event Hubs samples</span></span> 

<span data-ttu-id="550be-104">conjunto de amostras de Hubs de eventos do Azure Hello demonstra os principais recursos [Hubs de eventos do Azure](/azure/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="550be-104">hello set of Azure Event Hubs samples demonstrates key features in [Azure Event Hubs](/azure/event-hubs/).</span></span> <span data-ttu-id="550be-105">Este artigo categoriza e descreve Olá exemplos disponíveis, com links tooeach.</span><span class="sxs-lookup"><span data-stu-id="550be-105">This article categorizes and describes hello samples available, with links tooeach.</span></span>

<span data-ttu-id="550be-106">Em tempo de saudação da redação deste artigo, exemplos de Hubs de eventos estão localizados em vários lugares diferentes:</span><span class="sxs-lookup"><span data-stu-id="550be-106">At hello time of this writing, Event Hubs samples are located in several different places:</span></span>

- [<span data-ttu-id="550be-107">Exemplos de código do desenvolvedor do MSDN</span><span class="sxs-lookup"><span data-stu-id="550be-107">MSDN developer code samples</span></span>](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [<span data-ttu-id="550be-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="550be-108">GitHub</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="550be-109">Para obter mais informações sobre as diferentes versões de saudação do .NET Framework, consulte [estruturas e destinos](/dotnet/articles/standard/frameworks).</span><span class="sxs-lookup"><span data-stu-id="550be-109">For more information about different versions of hello .NET Framework, see [Frameworks and Targets](/dotnet/articles/standard/frameworks).</span></span>

<span data-ttu-id="550be-110">Mais exemplos será adicionado ao longo do tempo, então verifique novamente com frequência para atualizações.</span><span class="sxs-lookup"><span data-stu-id="550be-110">More samples will be added over time, so check back here frequently for updates.</span></span>

## <a name="net-standard"></a><span data-ttu-id="550be-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="550be-111">.NET Standard</span></span>

<span data-ttu-id="550be-112">Olá exemplos a seguir demonstram como toosend e receber eventos usando Olá [cliente Hubs de eventos](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) para Olá [biblioteca .NET padrão](/dotnet/articles/standard/library).</span><span class="sxs-lookup"><span data-stu-id="550be-112">hello following samples demonstrate how toosend and receive events using hello [Event Hubs client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) for hello [.NET Standard library](/dotnet/articles/standard/library).</span></span>

### <a name="send-events"></a><span data-ttu-id="550be-113">Enviar eventos</span><span class="sxs-lookup"><span data-stu-id="550be-113">Send events</span></span> 

<span data-ttu-id="550be-114">Olá [começar a enviar](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) exemplo mostra como o aplicativo que envia o hub de eventos de tooan eventos de console toowrite um núcleo do .NET.</span><span class="sxs-lookup"><span data-stu-id="550be-114">hello [Get started sending](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) sample shows how toowrite a .NET Core console application that sends events tooan event hub.</span></span>

### <a name="receive-events"></a><span data-ttu-id="550be-115">Receber eventos</span><span class="sxs-lookup"><span data-stu-id="550be-115">Receive events</span></span> 

<span data-ttu-id="550be-116">Olá [começar a receber com hello Host de processador de evento](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) exemplo é um aplicativo de console .NET Core que recebe mensagens de um hub de eventos usando Olá Host de processador de evento.</span><span class="sxs-lookup"><span data-stu-id="550be-116">hello [Get started receiving with hello Event Processor Host](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) sample is a .NET Core console application that receives messages from an event hub using hello Event Processor Host.</span></span>

## <a name="net-framework"></a><span data-ttu-id="550be-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="550be-117">.NET Framework</span></span>   

<span data-ttu-id="550be-118">Esses exemplos demonstram vários outros recursos de Hubs de eventos do Azure, direcionando Olá [biblioteca do .NET Framework](/dotnet/framework/index).</span><span class="sxs-lookup"><span data-stu-id="550be-118">These samples demonstrate various other features of Azure Event Hubs, targeting hello [.NET Framework library](/dotnet/framework/index).</span></span>
 
### <a name="notify-users-of-events-received"></a><span data-ttu-id="550be-119">Notificar os usuários de eventos recebidos</span><span class="sxs-lookup"><span data-stu-id="550be-119">Notify users of events received</span></span>

<span data-ttu-id="550be-120">Olá [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) exemplo notifica os usuários dos dados recebidos de sensores ou outros sistemas.</span><span class="sxs-lookup"><span data-stu-id="550be-120">hello [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) sample notifies users of data received from sensors or other systems.</span></span>

### <a name="get-started-with-event-hubs"></a><span data-ttu-id="550be-121">Introdução aos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="550be-121">Get started with Event Hubs</span></span> 

<span data-ttu-id="550be-122">Olá [guia de Introdução do evento Hubs](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) demonstra os recursos básicos de saudação de Hubs de eventos, como toocreate um hub de eventos, enviar o hub de eventos de tooan de eventos e consumir eventos usando Olá [Host de processador de evento](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="550be-122">hello [Event Hubs Getting Started](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) sample demonstrates hello basic capabilities of Event Hubs, such as how toocreate an event hub, send events tooan event hub, and consume events using hello [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>

### <a name="scale-out-event-processing"></a><span data-ttu-id="550be-123">Processamento de eventos de escala horizontal</span><span class="sxs-lookup"><span data-stu-id="550be-123">Scale out event processing</span></span> 

<span data-ttu-id="550be-124">Olá [expansão de processamento de eventos](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) demonstra como Olá toouse [Host de processador de evento](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) toodistribute carga de trabalho de saudação do consumo de fluxo de Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="550be-124">hello [Scale out event processing](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) sample demonstrates how toouse hello [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) toodistribute hello workload of Event Hubs stream consumption.</span></span> <span data-ttu-id="550be-125">Ele mostra como Olá tooimplement **EventProcessor** e **EventProcessorFactory** fluxo de eventos objetos toomanage hello.</span><span class="sxs-lookup"><span data-stu-id="550be-125">It shows how tooimplement hello **EventProcessor** and **EventProcessorFactory** objects toomanage hello event stream.</span></span> 

###  <a name="pull-data-from-sql-into-an-event-hub"></a><span data-ttu-id="550be-126">Efetuar pull de dados do SQL para um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="550be-126">Pull data from SQL into an event hub</span></span>

<span data-ttu-id="550be-127">Olá [de dados do SQL puxando](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) exemplo mostra como toopull dados de um SQL de tabela e por push tooan hub de eventos, toouse como uma entrada em aplicativos analíticos downstream.</span><span class="sxs-lookup"><span data-stu-id="550be-127">hello [Pulling SQL data](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) sample shows how toopull data from a SQL table and push it tooan event hub, toouse as an input in downstream analytical applications.</span></span>

### <a name="pull-web-data-into-an-event-hub"></a><span data-ttu-id="550be-128">Efetuar pull de dados da Web para um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="550be-128">Pull web data into an event hub</span></span> 

<span data-ttu-id="550be-129">Olá [importar dados de Olá web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) exemplo mostra como os dados toopull do público feeds (como Olá feed de informações de tráfego do departamento de transporte) e por push tooan hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="550be-129">hello [Import data from hello web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) sample shows how toopull data from public feeds (such as hello Department of Transportation's traffic information feed) and push it tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="550be-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="550be-130">Next steps</span></span>

<span data-ttu-id="550be-131">Saiba mais sobre as versões do .NET Framework visitando Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="550be-131">Learn more about .NET Framework versions by visiting hello following links:</span></span>

- [<span data-ttu-id="550be-132">Estruturas e destinos</span><span class="sxs-lookup"><span data-stu-id="550be-132">Frameworks and targets</span></span>](/dotnet/articles/standard/frameworks)
- [<span data-ttu-id="550be-133">.NET Framework 4.6 e 4.5</span><span class="sxs-lookup"><span data-stu-id="550be-133">.NET Framework 4.6 and 4.5</span></span>](/dotnet/framework/index)

<span data-ttu-id="550be-134">Você pode aprender mais sobre os Hubs de eventos Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="550be-134">You can learn more about Event Hubs in hello following articles:</span></span>

- [<span data-ttu-id="550be-135">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="550be-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="550be-136">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="550be-136">Create an event hub</span></span>](event-hubs-create.md)
- [<span data-ttu-id="550be-137">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="550be-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)