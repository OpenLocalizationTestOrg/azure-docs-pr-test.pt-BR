---
title: "entidades de mensagens de barramento de serviço do Azure de encaminhamento aaaAuto | Microsoft Docs"
description: "Como toochain um barramento de serviço fila ou assinatura tooanother fila ou um tópico."
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
ms.openlocfilehash: af18273e4e2f81c5363eb830c7decf313afd8307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a><span data-ttu-id="c4b66-103">Encadeando entidades do Barramento de Serviço com o encaminhamento automático</span><span class="sxs-lookup"><span data-stu-id="c4b66-103">Chaining Service Bus entities with auto-forwarding</span></span>

<span data-ttu-id="c4b66-104">Olá barramento de serviço *encaminhamento automático* recurso permite que você toochain uma fila ou assinatura tooanother fila ou um tópico que faz parte da saudação mesmo namespace.</span><span class="sxs-lookup"><span data-stu-id="c4b66-104">hello Service Bus *auto-forwarding* feature enables you toochain a queue or subscription tooanother queue or topic that is part of hello same namespace.</span></span> <span data-ttu-id="c4b66-105">Quando o encaminhamento automático está habilitado, barramento de serviço automaticamente remove as mensagens que são colocadas na primeira fila de saudação ou assinatura (origem) e as coloca na fila segundo hello ou tópico (destino).</span><span class="sxs-lookup"><span data-stu-id="c4b66-105">When auto-forwarding is enabled, Service Bus automatically removes messages that are placed in hello first queue or subscription (source) and puts them in hello second queue or topic (destination).</span></span> <span data-ttu-id="c4b66-106">Observe que é possível toosend uma entidade de destino toohello mensagem diretamente.</span><span class="sxs-lookup"><span data-stu-id="c4b66-106">Note that it is still possible toosend a message toohello destination entity directly.</span></span> <span data-ttu-id="c4b66-107">Além disso, não é possível toochain uma subfila, tal como uma fila de mensagens mortas, tooanother fila ou tópico.</span><span class="sxs-lookup"><span data-stu-id="c4b66-107">Also, it is not possible toochain a subqueue, such as a deadletter queue, tooanother queue or topic.</span></span>

## <a name="using-auto-forwarding"></a><span data-ttu-id="c4b66-108">Usando o encaminhamento automático</span><span class="sxs-lookup"><span data-stu-id="c4b66-108">Using auto-forwarding</span></span>
<span data-ttu-id="c4b66-109">Você pode habilitar o encaminhamento automático definindo Olá [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] ou [SubscriptionDescription.ForwardTo] [ SubscriptionDescription.ForwardTo] propriedades em Olá [QueueDescription] [ QueueDescription] ou [SubscriptionDescription] [ SubscriptionDescription] objetos origem hello, como Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c4b66-109">You can enable auto-forwarding by setting hello [QueueDescription.ForwardTo][QueueDescription.ForwardTo] or [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] properties on hello [QueueDescription][QueueDescription] or [SubscriptionDescription][SubscriptionDescription] objects for hello source, as in hello following example.</span></span>

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

<span data-ttu-id="c4b66-110">entidade de destino Olá deve existir no tempo de saudação Olá fonte entidade é criada.</span><span class="sxs-lookup"><span data-stu-id="c4b66-110">hello destination entity must exist at hello time hello source entity is created.</span></span> <span data-ttu-id="c4b66-111">Se a entidade de destino Olá não existir, o barramento de serviço retorna uma exceção quando toocreate frequentes Olá entidade de origem.</span><span class="sxs-lookup"><span data-stu-id="c4b66-111">If hello destination entity does not exist, Service Bus returns an exception when asked toocreate hello source entity.</span></span>

<span data-ttu-id="c4b66-112">Você pode usar o encaminhamento automático tooscale-out de um tópico individual.</span><span class="sxs-lookup"><span data-stu-id="c4b66-112">You can use auto-forwarding tooscale out an individual topic.</span></span> <span data-ttu-id="c4b66-113">Saudação de limites de barramento de serviço [número de assinaturas em um determinado tópico](service-bus-quotas.md) too2, 000.</span><span class="sxs-lookup"><span data-stu-id="c4b66-113">Service Bus limits hello [number of subscriptions on a given topic](service-bus-quotas.md) too2,000.</span></span> <span data-ttu-id="c4b66-114">Você pode acomodar outras assinaturas criando tópicos de segundo nível.</span><span class="sxs-lookup"><span data-stu-id="c4b66-114">You can accommodate additional subscriptions by creating second-level topics.</span></span> <span data-ttu-id="c4b66-115">Observe que mesmo se você não estiver vinculado Olá limitação no número de saudação de assinaturas, adicionar tópicos de segundo nível pode melhorar o barramento de serviço Olá produtividade geral do seu tópico.</span><span class="sxs-lookup"><span data-stu-id="c4b66-115">Note that even if you are not bound by hello Service Bus limitation on hello number of subscriptions, adding a second level of topics can improve hello overall throughput of your topic.</span></span>

