---
title: "aaaAvailability e a consistência nos Hubs de eventos do Azure | Microsoft Docs"
description: "Como tooprovide Olá máximo de disponibilidade e a consistência com Hubs de eventos do Azure usando partições."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 8f3637a1-bbd7-481e-be49-b3adf9510ba1
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a8ededaae1589830da21cb8910ca694d2d628bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a><span data-ttu-id="39593-103">Disponibilidade e consistência nos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="39593-103">Availability and consistency in Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="39593-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="39593-104">Overview</span></span>
<span data-ttu-id="39593-105">Hubs de eventos do Azure usa um [particionamento modelo](event-hubs-features.md#partitions) tooimprove paralelização dentro de um hub de evento único e disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="39593-105">Azure Event Hubs uses a [partitioning model](event-hubs-features.md#partitions) tooimprove availability and parallelization within a single event hub.</span></span> <span data-ttu-id="39593-106">Por exemplo, se um hub de eventos tem quatro partições, e um essas partições é movido de um servidor tooanother em uma operação de balanceamento de carga, você ainda pode enviar e receber de três outras partições.</span><span class="sxs-lookup"><span data-stu-id="39593-106">For example, if an event hub has four partitions, and one of those partitions is moved from one server tooanother in a load balancing operation, you can still send and receive from three other partitions.</span></span> <span data-ttu-id="39593-107">Além disso, ter mais partições permite que você toohave leitores simultâneos mais processar seus dados, melhorando a taxa de transferência agregada.</span><span class="sxs-lookup"><span data-stu-id="39593-107">Additionally, having more partitions enables you toohave more concurrent readers processing your data, improving your aggregate throughput.</span></span> <span data-ttu-id="39593-108">Noções básicas sobre as implicações de saudação de particionamento e a ordenação em um sistema distribuído é um aspecto crítico de design da solução.</span><span class="sxs-lookup"><span data-stu-id="39593-108">Understanding hello implications of partitioning and ordering in a distributed system is a critical aspect of solution design.</span></span>

<span data-ttu-id="39593-109">toohelp explicam a compensação de saudação entre pedidos e disponibilidade, consulte Olá [Teorema de CAP](https://en.wikipedia.org/wiki/CAP_theorem), também conhecido como Teorema do Brewer.</span><span class="sxs-lookup"><span data-stu-id="39593-109">toohelp explain hello trade-off between ordering and availability, see hello [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem), also known as Brewer's theorem.</span></span> <span data-ttu-id="39593-110">Este Teorema discute escolha Olá entre consistência, disponibilidade e tolerância a partição.</span><span class="sxs-lookup"><span data-stu-id="39593-110">This theorem discusses hello choice between consistency, availability, and partition tolerance.</span></span>

<span data-ttu-id="39593-111">O teorema de Brewer define a consistência e a disponibilidade como a seguir:</span><span class="sxs-lookup"><span data-stu-id="39593-111">Brewer's theorem defines consistency and availability as follows:</span></span>
* <span data-ttu-id="39593-112">Tolerância de partição: Olá a capacidade de um toocontinue do sistema de processamento de dados processamento de dados mesmo se ocorrer uma falha de partição.</span><span class="sxs-lookup"><span data-stu-id="39593-112">Partition tolerance: hello ability of a data processing system toocontinue processing data even if a partition failure occurs.</span></span>
* <span data-ttu-id="39593-113">Disponibilidade: um nó sem falha retorna uma resposta razoável dentro de um período razoável (sem erros nem tempos limites).</span><span class="sxs-lookup"><span data-stu-id="39593-113">Availability: a non-failing node returns a reasonable response within a reasonable amount of time (with no errors or timeouts).</span></span>
* <span data-ttu-id="39593-114">Consistência: uma leitura é garantida tooreturn hello mais recente na gravação para um determinado cliente.</span><span class="sxs-lookup"><span data-stu-id="39593-114">Consistency: a read is guaranteed tooreturn hello most recent write for a given client.</span></span>

## <a name="partition-tolerance"></a><span data-ttu-id="39593-115">Tolerância a partição</span><span class="sxs-lookup"><span data-stu-id="39593-115">Partition tolerance</span></span>
<span data-ttu-id="39593-116">Os Hubs de Eventos são criados sobre um modelo de dados particionado.</span><span class="sxs-lookup"><span data-stu-id="39593-116">Event Hubs is built on top of a partitioned data model.</span></span> <span data-ttu-id="39593-117">Você pode configurar o número de saudação de partições em seu hub de eventos durante a instalação, mas você não pode alterar esse valor posteriormente.</span><span class="sxs-lookup"><span data-stu-id="39593-117">You can configure hello number of partitions in your event hub during setup, but you cannot change this value later.</span></span> <span data-ttu-id="39593-118">Como você deve usar partições com Hubs de eventos, você tem toomake uma decisão sobre a disponibilidade e a consistência de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="39593-118">Since you must use partitions with Event Hubs, you have toomake a decision about availability and consistency for your application.</span></span>

## <a name="availability"></a><span data-ttu-id="39593-119">Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="39593-119">Availability</span></span>
<span data-ttu-id="39593-120">Olá tooget de maneira mais simples de Introdução com Hubs de eventos é o comportamento do toouse saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="39593-120">hello simplest way tooget started with Event Hubs is toouse hello default behavior.</span></span> <span data-ttu-id="39593-121">Se você criar um novo `EventHubClient` de objeto e usar Olá `Send` método, os eventos são distribuídos automaticamente entre partições em seu hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="39593-121">If you create a new `EventHubClient` object and use hello `Send` method, your events are automatically distributed between partitions in your event hub.</span></span> <span data-ttu-id="39593-122">Esse comportamento permite Olá maior quantidade de tempo.</span><span class="sxs-lookup"><span data-stu-id="39593-122">This behavior allows for hello greatest amount of up time.</span></span>

<span data-ttu-id="39593-123">Para casos de uso que exigem o máximo de saudação o tempo, esse modelo é preferencial.</span><span class="sxs-lookup"><span data-stu-id="39593-123">For use cases that require hello maximum up time, this model is preferred.</span></span>

## <a name="consistency"></a><span data-ttu-id="39593-124">Consistência</span><span class="sxs-lookup"><span data-stu-id="39593-124">Consistency</span></span>
<span data-ttu-id="39593-125">Em alguns cenários, a saudação de ordenação de eventos pode ser importante.</span><span class="sxs-lookup"><span data-stu-id="39593-125">In some scenarios, hello ordering of events can be important.</span></span> <span data-ttu-id="39593-126">Por exemplo, talvez você queira tooprocess seu sistema back-end um comando de atualização antes de um comando de exclusão.</span><span class="sxs-lookup"><span data-stu-id="39593-126">For example, you may want your back-end system tooprocess an update command before a delete command.</span></span> <span data-ttu-id="39593-127">Neste exemplo, defina a chave de partição Olá em um evento ou use um `PartitionSender` tooonly objeto enviar eventos tooa certa partição.</span><span class="sxs-lookup"><span data-stu-id="39593-127">In this instance, you can either set hello partition key on an event, or use a `PartitionSender` object tooonly send events tooa certain partition.</span></span> <span data-ttu-id="39593-128">Isso garante que, quando esses eventos são lidos da partição hello, que são lidas em ordem.</span><span class="sxs-lookup"><span data-stu-id="39593-128">Doing so ensures that when these events are read from hello partition, they are read in order.</span></span>

<span data-ttu-id="39593-129">Com essa configuração, tenha em mente que, se Olá determinada partição toowhich que estiver enviando não estiver disponível, você receberá uma resposta de erro.</span><span class="sxs-lookup"><span data-stu-id="39593-129">With this configuration, keep in mind that if hello particular partition toowhich you are sending is unavailable, you will receive an error response.</span></span> <span data-ttu-id="39593-130">Como um ponto de comparação, se você não tiver uma partição única tooa de afinidade, hello serviço de Hubs de eventos envia a evento toohello próxima partição disponível.</span><span class="sxs-lookup"><span data-stu-id="39593-130">As a point of comparison, if you do not have an affinity tooa single partition, hello Event Hubs service sends your event toohello next available partition.</span></span>

<span data-ttu-id="39593-131">Um tooensure solução possível ordenação, maximizando o tempo, também seria tooaggregate eventos como parte de seu aplicativo de processamento de eventos.</span><span class="sxs-lookup"><span data-stu-id="39593-131">One possible solution tooensure ordering, while also maximizing up time, would be tooaggregate events as part of your event processing application.</span></span> <span data-ttu-id="39593-132">Olá tooaccomplish de maneira mais fácil isso é toostamp seu evento com uma propriedade de número de sequência personalizado.</span><span class="sxs-lookup"><span data-stu-id="39593-132">hello easiest way tooaccomplish this is toostamp your event with a custom sequence number property.</span></span> <span data-ttu-id="39593-133">saudação de código a seguir mostra um exemplo:</span><span class="sxs-lookup"><span data-stu-id="39593-133">hello following code shows an example:</span></span>

```csharp
// Get hello latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

<span data-ttu-id="39593-134">Este exemplo envia sua tooone de evento de partições disponíveis Olá em seu hub de eventos e define o número de sequência correspondente de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="39593-134">This example sends your event tooone of hello available partitions in your event hub, and sets hello corresponding sequence number from your application.</span></span> <span data-ttu-id="39593-135">Essa solução requer toobe estado mantido pelo seu aplicativo de processamento, mas oferece os remetentes um ponto de extremidade que é mais provável toobe disponível.</span><span class="sxs-lookup"><span data-stu-id="39593-135">This solution requires state toobe kept by your processing application, but gives your senders an endpoint that is more likely toobe available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39593-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="39593-136">Next steps</span></span>
<span data-ttu-id="39593-137">Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="39593-137">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="39593-138">Visão geral do serviço dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="39593-138">Event Hubs service overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="39593-139">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="39593-139">Create an event hub</span></span>](event-hubs-create.md)
