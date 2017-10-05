---
title: "Criar seu primeiro microsserviço do Azure baseado em ator em Java | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de criação, depuração e implantação de um serviço simples baseado em ator usando os Reliable Actors do Service Fabric."
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
ms.openlocfilehash: 288f1ed1016f50031065e66444d2562427194dc7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="5e135-103">Introdução aos Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="5e135-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5e135-104">C# em Windows</span><span class="sxs-lookup"><span data-stu-id="5e135-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="5e135-105">Java no Linux</span><span class="sxs-lookup"><span data-stu-id="5e135-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="5e135-106">Este artigo explica os conceitos básicos dos Reliable Actors do Azure Service Fabric e orienta você durante a criação e a implantação de um aplicativo Reliable Actor simples em Java.</span><span class="sxs-lookup"><span data-stu-id="5e135-106">This article explains the basics of Azure Service Fabric Reliable Actors and walks you through creating and deploying a simple Reliable Actor application in Java.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="5e135-107">Instalação e configuração</span><span class="sxs-lookup"><span data-stu-id="5e135-107">Installation and setup</span></span>
<span data-ttu-id="5e135-108">Antes de começar, verifique se há um ambiente de desenvolvimento do Service Fabric configurado no seu computador.</span><span class="sxs-lookup"><span data-stu-id="5e135-108">Before you start, make sure you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="5e135-109">Se precisar configurá-lo, vá para o [guia de introdução ao Mac](service-fabric-get-started-mac.md) ou o [guia de introdução ao Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5e135-109">If you need to set it up, go to [getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="5e135-110">Conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="5e135-110">Basic concepts</span></span>
<span data-ttu-id="5e135-111">Para começar a usar os Reliable Actors, você só precisa entender alguns conceitos básicos:</span><span class="sxs-lookup"><span data-stu-id="5e135-111">To get started with Reliable Actors, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="5e135-112">**Serviço do ator**.</span><span class="sxs-lookup"><span data-stu-id="5e135-112">**Actor service**.</span></span> <span data-ttu-id="5e135-113">Os Reliable Actors são empacotados em Reliable Services que podem ser implantados na infraestrutura do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5e135-113">Reliable Actors are packaged in Reliable Services that can be deployed in the Service Fabric infrastructure.</span></span> <span data-ttu-id="5e135-114">As instâncias de ator são ativadas em uma instância de serviço nomeado.</span><span class="sxs-lookup"><span data-stu-id="5e135-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="5e135-115">**Registro do ator**.</span><span class="sxs-lookup"><span data-stu-id="5e135-115">**Actor registration**.</span></span> <span data-ttu-id="5e135-116">Como ocorre com Reliable Services, um serviço de Reliable Actor precisa ser registrado com o tempo de execução do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5e135-116">As with Reliable Services, a Reliable Actor service needs to be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="5e135-117">Além disso, o tipo de ator precisa ser registrado com o tempo de execução do ator.</span><span class="sxs-lookup"><span data-stu-id="5e135-117">In addition, the actor type needs to be registered with the Actor runtime.</span></span>
* <span data-ttu-id="5e135-118">**Interface do Ator**.</span><span class="sxs-lookup"><span data-stu-id="5e135-118">**Actor interface**.</span></span> <span data-ttu-id="5e135-119">A interface do ator é usada para definir uma interface pública fortemente tipada de um ator.</span><span class="sxs-lookup"><span data-stu-id="5e135-119">The actor interface is used to define a strongly typed public interface of an actor.</span></span> <span data-ttu-id="5e135-120">Na terminologia do modelo de Reliable Actor, a interface do ator define os tipos de mensagem que o ator pode entender e processar.</span><span class="sxs-lookup"><span data-stu-id="5e135-120">In the Reliable Actor model terminology, the actor interface defines the types of messages that the actor can understand and process.</span></span> <span data-ttu-id="5e135-121">A interface do ator é usada por outros atores ou aplicativos cliente para “enviar” (de modo assíncrono) mensagens ao ator.</span><span class="sxs-lookup"><span data-stu-id="5e135-121">The actor interface is used by other actors and client applications to "send" (asynchronously) messages to the actor.</span></span> <span data-ttu-id="5e135-122">Os Reliable Actors pode implantar várias interfaces.</span><span class="sxs-lookup"><span data-stu-id="5e135-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="5e135-123">**Classe ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="5e135-123">**ActorProxy class**.</span></span> <span data-ttu-id="5e135-124">A classe ActorProxy é usada por aplicativos cliente para invocar os métodos expostos por meio de suas interfaces de ator.</span><span class="sxs-lookup"><span data-stu-id="5e135-124">The ActorProxy class is used by client applications to invoke the methods exposed through the actor interface.</span></span> <span data-ttu-id="5e135-125">A classe ActorProxy apresenta duas funcionalidades importantes:</span><span class="sxs-lookup"><span data-stu-id="5e135-125">The ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="5e135-126">Resolução do nome: ela consegue localizar o ator no cluster (localizar o nó do cluster no qual ele está hospedado).</span><span class="sxs-lookup"><span data-stu-id="5e135-126">Name resolution: It is able to locate the actor in the cluster (find the node of the cluster where it is hosted).</span></span>
  * <span data-ttu-id="5e135-127">Tratamento de falhas: ela pode repetir as invocações do método e resolver novamente o local do ator, por exemplo, depois que uma falha exige que ele seja relocado para outro nó no cluster.</span><span class="sxs-lookup"><span data-stu-id="5e135-127">Failure handling: It can retry method invocations and re-resolve the actor location after, for example, a failure that requires the actor to be relocated to another node in the cluster.</span></span>

<span data-ttu-id="5e135-128">Vale a pena mencionar as seguintes regras que pertencem às interfaces de ator:</span><span class="sxs-lookup"><span data-stu-id="5e135-128">The following rules that pertain to actor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="5e135-129">Métodos da interface de ator não podem ser sobrecarregados.</span><span class="sxs-lookup"><span data-stu-id="5e135-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="5e135-130">Métodos da interface de ator não podem ter parâmetros de saída, de referência e opcionais.</span><span class="sxs-lookup"><span data-stu-id="5e135-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="5e135-131">Não há suporte para interfaces genéricas.</span><span class="sxs-lookup"><span data-stu-id="5e135-131">Generic interfaces are not supported.</span></span>

## <a name="create-an-actor-service"></a><span data-ttu-id="5e135-132">Criar um serviço de ator</span><span class="sxs-lookup"><span data-stu-id="5e135-132">Create an actor service</span></span>
<span data-ttu-id="5e135-133">Comece criando um novo aplicativo de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5e135-133">Start by creating a new Service Fabric application.</span></span> <span data-ttu-id="5e135-134">O SDK do Service Fabric para Linux inclui um gerador Yeoman para fornecer o scaffolding de um aplicativo de Service Fabric com um serviço sem estado.</span><span class="sxs-lookup"><span data-stu-id="5e135-134">The Service Fabric SDK for Linux includes a Yeoman generator to provide the scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="5e135-135">Comece executando o seguinte comando Yeoman:</span><span class="sxs-lookup"><span data-stu-id="5e135-135">Start by running the following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="5e135-136">Siga as instruções para criar um **Serviço de Ator Confiável**.</span><span class="sxs-lookup"><span data-stu-id="5e135-136">Follow the instructions to create a **Reliable Actor Service**.</span></span> <span data-ttu-id="5e135-137">Para este tutorial, nomeie o aplicativo "HelloWorldActorApplication" e o ator "HelloWorldActor".</span><span class="sxs-lookup"><span data-stu-id="5e135-137">For this tutorial, name the application "HelloWorldActorApplication" and the actor "HelloWorldActor."</span></span> <span data-ttu-id="5e135-138">O scaffolding a seguir será criado:</span><span class="sxs-lookup"><span data-stu-id="5e135-138">The following scaffolding will be created:</span></span>

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

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="5e135-139">Blocos de construção básicos de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="5e135-139">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="5e135-140">Os conceitos básicos descritos anteriormente são convertidos em blocos de construção básicos de um serviço Reliable Actor.</span><span class="sxs-lookup"><span data-stu-id="5e135-140">The basic concepts described earlier translate into the basic building blocks of a Reliable Actor service.</span></span>

### <a name="actor-interface"></a><span data-ttu-id="5e135-141">Interface do ator</span><span class="sxs-lookup"><span data-stu-id="5e135-141">Actor interface</span></span>
<span data-ttu-id="5e135-142">Contém a definição da interface para o ator.</span><span class="sxs-lookup"><span data-stu-id="5e135-142">This contains the interface definition for the actor.</span></span> <span data-ttu-id="5e135-143">Essa interface define o contrato de ator que é compartilhado com a implementação do ator e os clientes chamando o ator, assim, geralmente faz sentido defini-lo em um local separado da implementação do ator e pode ser compartilhado por vários outros serviços ou aplicativos cliente.</span><span class="sxs-lookup"><span data-stu-id="5e135-143">This interface defines the actor contract that is shared by the actor implementation and the clients calling the actor, so it typically makes sense to define it in a place that is separate from the actor implementation and can be shared by multiple other services or client applications.</span></span>

<span data-ttu-id="5e135-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span><span class="sxs-lookup"><span data-stu-id="5e135-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span></span>

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a><span data-ttu-id="5e135-145">Serviço de ator</span><span class="sxs-lookup"><span data-stu-id="5e135-145">Actor service</span></span>
<span data-ttu-id="5e135-146">Contém a implementação do ator e o código de registro do ator.</span><span class="sxs-lookup"><span data-stu-id="5e135-146">This contains your actor implementation and actor registration code.</span></span> <span data-ttu-id="5e135-147">A classe de ator implementa a interface do ator.</span><span class="sxs-lookup"><span data-stu-id="5e135-147">The actor class implements the actor interface.</span></span> <span data-ttu-id="5e135-148">É o local em que o ator faz seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="5e135-148">This is where your actor does its work.</span></span>

<span data-ttu-id="5e135-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span><span class="sxs-lookup"><span data-stu-id="5e135-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span></span>

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

### <a name="actor-registration"></a><span data-ttu-id="5e135-150">Registro do ator</span><span class="sxs-lookup"><span data-stu-id="5e135-150">Actor registration</span></span>
<span data-ttu-id="5e135-151">O serviço de ator deve ser registrado com um tipo de serviço no tempo de execução do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5e135-151">The actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="5e135-152">Para que o Serviço de Ator seja executado em suas instâncias de ator, o tipo de ator também deve ser registrado no Serviço de Ator.</span><span class="sxs-lookup"><span data-stu-id="5e135-152">In order for the Actor Service to run your actor instances, your actor type must also be registered with the Actor Service.</span></span> <span data-ttu-id="5e135-153">O método de registro `ActorRuntime` realiza esse trabalho para os atores.</span><span class="sxs-lookup"><span data-stu-id="5e135-153">The `ActorRuntime` registration method performs this work for actors.</span></span>

<span data-ttu-id="5e135-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span><span class="sxs-lookup"><span data-stu-id="5e135-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span></span>

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

### <a name="test-client"></a><span data-ttu-id="5e135-155">Cliente de teste</span><span class="sxs-lookup"><span data-stu-id="5e135-155">Test client</span></span>
<span data-ttu-id="5e135-156">Este é um aplicativo de cliente de teste simples pode ser executado separadamente do aplicativo do Service Fabric para testar o serviço de ator.</span><span class="sxs-lookup"><span data-stu-id="5e135-156">This is a simple test client application you can run separately from the Service Fabric application to test your actor service.</span></span> <span data-ttu-id="5e135-157">Este é um exemplo de local em que o ActorProxy pode ser usado para ativar e comunicar-se com instâncias de ator.</span><span class="sxs-lookup"><span data-stu-id="5e135-157">This is an example of where the ActorProxy can be used to activate and communicate with actor instances.</span></span> <span data-ttu-id="5e135-158">Ele não é implantado com seu serviço.</span><span class="sxs-lookup"><span data-stu-id="5e135-158">It does not get deployed with your service.</span></span>

### <a name="the-application"></a><span data-ttu-id="5e135-159">O aplicativo</span><span class="sxs-lookup"><span data-stu-id="5e135-159">The application</span></span>
<span data-ttu-id="5e135-160">Por fim, o aplicativo empacota junto o serviço de ator e quaisquer outros serviços que você possa adicionar no futuro para implantação.</span><span class="sxs-lookup"><span data-stu-id="5e135-160">Finally, the application packages the actor service and any other services you might add in the future together for deployment.</span></span> <span data-ttu-id="5e135-161">Ele contém o *ApplicationManifest.xml* e espaços reservados para o pacote de serviço do ator.</span><span class="sxs-lookup"><span data-stu-id="5e135-161">It contains the *ApplicationManifest.xml* and place holders for the actor service package.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="5e135-162">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="5e135-162">Run the application</span></span>

<span data-ttu-id="5e135-163">O scaffolding Yeoman inclui um script gradle para compilar o aplicativo e os scripts bash para implantar e remover o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5e135-163">The Yeoman scaffolding includes a gradle script to build the application and bash scripts to deploy and remove the application.</span></span> <span data-ttu-id="5e135-164">Para implantar o aplicativo, primeiro compile o aplicativo com gradle:</span><span class="sxs-lookup"><span data-stu-id="5e135-164">To deploy the application, first build the application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="5e135-165">Isso produzirá um pacote de aplicativos do Service Fabric que poderá ser implantado usando ferramentas de CLI do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5e135-165">This will produce a Service Fabric application package that can be deployed using Service Fabric CLI tools.</span></span>

### <a name="deploy-service-fabric-cli"></a><span data-ttu-id="5e135-166">Implantar a CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5e135-166">Deploy Service Fabric CLI</span></span>

<span data-ttu-id="5e135-167">O script install.sh contém os comandos da CLI do Service Fabric (sfctl) necessários para implantar o pacote de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="5e135-167">The install.sh script contains the necessary Service Fabric CLI (sfctl) commands to deploy the application package.</span></span>
<span data-ttu-id="5e135-168">Execute o script install.sh para implantar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5e135-168">Run the install.sh script to deploy the application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="5e135-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5e135-169">Next steps</span></span>

* [<span data-ttu-id="5e135-170">Introdução à CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5e135-170">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
