---
title: Polimorfismo na estrutura Reliable Actors | Microsoft Docs
description: "Crie hierarquias de interfaces .NET e tipos na estrutura Reliable Actors para reutilizar a funcionalidade e as definições da API."
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
ms.openlocfilehash: 36a59a41b2261369a2062c76ef90aebf7e24a221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="polymorphism-in-the-reliable-actors-framework"></a><span data-ttu-id="7eb43-103">Polimorfismo na estrutura Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="7eb43-103">Polymorphism in the Reliable Actors framework</span></span>
<span data-ttu-id="7eb43-104">A estrutura Reliable Actors permite que você crie atores usando muitas das mesmas técnicas que usaria no design orientado a objeto.</span><span class="sxs-lookup"><span data-stu-id="7eb43-104">The Reliable Actors framework allows you to build actors using many of the same techniques that you would use in object-oriented design.</span></span> <span data-ttu-id="7eb43-105">Uma dessas técnicas é o polimorfismo, que permite que tipos e interfaces herdem de pais mais generalizados.</span><span class="sxs-lookup"><span data-stu-id="7eb43-105">One of those techniques is polymorphism, which allows types and interfaces to inherit from more generalized parents.</span></span> <span data-ttu-id="7eb43-106">A herança na estrutura de Reliable Actors geralmente segue o modelo de .NET com algumas restrições adicionais.</span><span class="sxs-lookup"><span data-stu-id="7eb43-106">Inheritance in the Reliable Actors framework generally follows the .NET model with a few additional constraints.</span></span> <span data-ttu-id="7eb43-107">No caso de Java/Linux, ele segue o modelo de Java.</span><span class="sxs-lookup"><span data-stu-id="7eb43-107">In case of Java/Linux, it follows the Java model.</span></span>

## <a name="interfaces"></a><span data-ttu-id="7eb43-108">Interfaces</span><span class="sxs-lookup"><span data-stu-id="7eb43-108">Interfaces</span></span>
<span data-ttu-id="7eb43-109">A estrutura de Reliable Actors exige que você defina pelo menos uma interface a ser implementada pelo seu tipo de ator.</span><span class="sxs-lookup"><span data-stu-id="7eb43-109">The Reliable Actors framework requires you to define at least one interface to be implemented by your actor type.</span></span> <span data-ttu-id="7eb43-110">Essa interface é usada para gerar uma classe proxy que pode ser usada pelos clientes para se comunicar com seus atores.</span><span class="sxs-lookup"><span data-stu-id="7eb43-110">This interface is used to generate a proxy class that can be used by clients to communicate with your actors.</span></span> <span data-ttu-id="7eb43-111">Interfaces podem herdar de outras interfaces, desde que cada interface implementada por um tipo de ator e todos os seus pais derivem, por fim, de IActor(C#) ou Actor(Java).</span><span class="sxs-lookup"><span data-stu-id="7eb43-111">Interfaces can inherit from other interfaces as long as every interface that is implemented by an actor type and all of its parents ultimately derive from IActor(C#) or Actor(Java) .</span></span> <span data-ttu-id="7eb43-112">IActor(C#) e Actor(Java) são as interfaces base definidas pela plataforma para atores em estruturas .NET e Java, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="7eb43-112">IActor(C#) and Actor(Java) are the platform-defined base interfaces for actors in the frameworks .NET and Java respectively.</span></span> <span data-ttu-id="7eb43-113">Assim, o exemplo de polimorfismo clássico usando formas pode parecer semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="7eb43-113">Thus, the classic polymorphism example using shapes might look something like this:</span></span>

![Hierarquia de interface de atores de forma][shapes-interface-hierarchy]

## <a name="types"></a><span data-ttu-id="7eb43-115">Tipos</span><span class="sxs-lookup"><span data-stu-id="7eb43-115">Types</span></span>
<span data-ttu-id="7eb43-116">Você também pode criar uma hierarquia de tipos de ator, derivados da classe base de ator fornecida pela plataforma.</span><span class="sxs-lookup"><span data-stu-id="7eb43-116">You can also create a hierarchy of actor types, which are derived from the base Actor class that is provided by the platform.</span></span> <span data-ttu-id="7eb43-117">No caso de formas, você pode ter um tipo base `Shape`(C#) ou `ShapeImpl`(Java):</span><span class="sxs-lookup"><span data-stu-id="7eb43-117">In the case of shapes, you might have a base `Shape`(C#) or `ShapeImpl`(Java) type:</span></span>

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

<span data-ttu-id="7eb43-118">Os subtipos de `Shape`(C#) ou `ShapeImpl`(Java) podem substituir os métodos da base.</span><span class="sxs-lookup"><span data-stu-id="7eb43-118">Subtypes of `Shape`(C#) or `ShapeImpl`(Java) can override methods from the base.</span></span>

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

<span data-ttu-id="7eb43-119">Observe o atributo `ActorService` no tipo de ator.</span><span class="sxs-lookup"><span data-stu-id="7eb43-119">Note the `ActorService` attribute on the actor type.</span></span> <span data-ttu-id="7eb43-120">Esse atributo informa à estrutura Reliable Actor que ela deverá criar automaticamente um serviço de hospedagem de atores desse tipo.</span><span class="sxs-lookup"><span data-stu-id="7eb43-120">This attribute tells the Reliable Actor framework that it should automatically create a service for hosting actors of this type.</span></span> <span data-ttu-id="7eb43-121">Em alguns casos, você poderá criar um tipo base que destina-se somente para o compartilhamento de recursos com subtipos e nunca será usado para criar uma instância de atores concretos.</span><span class="sxs-lookup"><span data-stu-id="7eb43-121">In some cases, you may wish to create a base type that is solely intended for sharing functionality with subtypes and will never be used to instantiate concrete actors.</span></span> <span data-ttu-id="7eb43-122">Nesses casos, você deve usar a palavra-chave `abstract` para indicar que você nunca criará um ator com base nesse tipo.</span><span class="sxs-lookup"><span data-stu-id="7eb43-122">In those cases, you should use the `abstract` keyword to indicate that you will never create an actor based on that type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7eb43-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7eb43-123">Next steps</span></span>
* <span data-ttu-id="7eb43-124">Veja [Como a estrutura Reliable Actors aproveita a plataforma do Service Fabric](service-fabric-reliable-actors-platform.md) para oferecer estado consistente, escalabilidade e confiabilidade.</span><span class="sxs-lookup"><span data-stu-id="7eb43-124">See [how the Reliable Actors framework leverages the Service Fabric platform](service-fabric-reliable-actors-platform.md) to provide reliability, scalability, and consistent state.</span></span>
* <span data-ttu-id="7eb43-125">Saiba mais sobre o [ciclo de vida do ator](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="7eb43-125">Learn about the [actor lifecycle](service-fabric-reliable-actors-lifecycle.md).</span></span>

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
