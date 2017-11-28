---
title: "Notificações de Reliable Services | Microsoft Docs"
description: "Documentação conceitual para notificações de Reliable Services do Service Fabric"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,vturecek
ms.assetid: cdc918dd-5e81-49c8-a03d-7ddcd12a9a76
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/29/2017
ms.author: mcoskun
ms.openlocfilehash: c6a53d851510ed5e6eec1f3ac0f636ad034a6d4c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-services-notifications"></a><span data-ttu-id="ab45c-103">Notificações do Reliable Services</span><span class="sxs-lookup"><span data-stu-id="ab45c-103">Reliable Services notifications</span></span>
<span data-ttu-id="ab45c-104">As notificações permitem que os clientes controle as alterações que estão sendo feitas em um objeto no qual eles estão interessados.</span><span class="sxs-lookup"><span data-stu-id="ab45c-104">Notifications allow clients to track the changes that are being made to an object that they're interested in.</span></span> <span data-ttu-id="ab45c-105">Dois tipos de objetos dão suporte a notificações: *Gerenciador de Estado Confiável* e *Dicionário Confiável*.</span><span class="sxs-lookup"><span data-stu-id="ab45c-105">Two types of objects support notifications: *Reliable State Manager* and *Reliable Dictionary*.</span></span>

<span data-ttu-id="ab45c-106">Os motivos comuns para usar as Notificações são:</span><span class="sxs-lookup"><span data-stu-id="ab45c-106">Common reasons for using notifications are:</span></span>

* <span data-ttu-id="ab45c-107">Criação de modos de exibição materializados, como índices secundários, ou modos de exibição agregadas e filtradas do estado da réplica.</span><span class="sxs-lookup"><span data-stu-id="ab45c-107">Building materialized views, such as secondary indexes or aggregated filtered views of the replica's state.</span></span> <span data-ttu-id="ab45c-108">Um exemplo é um índice classificado de todas as chaves em um Dicionário Confiável.</span><span class="sxs-lookup"><span data-stu-id="ab45c-108">An example is a sorted index of all keys in Reliable Dictionary.</span></span>
* <span data-ttu-id="ab45c-109">Envio de dados de monitoramento, como o número de usuários adicionados na última hora.</span><span class="sxs-lookup"><span data-stu-id="ab45c-109">Sending monitoring data, such as the number of users added in the last hour.</span></span>

<span data-ttu-id="ab45c-110">As notificações são disparadas como parte da aplicação de operações.</span><span class="sxs-lookup"><span data-stu-id="ab45c-110">Notifications are fired as part of applying operations.</span></span> <span data-ttu-id="ab45c-111">Por disso, as notificações devem ser manipuladas tão rápido quanto possível, e eventos síncronos não devem incluir operações dispendiosas.</span><span class="sxs-lookup"><span data-stu-id="ab45c-111">Because of that, notifications should be handled as fast as possible, and synchronous events shouldn't include any expensive operations.</span></span>

## <a name="reliable-state-manager-notifications"></a><span data-ttu-id="ab45c-112">Notificações do Gerenciador de Estado Confiável</span><span class="sxs-lookup"><span data-stu-id="ab45c-112">Reliable State Manager notifications</span></span>
<span data-ttu-id="ab45c-113">O Gerenciador de Estado Confiável fornece notificações para os eventos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab45c-113">Reliable State Manager provides notifications for the following events:</span></span>

* <span data-ttu-id="ab45c-114">Transação</span><span class="sxs-lookup"><span data-stu-id="ab45c-114">Transaction</span></span>
  * <span data-ttu-id="ab45c-115">Confirmar</span><span class="sxs-lookup"><span data-stu-id="ab45c-115">Commit</span></span>
* <span data-ttu-id="ab45c-116">Gerenciador de estado</span><span class="sxs-lookup"><span data-stu-id="ab45c-116">State manager</span></span>
  * <span data-ttu-id="ab45c-117">Recompilação</span><span class="sxs-lookup"><span data-stu-id="ab45c-117">Rebuild</span></span>
  * <span data-ttu-id="ab45c-118">Adição de um estado confiável</span><span class="sxs-lookup"><span data-stu-id="ab45c-118">Addition of a reliable state</span></span>
  * <span data-ttu-id="ab45c-119">Remoção de um estado confiável</span><span class="sxs-lookup"><span data-stu-id="ab45c-119">Removal of a reliable state</span></span>

