---
title: "aaaOverview de mensagens de filas, tópicos e assinaturas do Azure Service Bus | Microsoft Docs"
description: "Visão geral de entidades do sistema de mensagens do Barramento de Serviço."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a306ced4-74e9-47c6-990a-d9c47efa31d5
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 73135d2658e341c14dbb114ab938faed91578ff1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-queues-topics-and-subscriptions"></a>Filas, tópicos e assinaturas do Barramento de Serviço

O Barramento de Serviço do Microsoft Azure oferece suporte a um conjunto de tecnologias middleware orientado a mensagens, baseado em nuvem, incluindo o serviço de enfileiramento de mensagens confiável e o sistema de mensagens de publicação/assinatura durável. Esses recursos de mensagens "orientadas" podem ser considerados separado recursos que suporte publicação / assinatura de mensagens, temporal desacoplamento e cenários de malha mensagens do barramento de serviço de saudação de balanceamento de carga. A comunicação desacoplada tem diversas vantagens; por exemplo, clientes e servidores podem se conectar como necessário e executar as operações deles de forma assíncrona.

entidades de mensagens de saudação que formam o núcleo de saudação de recursos no barramento de serviço de mensagens de saudação são filas, tópicos, assinaturas e regras/ações.

## <a name="queues"></a>Filas

As filas oferecem *primeiro a entrar, primeiro a sair* tooone de entrega de mensagem (PEPS) ou mais consumidores concorrentes. Ou seja, as mensagens são normalmente esperado toobe recebidas e processadas pelos destinatários de saudação na Olá ordem em que eles foram adicionados toohello fila, e cada mensagem é recebida e processada por apenas um cliente de mensagem. Uma importante vantagem de usar filas é tooachieve "desacoplamento temporal" dos componentes do aplicativo. Olá em outras palavras, os produtores (remetentes) e os consumidores (destinatários) não tem toobe enviar e receber mensagens em Olá mesmo tempo porque as mensagens são armazenadas de forma duradoura na fila de saudação. Além disso, produtor Olá não tem toowait por uma resposta do consumidor de saudação em ordem toocontinue tooprocess e enviar mensagens.

Um benefício relacionado é "carga redistribuição," que permite que produtores e consumidores toosend e recebe mensagens em diferentes taxas. Em muitos aplicativos, a carga do sistema Olá varia ao longo do tempo; No entanto, o tempo de processamento de saudação necessário para cada unidade de trabalho é normalmente constante. Intermediação dos produtores e consumidores com uma fila significa que Olá consumindo o aplicativo só tem toobe toobe provisionados toohandle capaz de carga média em vez de picos de carga. profundidade de saudação da fila de saudação aumenta e diminui conforme a carga de entrada hello varia. Isso economiza o dinheiro diretamente com valor de toohello considerar a infraestrutura necessária tooservice Olá de carregamento de aplicativo. Como Olá carga aumenta, mais processos de trabalho podem ser adicionado tooread da fila de saudação. Cada mensagem é processada por apenas um dos processos de trabalho hello. Além disso, esse balanceamento de carga baseado em pull permite o uso otimizado dos computadores de trabalho Olá mesmo que sejam diferentes computadores de trabalho Olá com capacidade de tooprocessing de relação, conforme eles efetuarão pull das mensagens em sua própria velocidade máxima. Esse padrão é geralmente denominado padrão de "consumidor concorrente" hello.

Usar filas toointermediate entre os consumidores e produtores de mensagens fornece um acoplamento flexível entre os componentes de saudação. Como produtores e consumidores não têm conhecimento uns dos outros, um consumidor pode ser atualizado sem causar qualquer impacto produtor hello.

A criação de uma fila é um processo de várias etapas. Executar operações de gerenciamento para entidades (filas e tópicos) por meio de saudação de mensagens do barramento de serviço [Microsoft.ServiceBus.NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) classe, que é construído, fornecendo o endereço de base de saudação do hello barramento de serviço namespace e hello credenciais do usuário. [Gerenciador de namespace](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) fornece métodos toocreate, enumerar e excluir entidades de mensagens. Depois de criar um [Microsoft.ServiceBus.TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) objeto do nome SAS do hello e chave e um gerenciamento de namespace de serviço do objeto, você pode usar o hello [Microsoft.ServiceBus.NamespaceManager.CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) fila de saudação do método toocreate. Por exemplo:

```csharp
// Create management credentials
TokenProvider credentials = TokenProvider.CreateSharedAccessSignatureTokenProvider(sasKeyName,sasKeyValue);
// Create namespace client
NamespaceManager namespaceClient = new NamespaceManager(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials);
```

Em seguida, você pode criar um objeto de fila e uma fábrica de mensagens com hello URI de barramento de serviço como um argumento. Por exemplo:

```csharp
QueueDescription myQueue;
myQueue = namespaceClient.CreateQueue("TestQueue");
MessagingFactory factory = MessagingFactory.Create(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials); 
QueueClient myQueueClient = factory.CreateQueueClient("TestQueue");
```

