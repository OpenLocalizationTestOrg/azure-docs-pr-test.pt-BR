---
title: Temporizadores e lembretes de Reliable Actors | Microsoft Docs
description: "Introdução a temporizadores e lembretes para Reliable Actors do Service Fabric."
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
ms.openlocfilehash: 06b026ce06e0f16a77ac238de0af2263f272933c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="actor-timers-and-reminders"></a><span data-ttu-id="6ead1-103">Lembretes e temporizadores de ator</span><span class="sxs-lookup"><span data-stu-id="6ead1-103">Actor timers and reminders</span></span>
<span data-ttu-id="6ead1-104">Os atores podem agendar o trabalho periódico neles mesmos ao registrarem temporizadores ou lembretes.</span><span class="sxs-lookup"><span data-stu-id="6ead1-104">Actors can schedule periodic work on themselves by registering either timers or reminders.</span></span> <span data-ttu-id="6ead1-105">Este artigo mostra como usar temporizadores e lembretes e explica as diferenças entre eles.</span><span class="sxs-lookup"><span data-stu-id="6ead1-105">This article shows how to use timers and reminders and explains the differences between them.</span></span>

## <a name="actor-timers"></a><span data-ttu-id="6ead1-106">Temporizadores de ator</span><span class="sxs-lookup"><span data-stu-id="6ead1-106">Actor timers</span></span>
<span data-ttu-id="6ead1-107">Os temporizadores de ator oferecem um wrapper simples em torno de um temporizador Java ou .NET para garantir que os métodos de retorno de chamada respeitem as garantias de simultaneidade baseada em turnos fornecidas pelo tempo de execução dos Atores.</span><span class="sxs-lookup"><span data-stu-id="6ead1-107">Actor timers provide a simple wrapper around a .NET or Java timer to ensure that the callback methods respect the turn-based concurrency guarantees that the Actors runtime provides.</span></span>

<span data-ttu-id="6ead1-108">Os atores podem usar os métodos `RegisterTimer`(C#) ou `registerTimer`(Java) e `UnregisterTimer`(C#) ou `unregisterTimer`(Java) em sua classe base para registrar e cancelar o registro de seus temporizadores.</span><span class="sxs-lookup"><span data-stu-id="6ead1-108">Actors can use the `RegisterTimer`(C#) or `registerTimer`(Java)  and `UnregisterTimer`(C#) or `unregisterTimer`(Java) methods on their base class to register and unregister their timers.</span></span> <span data-ttu-id="6ead1-109">O exemplo a seguir mostra o uso de APIs de temorizador.</span><span class="sxs-lookup"><span data-stu-id="6ead1-109">The example below shows the use of timer APIs.</span></span> <span data-ttu-id="6ead1-110">As APIs são muito semelhantes ao temporizador do .NET ou do Java.</span><span class="sxs-lookup"><span data-stu-id="6ead1-110">The APIs are very similar to the .NET timer or Java timer.</span></span> <span data-ttu-id="6ead1-111">Neste exemplo, quando o temporizador chega ao fim, o tempo de execução dos Atores chamará o método `MoveObject`(C#) ou `moveObject`(Java).</span><span class="sxs-lookup"><span data-stu-id="6ead1-111">In this example, when the timer is due, the Actors runtime will call the `MoveObject`(C#) or `moveObject`(Java) method.</span></span> <span data-ttu-id="6ead1-112">É garantido que o método respeitará a simultaneidade baseada em turnos.</span><span class="sxs-lookup"><span data-stu-id="6ead1-112">The method is guaranteed to respect the turn-based concurrency.</span></span> <span data-ttu-id="6ead1-113">Isso significa que nenhum outro método de ator ou retornos de chamada de temporizador/lembrete estará em andamento até que a execução desse retorno de chamada seja concluída.</span><span class="sxs-lookup"><span data-stu-id="6ead1-113">This means that no other actor methods or timer/reminder callbacks will be in progress until this callback completes execution.</span></span>

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
            null,                           // Parameter to pass to the callback method
            TimeSpan.FromMilliseconds(15),  // Amount of time to delay before the callback is invoked
            TimeSpan.FromMilliseconds(15)); // Time interval between invocations of the callback method

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
                            null,                                             // Parameter to pass to the callback method
                            Duration.ofMillis(10),                            // Amount of time to delay before the callback is invoked
                            Duration.ofMillis(timerIntervalInMilliSeconds));  // Time interval between invocations of the callback method
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

<span data-ttu-id="6ead1-114">O período seguinte do temporizador é iniciado depois que o retorno de chamada concluir a execução.</span><span class="sxs-lookup"><span data-stu-id="6ead1-114">The next period of the timer starts after the callback completes execution.</span></span> <span data-ttu-id="6ead1-115">Isso significa que o temporizador será interrompido enquanto o retorno de chamada estiver em execução será iniciado quando o retorno de chamada for concluído.</span><span class="sxs-lookup"><span data-stu-id="6ead1-115">This implies that the timer is stopped while the callback is executing and is started when the callback finishes.</span></span>