<span data-ttu-id="ab45c-120">O Gerenciador de Estado Confiável rastreia as transações em execução no momento.</span><span class="sxs-lookup"><span data-stu-id="ab45c-120">Reliable State Manager tracks the current inflight transactions.</span></span> <span data-ttu-id="ab45c-121">A única alteração no estado da transação que faz com que uma notificação seja acionada é uma confirmação de transação.</span><span class="sxs-lookup"><span data-stu-id="ab45c-121">The only change in transaction state that causes a notification to be fired is a transaction being committed.</span></span>

<span data-ttu-id="ab45c-122">O Gerenciador de Estado Confiável mantém uma coleção de estados confiáveis, como Dicionário Confiável e Fila Confiável.</span><span class="sxs-lookup"><span data-stu-id="ab45c-122">Reliable State Manager maintains a collection of reliable states like Reliable Dictionary and Reliable Queue.</span></span> <span data-ttu-id="ab45c-123">O Gerenciador de Estado Confiável dispara notificações quando essa coleção muda: um estado confiável é adicionado ou removido ou toda a coleção é recompilada.</span><span class="sxs-lookup"><span data-stu-id="ab45c-123">Reliable State Manager fires notifications when this collection changes: a reliable state is added or removed, or the entire collection is rebuilt.</span></span>
<span data-ttu-id="ab45c-124">A coleção do Gerenciador de Estado Confiável é recompilada em três casos:</span><span class="sxs-lookup"><span data-stu-id="ab45c-124">The Reliable State Manager collection is rebuilt in three cases:</span></span>

* <span data-ttu-id="ab45c-125">Recuperação: quando uma réplica é iniciada, recupera seu estado anterior do disco.</span><span class="sxs-lookup"><span data-stu-id="ab45c-125">Recovery: When a replica starts, it recovers its previous state from the disk.</span></span> <span data-ttu-id="ab45c-126">Ao fim da recuperação, ela usa **NotifyStateManagerChangedEventArgs** para disparar um evento que contém o conjunto de estados confiáveis recuperados.</span><span class="sxs-lookup"><span data-stu-id="ab45c-126">At the end of recovery, it uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of recovered reliable states.</span></span>
* <span data-ttu-id="ab45c-127">Cópia completa: para que uma réplica possa ingressar no conjunto de configurações, ela deve ser compilada.</span><span class="sxs-lookup"><span data-stu-id="ab45c-127">Full copy: Before a replica can join the configuration set, it has to be built.</span></span> <span data-ttu-id="ab45c-128">Às vezes, isso exige a aplicação de uma cópia completa do estado do Gerenciador de Estado Confiável da réplica primária para a réplica secundária ociosa.</span><span class="sxs-lookup"><span data-stu-id="ab45c-128">Sometimes, this requires a full copy of Reliable State Manager's state from the primary replica to be applied to the idle secondary replica.</span></span> <span data-ttu-id="ab45c-129">O Gerenciador de Estado Confiável na réplica secundária usa **NotifyStateManagerChangedEventArgs** para disparar um evento que contém o conjunto de estados confiáveis que adquiriu da réplica primária.</span><span class="sxs-lookup"><span data-stu-id="ab45c-129">Reliable State Manager on the secondary replica uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of reliable states that it acquired from the primary replica.</span></span>
* <span data-ttu-id="ab45c-130">Restore: em cenários de recuperação de desastres, o estado da réplica pode ser restaurado de um backup por meio de **RestoreAsync**.</span><span class="sxs-lookup"><span data-stu-id="ab45c-130">Restore: In disaster recovery scenarios, the replica's state can be restored from a backup via **RestoreAsync**.</span></span> <span data-ttu-id="ab45c-131">Nesses casos, o Gerenciador de Estado Confiável na réplica primária usa **NotifyStateManagerChangedEventArgs** para disparar um evento que contém o conjunto de estados confiáveis que ele restaurou do backup.</span><span class="sxs-lookup"><span data-stu-id="ab45c-131">In such cases, Reliable State Manager on the primary replica uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of reliable states that it restored from the backup.</span></span>

