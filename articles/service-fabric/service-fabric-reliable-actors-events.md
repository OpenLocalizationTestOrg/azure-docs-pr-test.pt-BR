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
# <a name="actor-events"></a>Eventos de ator
Os eventos de ator fornecem notificações de melhor esforço de toosend uma maneira de clientes do hello ator toohello. Os eventos de ator foram desenvolvidos para comunicação entre ator e cliente e não devem ser usados para comunicação entre ator e ator.

saudação de código a seguir trechos de código mostram como eventos de ator toouse em seu aplicativo.

Defina uma interface que descreve eventos de saudação publicados pelo ator hello. Esta interface deve ser derivada de saudação `IActorEvents` interface. Olá argumentos de métodos Olá devem ser [de contrato de dados serializáveis](service-fabric-reliable-actors-notes-on-actor-type-serialization.md). métodos de saudação devem retornar void, como eventos notificações são uma maneira e melhor esforço.

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
Declare eventos Olá publicados por ator Olá na interface de ator hello.

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
No lado do cliente hello, implemente o manipulador de eventos de saudação.

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

No cliente hello, crie um ator toohello proxy que publica o evento hello e assinar eventos tooits.

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

No caso de saudação de failovers, ator Olá pode fazer failover tooa outro processo ou nó. proxy de ator Olá gerencia assinaturas ativas hello e automaticamente assina-os novamente. Você pode controlar o intervalo de nova assinatura saudação por meio de saudação `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API. toounsubscribe, use Olá `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.

Em ator hello, publica eventos Olá conforme elas ocorrem. Se houver um evento de toohello de assinantes, tempo de execução de atores Olá será enviá-los notificação hello.

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a>Próximas etapas
* [Reentrância de ator](service-fabric-reliable-actors-reentrancy.md)
* [Diagnóstico e monitoramento de desempenho do ator](service-fabric-reliable-actors-diagnostics.md)
* [Documentação de referência da API do Ator](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Código de exemplo C#](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Código de exemplo em c# .NET Core](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [Código de exemplo Java](http://github.com/Azure-Samples/service-fabric-java-getting-started)