<span data-ttu-id="6ead1-116">O tempo de execução dos Atores salva as alterações feitas ao Gerenciador de Estado do ator quando o retorno de chamada é concluído.</span><span class="sxs-lookup"><span data-stu-id="6ead1-116">The Actors runtime saves changes made to the actor's State Manager when the callback finishes.</span></span> <span data-ttu-id="6ead1-117">Se ocorrer um erro ao salvar o estado, esse objeto de ator será desativado e uma nova instância será ativada.</span><span class="sxs-lookup"><span data-stu-id="6ead1-117">If an error occurs in saving the state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="6ead1-118">Todos os temporizadores são interrompidos quando o ator é desativado como parte da coleta de lixo.</span><span class="sxs-lookup"><span data-stu-id="6ead1-118">All timers are stopped when the actor is deactivated as part of garbage collection.</span></span> <span data-ttu-id="6ead1-119">Nenhum retorno de chamada de temporizador é chamado depois disso.</span><span class="sxs-lookup"><span data-stu-id="6ead1-119">No timer callbacks are invoked after that.</span></span> <span data-ttu-id="6ead1-120">Além disso, o tempo de execução de atores não retém todas as informações sobre os temporizadores que estavam em execução antes de desativação.</span><span class="sxs-lookup"><span data-stu-id="6ead1-120">Also, the Actors runtime does not retain any information about the timers that were running before deactivation.</span></span> <span data-ttu-id="6ead1-121">Cabe ao ator registrar todos os temporizadores necessários quando ele for reativado no futuro.</span><span class="sxs-lookup"><span data-stu-id="6ead1-121">It is up to the actor to register any timers that it needs when it is reactivated in the future.</span></span> <span data-ttu-id="6ead1-122">Para obter mais informações, consulte a seção sobre [coleta de lixo de ator](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="6ead1-122">For more information, see the section on [actor garbage collection](service-fabric-reliable-actors-lifecycle.md).</span></span>

## <a name="actor-reminders"></a><span data-ttu-id="6ead1-123">Lembretes de ator</span><span class="sxs-lookup"><span data-stu-id="6ead1-123">Actor reminders</span></span>
<span data-ttu-id="6ead1-124">Os lembretes são um mecanismo para disparar chamadas de retorno persistentes em um ator em horários específicos.</span><span class="sxs-lookup"><span data-stu-id="6ead1-124">Reminders are a mechanism to trigger persistent callbacks on an actor at specified times.</span></span> <span data-ttu-id="6ead1-125">Sua funcionalidade é semelhante à dos temporizadores.</span><span class="sxs-lookup"><span data-stu-id="6ead1-125">Their functionality is similar to timers.</span></span> <span data-ttu-id="6ead1-126">Mas, ao contrário dos temporizadores, os lembretes são acionados em todas as circunstâncias até que o ator cancele o registro deles explicitamente ou até que o ator seja explicitamente excluído.</span><span class="sxs-lookup"><span data-stu-id="6ead1-126">But unlike timers, reminders are triggered under all circumstances until the actor explicitly unregisters them or the actor is explicitly deleted.</span></span> <span data-ttu-id="6ead1-127">Especificamente, os lembretes são acionados em todas as desativações e failovers ator porque o tempo de execução de atores retém as informações sobre os lembretes do ator.</span><span class="sxs-lookup"><span data-stu-id="6ead1-127">Specifically, reminders are triggered across actor deactivations and failovers because the Actors runtime persists information about the actor's reminders.</span></span>

