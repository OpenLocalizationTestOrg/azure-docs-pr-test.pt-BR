---
title: "Visão geral das APIs do .NET Standard dos Hubs de Eventos do Azure | Microsoft Docs"
description: "Visão geral da API do .NET Standard"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a173f8e4-556c-42b8-b856-838189f7e636
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: eea682c40cd415b383a8b2f0004a5f3648e2f01f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-net-standard-api-overview"></a><span data-ttu-id="3ae1a-103">Visão geral de API do .NET Standard de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="3ae1a-103">Event Hubs .NET Standard API overview</span></span>
<span data-ttu-id="3ae1a-104">Este artigo resume algumas das principais APIs de cliente .NET Standard de Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="3ae1a-104">This article summarizes some of the key Event Hubs .NET Standard client APIs.</span></span> <span data-ttu-id="3ae1a-105">Atualmente, há duas bibliotecas de cliente do .NET Standard:</span><span class="sxs-lookup"><span data-stu-id="3ae1a-105">There are currently two .NET Standard client libraries:</span></span>
* [<span data-ttu-id="3ae1a-106">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="3ae1a-106">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
  *  <span data-ttu-id="3ae1a-107">Esta biblioteca fornece todas as operações básicas de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="3ae1a-107">This library provides all basic runtime operations.</span></span>
* [<span data-ttu-id="3ae1a-108">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="3ae1a-108">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)
  * <span data-ttu-id="3ae1a-109">Esta biblioteca adiciona outra funcionalidade que permite manter o controle de eventos processados e é a maneira mais fácil de ler em um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="3ae1a-109">This library adds additional functionality that allows for keeping track of processed events, and is the easiest way to read from an event hub.</span></span>

## <a name="event-hubs-client"></a><span data-ttu-id="3ae1a-110">Cliente dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="3ae1a-110">Event Hubs client</span></span>
<span data-ttu-id="3ae1a-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) é o objeto principal que você usa para enviar eventos, criar receptores e obter informações de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="3ae1a-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) is the primary object you use to send events, create receivers, and to get run-time information.</span></span> <span data-ttu-id="3ae1a-112">Esse cliente está vinculado a um hub de eventos específico e cria uma nova conexão para o ponto de extremidade de Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="3ae1a-112">This client is linked to a particular event hub, and creates a new connection to the Event Hubs endpoint.</span></span>

### <a name="create-an-event-hubs-client"></a><span data-ttu-id="3ae1a-113">Criar um cliente de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="3ae1a-113">Create an Event Hubs client</span></span>
<span data-ttu-id="3ae1a-114">Um objeto [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) é criado de uma cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="3ae1a-114">An [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) object is created from a connection string.</span></span> <span data-ttu-id="3ae1a-115">A maneira mais simples para instanciar um novo cliente é mostrada no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ae1a-115">The simplest way to instantiate a new client is shown in the following example:</span></span>

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