<span data-ttu-id="ab45c-132">Para se registrar e receber notificações de transação e/ou notificações do gerenciador de estado, você precisa se registrar com eventos **TransactionChanged** ou **StateManagerChanged** no Gerenciador de Estado Confiável.</span><span class="sxs-lookup"><span data-stu-id="ab45c-132">To register for transaction notifications and/or state manager notifications, you need to register with the **TransactionChanged** or **StateManagerChanged** events on Reliable State Manager.</span></span> <span data-ttu-id="ab45c-133">Um lugar comum para registrar esses manipuladores de eventos é o construtor de seu serviço com estado.</span><span class="sxs-lookup"><span data-stu-id="ab45c-133">A common place to register with these event handlers is the constructor of your stateful service.</span></span> <span data-ttu-id="ab45c-134">Quando você se registrar no construtor, não perderá notificações causadas por uma alteração durante a vida útil de **IReliableStateManager**.</span><span class="sxs-lookup"><span data-stu-id="ab45c-134">When you register on the constructor, you won't miss any notification that's caused by a change during the lifetime of **IReliableStateManager**.</span></span>

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

<span data-ttu-id="ab45c-135">O manipulador de eventos **TransactionChanged** usa **NotifyTransactionChangedEventArgs** para fornecer detalhes sobre o evento.</span><span class="sxs-lookup"><span data-stu-id="ab45c-135">The **TransactionChanged** event handler uses **NotifyTransactionChangedEventArgs** to provide details about the event.</span></span> <span data-ttu-id="ab45c-136">Contém a propriedade de ação (por exemplo, **NotifyTransactionChangedAction.Commit**) que especifica o tipo de alteração.</span><span class="sxs-lookup"><span data-stu-id="ab45c-136">It contains the action property (for example, **NotifyTransactionChangedAction.Commit**) that specifies the type of change.</span></span> <span data-ttu-id="ab45c-137">Também contém a propriedade de transação que fornece uma referência para a transação que foi alterada.</span><span class="sxs-lookup"><span data-stu-id="ab45c-137">It also contains the transaction property that provides a reference to the transaction that changed.</span></span>

> [!NOTE]
> <span data-ttu-id="ab45c-138">Hoje, eventos **TransactionChanged** são gerados somente se a transação é confirmada.</span><span class="sxs-lookup"><span data-stu-id="ab45c-138">Today, **TransactionChanged** events are raised only if the transaction is committed.</span></span> <span data-ttu-id="ab45c-139">A ação é igual a **NotifyTransactionChangedAction.Commit**.</span><span class="sxs-lookup"><span data-stu-id="ab45c-139">The action is then equal to **NotifyTransactionChangedAction.Commit**.</span></span> <span data-ttu-id="ab45c-140">Porém, no futuro, eventos poderão ser gerados para outros tipos de alterações de estado de transação.</span><span class="sxs-lookup"><span data-stu-id="ab45c-140">But in the future, events might be raised for other types of transaction state changes.</span></span> <span data-ttu-id="ab45c-141">É recomendável verificar a ação e processar o evento somente se ele for o que você espera.</span><span class="sxs-lookup"><span data-stu-id="ab45c-141">We recommend checking the action and processing the event only if it's one that you expect.</span></span>
> 
> 

<span data-ttu-id="ab45c-142">Veja a seguir um exemplo de manipulador de eventos **TransactionChanged** .</span><span class="sxs-lookup"><span data-stu-id="ab45c-142">Following is an example **TransactionChanged** event handler.</span></span>

```C#
private void OnTransactionChangedHandler(object sender, NotifyTransactionChangedEventArgs e)
{
    if (e.Action == NotifyTransactionChangedAction.Commit)
    {
        this.lastCommitLsn = e.Transaction.CommitSequenceNumber;
        this.lastTransactionId = e.Transaction.TransactionId;

        this.lastCommittedTransactionList.Add(e.Transaction.TransactionId);
    }
}
```

