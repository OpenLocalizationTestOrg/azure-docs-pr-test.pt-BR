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
# <a name="introduction-tooreliableconcurrentqueue-in-azure-service-fabric"></a>Introdução tooReliableConcurrentQueue no Azure Service Fabric
Fila Simultânea Confiável é uma fila assíncrona, transacional e replicada quais apresenta alta simultaneidade para operações de enfileirar e remover da fila. É projetado toodeliver alta taxa de transferência e baixa latência ordenando relaxando Olá estrito FIFO fornecidos pelo [fila confiável](https://msdn.microsoft.com/library/azure/dn971527.aspx) e fornece uma ordenação de melhor esforço.

## <a name="apis"></a>APIs

|Fila Simultânea                |Fila Simultânea Confiável                                         |
|--------------------------------|------------------------------------------------------------------|
| void Enqueue(T item)           | Task EnqueueAsync(ITransaction tx, T item)                       |
| bool TryDequeue(out T result)  | Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)  |
| int Count()                    | long Count()                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a>Comparação com [Fila Confiável](https://msdn.microsoft.com/library/azure/dn971527.aspx)

Confiável simultâneos na fila é oferecido como uma alternativa muito[fila confiável](https://msdn.microsoft.com/library/azure/dn971527.aspx). Ela deve ser usada em casos em que ordenação PEPS estrita não seja necessária, como garantir que PEPS exija uma compensação com simultaneidade.  [Fila confiável](https://msdn.microsoft.com/library/azure/dn971527.aspx) usa bloqueios tooenforce FIFO pedidos, no máximo uma transação permitido tooenqueue e no máximo uma transação permitido toodequeue por vez. Em comparação, simultâneos na fila confiável alivia Olá ordenação de restrição e permite que qualquer número toointerleave de transações simultâneas seu enfileirar e operações de remoção da fila. Ordenação de melhor esforço for fornecido, porém Olá a ordenação relativa de dois valores em uma fila simultâneas confiável pode nunca ser garantida.

Fila Simultâneas Confiáveis fornecem maior taxa de transferência e menor latência que [Fila Confiável](https://msdn.microsoft.com/library/azure/dn971527.aspx) sempre que há várias transações simultâneas executando ações de enfileirar e/ou remover da fila.

Um exemplo de caso de uso para Olá ReliableConcurrentQueue é Olá [fila de mensagens](https://en.wikipedia.org/wiki/Message_queue) cenário. Nesse cenário, produtores de mensagens de uma ou mais criar e adicionar itens toohello fila e um ou mais consumidores de mensagens receber mensagens da fila de saudação e processá-las. Vários produtores e consumidores podem trabalhar de forma independente, usando transações simultâneas na fila de saudação do tooprocess de ordem.

## <a name="usage-guidelines"></a>Diretrizes de uso
* fila de saudação espera que itens de saudação na fila de saudação têm um período de retenção de baixa. Ou seja, itens de saudação não permanece na fila de saudação por um longo tempo.
* fila Olá não garante a ordenação de FIFO estrito.
* fila de saudação não ler seus próprios gravações. Se um item é colocado dentro de uma transação, não será visível tooa dequeuer em hello mesma transação.
* As operações de remover da fila não são isoladas umas das outras. Se o item *um* é removida da fila na transação *txnA*, embora *txnA* item não for confirmada, *um* não será visível tooa simultâneos transação *txnB*.  Se *txnA* anula, *um* ficará visível muito*txnB* imediatamente.
* *TryPeekAsync* comportamento pode ser implementado usando um *TryDequeueAsync* e, em seguida, anulando a transação de saudação. Um exemplo disso pode ser encontrado na seção de padrões de programação de saudação.
* A contagem é não transacional. Pode ser usado tooget uma ideia do número de saudação de elementos na fila Olá, mas representa um point-in-time e não pode ser usado.
* Caro processamento Olá removidas da fila de itens não devem ser executadas enquanto Olá transação está ativa, transações de longa execução tooavoid que podem ter um impacto de desempenho no sistema de saudação.

## <a name="code-snippets"></a>Trechos de código
Vamos analisar alguns trechos de código e suas saídas esperadas. O tratamento de exceção é ignorado nesta seção.

### <a name="enqueueasync"></a>EnqueueAsync
Aqui estão alguns trechos de código para usar EnqueueAsync seguidos por suas saídas esperadas.

- *Caso 1: Tarefa única de enfileiramento*

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

Suponha que essa tarefa Olá foi concluída com êxito e que houve as transações simultâneas modificando fila hello. usuário de saudação pode esperar itens da saudação fila toocontain hello em qualquer Olá pedidos a seguir:

> 10, 20

> 20, 10


- *Caso 2: Tarefa paralela de enfileiramento*

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

Suponha que tarefas Olá concluída com êxito, que tarefas Olá foi executado em paralelo e que não houve nenhuma outra transação simultânea modificando fila hello. A inferência não pode ser feita sobre ordem de saudação de itens na fila de saudação. Este trecho de código, itens de saudação podem aparecer em qualquer um dos Olá 4! ordenações possíveis.  fila de saudação tentará itens de saudação tookeep na ordem do hello original (enfileirados), mas pode ser forçado tooreordê-los devido a operações de tooconcurrent ou falhas.


### <a name="dequeueasync"></a>DequeueAsync
Aqui estão alguns trechos de código para usar TryDequeueAsync seguido de saídas Olá esperado. Suponha que essa fila Olá já está preenchida com hello itens na fila de saudação a seguir:
> 10, 20, 30, 40, 50, 60

- *Caso 1: Tarefa única de remoção da fila*

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

Suponha que essa tarefa Olá foi concluída com êxito e que houve as transações simultâneas modificando fila hello. Desde a inferência não pode ser feita sobre ordem de saudação de itens de saudação na fila de saudação, qualquer três itens Olá podem ser removida da fila, em qualquer ordem. fila de saudação tentará itens de saudação tookeep na ordem do hello original (enfileirados), mas pode ser forçado tooreordê-los devido a operações de tooconcurrent ou falhas.  

- *Caso 2: Tarefa paralela de remoção da fila*

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

Suponha que tarefas Olá concluída com êxito, que tarefas Olá foi executado em paralelo e que não houve nenhuma outra transação simultânea modificando fila hello. Desde que a inferência não pode ser feita sobre ordem de saudação de itens de saudação na fila de saudação, Olá listas *dequeue1* e *dequeue2* cada conterá quaisquer dois itens, em qualquer ordem.

Olá mesmo item será *não* aparecem em ambas as listas. Assim, dequeue1 tiver *10*, *30*, então dequeue2 terá *20*, *40*.

- *Caso 3: Ordenação de remoção da fila com anulação da transação*

Anular uma transação com em curso remove da fila coloca itens Olá de volta no cabeçalho de saudação da fila de saudação. ordem de saudação na qual itens Olá sejam colocados de volta no cabeçalho de saudação da fila de saudação não é garantida. Vamos dar uma olhada em Olá código a seguir:

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort hello transaction
    await txn.AbortAsync();
}
```
Suponha que foram removidas da fila itens Olá no hello ordem a seguir:
> 10, 20

Quando podemos anulá-Olá, itens Olá seriam adicionados o back toohello do cabeçalho da fila de saudação em qualquer Olá pedidos a seguir:
> 10, 20

> 20, 10

Olá mesmo é verdadeiro para todos os casos onde transação Olá não foi *confirmado*.

## <a name="programming-patterns"></a>Padrões de programação
Nesta seção, vamos analisar alguns padrões de programação que podem ser úteis no uso de ReliableConcurrentQueue.

### <a name="batch-dequeues"></a>Remoções de fila em lote
A recomendado é padrão de programação para Olá consumidor tarefa toobatch seu remove da fila em vez de executar uma remoção da fila por vez. usuário Olá pode escolher toothrottle atrasos entre cada tamanho de lote de lote ou hello. Olá trecho de código a seguir mostra o modelo de programação.  Observe que neste exemplo, processamento de saudação é feito Olá transação é confirmada, para que se uma falha de toooccur durante o processamento, hello itens não processados serão perdidos sem ter sido processado.  Como alternativa, o processamento de saudação pode ser feito no escopo da transação hello, no entanto, isso pode ter um impacto negativo no desempenho e requer manipulação de itens de saudação já processados.

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

### <a name="best-effort-notification-based-processing"></a>Processamento de melhor esforço baseado em notificação
Outro padrão de programação interessante usa Olá API de contagem. Aqui, podemos implementar processamento baseada em notificação de melhor esforço para fila de saudação. fila de saudação contagem pode ser usado toothrottle um enfileirar ou uma tarefa de remoção da fila.  Observe que exemplo hello anterior, como processamento de saudação ocorre fora de transação hello, itens não processados poderão ser perdidos se ocorrer uma falha durante o processamento.

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

### <a name="best-effort-drain"></a>Drenagem de melhor esforço
Uma drenagem da fila de saudação não pode ser garantida devido a natureza simultâneas toohello Olá da estrutura de dados.  É possível que, mesmo se nenhuma operação de usuário na fila de saudação em curso, tooTryDequeueAsync uma chamada específica pode não retornar um item que foi previamente enfileirada e confirmada.  item de mensagens de saudação é garantida muito*eventualmente* se tornam visível toodequeue, mas sem um mecanismo de comunicação de fora da banda, um consumidor independente não pode saber essa fila Olá atingiu um estado estável mesmo se todos os produtores tenham sido interrompidos e nenhuma nova operação enqueue é permitidas. Assim, a operação de drenagem de saudação é melhor esforço conforme implementado abaixo.

usuário Olá deve interromper todas as outra produtor e tarefas do consumidor e aguarde para qualquer toocommit de transações em trânsito ou anulação, antes de tentar a fila de saudação toodrain.  Se o usuário Olá sabe número Olá esperado de itens na fila de hello, eles podem configurar uma notificação que indica que todos os itens têm foi removida da fila.

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

### <a name="peek"></a>Espiar
ReliableConcurrentQueue não fornece Olá *TryPeekAsync* api. Os usuários podem obter uma inspeção Olá semântica usando um *TryDequeueAsync* e, em seguida, anulando a transação de saudação. Neste exemplo, remove da fila são processadas somente se o valor do item de saudação for maior que *10*.

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

## <a name="must-read"></a>Deve ler
* [Início rápido de Reliable Services](service-fabric-reliable-services-quick-start.md)
* [Trabalhando com Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Notificações do Reliable Services](service-fabric-reliable-services-notifications.md)
* [Backup e restauração de Reliable Services (recuperação de desastre)](service-fabric-reliable-services-backup-restore.md)
* [Configuração do Gerenciador de Estado Confiável](service-fabric-reliable-services-configuration.md)
* [Introdução aos serviços de API Web do Service Fabric](service-fabric-reliable-services-communication-webapi.md)
* [Uso avançado de saudação o modelo de programação de serviços confiável](service-fabric-reliable-services-advanced-usage.md)
* [Referência do desenvolvedor para Coleções Confiáveis](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
