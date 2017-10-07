---
title: aaaOverview do ciclo de vida baseado em ator microservices do Azure | Microsoft Docs
description: "Explica o ciclo de vida, a coleta de lixo e a exclusão manual de atores e seu estado de Reliable Actor do Service Fabric"
services: service-fabric
documentationcenter: .net
author: amanbha
manager: timlt
editor: vturecek
ms.assetid: b91384cc-804c-49d6-a6cb-f3f3d7d65a8e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: a7926e372449048f0a579c2c58573754a4a82363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a><span data-ttu-id="1c948-103">Ciclo de vida, coleta automática de lixo e exclusão manual do ator</span><span class="sxs-lookup"><span data-stu-id="1c948-103">Actor lifecycle, automatic garbage collection, and manual delete</span></span>
<span data-ttu-id="1c948-104">Um ator é ativado Olá a primeira vez que é feita uma chamada tooany de seus métodos.</span><span class="sxs-lookup"><span data-stu-id="1c948-104">An actor is activated hello first time a call is made tooany of its methods.</span></span> <span data-ttu-id="1c948-105">Um ator é desativado (lixo coletado pelo tempo de execução do hello atores) se ele não for usado por um período configurável.</span><span class="sxs-lookup"><span data-stu-id="1c948-105">An actor is deactivated (garbage collected by hello Actors runtime) if it is not used for a configurable period of time.</span></span> <span data-ttu-id="1c948-106">Um ator e seu estado também podem ser excluídos manualmente a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="1c948-106">An actor and its state can also be deleted manually at any time.</span></span>

## <a name="actor-activation"></a><span data-ttu-id="1c948-107">Ativação do ator</span><span class="sxs-lookup"><span data-stu-id="1c948-107">Actor activation</span></span>
<span data-ttu-id="1c948-108">Quando um ator é ativado, a seguir Olá ocorre:</span><span class="sxs-lookup"><span data-stu-id="1c948-108">When an actor is activated, hello following occurs:</span></span>