<span data-ttu-id="6ead1-128">Para registrar um lembrete, um ator chama o método `RegisterReminderAsync` fornecido na classe base, como mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ead1-128">To register a reminder, an actor calls the `RegisterReminderAsync` method provided on the base class, as shown in the following example:</span></span>

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
            dueTime,    //The amount of time to delay before firing the reminder
            period);    //The time interval between firing of reminders
}
```

<span data-ttu-id="6ead1-129">Neste exemplo, `"Pay cell phone bill"` é o nome do lembrete.</span><span class="sxs-lookup"><span data-stu-id="6ead1-129">In this example, `"Pay cell phone bill"` is the reminder name.</span></span> <span data-ttu-id="6ead1-130">Essa é uma cadeia de caracteres usada pelo ator para identificar exclusivamente um lembrete.</span><span class="sxs-lookup"><span data-stu-id="6ead1-130">This is a string that the actor uses to uniquely identify a reminder.</span></span> <span data-ttu-id="6ead1-131">`BitConverter.GetBytes(amountInDollars)`(C#) é o contexto que está associado ao lembrete.</span><span class="sxs-lookup"><span data-stu-id="6ead1-131">`BitConverter.GetBytes(amountInDollars)`(C#) is the context that is associated with the reminder.</span></span> <span data-ttu-id="6ead1-132">Ele será devolvido para o ator como um argumento para o retorno de chamada do lembrete, ou seja, `IRemindable.ReceiveReminderAsync`(C#) ou `Remindable.receiveReminderAsync`(Java).</span><span class="sxs-lookup"><span data-stu-id="6ead1-132">It will be passed back to the actor as an argument to the reminder callback, i.e. `IRemindable.ReceiveReminderAsync`(C#) or `Remindable.receiveReminderAsync`(Java).</span></span>

<span data-ttu-id="6ead1-133">Os atores que usam lembretes devem implementar a interface `IRemindable` como mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="6ead1-133">Actors that use reminders must implement the `IRemindable` interface, as shown in the example below.</span></span>

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

<span data-ttu-id="6ead1-134">Quando um lembrete é disparado, o tempo de execução dos Reliable Actors invoca o método `ReceiveReminderAsync`(C#) ou `receiveReminderAsync`(Java) no Ator.</span><span class="sxs-lookup"><span data-stu-id="6ead1-134">When a reminder is triggered, the Reliable Actors runtime will invoke the  `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method on the Actor.</span></span> <span data-ttu-id="6ead1-135">Um ator pode registrar vários lembretes, que o método `ReceiveReminderAsync`(C#) ou `receiveReminderAsync`(Java) será chamado quando qualquer um desses lembretes for disparado.</span><span class="sxs-lookup"><span data-stu-id="6ead1-135">An actor can register multiple reminders, and the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method is invoked when any of those reminders is triggered.</span></span> <span data-ttu-id="6ead1-136">O ator pode usar o nome de lembrete que é passado para o método `ReceiveReminderAsync`(C#) ou `receiveReminderAsync`(Java) para descobrir qual lembrete foi acionado.</span><span class="sxs-lookup"><span data-stu-id="6ead1-136">The actor can use the reminder name that is passed in to the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method to figure out which reminder was triggered.</span></span>

<span data-ttu-id="6ead1-137">O tempo de execução dos Atores salva o estado do ator quando a chamada `ReceiveReminderAsync`(C#) ou `receiveReminderAsync`(Java) é concluída.</span><span class="sxs-lookup"><span data-stu-id="6ead1-137">The Actors runtime saves the actor's state when the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) call finishes.</span></span> <span data-ttu-id="6ead1-138">Se ocorrer um erro ao salvar o estado, esse objeto de ator será desativado e uma nova instância será ativada.</span><span class="sxs-lookup"><span data-stu-id="6ead1-138">If an error occurs in saving the state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="6ead1-139">Para cancelar o registro de um lembrete, um ator chama o método `UnregisterReminderAsync`(C#) ou `unregisterReminderAsync`(Java) como mostrado no exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="6ead1-139">To unregister a reminder, an actor calls the `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method, as shown in the examples below.</span></span>

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

<span data-ttu-id="6ead1-140">Como mostrado acima, o método `UnregisterReminderAsync`(C#) ou `unregisterReminderAsync`(Java) aceita uma interface `IActorReminder`(C#) ou `ActorReminder`(Java).</span><span class="sxs-lookup"><span data-stu-id="6ead1-140">As shown above, the `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method accepts an `IActorReminder`(C#) or `ActorReminder`(Java) interface.</span></span> <span data-ttu-id="6ead1-141">A classe base de ator dá suporte a um método `GetReminder`(C#) ou `getReminder`(Java), que pode ser usado para recuperar a interface `IActorReminder`(C#) ou `ActorReminder`(Java) passando-se o nome do lembrete.</span><span class="sxs-lookup"><span data-stu-id="6ead1-141">The actor base class supports a `GetReminder`(C#) or `getReminder`(Java) method that can be used to retrieve the `IActorReminder`(C#) or `ActorReminder`(Java) interface by passing in the reminder name.</span></span> <span data-ttu-id="6ead1-142">Isso é conveniente porque o ator não precisa manter a interface `IActorReminder`(C#) ou `ActorReminder`(Java) que foi retornada com a chamada do método `RegisterReminder`(C#) ou `registerReminder`(Java).</span><span class="sxs-lookup"><span data-stu-id="6ead1-142">This is convenient because the actor does not need to persist the `IActorReminder`(C#) or `ActorReminder`(Java) interface that was returned from the `RegisterReminder`(C#) or `registerReminder`(Java) method call.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ead1-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6ead1-143">Next Steps</span></span>
<span data-ttu-id="6ead1-144">Saiba mais sobre reentrada e eventos de Ator Confiável:</span><span class="sxs-lookup"><span data-stu-id="6ead1-144">Learn about Reliable Actor events and reentrancy:</span></span>
* [<span data-ttu-id="6ead1-145">Eventos de ator</span><span class="sxs-lookup"><span data-stu-id="6ead1-145">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="6ead1-146">Reentrância de ator</span><span class="sxs-lookup"><span data-stu-id="6ead1-146">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
