---
title: "aaaCreate sua primeira baseado em ator Azure microsserviço em Java | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de saudação de criar, depurar e implantar um serviço baseado em ator simples usando o serviço de malha Reliable Actors."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: 24718a8d7034360c53597f139169580f1a6ce732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="eac79-103">Introdução aos Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="eac79-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eac79-104">C# em Windows</span><span class="sxs-lookup"><span data-stu-id="eac79-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="eac79-105">Java no Linux</span><span class="sxs-lookup"><span data-stu-id="eac79-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="eac79-106">Este artigo explica as Noções básicas de saudação do Azure Service Fabric Reliable Actors e orienta você a criar e implantar um aplicativo simples de Reliable Actor em Java.</span><span class="sxs-lookup"><span data-stu-id="eac79-106">This article explains hello basics of Azure Service Fabric Reliable Actors and walks you through creating and deploying a simple Reliable Actor application in Java.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="eac79-107">Instalação e configuração</span><span class="sxs-lookup"><span data-stu-id="eac79-107">Installation and setup</span></span>
<span data-ttu-id="eac79-108">Antes de começar, certifique-se de que o ambiente de desenvolvimento do Service Fabric Olá configurado no seu computador.</span><span class="sxs-lookup"><span data-stu-id="eac79-108">Before you start, make sure you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="eac79-109">Se você precisar tooset-lo, vá muito[guia de Introdução no Mac](service-fabric-get-started-mac.md) ou [guia de Introdução no Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="eac79-109">If you need tooset it up, go too[getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="eac79-110">Conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="eac79-110">Basic concepts</span></span>
<span data-ttu-id="eac79-111">tooget iniciado com atores confiável, você só precisa toounderstand alguns conceitos básicos:</span><span class="sxs-lookup"><span data-stu-id="eac79-111">tooget started with Reliable Actors, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="eac79-112">**Serviço do ator**.</span><span class="sxs-lookup"><span data-stu-id="eac79-112">**Actor service**.</span></span> <span data-ttu-id="eac79-113">Confiáveis atores são empacotados em serviços confiáveis que podem ser implantados na infraestrutura de malha do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="eac79-113">Reliable Actors are packaged in Reliable Services that can be deployed in hello Service Fabric infrastructure.</span></span> <span data-ttu-id="eac79-114">As instâncias de ator são ativadas em uma instância de serviço nomeado.</span><span class="sxs-lookup"><span data-stu-id="eac79-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="eac79-115">**Registro do ator**.</span><span class="sxs-lookup"><span data-stu-id="eac79-115">**Actor registration**.</span></span> <span data-ttu-id="eac79-116">Como com serviços confiáveis, um serviço de Reliable Actor deve toobe registrado com o tempo de execução do hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="eac79-116">As with Reliable Services, a Reliable Actor service needs toobe registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="eac79-117">Além disso, o tipo de ator Olá precisa toobe registrado com o tempo de execução do hello ator.</span><span class="sxs-lookup"><span data-stu-id="eac79-117">In addition, hello actor type needs toobe registered with hello Actor runtime.</span></span>
* <span data-ttu-id="eac79-118">**Interface do Ator**.</span><span class="sxs-lookup"><span data-stu-id="eac79-118">**Actor interface**.</span></span> <span data-ttu-id="eac79-119">interface de ator Olá é usado toodefine uma interface pública fortemente tipada de um ator.</span><span class="sxs-lookup"><span data-stu-id="eac79-119">hello actor interface is used toodefine a strongly typed public interface of an actor.</span></span> <span data-ttu-id="eac79-120">No hello terminologia do modelo confiável ator, interface de ator Olá define Olá tipos de mensagens que Olá ator podem entender e processar.</span><span class="sxs-lookup"><span data-stu-id="eac79-120">In hello Reliable Actor model terminology, hello actor interface defines hello types of messages that hello actor can understand and process.</span></span> <span data-ttu-id="eac79-121">interface de ator Olá é usado por outros atores e aplicativos cliente muito "enviam" (de forma assíncrona) ator de toohello de mensagens.</span><span class="sxs-lookup"><span data-stu-id="eac79-121">hello actor interface is used by other actors and client applications too"send" (asynchronously) messages toohello actor.</span></span> <span data-ttu-id="eac79-122">Os Reliable Actors pode implantar várias interfaces.</span><span class="sxs-lookup"><span data-stu-id="eac79-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="eac79-123">**Classe ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="eac79-123">**ActorProxy class**.</span></span> <span data-ttu-id="eac79-124">Olá ActorProxy classe é usada pelo cliente aplicativos tooinvoke Olá métodos expostos pela interface de ator hello.</span><span class="sxs-lookup"><span data-stu-id="eac79-124">hello ActorProxy class is used by client applications tooinvoke hello methods exposed through hello actor interface.</span></span> <span data-ttu-id="eac79-125">Olá ActorProxy classe fornece dois recursos importantes:</span><span class="sxs-lookup"><span data-stu-id="eac79-125">hello ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="eac79-126">A resolução de nome: é toolocate capaz de ator de saudação em cluster hello (localizar o nó de saudação do cluster de saudação onde ele está hospedado).</span><span class="sxs-lookup"><span data-stu-id="eac79-126">Name resolution: It is able toolocate hello actor in hello cluster (find hello node of hello cluster where it is hosted).</span></span>
  * <span data-ttu-id="eac79-127">Tratamento de falha: pode repetir invocações de método e resolver o local de ator Olá após novamente, por exemplo, uma falha que exija Olá ator toobe realocado tooanother nó no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="eac79-127">Failure handling: It can retry method invocations and re-resolve hello actor location after, for example, a failure that requires hello actor toobe relocated tooanother node in hello cluster.</span></span>

<span data-ttu-id="eac79-128">Olá, seguindo as regras que pertencem a interfaces tooactor é vale a pena mencionar:</span><span class="sxs-lookup"><span data-stu-id="eac79-128">hello following rules that pertain tooactor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="eac79-129">Métodos da interface de ator não podem ser sobrecarregados.</span><span class="sxs-lookup"><span data-stu-id="eac79-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="eac79-130">Métodos da interface de ator não podem ter parâmetros de saída, de referência e opcionais.</span><span class="sxs-lookup"><span data-stu-id="eac79-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="eac79-131">Não há suporte para interfaces genéricas.</span><span class="sxs-lookup"><span data-stu-id="eac79-131">Generic interfaces are not supported.</span></span>

## <a name="create-an-actor-service"></a><span data-ttu-id="eac79-132">Criar um serviço de ator</span><span class="sxs-lookup"><span data-stu-id="eac79-132">Create an actor service</span></span>
<span data-ttu-id="eac79-133">Comece criando um novo aplicativo de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="eac79-133">Start by creating a new Service Fabric application.</span></span> <span data-ttu-id="eac79-134">Olá SDK do Service Fabric para Linux inclui um Yeoman scaffolding de saudação do gerador tooprovide para um aplicativo de malha do serviço com um serviço sem monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="eac79-134">hello Service Fabric SDK for Linux includes a Yeoman generator tooprovide hello scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="eac79-135">Inicie executando Olá Yeoman a seguir de comando:</span><span class="sxs-lookup"><span data-stu-id="eac79-135">Start by running hello following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="eac79-136">Siga Olá instruções toocreate um **serviço de ator confiável**.</span><span class="sxs-lookup"><span data-stu-id="eac79-136">Follow hello instructions toocreate a **Reliable Actor Service**.</span></span> <span data-ttu-id="eac79-137">Neste tutorial, nomeie Olá aplicativo "HelloWorldActorApplication" e hello ator "HelloWorldActor".</span><span class="sxs-lookup"><span data-stu-id="eac79-137">For this tutorial, name hello application "HelloWorldActorApplication" and hello actor "HelloWorldActor."</span></span> <span data-ttu-id="eac79-138">Olá scaffolding a seguir será criado:</span><span class="sxs-lookup"><span data-stu-id="eac79-138">hello following scaffolding will be created:</span></span>

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="eac79-139">Blocos de construção básicos de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="eac79-139">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="eac79-140">conceitos básicos de saudação descritos anteriormente traduzem em Olá blocos de construção básicos de um serviço de Reliable Actor.</span><span class="sxs-lookup"><span data-stu-id="eac79-140">hello basic concepts described earlier translate into hello basic building blocks of a Reliable Actor service.</span></span>

### <a name="actor-interface"></a><span data-ttu-id="eac79-141">Interface do ator</span><span class="sxs-lookup"><span data-stu-id="eac79-141">Actor interface</span></span>
<span data-ttu-id="eac79-142">Isso contém a definição de interface de saudação de ator hello.</span><span class="sxs-lookup"><span data-stu-id="eac79-142">This contains hello interface definition for hello actor.</span></span> <span data-ttu-id="eac79-143">Essa interface define o contrato de ator de saudação que é compartilhado por clientes de Olá chamando ator hello, então, geralmente faz sentido toodefine-lo em um local que é separar da implementação de ator hello e pode ser compartilhado por vários outros e implementação de ator Olá serviços ou aplicativos cliente.</span><span class="sxs-lookup"><span data-stu-id="eac79-143">This interface defines hello actor contract that is shared by hello actor implementation and hello clients calling hello actor, so it typically makes sense toodefine it in a place that is separate from hello actor implementation and can be shared by multiple other services or client applications.</span></span>

<span data-ttu-id="eac79-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span><span class="sxs-lookup"><span data-stu-id="eac79-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span></span>

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a><span data-ttu-id="eac79-145">Serviço de ator</span><span class="sxs-lookup"><span data-stu-id="eac79-145">Actor service</span></span>
<span data-ttu-id="eac79-146">Contém a implementação do ator e o código de registro do ator.</span><span class="sxs-lookup"><span data-stu-id="eac79-146">This contains your actor implementation and actor registration code.</span></span> <span data-ttu-id="eac79-147">classe de ator Olá implementa a interface de ator do hello.</span><span class="sxs-lookup"><span data-stu-id="eac79-147">hello actor class implements hello actor interface.</span></span> <span data-ttu-id="eac79-148">É o local em que o ator faz seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="eac79-148">This is where your actor does its work.</span></span>

<span data-ttu-id="eac79-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span><span class="sxs-lookup"><span data-stu-id="eac79-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span></span>

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a><span data-ttu-id="eac79-150">Registro do ator</span><span class="sxs-lookup"><span data-stu-id="eac79-150">Actor registration</span></span>
<span data-ttu-id="eac79-151">serviço de ator Olá deve ser registrado com um tipo de serviço em tempo de execução do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="eac79-151">hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="eac79-152">Em ordem para Olá toorun do serviço de ator suas instâncias de ator, seu tipo de ator também deve ser registrado com hello serviço de ator.</span><span class="sxs-lookup"><span data-stu-id="eac79-152">In order for hello Actor Service toorun your actor instances, your actor type must also be registered with hello Actor Service.</span></span> <span data-ttu-id="eac79-153">Olá `ActorRuntime` método de registro executa essa tarefa para atores.</span><span class="sxs-lookup"><span data-stu-id="eac79-153">hello `ActorRuntime` registration method performs this work for actors.</span></span>

<span data-ttu-id="eac79-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span><span class="sxs-lookup"><span data-stu-id="eac79-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span></span>

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a><span data-ttu-id="eac79-155">Cliente de teste</span><span class="sxs-lookup"><span data-stu-id="eac79-155">Test client</span></span>
<span data-ttu-id="eac79-156">Este é um aplicativo de cliente de teste simples você pode executar separadamente de saudação do Service Fabric application tootest seu serviço de ator.</span><span class="sxs-lookup"><span data-stu-id="eac79-156">This is a simple test client application you can run separately from hello Service Fabric application tootest your actor service.</span></span> <span data-ttu-id="eac79-157">Este é um exemplo de onde hello ActorProxy pode ser usado tooactivate e se comunicar com instâncias de ator.</span><span class="sxs-lookup"><span data-stu-id="eac79-157">This is an example of where hello ActorProxy can be used tooactivate and communicate with actor instances.</span></span> <span data-ttu-id="eac79-158">Ele não é implantado com seu serviço.</span><span class="sxs-lookup"><span data-stu-id="eac79-158">It does not get deployed with your service.</span></span>

### <a name="hello-application"></a><span data-ttu-id="eac79-159">aplicativo Hello</span><span class="sxs-lookup"><span data-stu-id="eac79-159">hello application</span></span>
<span data-ttu-id="eac79-160">Por fim, pacotes de aplicativos Olá Olá serviço ator e qualquer outro serviço que você pode adicionar em Olá futura juntas para implantação.</span><span class="sxs-lookup"><span data-stu-id="eac79-160">Finally, hello application packages hello actor service and any other services you might add in hello future together for deployment.</span></span> <span data-ttu-id="eac79-161">Ele contém Olá *ApplicationManifest.xml* e espaços reservados para o pacote de serviço de ator hello.</span><span class="sxs-lookup"><span data-stu-id="eac79-161">It contains hello *ApplicationManifest.xml* and place holders for hello actor service package.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="eac79-162">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="eac79-162">Run hello application</span></span>

<span data-ttu-id="eac79-163">Olá Yeoman scaffolding inclui um gradle script toobuild Olá aplicativo e bash scripts toodeploy e remover o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eac79-163">hello Yeoman scaffolding includes a gradle script toobuild hello application and bash scripts toodeploy and remove the application.</span></span> <span data-ttu-id="eac79-164">aplicativo de hello toodeploy, primeiro aplicativo hello de compilação com gradle:</span><span class="sxs-lookup"><span data-stu-id="eac79-164">toodeploy hello application, first build hello application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="eac79-165">Isso produzirá um pacote de aplicativos do Service Fabric que poderá ser implantado usando ferramentas de CLI do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="eac79-165">This will produce a Service Fabric application package that can be deployed using Service Fabric CLI tools.</span></span>

### <a name="deploy-service-fabric-cli"></a><span data-ttu-id="eac79-166">Implantar a CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="eac79-166">Deploy Service Fabric CLI</span></span>

<span data-ttu-id="eac79-167">script de install.sh de Olá contém Olá necessário CLI de malha do serviço (sfctl) comandos toodeploy Olá pacote de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eac79-167">hello install.sh script contains hello necessary Service Fabric CLI (sfctl) commands toodeploy hello application package.</span></span>
<span data-ttu-id="eac79-168">Execute o aplicativo de saudação do hello install.sh script toodeploy.</span><span class="sxs-lookup"><span data-stu-id="eac79-168">Run hello install.sh script toodeploy hello application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="eac79-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eac79-169">Next steps</span></span>

* [<span data-ttu-id="eac79-170">Introdução à CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="eac79-170">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