![Cenário de encaminhamento automático][0]

<span data-ttu-id="c4b66-117">Você também pode usar o encaminhamento automático toodecouple remetentes dos destinatários.</span><span class="sxs-lookup"><span data-stu-id="c4b66-117">You can also use auto-forwarding toodecouple message senders from receivers.</span></span> <span data-ttu-id="c4b66-118">Por exemplo, considere um sistema ERP composto por três módulos: processamento de pedidos, gerenciamento de estoque e gerenciamento de relacionamentos com o cliente.</span><span class="sxs-lookup"><span data-stu-id="c4b66-118">For example, consider an ERP system that consists of three modules: order processing, inventory management, and customer relations management.</span></span> <span data-ttu-id="c4b66-119">Cada um desses módulos gera mensagens que são enfileiradas em um tópico correspondente.</span><span class="sxs-lookup"><span data-stu-id="c4b66-119">Each of these modules generates messages that are enqueued into a corresponding topic.</span></span> <span data-ttu-id="c4b66-120">Alice e Bob é representantes de vendas interessados em todas as mensagens relacionadas tootheir clientes.</span><span class="sxs-lookup"><span data-stu-id="c4b66-120">Alice and Bob are sales representatives that are interested in all messages that relate tootheir customers.</span></span> <span data-ttu-id="c4b66-121">tooreceive as mensagens, Alice e Bob cria uma fila pessoal e uma assinatura em cada um dos tópicos ERP Olá que encaminham automaticamente todas as filas de tootheir de mensagens.</span><span class="sxs-lookup"><span data-stu-id="c4b66-121">tooreceive those messages, Alice and Bob each create a personal queue and a subscription on each of hello ERP topics that automatically forward all messages tootheir queue.</span></span>

![Cenário de encaminhamento automático][1]

<span data-ttu-id="c4b66-123">Se a Eliane tirar férias, sua fila pessoal, em vez de tópico ERP hello, preenchido.</span><span class="sxs-lookup"><span data-stu-id="c4b66-123">If Alice goes on vacation, her personal queue, rather than hello ERP topic, fills up.</span></span> <span data-ttu-id="c4b66-124">Nesse cenário, porque um representante de vendas não recebeu as mensagens, nenhum dos tópicos ERP Olá atingiu a cota.</span><span class="sxs-lookup"><span data-stu-id="c4b66-124">In this scenario, because a sales representative has not received any messages, none of hello ERP topics ever reach quota.</span></span>

## <a name="auto-forwarding-considerations"></a><span data-ttu-id="c4b66-125">Considerações sobre o encaminhamento automático</span><span class="sxs-lookup"><span data-stu-id="c4b66-125">Auto-forwarding considerations</span></span>

<span data-ttu-id="c4b66-126">Se entidade de destino Olá acumula muitas mensagens e excede a cota de hello, ou entidade de destino hello está desabilitada, entidade de origem Olá adiciona mensagens de saudação tooits [fila de mensagens mortas](service-bus-dead-letter-queues.md) até que haja espaço no destino Olá (ou entidade de saudação é reativada).</span><span class="sxs-lookup"><span data-stu-id="c4b66-126">If hello destination entity accumulates too many messages and exceeds hello quota, or hello destination entity is disabled, hello source entity adds hello messages tooits [dead-letter queue](service-bus-dead-letter-queues.md) until there is space in hello destination (or hello entity is re-enabled).</span></span> <span data-ttu-id="c4b66-127">Essas mensagens continuará toolive na fila de mensagens mortas hello, para que você deve receber e processá-los da fila de mensagens mortas Olá explicitamente.</span><span class="sxs-lookup"><span data-stu-id="c4b66-127">Those messages will continue toolive in hello dead-letter queue, so you must explicitly receive and process them from hello dead-letter queue.</span></span>