* <span data-ttu-id="1c948-109">Quando uma chamada chega para um ator e ele ainda não está ativo, é criado um novo ator.</span><span class="sxs-lookup"><span data-stu-id="1c948-109">When a call comes for an actor and one is not already active, a new actor is created.</span></span>
* <span data-ttu-id="1c948-110">estado de saudação do ator é carregado se ele mantém o estado.</span><span class="sxs-lookup"><span data-stu-id="1c948-110">hello actor's state is loaded if it's maintaining state.</span></span>
* <span data-ttu-id="1c948-111">Olá `OnActivateAsync` (c#) ou `onActivateAsync` método (Java) (que pode ser substituído na implementação de ator Olá) é chamado.</span><span class="sxs-lookup"><span data-stu-id="1c948-111">hello `OnActivateAsync` (C#) or `onActivateAsync` (Java) method (which can be overridden in hello actor implementation) is called.</span></span>
* <span data-ttu-id="1c948-112">ator Olá agora é considerado ativo.</span><span class="sxs-lookup"><span data-stu-id="1c948-112">hello actor is now considered active.</span></span>

## <a name="actor-deactivation"></a><span data-ttu-id="1c948-113">Desativação do ator</span><span class="sxs-lookup"><span data-stu-id="1c948-113">Actor deactivation</span></span>
<span data-ttu-id="1c948-114">Quando um ator é desativado, ocorre a seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="1c948-114">When an actor is deactivated, hello following occurs:</span></span>

* <span data-ttu-id="1c948-115">Quando um ator não é usado por um período de tempo, ele será removido da tabela de atores Active hello.</span><span class="sxs-lookup"><span data-stu-id="1c948-115">When an actor is not used for some period of time, it is removed from hello Active Actors table.</span></span>
* <span data-ttu-id="1c948-116">Olá `OnDeactivateAsync` (c#) ou `onDeactivateAsync` método (Java) (que pode ser substituído na implementação de ator Olá) é chamado.</span><span class="sxs-lookup"><span data-stu-id="1c948-116">hello `OnDeactivateAsync` (C#) or `onDeactivateAsync` (Java) method (which can be overridden in hello actor implementation) is called.</span></span> <span data-ttu-id="1c948-117">Isso limpará todos os timers de saudação de ator hello.</span><span class="sxs-lookup"><span data-stu-id="1c948-117">This clears all hello timers for hello actor.</span></span> <span data-ttu-id="1c948-118">Operações de ator, como alterações de estado, não devem ser chamadas por meio desse método.</span><span class="sxs-lookup"><span data-stu-id="1c948-118">Actor operations like state changes should not be called from this method.</span></span>

> [!TIP]
> <span data-ttu-id="1c948-119">Olá atores Fabric runtime emite alguns [eventos relacionados tooactor ativação e desativação](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="1c948-119">hello Fabric Actors runtime emits some [events related tooactor activation and deactivation](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span></span> <span data-ttu-id="1c948-120">Eles são úteis para diagnóstico e monitoramento de desempenho.</span><span class="sxs-lookup"><span data-stu-id="1c948-120">They are useful in diagnostics and performance monitoring.</span></span>
>
>

### <a name="actor-garbage-collection"></a><span data-ttu-id="1c948-121">Coleta de Lixo de Ator</span><span class="sxs-lookup"><span data-stu-id="1c948-121">Actor garbage collection</span></span>
<span data-ttu-id="1c948-122">Quando um ator é desativado, objeto de ator toohello referências são liberados e pode ser coletada como lixo normalmente por Olá common language runtime (CLR) ou o coletor de lixo do java (JVM) de VM.</span><span class="sxs-lookup"><span data-stu-id="1c948-122">When an actor is deactivated, references toohello actor object are released and it can be garbage collected normally by hello common language runtime (CLR) or java virtual machine (JVM) garbage collector.</span></span> <span data-ttu-id="1c948-123">Coleta de lixo só limpa o objeto de ator Olá; ele faz **não** remover o estado armazenado no Gerenciador de estado do ator hello.</span><span class="sxs-lookup"><span data-stu-id="1c948-123">Garbage collection only cleans up hello actor object; it does **not** remove state stored in hello actor's State Manager.</span></span> <span data-ttu-id="1c948-124">Olá próximo tempo Olá ator é ativado, um novo objeto de ator é criado e seu estado é restaurado.</span><span class="sxs-lookup"><span data-stu-id="1c948-124">hello next time hello actor is activated, a new actor object is created and its state is restored.</span></span>

<span data-ttu-id="1c948-125">O que conta como "é usada" para fins de saudação de desativação e coleta de lixo?</span><span class="sxs-lookup"><span data-stu-id="1c948-125">What counts as “being used” for hello purpose of deactivation and garbage collection?</span></span>

* <span data-ttu-id="1c948-126">Recebimento de chamadas</span><span class="sxs-lookup"><span data-stu-id="1c948-126">Receiving a call</span></span>
* <span data-ttu-id="1c948-127">`IRemindable.ReceiveReminderAsync`método que está sendo invocado (aplicável somente se o ator Olá usa lembretes)</span><span class="sxs-lookup"><span data-stu-id="1c948-127">`IRemindable.ReceiveReminderAsync` method being invoked (applicable only if hello actor uses reminders)</span></span>

> [!NOTE]
> <span data-ttu-id="1c948-128">Se o ator Olá usa temporizadores e seu retorno de chamada timer é invocado, ele não **não** contagem como "é usada".</span><span class="sxs-lookup"><span data-stu-id="1c948-128">if hello actor uses timers and its timer callback is invoked, it does **not** count as "being used".</span></span>
>
>

<span data-ttu-id="1c948-129">Antes de entrarmos em detalhes de saudação de desativação, é importante toodefine Olá termos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c948-129">Before we go into hello details of deactivation, it is important toodefine hello following terms:</span></span>

* <span data-ttu-id="1c948-130">*Intervalo de verificação*.</span><span class="sxs-lookup"><span data-stu-id="1c948-130">*Scan interval*.</span></span> <span data-ttu-id="1c948-131">Esse é o intervalo de saudação no qual Olá atores em tempo de execução verifica sua tabela de atores Active atores que podem ser desativados e coletado como lixo.</span><span class="sxs-lookup"><span data-stu-id="1c948-131">This is hello interval at which hello Actors runtime scans its Active Actors table for actors that can be deactivated and garbage collected.</span></span> <span data-ttu-id="1c948-132">valor padrão de saudação para isso é 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="1c948-132">hello default value for this is 1 minute.</span></span>
* <span data-ttu-id="1c948-133">*Tempo limite de ociosidade*.</span><span class="sxs-lookup"><span data-stu-id="1c948-133">*Idle timeout*.</span></span> <span data-ttu-id="1c948-134">Isso é Olá tempo que um ator precisa tooremain não utilizados (ocioso) antes que ele pode ser desativado e coletado como lixo.</span><span class="sxs-lookup"><span data-stu-id="1c948-134">This is hello amount of time that an actor needs tooremain unused (idle) before it can be deactivated and garbage collected.</span></span> <span data-ttu-id="1c948-135">valor padrão de saudação para isso é 60 minutos.</span><span class="sxs-lookup"><span data-stu-id="1c948-135">hello default value for this is 60 minutes.</span></span>

<span data-ttu-id="1c948-136">Normalmente, não é necessário toochange esses padrões.</span><span class="sxs-lookup"><span data-stu-id="1c948-136">Typically, you do not need toochange these defaults.</span></span> <span data-ttu-id="1c948-137">No entanto, se necessário, esses intervalos podem ser alterados por meio de `ActorServiceSettings` ao registrar seu [Serviço de Ator](service-fabric-reliable-actors-platform.md):</span><span class="sxs-lookup"><span data-stu-id="1c948-137">However, if necessary, these intervals can be changed through `ActorServiceSettings` when registering your [Actor Service](service-fabric-reliable-actors-platform.md):</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        ActorRuntime.RegisterActorAsync<MyActor>((context, actorType) =>
                new ActorService(context, actorType,
                    settings:
                        new ActorServiceSettings()
                        {
                            ActorGarbageCollectionSettings =
                                new ActorGarbageCollectionSettings(10, 2)
                        }))
            .GetAwaiter()
            .GetResult();
    }
}
```

```Java
public class Program
{
    public static void main(String[] args)
    {
        ActorRuntime.registerActorAsync(
                MyActor.class,
                (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
                timeout);
    }
}
```
<span data-ttu-id="1c948-138">Para cada ativo ator, tempo de execução de ator Olá controla de Olá período de tempo que ele ficar ocioso (ou seja, não usado).</span><span class="sxs-lookup"><span data-stu-id="1c948-138">For each active actor, hello actor runtime keeps track of hello amount of time that it has been idle (i.e. not used).</span></span> <span data-ttu-id="1c948-139">tempo de execução de ator Olá verifica cada atores Olá cada `ScanIntervalInSeconds` toosee se ele puder ser lixo coletado e coleta-lo se ele estiver inativo por `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="1c948-139">hello actor runtime checks each of hello actors every `ScanIntervalInSeconds` toosee if it can be garbage collected and collects it if it has been idle for `IdleTimeoutInSeconds`.</span></span>

<span data-ttu-id="1c948-140">Sempre que um ator é usado, o tempo ocioso é too0 de redefinição.</span><span class="sxs-lookup"><span data-stu-id="1c948-140">Anytime an actor is used, its idle time is reset too0.</span></span> <span data-ttu-id="1c948-141">Depois disso, ator Olá pode ser limpos somente se ele permanecerá ocioso novamente `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="1c948-141">After this, hello actor can be garbage collected only if it again remains idle for `IdleTimeoutInSeconds`.</span></span> <span data-ttu-id="1c948-142">Lembre-se de que um ator é considerado toohave foi usado se um método de interface de ator ou um retorno de chamada de lembrete de ator é executado.</span><span class="sxs-lookup"><span data-stu-id="1c948-142">Recall that an actor is considered toohave been used if either an actor interface method or an actor reminder callback is executed.</span></span> <span data-ttu-id="1c948-143">Um ator é **não** considerado toohave foi usado se seu retorno de chamada timer é executado.</span><span class="sxs-lookup"><span data-stu-id="1c948-143">An actor is **not** considered toohave been used if its timer callback is executed.</span></span>

<span data-ttu-id="1c948-144">Olá diagrama a seguir mostra Olá ciclo de vida de um único ator tooillustrate esses conceitos.</span><span class="sxs-lookup"><span data-stu-id="1c948-144">hello following diagram shows hello lifecycle of a single actor tooillustrate these concepts.</span></span>

![Exemplo de tempo ocioso][1]

<span data-ttu-id="1c948-146">exemplo Hello mostra o impacto de saudação de chamadas de método de ator, lembretes e temporizadores no tempo de vida de saudação deste ator.</span><span class="sxs-lookup"><span data-stu-id="1c948-146">hello example shows hello impact of actor method calls, reminders, and timers on hello lifetime of this actor.</span></span> <span data-ttu-id="1c948-147">Olá seguintes pontos sobre o exemplo hello é vale a pena mencionar:</span><span class="sxs-lookup"><span data-stu-id="1c948-147">hello following points about hello example are worth mentioning:</span></span>

* <span data-ttu-id="1c948-148">ScanInterval e IdleTimeout são definidos too5 e 10 respectivamente.</span><span class="sxs-lookup"><span data-stu-id="1c948-148">ScanInterval and IdleTimeout are set too5 and 10 respectively.</span></span> <span data-ttu-id="1c948-149">(Unidades não importa aqui, desde que o nosso objetivo é o conceito de saudação de tooillustrate somente.)</span><span class="sxs-lookup"><span data-stu-id="1c948-149">(Units do not matter here, since our purpose is only tooillustrate hello concept.)</span></span>
* <span data-ttu-id="1c948-150">verificação de saudação para atores coletado como lixo toobe acontece em T = 0, 5, 10, 15, 20, 25, conforme definido pelo intervalo de verificação de saudação de 5.</span><span class="sxs-lookup"><span data-stu-id="1c948-150">hello scan for actors toobe garbage collected happens at T=0,5,10,15,20,25, as defined by hello scan interval of 5.</span></span>
* <span data-ttu-id="1c948-151">Um medidor de tempo periódico é acionado em T = 4, 8, 12, 16, 20, 24 e executa seu retorno de chamada.</span><span class="sxs-lookup"><span data-stu-id="1c948-151">A periodic timer fires at T=4,8,12,16,20,24, and its callback executes.</span></span> <span data-ttu-id="1c948-152">Ele não afeta o tempo ocioso de saudação do ator hello.</span><span class="sxs-lookup"><span data-stu-id="1c948-152">It does not impact hello idle time of hello actor.</span></span>
* <span data-ttu-id="1c948-153">Uma chamada de método de ator em T = 7 redefine Olá tempo ocioso too0 e adia a coleta de lixo de saudação do ator hello.</span><span class="sxs-lookup"><span data-stu-id="1c948-153">An actor method call at T=7 resets hello idle time too0 and delays hello garbage collection of hello actor.</span></span>
* <span data-ttu-id="1c948-154">Executa um retorno de chamada de lembrete de ator em T = 14 e mais atrasos Olá coleta de lixo de ator hello.</span><span class="sxs-lookup"><span data-stu-id="1c948-154">An actor reminder callback executes at T=14 and further delays hello garbage collection of hello actor.</span></span>
* <span data-ttu-id="1c948-155">Durante a verificação de coleta de lixo Olá T = 25, tempo ocioso do ator Olá finalmente excede o tempo limite de ociosidade de saudação de 10 e ator Olá é coletado como lixo.</span><span class="sxs-lookup"><span data-stu-id="1c948-155">During hello garbage collection scan at T=25, hello actor's idle time finally exceeds hello idle timeout of 10, and hello actor is garbage collected.</span></span>

<span data-ttu-id="1c948-156">Um ator nunca terá o lixo coletado durante a execução de um de seus métodos, não importa quanto tempo seja gasto na execução do método.</span><span class="sxs-lookup"><span data-stu-id="1c948-156">An actor will never be garbage collected while it is executing one of its methods, no matter how much time is spent in executing that method.</span></span> <span data-ttu-id="1c948-157">Como mencionado anteriormente, execução de saudação de métodos de interface de ator e retornos de chamada de lembrete impede que a coleta de lixo redefinindo too0 de tempo ocioso do ator hello.</span><span class="sxs-lookup"><span data-stu-id="1c948-157">As mentioned earlier, hello execution of actor interface methods and reminder callbacks prevents garbage collection by resetting hello actor's idle time too0.</span></span> <span data-ttu-id="1c948-158">execução de saudação de retornos de chamada timer não redefine Olá too0 de tempo ocioso.</span><span class="sxs-lookup"><span data-stu-id="1c948-158">hello execution of timer callbacks does not reset hello idle time too0.</span></span> <span data-ttu-id="1c948-159">No entanto, coleta de lixo de saudação do ator Olá é adiada até que a chamada de timer Olá concluiu a execução.</span><span class="sxs-lookup"><span data-stu-id="1c948-159">However, hello garbage collection of hello actor is deferred until hello timer callback has completed execution.</span></span>

## <a name="deleting-actors-and-their-state"></a><span data-ttu-id="1c948-160">Excluindo atores e seu estado</span><span class="sxs-lookup"><span data-stu-id="1c948-160">Deleting actors and their state</span></span>
<span data-ttu-id="1c948-161">Coleta de lixo de atores desativados só limpa o objeto de ator hello, mas não remove os dados armazenados no Gerenciador de estado de um ator.</span><span class="sxs-lookup"><span data-stu-id="1c948-161">Garbage collection of deactivated actors only cleans up hello actor object, but it does not remove data that is stored in an actor's State Manager.</span></span> <span data-ttu-id="1c948-162">Quando um ator é reativado, os dados novamente são feitos tooit disponível por meio do Gerenciador de estado de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c948-162">When an actor is re-activated, its data is again made available tooit through hello State Manager.</span></span> <span data-ttu-id="1c948-163">Em casos onde atores armazenar dados no Gerenciador de estado e são desativados, mas nunca ativados novamente, pode ser necessário tooclean backup de seus dados.</span><span class="sxs-lookup"><span data-stu-id="1c948-163">In cases where actors store data in State Manager and are deactivated but never re-activated, it may be necessary tooclean up their data.</span></span>

<span data-ttu-id="1c948-164">Olá [serviço de ator](service-fabric-reliable-actors-platform.md) fornece uma função para excluir os atores de um chamador remoto:</span><span class="sxs-lookup"><span data-stu-id="1c948-164">hello [Actor Service](service-fabric-reliable-actors-platform.md) provides a function for deleting actors from a remote caller:</span></span>

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

<span data-ttu-id="1c948-165">Excluir um ator tem Olá efeitos dependendo se ou não está ativo no momento ator Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c948-165">Deleting an actor has hello following effects depending on whether or not hello actor is currently active:</span></span>

* <span data-ttu-id="1c948-166">**Ator ativo**</span><span class="sxs-lookup"><span data-stu-id="1c948-166">**Active Actor**</span></span>
  * <span data-ttu-id="1c948-167">O ator é removido da lista de atores ativos e é desativado.</span><span class="sxs-lookup"><span data-stu-id="1c948-167">Actor is removed from active actors list and is deactivated.</span></span>
  * <span data-ttu-id="1c948-168">Seu estado é excluído permanentemente.</span><span class="sxs-lookup"><span data-stu-id="1c948-168">Its state is deleted permanently.</span></span>
* <span data-ttu-id="1c948-169">**Ator inativo**</span><span class="sxs-lookup"><span data-stu-id="1c948-169">**Inactive Actor**</span></span>
  * <span data-ttu-id="1c948-170">Seu estado é excluído permanentemente.</span><span class="sxs-lookup"><span data-stu-id="1c948-170">Its state is deleted permanently.</span></span>

<span data-ttu-id="1c948-171">Observe que não é possível chamar um ator excluir no próprio de um dos seus métodos de ator porque não é possível excluir o ator Olá ao ser executado em um contexto de chamada de ator, no qual Olá runtime obteve um bloqueio em torno de acesso de thread único tooenforce chamada ator hello.</span><span class="sxs-lookup"><span data-stu-id="1c948-171">Note that an actor cannot call delete on itself from one of its actor methods because hello actor cannot be deleted while executing within an actor call context, in which hello runtime has obtained a lock around hello actor call tooenforce single-threaded access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c948-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1c948-172">Next steps</span></span>
* [<span data-ttu-id="1c948-173">Lembretes e temporizadores de ator</span><span class="sxs-lookup"><span data-stu-id="1c948-173">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="1c948-174">Eventos de ator</span><span class="sxs-lookup"><span data-stu-id="1c948-174">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="1c948-175">Reentrância de ator</span><span class="sxs-lookup"><span data-stu-id="1c948-175">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="1c948-176">Diagnóstico e monitoramento de desempenho do ator</span><span class="sxs-lookup"><span data-stu-id="1c948-176">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="1c948-177">Documentação de referência da API do Ator</span><span class="sxs-lookup"><span data-stu-id="1c948-177">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="1c948-178">Código de exemplo C#</span><span class="sxs-lookup"><span data-stu-id="1c948-178">C# Sample code</span></span>](https://github.com/Azure/servicefabric-samples)
* [<span data-ttu-id="1c948-179">Código de exemplo Java</span><span class="sxs-lookup"><span data-stu-id="1c948-179">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
