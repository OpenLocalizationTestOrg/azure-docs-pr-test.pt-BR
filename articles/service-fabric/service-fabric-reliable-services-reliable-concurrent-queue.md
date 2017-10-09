---
title: aaaReliableConcurrentQueue no Azure Service Fabric
description: "ReliableConcurrentQueue é uma fila de alta taxa de transferência que permite enfileirar e remover da fila de modo paralelo."
services: service-fabric
documentationcenter: .net
author: sangarg
manager: timlt
editor: raja,tyadam,masnider,vturecek
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: sangarg
ms.openlocfilehash: 78a9905996b9ab265c1288d2b49753638d7bc445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliableconcurrentqueue-in-azure-service-fabric"></a><span data-ttu-id="95d8d-103">Introdução tooReliableConcurrentQueue no Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="95d8d-103">Introduction tooReliableConcurrentQueue in Azure Service Fabric</span></span>
<span data-ttu-id="95d8d-104">Fila Simultânea Confiável é uma fila assíncrona, transacional e replicada quais apresenta alta simultaneidade para operações de enfileirar e remover da fila.</span><span class="sxs-lookup"><span data-stu-id="95d8d-104">Reliable Concurrent Queue is an asynchronous, transactional, and replicated queue which features high concurrency for enqueue and dequeue operations.</span></span> <span data-ttu-id="95d8d-105">É projetado toodeliver alta taxa de transferência e baixa latência ordenando relaxando Olá estrito FIFO fornecidos pelo [fila confiável](https://msdn.microsoft.com/library/azure/dn971527.aspx) e fornece uma ordenação de melhor esforço.</span><span class="sxs-lookup"><span data-stu-id="95d8d-105">It is designed toodeliver high throughput and low latency by relaxing hello strict FIFO ordering provided by [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) and instead provides a best-effort ordering.</span></span>

## <a name="apis"></a><span data-ttu-id="95d8d-106">APIs</span><span class="sxs-lookup"><span data-stu-id="95d8d-106">APIs</span></span>

|<span data-ttu-id="95d8d-107">Fila Simultânea</span><span class="sxs-lookup"><span data-stu-id="95d8d-107">Concurrent Queue</span></span>                |<span data-ttu-id="95d8d-108">Fila Simultânea Confiável</span><span class="sxs-lookup"><span data-stu-id="95d8d-108">Reliable Concurrent Queue</span></span>                                         |
|--------------------------------|------------------------------------------------------------------|
| <span data-ttu-id="95d8d-109">void Enqueue(T item)</span><span class="sxs-lookup"><span data-stu-id="95d8d-109">void Enqueue(T item)</span></span>           | <span data-ttu-id="95d8d-110">Task EnqueueAsync(ITransaction tx, T item)</span><span class="sxs-lookup"><span data-stu-id="95d8d-110">Task EnqueueAsync(ITransaction tx, T item)</span></span>                       |
| <span data-ttu-id="95d8d-111">bool TryDequeue(out T result)</span><span class="sxs-lookup"><span data-stu-id="95d8d-111">bool TryDequeue(out T result)</span></span>  | <span data-ttu-id="95d8d-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span><span class="sxs-lookup"><span data-stu-id="95d8d-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span></span>  |
| <span data-ttu-id="95d8d-113">int Count()</span><span class="sxs-lookup"><span data-stu-id="95d8d-113">int Count()</span></span>                    | <span data-ttu-id="95d8d-114">long Count()</span><span class="sxs-lookup"><span data-stu-id="95d8d-114">long Count()</span></span>                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a><span data-ttu-id="95d8d-115">Comparação com [Fila Confiável](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span><span class="sxs-lookup"><span data-stu-id="95d8d-115">Comparison with [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span></span>

<span data-ttu-id="95d8d-116">Confiável simultâneos na fila é oferecido como uma alternativa muito[fila confiável](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span><span class="sxs-lookup"><span data-stu-id="95d8d-116">Reliable Concurrent Queue is offered as an alternative too[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span></span> <span data-ttu-id="95d8d-117">Ela deve ser usada em casos em que ordenação PEPS estrita não seja necessária, como garantir que PEPS exija uma compensação com simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="95d8d-117">It should be used in cases where strict FIFO ordering is not required, as guaranteeing FIFO requires a tradeoff with concurrency.</span></span>  <span data-ttu-id="95d8d-118">[Fila confiável](https://msdn.microsoft.com/library/azure/dn971527.aspx) usa bloqueios tooenforce FIFO pedidos, no máximo uma transação permitido tooenqueue e no máximo uma transação permitido toodequeue por vez.</span><span class="sxs-lookup"><span data-stu-id="95d8d-118">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) uses locks tooenforce FIFO ordering, with at most one transaction allowed tooenqueue and at most one transaction allowed toodequeue at a time.</span></span> <span data-ttu-id="95d8d-119">Em comparação, simultâneos na fila confiável alivia Olá ordenação de restrição e permite que qualquer número toointerleave de transações simultâneas seu enfileirar e operações de remoção da fila.</span><span class="sxs-lookup"><span data-stu-id="95d8d-119">In comparison, Reliable Concurrent Queue relaxes hello ordering constraint and allows any number concurrent transactions toointerleave their enqueue and dequeue operations.</span></span> <span data-ttu-id="95d8d-120">Ordenação de melhor esforço for fornecido, porém Olá a ordenação relativa de dois valores em uma fila simultâneas confiável pode nunca ser garantida.</span><span class="sxs-lookup"><span data-stu-id="95d8d-120">Best-effort ordering is provided, however hello relative ordering of two values in a Reliable Concurrent Queue can never be guaranteed.</span></span>

<span data-ttu-id="95d8d-121">Fila Simultâneas Confiáveis fornecem maior taxa de transferência e menor latência que [Fila Confiável](https://msdn.microsoft.com/library/azure/dn971527.aspx) sempre que há várias transações simultâneas executando ações de enfileirar e/ou remover da fila.</span><span class="sxs-lookup"><span data-stu-id="95d8d-121">Reliable Concurrent Queue provides higher throughput and lower latency than [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) whenever there are multiple concurrent transactions performing enqueues and/or dequeues.</span></span>

<span data-ttu-id="95d8d-122">Um exemplo de caso de uso para Olá ReliableConcurrentQueue é Olá [fila de mensagens](https://en.wikipedia.org/wiki/Message_queue) cenário.</span><span class="sxs-lookup"><span data-stu-id="95d8d-122">A sample use case for hello ReliableConcurrentQueue is hello [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario.</span></span> <span data-ttu-id="95d8d-123">Nesse cenário, produtores de mensagens de uma ou mais criar e adicionar itens toohello fila e um ou mais consumidores de mensagens receber mensagens da fila de saudação e processá-las.</span><span class="sxs-lookup"><span data-stu-id="95d8d-123">In this scenario, one or more message producers create and add items toohello queue, and one or more message consumers pull messages from hello queue and process them.</span></span> <span data-ttu-id="95d8d-124">Vários produtores e consumidores podem trabalhar de forma independente, usando transações simultâneas na fila de saudação do tooprocess de ordem.</span><span class="sxs-lookup"><span data-stu-id="95d8d-124">Multiple producers and consumers can work independently, using concurrent transactions in order tooprocess hello queue.</span></span>

## <a name="usage-guidelines"></a><span data-ttu-id="95d8d-125">Diretrizes de uso</span><span class="sxs-lookup"><span data-stu-id="95d8d-125">Usage Guidelines</span></span>
* <span data-ttu-id="95d8d-126">fila de saudação espera que itens de saudação na fila de saudação têm um período de retenção de baixa.</span><span class="sxs-lookup"><span data-stu-id="95d8d-126">hello queue expects that hello items in hello queue have a low retention period.</span></span> <span data-ttu-id="95d8d-127">Ou seja, itens de saudação não permanece na fila de saudação por um longo tempo.</span><span class="sxs-lookup"><span data-stu-id="95d8d-127">That is, hello items would not stay in hello queue for a long time.</span></span>
* <span data-ttu-id="95d8d-128">fila Olá não garante a ordenação de FIFO estrito.</span><span class="sxs-lookup"><span data-stu-id="95d8d-128">hello queue does not guarantee strict FIFO ordering.</span></span>
* <span data-ttu-id="95d8d-129">fila de saudação não ler seus próprios gravações.</span><span class="sxs-lookup"><span data-stu-id="95d8d-129">hello queue does not read its own writes.</span></span> <span data-ttu-id="95d8d-130">Se um item é colocado dentro de uma transação, não será visível tooa dequeuer em hello mesma transação.</span><span class="sxs-lookup"><span data-stu-id="95d8d-130">If an item is enqueued within a transaction, it will not be visible tooa dequeuer within hello same transaction.</span></span>
* <span data-ttu-id="95d8d-131">As operações de remover da fila não são isoladas umas das outras.</span><span class="sxs-lookup"><span data-stu-id="95d8d-131">Dequeues are not isolated from each other.</span></span> <span data-ttu-id="95d8d-132">Se o item *um* é removida da fila na transação *txnA*, embora *txnA* item não for confirmada, *um* não será visível tooa simultâneos transação *txnB*.</span><span class="sxs-lookup"><span data-stu-id="95d8d-132">If item *A* is dequeued in transaction *txnA*, even though *txnA* is not committed, item *A* would not be visible tooa concurrent transaction *txnB*.</span></span>  <span data-ttu-id="95d8d-133">Se *txnA* anula, *um* ficará visível muito*txnB* imediatamente.</span><span class="sxs-lookup"><span data-stu-id="95d8d-133">If *txnA* aborts, *A* will become visible too*txnB* immediately.</span></span>
* <span data-ttu-id="95d8d-134">*TryPeekAsync* comportamento pode ser implementado usando um *TryDequeueAsync* e, em seguida, anulando a transação de saudação.</span><span class="sxs-lookup"><span data-stu-id="95d8d-134">*TryPeekAsync* behavior can be implemented by using a *TryDequeueAsync* and then aborting hello transaction.</span></span> <span data-ttu-id="95d8d-135">Um exemplo disso pode ser encontrado na seção de padrões de programação de saudação.</span><span class="sxs-lookup"><span data-stu-id="95d8d-135">An example of this can be found in hello Programming Patterns section.</span></span>
* <span data-ttu-id="95d8d-136">A contagem é não transacional.</span><span class="sxs-lookup"><span data-stu-id="95d8d-136">Count is non-transactional.</span></span> <span data-ttu-id="95d8d-137">Pode ser usado tooget uma ideia do número de saudação de elementos na fila Olá, mas representa um point-in-time e não pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="95d8d-137">It can be used tooget an idea of hello number of elements in hello queue, but represents a point-in-time and cannot be relied upon.</span></span>
* <span data-ttu-id="95d8d-138">Caro processamento Olá removidas da fila de itens não devem ser executadas enquanto Olá transação está ativa, transações de longa execução tooavoid que podem ter um impacto de desempenho no sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="95d8d-138">Expensive processing on hello dequeued items should not be performed while hello transaction is active, tooavoid long-running transactions which may have a performance impact on hello system.</span></span>

## <a name="code-snippets"></a><span data-ttu-id="95d8d-139">Trechos de código</span><span class="sxs-lookup"><span data-stu-id="95d8d-139">Code Snippets</span></span>
<span data-ttu-id="95d8d-140">Vamos analisar alguns trechos de código e suas saídas esperadas.</span><span class="sxs-lookup"><span data-stu-id="95d8d-140">Let us look at a few code snippets and their expected outputs.</span></span> <span data-ttu-id="95d8d-141">O tratamento de exceção é ignorado nesta seção.</span><span class="sxs-lookup"><span data-stu-id="95d8d-141">Exception handling is ignored in this section.</span></span>

### <a name="enqueueasync"></a><span data-ttu-id="95d8d-142">EnqueueAsync</span><span class="sxs-lookup"><span data-stu-id="95d8d-142">EnqueueAsync</span></span>
<span data-ttu-id="95d8d-143">Aqui estão alguns trechos de código para usar EnqueueAsync seguidos por suas saídas esperadas.</span><span class="sxs-lookup"><span data-stu-id="95d8d-143">Here are a few code snippets for using EnqueueAsync followed by their expected outputs.</span></span>

- <span data-ttu-id="95d8d-144">*Caso 1: Tarefa única de enfileiramento*</span><span class="sxs-lookup"><span data-stu-id="95d8d-144">*Case 1: Single Enqueue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="95d8d-145">Suponha que essa tarefa Olá foi concluída com êxito e que houve as transações simultâneas modificando fila hello.</span><span class="sxs-lookup"><span data-stu-id="95d8d-145">Assume that hello task completed successfully, and that there were no concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="95d8d-146">usuário de saudação pode esperar itens da saudação fila toocontain hello em qualquer Olá pedidos a seguir:</span><span class="sxs-lookup"><span data-stu-id="95d8d-146">hello user can expect hello queue toocontain hello items in any of hello following orders:</span></span>

> <span data-ttu-id="95d8d-147">10, 20</span><span class="sxs-lookup"><span data-stu-id="95d8d-147">10, 20</span></span>

> <span data-ttu-id="95d8d-148">20, 10</span><span class="sxs-lookup"><span data-stu-id="95d8d-148">20, 10</span></span>


- <span data-ttu-id="95d8d-149">*Caso 2: Tarefa paralela de enfileiramento*</span><span class="sxs-lookup"><span data-stu-id="95d8d-149">*Case 2: Parallel Enqueue Task*</span></span>

```
// Parallel Task 1
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}

// Parallel Task 2
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 30, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 40, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="95d8d-150">Suponha que tarefas Olá concluída com êxito, que tarefas Olá foi executado em paralelo e que não houve nenhuma outra transação simultânea modificando fila hello.</span><span class="sxs-lookup"><span data-stu-id="95d8d-150">Assume that hello tasks completed successfully, that hello tasks ran in parallel, and that there were no other concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="95d8d-151">A inferência não pode ser feita sobre ordem de saudação de itens na fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="95d8d-151">No inference can be made about hello order of items in hello queue.</span></span> <span data-ttu-id="95d8d-152">Este trecho de código, itens de saudação podem aparecer em qualquer um dos Olá 4!</span><span class="sxs-lookup"><span data-stu-id="95d8d-152">For this code snippet, hello items may appear in any of hello 4!</span></span> <span data-ttu-id="95d8d-153">ordenações possíveis.</span><span class="sxs-lookup"><span data-stu-id="95d8d-153">possible orderings.</span></span>  <span data-ttu-id="95d8d-154">fila de saudação tentará itens de saudação tookeep na ordem do hello original (enfileirados), mas pode ser forçado tooreordê-los devido a operações de tooconcurrent ou falhas.</span><span class="sxs-lookup"><span data-stu-id="95d8d-154">hello queue will attempt tookeep hello items in hello original (enqueued) order, but may be forced tooreorder them due tooconcurrent operations or faults.</span></span>


### <a name="dequeueasync"></a><span data-ttu-id="95d8d-155">DequeueAsync</span><span class="sxs-lookup"><span data-stu-id="95d8d-155">DequeueAsync</span></span>
<span data-ttu-id="95d8d-156">Aqui estão alguns trechos de código para usar TryDequeueAsync seguido de saídas Olá esperado.</span><span class="sxs-lookup"><span data-stu-id="95d8d-156">Here are a few code snippets for using TryDequeueAsync followed by hello expected outputs.</span></span> <span data-ttu-id="95d8d-157">Suponha que essa fila Olá já está preenchida com hello itens na fila de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="95d8d-157">Assume that hello queue is already populated with hello following items in hello queue:</span></span>
> <span data-ttu-id="95d8d-158">10, 20, 30, 40, 50, 60</span><span class="sxs-lookup"><span data-stu-id="95d8d-158">10, 20, 30, 40, 50, 60</span></span>

- <span data-ttu-id="95d8d-159">*Caso 1: Tarefa única de remoção da fila*</span><span class="sxs-lookup"><span data-stu-id="95d8d-159">*Case 1: Single Dequeue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="95d8d-160">Suponha que essa tarefa Olá foi concluída com êxito e que houve as transações simultâneas modificando fila hello.</span><span class="sxs-lookup"><span data-stu-id="95d8d-160">Assume that hello task completed successfully, and that there were no concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="95d8d-161">Desde a inferência não pode ser feita sobre ordem de saudação de itens de saudação na fila de saudação, qualquer três itens Olá podem ser removida da fila, em qualquer ordem.</span><span class="sxs-lookup"><span data-stu-id="95d8d-161">Since no inference can be made about hello order of hello items in hello queue, any three of hello items may be dequeued, in any order.</span></span> <span data-ttu-id="95d8d-162">fila de saudação tentará itens de saudação tookeep na ordem do hello original (enfileirados), mas pode ser forçado tooreordê-los devido a operações de tooconcurrent ou falhas.</span><span class="sxs-lookup"><span data-stu-id="95d8d-162">hello queue will attempt tookeep hello items in hello original (enqueued) order, but may be forced tooreorder them due tooconcurrent operations or faults.</span></span>  

- <span data-ttu-id="95d8d-163">*Caso 2: Tarefa paralela de remoção da fila*</span><span class="sxs-lookup"><span data-stu-id="95d8d-163">*Case 2: Parallel Dequeue Task*</span></span>

```
// Parallel Task 1
List<int> dequeue1;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}

// Parallel Task 2
List<int> dequeue2;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}
```

<span data-ttu-id="95d8d-164">Suponha que tarefas Olá concluída com êxito, que tarefas Olá foi executado em paralelo e que não houve nenhuma outra transação simultânea modificando fila hello.</span><span class="sxs-lookup"><span data-stu-id="95d8d-164">Assume that hello tasks completed successfully, that hello tasks ran in parallel, and that there were no other concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="95d8d-165">Desde que a inferência não pode ser feita sobre ordem de saudação de itens de saudação na fila de saudação, Olá listas *dequeue1* e *dequeue2* cada conterá quaisquer dois itens, em qualquer ordem.</span><span class="sxs-lookup"><span data-stu-id="95d8d-165">Since no inference can be made about hello order of hello items in hello queue, hello lists *dequeue1* and *dequeue2* will each contain any two items, in any order.</span></span>

<span data-ttu-id="95d8d-166">Olá mesmo item será *não* aparecem em ambas as listas.</span><span class="sxs-lookup"><span data-stu-id="95d8d-166">hello same item will *not* appear in both lists.</span></span> <span data-ttu-id="95d8d-167">Assim, dequeue1 tiver *10*, *30*, então dequeue2 terá *20*, *40*.</span><span class="sxs-lookup"><span data-stu-id="95d8d-167">Hence, if dequeue1 has *10*, *30*, then dequeue2 would have *20*, *40*.</span></span>

- <span data-ttu-id="95d8d-168">*Caso 3: Ordenação de remoção da fila com anulação da transação*</span><span class="sxs-lookup"><span data-stu-id="95d8d-168">*Case 3: Dequeue Ordering With Transaction Abort*</span></span>

<span data-ttu-id="95d8d-169">Anular uma transação com em curso remove da fila coloca itens Olá de volta no cabeçalho de saudação da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="95d8d-169">Aborting a transaction with in-flight dequeues puts hello items back on hello head of hello queue.</span></span> <span data-ttu-id="95d8d-170">ordem de saudação na qual itens Olá sejam colocados de volta no cabeçalho de saudação da fila de saudação não é garantida.</span><span class="sxs-lookup"><span data-stu-id="95d8d-170">hello order in which hello items are put back on hello head of hello queue is not guaranteed.</span></span> <span data-ttu-id="95d8d-171">Vamos dar uma olhada em Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="95d8d-171">Let us look at hello following code:</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort hello transaction
    await txn.AbortAsync();
}
```
<span data-ttu-id="95d8d-172">Suponha que foram removidas da fila itens Olá no hello ordem a seguir:</span><span class="sxs-lookup"><span data-stu-id="95d8d-172">Assume that hello items were dequeued in hello following order:</span></span>
> <span data-ttu-id="95d8d-173">10, 20</span><span class="sxs-lookup"><span data-stu-id="95d8d-173">10, 20</span></span>

<span data-ttu-id="95d8d-174">Quando podemos anulá-Olá, itens Olá seriam adicionados o back toohello do cabeçalho da fila de saudação em qualquer Olá pedidos a seguir:</span><span class="sxs-lookup"><span data-stu-id="95d8d-174">When we abort hello transaction, hello items would be added back toohello head of hello queue in any of hello following orders:</span></span>
> <span data-ttu-id="95d8d-175">10, 20</span><span class="sxs-lookup"><span data-stu-id="95d8d-175">10, 20</span></span>

> <span data-ttu-id="95d8d-176">20, 10</span><span class="sxs-lookup"><span data-stu-id="95d8d-176">20, 10</span></span>

<span data-ttu-id="95d8d-177">Olá mesmo é verdadeiro para todos os casos onde transação Olá não foi *confirmado*.</span><span class="sxs-lookup"><span data-stu-id="95d8d-177">hello same is true for all cases where hello transaction was not successfully *Committed*.</span></span>

## <a name="programming-patterns"></a><span data-ttu-id="95d8d-178">Padrões de programação</span><span class="sxs-lookup"><span data-stu-id="95d8d-178">Programming Patterns</span></span>
<span data-ttu-id="95d8d-179">Nesta seção, vamos analisar alguns padrões de programação que podem ser úteis no uso de ReliableConcurrentQueue.</span><span class="sxs-lookup"><span data-stu-id="95d8d-179">In this section, let us look at a few programming patterns that might be helpful in using ReliableConcurrentQueue.</span></span>

### <a name="batch-dequeues"></a><span data-ttu-id="95d8d-180">Remoções de fila em lote</span><span class="sxs-lookup"><span data-stu-id="95d8d-180">Batch Dequeues</span></span>
<span data-ttu-id="95d8d-181">A recomendado é padrão de programação para Olá consumidor tarefa toobatch seu remove da fila em vez de executar uma remoção da fila por vez.</span><span class="sxs-lookup"><span data-stu-id="95d8d-181">A recommended programming pattern is for hello consumer task toobatch its dequeues instead of performing one dequeue at a time.</span></span> <span data-ttu-id="95d8d-182">usuário Olá pode escolher toothrottle atrasos entre cada tamanho de lote de lote ou hello.</span><span class="sxs-lookup"><span data-stu-id="95d8d-182">hello user can choose toothrottle delays between every batch or hello batch size.</span></span> <span data-ttu-id="95d8d-183">Olá trecho de código a seguir mostra o modelo de programação.</span><span class="sxs-lookup"><span data-stu-id="95d8d-183">hello following code snippet shows this programming model.</span></span>  <span data-ttu-id="95d8d-184">Observe que neste exemplo, processamento de saudação é feito Olá transação é confirmada, para que se uma falha de toooccur durante o processamento, hello itens não processados serão perdidos sem ter sido processado.</span><span class="sxs-lookup"><span data-stu-id="95d8d-184">Note that in this example, hello processing is done after hello transaction is committed, so if a fault were toooccur while processing, hello unprocessed items will be lost without having been processed.</span></span>  <span data-ttu-id="95d8d-185">Como alternativa, o processamento de saudação pode ser feito no escopo da transação hello, no entanto, isso pode ter um impacto negativo no desempenho e requer manipulação de itens de saudação já processados.</span><span class="sxs-lookup"><span data-stu-id="95d8d-185">Alternatively, hello processing can be done within hello transaction's scope, however this may have a negative impact on performance and requires handling of hello items already processed.</span></span>

```
int batchSize = 5;
long delayMs = 100;

while(!cancellationToken.IsCancellationRequested)
{
    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        for(int i = 0; i < batchSize; ++i)
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
            else
            {
                // else break hello for loop
                break;
            }
        }

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }

    int delayFactor = batchSize - processItems.Count;
    await Task.Delay(TimeSpan.FromMilliseconds(delayMs * delayFactor), cancellationToken);
}
```

### <a name="best-effort-notification-based-processing"></a><span data-ttu-id="95d8d-186">Processamento de melhor esforço baseado em notificação</span><span class="sxs-lookup"><span data-stu-id="95d8d-186">Best-Effort Notification-Based Processing</span></span>
<span data-ttu-id="95d8d-187">Outro padrão de programação interessante usa Olá API de contagem.</span><span class="sxs-lookup"><span data-stu-id="95d8d-187">Another interesting programming pattern uses hello Count API.</span></span> <span data-ttu-id="95d8d-188">Aqui, podemos implementar processamento baseada em notificação de melhor esforço para fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="95d8d-188">Here, we can implement best-effort notification-based processing for hello queue.</span></span> <span data-ttu-id="95d8d-189">fila de saudação contagem pode ser usado toothrottle um enfileirar ou uma tarefa de remoção da fila.</span><span class="sxs-lookup"><span data-stu-id="95d8d-189">hello queue Count can be used toothrottle an enqueue or a dequeue task.</span></span>  <span data-ttu-id="95d8d-190">Observe que exemplo hello anterior, como processamento de saudação ocorre fora de transação hello, itens não processados poderão ser perdidos se ocorrer uma falha durante o processamento.</span><span class="sxs-lookup"><span data-stu-id="95d8d-190">Note that as in hello previous example, since hello processing occurs outside hello transaction, unprocessed items may be lost if a fault occurs during processing.</span></span>

```
int threshold = 5;
long delayMs = 1000;

while(!cancellationToken.IsCancellationRequested)
{
    while (this.Queue.Count < threshold)
    {
        cancellationToken.ThrowIfCancellationRequested();

        // If hello queue does not have hello threshold number of items, delay hello task and check again
        await Task.Delay(TimeSpan.FromMilliseconds(delayMs), cancellationToken);
    }

    // If there are approximately threshold number of items, try and process hello queue

    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
        } while (processItems.Count < threshold && ret.HasValue);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
}
```

### <a name="best-effort-drain"></a><span data-ttu-id="95d8d-191">Drenagem de melhor esforço</span><span class="sxs-lookup"><span data-stu-id="95d8d-191">Best-Effort Drain</span></span>
<span data-ttu-id="95d8d-192">Uma drenagem da fila de saudação não pode ser garantida devido a natureza simultâneas toohello Olá da estrutura de dados.</span><span class="sxs-lookup"><span data-stu-id="95d8d-192">A drain of hello queue cannot be guaranteed due toohello concurrent nature of hello data structure.</span></span>  <span data-ttu-id="95d8d-193">É possível que, mesmo se nenhuma operação de usuário na fila de saudação em curso, tooTryDequeueAsync uma chamada específica pode não retornar um item que foi previamente enfileirada e confirmada.</span><span class="sxs-lookup"><span data-stu-id="95d8d-193">It is possible that, even if no user operations on hello queue are in-flight, a particular call tooTryDequeueAsync may not return an item which was previously enqueued and committed.</span></span>  <span data-ttu-id="95d8d-194">item de mensagens de saudação é garantida muito*eventualmente* se tornam visível toodequeue, mas sem um mecanismo de comunicação de fora da banda, um consumidor independente não pode saber essa fila Olá atingiu um estado estável mesmo se todos os produtores tenham sido interrompidos e nenhuma nova operação enqueue é permitidas.</span><span class="sxs-lookup"><span data-stu-id="95d8d-194">hello enqueued item is guaranteed too*eventually* become visible toodequeue, however without an out-of-band communication mechanism, an independent consumer cannot know that hello queue has reached a steady-state even if all producers have been stopped and no new enqueue operations are allowed.</span></span> <span data-ttu-id="95d8d-195">Assim, a operação de drenagem de saudação é melhor esforço conforme implementado abaixo.</span><span class="sxs-lookup"><span data-stu-id="95d8d-195">Thus, hello drain operation is best-effort as implemented below.</span></span>

<span data-ttu-id="95d8d-196">usuário Olá deve interromper todas as outra produtor e tarefas do consumidor e aguarde para qualquer toocommit de transações em trânsito ou anulação, antes de tentar a fila de saudação toodrain.</span><span class="sxs-lookup"><span data-stu-id="95d8d-196">hello user should stop all further producer and consumer tasks, and wait for any in-flight transactions toocommit or abort, before attempting toodrain hello queue.</span></span>  <span data-ttu-id="95d8d-197">Se o usuário Olá sabe número Olá esperado de itens na fila de hello, eles podem configurar uma notificação que indica que todos os itens têm foi removida da fila.</span><span class="sxs-lookup"><span data-stu-id="95d8d-197">If hello user knows hello expected number of items in hello queue, they can set up a notification which signals that all items have been dequeued.</span></span>

```
int numItemsDequeued;
int batchSize = 5;

ConditionalValue ret;

do
{
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if(ret.HasValue)
            {
                // Buffer hello dequeues
                processItems.Add(ret.Value);
            }
        } while (ret.HasValue && processItems.Count < batchSize);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
} while (ret.HasValue);
```

### <a name="peek"></a><span data-ttu-id="95d8d-198">Espiar</span><span class="sxs-lookup"><span data-stu-id="95d8d-198">Peek</span></span>
<span data-ttu-id="95d8d-199">ReliableConcurrentQueue não fornece Olá *TryPeekAsync* api.</span><span class="sxs-lookup"><span data-stu-id="95d8d-199">ReliableConcurrentQueue does not provide hello *TryPeekAsync* api.</span></span> <span data-ttu-id="95d8d-200">Os usuários podem obter uma inspeção Olá semântica usando um *TryDequeueAsync* e, em seguida, anulando a transação de saudação.</span><span class="sxs-lookup"><span data-stu-id="95d8d-200">Users can get hello peek semantic by using a *TryDequeueAsync* and then aborting hello transaction.</span></span> <span data-ttu-id="95d8d-201">Neste exemplo, remove da fila são processadas somente se o valor do item de saudação for maior que *10*.</span><span class="sxs-lookup"><span data-stu-id="95d8d-201">In this example, dequeues are processed only if hello item's value is greater than *10*.</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    ConditionalValue ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);
    bool valueProcessed = false;

    if (ret.HasValue)
    {
        if (ret.Value > 10)
        {
            // Process hello item
            Console.WriteLine("Value : " + ret.Value);
            valueProcessed = true;
        }
    }

    if (valueProcessed)
    {
        await txn.CommitAsync();    
    }
    else
    {
        await txn.AbortAsync();
    }
}
```

## <a name="must-read"></a><span data-ttu-id="95d8d-202">Deve ler</span><span class="sxs-lookup"><span data-stu-id="95d8d-202">Must Read</span></span>
* [<span data-ttu-id="95d8d-203">Início rápido de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="95d8d-203">Reliable Services Quick Start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="95d8d-204">Trabalhando com Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="95d8d-204">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="95d8d-205">Notificações do Reliable Services</span><span class="sxs-lookup"><span data-stu-id="95d8d-205">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="95d8d-206">Backup e restauração de Reliable Services (recuperação de desastre)</span><span class="sxs-lookup"><span data-stu-id="95d8d-206">Reliable Services Backup and Restore (Disaster Recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="95d8d-207">Configuração do Gerenciador de Estado Confiável</span><span class="sxs-lookup"><span data-stu-id="95d8d-207">Reliable State Manager Configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="95d8d-208">Introdução aos serviços de API Web do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="95d8d-208">Getting Started with Service Fabric Web API Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="95d8d-209">Uso avançado de saudação o modelo de programação de serviços confiável</span><span class="sxs-lookup"><span data-stu-id="95d8d-209">Advanced Usage of hello Reliable Services Programming Model</span></span>](service-fabric-reliable-services-advanced-usage.md)
* [<span data-ttu-id="95d8d-210">Referência do desenvolvedor para Coleções Confiáveis</span><span class="sxs-lookup"><span data-stu-id="95d8d-210">Developer Reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
