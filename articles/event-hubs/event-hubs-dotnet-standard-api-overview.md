---
title: "aaaOverview de saudação APIs padrão do .NET do Azure evento Hubs | Microsoft Docs"
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
ms.openlocfilehash: c97acecb35b69039e06ded7203c75fca41ce98f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-net-standard-api-overview"></a><span data-ttu-id="ed723-103">Visão geral de API do .NET Standard de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="ed723-103">Event Hubs .NET Standard API overview</span></span>
<span data-ttu-id="ed723-104">Este artigo resume algumas das APIs de cliente .NET Standard dos Hubs de eventos de chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed723-104">This article summarizes some of hello key Event Hubs .NET Standard client APIs.</span></span> <span data-ttu-id="ed723-105">Atualmente, há duas bibliotecas de cliente do .NET Standard:</span><span class="sxs-lookup"><span data-stu-id="ed723-105">There are currently two .NET Standard client libraries:</span></span>
* [<span data-ttu-id="ed723-106">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="ed723-106">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
  *  <span data-ttu-id="ed723-107">Esta biblioteca fornece todas as operações básicas de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="ed723-107">This library provides all basic runtime operations.</span></span>
* [<span data-ttu-id="ed723-108">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="ed723-108">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)
  * <span data-ttu-id="ed723-109">Esta biblioteca adiciona funcionalidade adicional que permite manter o controle de eventos processados e é Olá tooread de maneira mais fácil de um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="ed723-109">This library adds additional functionality that allows for keeping track of processed events, and is hello easiest way tooread from an event hub.</span></span>

## <a name="event-hubs-client"></a><span data-ttu-id="ed723-110">Cliente dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="ed723-110">Event Hubs client</span></span>
<span data-ttu-id="ed723-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) é hello objeto primário que você usar eventos toosend, criar receptores e tooget informações de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="ed723-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) is hello primary object you use toosend events, create receivers, and tooget run-time information.</span></span> <span data-ttu-id="ed723-112">Esse cliente é vinculado tooa hub de evento específico e cria um ponto de extremidade de Hubs de eventos de toohello conexão nova.</span><span class="sxs-lookup"><span data-stu-id="ed723-112">This client is linked tooa particular event hub, and creates a new connection toohello Event Hubs endpoint.</span></span>

### <a name="create-an-event-hubs-client"></a><span data-ttu-id="ed723-113">Criar um cliente de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="ed723-113">Create an Event Hubs client</span></span>
<span data-ttu-id="ed723-114">Um objeto [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) é criado de uma cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="ed723-114">An [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) object is created from a connection string.</span></span> <span data-ttu-id="ed723-115">tooinstantiate de maneira mais simples de saudação um novo cliente é mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="ed723-115">hello simplest way tooinstantiate a new client is shown in hello following example:</span></span>

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

