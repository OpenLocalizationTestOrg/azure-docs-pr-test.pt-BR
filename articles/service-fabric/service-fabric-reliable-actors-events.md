---
title: aaaEvents em microservices do Azure baseado em ator | Microsoft Docs
description: "Introdução tooevents para atores confiável do serviço de malha."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: aa01b0f7-8f88-403a-bfe1-5aba00312c24
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: a51e41c35441a5fea508138968b36a35f0ba6699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="actor-events"></a><span data-ttu-id="74b62-103">Eventos de ator</span><span class="sxs-lookup"><span data-stu-id="74b62-103">Actor events</span></span>
<span data-ttu-id="74b62-104">Os eventos de ator fornecem notificações de melhor esforço de toosend uma maneira de clientes do hello ator toohello.</span><span class="sxs-lookup"><span data-stu-id="74b62-104">Actor events provide a way toosend best-effort notifications from hello actor toohello clients.</span></span> <span data-ttu-id="74b62-105">Os eventos de ator foram desenvolvidos para comunicação entre ator e cliente e não devem ser usados para comunicação entre ator e ator.</span><span class="sxs-lookup"><span data-stu-id="74b62-105">Actor events are designed for actor-to-client communication and should not be used for actor-to-actor communication.</span></span>

<span data-ttu-id="74b62-106">saudação de código a seguir trechos de código mostram como eventos de ator toouse em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74b62-106">hello following code snippets show how toouse actor events in your application.</span></span>

<span data-ttu-id="74b62-107">Defina uma interface que descreve eventos de saudação publicados pelo ator hello.</span><span class="sxs-lookup"><span data-stu-id="74b62-107">Define an interface that describes hello events published by hello actor.</span></span> <span data-ttu-id="74b62-108">Esta interface deve ser derivada de saudação `IActorEvents` interface.</span><span class="sxs-lookup"><span data-stu-id="74b62-108">This interface must be derived from hello `IActorEvents` interface.</span></span> <span data-ttu-id="74b62-109">Olá argumentos de métodos Olá devem ser [de contrato de dados serializáveis](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="74b62-109">hello arguments of hello methods must be [data contract serializable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span> <span data-ttu-id="74b62-110">métodos de saudação devem retornar void, como eventos notificações são uma maneira e melhor esforço.</span><span class="sxs-lookup"><span data-stu-id="74b62-110">hello methods must return void, as event notifications are one way and best effort.</span></span>

```csharp
public interface IGameEvents : IActorEvents
{
    void GameScoreUpdated(Guid gameId, string currentScore);
}
```
```Java
public interface GameEvents implements ActorEvents
{
    void gameScoreUpdated(UUID gameId, String currentScore);
}
```
<span data-ttu-id="74b62-111">Declare eventos Olá publicados por ator Olá na interface de ator hello.</span><span class="sxs-lookup"><span data-stu-id="74b62-111">Declare hello events published by hello actor in hello actor interface.</span></span>

```csharp
public interface IGameActor : IActor, IActorEventPublisher<IGameEvents>
{
    Task UpdateGameStatus(GameStatus status);

    Task<string> GetGameScore();
}
```
```Java
public interface GameActor extends Actor, ActorEventPublisherE<GameEvents>
{
    CompletableFuture<?> updateGameStatus(GameStatus status);

    CompletableFuture<String> getGameScore();
}
```
<span data-ttu-id="74b62-112">No lado do cliente hello, implemente o manipulador de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="74b62-112">On hello client side, implement hello event handler.</span></span>

```csharp
class GameEventsHandler : IGameEvents
{
    public void GameScoreUpdated(Guid gameId, string currentScore)
    {
        Console.WriteLine(@"Updates: Game: {0}, Score: {1}", gameId, currentScore);
    }
}
```

```Java
class GameEventsHandler implements GameEvents {
    public void gameScoreUpdated(UUID gameId, String currentScore)
    {
        System.out.println("Updates: Game: "+gameId+" ,Score: "+currentScore);
    }
}
```

<span data-ttu-id="74b62-113">No cliente hello, crie um ator toohello proxy que publica o evento hello e assinar eventos tooits.</span><span class="sxs-lookup"><span data-stu-id="74b62-113">On hello client, create a proxy toohello actor that publishes hello event and subscribe tooits events.</span></span>

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

<span data-ttu-id="74b62-114">No caso de saudação de failovers, ator Olá pode fazer failover tooa outro processo ou nó.</span><span class="sxs-lookup"><span data-stu-id="74b62-114">In hello event of failovers, hello actor may fail over tooa different process or node.</span></span> <span data-ttu-id="74b62-115">proxy de ator Olá gerencia assinaturas ativas hello e automaticamente assina-os novamente.</span><span class="sxs-lookup"><span data-stu-id="74b62-115">hello actor proxy manages hello active subscriptions and automatically re-subscribes them.</span></span> <span data-ttu-id="74b62-116">Você pode controlar o intervalo de nova assinatura saudação por meio de saudação `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span><span class="sxs-lookup"><span data-stu-id="74b62-116">You can control hello re-subscription interval through hello `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span></span> <span data-ttu-id="74b62-117">toounsubscribe, use Olá `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span><span class="sxs-lookup"><span data-stu-id="74b62-117">toounsubscribe, use hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span></span>

<span data-ttu-id="74b62-118">Em ator hello, publica eventos Olá conforme elas ocorrem.</span><span class="sxs-lookup"><span data-stu-id="74b62-118">On hello actor, simply publish hello events as they happen.</span></span> <span data-ttu-id="74b62-119">Se houver um evento de toohello de assinantes, tempo de execução de atores Olá será enviá-los notificação hello.</span><span class="sxs-lookup"><span data-stu-id="74b62-119">If there are subscribers toohello event, hello Actors runtime will send them hello notification.</span></span>

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a><span data-ttu-id="74b62-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="74b62-120">Next steps</span></span>
* [<span data-ttu-id="74b62-121">Reentrância de ator</span><span class="sxs-lookup"><span data-stu-id="74b62-121">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="74b62-122">Diagnóstico e monitoramento de desempenho do ator</span><span class="sxs-lookup"><span data-stu-id="74b62-122">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="74b62-123">Documentação de referência da API do Ator</span><span class="sxs-lookup"><span data-stu-id="74b62-123">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="74b62-124">Código de exemplo C#</span><span class="sxs-lookup"><span data-stu-id="74b62-124">C# Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="74b62-125">Código de exemplo em c# .NET Core</span><span class="sxs-lookup"><span data-stu-id="74b62-125">C# .NET Core Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [<span data-ttu-id="74b62-126">Código de exemplo Java</span><span class="sxs-lookup"><span data-stu-id="74b62-126">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