<span data-ttu-id="3ae1a-116">Para editar a cadeia de conexão programaticamente, você pode usar a classe [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) e passar a cadeia de conexão como um parâmetro para [EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span><span class="sxs-lookup"><span data-stu-id="3ae1a-116">To programmatically edit the connection string, you can use the [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) class, and pass the connection string as a parameter to [EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span></span>

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a><span data-ttu-id="3ae1a-117">Enviar eventos</span><span class="sxs-lookup"><span data-stu-id="3ae1a-117">Send events</span></span>
<span data-ttu-id="3ae1a-118">Para enviar eventos a um hub de eventos, use a classe [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata).</span><span class="sxs-lookup"><span data-stu-id="3ae1a-118">To send events to an event hub, use the [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) class.</span></span> <span data-ttu-id="3ae1a-119">O corpo deve ser uma matriz `byte` ou um segmento de matriz `byte`.</span><span class="sxs-lookup"><span data-stu-id="3ae1a-119">The body must be a `byte` array, or a `byte` array segment.</span></span>

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a><span data-ttu-id="3ae1a-120">Receber eventos</span><span class="sxs-lookup"><span data-stu-id="3ae1a-120">Receive events</span></span>
<span data-ttu-id="3ae1a-121">A maneira recomendada de receber eventos dos Hubs de Eventos é usar o [Host do Processador de Eventos](#event-processor-host-apis), que fornece funcionalidade para controlar automaticamente o deslocamento e as informações de partição.</span><span class="sxs-lookup"><span data-stu-id="3ae1a-121">The recommended way to receive events from Event Hubs is using the [Event Processor Host](#event-processor-host-apis), which provides functionality to automatically keep track of offset, and partition information.</span></span> <span data-ttu-id="3ae1a-122">No entanto, há algumas situações em que você talvez queira usar a flexibilidade da biblioteca principal do Hubs de Eventos para receber eventos.</span><span class="sxs-lookup"><span data-stu-id="3ae1a-122">However, there are certain situations in which you may want to use the flexibility of the core Event Hubs library to receive events.</span></span>

#### <a name="create-a-receiver"></a><span data-ttu-id="3ae1a-123">Criar um receptor</span><span class="sxs-lookup"><span data-stu-id="3ae1a-123">Create a receiver</span></span>
<span data-ttu-id="3ae1a-124">Os destinatários estão vinculados a partições específicas, então, para receber todos os eventos em um hub de eventos, você precisará criar várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="3ae1a-124">Receivers are tied to specific partitions, so in order to receive all events in an event hub, you will need to create multiple instances.</span></span> <span data-ttu-id="3ae1a-125">Em geral, é uma boa prática para obter as informações de partição de forma programática, em vez de embutir a ID de partição.</span><span class="sxs-lookup"><span data-stu-id="3ae1a-125">Generally speaking, it is a good practice to get the partition information programatically, rather than hard-coding the partition ids.</span></span> <span data-ttu-id="3ae1a-126">Para fazer isso, você pode usar o método [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync).</span><span class="sxs-lookup"><span data-stu-id="3ae1a-126">In order to do so, you can use the [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) method.</span></span>

```csharp
// Create a list to keep track of the receivers
var receivers = new List<PartitionReceiver>();
// Use the eventHubClient created above to get the runtime information
var runTimeInformation = await eventHubClient.GetRuntimeInformationAsync();
// Loop over the resulting partition ids
foreach (var partitionId in runTimeInformation.PartitionIds)
{
    // Create the receiver
    var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);
    // Add the receiver to the list
    receivers.Add(receiver);
}
```

<span data-ttu-id="3ae1a-127">Como os eventos nunca são removidos de um hub de eventos (e apenas expiram), é preciso especificar o ponto de partida adequado.</span><span class="sxs-lookup"><span data-stu-id="3ae1a-127">Since events are never removed from an event hub (and only expire), you need to specify the proper starting point.</span></span> <span data-ttu-id="3ae1a-128">O exemplo a seguir mostra as combinações possíveis.</span><span class="sxs-lookup"><span data-stu-id="3ae1a-128">The following example shows possible combinations.</span></span>

```csharp
// partitionId is assumed to come from GetRuntimeInformationAsync()

// Using the constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a><span data-ttu-id="3ae1a-129">Consumir um evento</span><span class="sxs-lookup"><span data-stu-id="3ae1a-129">Consume an event</span></span>
```csharp
// Receive a maximum of 100 messages in this call to ReceiveAsync
var ehEvents = await receiver.ReceiveAsync(100);
// ReceiveAsync can return null if there are no messages
if (ehEvents != null)
{
    // Since ReceiveAsync can return more than a single event you will need a loop to process
    foreach (var ehEvent in ehEvents)
    {
        // Decode the byte array segment
        var message = UnicodeEncoding.UTF8.GetString(ehEvent.Body.Array);
        // Load the custom property that we set in the send example
        var customType = ehEvent.Properties["Type"];
        // Implement processing logic here
    }
}       
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="3ae1a-130">APIs de host do processador de eventos</span><span class="sxs-lookup"><span data-stu-id="3ae1a-130">Event Processor Host APIs</span></span>
<span data-ttu-id="3ae1a-131">Essas APIs fornecem resiliência aos processos de trabalho que podem se tornar indisponíveis, distribuindo partições entre os trabalhadores disponíveis.</span><span class="sxs-lookup"><span data-stu-id="3ae1a-131">These APIs provide resiliency to worker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within the SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.

// Read these connection strings from a secure location
var ehConnectionString = "{Event Hubs connection string}";
var ehEntityPath = "{event hub path/name}";
var storageConnectionString = "{Storage connection string}";
var storageContainerName = "{Storage account container name}";

var eventProcessorHost = new EventProcessorHost(
    ehEntityPath,
    PartitionReceiver.DefaultConsumerGroupName,
    ehConnectionString,
    storageConnectionString,
    storageContainerName);

// Start/register an EventProcessorHost
await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

// Disposes of the Event Processor Host
await eventProcessorHost.UnregisterEventProcessorAsync();
```

<span data-ttu-id="3ae1a-132">A seguir é uma implementação de exemplo de [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span><span class="sxs-lookup"><span data-stu-id="3ae1a-132">The following is a sample implementation of the [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span></span>

```csharp
public class SimpleEventProcessor : IEventProcessor
{
    public Task CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
        return Task.CompletedTask;
    }

    public Task OpenAsync(PartitionContext context)
    {
        Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
        return Task.CompletedTask;
    }

    public Task ProcessErrorAsync(PartitionContext context, Exception error)
    {
        Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
        return Task.CompletedTask;
    }

    public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (var eventData in messages)
        {
            var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
            Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
        }

        return context.CheckpointAsync();
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="3ae1a-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3ae1a-133">Next steps</span></span>
<span data-ttu-id="3ae1a-134">Para saber mais sobre os cenários de Hubs de Eventos, consulte estes links:</span><span class="sxs-lookup"><span data-stu-id="3ae1a-134">To learn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="3ae1a-135">O que é Hub de Eventos do Azure?</span><span class="sxs-lookup"><span data-stu-id="3ae1a-135">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="3ae1a-136">Apis de Hubs de Eventos disponíveis</span><span class="sxs-lookup"><span data-stu-id="3ae1a-136">Available Event Hubs apis</span></span>](event-hubs-api-overview.md)

<span data-ttu-id="3ae1a-137">As referências de API .NET estão aqui:</span><span class="sxs-lookup"><span data-stu-id="3ae1a-137">The .NET API references are here:</span></span>

* [<span data-ttu-id="3ae1a-138">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="3ae1a-138">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
* [<span data-ttu-id="3ae1a-139">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="3ae1a-139">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)