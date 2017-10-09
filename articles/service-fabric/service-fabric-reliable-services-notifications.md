---
title: "notificações de serviços aaaReliable | Microsoft Docs"
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
ms.openlocfilehash: 8c43190d31dbe82d1dc7fa1c228128bdcc3684f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-notifications"></a><span data-ttu-id="f6df7-103">Notificações do Reliable Services</span><span class="sxs-lookup"><span data-stu-id="f6df7-103">Reliable Services notifications</span></span>
<span data-ttu-id="f6df7-104">As notificações permitem que os clientes tootrack alterações de saudação que estão sendo feitas objeto tooan que elas têm interesse em.</span><span class="sxs-lookup"><span data-stu-id="f6df7-104">Notifications allow clients tootrack hello changes that are being made tooan object that they're interested in.</span></span> <span data-ttu-id="f6df7-105">Dois tipos de objetos dão suporte a notificações: *Gerenciador de Estado Confiável* e *Dicionário Confiável*.</span><span class="sxs-lookup"><span data-stu-id="f6df7-105">Two types of objects support notifications: *Reliable State Manager* and *Reliable Dictionary*.</span></span>

<span data-ttu-id="f6df7-106">Os motivos comuns para usar as Notificações são:</span><span class="sxs-lookup"><span data-stu-id="f6df7-106">Common reasons for using notifications are:</span></span>

* <span data-ttu-id="f6df7-107">Criando exibições, como índices secundários materializadas ou agregado exibições filtradas de estado da réplica de saudação.</span><span class="sxs-lookup"><span data-stu-id="f6df7-107">Building materialized views, such as secondary indexes or aggregated filtered views of hello replica's state.</span></span> <span data-ttu-id="f6df7-108">Um exemplo é um índice classificado de todas as chaves em um Dicionário Confiável.</span><span class="sxs-lookup"><span data-stu-id="f6df7-108">An example is a sorted index of all keys in Reliable Dictionary.</span></span>
* <span data-ttu-id="f6df7-109">Enviados dados de monitoramento, como o número de saudação de usuários adicionados no hello última hora.</span><span class="sxs-lookup"><span data-stu-id="f6df7-109">Sending monitoring data, such as hello number of users added in hello last hour.</span></span>

<span data-ttu-id="f6df7-110">As notificações são disparadas como parte da aplicação de operações.</span><span class="sxs-lookup"><span data-stu-id="f6df7-110">Notifications are fired as part of applying operations.</span></span> <span data-ttu-id="f6df7-111">Por disso, as notificações devem ser manipuladas tão rápido quanto possível, e eventos síncronos não devem incluir operações dispendiosas.</span><span class="sxs-lookup"><span data-stu-id="f6df7-111">Because of that, notifications should be handled as fast as possible, and synchronous events shouldn't include any expensive operations.</span></span>

## <a name="reliable-state-manager-notifications"></a><span data-ttu-id="f6df7-112">Notificações do Gerenciador de Estado Confiável</span><span class="sxs-lookup"><span data-stu-id="f6df7-112">Reliable State Manager notifications</span></span>
<span data-ttu-id="f6df7-113">Gerenciador de estado confiável oferece notificações para Olá eventos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f6df7-113">Reliable State Manager provides notifications for hello following events:</span></span>

* <span data-ttu-id="f6df7-114">Transação</span><span class="sxs-lookup"><span data-stu-id="f6df7-114">Transaction</span></span>
  * <span data-ttu-id="f6df7-115">Confirmar</span><span class="sxs-lookup"><span data-stu-id="f6df7-115">Commit</span></span>
* <span data-ttu-id="f6df7-116">Gerenciador de estado</span><span class="sxs-lookup"><span data-stu-id="f6df7-116">State manager</span></span>
  * <span data-ttu-id="f6df7-117">Recompilação</span><span class="sxs-lookup"><span data-stu-id="f6df7-117">Rebuild</span></span>
  * <span data-ttu-id="f6df7-118">Adição de um estado confiável</span><span class="sxs-lookup"><span data-stu-id="f6df7-118">Addition of a reliable state</span></span>
  * <span data-ttu-id="f6df7-119">Remoção de um estado confiável</span><span class="sxs-lookup"><span data-stu-id="f6df7-119">Removal of a reliable state</span></span>

