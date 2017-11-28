---
title: ReliableConcurrentQueue no Azure Service Fabric
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
ms.openlocfilehash: 122cb48149477f295a65b8ee623c647b6db10a86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-reliableconcurrentqueue-in-azure-service-fabric"></a><span data-ttu-id="c0008-103">Introdução a ReliableConcurrentQueue no Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c0008-103">Introduction to ReliableConcurrentQueue in Azure Service Fabric</span></span>
<span data-ttu-id="c0008-104">Fila Simultânea Confiável é uma fila assíncrona, transacional e replicada quais apresenta alta simultaneidade para operações de enfileirar e remover da fila.</span><span class="sxs-lookup"><span data-stu-id="c0008-104">Reliable Concurrent Queue is an asynchronous, transactional, and replicated queue which features high concurrency for enqueue and dequeue operations.</span></span> <span data-ttu-id="c0008-105">Ele é projetado para oferecer alta taxa de transferência e baixa latência flexibilizando a rígida ordenação de PEPS fornecida pela [Fila Confiável](https://msdn.microsoft.com/library/azure/dn971527.aspx) e, em vez disso, fornece uma ordenação de melhor esforço.</span><span class="sxs-lookup"><span data-stu-id="c0008-105">It is designed to deliver high throughput and low latency by relaxing the strict FIFO ordering provided by [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) and instead provides a best-effort ordering.</span></span>

## <a name="apis"></a><span data-ttu-id="c0008-106">APIs</span><span class="sxs-lookup"><span data-stu-id="c0008-106">APIs</span></span>

|<span data-ttu-id="c0008-107">Fila Simultânea</span><span class="sxs-lookup"><span data-stu-id="c0008-107">Concurrent Queue</span></span>                |<span data-ttu-id="c0008-108">Fila Simultânea Confiável</span><span class="sxs-lookup"><span data-stu-id="c0008-108">Reliable Concurrent Queue</span></span>                                         |
|--------------------------------|------------------------------------------------------------------|
| <span data-ttu-id="c0008-109">void Enqueue(T item)</span><span class="sxs-lookup"><span data-stu-id="c0008-109">void Enqueue(T item)</span></span>           | <span data-ttu-id="c0008-110">Task EnqueueAsync(ITransaction tx, T item)</span><span class="sxs-lookup"><span data-stu-id="c0008-110">Task EnqueueAsync(ITransaction tx, T item)</span></span>                       |
| <span data-ttu-id="c0008-111">bool TryDequeue(out T result)</span><span class="sxs-lookup"><span data-stu-id="c0008-111">bool TryDequeue(out T result)</span></span>  | <span data-ttu-id="c0008-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span><span class="sxs-lookup"><span data-stu-id="c0008-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span></span>  |
| <span data-ttu-id="c0008-113">int Count()</span><span class="sxs-lookup"><span data-stu-id="c0008-113">int Count()</span></span>                    | <span data-ttu-id="c0008-114">long Count()</span><span class="sxs-lookup"><span data-stu-id="c0008-114">long Count()</span></span>                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a><span data-ttu-id="c0008-115">Comparação com [Fila Confiável](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span><span class="sxs-lookup"><span data-stu-id="c0008-115">Comparison with [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span></span>

<span data-ttu-id="c0008-116">A Fila Simultâneas Confiável é oferecida como uma alternativa à [Fila Confiável](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0008-116">Reliable Concurrent Queue is offered as an alternative to [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span></span> <span data-ttu-id="c0008-117">Ela deve ser usada em casos em que ordenação PEPS estrita não seja necessária, como garantir que PEPS exija uma compensação com simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="c0008-117">It should be used in cases where strict FIFO ordering is not required, as guaranteeing FIFO requires a tradeoff with concurrency.</span></span>  <span data-ttu-id="c0008-118">[Fila Confiável](https://msdn.microsoft.com/library/azure/dn971527.aspx) usa bloqueios para impor a ordenação PEPS, com no máximo uma transação com permissão para enfileirar e no máximo uma transação com permissão para remover da fila por vez.</span><span class="sxs-lookup"><span data-stu-id="c0008-118">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) uses locks to enforce FIFO ordering, with at most one transaction allowed to enqueue and at most one transaction allowed to dequeue at a time.</span></span> <span data-ttu-id="c0008-119">Em comparação, Fila Simultâneos Confiável flexibiliza a restrição de ordenação e permite que qualquer número de transações simultâneas intercale suas operações de enfileirar e remover da fila.</span><span class="sxs-lookup"><span data-stu-id="c0008-119">In comparison, Reliable Concurrent Queue relaxes the ordering constraint and allows any number concurrent transactions to interleave their enqueue and dequeue operations.</span></span> <span data-ttu-id="c0008-120">Ordenação de melhor esforço é fornecido, porém, a ordenação relativa de dois valores em uma Fila Simultânea Confiável nunca pode ser garantida.</span><span class="sxs-lookup"><span data-stu-id="c0008-120">Best-effort ordering is provided, however the relative ordering of two values in a Reliable Concurrent Queue can never be guaranteed.</span></span>

<span data-ttu-id="c0008-121">Fila Simultâneas Confiáveis fornecem maior taxa de transferência e menor latência que [Fila Confiável](https://msdn.microsoft.com/library/azure/dn971527.aspx) sempre que há várias transações simultâneas executando ações de enfileirar e/ou remover da fila.</span><span class="sxs-lookup"><span data-stu-id="c0008-121">Reliable Concurrent Queue provides higher throughput and lower latency than [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) whenever there are multiple concurrent transactions performing enqueues and/or dequeues.</span></span>

<span data-ttu-id="c0008-122">Um exemplo de caso de uso para o ReliableConcurrentQueue é o cenário [Fila de Mensagens](https://en.wikipedia.org/wiki/Message_queue).</span><span class="sxs-lookup"><span data-stu-id="c0008-122">A sample use case for the ReliableConcurrentQueue is the [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario.</span></span> <span data-ttu-id="c0008-123">Nesse cenário, um ou mais produtores de mensagem criam e adicionam itens à fila, e um ou mais consumidores de mensagens capturam mensagens da fila e as processam.</span><span class="sxs-lookup"><span data-stu-id="c0008-123">In this scenario, one or more message producers create and add items to the queue, and one or more message consumers pull messages from the queue and process them.</span></span> <span data-ttu-id="c0008-124">Vários produtores e consumidores podem trabalhar de modo independente, usando transações simultâneas para processar a fila.</span><span class="sxs-lookup"><span data-stu-id="c0008-124">Multiple producers and consumers can work independently, using concurrent transactions in order to process the queue.</span></span>

## <a name="usage-guidelines"></a><span data-ttu-id="c0008-125">Diretrizes de uso</span><span class="sxs-lookup"><span data-stu-id="c0008-125">Usage Guidelines</span></span>
* <span data-ttu-id="c0008-126">A fila espera que os itens na fila tenham um baixo período de retenção.</span><span class="sxs-lookup"><span data-stu-id="c0008-126">The queue expects that the items in the queue have a low retention period.</span></span> <span data-ttu-id="c0008-127">Ou seja, os itens não permanecem na fila por um longo período.</span><span class="sxs-lookup"><span data-stu-id="c0008-127">That is, the items would not stay in the queue for a long time.</span></span>
* <span data-ttu-id="c0008-128">A fila não assegura a ordenação PEPS estrita.</span><span class="sxs-lookup"><span data-stu-id="c0008-128">The queue does not guarantee strict FIFO ordering.</span></span>
* <span data-ttu-id="c0008-129">A fila não lê suas próprias gravações.</span><span class="sxs-lookup"><span data-stu-id="c0008-129">The queue does not read its own writes.</span></span> <span data-ttu-id="c0008-130">Se um item for enfileirado em uma transação, ele não será visível para uma operação de remover da fila na mesma transação.</span><span class="sxs-lookup"><span data-stu-id="c0008-130">If an item is enqueued within a transaction, it will not be visible to a dequeuer within the same transaction.</span></span>
* <span data-ttu-id="c0008-131">As operações de remover da fila não são isoladas umas das outras.</span><span class="sxs-lookup"><span data-stu-id="c0008-131">Dequeues are not isolated from each other.</span></span> <span data-ttu-id="c0008-132">Se o item *A* for removido da fila na transação *txnA*, embora *txnA* não esteja confirmado, o item *A* não ficará visível a uma transação simultânea *txnB*.</span><span class="sxs-lookup"><span data-stu-id="c0008-132">If item *A* is dequeued in transaction *txnA*, even though *txnA* is not committed, item *A* would not be visible to a concurrent transaction *txnB*.</span></span>  <span data-ttu-id="c0008-133">Se *txnA* for anulada, *A* ficará visível a *txnB* imediatamente.</span><span class="sxs-lookup"><span data-stu-id="c0008-133">If *txnA* aborts, *A* will become visible to *txnB* immediately.</span></span>
* <span data-ttu-id="c0008-134">O comportamento *TryPeekAsync* pode ser implementado usando um *TryDequeueAsync* e, em seguida, anulando a transação.</span><span class="sxs-lookup"><span data-stu-id="c0008-134">*TryPeekAsync* behavior can be implemented by using a *TryDequeueAsync* and then aborting the transaction.</span></span> <span data-ttu-id="c0008-135">Um exemplo disso pode ser encontrado na seção de Padrões de Programação.</span><span class="sxs-lookup"><span data-stu-id="c0008-135">An example of this can be found in the Programming Patterns section.</span></span>
* <span data-ttu-id="c0008-136">A contagem é não transacional.</span><span class="sxs-lookup"><span data-stu-id="c0008-136">Count is non-transactional.</span></span> <span data-ttu-id="c0008-137">Você pode usá-la para ter uma ideia do número de elementos na fila, mas representa um ponto no tempo e não é confiável.</span><span class="sxs-lookup"><span data-stu-id="c0008-137">It can be used to get an idea of the number of elements in the queue, but represents a point-in-time and cannot be relied upon.</span></span>
* <span data-ttu-id="c0008-138">Processamento dispendioso nos itens de remoção da fila não deve ser executado enquanto a transação estiver ativa para evitar transações de execução longa que podem afetar o desempenho do sistema.</span><span class="sxs-lookup"><span data-stu-id="c0008-138">Expensive processing on the dequeued items should not be performed while the transaction is active, to avoid long-running transactions which may have a performance impact on the system.</span></span>

## <a name="code-snippets"></a><span data-ttu-id="c0008-139">Trechos de código</span><span class="sxs-lookup"><span data-stu-id="c0008-139">Code Snippets</span></span>
<span data-ttu-id="c0008-140">Vamos analisar alguns trechos de código e suas saídas esperadas.</span><span class="sxs-lookup"><span data-stu-id="c0008-140">Let us look at a few code snippets and their expected outputs.</span></span> <span data-ttu-id="c0008-141">O tratamento de exceção é ignorado nesta seção.</span><span class="sxs-lookup"><span data-stu-id="c0008-141">Exception handling is ignored in this section.</span></span>

### <a name="enqueueasync"></a><span data-ttu-id="c0008-142">EnqueueAsync</span><span class="sxs-lookup"><span data-stu-id="c0008-142">EnqueueAsync</span></span>
<span data-ttu-id="c0008-143">Aqui estão alguns trechos de código para usar EnqueueAsync seguidos por suas saídas esperadas.</span><span class="sxs-lookup"><span data-stu-id="c0008-143">Here are a few code snippets for using EnqueueAsync followed by their expected outputs.</span></span>

- <span data-ttu-id="c0008-144">*Caso 1: Tarefa única de enfileiramento*</span><span class="sxs-lookup"><span data-stu-id="c0008-144">*Case 1: Single Enqueue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="c0008-145">Suponha que a tarefa tenha sido concluída com êxito e que não tenham ocorrido transações simultâneas que modificassem a fila.</span><span class="sxs-lookup"><span data-stu-id="c0008-145">Assume that the task completed successfully, and that there were no concurrent transactions modifying the queue.</span></span> <span data-ttu-id="c0008-146">O usuário pode esperar que a fila contenha os itens em qualquer uma destas ordens:</span><span class="sxs-lookup"><span data-stu-id="c0008-146">The user can expect the queue to contain the items in any of the following orders:</span></span>

> <span data-ttu-id="c0008-147">10, 20</span><span class="sxs-lookup"><span data-stu-id="c0008-147">10, 20</span></span>

> <span data-ttu-id="c0008-148">20, 10</span><span class="sxs-lookup"><span data-stu-id="c0008-148">20, 10</span></span>


- <span data-ttu-id="c0008-149">*Caso 2: Tarefa paralela de enfileiramento*</span><span class="sxs-lookup"><span data-stu-id="c0008-149">*Case 2: Parallel Enqueue Task*</span></span>

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

<span data-ttu-id="c0008-150">Suponha que as tarefas tenham sido concluídas com êxito, que as tarefas foram executadas em paralelo e que não tenham ocorrido outras transações simultâneas que modificassem a fila.</span><span class="sxs-lookup"><span data-stu-id="c0008-150">Assume that the tasks completed successfully, that the tasks ran in parallel, and that there were no other concurrent transactions modifying the queue.</span></span> <span data-ttu-id="c0008-151">Não é possível inferir a ordem dos itens na fila.</span><span class="sxs-lookup"><span data-stu-id="c0008-151">No inference can be made about the order of items in the queue.</span></span> <span data-ttu-id="c0008-152">Para esse trecho de código, os itens podem aparecer em qualquer uma das 4!</span><span class="sxs-lookup"><span data-stu-id="c0008-152">For this code snippet, the items may appear in any of the 4!</span></span> <span data-ttu-id="c0008-153">ordenações possíveis.</span><span class="sxs-lookup"><span data-stu-id="c0008-153">possible orderings.</span></span>  <span data-ttu-id="c0008-154">A fila tentará manter os itens na ordem original (enfileirados), mas poderá ser forçada a reordená-los devido a falhas ou operações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="c0008-154">The queue will attempt to keep the items in the original (enqueued) order, but may be forced to reorder them due to concurrent operations or faults.</span></span>


### <a name="dequeueasync"></a><span data-ttu-id="c0008-155">DequeueAsync</span><span class="sxs-lookup"><span data-stu-id="c0008-155">DequeueAsync</span></span>
<span data-ttu-id="c0008-156">Aqui estão alguns trechos de código para usar TryDequeueAsync seguidos pelas suas saídas esperadas.</span><span class="sxs-lookup"><span data-stu-id="c0008-156">Here are a few code snippets for using TryDequeueAsync followed by the expected outputs.</span></span> <span data-ttu-id="c0008-157">Suponha que a fila já está preenchida com os seguintes itens na fila:</span><span class="sxs-lookup"><span data-stu-id="c0008-157">Assume that the queue is already populated with the following items in the queue:</span></span>
> <span data-ttu-id="c0008-158">10, 20, 30, 40, 50, 60</span><span class="sxs-lookup"><span data-stu-id="c0008-158">10, 20, 30, 40, 50, 60</span></span>

- <span data-ttu-id="c0008-159">*Caso 1: Tarefa única de remoção da fila*</span><span class="sxs-lookup"><span data-stu-id="c0008-159">*Case 1: Single Dequeue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="c0008-160">Suponha que a tarefa tenha sido concluída com êxito e que não tenham ocorrido transações simultâneas que modificassem a fila.</span><span class="sxs-lookup"><span data-stu-id="c0008-160">Assume that the task completed successfully, and that there were no concurrent transactions modifying the queue.</span></span> <span data-ttu-id="c0008-161">Uma vez que não se pode fazer nenhuma inferência sobre a ordem dos itens na fila, qualquer um dos três itens pode ser removido da fila em qualquer ordem.</span><span class="sxs-lookup"><span data-stu-id="c0008-161">Since no inference can be made about the order of the items in the queue, any three of the items may be dequeued, in any order.</span></span> <span data-ttu-id="c0008-162">A fila tentará manter os itens na ordem original (enfileirados), mas poderá ser forçada a reordená-los devido a falhas ou operações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="c0008-162">The queue will attempt to keep the items in the original (enqueued) order, but may be forced to reorder them due to concurrent operations or faults.</span></span>  

- <span data-ttu-id="c0008-163">*Caso 2: Tarefa paralela de remoção da fila*</span><span class="sxs-lookup"><span data-stu-id="c0008-163">*Case 2: Parallel Dequeue Task*</span></span>

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

<span data-ttu-id="c0008-164">Suponha que as tarefas tenham sido concluídas com êxito, que as tarefas foram executadas em paralelo e que não tenham ocorrido outras transações simultâneas que modificassem a fila.</span><span class="sxs-lookup"><span data-stu-id="c0008-164">Assume that the tasks completed successfully, that the tasks ran in parallel, and that there were no other concurrent transactions modifying the queue.</span></span> <span data-ttu-id="c0008-165">Uma vez que não se pode fazer nenhuma inferência sobre a ordem dos itens na fila, as listas *dequeue1* e *dequeue2* conterão, cada uma, qualquer um dos dois itens em qualquer ordem.</span><span class="sxs-lookup"><span data-stu-id="c0008-165">Since no inference can be made about the order of the items in the queue, the lists *dequeue1* and *dequeue2* will each contain any two items, in any order.</span></span>

<span data-ttu-id="c0008-166">O mesmo item *não* aparecerá em ambas as listas.</span><span class="sxs-lookup"><span data-stu-id="c0008-166">The same item will *not* appear in both lists.</span></span> <span data-ttu-id="c0008-167">Assim, dequeue1 tiver *10*, *30*, então dequeue2 terá *20*, *40*.</span><span class="sxs-lookup"><span data-stu-id="c0008-167">Hence, if dequeue1 has *10*, *30*, then dequeue2 would have *20*, *40*.</span></span>

- <span data-ttu-id="c0008-168">*Caso 3: Ordenação de remoção da fila com anulação da transação*</span><span class="sxs-lookup"><span data-stu-id="c0008-168">*Case 3: Dequeue Ordering With Transaction Abort*</span></span>

<span data-ttu-id="c0008-169">Anular uma transação com remoções de fila em andamento coloca que os itens de volta no topo da fila.</span><span class="sxs-lookup"><span data-stu-id="c0008-169">Aborting a transaction with in-flight dequeues puts the items back on the head of the queue.</span></span> <span data-ttu-id="c0008-170">A ordem em que os itens são colocados de volta no topo da fila não é garantida.</span><span class="sxs-lookup"><span data-stu-id="c0008-170">The order in which the items are put back on the head of the queue is not guaranteed.</span></span> <span data-ttu-id="c0008-171">Vamos examine o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="c0008-171">Let us look at the following code:</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort the transaction
    await txn.AbortAsync();
}
```
<span data-ttu-id="c0008-172">Suponha que os itens foram removidos da fila na seguinte ordem:</span><span class="sxs-lookup"><span data-stu-id="c0008-172">Assume that the items were dequeued in the following order:</span></span>
> <span data-ttu-id="c0008-173">10, 20</span><span class="sxs-lookup"><span data-stu-id="c0008-173">10, 20</span></span>

<span data-ttu-id="c0008-174">Quando anulamos a transação, os itens são adicionados de volta ao topo da fila em qualquer uma das ordens a seguir:</span><span class="sxs-lookup"><span data-stu-id="c0008-174">When we abort the transaction, the items would be added back to the head of the queue in any of the following orders:</span></span>
> <span data-ttu-id="c0008-175">10, 20</span><span class="sxs-lookup"><span data-stu-id="c0008-175">10, 20</span></span>

> <span data-ttu-id="c0008-176">20, 10</span><span class="sxs-lookup"><span data-stu-id="c0008-176">20, 10</span></span>

<span data-ttu-id="c0008-177">O mesmo é verdadeiro para todos os casos em que a transação não foi *Confirmada* com sucesso.</span><span class="sxs-lookup"><span data-stu-id="c0008-177">The same is true for all cases where the transaction was not successfully *Committed*.</span></span>

## <a name="programming-patterns"></a><span data-ttu-id="c0008-178">Padrões de programação</span><span class="sxs-lookup"><span data-stu-id="c0008-178">Programming Patterns</span></span>
<span data-ttu-id="c0008-179">Nesta seção, vamos analisar alguns padrões de programação que podem ser úteis no uso de ReliableConcurrentQueue.</span><span class="sxs-lookup"><span data-stu-id="c0008-179">In this section, let us look at a few programming patterns that might be helpful in using ReliableConcurrentQueue.</span></span>

### <a name="batch-dequeues"></a><span data-ttu-id="c0008-180">Remoções de fila em lote</span><span class="sxs-lookup"><span data-stu-id="c0008-180">Batch Dequeues</span></span>
<span data-ttu-id="c0008-181">O padrão de programação recomendado é a tarefa de consumidor realizar remoções da fila em lote, em vez de executar uma remoção da fila por vez.</span><span class="sxs-lookup"><span data-stu-id="c0008-181">A recommended programming pattern is for the consumer task to batch its dequeues instead of performing one dequeue at a time.</span></span> <span data-ttu-id="c0008-182">O usuário pode optar por restringir atrasos entre cada lote ou o tamanho do lote.</span><span class="sxs-lookup"><span data-stu-id="c0008-182">The user can choose to throttle delays between every batch or the batch size.</span></span> <span data-ttu-id="c0008-183">O trecho de código a seguir mostra esse modelo de programação.</span><span class="sxs-lookup"><span data-stu-id="c0008-183">The following code snippet shows this programming model.</span></span>  <span data-ttu-id="c0008-184">Observe que, neste exemplo, o processamento é feito depois que a transação é confirmada, portanto, se ocorrer uma falha durante o processamento, os itens não processados serão perdidos sem terem sido processados.</span><span class="sxs-lookup"><span data-stu-id="c0008-184">Note that in this example, the processing is done after the transaction is committed, so if a fault were to occur while processing, the unprocessed items will be lost without having been processed.</span></span>  <span data-ttu-id="c0008-185">Como alternativa, o processamento pode ser feito no escopo da transação, no entanto, isso pode ter um impacto negativo no desempenho e requer tratamento dos itens já processados.</span><span class="sxs-lookup"><span data-stu-id="c0008-185">Alternatively, the processing can be done within the transaction's scope, however this may have a negative impact on performance and requires handling of the items already processed.</span></span>

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
                // If an item was dequeued, add to the buffer for processing
                processItems.Add(ret.Value);
            }
            else
            {
                // else break the for loop
                break;
            }
        }

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }

    int delayFactor = batchSize - processItems.Count;
    await Task.Delay(TimeSpan.FromMilliseconds(delayMs * delayFactor), cancellationToken);
}
```

### <a name="best-effort-notification-based-processing"></a><span data-ttu-id="c0008-186">Processamento de melhor esforço baseado em notificação</span><span class="sxs-lookup"><span data-stu-id="c0008-186">Best-Effort Notification-Based Processing</span></span>
<span data-ttu-id="c0008-187">Outro padrão de programação interessante usa a API de Contagem.</span><span class="sxs-lookup"><span data-stu-id="c0008-187">Another interesting programming pattern uses the Count API.</span></span> <span data-ttu-id="c0008-188">Aqui, podemos implementar o processamento baseado em notificação de melhor esforço para a fila.</span><span class="sxs-lookup"><span data-stu-id="c0008-188">Here, we can implement best-effort notification-based processing for the queue.</span></span> <span data-ttu-id="c0008-189">A Contagem de fila pode ser usada para restringir uma tarefa de enfileiramento ou de remoção da fila.</span><span class="sxs-lookup"><span data-stu-id="c0008-189">The queue Count can be used to throttle an enqueue or a dequeue task.</span></span>  <span data-ttu-id="c0008-190">Observe que, como no exemplo anterior, já que o processamento ocorre fora da transação, os itens não processados poderão ser perdidos se ocorrer uma falha durante o processamento.</span><span class="sxs-lookup"><span data-stu-id="c0008-190">Note that as in the previous example, since the processing occurs outside the transaction, unprocessed items may be lost if a fault occurs during processing.</span></span>

```
int threshold = 5;
long delayMs = 1000;

while(!cancellationToken.IsCancellationRequested)
{
    while (this.Queue.Count < threshold)
    {
        cancellationToken.ThrowIfCancellationRequested();

        // If the queue does not have the threshold number of items, delay the task and check again
        await Task.Delay(TimeSpan.FromMilliseconds(delayMs), cancellationToken);
    }

    // If there are approximately threshold number of items, try and process the queue

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
                // If an item was dequeued, add to the buffer for processing
                processItems.Add(ret.Value);
            }
        } while (processItems.Count < threshold && ret.HasValue);

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
}
```

### <a name="best-effort-drain"></a><span data-ttu-id="c0008-191">Drenagem de melhor esforço</span><span class="sxs-lookup"><span data-stu-id="c0008-191">Best-Effort Drain</span></span>
<span data-ttu-id="c0008-192">Uma drenagem da fila não pode ser garantida devido à natureza simultânea da estrutura de dados.</span><span class="sxs-lookup"><span data-stu-id="c0008-192">A drain of the queue cannot be guaranteed due to the concurrent nature of the data structure.</span></span>  <span data-ttu-id="c0008-193">É possível que, mesmo que nenhuma operação de usuário na fila esteja em andamento, uma chamada específica para TryDequeueAsync não retorne um item que foi anteriormente enfileirado e confirmado.</span><span class="sxs-lookup"><span data-stu-id="c0008-193">It is possible that, even if no user operations on the queue are in-flight, a particular call to TryDequeueAsync may not return an item which was previously enqueued and committed.</span></span>  <span data-ttu-id="c0008-194">É garantido que o item enfileirado *acabará* ficando visível à remoção da fila, porém, sem um mecanismo de comunicação fora da banda, um consumidor independente não tem como saber que a fila atingiu um estado estável mesmo que todos os produtores tenham sido interrompidos e nenhuma nova operação de enfileiramento seja permitida.</span><span class="sxs-lookup"><span data-stu-id="c0008-194">The enqueued item is guaranteed to *eventually* become visible to dequeue, however without an out-of-band communication mechanism, an independent consumer cannot know that the queue has reached a steady-state even if all producers have been stopped and no new enqueue operations are allowed.</span></span> <span data-ttu-id="c0008-195">Portanto, a operação de drenagem é o melhor esforço conforme implementado abaixo.</span><span class="sxs-lookup"><span data-stu-id="c0008-195">Thus, the drain operation is best-effort as implemented below.</span></span>

<span data-ttu-id="c0008-196">O usuário deve interromper todas as outras tarefas de produtor e consumidor e esperar qualquer transação em andamento ser confirmada ou anulada antes de tentar drenar a fila.</span><span class="sxs-lookup"><span data-stu-id="c0008-196">The user should stop all further producer and consumer tasks, and wait for any in-flight transactions to commit or abort, before attempting to drain the queue.</span></span>  <span data-ttu-id="c0008-197">Se o usuário souber qual é o número esperado de itens na fila, ele poderá configurar uma notificação que sinalize que todos os itens foram removidos da fila.</span><span class="sxs-lookup"><span data-stu-id="c0008-197">If the user knows the expected number of items in the queue, they can set up a notification which signals that all items have been dequeued.</span></span>

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
                // Buffer the dequeues
                processItems.Add(ret.Value);
            }
        } while (ret.HasValue && processItems.Count < batchSize);

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
} while (ret.HasValue);
```

### <a name="peek"></a><span data-ttu-id="c0008-198">Espiar</span><span class="sxs-lookup"><span data-stu-id="c0008-198">Peek</span></span>
<span data-ttu-id="c0008-199">ReliableConcurrentQueue não fornece a API *TryPeekAsync*.</span><span class="sxs-lookup"><span data-stu-id="c0008-199">ReliableConcurrentQueue does not provide the *TryPeekAsync* api.</span></span> <span data-ttu-id="c0008-200">Os usuários podem obter a semântica da espiada usando um *TryDequeueAsync* e, em seguida, anulando a transação.</span><span class="sxs-lookup"><span data-stu-id="c0008-200">Users can get the peek semantic by using a *TryDequeueAsync* and then aborting the transaction.</span></span> <span data-ttu-id="c0008-201">Neste exemplo, remoções da fila serão processadas somente se o valor do item for maior do que *10*.</span><span class="sxs-lookup"><span data-stu-id="c0008-201">In this example, dequeues are processed only if the item's value is greater than *10*.</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    ConditionalValue ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);
    bool valueProcessed = false;

    if (ret.HasValue)
    {
        if (ret.Value > 10)
        {
            // Process the item
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

## <a name="must-read"></a><span data-ttu-id="c0008-202">Deve ler</span><span class="sxs-lookup"><span data-stu-id="c0008-202">Must Read</span></span>
* [<span data-ttu-id="c0008-203">Início rápido de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="c0008-203">Reliable Services Quick Start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="c0008-204">Trabalhando com Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="c0008-204">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="c0008-205">Notificações do Reliable Services</span><span class="sxs-lookup"><span data-stu-id="c0008-205">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="c0008-206">Backup e restauração de Reliable Services (recuperação de desastre)</span><span class="sxs-lookup"><span data-stu-id="c0008-206">Reliable Services Backup and Restore (Disaster Recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="c0008-207">Configuração do Gerenciador de Estado Confiável</span><span class="sxs-lookup"><span data-stu-id="c0008-207">Reliable State Manager Configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="c0008-208">Introdução aos serviços de API Web do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c0008-208">Getting Started with Service Fabric Web API Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="c0008-209">Uso avançado do modelo de programação de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="c0008-209">Advanced Usage of the Reliable Services Programming Model</span></span>](service-fabric-reliable-services-advanced-usage.md)
* [<span data-ttu-id="c0008-210">Referência do desenvolvedor para Coleções Confiáveis</span><span class="sxs-lookup"><span data-stu-id="c0008-210">Developer Reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
