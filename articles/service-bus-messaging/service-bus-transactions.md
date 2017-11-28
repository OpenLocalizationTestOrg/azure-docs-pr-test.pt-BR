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
# <a name="overview-of-service-bus-transaction-processing"></a><span data-ttu-id="659c3-103">Visão geral do processamento de transações do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="659c3-103">Overview of Service Bus transaction processing</span></span>
<span data-ttu-id="659c3-104">Este artigo aborda os recursos de transação de saudação do barramento de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="659c3-104">This article discusses hello transaction capabilities of Azure Service Bus.</span></span> <span data-ttu-id="659c3-105">Grande parte da discussão Olá é ilustrada Olá [transações atômicas com exemplo de barramento de serviço](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span><span class="sxs-lookup"><span data-stu-id="659c3-105">Much of hello discussion is illustrated by hello [Atomic Transactions with Service Bus sample](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span></span> <span data-ttu-id="659c3-106">Este artigo é visão geral de tooan limitada de processamento de transações e hello *Enviar via* recurso no barramento de serviço, enquanto o exemplo de transações atômicas hello é mais amplo e mais complexas no escopo.</span><span class="sxs-lookup"><span data-stu-id="659c3-106">This article is limited tooan overview of transaction processing and hello *send via* feature in Service Bus, while hello Atomic Transactions sample is broader and more complex in scope.</span></span>

## <a name="transactions-in-service-bus"></a><span data-ttu-id="659c3-107">Transações no Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="659c3-107">Transactions in Service Bus</span></span>
<span data-ttu-id="659c3-108">Uma [transação](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) agrupa duas ou mais operações em um *escopo de execução*.</span><span class="sxs-lookup"><span data-stu-id="659c3-108">A [transaction](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) groups two or more operations together into an *execution scope*.</span></span> <span data-ttu-id="659c3-109">Por natureza, uma transação deve garantir que todas as operações que pertencem a tooa fornecido o grupo de operações bem-sucedidas ou falham em conjunto.</span><span class="sxs-lookup"><span data-stu-id="659c3-109">By nature, such a transaction must ensure that all operations belonging tooa given group of operations either succeed or fail jointly.</span></span> <span data-ttu-id="659c3-110">Nesse sentido, as transações agem como uma unidade, que é geralmente chamado tooas *atomicidade*.</span><span class="sxs-lookup"><span data-stu-id="659c3-110">In this respect transactions act as one unit, which is often referred tooas *atomicity*.</span></span> 

<span data-ttu-id="659c3-111">O Barramento de Serviço é um agente de mensagens transacionais e assegura a integridade transacional de todas as operações internas em seus repositórios de mensagens.</span><span class="sxs-lookup"><span data-stu-id="659c3-111">Service Bus is a transactional message broker and ensures transactional integrity for all internal operations against its message stores.</span></span> <span data-ttu-id="659c3-112">Todas as transferências de mensagens dentro de barramento de serviço, como mover tooa de mensagens [fila de mensagens mortas](service-bus-dead-letter-queues.md) ou [encaminhamento automático](service-bus-auto-forwarding.md) de mensagens entre entidades, são transacionais.</span><span class="sxs-lookup"><span data-stu-id="659c3-112">All transfers of messages inside of Service Bus, such as moving messages tooa [dead-letter queue](service-bus-dead-letter-queues.md) or [automatic forwarding](service-bus-auto-forwarding.md) of messages between entities, are transactional.</span></span> <span data-ttu-id="659c3-113">Assim, caso o Barramento de Serviço aceite uma mensagem, isso significa ela já foi armazenada e rotulada com um número de sequência.</span><span class="sxs-lookup"><span data-stu-id="659c3-113">As such, if Service Bus accepts a message, it has already been stored and labeled with a sequence number.</span></span> <span data-ttu-id="659c3-114">Daí em seguida diante, qualquer transferência de mensagem no barramento de serviço é operações coordenadas entre entidades, e nenhum levará tooloss (origem terá êxito e falha de destino) ou tooduplication (Falha de origem e destino for bem-sucedida) da mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="659c3-114">From then on, any message transfers within Service Bus are coordinated operations across entities, and will neither lead tooloss (source succeeds and target fails) or tooduplication (source fails and target succeeds) of hello message.</span></span>

<span data-ttu-id="659c3-115">Barramento de serviço oferece suporte a operações de agrupamento em uma única entidade de mensagens (fila, tópico, assinatura) dentro do escopo de saudação de uma transação.</span><span class="sxs-lookup"><span data-stu-id="659c3-115">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within hello scope of a transaction.</span></span> <span data-ttu-id="659c3-116">Por exemplo, você pode enviar várias filas de tooone mensagens de dentro de um escopo de transação e mensagens de saudação só será log toohello confirmada da fila quando a transação de saudação seja concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="659c3-116">For example, you can send several messages tooone queue from within a transaction scope, and hello messages will only be committed toohello queue's log when hello transaction successfully completes.</span></span>

## <a name="operations-within-a-transaction-scope"></a><span data-ttu-id="659c3-117">Operações em um escopo de transação</span><span class="sxs-lookup"><span data-stu-id="659c3-117">Operations within a transaction scope</span></span>
<span data-ttu-id="659c3-118">operações de saudação que podem ser executadas em um escopo de transação são da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="659c3-118">hello operations that can be performed within a transaction scope are as follows:</span></span>

* <span data-ttu-id="659c3-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span><span class="sxs-lookup"><span data-stu-id="659c3-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span></span> 
* <span data-ttu-id="659c3-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span><span class="sxs-lookup"><span data-stu-id="659c3-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span></span> 

<span data-ttu-id="659c3-121">Receber operações não são incluídas, porque supõe-se que o aplicativo hello adquire mensagens usando Olá [Receivemode](/dotnet/api/microsoft.servicebus.messaging.receivemode) loop de recebimento de modo dentro de alguns ou com um [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) retorno de chamada, e só depois abre uma transação de escopo para processar a mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="659c3-121">Receive operations are not included, because it is assumed that hello application acquires messages using hello [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, inside some receive loop or with an [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback, and only then opens a transaction scope for processing hello message.</span></span>

<span data-ttu-id="659c3-122">Olá disposição de mensagem de saudação (completa, abandono, mensagens mortas, adiar), em seguida, ocorre dentro de escopo hello e dependente, hello resultado geral da transação de saudação.</span><span class="sxs-lookup"><span data-stu-id="659c3-122">hello disposition of hello message (complete, abandon, dead-letter, defer) then occurs within hello scope of, and dependent on, hello overall outcome of hello transaction.</span></span>

## <a name="transfers-and-send-via"></a><span data-ttu-id="659c3-123">Transferências e “enviar por”</span><span class="sxs-lookup"><span data-stu-id="659c3-123">Transfers and "send via"</span></span>
<span data-ttu-id="659c3-124">tooenable transferência transacional dos dados de um processador de fila de tooa e tooanother fila, Service Bus suporta *transferências*.</span><span class="sxs-lookup"><span data-stu-id="659c3-124">tooenable transactional handover of data from a queue tooa processor, and then tooanother queue, Service Bus supports *transfers*.</span></span> <span data-ttu-id="659c3-125">Em uma operação de transferência, um remetente primeiro envia uma mensagem tooa "fila de transferência" e fila de transferência Olá move imediatamente toohello de mensagem de saudação se destina a fila de destino usando Olá mesmo robusto transferir implementação que depende do encaminhamento automático de saudação no.</span><span class="sxs-lookup"><span data-stu-id="659c3-125">In a transfer operation, a sender first sends a message tooa "transfer queue" and hello transfer queue immediately moves hello message toohello intended destination queue using hello same robust transfer implementation that hello auto-forward capability relies on.</span></span> <span data-ttu-id="659c3-126">mensagem de saudação nunca é log da fila de transferência toohello confirmados de forma que ele fique visível para os consumidores da fila de transferência hello.</span><span class="sxs-lookup"><span data-stu-id="659c3-126">hello message is never committed toohello transfer queue's log in a way that it becomes visible for hello transfer queue's consumers.</span></span>

<span data-ttu-id="659c3-127">energia Olá dessa funcionalidade transacional se torna aparente quando a própria fila de transferência Olá é a origem de saudação de mensagens de entrada do remetente hello.</span><span class="sxs-lookup"><span data-stu-id="659c3-127">hello power of this transactional capability becomes apparent when hello transfer queue itself is hello source of hello sender's input messages.</span></span> <span data-ttu-id="659c3-128">Em outras palavras, barramento de serviço pode transferir fila de destino de toohello de mensagem de saudação "via" fila de transferência hello, ao executar uma completa (ou adiar, ou inatividade) operação na mensagem de entrada hello, tudo em uma operação atômica.</span><span class="sxs-lookup"><span data-stu-id="659c3-128">In other words, Service Bus can transfer hello message toohello destination queue "via" hello transfer queue, while performing a complete (or defer, or dead-letter) operation on hello input message, all in one atomic operation.</span></span> 

### <a name="see-it-in-code"></a><span data-ttu-id="659c3-129">Ver em código</span><span class="sxs-lookup"><span data-stu-id="659c3-129">See it in code</span></span>
<span data-ttu-id="659c3-130">tooset backup essas transferências, você cria um remetente da mensagem que tem como alvo a fila de destino Olá por meio de fila de transferência de saudação.</span><span class="sxs-lookup"><span data-stu-id="659c3-130">tooset up such transfers, you create a message sender that targets hello destination queue via hello transfer queue.</span></span> <span data-ttu-id="659c3-131">Você também terá um destinatário que efetua pull das mensagens dessa mesma fila.</span><span class="sxs-lookup"><span data-stu-id="659c3-131">You will also have a receiver that pulls messages from that same queue.</span></span> <span data-ttu-id="659c3-132">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="659c3-132">For example:</span></span>

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

<span data-ttu-id="659c3-133">Uma transação simple, em seguida, usa esses elementos, como no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="659c3-133">A simple transaction then uses these elements, as in hello following example:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="659c3-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="659c3-134">Next steps</span></span>

<span data-ttu-id="659c3-135">Consulte Olá artigos para obter mais informações sobre as filas do barramento de serviço a seguir:</span><span class="sxs-lookup"><span data-stu-id="659c3-135">See hello following articles for more information about Service Bus queues:</span></span>

* [<span data-ttu-id="659c3-136">Encadeando entidades do Barramento de Serviço com o encaminhamento automático</span><span class="sxs-lookup"><span data-stu-id="659c3-136">Chaining Service Bus entities with auto-forwarding</span></span>](service-bus-auto-forwarding.md)
* [<span data-ttu-id="659c3-137">Amostra de encaminhamento automático</span><span class="sxs-lookup"><span data-stu-id="659c3-137">Auto-forward sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [<span data-ttu-id="659c3-138">Amostra de Transações atômicas com o Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="659c3-138">Atomic Transactions with Service Bus sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [<span data-ttu-id="659c3-139">Filas do Azure e filas do Barramento de Serviço – comparações</span><span class="sxs-lookup"><span data-stu-id="659c3-139">Azure Queues and Service Bus queues compared</span></span>](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [<span data-ttu-id="659c3-140">Como as filas do barramento de serviço toouse</span><span class="sxs-lookup"><span data-stu-id="659c3-140">How toouse Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