<span data-ttu-id="ed723-116">tooprogrammatically Editar cadeia de caracteres de conexão hello, você pode usar o hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) classe e passar a cadeia de caracteres de conexão hello como um parâmetro muito[EventHubClient.CreateFromConnectionString ](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span><span class="sxs-lookup"><span data-stu-id="ed723-116">tooprogrammatically edit hello connection string, you can use hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) class, and pass hello connection string as a parameter too[EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span></span>

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a><span data-ttu-id="ed723-117">Enviar eventos</span><span class="sxs-lookup"><span data-stu-id="ed723-117">Send events</span></span>
<span data-ttu-id="ed723-118">hub de eventos do toosend eventos tooan, use Olá [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) classe.</span><span class="sxs-lookup"><span data-stu-id="ed723-118">toosend events tooan event hub, use hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) class.</span></span> <span data-ttu-id="ed723-119">Olá corpo deve ser um `byte` matriz, ou um `byte` segmento da matriz.</span><span class="sxs-lookup"><span data-stu-id="ed723-119">hello body must be a `byte` array, or a `byte` array segment.</span></span>

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a><span data-ttu-id="ed723-120">Receber eventos</span><span class="sxs-lookup"><span data-stu-id="ed723-120">Receive events</span></span>
<span data-ttu-id="ed723-121">Olá recomendado eventos de tooreceive de maneira dos Hubs de eventos está usando Olá [Host de processador de evento](#event-processor-host-apis), que fornece funcionalidade tooautomatically manter o controle de deslocamento e informações de partição.</span><span class="sxs-lookup"><span data-stu-id="ed723-121">hello recommended way tooreceive events from Event Hubs is using hello [Event Processor Host](#event-processor-host-apis), which provides functionality tooautomatically keep track of offset, and partition information.</span></span> <span data-ttu-id="ed723-122">No entanto, há certas situações em que pode ser toouse flexibilidade de saudação de eventos de tooreceive de biblioteca do hello core Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="ed723-122">However, there are certain situations in which you may want toouse hello flexibility of hello core Event Hubs library tooreceive events.</span></span>

#### <a name="create-a-receiver"></a><span data-ttu-id="ed723-123">Criar um receptor</span><span class="sxs-lookup"><span data-stu-id="ed723-123">Create a receiver</span></span>
<span data-ttu-id="ed723-124">Receptores são toospecific empatados partições, portanto em ordem tooreceive todos os eventos em um hub de eventos, você precisará toocreate várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="ed723-124">Receivers are tied toospecific partitions, so in order tooreceive all events in an event hub, you will need toocreate multiple instances.</span></span> <span data-ttu-id="ed723-125">Em geral, é uma informações de partição boa prática tooget Olá programaticamente, em vez de embutir em código ids de partição de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed723-125">Generally speaking, it is a good practice tooget hello partition information programatically, rather than hard-coding hello partition ids.</span></span> <span data-ttu-id="ed723-126">Em ordem toodo, portanto, você pode usar o hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) método.</span><span class="sxs-lookup"><span data-stu-id="ed723-126">In order toodo so, you can use hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) method.</span></span>

```csharp
// Create a list tookeep track of hello receivers
var receivers = new List<PartitionReceiver>();
// Use hello eventHubClient created above tooget hello runtime information
var runTimeInformation = await eventHubClient.GetRuntimeInformationAsync();
// Loop over hello resulting partition ids
foreach (var partitionId in runTimeInformation.PartitionIds)
{
    // Create hello receiver
    var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);
    // Add hello receiver toohello list
    receivers.Add(receiver);
}
```

<span data-ttu-id="ed723-127">Como os eventos nunca são removidos de um hub de eventos (e apenas expirarem), é necessário ponto de partida correta toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="ed723-127">Since events are never removed from an event hub (and only expire), you need toospecify hello proper starting point.</span></span> <span data-ttu-id="ed723-128">Olá, exemplo a seguir mostra as combinações possíveis.</span><span class="sxs-lookup"><span data-stu-id="ed723-128">hello following example shows possible combinations.</span></span>

```csharp
// partitionId is assumed toocome from GetRuntimeInformationAsync()

// Using hello constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a><span data-ttu-id="ed723-129">Consumir um evento</span><span class="sxs-lookup"><span data-stu-id="ed723-129">Consume an event</span></span>
```csharp
// Receive a maximum of 100 messages in this call tooReceiveAsync
var ehEvents = await receiver.ReceiveAsync(100);
// ReceiveAsync can return null if there are no messages
if (ehEvents != null)
{
    // Since ReceiveAsync can return more than a single event you will need a loop tooprocess
    foreach (var ehEvent in ehEvents)
    {
        // Decode hello byte array segment
        var message = UnicodeEncoding.UTF8.GetString(ehEvent.Body.Array);
        // Load hello custom property that we set in hello send example
        var customType = ehEvent.Properties["Type"];
        // Implement processing logic here
    }
}       
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="ed723-130">APIs de host do processador de eventos</span><span class="sxs-lookup"><span data-stu-id="ed723-130">Event Processor Host APIs</span></span>
<span data-ttu-id="ed723-131">Essas APIs fornecem processos tooworker de resiliência que podem se tornar indisponíveis, distribuindo partições entre os trabalhadores disponíveis.</span><span class="sxs-lookup"><span data-stu-id="ed723-131">These APIs provide resiliency tooworker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within hello SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.

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

// Disposes of hello Event Processor Host
await eventProcessorHost.UnregisterEventProcessorAsync();
```

<span data-ttu-id="ed723-132">Olá, a seguir é um exemplo da implementação de saudação [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span><span class="sxs-lookup"><span data-stu-id="ed723-132">hello following is a sample implementation of hello [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ed723-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ed723-133">Next steps</span></span>
<span data-ttu-id="ed723-134">toolearn mais informações sobre cenários de Hubs de eventos, consulte estes links:</span><span class="sxs-lookup"><span data-stu-id="ed723-134">toolearn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="ed723-135">O que é Hub de Eventos do Azure?</span><span class="sxs-lookup"><span data-stu-id="ed723-135">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="ed723-136">Apis de Hubs de Eventos disponíveis</span><span class="sxs-lookup"><span data-stu-id="ed723-136">Available Event Hubs apis</span></span>](event-hubs-api-overview.md)

<span data-ttu-id="ed723-137">referências de API .NET Olá são aqui:</span><span class="sxs-lookup"><span data-stu-id="ed723-137">hello .NET API references are here:</span></span>

* [<span data-ttu-id="ed723-138">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="ed723-138">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
* [<span data-ttu-id="ed723-139">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="ed723-139">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)