<span data-ttu-id="f6df7-120">Gerenciador de estado confiável rastreia transações atuais de inflight hello.</span><span class="sxs-lookup"><span data-stu-id="f6df7-120">Reliable State Manager tracks hello current inflight transactions.</span></span> <span data-ttu-id="f6df7-121">Olá única alteração no estado de transação que faz com que um toobe notificação acionado é uma transação sendo confirmada.</span><span class="sxs-lookup"><span data-stu-id="f6df7-121">hello only change in transaction state that causes a notification toobe fired is a transaction being committed.</span></span>

<span data-ttu-id="f6df7-122">O Gerenciador de Estado Confiável mantém uma coleção de estados confiáveis, como Dicionário Confiável e Fila Confiável.</span><span class="sxs-lookup"><span data-stu-id="f6df7-122">Reliable State Manager maintains a collection of reliable states like Reliable Dictionary and Reliable Queue.</span></span> <span data-ttu-id="f6df7-123">Gerenciador de estado confiável dispara notificações quando essa coleção é alterada: um estado confiável é adicionado ou removido, ou toda a coleção Olá é reconstruída.</span><span class="sxs-lookup"><span data-stu-id="f6df7-123">Reliable State Manager fires notifications when this collection changes: a reliable state is added or removed, or hello entire collection is rebuilt.</span></span>
<span data-ttu-id="f6df7-124">Olá Gerenciador de estado confiável coleção será recriado em três casos:</span><span class="sxs-lookup"><span data-stu-id="f6df7-124">hello Reliable State Manager collection is rebuilt in three cases:</span></span>

* <span data-ttu-id="f6df7-125">Recuperação: Quando uma réplica é iniciado, ele recupera seu estado anterior de disco hello.</span><span class="sxs-lookup"><span data-stu-id="f6df7-125">Recovery: When a replica starts, it recovers its previous state from hello disk.</span></span> <span data-ttu-id="f6df7-126">No final da saudação de recuperação, ele usa **NotifyStateManagerChangedEventArgs** toofire um evento que contém o conjunto de saudação de estados confiáveis recuperados.</span><span class="sxs-lookup"><span data-stu-id="f6df7-126">At hello end of recovery, it uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of recovered reliable states.</span></span>
* <span data-ttu-id="f6df7-127">Cópia completa: antes de conjunto de configurações de saudação ingressar em uma réplica, ele tem toobe criado.</span><span class="sxs-lookup"><span data-stu-id="f6df7-127">Full copy: Before a replica can join hello configuration set, it has toobe built.</span></span> <span data-ttu-id="f6df7-128">Às vezes, isso requer uma cópia completa do estado do Gerenciador de estado confiável de saudação réplica primária toobe toohello aplicada ocioso réplica secundária.</span><span class="sxs-lookup"><span data-stu-id="f6df7-128">Sometimes, this requires a full copy of Reliable State Manager's state from hello primary replica toobe applied toohello idle secondary replica.</span></span> <span data-ttu-id="f6df7-129">Gerenciador de estado confiável em usos de réplica secundária Olá **NotifyStateManagerChangedEventArgs** toofire um evento que contém o conjunto de saudação de estados confiáveis que adquiriu a réplica primária hello.</span><span class="sxs-lookup"><span data-stu-id="f6df7-129">Reliable State Manager on hello secondary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it acquired from hello primary replica.</span></span>
* <span data-ttu-id="f6df7-130">Restaurar: Em cenários de recuperação de desastres, estado da réplica de saudação pode ser restaurado de um backup por meio de **RestoreAsync**.</span><span class="sxs-lookup"><span data-stu-id="f6df7-130">Restore: In disaster recovery scenarios, hello replica's state can be restored from a backup via **RestoreAsync**.</span></span> <span data-ttu-id="f6df7-131">Nesses casos, usa o Gerenciador de estado confiável na réplica primária Olá **NotifyStateManagerChangedEventArgs** toofire um evento que contém Olá conjunto confiáveis de estados de que ela restaurada do backup hello.</span><span class="sxs-lookup"><span data-stu-id="f6df7-131">In such cases, Reliable State Manager on hello primary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it restored from hello backup.</span></span>

