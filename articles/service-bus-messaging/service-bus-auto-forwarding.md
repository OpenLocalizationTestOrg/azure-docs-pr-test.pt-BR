---
title: "Encaminhamento automático de entidades de mensagens do Barramento de Serviço do Azure | Microsoft Docs"
description: "Como encadear uma fila ou assinatura do Barramento de Serviço em outra fila ou outro tópico."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f7060778-3421-402c-97c7-735dbf6a61e8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 2656b3a276c542ca836b3949e4e493d7c7f48f16
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a><span data-ttu-id="631e5-103">Encadeando entidades do Barramento de Serviço com o encaminhamento automático</span><span class="sxs-lookup"><span data-stu-id="631e5-103">Chaining Service Bus entities with auto-forwarding</span></span>

<span data-ttu-id="631e5-104">O recurso *encaminhamento automático* do Barramento de Serviço permite encadear uma fila ou assinatura a outra fila ou outro tópico que faz parte do mesmo namespace.</span><span class="sxs-lookup"><span data-stu-id="631e5-104">The Service Bus *auto-forwarding* feature enables you to chain a queue or subscription to another queue or topic that is part of the same namespace.</span></span> <span data-ttu-id="631e5-105">Quando o encaminhamento automático está habilitado, o Barramento de Serviço remove automaticamente as mensagens colocadas na primeira fila ou assinatura (origem) e as coloca na segunda fila ou no segundo tópico (destino).</span><span class="sxs-lookup"><span data-stu-id="631e5-105">When auto-forwarding is enabled, Service Bus automatically removes messages that are placed in the first queue or subscription (source) and puts them in the second queue or topic (destination).</span></span> <span data-ttu-id="631e5-106">Observe que ainda é possível enviar uma mensagem diretamente para a entidade de destino.</span><span class="sxs-lookup"><span data-stu-id="631e5-106">Note that it is still possible to send a message to the destination entity directly.</span></span> <span data-ttu-id="631e5-107">Além disso, não é possível encadear uma subfila, por exemplo, uma fila de mensagens mortas, em outra fila ou outro tópico.</span><span class="sxs-lookup"><span data-stu-id="631e5-107">Also, it is not possible to chain a subqueue, such as a deadletter queue, to another queue or topic.</span></span>

## <a name="using-auto-forwarding"></a><span data-ttu-id="631e5-108">Usando o encaminhamento automático</span><span class="sxs-lookup"><span data-stu-id="631e5-108">Using auto-forwarding</span></span>
<span data-ttu-id="631e5-109">Você pode habilitar o encaminhamento automático configurando as propriedades [QueueDescription.ForwardTo][QueueDescription.ForwardTo] ou [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] nos objetos [QueueDescription][QueueDescription] ou [SubscriptionDescription][SubscriptionDescription] para a origem, como no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="631e5-109">You can enable auto-forwarding by setting the [QueueDescription.ForwardTo][QueueDescription.ForwardTo] or [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] properties on the [QueueDescription][QueueDescription] or [SubscriptionDescription][SubscriptionDescription] objects for the source, as in the following example.</span></span>

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

<span data-ttu-id="631e5-110">A entidade de destino deverá existir no momento da criação da entidade de origem.</span><span class="sxs-lookup"><span data-stu-id="631e5-110">The destination entity must exist at the time the source entity is created.</span></span> <span data-ttu-id="631e5-111">Se a entidade de destino não existir, o Barramento de Serviço retornará uma exceção quando receber uma solicitação para criar a entidade de origem.</span><span class="sxs-lookup"><span data-stu-id="631e5-111">If the destination entity does not exist, Service Bus returns an exception when asked to create the source entity.</span></span>

<span data-ttu-id="631e5-112">Você pode usar o encaminhamento automático para escalar horizontalmente um tópico individual.</span><span class="sxs-lookup"><span data-stu-id="631e5-112">You can use auto-forwarding to scale out an individual topic.</span></span> <span data-ttu-id="631e5-113">O Barramento de Serviço limita a [quantidade de assinaturas em determinado tópico](service-bus-quotas.md) em 2.000.</span><span class="sxs-lookup"><span data-stu-id="631e5-113">Service Bus limits the [number of subscriptions on a given topic](service-bus-quotas.md) to 2,000.</span></span> <span data-ttu-id="631e5-114">Você pode acomodar outras assinaturas criando tópicos de segundo nível.</span><span class="sxs-lookup"><span data-stu-id="631e5-114">You can accommodate additional subscriptions by creating second-level topics.</span></span> <span data-ttu-id="631e5-115">Observe que, mesmo se o número de assinaturas que você tem não estiver limitado pelo Barramento de Serviço, a adição de um segundo nível de tópicos poderá melhorar a taxa de transferência geral do tópico.</span><span class="sxs-lookup"><span data-stu-id="631e5-115">Note that even if you are not bound by the Service Bus limitation on the number of subscriptions, adding a second level of topics can improve the overall throughput of your topic.</span></span>

