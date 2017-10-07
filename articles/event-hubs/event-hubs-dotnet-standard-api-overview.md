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
# <a name="event-hubs-net-standard-api-overview"></a>Visão geral de API do .NET Standard de Hubs de Eventos
Este artigo resume algumas das APIs de cliente .NET Standard dos Hubs de eventos de chave de saudação. Atualmente, há duas bibliotecas de cliente do .NET Standard:
* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs)
  *  Esta biblioteca fornece todas as operações básicas de tempo de execução.
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor)
  * Esta biblioteca adiciona funcionalidade adicional que permite manter o controle de eventos processados e é Olá tooread de maneira mais fácil de um hub de eventos.

## <a name="event-hubs-client"></a>Cliente dos Hubs de Eventos
[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) é hello objeto primário que você usar eventos toosend, criar receptores e tooget informações de tempo de execução. Esse cliente é vinculado tooa hub de evento específico e cria um ponto de extremidade de Hubs de eventos de toohello conexão nova.

### <a name="create-an-event-hubs-client"></a>Criar um cliente de Hubs de Eventos
Um objeto [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) é criado de uma cadeia de conexão. tooinstantiate de maneira mais simples de saudação um novo cliente é mostrado no exemplo a seguir de saudação:

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

tooprogrammatically Editar cadeia de caracteres de conexão hello, você pode usar o hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) classe e passar a cadeia de caracteres de conexão hello como um parâmetro muito[EventHubClient.CreateFromConnectionString ](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a>Enviar eventos
hub de eventos do toosend eventos tooan, use Olá [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) classe. Olá corpo deve ser um `byte` matriz, ou um `byte` segmento da matriz.

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a>Receber eventos
Olá recomendado eventos de tooreceive de maneira dos Hubs de eventos está usando Olá [Host de processador de evento](#event-processor-host-apis), que fornece funcionalidade tooautomatically manter o controle de deslocamento e informações de partição. No entanto, há certas situações em que pode ser toouse flexibilidade de saudação de eventos de tooreceive de biblioteca do hello core Hubs de eventos.

#### <a name="create-a-receiver"></a>Criar um receptor
Receptores são toospecific empatados partições, portanto em ordem tooreceive todos os eventos em um hub de eventos, você precisará toocreate várias instâncias. Em geral, é uma informações de partição boa prática tooget Olá programaticamente, em vez de embutir em código ids de partição de saudação. Em ordem toodo, portanto, você pode usar o hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) método.

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

Como os eventos nunca são removidos de um hub de eventos (e apenas expirarem), é necessário ponto de partida correta toospecify hello. Olá, exemplo a seguir mostra as combinações possíveis.

```csharp
// partitionId is assumed toocome from GetRuntimeInformationAsync()

// Using hello constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a>Consumir um evento
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

## <a name="event-processor-host-apis"></a>APIs de host do processador de eventos
Essas APIs fornecem processos tooworker de resiliência que podem se tornar indisponíveis, distribuindo partições entre os trabalhadores disponíveis.

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

Olá, a seguir é um exemplo da implementação de saudação [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).

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

## <a name="next-steps"></a>Próximas etapas
toolearn mais informações sobre cenários de Hubs de eventos, consulte estes links:

* [O que é Hub de Eventos do Azure?](event-hubs-what-is-event-hubs.md)
* [Apis de Hubs de Eventos disponíveis](event-hubs-api-overview.md)

referências de API .NET Olá são aqui:

* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs)
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor)