---
title: "aaaCreate sua primeira baseado em ator Azure microsserviço em c# | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de saudação de criar, depurar e implantar um serviço baseado em ator simples usando o serviço de malha Reliable Actors."
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
ms.openlocfilehash: ab4f75bef0adb6e70f0ead587475b3fb51e6e6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="30645-103">Introdução aos Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="30645-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="30645-104">C# em Windows</span><span class="sxs-lookup"><span data-stu-id="30645-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="30645-105">Java no Linux</span><span class="sxs-lookup"><span data-stu-id="30645-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="30645-106">Este artigo explica as Noções básicas de saudação do Azure Service Fabric Reliable Actors e orienta você por criar, depurar e implantar um aplicativo de Reliable Actor simples no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="30645-106">This article explains hello basics of Azure Service Fabric Reliable Actors and walks you through creating, debugging, and deploying a simple Reliable Actor application in Visual Studio.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="30645-107">Instalação e configuração</span><span class="sxs-lookup"><span data-stu-id="30645-107">Installation and setup</span></span>
<span data-ttu-id="30645-108">Antes de começar, certifique-se de que você tenha o ambiente de desenvolvimento do Service Fabric Olá configurado no seu computador.</span><span class="sxs-lookup"><span data-stu-id="30645-108">Before you start, ensure that you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="30645-109">Se você precisar tooset-lo, consulte as instruções detalhadas em [como tooset ambiente de desenvolvimento Olá](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="30645-109">If you need tooset it up, see detailed instructions on [how tooset up hello development environment](service-fabric-get-started.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="30645-110">Conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="30645-110">Basic concepts</span></span>
<span data-ttu-id="30645-111">tooget iniciado com atores confiável, você só precisa toounderstand alguns conceitos básicos:</span><span class="sxs-lookup"><span data-stu-id="30645-111">tooget started with Reliable Actors, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="30645-112">**Serviço do ator**.</span><span class="sxs-lookup"><span data-stu-id="30645-112">**Actor service**.</span></span> <span data-ttu-id="30645-113">Confiáveis atores são empacotados em serviços confiáveis que podem ser implantados na infraestrutura de malha do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="30645-113">Reliable Actors are packaged in Reliable Services that can be deployed in hello Service Fabric infrastructure.</span></span> <span data-ttu-id="30645-114">As instâncias de ator são ativadas em uma instância de serviço nomeado.</span><span class="sxs-lookup"><span data-stu-id="30645-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="30645-115">**Registro do ator**.</span><span class="sxs-lookup"><span data-stu-id="30645-115">**Actor registration**.</span></span> <span data-ttu-id="30645-116">Como com serviços confiáveis, um serviço de Reliable Actor deve toobe registrado com o tempo de execução do hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="30645-116">As with Reliable Services, a Reliable Actor service needs toobe registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="30645-117">Além disso, o tipo de ator Olá precisa toobe registrado com o tempo de execução do hello ator.</span><span class="sxs-lookup"><span data-stu-id="30645-117">In addition, hello actor type needs toobe registered with hello Actor runtime.</span></span>
* <span data-ttu-id="30645-118">**Interface do Ator**.</span><span class="sxs-lookup"><span data-stu-id="30645-118">**Actor interface**.</span></span> <span data-ttu-id="30645-119">interface de ator Olá é usado toodefine uma interface pública fortemente tipada de um ator.</span><span class="sxs-lookup"><span data-stu-id="30645-119">hello actor interface is used toodefine a strongly typed public interface of an actor.</span></span> <span data-ttu-id="30645-120">No hello terminologia do modelo confiável ator, interface de ator Olá define Olá tipos de mensagens que Olá ator podem entender e processar.</span><span class="sxs-lookup"><span data-stu-id="30645-120">In hello Reliable Actor model terminology, hello actor interface defines hello types of messages that hello actor can understand and process.</span></span> <span data-ttu-id="30645-121">interface de ator Olá é usado por outros atores e aplicativos cliente muito "enviam" (de forma assíncrona) ator de toohello de mensagens.</span><span class="sxs-lookup"><span data-stu-id="30645-121">hello actor interface is used by other actors and client applications too"send" (asynchronously) messages toohello actor.</span></span> <span data-ttu-id="30645-122">Os Reliable Actors pode implantar várias interfaces.</span><span class="sxs-lookup"><span data-stu-id="30645-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="30645-123">**Classe ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="30645-123">**ActorProxy class**.</span></span> <span data-ttu-id="30645-124">Olá ActorProxy classe é usada pelo cliente aplicativos tooinvoke Olá métodos expostos pela interface de ator hello.</span><span class="sxs-lookup"><span data-stu-id="30645-124">hello ActorProxy class is used by client applications tooinvoke hello methods exposed through hello actor interface.</span></span> <span data-ttu-id="30645-125">Olá ActorProxy classe fornece dois recursos importantes:</span><span class="sxs-lookup"><span data-stu-id="30645-125">hello ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="30645-126">A resolução de nome: é toolocate capaz de ator de saudação em cluster hello (localizar o nó de saudação do cluster de saudação onde ele está hospedado).</span><span class="sxs-lookup"><span data-stu-id="30645-126">Name resolution: It is able toolocate hello actor in hello cluster (find hello node of hello cluster where it is hosted).</span></span>
  * <span data-ttu-id="30645-127">Tratamento de falha: pode repetir invocações de método e resolver o local de ator Olá após novamente, por exemplo, uma falha que exija Olá ator toobe realocado tooanother nó no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="30645-127">Failure handling: It can retry method invocations and re-resolve hello actor location after, for example, a failure that requires hello actor toobe relocated tooanother node in hello cluster.</span></span>

<span data-ttu-id="30645-128">Olá, seguindo as regras que pertencem a interfaces tooactor é vale a pena mencionar:</span><span class="sxs-lookup"><span data-stu-id="30645-128">hello following rules that pertain tooactor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="30645-129">Métodos da interface de ator não podem ser sobrecarregados.</span><span class="sxs-lookup"><span data-stu-id="30645-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="30645-130">Métodos da interface de ator não podem ter parâmetros de saída, de referência e opcionais.</span><span class="sxs-lookup"><span data-stu-id="30645-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="30645-131">Não há suporte para interfaces genéricas.</span><span class="sxs-lookup"><span data-stu-id="30645-131">Generic interfaces are not supported.</span></span>

## <a name="create-a-new-project-in-visual-studio"></a><span data-ttu-id="30645-132">Criar um novo projeto no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="30645-132">Create a new project in Visual Studio</span></span>
<span data-ttu-id="30645-133">Inicie o Visual Studio 2015 ou 2017 como administrador e crie um novo projeto de aplicativo do Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="30645-133">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project:</span></span>

![Ferramentas do Service Fabric para Visual Studio – novo projeto][1]

<span data-ttu-id="30645-135">Na próxima caixa de diálogo hello, você pode escolher o tipo de saudação do projeto que você deseja toocreate.</span><span class="sxs-lookup"><span data-stu-id="30645-135">In hello next dialog box, you can choose hello type of project that you want toocreate.</span></span>

![Modelos de projeto do Service Fabric][5]

<span data-ttu-id="30645-137">Para o projeto de HelloWorld Olá, vamos usar o serviço do Service Fabric Reliable Actors hello.</span><span class="sxs-lookup"><span data-stu-id="30645-137">For hello HelloWorld project, let's use hello Service Fabric Reliable Actors service.</span></span>

<span data-ttu-id="30645-138">Depois que você criou a solução hello, você deve ver Olá estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="30645-138">After you have created hello solution, you should see hello following structure:</span></span>

![Estrutura de projeto do Service Fabric][2]

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="30645-140">Blocos de construção básicos de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="30645-140">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="30645-141">Uma solução comum do Reliable Actors é composta por três projetos:</span><span class="sxs-lookup"><span data-stu-id="30645-141">A typical Reliable Actors solution is composed of three projects:</span></span>

* <span data-ttu-id="30645-142">**projeto de aplicativo Hello (MyActorApplication)**.</span><span class="sxs-lookup"><span data-stu-id="30645-142">**hello application project (MyActorApplication)**.</span></span> <span data-ttu-id="30645-143">Esse é o projeto de saudação que todos os serviços de saudação juntos para implantação de pacotes.</span><span class="sxs-lookup"><span data-stu-id="30645-143">This is hello project that packages all of hello services together for deployment.</span></span> <span data-ttu-id="30645-144">Ele contém Olá *ApplicationManifest.xml* e scripts do PowerShell para gerenciar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="30645-144">It contains hello *ApplicationManifest.xml* and PowerShell scripts for managing hello application.</span></span>
* <span data-ttu-id="30645-145">**projeto de interface de saudação (MyActor.Interfaces)**.</span><span class="sxs-lookup"><span data-stu-id="30645-145">**hello interface project (MyActor.Interfaces)**.</span></span> <span data-ttu-id="30645-146">Esse é o projeto de saudação que contém a definição de interface de saudação de ator hello.</span><span class="sxs-lookup"><span data-stu-id="30645-146">This is hello project that contains hello interface definition for hello actor.</span></span> <span data-ttu-id="30645-147">No projeto de MyActor.Interfaces hello, você pode definir interfaces Olá que serão usados por atores Olá na solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="30645-147">In hello MyActor.Interfaces project, you can define hello interfaces that will be used by hello actors in hello solution.</span></span> <span data-ttu-id="30645-148">As interfaces de ator podem ser definidas em qualquer projeto com qualquer nome, mas interface Olá define o contrato de ator de saudação que é compartilhado por clientes de saudação chamando ator hello, então, geralmente faz sentido toodefine e implementação de ator Olá-lo em um assembly separar da implementação de ator hello e pode ser compartilhado por vários outros projetos.</span><span class="sxs-lookup"><span data-stu-id="30645-148">Your actor interfaces can be defined in any project with any name, however hello interface defines hello actor contract that is shared by hello actor implementation and hello clients calling hello actor, so it typically makes sense toodefine it in an assembly that is separate from hello actor implementation and can be shared by multiple other projects.</span></span>

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* <span data-ttu-id="30645-149">**projeto de serviço de ator Hello (MyActor)**.</span><span class="sxs-lookup"><span data-stu-id="30645-149">**hello actor service project (MyActor)**.</span></span> <span data-ttu-id="30645-150">Isso é Olá projeto usado toodefine Olá Service Fabric serviço ator de saudação toohost contínuo.</span><span class="sxs-lookup"><span data-stu-id="30645-150">This is hello project used toodefine hello Service Fabric service that is going toohost hello actor.</span></span> <span data-ttu-id="30645-151">Ele contém a implementação de saudação de ator hello.</span><span class="sxs-lookup"><span data-stu-id="30645-151">It contains hello implementation of hello actor.</span></span> <span data-ttu-id="30645-152">Uma implementação de ator é uma classe que deriva do tipo base Olá `Actor` e implementa Olá interfaces que são definidos no projeto de MyActor.Interfaces hello.</span><span class="sxs-lookup"><span data-stu-id="30645-152">An actor implementation is a class that derives from hello base type `Actor` and implements hello interface(s) that are defined in hello MyActor.Interfaces project.</span></span> <span data-ttu-id="30645-153">Uma classe de ator também deve implementar um construtor que aceite um `ActorService` instância e um `ActorId` e os passa toohello base `Actor` classe.</span><span class="sxs-lookup"><span data-stu-id="30645-153">An actor class must also implement a constructor that accepts an `ActorService` instance and an `ActorId` and passes them toohello base `Actor` class.</span></span> <span data-ttu-id="30645-154">Isso possibilita a injeção de dependência do construtor de dependências de plataforma.</span><span class="sxs-lookup"><span data-stu-id="30645-154">This allows for constructor dependency injection of platform dependencies.</span></span>

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

<span data-ttu-id="30645-155">serviço de ator Olá deve ser registrado com um tipo de serviço em tempo de execução do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="30645-155">hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="30645-156">Em ordem para Olá toorun do serviço de ator suas instâncias de ator, seu tipo de ator também deve ser registrado com hello serviço de ator.</span><span class="sxs-lookup"><span data-stu-id="30645-156">In order for hello Actor Service toorun your actor instances, your actor type must also be registered with hello Actor Service.</span></span> <span data-ttu-id="30645-157">Olá `ActorRuntime` método de registro executa essa tarefa para atores.</span><span class="sxs-lookup"><span data-stu-id="30645-157">hello `ActorRuntime` registration method performs this work for actors.</span></span>

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

<span data-ttu-id="30645-158">Se você iniciar um novo projeto no Visual Studio e você tiver apenas uma definição de ator, registro de saudação é incluído por padrão no código de saudação que o Visual Studio gera.</span><span class="sxs-lookup"><span data-stu-id="30645-158">If you start from a new project in Visual Studio and you have only one actor definition, hello registration is included by default in hello code that Visual Studio generates.</span></span> <span data-ttu-id="30645-159">Se você definir outros atores no serviço Olá, você precisa de registro de ator Olá tooadd usando:</span><span class="sxs-lookup"><span data-stu-id="30645-159">If you define other actors in hello service, you need tooadd hello actor registration by using:</span></span>

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> <span data-ttu-id="30645-160">Olá atores de malha do serviço de tempo de execução emite alguns [eventos e contadores de desempenho relacionam métodos tooactor](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="30645-160">hello Service Fabric Actors runtime emits some [events and performance counters related tooactor methods](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span></span> <span data-ttu-id="30645-161">Eles são úteis para diagnóstico e monitoramento de desempenho.</span><span class="sxs-lookup"><span data-stu-id="30645-161">They are useful in diagnostics and performance monitoring.</span></span>
> 
> 

## <a name="debugging"></a><span data-ttu-id="30645-162">Depurando</span><span class="sxs-lookup"><span data-stu-id="30645-162">Debugging</span></span>
<span data-ttu-id="30645-163">ferramentas do Hello Service Fabric para Visual Studio oferece suporte à depuração no computador local.</span><span class="sxs-lookup"><span data-stu-id="30645-163">hello Service Fabric tools for Visual Studio support debugging on your local machine.</span></span> <span data-ttu-id="30645-164">Você pode iniciar uma sessão de depuração, atingindo Olá a tecla F5.</span><span class="sxs-lookup"><span data-stu-id="30645-164">You can start a debugging session by hitting hello F5 key.</span></span> <span data-ttu-id="30645-165">O Visual Studio cria (se necessário) pacotes.</span><span class="sxs-lookup"><span data-stu-id="30645-165">Visual Studio builds (if necessary) packages.</span></span> <span data-ttu-id="30645-166">Também implanta o aplicativo hello no cluster de malha do serviço local hello e anexa o depurador hello.</span><span class="sxs-lookup"><span data-stu-id="30645-166">It also deploys hello application on hello local Service Fabric cluster and attaches hello debugger.</span></span>

<span data-ttu-id="30645-167">Durante o processo de implantação Olá, você pode ver o progresso Olá no hello **saída** janela.</span><span class="sxs-lookup"><span data-stu-id="30645-167">During hello deployment process, you can see hello progress in hello **Output** window.</span></span>

![Janela de saída de depuração do Service Fabric][3]

## <a name="next-steps"></a><span data-ttu-id="30645-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="30645-169">Next steps</span></span>
<span data-ttu-id="30645-170">Saiba mais sobre [como Reliable Actors usar plataforma do Service Fabric Olá](service-fabric-reliable-actors-platform.md).</span><span class="sxs-lookup"><span data-stu-id="30645-170">Learn more about [how Reliable Actors use hello Service Fabric platform](service-fabric-reliable-actors-platform.md).</span></span>

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
