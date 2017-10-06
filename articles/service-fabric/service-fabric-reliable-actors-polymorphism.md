---
title: "aaaPolymorphism no framework de Reliable Actors Olá | Microsoft Docs"
description: "Crie hierarquias de tipos em Olá funcionalidade de tooreuse do framework Reliable Actors e definições de API e interfaces do .NET."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: vturecek
ms.assetid: ef0eeff6-32b7-410d-ac69-87cba8b8fd46
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ed9ec442595bd9a5e48c9af1f6aac003439b81f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="polymorphism-in-hello-reliable-actors-framework"></a>Polimorfismo no framework de Reliable Actors Olá
Olá Reliable Actors estrutura permite que você toobuild atores usando muitos dos Olá mesmas técnicas que você usaria no design orientado a objeto. Uma dessas técnicas é polimorfismo, que permite que os tipos e interfaces tooinherit de mais generalizada pais. Herança no framework de Reliable Actors Olá geralmente segue o modelo de .NET de saudação com algumas restrições adicionais. No caso de Java/Linux, ele segue o modelo Java de saudação.

## <a name="interfaces"></a>Interfaces
estrutura de Reliable Actors Olá requer toodefine toobe pelo menos uma interface implementada por seu tipo de ator. Esta interface é usada toogenerate uma classe proxy que pode ser usada por clientes toocommunicate com seus atores. Interfaces podem herdar de outras interfaces, desde que cada interface implementada por um tipo de ator e todos os seus pais derivem, por fim, de IActor(C#) ou Actor(Java). IActor(C#) e Actor(Java) são Olá definido plataforma interfaces base para os atores em estruturas de saudação .NET e Java, respectivamente. Assim, exemplo de polimorfismo clássico hello usando formas pode parecer semelhante a este:

![Hierarquia de interface de atores de forma][shapes-interface-hierarchy]

## <a name="types"></a>Tipos
Você também pode criar uma hierarquia de tipos de ator, que são derivadas da classe ator base Olá que é fornecida pela plataforma de saudação. No caso de saudação de formas, você pode ter uma base `Shape`(c#) ou `ShapeImpl`(Java) do tipo:

```csharp
public abstract class Shape : Actor, IShape
{
    public abstract Task<int> GetVerticeCount();

    public abstract Task<double> GetAreaAsync();
}
```
```Java
public abstract class ShapeImpl extends FabricActor implements Shape
{
    public abstract CompletableFuture<int> getVerticeCount();

    public abstract CompletableFuture<double> getAreaAsync();
}
```

Subtipos de `Shape`(c#) ou `ShapeImpl`(Java) pode substituir métodos da saudação base.

```csharp
[ActorService(Name = "Circle")]
[StatePersistence(StatePersistence.Persisted)]
public class Circle : Shape, ICircle
{
    public override Task<int> GetVerticeCount()
    {
        return Task.FromResult(0);
    }

    public override async Task<double> GetAreaAsync()
    {
        CircleState state = await this.StateManager.GetStateAsync<CircleState>("circle");

        return Math.PI *
            state.Radius *
            state.Radius;
    }
}
```
```Java
@ActorServiceAttribute(name = "Circle")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class Circle extends ShapeImpl implements Circle
{
    @Override
    public CompletableFuture<Integer> getVerticeCount()
    {
        return CompletableFuture.completedFuture(0);
    }

    @Override
    public CompletableFuture<Double> getAreaAsync()
    {
        return (this.stateManager().getStateAsync<CircleState>("circle").thenApply(state->{
          return Math.PI * state.radius * state.radius;
        }));
    }
}
```

Saudação de Observação `ActorService` atributo no tipo de ator hello. Esse atributo diz o framework de Reliable Actor Olá que ele crie automaticamente um serviço de hospedagem atores desse tipo. Em alguns casos, você poderá toocreate um tipo base que é destinado somente para a funcionalidade de compartilhamento com subtipos e nunca serão usada tooinstantiate atores concretos. Nesses casos, você deve usar o hello `abstract` tooindicate de palavra-chave que você nunca criará um ator com base nesse tipo.

## <a name="next-steps"></a>Próximas etapas
* Consulte [como framework de Reliable Actors Olá aproveita a plataforma do Service Fabric Olá](service-fabric-reliable-actors-platform.md) tooprovide estado consistente, escalabilidade e confiabilidade.
* Saiba mais sobre Olá [ciclo de vida de ator](service-fabric-reliable-actors-lifecycle.md).

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
