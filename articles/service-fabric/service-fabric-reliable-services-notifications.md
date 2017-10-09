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
# <a name="reliable-services-notifications"></a>Notificações do Reliable Services
As notificações permitem que os clientes tootrack alterações de saudação que estão sendo feitas objeto tooan que elas têm interesse em. Dois tipos de objetos dão suporte a notificações: *Gerenciador de Estado Confiável* e *Dicionário Confiável*.

Os motivos comuns para usar as Notificações são:

* Criando exibições, como índices secundários materializadas ou agregado exibições filtradas de estado da réplica de saudação. Um exemplo é um índice classificado de todas as chaves em um Dicionário Confiável.
* Enviados dados de monitoramento, como o número de saudação de usuários adicionados no hello última hora.

As notificações são disparadas como parte da aplicação de operações. Por disso, as notificações devem ser manipuladas tão rápido quanto possível, e eventos síncronos não devem incluir operações dispendiosas.

## <a name="reliable-state-manager-notifications"></a>Notificações do Gerenciador de Estado Confiável
Gerenciador de estado confiável oferece notificações para Olá eventos a seguir:

* Transação
  * Confirmar
* Gerenciador de estado
  * Recompilação
  * Adição de um estado confiável
  * Remoção de um estado confiável

Gerenciador de estado confiável rastreia transações atuais de inflight hello. Olá única alteração no estado de transação que faz com que um toobe notificação acionado é uma transação sendo confirmada.

O Gerenciador de Estado Confiável mantém uma coleção de estados confiáveis, como Dicionário Confiável e Fila Confiável. Gerenciador de estado confiável dispara notificações quando essa coleção é alterada: um estado confiável é adicionado ou removido, ou toda a coleção Olá é reconstruída.
Olá Gerenciador de estado confiável coleção será recriado em três casos:

* Recuperação: Quando uma réplica é iniciado, ele recupera seu estado anterior de disco hello. No final da saudação de recuperação, ele usa **NotifyStateManagerChangedEventArgs** toofire um evento que contém o conjunto de saudação de estados confiáveis recuperados.
* Cópia completa: antes de conjunto de configurações de saudação ingressar em uma réplica, ele tem toobe criado. Às vezes, isso requer uma cópia completa do estado do Gerenciador de estado confiável de saudação réplica primária toobe toohello aplicada ocioso réplica secundária. Gerenciador de estado confiável em usos de réplica secundária Olá **NotifyStateManagerChangedEventArgs** toofire um evento que contém o conjunto de saudação de estados confiáveis que adquiriu a réplica primária hello.
* Restaurar: Em cenários de recuperação de desastres, estado da réplica de saudação pode ser restaurado de um backup por meio de **RestoreAsync**. Nesses casos, usa o Gerenciador de estado confiável na réplica primária Olá **NotifyStateManagerChangedEventArgs** toofire um evento que contém Olá conjunto confiáveis de estados de que ela restaurada do backup hello.

tooregister para notificações de transação e/ou notificações de Gerenciador de estado, você precisa tooregister com hello **TransactionChanged** ou **StateManagerChanged** eventos no Gerenciador de estado confiável. Um local comum tooregister com esses manipuladores de eventos é o construtor de saudação do seu serviço com monitoração de estado. Quando você se registrar no construtor de hello, não perder qualquer notificação causado por uma alteração durante o tempo de vida de saudação do **IReliableStateManager**.

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

Olá **TransactionChanged** usa o manipulador de eventos **NotifyTransactionChangedEventArgs** tooprovide detalhes sobre o evento hello. Ele contém a propriedade de ação da saudação (por exemplo, **NotifyTransactionChangedAction.Commit**) que especifica o tipo de saudação de alteração. Ele também contém a propriedade de transação de saudação que fornece uma transação de toohello de referência que foram alteradas.

> [!NOTE]
> Hoje, **TransactionChanged** os eventos são gerados somente se Olá a transação é confirmada. Olá ação é igual muito**NotifyTransactionChangedAction.Commit**. Mas em Olá futuras, eventos podem ser gerados para outros tipos de alterações de estado de transação. É recomendável verificando ação hello e processar o evento de saudação somente se ele é aquele que você espera.
> 
> 

Veja a seguir um exemplo de manipulador de eventos **TransactionChanged** .

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

Olá **StateManagerChanged** usa o manipulador de eventos **NotifyStateManagerChangedEventArgs** tooprovide detalhes sobre o evento hello.
**NotifyStateManagerChangedEventArgs** tem duas subclasses: **NotifyStateManagerRebuildEventArgs** e **NotifyStateManagerSingleEntityChangedEventArgs**.
Você usar a propriedade de ação de saudação na **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** subclasse correto toohello:

* **NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**
* **NotifyStateManagerChangedAction.Add** e **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**

Veja a seguir um exemplo de manipulador de notificação **StateManagerChanged** .

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

## <a name="reliable-dictionary-notifications"></a>Notificações de Dicionário Confiável
Dicionário confiável oferece notificações para Olá eventos a seguir:

* Recompilar: chamada quando **ReliableDictionary** recuperou o estado de um backup ou recuperou ou copiou o estado local ou backup.
* Limpar: Chamado quando Olá estado de **ReliableDictionary** foi limpo por meio de saudação **ClearAsync** método.
* Adicione: Chamado quando um item foi adicionado muito**ReliableDictionary**.
* Update: chamado quando um item em **IReliableDictionary** tiver sido atualizado.
* Remove: chamado quando um item em **IReliableDictionary** tiver sido removido.

notificações de dicionário confiável tooget, você precisa tooregister com hello **DictionaryChanged** manipulador de eventos **IReliableDictionary**. Um local comum é tooregister com esses manipuladores de eventos em Olá **ReliableStateManager.StateManagerChanged** adicionar notificação.
Registrando quando **IReliableDictionary** é adicionado muito**IReliableStateManager** garante que as notificações não perder.

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
> **ProcessStateManagerSingleEntityNotification** é o método de exemplo hello que hello anterior **OnStateManagerChangedHandler** exemplo chama.
> 
> 

código anterior Hello define Olá **IReliableNotificationAsyncCallback** interface, juntamente com **DictionaryChanged**. Porque **NotifyDictionaryRebuildEventArgs** contém um **IAsyncEnumerable** interface – qual precisa toobe enumerado assincronamente – reconstrução notificações são disparadas por meio de  **RebuildNotificationAsyncCallback** em vez de **OnDictionaryChangedHandler**.

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
> Saudação anterior do código, como parte do processamento de notificação de recriação Olá, Olá primeiro mantidos agregadas do estado é limpo. Porque a coleção confiável Olá estiver sendo reconstruída com um novo estado, todas as notificações anteriores são irrelevantes.
> 
> 

Olá **DictionaryChanged** usa o manipulador de eventos **NotifyDictionaryChangedEventArgs** tooprovide detalhes sobre o evento hello.
**NotifyDictionaryChangedEventArgs** tem cinco subclasses. Usar a propriedade de ação Olá em **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** subclasse correto toohello:

* **NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**
* **NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**
* **NotifyDictionaryChangedAction.Add** e **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**
* **NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**
* **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**

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

## <a name="recommendations"></a>Recomendações
* *Conclua* os eventos de notificações o mais rápido possível.
* *Não* execute quaisquer operações dispendiosas (por exemplo, operações de E/S) como parte de eventos síncronos.
* *Fazer* verificar o tipo de ação de saudação antes de processar eventos hello. Novos tipos de ação podem ser adicionados em Olá futuras.

Aqui estão algumas coisas tookeep em mente:

* As notificações são disparadas como parte da execução de saudação de uma operação. Por exemplo, uma notificação de restauração é acionada como última etapa saudação de uma operação de restauração. Uma restauração não será concluído até que o evento de notificação de saudação é processado.
* Como as notificações são acionadas como parte da saudação aplicar operações, os clientes verão apenas as notificações para operações confirmadas localmente. E, como operações têm a garantia de apenas toobe confirmada localmente (em outras palavras, conectado), eles podem ou não pode ser desfeitos no hello futuras.
* No caminho de restauração hello, uma única notificação é disparada para cada operação aplicada. Isso significa que se a transação T1 inclui Create(X), Delete(X) e Create(X), você obterá uma notificação para criação de saudação de X, um para exclusão hello e um para a criação de saudação novamente, nessa ordem.
* Para transações que contêm várias operações, as operações são aplicadas na ordem de saudação em que foram recebidos na réplica primária de saudação do usuário hello.
* Como parte do processamento do progresso falso, algumas operações podem ser desfeitas. As notificações são geradas para essas operações de desfazer, reverter o estado de saudação do ponto estável do hello réplica tooa voltar. Uma diferença importante das notificações de ação de desfazer é que os eventos que têm chaves duplicadas são agregados. Por exemplo, se a transação T1 é desfeita, você verá uma única notificação tooDelete(X).

## <a name="next-steps"></a>Próximas etapas
* [Coleções Confiáveis](service-fabric-work-with-reliable-collections.md)
* [Início Rápido dos Serviços Confiáveis](service-fabric-reliable-services-quick-start.md)
* [Backup e restauração do Reliable Services (recuperação de desastre)](service-fabric-reliable-services-backup-restore.md)
* [Referência do desenvolvedor para Coleções Confiáveis](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