<span data-ttu-id="f6df7-132">tooregister para notificações de transação e/ou notificações de Gerenciador de estado, você precisa tooregister com hello **TransactionChanged** ou **StateManagerChanged** eventos no Gerenciador de estado confiável.</span><span class="sxs-lookup"><span data-stu-id="f6df7-132">tooregister for transaction notifications and/or state manager notifications, you need tooregister with hello **TransactionChanged** or **StateManagerChanged** events on Reliable State Manager.</span></span> <span data-ttu-id="f6df7-133">Um local comum tooregister com esses manipuladores de eventos é o construtor de saudação do seu serviço com monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="f6df7-133">A common place tooregister with these event handlers is hello constructor of your stateful service.</span></span> <span data-ttu-id="f6df7-134">Quando você se registrar no construtor de hello, não perder qualquer notificação causado por uma alteração durante o tempo de vida de saudação do **IReliableStateManager**.</span><span class="sxs-lookup"><span data-stu-id="f6df7-134">When you register on hello constructor, you won't miss any notification that's caused by a change during hello lifetime of **IReliableStateManager**.</span></span>

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

<span data-ttu-id="f6df7-135">Olá **TransactionChanged** usa o manipulador de eventos **NotifyTransactionChangedEventArgs** tooprovide detalhes sobre o evento hello.</span><span class="sxs-lookup"><span data-stu-id="f6df7-135">hello **TransactionChanged** event handler uses **NotifyTransactionChangedEventArgs** tooprovide details about hello event.</span></span> <span data-ttu-id="f6df7-136">Ele contém a propriedade de ação da saudação (por exemplo, **NotifyTransactionChangedAction.Commit**) que especifica o tipo de saudação de alteração.</span><span class="sxs-lookup"><span data-stu-id="f6df7-136">It contains hello action property (for example, **NotifyTransactionChangedAction.Commit**) that specifies hello type of change.</span></span> <span data-ttu-id="f6df7-137">Ele também contém a propriedade de transação de saudação que fornece uma transação de toohello de referência que foram alteradas.</span><span class="sxs-lookup"><span data-stu-id="f6df7-137">It also contains hello transaction property that provides a reference toohello transaction that changed.</span></span>

> [!NOTE]
> <span data-ttu-id="f6df7-138">Hoje, **TransactionChanged** os eventos são gerados somente se Olá a transação é confirmada.</span><span class="sxs-lookup"><span data-stu-id="f6df7-138">Today, **TransactionChanged** events are raised only if hello transaction is committed.</span></span> <span data-ttu-id="f6df7-139">Olá ação é igual muito**NotifyTransactionChangedAction.Commit**.</span><span class="sxs-lookup"><span data-stu-id="f6df7-139">hello action is then equal too**NotifyTransactionChangedAction.Commit**.</span></span> <span data-ttu-id="f6df7-140">Mas em Olá futuras, eventos podem ser gerados para outros tipos de alterações de estado de transação.</span><span class="sxs-lookup"><span data-stu-id="f6df7-140">But in hello future, events might be raised for other types of transaction state changes.</span></span> <span data-ttu-id="f6df7-141">É recomendável verificando ação hello e processar o evento de saudação somente se ele é aquele que você espera.</span><span class="sxs-lookup"><span data-stu-id="f6df7-141">We recommend checking hello action and processing hello event only if it's one that you expect.</span></span>
> 
> 

<span data-ttu-id="f6df7-142">Veja a seguir um exemplo de manipulador de eventos **TransactionChanged** .</span><span class="sxs-lookup"><span data-stu-id="f6df7-142">Following is an example **TransactionChanged** event handler.</span></span>

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

<span data-ttu-id="f6df7-143">Olá **StateManagerChanged** usa o manipulador de eventos **NotifyStateManagerChangedEventArgs** tooprovide detalhes sobre o evento hello.</span><span class="sxs-lookup"><span data-stu-id="f6df7-143">hello **StateManagerChanged** event handler uses **NotifyStateManagerChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="f6df7-144">**NotifyStateManagerChangedEventArgs** tem duas subclasses: **NotifyStateManagerRebuildEventArgs** e **NotifyStateManagerSingleEntityChangedEventArgs**.</span><span class="sxs-lookup"><span data-stu-id="f6df7-144">**NotifyStateManagerChangedEventArgs** has two subclasses: **NotifyStateManagerRebuildEventArgs** and **NotifyStateManagerSingleEntityChangedEventArgs**.</span></span>
<span data-ttu-id="f6df7-145">Você usar a propriedade de ação de saudação na **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** subclasse correto toohello:</span><span class="sxs-lookup"><span data-stu-id="f6df7-145">You use hello action property in **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="f6df7-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="f6df7-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span></span>
* <span data-ttu-id="f6df7-147">**NotifyStateManagerChangedAction.Add** e **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="f6df7-147">**NotifyStateManagerChangedAction.Add** and **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span></span>

<span data-ttu-id="f6df7-148">Veja a seguir um exemplo de manipulador de notificação **StateManagerChanged** .</span><span class="sxs-lookup"><span data-stu-id="f6df7-148">Following is an example **StateManagerChanged** notification handler.</span></span>

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

## <a name="reliable-dictionary-notifications"></a><span data-ttu-id="f6df7-149">Notificações de Dicionário Confiável</span><span class="sxs-lookup"><span data-stu-id="f6df7-149">Reliable Dictionary notifications</span></span>
<span data-ttu-id="f6df7-150">Dicionário confiável oferece notificações para Olá eventos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f6df7-150">Reliable Dictionary provides notifications for hello following events:</span></span>

* <span data-ttu-id="f6df7-151">Recompilar: chamada quando **ReliableDictionary** recuperou o estado de um backup ou recuperou ou copiou o estado local ou backup.</span><span class="sxs-lookup"><span data-stu-id="f6df7-151">Rebuild: Called when **ReliableDictionary** has recovered its state from a recovered or copied local state or backup.</span></span>
* <span data-ttu-id="f6df7-152">Limpar: Chamado quando Olá estado de **ReliableDictionary** foi limpo por meio de saudação **ClearAsync** método.</span><span class="sxs-lookup"><span data-stu-id="f6df7-152">Clear: Called when hello state of **ReliableDictionary** has been cleared through hello **ClearAsync** method.</span></span>
* <span data-ttu-id="f6df7-153">Adicione: Chamado quando um item foi adicionado muito**ReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="f6df7-153">Add: Called when an item has been added too**ReliableDictionary**.</span></span>
* <span data-ttu-id="f6df7-154">Update: chamado quando um item em **IReliableDictionary** tiver sido atualizado.</span><span class="sxs-lookup"><span data-stu-id="f6df7-154">Update: Called when an item in **IReliableDictionary** has been updated.</span></span>
* <span data-ttu-id="f6df7-155">Remove: chamado quando um item em **IReliableDictionary** tiver sido removido.</span><span class="sxs-lookup"><span data-stu-id="f6df7-155">Remove: Called when an item in **IReliableDictionary** has been deleted.</span></span>

<span data-ttu-id="f6df7-156">notificações de dicionário confiável tooget, você precisa tooregister com hello **DictionaryChanged** manipulador de eventos **IReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="f6df7-156">tooget Reliable Dictionary notifications, you need tooregister with hello **DictionaryChanged** event handler on **IReliableDictionary**.</span></span> <span data-ttu-id="f6df7-157">Um local comum é tooregister com esses manipuladores de eventos em Olá **ReliableStateManager.StateManagerChanged** adicionar notificação.</span><span class="sxs-lookup"><span data-stu-id="f6df7-157">A common place tooregister with these event handlers is in hello **ReliableStateManager.StateManagerChanged** add notification.</span></span>
<span data-ttu-id="f6df7-158">Registrando quando **IReliableDictionary** é adicionado muito**IReliableStateManager** garante que as notificações não perder.</span><span class="sxs-lookup"><span data-stu-id="f6df7-158">Registering when **IReliableDictionary** is added too**IReliableStateManager** ensures that you won't miss any notifications.</span></span>

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
> <span data-ttu-id="f6df7-159">**ProcessStateManagerSingleEntityNotification** é o método de exemplo hello que hello anterior **OnStateManagerChangedHandler** exemplo chama.</span><span class="sxs-lookup"><span data-stu-id="f6df7-159">**ProcessStateManagerSingleEntityNotification** is hello sample method that hello preceding **OnStateManagerChangedHandler** example calls.</span></span>
> 
> 