<span data-ttu-id="c4b66-128">Ao encadear tópicos individuais tooobtain um tópico composto com diversas assinaturas, é recomendável que você tenha um número moderado de assinaturas no tópico de primeiro nível hello e diversas assinaturas nos tópicos de segundo nível hello.</span><span class="sxs-lookup"><span data-stu-id="c4b66-128">When chaining together individual topics tooobtain a composite topic with many subscriptions, it is recommended that you have a moderate number of subscriptions on hello first-level topic and many subscriptions on hello second-level topics.</span></span> <span data-ttu-id="c4b66-129">Por exemplo, um tópico de primeiro nível com 20 assinaturas, cada uma delas encadeada tooa tópico de segundo nível com 200 assinaturas, permite mais rendimento do que um tópico de primeiro nível com 200 assinaturas, cada uma encadeada tooa tópico de segundo nível com 20 assinaturas .</span><span class="sxs-lookup"><span data-stu-id="c4b66-129">For example, a first-level topic with 20 subscriptions, each of them chained tooa second-level topic with 200 subscriptions, allows for higher throughput than a first-level topic with 200 subscriptions, each chained tooa second-level topic with 20 subscriptions.</span></span>

<span data-ttu-id="c4b66-130">O Barramento de Serviço cobra uma operação por cada mensagem encaminhada.</span><span class="sxs-lookup"><span data-stu-id="c4b66-130">Service Bus bills one operation for each forwarded message.</span></span> <span data-ttu-id="c4b66-131">Por exemplo, enviando um tópico de mensagem de tooa com 20 assinaturas, cada um deles configurado tooauto encaminhar mensagens tooanother fila ou tópico, é cobrada como 21 operações se todas as assinaturas de primeiro nível recebem uma cópia da mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4b66-131">For example, sending a message tooa topic with 20 subscriptions, each of them configured tooauto-forward messages tooanother queue or topic, is billed as 21 operations if all first-level subscriptions receive a copy of hello message.</span></span>

<span data-ttu-id="c4b66-132">toocreate uma assinatura encadeada tooanother fila ou tópico, o criador de saudação de assinatura Olá deve ter **gerenciar** permissões na origem hello e entidade de destino hello.</span><span class="sxs-lookup"><span data-stu-id="c4b66-132">toocreate a subscription that is chained tooanother queue or topic, hello creator of hello subscription must have **Manage** permissions on both hello source and hello destination entity.</span></span> <span data-ttu-id="c4b66-133">Enviar somente requer um tópico de origem toohello mensagens **enviar** permissões no tópico de origem hello.</span><span class="sxs-lookup"><span data-stu-id="c4b66-133">Sending messages toohello source topic only requires **Send** permissions on hello source topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4b66-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c4b66-134">Next steps</span></span>

<span data-ttu-id="c4b66-135">Para obter informações detalhadas sobre o encaminhamento automático, consulte Olá tópicos de referência a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4b66-135">For detailed information about auto-forwarding, see hello following reference topics:</span></span>

* <span data-ttu-id="c4b66-136">[ForwardTo][QueueDescription.ForwardTo]</span><span class="sxs-lookup"><span data-stu-id="c4b66-136">[ForwardTo][QueueDescription.ForwardTo]</span></span>
* <span data-ttu-id="c4b66-137">[QueueDescription][QueueDescription]</span><span class="sxs-lookup"><span data-stu-id="c4b66-137">[QueueDescription][QueueDescription]</span></span>
* <span data-ttu-id="c4b66-138">[SubscriptionDescription][SubscriptionDescription]</span><span class="sxs-lookup"><span data-stu-id="c4b66-138">[SubscriptionDescription][SubscriptionDescription]</span></span>

<span data-ttu-id="c4b66-139">toolearn mais informações sobre aprimoramentos de desempenho do barramento de serviço, consulte</span><span class="sxs-lookup"><span data-stu-id="c4b66-139">toolearn more about Service Bus performance improvements, see</span></span> 

* [<span data-ttu-id="c4b66-140">Práticas recomendadas para melhorias de desempenho usando o Sistema de Mensagens do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="c4b66-140">Best Practices for performance improvements using Service Bus Messaging</span></span>](service-bus-performance-improvements.md)
* <span data-ttu-id="c4b66-141">[Entidades de mensagens particionadas][Partitioned messaging entities].</span><span class="sxs-lookup"><span data-stu-id="c4b66-141">[Partitioned messaging entities][Partitioned messaging entities].</span></span>

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
