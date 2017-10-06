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
# <a name="polymorphism-in-hello-reliable-actors-framework"></a><span data-ttu-id="e19e0-103">Polimorfismo no framework de Reliable Actors Olá</span><span class="sxs-lookup"><span data-stu-id="e19e0-103">Polymorphism in hello Reliable Actors framework</span></span>
<span data-ttu-id="e19e0-104">Olá Reliable Actors estrutura permite que você toobuild atores usando muitos dos Olá mesmas técnicas que você usaria no design orientado a objeto.</span><span class="sxs-lookup"><span data-stu-id="e19e0-104">hello Reliable Actors framework allows you toobuild actors using many of hello same techniques that you would use in object-oriented design.</span></span> <span data-ttu-id="e19e0-105">Uma dessas técnicas é polimorfismo, que permite que os tipos e interfaces tooinherit de mais generalizada pais.</span><span class="sxs-lookup"><span data-stu-id="e19e0-105">One of those techniques is polymorphism, which allows types and interfaces tooinherit from more generalized parents.</span></span> <span data-ttu-id="e19e0-106">Herança no framework de Reliable Actors Olá geralmente segue o modelo de .NET de saudação com algumas restrições adicionais.</span><span class="sxs-lookup"><span data-stu-id="e19e0-106">Inheritance in hello Reliable Actors framework generally follows hello .NET model with a few additional constraints.</span></span> <span data-ttu-id="e19e0-107">No caso de Java/Linux, ele segue o modelo Java de saudação.</span><span class="sxs-lookup"><span data-stu-id="e19e0-107">In case of Java/Linux, it follows hello Java model.</span></span>

## <a name="interfaces"></a><span data-ttu-id="e19e0-108">Interfaces</span><span class="sxs-lookup"><span data-stu-id="e19e0-108">Interfaces</span></span>
<span data-ttu-id="e19e0-109">estrutura de Reliable Actors Olá requer toodefine toobe pelo menos uma interface implementada por seu tipo de ator.</span><span class="sxs-lookup"><span data-stu-id="e19e0-109">hello Reliable Actors framework requires you toodefine at least one interface toobe implemented by your actor type.</span></span> <span data-ttu-id="e19e0-110">Esta interface é usada toogenerate uma classe proxy que pode ser usada por clientes toocommunicate com seus atores.</span><span class="sxs-lookup"><span data-stu-id="e19e0-110">This interface is used toogenerate a proxy class that can be used by clients toocommunicate with your actors.</span></span> <span data-ttu-id="e19e0-111">Interfaces podem herdar de outras interfaces, desde que cada interface implementada por um tipo de ator e todos os seus pais derivem, por fim, de IActor(C#) ou Actor(Java).</span><span class="sxs-lookup"><span data-stu-id="e19e0-111">Interfaces can inherit from other interfaces as long as every interface that is implemented by an actor type and all of its parents ultimately derive from IActor(C#) or Actor(Java) .</span></span> <span data-ttu-id="e19e0-112">IActor(C#) e Actor(Java) são Olá definido plataforma interfaces base para os atores em estruturas de saudação .NET e Java, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="e19e0-112">IActor(C#) and Actor(Java) are hello platform-defined base interfaces for actors in hello frameworks .NET and Java respectively.</span></span> <span data-ttu-id="e19e0-113">Assim, exemplo de polimorfismo clássico hello usando formas pode parecer semelhante a este:</span><span class="sxs-lookup"><span data-stu-id="e19e0-113">Thus, hello classic polymorphism example using shapes might look something like this:</span></span>

![Hierarquia de interface de atores de forma][shapes-interface-hierarchy]

## <a name="types"></a><span data-ttu-id="e19e0-115">Tipos</span><span class="sxs-lookup"><span data-stu-id="e19e0-115">Types</span></span>
<span data-ttu-id="e19e0-116">Você também pode criar uma hierarquia de tipos de ator, que são derivadas da classe ator base Olá que é fornecida pela plataforma de saudação.</span><span class="sxs-lookup"><span data-stu-id="e19e0-116">You can also create a hierarchy of actor types, which are derived from hello base Actor class that is provided by hello platform.</span></span> <span data-ttu-id="e19e0-117">No caso de saudação de formas, você pode ter uma base `Shape`(c#) ou `ShapeImpl`(Java) do tipo:</span><span class="sxs-lookup"><span data-stu-id="e19e0-117">In hello case of shapes, you might have a base `Shape`(C#) or `ShapeImpl`(Java) type:</span></span>

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

<span data-ttu-id="e19e0-118">Subtipos de `Shape`(c#) ou `ShapeImpl`(Java) pode substituir métodos da saudação base.</span><span class="sxs-lookup"><span data-stu-id="e19e0-118">Subtypes of `Shape`(C#) or `ShapeImpl`(Java) can override methods from hello base.</span></span>

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

<span data-ttu-id="e19e0-119">Saudação de Observação `ActorService` atributo no tipo de ator hello.</span><span class="sxs-lookup"><span data-stu-id="e19e0-119">Note hello `ActorService` attribute on hello actor type.</span></span> <span data-ttu-id="e19e0-120">Esse atributo diz o framework de Reliable Actor Olá que ele crie automaticamente um serviço de hospedagem atores desse tipo.</span><span class="sxs-lookup"><span data-stu-id="e19e0-120">This attribute tells hello Reliable Actor framework that it should automatically create a service for hosting actors of this type.</span></span> <span data-ttu-id="e19e0-121">Em alguns casos, você poderá toocreate um tipo base que é destinado somente para a funcionalidade de compartilhamento com subtipos e nunca serão usada tooinstantiate atores concretos.</span><span class="sxs-lookup"><span data-stu-id="e19e0-121">In some cases, you may wish toocreate a base type that is solely intended for sharing functionality with subtypes and will never be used tooinstantiate concrete actors.</span></span> <span data-ttu-id="e19e0-122">Nesses casos, você deve usar o hello `abstract` tooindicate de palavra-chave que você nunca criará um ator com base nesse tipo.</span><span class="sxs-lookup"><span data-stu-id="e19e0-122">In those cases, you should use hello `abstract` keyword tooindicate that you will never create an actor based on that type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e19e0-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e19e0-123">Next steps</span></span>
* <span data-ttu-id="e19e0-124">Consulte [como framework de Reliable Actors Olá aproveita a plataforma do Service Fabric Olá](service-fabric-reliable-actors-platform.md) tooprovide estado consistente, escalabilidade e confiabilidade.</span><span class="sxs-lookup"><span data-stu-id="e19e0-124">See [how hello Reliable Actors framework leverages hello Service Fabric platform](service-fabric-reliable-actors-platform.md) tooprovide reliability, scalability, and consistent state.</span></span>
* <span data-ttu-id="e19e0-125">Saiba mais sobre Olá [ciclo de vida de ator](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="e19e0-125">Learn about hello [actor lifecycle](service-fabric-reliable-actors-lifecycle.md).</span></span>

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