<span data-ttu-id="f6df7-160">código anterior Hello define Olá **IReliableNotificationAsyncCallback** interface, juntamente com **DictionaryChanged**.</span><span class="sxs-lookup"><span data-stu-id="f6df7-160">hello preceding code sets hello **IReliableNotificationAsyncCallback** interface, along with **DictionaryChanged**.</span></span> <span data-ttu-id="f6df7-161">Porque **NotifyDictionaryRebuildEventArgs** contém um **IAsyncEnumerable** interface – qual precisa toobe enumerado assincronamente – reconstrução notificações são disparadas por meio de  **RebuildNotificationAsyncCallback** em vez de **OnDictionaryChangedHandler**.</span><span class="sxs-lookup"><span data-stu-id="f6df7-161">Because **NotifyDictionaryRebuildEventArgs** contains an **IAsyncEnumerable** interface--which needs toobe enumerated asynchronously--rebuild notifications are fired through **RebuildNotificationAsyncCallback** instead of **OnDictionaryChangedHandler**.</span></span>

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
> <span data-ttu-id="f6df7-162">Saudação anterior do código, como parte do processamento de notificação de recriação Olá, Olá primeiro mantidos agregadas do estado é limpo.</span><span class="sxs-lookup"><span data-stu-id="f6df7-162">In hello preceding code, as part of processing hello rebuild notification, first hello maintained aggregated state is cleared.</span></span> <span data-ttu-id="f6df7-163">Porque a coleção confiável Olá estiver sendo reconstruída com um novo estado, todas as notificações anteriores são irrelevantes.</span><span class="sxs-lookup"><span data-stu-id="f6df7-163">Because hello reliable collection is being rebuilt with a new state, all previous notifications are irrelevant.</span></span>
> 
> 

<span data-ttu-id="f6df7-164">Olá **DictionaryChanged** usa o manipulador de eventos **NotifyDictionaryChangedEventArgs** tooprovide detalhes sobre o evento hello.</span><span class="sxs-lookup"><span data-stu-id="f6df7-164">hello **DictionaryChanged** event handler uses **NotifyDictionaryChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="f6df7-165">**NotifyDictionaryChangedEventArgs** tem cinco subclasses.</span><span class="sxs-lookup"><span data-stu-id="f6df7-165">**NotifyDictionaryChangedEventArgs** has five subclasses.</span></span> <span data-ttu-id="f6df7-166">Usar a propriedade de ação Olá em **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** subclasse correto toohello:</span><span class="sxs-lookup"><span data-stu-id="f6df7-166">Use hello action property in **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="f6df7-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="f6df7-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span></span>
* <span data-ttu-id="f6df7-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span><span class="sxs-lookup"><span data-stu-id="f6df7-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span></span>
* <span data-ttu-id="f6df7-169">**NotifyDictionaryChangedAction.Add** e **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="f6df7-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span></span>
* <span data-ttu-id="f6df7-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="f6df7-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span></span>
* <span data-ttu-id="f6df7-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="f6df7-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span></span>

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

## <a name="recommendations"></a><span data-ttu-id="f6df7-172">Recomendações</span><span class="sxs-lookup"><span data-stu-id="f6df7-172">Recommendations</span></span>
* <span data-ttu-id="f6df7-173">*Conclua* os eventos de notificações o mais rápido possível.</span><span class="sxs-lookup"><span data-stu-id="f6df7-173">*Do* complete notification events as fast as possible.</span></span>
* <span data-ttu-id="f6df7-174">*Não* execute quaisquer operações dispendiosas (por exemplo, operações de E/S) como parte de eventos síncronos.</span><span class="sxs-lookup"><span data-stu-id="f6df7-174">*Do not* execute any expensive operations (for example, I/O operations) as part of synchronous events.</span></span>
* <span data-ttu-id="f6df7-175">*Fazer* verificar o tipo de ação de saudação antes de processar eventos hello.</span><span class="sxs-lookup"><span data-stu-id="f6df7-175">*Do* check hello action type before you process hello event.</span></span> <span data-ttu-id="f6df7-176">Novos tipos de ação podem ser adicionados em Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="f6df7-176">New action types might be added in hello future.</span></span>

<span data-ttu-id="f6df7-177">Aqui estão algumas coisas tookeep em mente:</span><span class="sxs-lookup"><span data-stu-id="f6df7-177">Here are some things tookeep in mind:</span></span>

