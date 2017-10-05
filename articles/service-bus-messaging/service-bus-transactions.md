---
title: "Visão geral do processamento de transações no Barramento de Serviço do Azure | Microsoft Docs"
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
ms.openlocfilehash: a88f2d81ab43e38c9363a67aaefc178b47bfb259
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-service-bus-transaction-processing"></a><span data-ttu-id="f200b-103">Visão geral do processamento de transações do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="f200b-103">Overview of Service Bus transaction processing</span></span>
<span data-ttu-id="f200b-104">Este artigo aborda as funcionalidades de transação do Barramento de Serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="f200b-104">This article discusses the transaction capabilities of Azure Service Bus.</span></span> <span data-ttu-id="f200b-105">Grande parte da discussão é ilustrada na [amostra de Transações atômicas com o Barramento de Serviço](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span><span class="sxs-lookup"><span data-stu-id="f200b-105">Much of the discussion is illustrated by the [Atomic Transactions with Service Bus sample](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span></span> <span data-ttu-id="f200b-106">Este artigo é limitado a uma visão geral do processamento de transações e ao recurso *Enviar por* do Barramento de Serviço, enquanto a amostra Transações atômicas tem um escopo mais amplo e complexo.</span><span class="sxs-lookup"><span data-stu-id="f200b-106">This article is limited to an overview of transaction processing and the *send via* feature in Service Bus, while the Atomic Transactions sample is broader and more complex in scope.</span></span>

## <a name="transactions-in-service-bus"></a><span data-ttu-id="f200b-107">Transações no Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="f200b-107">Transactions in Service Bus</span></span>
<span data-ttu-id="f200b-108">Uma [transação](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) agrupa duas ou mais operações em um *escopo de execução*.</span><span class="sxs-lookup"><span data-stu-id="f200b-108">A [transaction](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) groups two or more operations together into an *execution scope*.</span></span> <span data-ttu-id="f200b-109">Por natureza, essa transação deve garantir que todas as operações que pertencem a determinado grupo de operações sejam concluídas com êxito ou com falha em conjunto.</span><span class="sxs-lookup"><span data-stu-id="f200b-109">By nature, such a transaction must ensure that all operations belonging to a given group of operations either succeed or fail jointly.</span></span> <span data-ttu-id="f200b-110">Nesse sentido, as transações agem como uma unidade, que, geralmente, é conhecida como *atomicidade*.</span><span class="sxs-lookup"><span data-stu-id="f200b-110">In this respect transactions act as one unit, which is often referred to as *atomicity*.</span></span> 

<span data-ttu-id="f200b-111">O Barramento de Serviço é um agente de mensagens transacionais e assegura a integridade transacional de todas as operações internas em seus repositórios de mensagens.</span><span class="sxs-lookup"><span data-stu-id="f200b-111">Service Bus is a transactional message broker and ensures transactional integrity for all internal operations against its message stores.</span></span> <span data-ttu-id="f200b-112">Todas as transferências de mensagens no Barramento de Serviço, como a movimentação de mensagens para uma [fila de mensagens mortas](service-bus-dead-letter-queues.md) ou [encaminhamento automático](service-bus-auto-forwarding.md) de mensagens entre entidades, são transacionais.</span><span class="sxs-lookup"><span data-stu-id="f200b-112">All transfers of messages inside of Service Bus, such as moving messages to a [dead-letter queue](service-bus-dead-letter-queues.md) or [automatic forwarding](service-bus-auto-forwarding.md) of messages between entities, are transactional.</span></span> <span data-ttu-id="f200b-113">Assim, caso o Barramento de Serviço aceite uma mensagem, isso significa ela já foi armazenada e rotulada com um número de sequência.</span><span class="sxs-lookup"><span data-stu-id="f200b-113">As such, if Service Bus accepts a message, it has already been stored and labeled with a sequence number.</span></span> <span data-ttu-id="f200b-114">Daí em diante, todas as transferências de mensagens no Barramento de Serviço são operações coordenadas entre entidades e não resultarão em perda (origem com êxito e destino com falha) nem em duplicação (origem com falha e destino com êxito) da mensagem.</span><span class="sxs-lookup"><span data-stu-id="f200b-114">From then on, any message transfers within Service Bus are coordinated operations across entities, and will neither lead to loss (source succeeds and target fails) or to duplication (source fails and target succeeds) of the message.</span></span>

<span data-ttu-id="f200b-115">O Barramento de Serviço dá suporte a operações de agrupamento em uma única entidade de mensagens (fila, tópico e assinatura) no escopo de uma transação.</span><span class="sxs-lookup"><span data-stu-id="f200b-115">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within the scope of a transaction.</span></span> <span data-ttu-id="f200b-116">Por exemplo, você pode enviar várias mensagens para uma fila em um escopo de transação, e as mensagens só serão confirmadas no log da fila quando a transação for concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="f200b-116">For example, you can send several messages to one queue from within a transaction scope, and the messages will only be committed to the queue's log when the transaction successfully completes.</span></span>

## <a name="operations-within-a-transaction-scope"></a><span data-ttu-id="f200b-117">Operações em um escopo de transação</span><span class="sxs-lookup"><span data-stu-id="f200b-117">Operations within a transaction scope</span></span>
<span data-ttu-id="f200b-118">As operações que podem ser executadas em um escopo de transação são as seguintes:</span><span class="sxs-lookup"><span data-stu-id="f200b-118">The operations that can be performed within a transaction scope are as follows:</span></span>

* <span data-ttu-id="f200b-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span><span class="sxs-lookup"><span data-stu-id="f200b-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span></span> 
* <span data-ttu-id="f200b-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span><span class="sxs-lookup"><span data-stu-id="f200b-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span></span> 

<span data-ttu-id="f200b-121">As operações de recebimento não são incluídas, pois presume-se que o aplicativo obtenha as mensagens usando o modo [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) em algum loop de recebimento ou com um retorno de chamada [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) e só então abre um escopo de transação para o processamento da mensagem.</span><span class="sxs-lookup"><span data-stu-id="f200b-121">Receive operations are not included, because it is assumed that the application acquires messages using the [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, inside some receive loop or with an [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback, and only then opens a transaction scope for processing the message.</span></span>

<span data-ttu-id="f200b-122">Em seguida, a disposição da mensagem (conclusão, abandono, mensagens mortas, adiamento) ocorre no escopo do resultado geral da transação e depende dele.</span><span class="sxs-lookup"><span data-stu-id="f200b-122">The disposition of the message (complete, abandon, dead-letter, defer) then occurs within the scope of, and dependent on, the overall outcome of the transaction.</span></span>

## <a name="transfers-and-send-via"></a><span data-ttu-id="f200b-123">Transferências e “enviar por”</span><span class="sxs-lookup"><span data-stu-id="f200b-123">Transfers and "send via"</span></span>
<span data-ttu-id="f200b-124">Para habilitar a transferência transacional dos dados de uma fila para um processador e, em seguida, para outra fila, o Barramento de Serviço dá suporte a *transferências*.</span><span class="sxs-lookup"><span data-stu-id="f200b-124">To enable transactional handover of data from a queue to a processor, and then to another queue, Service Bus supports *transfers*.</span></span> <span data-ttu-id="f200b-125">Em uma operação de transferência, um remetente primeiro envia uma mensagem para uma “fila de transferência” e a fila de transferência move imediatamente a mensagem para a fila de destino pretendida usando a mesma implementação de transferência robusta da qual a funcionalidade de encaminhamento automático depende.</span><span class="sxs-lookup"><span data-stu-id="f200b-125">In a transfer operation, a sender first sends a message to a "transfer queue" and the transfer queue immediately moves the message to the intended destination queue using the same robust transfer implementation that the auto-forward capability relies on.</span></span> <span data-ttu-id="f200b-126">A mensagem nunca é confirmada no log da fila de transferência de modo que fique visível para os consumidores da fila de transferência.</span><span class="sxs-lookup"><span data-stu-id="f200b-126">The message is never committed to the transfer queue's log in a way that it becomes visible for the transfer queue's consumers.</span></span>

<span data-ttu-id="f200b-127">A potência dessa funcionalidade transacional se torna aparente quando a própria fila de transferência é a origem das mensagens de entrada do remetente.</span><span class="sxs-lookup"><span data-stu-id="f200b-127">The power of this transactional capability becomes apparent when the transfer queue itself is the source of the sender's input messages.</span></span> <span data-ttu-id="f200b-128">Em outras palavras, o Barramento de Serviço pode transferir a mensagem para a fila de destino por meio da fila de transferência, ao mesmo tempo que executa uma operação de conclusão (ou adiamento ou mensagens mortas) nas mensagens de entrada, tudo em uma única operação atômica.</span><span class="sxs-lookup"><span data-stu-id="f200b-128">In other words, Service Bus can transfer the message to the destination queue "via" the transfer queue, while performing a complete (or defer, or dead-letter) operation on the input message, all in one atomic operation.</span></span> 

### <a name="see-it-in-code"></a><span data-ttu-id="f200b-129">Ver em código</span><span class="sxs-lookup"><span data-stu-id="f200b-129">See it in code</span></span>
<span data-ttu-id="f200b-130">Para configurar essas transferências, você cria um remetente da mensagem que tem como alvo a fila de destino por meio da fila de transferência.</span><span class="sxs-lookup"><span data-stu-id="f200b-130">To set up such transfers, you create a message sender that targets the destination queue via the transfer queue.</span></span> <span data-ttu-id="f200b-131">Você também terá um destinatário que efetua pull das mensagens dessa mesma fila.</span><span class="sxs-lookup"><span data-stu-id="f200b-131">You will also have a receiver that pulls messages from that same queue.</span></span> <span data-ttu-id="f200b-132">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f200b-132">For example:</span></span>

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

<span data-ttu-id="f200b-133">Uma transação simples usa então esses elementos, como mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="f200b-133">A simple transaction then uses these elements, as in the following example:</span></span>

```csharp
var msg = receiver.Receive();

using (scope = new TransactionScope())
{
    // Do whatever work is required 

    var newmsg = ... // package the result 

    msg.Complete(); // mark the message as done
    sender.Send(newmsg); // forward the result

    scope.Complete(); // declare the transaction done
} 
```

## <a name="next-steps"></a><span data-ttu-id="f200b-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f200b-134">Next steps</span></span>

<span data-ttu-id="f200b-135">Confira os artigos a seguir para obter mais informações sobre as filas do Barramento de Serviço:</span><span class="sxs-lookup"><span data-stu-id="f200b-135">See the following articles for more information about Service Bus queues:</span></span>

* [<span data-ttu-id="f200b-136">Encadeando entidades do Barramento de Serviço com o encaminhamento automático</span><span class="sxs-lookup"><span data-stu-id="f200b-136">Chaining Service Bus entities with auto-forwarding</span></span>](service-bus-auto-forwarding.md)
* [<span data-ttu-id="f200b-137">Amostra de encaminhamento automático</span><span class="sxs-lookup"><span data-stu-id="f200b-137">Auto-forward sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [<span data-ttu-id="f200b-138">Amostra de Transações atômicas com o Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="f200b-138">Atomic Transactions with Service Bus sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [<span data-ttu-id="f200b-139">Filas do Azure e filas do Barramento de Serviço – comparações</span><span class="sxs-lookup"><span data-stu-id="f200b-139">Azure Queues and Service Bus queues compared</span></span>](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [<span data-ttu-id="f200b-140">Como usar filas do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="f200b-140">How to use Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