<span data-ttu-id="ab45c-143">O manipulador de eventos **StateManagerChanged** usa **NotifyStateManagerChangedEventArgs** para fornecer detalhes sobre o evento.</span><span class="sxs-lookup"><span data-stu-id="ab45c-143">The **StateManagerChanged** event handler uses **NotifyStateManagerChangedEventArgs** to provide details about the event.</span></span>
<span data-ttu-id="ab45c-144">**NotifyStateManagerChangedEventArgs** tem duas subclasses: **NotifyStateManagerRebuildEventArgs** e **NotifyStateManagerSingleEntityChangedEventArgs**.</span><span class="sxs-lookup"><span data-stu-id="ab45c-144">**NotifyStateManagerChangedEventArgs** has two subclasses: **NotifyStateManagerRebuildEventArgs** and **NotifyStateManagerSingleEntityChangedEventArgs**.</span></span>
<span data-ttu-id="ab45c-145">Use a propriedade de ação no **NotifyStateManagerChangedEventArgs** para converter **NotifyStateManagerChangedEventArgs** na subclasse correta:</span><span class="sxs-lookup"><span data-stu-id="ab45c-145">You use the action property in **NotifyStateManagerChangedEventArgs** to cast **NotifyStateManagerChangedEventArgs** to the correct subclass:</span></span>

* <span data-ttu-id="ab45c-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="ab45c-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span></span>
* <span data-ttu-id="ab45c-147">**NotifyStateManagerChangedAction.Add** e **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="ab45c-147">**NotifyStateManagerChangedAction.Add** and **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span></span>

<span data-ttu-id="ab45c-148">Veja a seguir um exemplo de manipulador de notificação **StateManagerChanged** .</span><span class="sxs-lookup"><span data-stu-id="ab45c-148">Following is an example **StateManagerChanged** notification handler.</span></span>

```C#
public void OnStateManagerChangedHandler(object sender, NotifyStateManagerChangedEventArgs e)
{
    if (e.Action == NotifyStateManagerChangedAction.Rebuild)
    {
        this.ProcessStataManagerRebuildNotification(e);

        return;
    }

    this.ProcessStateManagerSingleEntityNotification(e);
}
```

## <a name="reliable-dictionary-notifications"></a><span data-ttu-id="ab45c-149">Notificações de Dicionário Confiável</span><span class="sxs-lookup"><span data-stu-id="ab45c-149">Reliable Dictionary notifications</span></span>
<span data-ttu-id="ab45c-150">O Dicionário Confiável fornece notificações para os seguintes eventos:</span><span class="sxs-lookup"><span data-stu-id="ab45c-150">Reliable Dictionary provides notifications for the following events:</span></span>

* <span data-ttu-id="ab45c-151">Recompilar: chamada quando **ReliableDictionary** recuperou o estado de um backup ou recuperou ou copiou o estado local ou backup.</span><span class="sxs-lookup"><span data-stu-id="ab45c-151">Rebuild: Called when **ReliableDictionary** has recovered its state from a recovered or copied local state or backup.</span></span>
* <span data-ttu-id="ab45c-152">Limpar: chamado quando o estado de **ReliableDictionary** foi limpo por meio do método **ClearAsync**.</span><span class="sxs-lookup"><span data-stu-id="ab45c-152">Clear: Called when the state of **ReliableDictionary** has been cleared through the **ClearAsync** method.</span></span>
* <span data-ttu-id="ab45c-153">Adicione: Chamado quando um item foi adicionado ao **ReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="ab45c-153">Add: Called when an item has been added to **ReliableDictionary**.</span></span>
* <span data-ttu-id="ab45c-154">Update: chamado quando um item em **IReliableDictionary** tiver sido atualizado.</span><span class="sxs-lookup"><span data-stu-id="ab45c-154">Update: Called when an item in **IReliableDictionary** has been updated.</span></span>
* <span data-ttu-id="ab45c-155">Remove: chamado quando um item em **IReliableDictionary** tiver sido removido.</span><span class="sxs-lookup"><span data-stu-id="ab45c-155">Remove: Called when an item in **IReliableDictionary** has been deleted.</span></span>

