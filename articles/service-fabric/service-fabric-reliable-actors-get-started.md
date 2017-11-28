---
title: "Criar seu primeiro microsserviço do Azure baseado em ator em C# | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de criação, depuração e implantação de um serviço simples baseado em ator usando os Reliable Actors do Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 3f447e049ccd33c77f422e8aa703ad6646f9ffa2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="af724-103">Introdução aos Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="af724-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="af724-104">C# em Windows</span><span class="sxs-lookup"><span data-stu-id="af724-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="af724-105">Java no Linux</span><span class="sxs-lookup"><span data-stu-id="af724-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="af724-106">Este artigo explica os conceitos básicos dos Reliable Actors do Service Fabric e orienta você durante a criação, a depuração e a implantação de um aplicativo Reliable Actor simples no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af724-106">This article explains the basics of Azure Service Fabric Reliable Actors and walks you through creating, debugging, and deploying a simple Reliable Actor application in Visual Studio.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="af724-107">Instalação e configuração</span><span class="sxs-lookup"><span data-stu-id="af724-107">Installation and setup</span></span>
<span data-ttu-id="af724-108">Antes de começar, verifique se há um ambiente de desenvolvimento do Service Fabric configurado no seu computador.</span><span class="sxs-lookup"><span data-stu-id="af724-108">Before you start, ensure that you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="af724-109">Se você precisa configurá-lo, confira as instruções detalhadas em [Como configurar o ambiente de desenvolvimento](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="af724-109">If you need to set it up, see detailed instructions on [how to set up the development environment](service-fabric-get-started.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="af724-110">Conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="af724-110">Basic concepts</span></span>
<span data-ttu-id="af724-111">Para começar a usar os Reliable Actors, você só precisa entender alguns conceitos básicos:</span><span class="sxs-lookup"><span data-stu-id="af724-111">To get started with Reliable Actors, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="af724-112">**Serviço do ator**.</span><span class="sxs-lookup"><span data-stu-id="af724-112">**Actor service**.</span></span> <span data-ttu-id="af724-113">Os Reliable Actors são empacotados em Reliable Services que podem ser implantados na infraestrutura do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="af724-113">Reliable Actors are packaged in Reliable Services that can be deployed in the Service Fabric infrastructure.</span></span> <span data-ttu-id="af724-114">As instâncias de ator são ativadas em uma instância de serviço nomeado.</span><span class="sxs-lookup"><span data-stu-id="af724-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="af724-115">**Registro do ator**.</span><span class="sxs-lookup"><span data-stu-id="af724-115">**Actor registration**.</span></span> <span data-ttu-id="af724-116">Como ocorre com Reliable Services, um serviço de Reliable Actor precisa ser registrado com o tempo de execução do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="af724-116">As with Reliable Services, a Reliable Actor service needs to be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="af724-117">Além disso, o tipo de ator precisa ser registrado com o tempo de execução do ator.</span><span class="sxs-lookup"><span data-stu-id="af724-117">In addition, the actor type needs to be registered with the Actor runtime.</span></span>
* <span data-ttu-id="af724-118">**Interface do Ator**.</span><span class="sxs-lookup"><span data-stu-id="af724-118">**Actor interface**.</span></span> <span data-ttu-id="af724-119">A interface do ator é usada para definir uma interface pública fortemente tipada de um ator.</span><span class="sxs-lookup"><span data-stu-id="af724-119">The actor interface is used to define a strongly typed public interface of an actor.</span></span> <span data-ttu-id="af724-120">Na terminologia do modelo de Reliable Actor, a interface do ator define os tipos de mensagem que o ator pode entender e processar.</span><span class="sxs-lookup"><span data-stu-id="af724-120">In the Reliable Actor model terminology, the actor interface defines the types of messages that the actor can understand and process.</span></span> <span data-ttu-id="af724-121">A interface do ator é usada por outros atores ou aplicativos cliente para “enviar” (de modo assíncrono) mensagens ao ator.</span><span class="sxs-lookup"><span data-stu-id="af724-121">The actor interface is used by other actors and client applications to "send" (asynchronously) messages to the actor.</span></span> <span data-ttu-id="af724-122">Os Reliable Actors pode implantar várias interfaces.</span><span class="sxs-lookup"><span data-stu-id="af724-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="af724-123">**Classe ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="af724-123">**ActorProxy class**.</span></span> <span data-ttu-id="af724-124">A classe ActorProxy é usada por aplicativos cliente para invocar os métodos expostos por meio de suas interfaces de ator.</span><span class="sxs-lookup"><span data-stu-id="af724-124">The ActorProxy class is used by client applications to invoke the methods exposed through the actor interface.</span></span> <span data-ttu-id="af724-125">A classe ActorProxy apresenta duas funcionalidades importantes:</span><span class="sxs-lookup"><span data-stu-id="af724-125">The ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="af724-126">Resolução do nome: ela consegue localizar o ator no cluster (localizar o nó do cluster no qual ele está hospedado).</span><span class="sxs-lookup"><span data-stu-id="af724-126">Name resolution: It is able to locate the actor in the cluster (find the node of the cluster where it is hosted).</span></span>
  * <span data-ttu-id="af724-127">Tratamento de falhas: ela pode repetir as invocações do método e resolver novamente o local do ator, por exemplo, depois que uma falha exige que ele seja relocado para outro nó no cluster.</span><span class="sxs-lookup"><span data-stu-id="af724-127">Failure handling: It can retry method invocations and re-resolve the actor location after, for example, a failure that requires the actor to be relocated to another node in the cluster.</span></span>

<span data-ttu-id="af724-128">Vale a pena mencionar as seguintes regras que pertencem às interfaces de ator:</span><span class="sxs-lookup"><span data-stu-id="af724-128">The following rules that pertain to actor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="af724-129">Métodos da interface de ator não podem ser sobrecarregados.</span><span class="sxs-lookup"><span data-stu-id="af724-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="af724-130">Métodos da interface de ator não podem ter parâmetros de saída, de referência e opcionais.</span><span class="sxs-lookup"><span data-stu-id="af724-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="af724-131">Não há suporte para interfaces genéricas.</span><span class="sxs-lookup"><span data-stu-id="af724-131">Generic interfaces are not supported.</span></span>

## <a name="create-a-new-project-in-visual-studio"></a><span data-ttu-id="af724-132">Criar um novo projeto no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="af724-132">Create a new project in Visual Studio</span></span>
<span data-ttu-id="af724-133">Inicie o Visual Studio 2015 ou 2017 como administrador e crie um novo projeto de aplicativo do Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="af724-133">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project:</span></span>

![Ferramentas do Service Fabric para Visual Studio – novo projeto][1]

<span data-ttu-id="af724-135">Na próxima caixa de diálogo, você pode escolher o tipo de projeto que deseja criar.</span><span class="sxs-lookup"><span data-stu-id="af724-135">In the next dialog box, you can choose the type of project that you want to create.</span></span>

![Modelos de projeto do Service Fabric][5]

<span data-ttu-id="af724-137">Para o projeto HelloWorld, vamos usar o serviço Reliable Actors do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="af724-137">For the HelloWorld project, let's use the Service Fabric Reliable Actors service.</span></span>

<span data-ttu-id="af724-138">Depois de criar a solução, você verá a seguinte estrutura:</span><span class="sxs-lookup"><span data-stu-id="af724-138">After you have created the solution, you should see the following structure:</span></span>

![Estrutura de projeto do Service Fabric][2]

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="af724-140">Blocos de construção básicos de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="af724-140">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="af724-141">Uma solução comum do Reliable Actors é composta por três projetos:</span><span class="sxs-lookup"><span data-stu-id="af724-141">A typical Reliable Actors solution is composed of three projects:</span></span>

* <span data-ttu-id="af724-142">**O projeto do aplicativo (MyActorApplication)**.</span><span class="sxs-lookup"><span data-stu-id="af724-142">**The application project (MyActorApplication)**.</span></span> <span data-ttu-id="af724-143">Esse é o projeto que empacota todos os serviços juntos para implantação.</span><span class="sxs-lookup"><span data-stu-id="af724-143">This is the project that packages all of the services together for deployment.</span></span> <span data-ttu-id="af724-144">Ele contém os scripts do PowerShell e o *ApplicationManifest.xml* para gerenciamento do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="af724-144">It contains the *ApplicationManifest.xml* and PowerShell scripts for managing the application.</span></span>
* <span data-ttu-id="af724-145">**O projeto da interface (MyActor.Interfaces)**.</span><span class="sxs-lookup"><span data-stu-id="af724-145">**The interface project (MyActor.Interfaces)**.</span></span> <span data-ttu-id="af724-146">Esse é o projeto que contém a definição de interface para o ator.</span><span class="sxs-lookup"><span data-stu-id="af724-146">This is the project that contains the interface definition for the actor.</span></span> <span data-ttu-id="af724-147">No projeto MyActor.Interfaces, você pode definir as interfaces que serão usadas pelos atores na solução.</span><span class="sxs-lookup"><span data-stu-id="af724-147">In the MyActor.Interfaces project, you can define the interfaces that will be used by the actors in the solution.</span></span> <span data-ttu-id="af724-148">As interfaces de ator podem ser definidas em qualquer projeto com qualquer nome, mas a interface define o contrato de ator compartilhado pela implementação do ator e os clientes que chamam o ator e, portanto, geralmente faz sentido defini-lo em um assembly separado da implementação do ator e que possa ser compartilhado por vários outros projetos.</span><span class="sxs-lookup"><span data-stu-id="af724-148">Your actor interfaces can be defined in any project with any name, however the interface defines the actor contract that is shared by the actor implementation and the clients calling the actor, so it typically makes sense to define it in an assembly that is separate from the actor implementation and can be shared by multiple other projects.</span></span>

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* <span data-ttu-id="af724-149">**O projeto do serviço de ator (MyActor)**.</span><span class="sxs-lookup"><span data-stu-id="af724-149">**The actor service project (MyActor)**.</span></span> <span data-ttu-id="af724-150">Esse é o projeto usado para definir o serviço da Malha do Serviço que hospedará o ator.</span><span class="sxs-lookup"><span data-stu-id="af724-150">This is the project used to define the Service Fabric service that is going to host the actor.</span></span> <span data-ttu-id="af724-151">Ele contém a implementação do ator.</span><span class="sxs-lookup"><span data-stu-id="af724-151">It contains the implementation of the actor.</span></span> <span data-ttu-id="af724-152">Uma implementação do ator é uma classe derivada do tipo base `Actor` e implementa as interfaces definidas no projeto MyActor.Interfaces.</span><span class="sxs-lookup"><span data-stu-id="af724-152">An actor implementation is a class that derives from the base type `Actor` and implements the interface(s) that are defined in the MyActor.Interfaces project.</span></span> <span data-ttu-id="af724-153">Uma classe de ator também deve implementar um construtor que aceita uma instância `ActorService` e um `ActorId` e as passem para a classe de base `Actor`.</span><span class="sxs-lookup"><span data-stu-id="af724-153">An actor class must also implement a constructor that accepts an `ActorService` instance and an `ActorId` and passes them to the base `Actor` class.</span></span> <span data-ttu-id="af724-154">Isso possibilita a injeção de dependência do construtor de dependências de plataforma.</span><span class="sxs-lookup"><span data-stu-id="af724-154">This allows for constructor dependency injection of platform dependencies.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

<span data-ttu-id="af724-155">O serviço de ator deve ser registrado com um tipo de serviço no tempo de execução do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="af724-155">The actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="af724-156">Para que o Serviço de Ator seja executado em suas instâncias de ator, o tipo de ator também deve ser registrado no Serviço de Ator.</span><span class="sxs-lookup"><span data-stu-id="af724-156">In order for the Actor Service to run your actor instances, your actor type must also be registered with the Actor Service.</span></span> <span data-ttu-id="af724-157">O método de registro `ActorRuntime` realiza esse trabalho para os atores.</span><span class="sxs-lookup"><span data-stu-id="af724-157">The `ActorRuntime` registration method performs this work for actors.</span></span>

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

<span data-ttu-id="af724-158">Se você iniciar um novo projeto no Visual Studio e tiver apenas uma definição de ator, o registro será incluído por padrão no código gerado pelo Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af724-158">If you start from a new project in Visual Studio and you have only one actor definition, the registration is included by default in the code that Visual Studio generates.</span></span> <span data-ttu-id="af724-159">Se você definir outros atores no serviço, será preciso adicionar o registro do ator usando:</span><span class="sxs-lookup"><span data-stu-id="af724-159">If you define other actors in the service, you need to add the actor registration by using:</span></span>

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> <span data-ttu-id="af724-160">O tempo de execução dos Atores do Service Fabric emitem alguns [eventos e contadores de desempenho relacionados aos métodos de ator](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="af724-160">The Service Fabric Actors runtime emits some [events and performance counters related to actor methods](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span></span> <span data-ttu-id="af724-161">Eles são úteis para diagnóstico e monitoramento de desempenho.</span><span class="sxs-lookup"><span data-stu-id="af724-161">They are useful in diagnostics and performance monitoring.</span></span>
> 
> 

## <a name="debugging"></a><span data-ttu-id="af724-162">Depurando</span><span class="sxs-lookup"><span data-stu-id="af724-162">Debugging</span></span>
<span data-ttu-id="af724-163">As ferramentas para Visual Studio do Service Fabric dão suporte à depuração no computador local.</span><span class="sxs-lookup"><span data-stu-id="af724-163">The Service Fabric tools for Visual Studio support debugging on your local machine.</span></span> <span data-ttu-id="af724-164">Você pode iniciar uma sessão de depuração pressionando a tecla F5.</span><span class="sxs-lookup"><span data-stu-id="af724-164">You can start a debugging session by hitting the F5 key.</span></span> <span data-ttu-id="af724-165">O Visual Studio cria (se necessário) pacotes.</span><span class="sxs-lookup"><span data-stu-id="af724-165">Visual Studio builds (if necessary) packages.</span></span> <span data-ttu-id="af724-166">Ele também implanta o aplicativo no cluster do Service Fabric local e anexa o depurador.</span><span class="sxs-lookup"><span data-stu-id="af724-166">It also deploys the application on the local Service Fabric cluster and attaches the debugger.</span></span>

<span data-ttu-id="af724-167">Durante o processo de implantação, você poderá ver o andamento na janela **Saída** .</span><span class="sxs-lookup"><span data-stu-id="af724-167">During the deployment process, you can see the progress in the **Output** window.</span></span>

![Janela de saída de depuração do Service Fabric][3]

## <a name="next-steps"></a><span data-ttu-id="af724-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="af724-169">Next steps</span></span>
<span data-ttu-id="af724-170">Saiba mais sobre [como os Reliable Actors usam a plataforma do Service Fabric](service-fabric-reliable-actors-platform.md).</span><span class="sxs-lookup"><span data-stu-id="af724-170">Learn more about [how Reliable Actors use the Service Fabric platform](service-fabric-reliable-actors-platform.md).</span></span>

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
