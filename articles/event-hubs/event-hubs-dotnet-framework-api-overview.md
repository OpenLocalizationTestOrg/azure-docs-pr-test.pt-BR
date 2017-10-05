---
title: "Visão geral das APIs do .NET Framework dos Hubs de Eventos do Azure | Microsoft Docs"
description: Um resumo de algumas das principais APIs de cliente .NET Framework de Hubs de Eventos.
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7f3b6cc0-9600-417f-9e80-2345411bd036
ms.service: event-hubs
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: bc525e7ca8b21e9e5f1e36b3152d71420b041700
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-net-framework-api-overview"></a><span data-ttu-id="6e714-103">Visão geral da API do .NET Framework de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="6e714-103">Event Hubs .NET Framework API overview</span></span>
<span data-ttu-id="6e714-104">Este artigo resume algumas das principais APIs de cliente .NET Framework de Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="6e714-104">This article summarizes some of the key Event Hubs .NET Framework client APIs.</span></span> <span data-ttu-id="6e714-105">Há duas categorias: APIs de gerenciamento e de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="6e714-105">There are two categories: management and run-time APIs.</span></span> <span data-ttu-id="6e714-106">As APIs de tempo de execução consistem de todas as operações necessárias para enviar e receber uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="6e714-106">Run-time APIs consist of all operations needed to send and receive a message.</span></span> <span data-ttu-id="6e714-107">Operações de gerenciamento permitem gerenciar um estado da entidade Hubs de Eventos, ao criar, atualizar e excluir entidades.</span><span class="sxs-lookup"><span data-stu-id="6e714-107">Management operations enable you to manage an Event Hubs entity state by creating, updating, and deleting entities.</span></span>

<span data-ttu-id="6e714-108">Os cenários de monitoramento abrangem tanto o gerenciamento quanto o tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="6e714-108">Monitoring scenarios span both management and run-time.</span></span> <span data-ttu-id="6e714-109">Para obter a documentação de referência detalhada sobre as APIs .NET, veja as referências [.NET do Barramento de Serviço](/dotnet/api/microsoft.servicebus.messaging) e [API EventProcessorHost](/dotnet/api/microsoft.azure.eventhubs.processor).</span><span class="sxs-lookup"><span data-stu-id="6e714-109">For detailed reference documentation on the .NET APIs, see the [Service Bus .NET](/dotnet/api/microsoft.servicebus.messaging) and [EventProcessorHost API](/dotnet/api/microsoft.azure.eventhubs.processor) references.</span></span>

## <a name="management-apis"></a><span data-ttu-id="6e714-110">APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="6e714-110">Management APIs</span></span>
<span data-ttu-id="6e714-111">Para executar as seguintes operações de gerenciamento, você deve ter permissões para **Gerenciar** no namespace de Hubs de Eventos:</span><span class="sxs-lookup"><span data-stu-id="6e714-111">To perform the following management operations, you must have **Manage** permissions on the Event Hubs namespace:</span></span>

### <a name="create"></a><span data-ttu-id="6e714-112">Criar</span><span class="sxs-lookup"><span data-stu-id="6e714-112">Create</span></span>
```csharp
// Create the event hub
var ehd = new EventHubDescription(eventHubName);
ehd.PartitionCount = SampleManager.numPartitions;
await namespaceManager.CreateEventHubAsync(ehd);
```

### <a name="update"></a><span data-ttu-id="6e714-113">Atualização</span><span class="sxs-lookup"><span data-stu-id="6e714-113">Update</span></span>
```csharp
var ehd = await namespaceManager.GetEventHubAsync(eventHubName);

// Create a customer SAS rule with Manage permissions
ehd.UserMetadata = "Some updated info";
var ruleName = "myeventhubmanagerule";
var ruleKey = SharedAccessAuthorizationRule.GenerateRandomKey();
ehd.Authorization.Add(new SharedAccessAuthorizationRule(ruleName, ruleKey, new AccessRights[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send} )); 
await namespaceManager.UpdateEventHubAsync(ehd);
```

### <a name="delete"></a><span data-ttu-id="6e714-114">Exclusão</span><span class="sxs-lookup"><span data-stu-id="6e714-114">Delete</span></span>
```csharp
await namespaceManager.DeleteEventHubAsync("Event Hub name");
```

## <a name="run-time-apis"></a><span data-ttu-id="6e714-115">APIs de tempo de execução</span><span class="sxs-lookup"><span data-stu-id="6e714-115">Run-time APIs</span></span>
### <a name="create-publisher"></a><span data-ttu-id="6e714-116">Criar publicador</span><span class="sxs-lookup"><span data-stu-id="6e714-116">Create publisher</span></span>
```csharp
// EventHubClient model (uses implicit factory instance, so all links on same connection)
var eventHubClient = EventHubClient.Create("Event Hub name");
```

