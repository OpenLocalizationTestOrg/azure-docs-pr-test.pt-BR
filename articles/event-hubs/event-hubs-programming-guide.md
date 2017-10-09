---
title: Guia de aaaProgramming para Hubs de eventos do Azure | Microsoft Docs
description: "Escreva código para Hubs de eventos do Azure usando Olá SDK .NET do Azure."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64cbfd3d-4a0e-4455-a90a-7f3d4f080323
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/17/2017
ms.author: sethm
ms.openlocfilehash: 43bebd126c2311af9e3daeb52324132b66cf0884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-programming-guide"></a>Guia de programação dos Hubs de Eventos

Este artigo aborda alguns cenários comuns de escrever código usando Hubs de eventos do Azure e hello SDK .NET do Azure. Ele supõe uma compreensão preliminar de Hubs de Eventos. Para obter uma visão geral conceitual dos Hubs de eventos, consulte Olá [visão geral de Hubs de evento](event-hubs-what-is-event-hubs.md).

## <a name="event-publishers"></a>Editores de eventos

Enviar o hub de eventos de tooan eventos usando HTTP POST ou via uma conexão AMQP 1.0. Olá escolha de qual toouse e quando depende Olá cenário específico que está sendo resolvido. Conexões do AMQP 1.0 são medidas como conexões negociadas no Barramento de Serviço e são mais apropriadas em cenários com volumes de mensagem frequentemente mais altos e requisitos de latência mais baixos, já que fornecem um canal de mensagens persistente.

Criar e gerenciar os Hubs de eventos usando Olá [NamespaceManager][] classe. Quando usando .NET Olá APIs gerenciadas, Olá primário construções para publicar dados tooEvent Hubs são Olá [EventHubClient](/dotnet/api/microsoft.servicebus.messaging.eventhubclient) e [EventData][] classes. [EventHubClient][] fornece um canal de comunicação AMQP Olá durante o qual os eventos são enviados toohello hub de eventos. Olá [EventData][] classe representa um evento e é usado toopublish hub de eventos de tooan de mensagens. Essa classe inclui Olá corpo, alguns metadados e informações de cabeçalho sobre eventos de saudação. Outras propriedades são adicionadas toohello [EventData][] conforme ele passa por um hub de eventos do objeto.

## <a name="get-started"></a>Introdução