<span data-ttu-id="ab45c-156">Para obter notificações de dicionário confiável, você precisa se registrar com o manipulador de eventos **DictionaryChanged** em **IReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="ab45c-156">To get Reliable Dictionary notifications, you need to register with the **DictionaryChanged** event handler on **IReliableDictionary**.</span></span> <span data-ttu-id="ab45c-157">Um lugar comum para se registrar com esses manipuladores de eventos é na notificação de adição **ReliableStateManager.StateManagerChanged** .</span><span class="sxs-lookup"><span data-stu-id="ab45c-157">A common place to register with these event handlers is in the **ReliableStateManager.StateManagerChanged** add notification.</span></span>
<span data-ttu-id="ab45c-158">O registro quando **IReliableDictionary** é adicionado a **IReliableStateManager** garante que você não perca notificações.</span><span class="sxs-lookup"><span data-stu-id="ab45c-158">Registering when **IReliableDictionary** is added to **IReliableStateManager** ensures that you won't miss any notifications.</span></span>

```C#
private void ProcessStateManagerSingleEntityNotification(NotifyStateManagerChangedEventArgs e)
{
    var operation = e as NotifyStateManagerSingleEntityChangedEventArgs;

    if (operation.Action == NotifyStateManagerChangedAction.Add)
    {
        if (operation.ReliableState is IReliableDictionary<TKey, TValue>)
        {
            var dictionary = (IReliableDictionary<TKey, TValue>)operation.ReliableState;
            dictionary.RebuildNotificationAsyncCallback = this.OnDictionaryRebuildNotificationHandlerAsync;
            dictionary.DictionaryChanged += this.OnDictionaryChangedHandler;
            }
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="ab45c-159">**ProcessStateManagerSingleEntityNotification** é o método de exemplo que o exemplo de **OnStateManagerChangedHandler** anterior chama.</span><span class="sxs-lookup"><span data-stu-id="ab45c-159">**ProcessStateManagerSingleEntityNotification** is the sample method that the preceding **OnStateManagerChangedHandler** example calls.</span></span>
> 
> 

<span data-ttu-id="ab45c-160">O conjunto de código anterior define a interface de **IReliableNotificationAsyncCallback**, juntamente com **DictionaryChanged**.</span><span class="sxs-lookup"><span data-stu-id="ab45c-160">The preceding code sets the **IReliableNotificationAsyncCallback** interface, along with **DictionaryChanged**.</span></span> <span data-ttu-id="ab45c-161">Como **NotifyDictionaryRebuildEventArgs** contém uma interface **IAsyncEnumerable** que precisa ser enumerada de forma assíncrona, as notificações de recriação são disparadas por meio de **RebuildNotificationAsyncCallback** em vez de **OnDictionaryChangedHandler**.</span><span class="sxs-lookup"><span data-stu-id="ab45c-161">Because **NotifyDictionaryRebuildEventArgs** contains an **IAsyncEnumerable** interface--which needs to be enumerated asynchronously--rebuild notifications are fired through **RebuildNotificationAsyncCallback** instead of **OnDictionaryChangedHandler**.</span></span>

```C#
public async Task OnDictionaryRebuildNotificationHandlerAsync(
    IReliableDictionary<TKey, TValue> origin,
    NotifyDictionaryRebuildEventArgs<TKey, TValue> rebuildNotification)
{
    this.secondaryIndex.Clear();

    var enumerator = e.State.GetAsyncEnumerator();
    while (await enumerator.MoveNextAsync(CancellationToken.None))
    {
        this.secondaryIndex.Add(enumerator.Current.Key, enumerator.Current.Value);
    }
}
```

> [!NOTE]
> <span data-ttu-id="ab45c-162">No código anterior, como parte do processamento da notificação de recriação, primeiro o estado agregado mantido é limpo.</span><span class="sxs-lookup"><span data-stu-id="ab45c-162">In the preceding code, as part of processing the rebuild notification, first the maintained aggregated state is cleared.</span></span> <span data-ttu-id="ab45c-163">Como a coleção confiável está sendo recompilada com um novo estado, todas as notificações anteriores são irrelevantes.</span><span class="sxs-lookup"><span data-stu-id="ab45c-163">Because the reliable collection is being rebuilt with a new state, all previous notifications are irrelevant.</span></span>
> 
> 

<span data-ttu-id="ab45c-164">O manipulador de eventos **DictionaryChanged** usa o **NotifyDictionaryChangedEventArgs** para fornecer detalhes sobre o evento.</span><span class="sxs-lookup"><span data-stu-id="ab45c-164">The **DictionaryChanged** event handler uses **NotifyDictionaryChangedEventArgs** to provide details about the event.</span></span>
<span data-ttu-id="ab45c-165">**NotifyDictionaryChangedEventArgs** tem cinco subclasses.</span><span class="sxs-lookup"><span data-stu-id="ab45c-165">**NotifyDictionaryChangedEventArgs** has five subclasses.</span></span> <span data-ttu-id="ab45c-166">Use a propriedade de ação em **NotifyDictionaryChangedEventArgs** para converter **NotifyDictionaryChangedEventArgs** na subclasse correta:</span><span class="sxs-lookup"><span data-stu-id="ab45c-166">Use the action property in **NotifyDictionaryChangedEventArgs** to cast **NotifyDictionaryChangedEventArgs** to the correct subclass:</span></span>

* <span data-ttu-id="ab45c-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="ab45c-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span></span>
* <span data-ttu-id="ab45c-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span><span class="sxs-lookup"><span data-stu-id="ab45c-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span></span>
* <span data-ttu-id="ab45c-169">**NotifyDictionaryChangedAction.Add** e **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="ab45c-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span></span>
* <span data-ttu-id="ab45c-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="ab45c-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span></span>
* <span data-ttu-id="ab45c-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="ab45c-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span></span>

```C#
public void OnDictionaryChangedHandler(object sender, NotifyDictionaryChangedEventArgs<TKey, TValue> e)
{
    switch (e.Action)
    {
        case NotifyDictionaryChangedAction.Clear:
            var clearEvent = e as NotifyDictionaryClearEventArgs<TKey, TValue>;
            this.ProcessClearNotification(clearEvent);
            return;

        case NotifyDictionaryChangedAction.Add:
            var addEvent = e as NotifyDictionaryItemAddedEventArgs<TKey, TValue>;
            this.ProcessAddNotification(addEvent);
            return;

        case NotifyDictionaryChangedAction.Update:
            var updateEvent = e as NotifyDictionaryItemUpdatedEventArgs<TKey, TValue>;
            this.ProcessUpdateNotification(updateEvent);
            return;

        case NotifyDictionaryChangedAction.Remove:
            var deleteEvent = e as NotifyDictionaryItemRemovedEventArgs<TKey, TValue>;
            this.ProcessRemoveNotification(deleteEvent);
            return;

        default:
            break;
    }
}
```

## <a name="recommendations"></a><span data-ttu-id="ab45c-172">Recomendações</span><span class="sxs-lookup"><span data-stu-id="ab45c-172">Recommendations</span></span>
* <span data-ttu-id="ab45c-173">*Conclua* os eventos de notificações o mais rápido possível.</span><span class="sxs-lookup"><span data-stu-id="ab45c-173">*Do* complete notification events as fast as possible.</span></span>
* <span data-ttu-id="ab45c-174">*Não* execute quaisquer operações dispendiosas (por exemplo, operações de E/S) como parte de eventos síncronos.</span><span class="sxs-lookup"><span data-stu-id="ab45c-174">*Do not* execute any expensive operations (for example, I/O operations) as part of synchronous events.</span></span>
* <span data-ttu-id="ab45c-175">*Verifique* o tipo de ação antes de processar o evento.</span><span class="sxs-lookup"><span data-stu-id="ab45c-175">*Do* check the action type before you process the event.</span></span> <span data-ttu-id="ab45c-176">Novos tipos de ação podem ser adicionados no futuro.</span><span class="sxs-lookup"><span data-stu-id="ab45c-176">New action types might be added in the future.</span></span>

<span data-ttu-id="ab45c-177">Eis aqui algumas coisas que se deve manter em mente:</span><span class="sxs-lookup"><span data-stu-id="ab45c-177">Here are some things to keep in mind:</span></span>

* <span data-ttu-id="ab45c-178">As notificações são disparadas como parte da execução de uma operação.</span><span class="sxs-lookup"><span data-stu-id="ab45c-178">Notifications are fired as part of the execution of an operation.</span></span> <span data-ttu-id="ab45c-179">Por exemplo, uma notificação de restauração é acionada como a última etapa de uma operação de restauração.</span><span class="sxs-lookup"><span data-stu-id="ab45c-179">For example, a restore notification is fired as the last step of a restore operation.</span></span> <span data-ttu-id="ab45c-180">Uma restauração não será concluída até que o evento de notificação seja processado.</span><span class="sxs-lookup"><span data-stu-id="ab45c-180">A restore will not finish until the notification event is processed.</span></span>
* <span data-ttu-id="ab45c-181">Como as notificações são disparadas como parte das operações de aplicação, os clientes veem apenas as notificações para operações confirmadas localmente.</span><span class="sxs-lookup"><span data-stu-id="ab45c-181">Because notifications are fired as part of the applying operations, clients see only notifications for locally committed operations.</span></span> <span data-ttu-id="ab45c-182">E como as operações têm garantia de serem confirmadas apenas localmente (em outras palavras, registradas em log), podem ou não pode ser desfeitas no futuro.</span><span class="sxs-lookup"><span data-stu-id="ab45c-182">And because operations are guaranteed only to be locally committed (in other words, logged), they might or might not be undone in the future.</span></span>
* <span data-ttu-id="ab45c-183">No caminho de restauração, uma única notificação é disparada para cada operação aplicada.</span><span class="sxs-lookup"><span data-stu-id="ab45c-183">On the redo path, a single notification is fired for each applied operation.</span></span> <span data-ttu-id="ab45c-184">Isso significa que se a transação T1 incluir Create(X), Delete(X) e Create(X), você obterá uma notificação para a criação de X, uma para a exclusão e outra para a criação, nessa ordem.</span><span class="sxs-lookup"><span data-stu-id="ab45c-184">This means that if transaction T1 includes Create(X), Delete(X), and Create(X), you'll get one notification for the creation of X, one for the deletion, and one for the creation again, in that order.</span></span>
* <span data-ttu-id="ab45c-185">Para transações que contêm várias operações, as operações são aplicadas na ordem em que foram recebidas na réplica primária do usuário.</span><span class="sxs-lookup"><span data-stu-id="ab45c-185">For transactions that contain multiple operations, operations are applied in the order in which they were received on the primary replica from the user.</span></span>
* <span data-ttu-id="ab45c-186">Como parte do processamento do progresso falso, algumas operações podem ser desfeitas.</span><span class="sxs-lookup"><span data-stu-id="ab45c-186">As part of processing false progress, some operations might be undone.</span></span> <span data-ttu-id="ab45c-187">As notificações são geradas para essas operações da ação de desfazer, revertendo o estado da réplica de volta a um ponto estável.</span><span class="sxs-lookup"><span data-stu-id="ab45c-187">Notifications are raised for such undo operations, rolling the state of the replica back to a stable point.</span></span> <span data-ttu-id="ab45c-188">Uma diferença importante das notificações de ação de desfazer é que os eventos que têm chaves duplicadas são agregados.</span><span class="sxs-lookup"><span data-stu-id="ab45c-188">One important difference of undo notifications is that events that have duplicate keys are aggregated.</span></span> <span data-ttu-id="ab45c-189">Por exemplo, se a transação T1 estiver sendo desfeita, você verá uma notificação única para Delete(X).</span><span class="sxs-lookup"><span data-stu-id="ab45c-189">For example, if transaction T1 is being undone, you'll see a single notification to Delete(X).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab45c-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ab45c-190">Next steps</span></span>
* [<span data-ttu-id="ab45c-191">Coleções Confiáveis</span><span class="sxs-lookup"><span data-stu-id="ab45c-191">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="ab45c-192">Início Rápido dos Serviços Confiáveis</span><span class="sxs-lookup"><span data-stu-id="ab45c-192">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="ab45c-193">Backup e restauração do Reliable Services (recuperação de desastre)</span><span class="sxs-lookup"><span data-stu-id="ab45c-193">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="ab45c-194">Referência do desenvolvedor para Coleções Confiáveis</span><span class="sxs-lookup"><span data-stu-id="ab45c-194">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