### <a name="publish-message"></a><span data-ttu-id="6e714-117">Publicar mensagem</span><span class="sxs-lookup"><span data-stu-id="6e714-117">Publish message</span></span>
```csharp
// Create the device/temperature metric
var info = new MetricEvent() { DeviceId = random.Next(SampleManager.NumDevices), Temperature = random.Next(100) };
var data = new EventData(new byte[10]); // Byte array
var data = new EventData(Stream); // Stream 
var data = new EventData(info, serializer) //Object and serializer 
{
    PartitionKey = info.DeviceId.ToString()
};

// Set user properties if needed
data.Properties.Add("Type", "Telemetry_" + DateTime.Now.ToLongTimeString());

// Send single message async
await client.SendAsync(data);
```

### <a name="create-consumer"></a><span data-ttu-id="6e714-118">Criar consumidor</span><span class="sxs-lookup"><span data-stu-id="6e714-118">Create consumer</span></span>
```csharp
// Create the Event Hubs client
var eventHubClient = EventHubClient.Create(EventHubName);

// Get the default consumer group
var defaultConsumerGroup = eventHubClient.GetDefaultConsumerGroup();

// All messages
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index);

// From one day ago
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index, startingDateTimeUtc:DateTime.Now.AddDays(-1));

// From specific offset, -1 means oldest
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index,startingOffset:-1); 
```

### <a name="consume-message"></a><span data-ttu-id="6e714-119">Consumir mensagem</span><span class="sxs-lookup"><span data-stu-id="6e714-119">Consume message</span></span>
```csharp
var message = await consumer.ReceiveAsync();

// Provide a serializer
var info = message.GetBody<Type>(Serializer)

// Get a byte[]
var info = message.GetBytes(); 
msg = UnicodeEncoding.UTF8.GetString(info);
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="6e714-120">APIs de host do processador de eventos</span><span class="sxs-lookup"><span data-stu-id="6e714-120">Event Processor Host APIs</span></span>
<span data-ttu-id="6e714-121">Essas APIs fornecem resiliência aos processos de trabalho que podem se tornar indisponíveis, distribuindo partições entre os trabalhadores disponíveis.</span><span class="sxs-lookup"><span data-stu-id="6e714-121">These APIs provide resiliency to worker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within the SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.
// Use the EventData.Offset value for checkpointing yourself, this value is unique per partition.

var eventHubConnectionString = System.Configuration.ConfigurationManager.AppSettings["Microsoft.ServiceBus.ConnectionString"];
var blobConnectionString = System.Configuration.ConfigurationManager.AppSettings["AzureStorageConnectionString"]; // Required for checkpoint/state

var eventHubDescription = new EventHubDescription(EventHubName);
var host = new EventProcessorHost(WorkerName, EventHubName, defaultConsumerGroup.GroupName, eventHubConnectionString, blobConnectionString);
await host.RegisterEventProcessorAsync<SimpleEventProcessor>();

// To close
await host.UnregisterEventProcessorAsync();
```

<span data-ttu-id="6e714-122">A interface [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) é definida da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6e714-122">The [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) interface is defined as follows:</span></span>

```csharp
public class SimpleEventProcessor : IEventProcessor
{
    IDictionary<string, string> map;
    PartitionContext partitionContext;

    public SimpleEventProcessor()
    {
        this.map = new Dictionary<string, string>();
    }

    public Task OpenAsync(PartitionContext context)
    {
        this.partitionContext = context;

        return Task.FromResult<object>(null);
    }

    public async Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (EventData message in messages)
        {
            // Process messages here
        }

        // Checkpoint when appropriate
        await context.CheckpointAsync();

    }

    public async Task CloseAsync(PartitionContext context, CloseReason reason)
    {
        if (reason == CloseReason.Shutdown)
        {
            await context.CheckpointAsync();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="6e714-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6e714-123">Next steps</span></span>
<span data-ttu-id="6e714-124">Para saber mais sobre os cenários de Hubs de Eventos, consulte estes links:</span><span class="sxs-lookup"><span data-stu-id="6e714-124">To learn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="6e714-125">O que é Hub de Eventos do Azure?</span><span class="sxs-lookup"><span data-stu-id="6e714-125">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="6e714-126">Guia de programação dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="6e714-126">Event Hubs programming guide</span></span>](event-hubs-programming-guide.md)

<span data-ttu-id="6e714-127">As referências de API .NET estão aqui:</span><span class="sxs-lookup"><span data-stu-id="6e714-127">The .NET API references are here:</span></span>

* [<span data-ttu-id="6e714-128">Microsoft.ServiceBus.Messaging</span><span class="sxs-lookup"><span data-stu-id="6e714-128">Microsoft.ServiceBus.Messaging</span></span>](/dotnet/api/microsoft.servicebus.messaging)
* [<span data-ttu-id="6e714-129">Microsoft.Azure.EventHubs.EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="6e714-129">Microsoft.Azure.EventHubs.EventProcessorHost</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor.eventprocessorhost)
