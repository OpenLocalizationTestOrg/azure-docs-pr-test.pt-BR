---
title: "aaaOverview de processamento de transações em um barramento de serviço do Azure | Microsoft Docs"
description: "Visão geral das transações atômicas do Barramento de Serviço do Azure e do recurso Enviar por"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64449247-1026-44ba-b15a-9610f9385ed8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: 5ed4d1fd3a089b8ebcd69a568f4ac863e753aecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-transaction-processing"></a>Visão geral do processamento de transações do Barramento de Serviço
Este artigo aborda os recursos de transação de saudação do barramento de serviço do Azure. Grande parte da discussão Olá é ilustrada Olá [transações atômicas com exemplo de barramento de serviço](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions). Este artigo é visão geral de tooan limitada de processamento de transações e hello *Enviar via* recurso no barramento de serviço, enquanto o exemplo de transações atômicas hello é mais amplo e mais complexas no escopo.

## <a name="transactions-in-service-bus"></a>Transações no Barramento de Serviço
Uma [transação](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) agrupa duas ou mais operações em um *escopo de execução*. Por natureza, uma transação deve garantir que todas as operações que pertencem a tooa fornecido o grupo de operações bem-sucedidas ou falham em conjunto. Nesse sentido, as transações agem como uma unidade, que é geralmente chamado tooas *atomicidade*. 

O Barramento de Serviço é um agente de mensagens transacionais e assegura a integridade transacional de todas as operações internas em seus repositórios de mensagens. Todas as transferências de mensagens dentro de barramento de serviço, como mover tooa de mensagens [fila de mensagens mortas](service-bus-dead-letter-queues.md) ou [encaminhamento automático](service-bus-auto-forwarding.md) de mensagens entre entidades, são transacionais. Assim, caso o Barramento de Serviço aceite uma mensagem, isso significa ela já foi armazenada e rotulada com um número de sequência. Daí em seguida diante, qualquer transferência de mensagem no barramento de serviço é operações coordenadas entre entidades, e nenhum levará tooloss (origem terá êxito e falha de destino) ou tooduplication (Falha de origem e destino for bem-sucedida) da mensagem de saudação.

Barramento de serviço oferece suporte a operações de agrupamento em uma única entidade de mensagens (fila, tópico, assinatura) dentro do escopo de saudação de uma transação. Por exemplo, você pode enviar várias filas de tooone mensagens de dentro de um escopo de transação e mensagens de saudação só será log toohello confirmada da fila quando a transação de saudação seja concluída com êxito.

## <a name="operations-within-a-transaction-scope"></a>Operações em um escopo de transação
operações de saudação que podem ser executadas em um escopo de transação são da seguinte maneira:

* **[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync 
* **[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync 

Receber operações não são incluídas, porque supõe-se que o aplicativo hello adquire mensagens usando Olá [Receivemode](/dotnet/api/microsoft.servicebus.messaging.receivemode) loop de recebimento de modo dentro de alguns ou com um [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) retorno de chamada, e só depois abre uma transação de escopo para processar a mensagem de saudação.

Olá disposição de mensagem de saudação (completa, abandono, mensagens mortas, adiar), em seguida, ocorre dentro de escopo hello e dependente, hello resultado geral da transação de saudação.

## <a name="transfers-and-send-via"></a>Transferências e “enviar por”
tooenable transferência transacional dos dados de um processador de fila de tooa e tooanother fila, Service Bus suporta *transferências*. Em uma operação de transferência, um remetente primeiro envia uma mensagem tooa "fila de transferência" e fila de transferência Olá move imediatamente toohello de mensagem de saudação se destina a fila de destino usando Olá mesmo robusto transferir implementação que depende do encaminhamento automático de saudação no. mensagem de saudação nunca é log da fila de transferência toohello confirmados de forma que ele fique visível para os consumidores da fila de transferência hello.

energia Olá dessa funcionalidade transacional se torna aparente quando a própria fila de transferência Olá é a origem de saudação de mensagens de entrada do remetente hello. Em outras palavras, barramento de serviço pode transferir fila de destino de toohello de mensagem de saudação "via" fila de transferência hello, ao executar uma completa (ou adiar, ou inatividade) operação na mensagem de entrada hello, tudo em uma operação atômica. 

### <a name="see-it-in-code"></a>Ver em código
tooset backup essas transferências, você cria um remetente da mensagem que tem como alvo a fila de destino Olá por meio de fila de transferência de saudação. Você também terá um destinatário que efetua pull das mensagens dessa mesma fila. Por exemplo:

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

Uma transação simple, em seguida, usa esses elementos, como no exemplo a seguir de saudação:

```csharp
var msg = receiver.Receive();

using (scope = new TransactionScope())
{
    // Do whatever work is required 

    var newmsg = ... // package hello result 

    msg.Complete(); // mark hello message as done
    sender.Send(newmsg); // forward hello result

    scope.Complete(); // declare hello transaction done
} 
```

## <a name="next-steps"></a>Próximas etapas

Consulte Olá artigos para obter mais informações sobre as filas do barramento de serviço a seguir:

* [Encadeando entidades do Barramento de Serviço com o encaminhamento automático](service-bus-auto-forwarding.md)
* [Amostra de encaminhamento automático](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [Amostra de Transações atômicas com o Barramento de Serviço](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [Filas do Azure e filas do Barramento de Serviço – comparações](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [Como as filas do barramento de serviço toouse](service-bus-dotnet-get-started-with-queues.md)