![Cenário de encaminhamento automático][0]

<span data-ttu-id="631e5-117">Você também pode usar o encaminhamento automático para separar os remetentes dos destinatários.</span><span class="sxs-lookup"><span data-stu-id="631e5-117">You can also use auto-forwarding to decouple message senders from receivers.</span></span> <span data-ttu-id="631e5-118">Por exemplo, considere um sistema ERP composto por três módulos: processamento de pedidos, gerenciamento de estoque e gerenciamento de relacionamentos com o cliente.</span><span class="sxs-lookup"><span data-stu-id="631e5-118">For example, consider an ERP system that consists of three modules: order processing, inventory management, and customer relations management.</span></span> <span data-ttu-id="631e5-119">Cada um desses módulos gera mensagens que são enfileiradas em um tópico correspondente.</span><span class="sxs-lookup"><span data-stu-id="631e5-119">Each of these modules generates messages that are enqueued into a corresponding topic.</span></span> <span data-ttu-id="631e5-120">Brenda e Pedro são representantes de vendas interessados em todas as mensagens relacionadas aos seus clientes.</span><span class="sxs-lookup"><span data-stu-id="631e5-120">Alice and Bob are sales representatives that are interested in all messages that relate to their customers.</span></span> <span data-ttu-id="631e5-121">Para receber essas mensagens, Brenda e Pedro criaram, cada um, uma fila e assinatura pessoais em cada um dos tópicos ERP que encaminham automaticamente todas as mensagens para suas filas.</span><span class="sxs-lookup"><span data-stu-id="631e5-121">To receive those messages, Alice and Bob each create a personal queue and a subscription on each of the ERP topics that automatically forward all messages to their queue.</span></span>

![Cenário de encaminhamento automático][1]

<span data-ttu-id="631e5-123">Se Brenda entrar de férias, sua fila pessoal, em vez do tópico ERP, ficará cheia.</span><span class="sxs-lookup"><span data-stu-id="631e5-123">If Alice goes on vacation, her personal queue, rather than the ERP topic, fills up.</span></span> <span data-ttu-id="631e5-124">Nesse cenário, como um representante de vendas não recebeu nenhuma mensagem, nenhum dos tópicos ERP atingirá a cota.</span><span class="sxs-lookup"><span data-stu-id="631e5-124">In this scenario, because a sales representative has not received any messages, none of the ERP topics ever reach quota.</span></span>

## <a name="auto-forwarding-considerations"></a><span data-ttu-id="631e5-125">Considerações sobre o encaminhamento automático</span><span class="sxs-lookup"><span data-stu-id="631e5-125">Auto-forwarding considerations</span></span>

<span data-ttu-id="631e5-126">Se a entidade de destino tiver acumulado mensagens demais e exceder a cota, ou se a entidade de destino estiver desabilitada, a entidade de origem adicionará as mensagens à sua [fila de mensagens mortas](service-bus-dead-letter-queues.md) até que haja espaço no destino (ou a entidade seja habilitada novamente).</span><span class="sxs-lookup"><span data-stu-id="631e5-126">If the destination entity accumulates too many messages and exceeds the quota, or the destination entity is disabled, the source entity adds the messages to its [dead-letter queue](service-bus-dead-letter-queues.md) until there is space in the destination (or the entity is re-enabled).</span></span> <span data-ttu-id="631e5-127">Essas mensagens continuarão ativas na fila de mensagens mortas, portanto, você deve receber e processá-las explicitamente a partir da fila de mensagens mortas.</span><span class="sxs-lookup"><span data-stu-id="631e5-127">Those messages will continue to live in the dead-letter queue, so you must explicitly receive and process them from the dead-letter queue.</span></span>