classes do .NET Olá que suportam Hubs de evento são fornecidas nos Olá assembly Microsoft.ServiceBus.dll. Olá mais fácil Olá tooreference de maneira API do barramento de serviço e tooconfigure seu aplicativo com todas as dependências de barramento de serviço Olá é Olá toodownload [pacote NuGet do barramento de serviço](https://www.nuget.org/packages/WindowsAzure.ServiceBus). Como alternativa, você pode usar o hello [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) no Visual Studio. toodo assim, emitir Olá após o comando no hello [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) janela:

```
Install-Package WindowsAzure.ServiceBus
```

## <a name="create-an-event-hub"></a>Criar um Hub de Evento
Você pode usar o hello [NamespaceManager][] toocreate Hubs de eventos de classe. Por exemplo:

```csharp
var manager = new Microsoft.ServiceBus.NamespaceManager("mynamespace.servicebus.windows.net");
var description = manager.CreateEventHub("MyEventHub");
```

Na maioria dos casos, é recomendável que você use Olá [CreateEventHubIfNotExists][] tooavoid métodos gerar exceções se Olá serviço seja reiniciado. Por exemplo:

```csharp
var description = manager.CreateEventHubIfNotExists("MyEventHub");
```

Todas as operações de criação de Hubs de eventos, inclusive [CreateEventHubIfNotExists][], exigem **gerenciar** permissões no namespace de saudação em questão. Se quiser toolimit Olá permissões de seus aplicativos de consumidor ou publicador, você pode evitar isso criar chamadas de operação no código de produção quando você usar credenciais com permissões limitadas.

Olá [EventHubDescription](/dotnet/api/microsoft.servicebus.messaging.eventhubdescription) classe contém detalhes sobre um hub de eventos, incluindo as regras de autorização hello, intervalo de retenção de mensagem de saudação, ID de partição, status e caminho. Você pode usar a classe tooupdate Olá metadados em um hub de eventos.

## <a name="create-an-event-hubs-client"></a>Criar um cliente de Hubs de Eventos
a classe principal Olá para interagir com Hubs de eventos é [Microsoft.ServiceBus.Messaging.EventHubClient][EventHubClient]. Essa classe fornece recursos de remetente e destinatário. Você pode criar uma instância desta classe usando Olá [criar](/dotnet/api/microsoft.servicebus.messaging.eventhubclient.create) método, conforme mostrado no exemplo a seguir de saudação.

```csharp
var client = EventHubClient.Create(description.Path);
```

Esse método usa informações de conexão do barramento do serviço de saudação no arquivo App. config hello, em hello `appSettings` seção. Para obter um exemplo de hello `appSettings` XML usado informações de conexão de barramento do serviço toostore hello, consulte documentação Olá Olá [Microsoft.ServiceBus.Messaging.EventHubClient.Create(System.String)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) método.

Outra opção é toocreate cliente de saudação de uma cadeia de conexão. Essa opção funciona bem quando estiver usando funções de trabalho do Azure, porque você pode armazenar a cadeia de caracteres hello nas propriedades de configuração de saudação do trabalho de saudação. Por exemplo:

```csharp
EventHubClient.CreateFromConnectionString("your_connection_string");
```

cadeia de caracteres de conexão Olá será em Olá mesmo formato, como ele aparece no arquivo App. config de saudação para métodos anteriores de saudação:

```
Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[key]
```

Por fim, também é possível toocreate um [EventHubClient][] de objeto um [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) instância, conforme mostrado no exemplo a seguir de saudação.

```csharp
var factory = MessagingFactory.CreateFromConnectionString("your_connection_string");
var client = factory.CreateEventHubClient("MyEventHub");
```

É importante toonote que outros [EventHubClient][] objetos criados a partir de uma instância da fábrica de mensagens reutilizará Olá mesmo subjacente conexão TCP. Portanto, esses objetos têm um limite, no lado do cliente, na taxa de transferência. Olá [criar](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) método reutiliza uma única fábrica de mensagens. Se você precisa de uma taxa de transferência muito alta de um único remetente, é possível criar diversas fábricas de mensagens e um objeto [EventHubClient][] de cada fábrica de mensagens.

## <a name="send-events-tooan-event-hub"></a>Enviar o hub de eventos de tooan de eventos
Enviar o hub de eventos de tooan de eventos, criando um [EventData][] instância e enviá-los por meio de saudação [enviar](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) método. Esse método usa um único [EventData][] parâmetro da instância e o envia de forma síncrona tooan hub de eventos.

## <a name="event-serialization"></a>Serialização de evento
Olá [EventData][] classe tem [quatro sobrecarregado construtores](/dotnet/api/microsoft.servicebus.messaging.eventdata#constructors_) que executar uma variedade de parâmetros, como um objeto e serializador, uma matriz de bytes ou um fluxo. Também é possível tooinstantiate Olá [EventData][] classe e definir o fluxo do corpo Olá posteriormente. Ao usar o JSON com [EventData][], você pode usar **Encoding.UTF8.GetBytes()** tooretrieve matriz de bytes de saudação para uma cadeia de caracteres codificada em JSON.

## <a name="partition-key"></a>Chave de partição
Olá [EventData][] classe tiver um [PartitionKey][] propriedade que permite que o remetente de saudação toospecify um valor que é transformado em hash tooproduce uma atribuição de partição. Usar uma chave de partição garante que todos os Olá eventos com hello são enviadas a mesma chave toohello mesma partição no hub de eventos de saudação. Chaves de partição comuns incluem IDs de sessão de usuário e IDs de remetente exclusivo. Olá [PartitionKey][] propriedade é opcional e pode ser fornecida ao usar Olá [Microsoft.ServiceBus.Messaging.EventHubClient.Send(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) ou [Microsoft.ServiceBus.Messaging.EventHubClient.SendAsync(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendAsync_Microsoft_ServiceBus_Messaging_EventData_) métodos. Se você não fornecer um valor para [PartitionKey][], enviados eventos são distribuídos toopartitions usando um modelo de rodízio.

### <a name="availability-considerations"></a>Considerações sobre disponibilidade

Usar uma chave de partição é opcional, e você deve considerar cuidadosamente se toouse um. Em muitos casos, usar uma chave de partição é uma boa opção se a ordem dos eventos for importante. Quando você usa uma chave de partição, essas partições exigem disponibilidade em um único nó, e podem ocorrer interrupções ao longo do tempo; por exemplo, durante a reinicialização e aplicação de patches de nós de computação. Dessa forma, se você definir um ID de partição e essa partição fica indisponível por algum motivo, um dados de saudação tooaccess tentativa nessa partição falhará. Se a alta disponibilidade é mais importante, não especifique uma chave de partição; Nesse caso eventos serão enviados toopartitions usando Olá round-robin modelo descrito anteriormente. Nesse cenário, você estiver fazendo uma escolha explícita entre disponibilidade (ID de partição) e a consistência (fixação eventos tooa ID da partição).

Outra consideração é o tratamento de atrasos no processamento de eventos. Em alguns casos, ele pode ser toodrop dados e repita que tootry e acompanhar o processamento, o que pode causar atrasos de processamento posterior downstream. Por exemplo, com uma cotação de ações é melhor toowait para dados atualizados completos, mas em um bate-papo ao vivo ou o cenário VOIP que prefere ter dados saudação rapidamente, mesmo se ele não está completo.

Dadas essas considerações de disponibilidade, nestes cenários você pode escolher uma saudação estratégias de tratamento de erros a seguir:

- Parar (para de ler de Hubs de Eventos até que tudo seja corrigido)
- Descartar (as mensagens não são importantes, descarte-as)
- Repetir (Olá repetição mensagens como você pode ver se ajustar)
- [Mensagens mortas](../service-bus-messaging/service-bus-dead-letter-queues.md) (use uma fila ou outro toodead de hub de evento carta somente mensagens de saudação que não pôde processar)

Para obter mais informações e uma discussão sobre Olá prós e contras disponibilidade e a consistência, consulte [disponibilidade e a consistência nos Hubs de eventos](event-hubs-availability-and-consistency.md). 

## <a name="batch-event-send-operations"></a>Operações de envio de eventos em lote
Envio de eventos em lotes pode aumentar significativamente a taxa de transferência. Olá [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__) leva um **IEnumerable** parâmetro do tipo [EventData][] e envia Olá lote inteiro como um hub de eventos de toohello operação atômica.

```csharp
public void SendBatch(IEnumerable<EventData> eventDataList);
```

Observe que um único lote não deve exceder o limite de 256 KB de saudação de um evento. Além disso, cada mensagem em lote Olá usa Olá mesma identidade do publicador. É responsabilidade de saudação do hello remetente tooensure que Olá lote não exceda o tamanho máximo de evento de saudação. Em caso afirmativo, um erro **Enviar** do cliente é gerado.

## <a name="send-asynchronously-and-send-at-scale"></a>Enviar de forma assíncrona e em escala
Você também pode enviar hub de eventos de tooan eventos assincronamente. Envio de forma assíncrona pode aumentar a taxa de saudação em que um cliente é capaz de toosend eventos. Ambos os Olá [enviar](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) e [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__) métodos estão disponíveis nas versões assíncronas que retornam um [tarefa](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) objeto. Embora essa técnica pode aumentar a taxa de transferência, ela também pode causar Olá eventos do cliente toocontinue toosend mesmo enquanto ele estiver sendo acelerado pelo Olá serviço de Hubs de eventos e pode resultar em Olá falhas ou mensagens perdidas se não implementada corretamente. Além disso, você pode usar o hello [RetryPolicy](/dotnet/api/microsoft.servicebus.messaging.cliententity#Microsoft_ServiceBus_Messaging_ClientEntity_RetryPolicy) propriedade nas opções de repetição Olá cliente toocontrol cliente.

## <a name="create-a-partition-sender"></a>Criar um remetente de partição
Embora seja mais comum sem uma chave de partição do hub de eventos dos tooan toosend eventos, em alguns casos, você pode querer toosend eventos diretamente tooa determinada partição. Por exemplo:

```csharp
var partitionedSender = client.CreatePartitionedSender(description.PartitionIds[0]);
```

[CreatePartitionedSender](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_CreatePartitionedSender_System_String_) retorna um [EventHubSender](/dotnet/api/microsoft.servicebus.messaging.eventhubsender) que você pode usar a partição do hub de evento específico do toopublish eventos tooa do objeto.

## <a name="event-consumers"></a>Consumidores de evento
O Hubs de Eventos tem dois modelos principais para consumo de eventos: receptores diretos e abstrações de nível superior, como [EventProcessorHost][]. Receptores diretos são responsáveis por sua própria coordenação de acesso toopartitions dentro de um grupo de consumidores.

### <a name="direct-consumer"></a>Consumidor direto
Olá tooread de maneira mais direta de uma partição em um grupo de consumidores é Olá toouse [EventHubReceiver](/dotnet/apie/microsoft.servicebus.messaging.eventhubreceiver) classe. toocreate uma instância dessa classe, você deve usar uma instância do hello [EventHubConsumerGroup](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup) classe. Em Olá exemplo a seguir, ID de partição Olá deve ser especificado ao criar o receptor Olá para o grupo de consumidores hello.

```csharp
EventHubConsumerGroup group = client.GetDefaultConsumerGroup();
var receiver = group.CreateReceiver(client.GetRuntimeInformation().PartitionIds[0]);
```

Olá [CreateReceiver](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup#methods_summary) método tem várias sobrecargas que facilitam o controle sobre o leitor hello está sendo criado. Esses métodos incluem especificar um deslocamento como uma cadeia de caracteres ou um carimbo de hora e Olá capacidade toospecify se tooinclude esse deslocamento especificado em Olá retornado de fluxo ou iniciar depois dele. Depois de criar o receptor Olá, você pode iniciar o recebimento de eventos no hello objeto retornado. Olá [Receive](/dotnet/api/microsoft.servicebus.messaging.eventhubreceiver#methods_summary) método tem quatro sobrecargas que Olá controle receber parâmetros de operação, como tamanho de lote e tempo de espera. Você pode usar versões assíncronas de saudação de taxa de transferência de saudação de tooincrease esses métodos de um consumidor. Por exemplo:

```csharp
bool receive = true;
string myOffset;
while(receive)
{
    var message = receiver.Receive();
    myOffset = message.Offset;
    string body = Encoding.UTF8.GetString(message.GetBytes());
    Console.WriteLine(String.Format("Received message offset: {0} \nbody: {1}", myOffset, body));
}
```

Com respeito tooa de partição específica, mensagens de saudação são recebidas em ordem de saudação em que foram enviadas toohello hub de eventos. deslocamento de saudação é uma cadeia de caracteres token usado tooidentify uma mensagem em uma partição.

Observe que uma única partição em um grupo de consumidores não pode ter mais de 5 leitores simultâneos conectados em algum momento. Como leitores de conexão ou desconexão, suas sessões podem ficar ativas por vários minutos antes que o serviço de saudação reconhece que foi desconectado. Durante esse tempo, reconectar-se a partição tooa pode falhar. Para obter um exemplo completo de como escrever um receptor direto para Hubs de eventos, consulte Olá [receptores diretos de Hubs de evento](https://code.msdn.microsoft.com/Event-Hub-Direct-Receivers-13fa95c6) exemplo.

### <a name="event-processor-host"></a>Host do processador de eventos
Olá [EventProcessorHost][] classe processa dados de Hubs de eventos. Você deve usar essa implementação ao criar os leitores de evento na plataforma .NET de saudação. [EventProcessorHost][] fornece um ambiente de tempo de execução seguro, thread-safe, de vários processos, para implementações de processador de eventos, que também fornece gerenciamento de concessão de ponto de verificação e partição.

Olá toouse [EventProcessorHost][] classe, você pode implementar [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor). Essa interface contém três métodos:

* [OpenAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_OpenAsync_Microsoft_ServiceBus_Messaging_PartitionContext_)
* [CloseAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_CloseAsync_Microsoft_ServiceBus_Messaging_PartitionContext_Microsoft_ServiceBus_Messaging_CloseReason_)
* [ProcessEventsAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_ProcessEventsAsync_Microsoft_ServiceBus_Messaging_PartitionContext_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__)

toostart processamento de eventos, instanciar [EventProcessorHost][], fornecendo os parâmetros adequados Olá para o hub de eventos. Em seguida, chame [RegisterEventProcessorAsync](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost#Microsoft_ServiceBus_Messaging_EventProcessorHost_RegisterEventProcessorAsync__1) tooregister sua [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) implementação com tempo de execução de saudação. Neste ponto, o host Olá tentará tooacquire uma concessão em todas as partições no hub de eventos hello usando um algoritmo de "greedy". Essas concessões vão durar por determinado período e, em seguida, devem ser renovadas. Como novos nós, instâncias de trabalho nesse caso, ficam online, eles usam reservas de concessão e ao longo do tempo carga Olá alterna entre os nós como cada tentativas tooacquire mais concessões.

![Host do processador de eventos](./media/event-hubs-programming-guide/IC759863.png)

Ao longo do tempo, é estabelecido um equilíbrio. Esse recurso dinâmico permite o dimensionamento automático com base em CPU toobe aplicada tooconsumers para ampliar e reduzir. Como Hubs de eventos não têm um conceito direto de contagens de mensagens, média de utilização da CPU é geralmente Olá melhor mecanismo toomeasure back final ou consumidor escala. Se os publicadores começarem toopublish que podem processar mais eventos que os consumidores, aumento de CPU de Olá consumidores pode ser usado toocause um dimensionamento automático na contagem de instâncias de trabalho.

Olá [EventProcessorHost][] classe também implementa um mecanismo de ponto de verificação com base em armazenamento do Azure. Saudação de repositórios esse mecanismo deslocamento em uma base por partição, para que cada consumidor pode determinar quais Olá último ponto de verificação do consumidor anterior Olá era. Como as partições transitam entre os nós por meio de concessões, esse é o mecanismo de sincronização de saudação que facilita a mudança de carga.

## <a name="publisher-revocation"></a>Revogação do publicador
Além disso, toohello avançados recursos de tempo de execução do [EventProcessorHost][], Hubs de eventos permitem a revogação de publicador em editores específicos do pedido tooblock enviem hub de eventos do evento tooan. Esses recursos são particularmente úteis se um token do publicador foi comprometido ou uma atualização de software está fazendo com que eles toobehave inadequadamente. Nessas situações, identidade do publicador hello, que faz parte de seu token SAS, pode ser impedida de publicar eventos.

Para obter mais informações sobre como toosend tooEvent Hubs como um publicador, consulte e revogação de publicador Olá [evento Hubs de grande escala publicação segura](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab) exemplo.

## <a name="next-steps"></a>Próximas etapas
toolearn mais informações sobre cenários de Hubs de eventos, consulte estes links:

* [Visão geral de API de Hubs de Eventos](event-hubs-api-overview.md)
* [O que são Hubs de Eventos](event-hubs-what-is-event-hubs.md)
* [Disponibilidade e consistência nos Hubs de Eventos](event-hubs-availability-and-consistency.md)
* [Referência de API do host de processador de eventos](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)

[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[EventHubClient]: /dotnet/api/microsoft.servicebus.messaging.eventhubclient
[EventData]: /dotnet/api/microsoft.servicebus.messaging.eventdata
[CreateEventHubIfNotExists]: /dotnet/api/microsoft.servicebus.namespacemanager.createeventhubifnotexists
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.eventdata#Microsoft_ServiceBus_Messaging_EventData_PartitionKey
[EventProcessorHost]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
