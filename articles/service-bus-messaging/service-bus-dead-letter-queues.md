---
title: filas de aaaService barramento mensagens mortas | Microsoft Docs
description: "Visão geral das filas de mensagens mortas do Barramento de Serviço"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68b2aa38-dba7-491a-9c26-0289bc15d397
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: 1638272085b8a3a59e8814f6f943caee35a2bfdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-dead-letter-queues"></a>Visão geral das filas de mensagens mortas do Barramento de Serviço 

As filas e as assinaturas de tópico do Barramento de Serviço fornecem uma subfila secundária chamada DLQ (*fila de mensagens mortas*). fila de mensagens mortas Olá não precisa toobe explicitamente criado e não pode ser excluído ou não independentes gerenciados da entidade principal hello.

Este artigo discute as filas de mensagens mortas no barramento de serviço do Azure. Grande parte da discussão Olá é ilustrada Olá [exemplo de filas de mensagens mortas](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/DeadletterQueue) no GitHub.
 
## <a name="hello-dead-letter-queue"></a>fila de mensagens mortas Olá

finalidade de saudação da fila de mensagens mortas Olá é mensagens de toohold que não podem ser entregues tooany receptor, ou que não pôde ser processado. Mensagens podem ser removidas da saudação DLQ e inspecionadas. Um aplicativo pode, com a Ajuda de um operador, corrigir problemas e reenviar a mensagem de saudação fatos Olá que houve um erro de log e tomar uma ação corretiva. 

De uma perspectiva de API e o protocolo, Olá DLQ é principalmente tooany semelhante outra fila, exceto que as mensagens podem ser enviadas somente por meio de gesto de mensagens mortas Olá da entidade pai de saudação. Além disso, a vida útil não é observada, e você não pode colocar uma mensagem em estado morto na DLQ. fila de mensagens mortas Olá totalmente dá suporte a operações transacionais e entrega de bloqueio de pico.

Observe que não há nenhuma limpeza automática de saudação DLQ. As mensagens permanecem na Olá DLQ até que você explicitamente recuperá-las do hello DLQ e chamada [Complete ()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_CompleteAsync) na mensagem de saudação do mensagens mortas.

## <a name="moving-messages-toohello-dlq"></a>Mover mensagens toohello DLQ

Há várias atividades no barramento de serviço que causam tooget mensagens enviada toohello DLQ de dentro do próprio mecanismo de mensagens de saudação. Um aplicativo explicitamente pode mover mensagens toohello DLQ. 

Como a mensagem de saudação é movida pelo agente Olá, duas propriedades são adicionadas toohello mensagem como broker Olá chama sua versão interna do hello [mensagens mortas](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeadLetter_System_String_System_String_) método na mensagem de saudação: `DeadLetterReason` e `DeadLetterErrorDescription`.

Os aplicativos podem definir seus próprios códigos de saudação `DeadLetterReason` propriedade, mas Olá sistema conjuntos Olá valores a seguir.

| Condição | DeadLetterReason | DeadLetterErrorDescription |
| --- | --- | --- |
| Sempre |HeaderSizeExceeded |cota de tamanho de saudação para este fluxo foi excedida. |
| !TopicDescription.<br />EnableFilteringMessagesBeforePublishing e SubscriptionDescription.<br />EnableDeadLetteringOnFilterEvaluationExceptions |exception.GetType().Name |exception.Message |
| EnableDeadLetteringOnMessageExpiration |TTLExpiredException |mensagem de saudação expirou e foi considerada morta dead. |
| SubscriptionDescription.RequiresSession |A ID da sessão é nula. |A entidade habilitada para sessão não permite uma mensagem cuja identificação de sessão seja nula. |
| !fila de mensagens mortas |MaxTransferHopCountExceeded |Nulo |
| Mensagem morta explícita do aplicativo |Especificado pelo aplicativo |Especificado pelo aplicativo |

## <a name="exceeding-maxdeliverycount"></a>Excedendo MaxDeliveryCount
Filas e assinaturas têm um [QueueDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount) e [SubscriptionDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_MaxDeliveryCount) propriedade respectivamente; hello o valor padrão é 10. Sempre que uma mensagem foi entregue em um bloqueio ([Receivemode](/dotnet/api/microsoft.servicebus.messaging.receivemode)), mas o foi explicitamente abandonada ou bloqueio Olá tiver expirado, mensagem de saudação [BrokeredMessage.DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) é incrementado. Quando [DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) excede [MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount), mensagem de saudação é movido toohello DLQ, especificando Olá `MaxDeliveryCountExceeded` código de motivo.