<span data-ttu-id="631e5-128">Ao encadear tópicos individuais a fim de obter um tópico composto com diversas assinaturas, recomendamos que você tenha uma quantidade moderada de assinaturas no tópico de primeiro nível e diversas assinaturas nos tópicos de segundo nível.</span><span class="sxs-lookup"><span data-stu-id="631e5-128">When chaining together individual topics to obtain a composite topic with many subscriptions, it is recommended that you have a moderate number of subscriptions on the first-level topic and many subscriptions on the second-level topics.</span></span> <span data-ttu-id="631e5-129">Por exemplo, um tópico de primeiro nível com 20 assinaturas, cada uma delas encadeada com um tópico de segundo nível com 200 assinaturas, permite uma taxa de transferência superior do que um tópico de primeiro nível com 200 assinaturas, cada uma delas encadeada com um tópico de segundo nível com 20 assinaturas.</span><span class="sxs-lookup"><span data-stu-id="631e5-129">For example, a first-level topic with 20 subscriptions, each of them chained to a second-level topic with 200 subscriptions, allows for higher throughput than a first-level topic with 200 subscriptions, each chained to a second-level topic with 20 subscriptions.</span></span>

<span data-ttu-id="631e5-130">O Barramento de Serviço cobra uma operação por cada mensagem encaminhada.</span><span class="sxs-lookup"><span data-stu-id="631e5-130">Service Bus bills one operation for each forwarded message.</span></span> <span data-ttu-id="631e5-131">Por exemplo, o envio de uma mensagem a um tópico com 20 assinaturas, cada uma delas configurada para encaminhar automaticamente mensagens para outra fila ou outro tópico, receberá uma cobrança por 21 operações, caso todas as assinaturas de primeiro nível recebam uma cópia da mensagem.</span><span class="sxs-lookup"><span data-stu-id="631e5-131">For example, sending a message to a topic with 20 subscriptions, each of them configured to auto-forward messages to another queue or topic, is billed as 21 operations if all first-level subscriptions receive a copy of the message.</span></span>

<span data-ttu-id="631e5-132">Para criar uma assinatura encadeada a outra fila ou outro tópico, o criador da assinatura deverá ter permissões para **Gerenciar** tanto na entidade de origem quanto na entidade de destino.</span><span class="sxs-lookup"><span data-stu-id="631e5-132">To create a subscription that is chained to another queue or topic, the creator of the subscription must have **Manage** permissions on both the source and the destination entity.</span></span> <span data-ttu-id="631e5-133">O envio de mensagens para o tópico de origem exige apenas permissões para **Enviar** no tópico de origem.</span><span class="sxs-lookup"><span data-stu-id="631e5-133">Sending messages to the source topic only requires **Send** permissions on the source topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="631e5-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="631e5-134">Next steps</span></span>

<span data-ttu-id="631e5-135">Para obter informações detalhadas sobre o encaminhamento automático, consulte os seguintes tópicos de referência:</span><span class="sxs-lookup"><span data-stu-id="631e5-135">For detailed information about auto-forwarding, see the following reference topics:</span></span>

* <span data-ttu-id="631e5-136">[ForwardTo][QueueDescription.ForwardTo]</span><span class="sxs-lookup"><span data-stu-id="631e5-136">[ForwardTo][QueueDescription.ForwardTo]</span></span>
* <span data-ttu-id="631e5-137">[QueueDescription][QueueDescription]</span><span class="sxs-lookup"><span data-stu-id="631e5-137">[QueueDescription][QueueDescription]</span></span>
* <span data-ttu-id="631e5-138">[SubscriptionDescription][SubscriptionDescription]</span><span class="sxs-lookup"><span data-stu-id="631e5-138">[SubscriptionDescription][SubscriptionDescription]</span></span>

<span data-ttu-id="631e5-139">Para saber mais sobre as melhorias de desempenho do Barramento de Serviço, consulte</span><span class="sxs-lookup"><span data-stu-id="631e5-139">To learn more about Service Bus performance improvements, see</span></span> 

* [<span data-ttu-id="631e5-140">Práticas recomendadas para melhorias de desempenho usando o Sistema de Mensagens do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="631e5-140">Best Practices for performance improvements using Service Bus Messaging</span></span>](service-bus-performance-improvements.md)
* <span data-ttu-id="631e5-141">[Entidades de mensagens particionadas][Partitioned messaging entities].</span><span class="sxs-lookup"><span data-stu-id="631e5-141">[Partitioned messaging entities][Partitioned messaging entities].</span></span>

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