Em seguida, você pode enviar fila de mensagens de toohello. Por exemplo, se você tiver uma lista de mensagens orientadas chamado `MessageList`, código de saudação é exibido a seguir toohello semelhante:

```csharp
for (int count = 0; count < 6; count++)
{
    var issue = MessageList[count];
    issue.Label = issue.Properties["IssueTitle"].ToString();
    myQueueClient.Send(issue);
}
```

Você então receber mensagens da fila de saudação da seguinte maneira:

```csharp
while ((message = myQueueClient.Receive(new TimeSpan(hours: 0, minutes: 0, seconds: 5))) != null)
    {
        Console.WriteLine(string.Format("Message received: {0}, {1}, {2}", message.SequenceNumber, message.Label, message.MessageId));
        message.Complete();

        Console.WriteLine("Processing message (sleeping...)");
        Thread.Sleep(1000);
    }
```

Em Olá [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) modo, Olá receber operação é a única etapa; ou seja, quando o barramento de serviço recebe a solicitação de hello, ele marca a mensagem de saudação como sendo consumida e retorna-toohello aplicativo. **ReceiveAndDelete** modo é o modelo mais simples de saudação e funciona melhor para cenários em que Olá aplicativo pode tolerar o não processar uma mensagem em caso de saudação de uma falha. toounderstand isso, considere um cenário em que problemas do consumidor Olá Olá receber a solicitação e falha antes de processá-lo. Porque o barramento de serviço marca a mensagem de saudação como sendo consumida, quando o aplicativo hello reinicia e começa a consumir mensagens novamente, ele terá perdido mensagem de saudação foi consumido falha toohello anterior.

Em [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) modo, Olá receber operação torna-se dois estágios, que torna possível toosupport aplicativos que não podem tolerar mensagens ausentes. Ao barramento de serviço recebe a solicitação de Olá, localiza Olá próxima mensagem toobe consumida, boqueia-tooprevent outros consumidores do recebimento e, em seguida, ele retorna toohello aplicativo. Depois que o aplicativo hello termina de processar a mensagem de saudação (ou armazena com segurança para processamento futuro), ele conclui Olá segunda etapa de saudação processo de recebimento chamando [concluir](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) na mensagem recebida. Quando o Service Bus vê Olá **concluir** chamada, ele marca a mensagem de saudação como sendo consumida.

Caso o aplicativo hello não é possível tooprocess Olá mensagem por algum motivo, ele pode chamar hello [abandonar](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) método na mensagem recebida (em vez de [concluir](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)). Isso permite que a mensagem de saudação do barramento de serviço toounlock e torná-lo disponível toobe recebida novamente, pelo Olá mesmo consumidor ou por outro consumidor concorrente. Em segundo lugar, há um tempo limite associado bloqueio hello e se o aplicativo hello falha tooprocess Olá mensagem antes de tempo limite de bloqueio de saudação expira (por exemplo, se o aplicativo hello falhar), barramento de serviço desbloqueia a mensagem de saudação e torna disponível toobe recebida novamente (basicamente a realização de uma [abandonar](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) operação por padrão).

Observe que, em Olá evento Olá aplicativo falha após o processamento de mensagem de saudação, mas antes de saudação **concluir** solicitação é emitida, a mensagem de saudação é entregue novamente toohello aplicativo quando ele for reiniciado. Com frequência, isso é chamado de processamento *Pelo menos uma vez*; ou seja, cada mensagem é processada pelo menos uma vez. No entanto, em determinados Olá situações mesma mensagem pode ser entregue novamente. Se o cenário de saudação não puder tolerar o processamento duplicado, lógica adicional será necessária em duplicatas de toodetect de aplicativo hello que podem ser obtidas com base no hello **MessageId** propriedade da mensagem de saudação, que permanece constante entre tentativas de entrega. Isso é conhecido como processamento *Exatamente Uma Vez*.

## <a name="topics-and-subscriptions"></a>Tópicos e assinaturas
Em contraste tooqueues, em que cada mensagem é processada por um único consumidor, *tópicos* e *assinaturas* fornecem uma forma de um-para-muitos de comunicação, em um *depublicação/assinatura* padrão. Útil para dimensionamento toovery grande número de destinatários, cada mensagem publicada é feita tooeach disponível assinatura registrada com o tópico de saudação. As mensagens são enviadas tooa tópico e entregue tooone ou mais assinaturas associadas, dependendo de regras de filtro que podem ser definidas em uma base por assinatura. assinaturas de saudação podem usar mensagens de saudação toorestrict filtros adicionais que deseja tooreceive. As mensagens são enviadas tooa tópico em Olá mesmo propósito são enviados tooa fila, mas as mensagens não são recebidas diretamente do tópico hello. Em vez disso, elas são recebidas de assinaturas. Uma assinatura de tópico é semelhante a uma fila virtual que recebe cópias das mensagens de saudação enviadas toohello tópico. As mensagens são recebidas de uma assinatura de forma idêntica toohello maneira que são recebidas de uma fila.