Esse comportamento não pode ser desabilitado, mas você pode definir [MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount) número muito grande de tooa.

## <a name="exceeding-timetolive"></a>Excedendo TimeToLive
Olá quando [QueueDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnableDeadLetteringOnMessageExpiration) ou [SubscriptionDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnMessageExpiration) propriedade for definida muito**true** (saudação padrão é **false**), todas as mensagens expiradas são movido toohello DLQ, especificando Olá `TTLExpiredException` código de motivo.

Observe que as mensagens expiradas só são limpos e, portanto, movido toohello DLQ quando há pelo menos um destinatário active puxando a fila principal hello ou assinatura; Esse comportamento ocorre por design.

## <a name="errors-while-processing-subscription-rules"></a>Erros ao processar as regras de assinatura
Olá quando [SubscriptionDescription.EnableDeadLetteringOnFilterEvaluationExceptions](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnFilterEvaluationExceptions) propriedade está habilitada para uma assinatura, os erros que ocorrem durante a execução de regra de filtro SQL da assinatura são capturados no hello DLQ juntamente com a cadeia de mensagem de saudação.

## <a name="application-level-dead-lettering"></a>Mensagens mortas no nível de aplicativo
Em adição toohello fornecido pelo sistema mensagens mortas recursos, os aplicativos podem usar mensagens inaceitáveis de rejeição Olá DLQ tooexplicitly. Isso pode incluir as mensagens que não podem ser processadas corretamente devido tooany classificação de problema do sistema, as mensagens que contêm cargas malformadas ou mensagens de falham quando algum esquema de segurança de nível de mensagem é usada na autenticação.

## <a name="dead-lettering-in-forwardto-or-sendvia-scenarios"></a>Mensagens mortas em cenários de ForwardTo ou SendVia

As mensagens serão enviados toohello fila de mensagens mortas de transferência em Olá condições a seguir:

- Uma mensagem passa por mais de 3 filas ou tópicos [encadeados](service-bus-auto-forwarding.md).
- Olá destino fila ou tópico está desabilitado ou excluído.
- Olá destino fila ou tópico excede o tamanho máximo de entidade de saudação.

tooretrieve essas mensagens mortas morta, você pode criar um destinatário usando Olá [FormatTransferDeadletterPath](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_FormatTransferDeadLetterPath_System_String_) método utilitário.

## <a name="example"></a>Exemplo
saudação de trecho de código a seguir cria um destinatário da mensagem. Olá receber loop para fila principal hello, código Olá recupera a mensagem de saudação com [Receive(TimeSpan.Zero)](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_Receive_System_TimeSpan_), que solicita a saudação broker tooinstantly retorno qualquer mensagem prontamente disponível ou tooreturn com nenhum resultado. Se o código de saudação recebe uma mensagem, ele imediatamente abandona, que incrementa Olá `DeliveryCount`. Depois que o sistema Olá move a mensagem de saudação toohello DLQ, fila principal hello está vazia e Olá sai do loop, como [ReceiveAsync](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_ReceiveAsync_System_TimeSpan_) retorna **nulo**.

```csharp
var receiver = await receiverFactory.CreateMessageReceiverAsync(queueName, ReceiveMode.PeekLock);
while(true)
{
    var msg = await receiver.ReceiveAsync(TimeSpan.Zero);
    if (msg != null)
    {
        Console.WriteLine("Picked up message; DeliveryCount {0}", msg.DeliveryCount);
        await msg.AbandonAsync();
    }
    else
    {
        break;
    }
}
```

## <a name="next-steps"></a>Próximas etapas
Consulte Olá artigos para obter mais informações sobre as filas do barramento de serviço a seguir:

* [Introdução às filas do Barramento de Serviço](service-bus-dotnet-get-started-with-queues.md)
* [Filas do Azure e filas do Barramento de Serviço – comparações](service-bus-azure-and-service-bus-queues-compared-contrasted.md)