* <span data-ttu-id="f6df7-178">As notificações são disparadas como parte da execução de saudação de uma operação.</span><span class="sxs-lookup"><span data-stu-id="f6df7-178">Notifications are fired as part of hello execution of an operation.</span></span> <span data-ttu-id="f6df7-179">Por exemplo, uma notificação de restauração é acionada como última etapa saudação de uma operação de restauração.</span><span class="sxs-lookup"><span data-stu-id="f6df7-179">For example, a restore notification is fired as hello last step of a restore operation.</span></span> <span data-ttu-id="f6df7-180">Uma restauração não será concluído até que o evento de notificação de saudação é processado.</span><span class="sxs-lookup"><span data-stu-id="f6df7-180">A restore will not finish until hello notification event is processed.</span></span>
* <span data-ttu-id="f6df7-181">Como as notificações são acionadas como parte da saudação aplicar operações, os clientes verão apenas as notificações para operações confirmadas localmente.</span><span class="sxs-lookup"><span data-stu-id="f6df7-181">Because notifications are fired as part of hello applying operations, clients see only notifications for locally committed operations.</span></span> <span data-ttu-id="f6df7-182">E, como operações têm a garantia de apenas toobe confirmada localmente (em outras palavras, conectado), eles podem ou não pode ser desfeitos no hello futuras.</span><span class="sxs-lookup"><span data-stu-id="f6df7-182">And because operations are guaranteed only toobe locally committed (in other words, logged), they might or might not be undone in hello future.</span></span>
* <span data-ttu-id="f6df7-183">No caminho de restauração hello, uma única notificação é disparada para cada operação aplicada.</span><span class="sxs-lookup"><span data-stu-id="f6df7-183">On hello redo path, a single notification is fired for each applied operation.</span></span> <span data-ttu-id="f6df7-184">Isso significa que se a transação T1 inclui Create(X), Delete(X) e Create(X), você obterá uma notificação para criação de saudação de X, um para exclusão hello e um para a criação de saudação novamente, nessa ordem.</span><span class="sxs-lookup"><span data-stu-id="f6df7-184">This means that if transaction T1 includes Create(X), Delete(X), and Create(X), you'll get one notification for hello creation of X, one for hello deletion, and one for hello creation again, in that order.</span></span>
* <span data-ttu-id="f6df7-185">Para transações que contêm várias operações, as operações são aplicadas na ordem de saudação em que foram recebidos na réplica primária de saudação do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="f6df7-185">For transactions that contain multiple operations, operations are applied in hello order in which they were received on hello primary replica from hello user.</span></span>
* <span data-ttu-id="f6df7-186">Como parte do processamento do progresso falso, algumas operações podem ser desfeitas.</span><span class="sxs-lookup"><span data-stu-id="f6df7-186">As part of processing false progress, some operations might be undone.</span></span> <span data-ttu-id="f6df7-187">As notificações são geradas para essas operações de desfazer, reverter o estado de saudação do ponto estável do hello réplica tooa voltar.</span><span class="sxs-lookup"><span data-stu-id="f6df7-187">Notifications are raised for such undo operations, rolling hello state of hello replica back tooa stable point.</span></span> <span data-ttu-id="f6df7-188">Uma diferença importante das notificações de ação de desfazer é que os eventos que têm chaves duplicadas são agregados.</span><span class="sxs-lookup"><span data-stu-id="f6df7-188">One important difference of undo notifications is that events that have duplicate keys are aggregated.</span></span> <span data-ttu-id="f6df7-189">Por exemplo, se a transação T1 é desfeita, você verá uma única notificação tooDelete(X).</span><span class="sxs-lookup"><span data-stu-id="f6df7-189">For example, if transaction T1 is being undone, you'll see a single notification tooDelete(X).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6df7-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f6df7-190">Next steps</span></span>
* [<span data-ttu-id="f6df7-191">Coleções Confiáveis</span><span class="sxs-lookup"><span data-stu-id="f6df7-191">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="f6df7-192">Início Rápido dos Serviços Confiáveis</span><span class="sxs-lookup"><span data-stu-id="f6df7-192">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="f6df7-193">Backup e restauração do Reliable Services (recuperação de desastre)</span><span class="sxs-lookup"><span data-stu-id="f6df7-193">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="f6df7-194">Referência do desenvolvedor para Coleções Confiáveis</span><span class="sxs-lookup"><span data-stu-id="f6df7-194">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

