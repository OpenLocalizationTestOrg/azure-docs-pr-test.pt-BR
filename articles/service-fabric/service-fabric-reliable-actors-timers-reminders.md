---
title: aaaReliable atores temporizadores e lembretes | Microsoft Docs
description: "Introdução tootimers e lembretes para atores confiável do serviço de malha."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 00c48716-569e-4a64-bd6c-25234c85ff4f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c5116ec1923014e131130b9f4e86dd1e133bbf7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="actor-timers-and-reminders"></a>Lembretes e temporizadores de ator
Os atores podem agendar o trabalho periódico neles mesmos ao registrarem temporizadores ou lembretes. Este artigo mostra como toouse temporizadores e lembretes e explica as diferenças de saudação entre elas.

## <a name="actor-timers"></a>Temporizadores de ator
Timers de ator fornecem um wrapper simple em torno de um tooensure de timer .NET ou Java, métodos de retorno de chamada hello respeitam as garantias de simultaneidade baseada em vez de saudação que Olá atores tempo de execução fornece.

Atores podem usar Olá `RegisterTimer`(c#) ou `registerTimer`(Java) e `UnregisterTimer`(c#) ou `unregisterTimer`métodos (Java) em sua base de classe tooregister e cancelar o registro de seus temporizadores. exemplo Hello abaixo mostra o uso de saudação de APIs do timer. Olá APIs são muito semelhante timer de .NET toohello ou timer de Java. Neste exemplo, quando o timer de saudação está vencido, tempo de execução de atores Olá chamará Olá `MoveObject`(c#) ou `moveObject`método (Java). método Hello é garantido simultaneidade baseada em vez do toorespect hello. Isso significa que nenhum outro método de ator ou retornos de chamada de temporizador/lembrete estará em andamento até que a execução desse retorno de chamada seja concluída.

```csharp
class VisualObjectActor : Actor, IVisualObject
{
    private IActorTimer _updateTimer;

    public VisualObjectActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    protected override Task OnActivateAsync()
    {
        ...

        _updateTimer = RegisterTimer(
            MoveObject,                     // Callback method
            null,                           // Parameter toopass toohello callback method
            TimeSpan.FromMilliseconds(15),  // Amount of time toodelay before hello callback is invoked
            TimeSpan.FromMilliseconds(15)); // Time interval between invocations of hello callback method

        return base.OnActivateAsync();
    }

    protected override Task OnDeactivateAsync()
    {
        if (_updateTimer != null)
        {
            UnregisterTimer(_updateTimer);
        }

        return base.OnDeactivateAsync();
    }

    private Task MoveObject(object state)
    {
        ...
        return Task.FromResult(true);
    }
}
```
```Java
public class VisualObjectActorImpl extends FabricActor implements VisualObjectActor
{
    private ActorTimer updateTimer;

    public VisualObjectActorImpl(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    @Override
    protected CompletableFuture onActivateAsync()
    {
        ...

        return this.stateManager()
                .getOrAddStateAsync(
                        stateName,
                        VisualObject.createRandom(
                                this.getId().toString(),
                                new Random(this.getId().toString().hashCode())))
                .thenApply((r) -> {
                    this.registerTimer(
                            (o) -> this.moveObject(o),                        // Callback method
                            "moveObject",
                            null,                                             // Parameter toopass toohello callback method
                            Duration.ofMillis(10),                            // Amount of time toodelay before hello callback is invoked
                            Duration.ofMillis(timerIntervalInMilliSeconds));  // Time interval between invocations of hello callback method
                    return null;
                });
    }

    @Override
    protected CompletableFuture onDeactivateAsync()
    {
        if (updateTimer != null)
        {
            unregisterTimer(updateTimer);
        }

        return super.onDeactivateAsync();
    }

    private CompletableFuture moveObject(Object state)
    {
        ...
        return this.stateManager().getStateAsync(this.stateName).thenCompose(v -> {
            VisualObject v1 = (VisualObject)v;
            v1.move();
            return (CompletableFuture<?>)this.stateManager().setStateAsync(stateName, v1).
                    thenApply(r -> {
                      ...
                      return null;});
        });
    }
}
```

Olá próximo período do temporizador de saudação é iniciado após a conclusão de retorno de chamada hello execução. Isso implica que timer Olá for interrompido enquanto o retorno de chamada hello está em execução e é iniciado quando termina de retorno de chamada de saudação.

tempo de execução de atores Olá salva as alterações feitas Gerenciador do ator toohello de estado quando termina de retorno de chamada de saudação. Se ocorrer um erro ao salvar estado hello, esse objeto de ator será desativado e uma nova instância será ativada.

Todos os timers são interrompidos quando ator hello está desativado como parte da coleta de lixo. Nenhum retorno de chamada de temporizador é chamado depois disso. Além disso, o tempo de execução do hello atores não mantém todas as informações sobre temporizadores Olá que estavam em execução antes da desativação. É o toohello ator tooregister qualquer timers que ele precisa quando ele é reativado Olá futuras. Para obter mais informações, consulte a seção Olá em [coleta de lixo de ator](service-fabric-reliable-actors-lifecycle.md).

## <a name="actor-reminders"></a>Lembretes de ator
Lembretes são um mecanismo tootrigger persistentes retornos de chamada em um ator em horários específicos. Sua funcionalidade é semelhante tootimers. Mas, ao contrário de temporizadores, lembretes são disparados em todas as circunstâncias até ator Olá explicitamente cancela o registro-los ou ator Olá explicitamente é excluído. Especificamente, lembretes são disparados em failovers e desativações de ator porque o tempo de execução de atores Olá persiste nas informações sobre lembretes Olá ator.

tooregister um lembrete, um ator chama Olá `RegisterReminderAsync` fornecido na classe base do hello, conforme mostrado no exemplo a seguir de saudação do método:

```csharp
protected override async Task OnActivateAsync()
{
    string reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    IActorReminder reminderRegistration = await this.RegisterReminderAsync(
        reminderName,
        BitConverter.GetBytes(amountInDollars),
        TimeSpan.FromDays(3),
        TimeSpan.FromDays(1));
}
```

```Java
@Override
protected CompletableFuture onActivateAsync()
{
    String reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    ActorReminder reminderRegistration = this.registerReminderAsync(
            reminderName,
            state,
            dueTime,    //hello amount of time toodelay before firing hello reminder
            period);    //hello time interval between firing of reminders
}
```

Neste exemplo, `"Pay cell phone bill"` é o nome de lembrete hello. Isso é uma cadeia de caracteres hello ator usa toouniquely identificar um lembrete. `BitConverter.GetBytes(amountInDollars)`(C#) é o contexto de saudação que está associado com o lembrete de saudação. Ela será transmitida toohello back ator como um retorno de chamada de lembrete toohello argumento, ou seja, `IRemindable.ReceiveReminderAsync`(c#) ou `Remindable.receiveReminderAsync`(Java).

Atores que usam lembretes devem implementar Olá `IRemindable` interface, conforme mostrado no exemplo hello abaixo.

```csharp
public class ToDoListActor : Actor, IToDoListActor, IRemindable
{
    public ToDoListActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task ReceiveReminderAsync(string reminderName, byte[] context, TimeSpan dueTime, TimeSpan period)
    {
        if (reminderName.Equals("Pay cell phone bill"))
        {
            int amountToPay = BitConverter.ToInt32(context, 0);
            System.Console.WriteLine("Please pay your cell phone bill of ${0}!", amountToPay);
        }
        return Task.FromResult(true);
    }
}
```
```Java
public class ToDoListActorImpl extends FabricActor implements ToDoListActor, Remindable
{
    public ToDoListActor(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture receiveReminderAsync(String reminderName, byte[] context, Duration dueTime, Duration period)
    {
        if (reminderName.equals("Pay cell phone bill"))
        {
            int amountToPay = ByteBuffer.wrap(context).getInt();
            System.out.println("Please pay your cell phone bill of " + amountToPay);
        }
        return CompletableFuture.completedFuture(true);
    }

```

Quando um lembrete é disparado, o tempo de execução do hello Reliable Actors invocará Olá `ReceiveReminderAsync`(c#) ou `receiveReminderAsync`método hello ator (Java). Um ator pode registrar vários lembretes e Olá `ReceiveReminderAsync`(c#) ou `receiveReminderAsync`(Java) método é invocado quando qualquer esses lembretes é disparado. ator Olá pode usar o nome de lembrete de saudação que é passada toohello `ReceiveReminderAsync`(c#) ou `receiveReminderAsync`(Java) método toofigure quais lembrete foi acionado.

tempo de execução de atores Hello salva de estado do ator hello quando hello `ReceiveReminderAsync`(c#) ou `receiveReminderAsync`(Java) chamada é concluída. Se ocorrer um erro ao salvar estado hello, esse objeto de ator será desativado e uma nova instância será ativada.

toounregister um lembrete, um ator chama Olá `UnregisterReminderAsync`(c#) ou `unregisterReminderAsync`método (Java), conforme mostrado nos exemplos de saudação abaixo.

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

Como mostrado acima, Olá `UnregisterReminderAsync`(c#) ou `unregisterReminderAsync`(Java) método aceita um `IActorReminder`(c#) ou `ActorReminder`interface (Java). Olá dá suporte a classe base de ator um `GetReminder`(c#) ou `getReminder`método (Java) que pode ser usado tooretrieve Olá `IActorReminder`(c#) ou `ActorReminder`interface (Java), passando em nome de lembrete hello. Isso é conveniente porque ator Olá não precisa Olá toopersist `IActorReminder`(c#) ou `ActorReminder`interface (Java) que foi retornada da saudação `RegisterReminder`(c#) ou `registerReminder`chamada de método (Java).

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre reentrada e eventos de Ator Confiável:
* [Eventos de ator](service-fabric-reliable-actors-events.md)
* [Reentrância de ator](service-fabric-reliable-actors-reentrancy.md)