Por comparação, hello funcionalidade de envio de mensagens de uma fila é mapeado diretamente tooa tópico e sua funcionalidade de recebimento de mensagens mapeia tooa assinatura. Entre outras coisas, isso significa que as assinaturas admitem Olá mesmos padrões descritos anteriormente nesta seção com relação tooqueues: consumidor concorrente, desacoplamento temporal, nivelamento de carga e balanceamento de carga.

Criar um tópico é semelhante toocreating uma fila, conforme mostrado no exemplo hello na seção anterior hello. Criar o URI do serviço hello e use Olá [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) cliente do namespace classe toocreate hello. Você pode criar um tópico usando Olá [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) método. Por exemplo:

```csharp
TopicDescription dataCollectionTopic = namespaceClient.CreateTopic("DataCollectionTopic");
```

Em seguida, adicione assinaturas como desejado:

```csharp
SubscriptionDescription myAgentSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Inventory");
SubscriptionDescription myAuditSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Dashboard");
```

Então, você poderá criar um cliente de tópico. Por exemplo:

```csharp
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider);
TopicClient myTopicClient = factory.CreateTopicClient(myTopic.Path)
```

Usando o remetente da mensagem de saudação, você pode enviar e receber mensagens tooand do tópico hello, conforme mostrado na seção anterior hello. Por exemplo:

```csharp
foreach (BrokeredMessage message in messageList)
{
    myTopicClient.Send(message);
    Console.WriteLine(
    string.Format("Message sent: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

Tooqueues semelhantes, as mensagens são recebidas de uma assinatura usando um [SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient) do objeto, em vez de um [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) objeto. Criar o cliente de assinatura hello, passando o nome Olá Olá tópico, nome hello de assinatura Olá, e (opcionalmente) Olá modo de recebimento como parâmetros. Por exemplo, com hello **inventário** assinatura:

```csharp
// Create hello subscription client
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider); 

SubscriptionClient agentSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Inventory", ReceiveMode.PeekLock);
SubscriptionClient auditSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Dashboard", ReceiveMode.ReceiveAndDelete); 

while ((message = agentSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Inventory...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
    message.Complete();
}          

// Create a receiver using ReceiveAndDelete mode
while ((message = auditSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Dashboard...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

### <a name="rules-and-actions"></a>Regras e ações
Em muitos cenários, as mensagens com características específicas precisam ser processadas de maneiras diferentes. tooenable isso, você pode configurar assinaturas toofind mensagens que tenham propriedades desejadas e, em seguida, executam determinadas propriedades de toothose modificações. Enquanto as assinaturas do barramento de serviço vejam todas as mensagens enviadas toohello tópico, você só pode copiar um subconjunto da fila de assinatura virtual de toohello mensagens. Isso é feito usando filtros de assinatura. Tais modificações são chamadas de *ações de filtro*. Quando uma assinatura é criada, você pode fornecer uma expressão de filtro que opera nas propriedades de saudação de mensagem de saudação, ambos Olá propriedades do sistema (por exemplo, **rótulo**) e as propriedades de aplicativo personalizado (por exemplo, **StoreName**.) Olá expressão de filtro SQL é opcional, nesse caso; sem uma expressão de filtro SQL, qualquer ação de filtro definida em uma assinatura será executada em todas as mensagens de saudação para essa assinatura.

Usando o exemplo anterior de saudação, toofilter mensagens vindas apenas de **Store1**, você deve criar a assinatura do painel de saudação da seguinte maneira:

```csharp
namespaceManager.CreateSubscription("IssueTrackingTopic", "Dashboard", new SqlFilter("StoreName = 'Store1'"));
```

Com esse filtro de assinatura no local, somente as mensagens com hello `StoreName` propriedade definida muito`Store1` são copiados toohello fila virtual Olá `Dashboard` assinatura.

Para obter mais informações sobre possíveis valores de filtro, consulte documentação Olá Olá [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) e [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) classes. Consulte também Olá [mensagens orientadas: filtros avançados](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749) e [tópico filtros](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters) exemplos.

## <a name="next-steps"></a>Próximas etapas
Consulte a seguir Olá tópicos para obter mais informações e exemplos de como usar o barramento de serviço de mensagens avançados.

* [Visão geral de mensagens do Barramento de Serviço](service-bus-messaging-overview.md)
* [Tutorial do .NET do sistema de mensagens agenciado do Barramento de Serviço](service-bus-brokered-tutorial-dotnet.md)
* [Tutorial REST do sistema de mensagens agenciado do Barramento de Serviço](service-bus-brokered-tutorial-rest.md)
* [Exemplo de filtros do tópico](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/TopicFilters)
* [Sistema de mensagens agenciado: filtros avançados](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749)

