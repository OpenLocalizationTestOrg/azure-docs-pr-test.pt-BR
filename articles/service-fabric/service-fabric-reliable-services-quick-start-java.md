---
title: "aaaCreate seu primeiro microsserviço confiável do Azure em Java | Microsoft Docs"
description: "Introdução toocreating um aplicativo do Microsoft Azure Service Fabric com serviços com e sem monitoração de estado."
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: 
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 577d96591797bbfe6be5c1094426b5f1435cca0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="54f82-103">Introdução aos Reliable Services</span><span class="sxs-lookup"><span data-stu-id="54f82-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="54f82-104">C# em Windows</span><span class="sxs-lookup"><span data-stu-id="54f82-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="54f82-105">Java no Linux</span><span class="sxs-lookup"><span data-stu-id="54f82-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
>
>

<span data-ttu-id="54f82-106">Este artigo explica conceitos básicos de saudação dos serviços do Azure Service Fabric confiável e ajuda você a criar e implantar um aplicativo de serviço confiável simples escrito em Java.</span><span class="sxs-lookup"><span data-stu-id="54f82-106">This article explains hello basics of Azure Service Fabric Reliable Services and walks you through creating and deploying a simple Reliable Service application written in Java.</span></span> <span data-ttu-id="54f82-107">Este vídeo Microsoft Virtual Academy também mostra como toocreate um serviço confiável sem monitoração de estado:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span><span class="sxs-lookup"><span data-stu-id="54f82-107">This Microsoft Virtual Academy video also shows you how toocreate a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a><span data-ttu-id="54f82-108">Instalação e configuração</span><span class="sxs-lookup"><span data-stu-id="54f82-108">Installation and setup</span></span>
<span data-ttu-id="54f82-109">Antes de começar, certifique-se de que o ambiente de desenvolvimento do Service Fabric Olá configurado no seu computador.</span><span class="sxs-lookup"><span data-stu-id="54f82-109">Before you start, make sure you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="54f82-110">Se você precisar tooset-lo, vá muito[guia de Introdução no Mac](service-fabric-get-started-mac.md) ou [guia de Introdução no Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="54f82-110">If you need tooset it up, go too[getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="54f82-111">Conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="54f82-111">Basic concepts</span></span>
<span data-ttu-id="54f82-112">tooget iniciado com serviços confiáveis, você só precisa toounderstand alguns conceitos básicos:</span><span class="sxs-lookup"><span data-stu-id="54f82-112">tooget started with Reliable Services, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="54f82-113">**Tipo de serviço**: esta é sua implementação de serviço.</span><span class="sxs-lookup"><span data-stu-id="54f82-113">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="54f82-114">Ele é definido pela classe Olá gravar que estende `StatelessService` e qualquer outro código ou dependências usadas neste documento, juntamente com um nome e um número de versão.</span><span class="sxs-lookup"><span data-stu-id="54f82-114">It is defined by hello class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="54f82-115">**Serviço de instância nomeada**: toorun seu serviço, você cria instâncias nomeadas do seu tipo de serviço, bem como criar instâncias de objeto de um tipo de classe.</span><span class="sxs-lookup"><span data-stu-id="54f82-115">**Named service instance**: toorun your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="54f82-116">Instâncias de serviço são, na verdade, as instâncias de objeto de sua classe de serviço que você escreve.</span><span class="sxs-lookup"><span data-stu-id="54f82-116">Service instances are in fact object instantiations of your service class that you write.</span></span>
* <span data-ttu-id="54f82-117">**Host de serviço**: Olá denominado criar necessidade toorun dentro de um host de instâncias de serviço.</span><span class="sxs-lookup"><span data-stu-id="54f82-117">**Service host**: hello named service instances you create need toorun inside a host.</span></span> <span data-ttu-id="54f82-118">host de serviço Olá é apenas um processo em que as instâncias do serviço podem executar.</span><span class="sxs-lookup"><span data-stu-id="54f82-118">hello service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="54f82-119">**Registro de serviço**: o registro reúne tudo.</span><span class="sxs-lookup"><span data-stu-id="54f82-119">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="54f82-120">Olá service type deve ser registrado com hello Service Fabric em tempo de execução em um serviço de hospedar instâncias de toocreate Service Fabric tooallow-toorun.</span><span class="sxs-lookup"><span data-stu-id="54f82-120">hello service type must be registered with hello Service Fabric runtime in a service host tooallow Service Fabric toocreate instances of it toorun.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="54f82-121">Criar um serviço sem estado</span><span class="sxs-lookup"><span data-stu-id="54f82-121">Create a stateless service</span></span>
<span data-ttu-id="54f82-122">Comece criando um aplicativo de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="54f82-122">Start by creating a Service Fabric application.</span></span> <span data-ttu-id="54f82-123">Olá SDK do Service Fabric para Linux inclui um Yeoman scaffolding de saudação do gerador tooprovide para um aplicativo de malha do serviço com um serviço sem monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="54f82-123">hello Service Fabric SDK for Linux includes a Yeoman generator tooprovide hello scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="54f82-124">Inicie executando Olá Yeoman a seguir de comando:</span><span class="sxs-lookup"><span data-stu-id="54f82-124">Start by running hello following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="54f82-125">Siga Olá instruções toocreate um **serviço sem monitoração de estado confiável**.</span><span class="sxs-lookup"><span data-stu-id="54f82-125">Follow hello instructions toocreate a **Reliable Stateless Service**.</span></span> <span data-ttu-id="54f82-126">Para este tutorial, o aplicativo hello de nome "HelloWorldApplication" e Olá serviço "Olámundo".</span><span class="sxs-lookup"><span data-stu-id="54f82-126">For this tutorial, name hello application "HelloWorldApplication" and hello service "HelloWorld".</span></span> <span data-ttu-id="54f82-127">saudação de resultados inclui diretórios para Olá `HelloWorldApplication` e `HelloWorld`.</span><span class="sxs-lookup"><span data-stu-id="54f82-127">hello result includes directories for hello `HelloWorldApplication` and `HelloWorld`.</span></span>

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="implement-hello-service"></a><span data-ttu-id="54f82-128">Implementar o serviço de saudação</span><span class="sxs-lookup"><span data-stu-id="54f82-128">Implement hello service</span></span>
<span data-ttu-id="54f82-129">Abra **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span><span class="sxs-lookup"><span data-stu-id="54f82-129">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span></span> <span data-ttu-id="54f82-130">Essa classe define o tipo de serviço hello e pode executar qualquer código.</span><span class="sxs-lookup"><span data-stu-id="54f82-130">This class defines hello service type, and can run any code.</span></span> <span data-ttu-id="54f82-131">API do serviço de saudação oferece dois pontos de entrada para o seu código:</span><span class="sxs-lookup"><span data-stu-id="54f82-131">hello service API provides two entry points for your code:</span></span>

* <span data-ttu-id="54f82-132">Um método de ponto de entrada em aberto chamado `runAsync()`, em que você pode começar a executar qualquer carga de trabalho, incluindo cargas de trabalho de computação de longa duração.</span><span class="sxs-lookup"><span data-stu-id="54f82-132">An open-ended entry point method, called `runAsync()`, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* <span data-ttu-id="54f82-133">Um ponto de entrada de comunicação no qual você pode conectar a pilha de comunicação de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="54f82-133">A communication entry point where you can plug in your communication stack of choice.</span></span> <span data-ttu-id="54f82-134">É onde você pode começar a receber solicitações de usuários e outros serviços.</span><span class="sxs-lookup"><span data-stu-id="54f82-134">This is where you can start receiving requests from users and other services.</span></span>

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

<span data-ttu-id="54f82-135">Neste tutorial, vamos nos concentrar em Olá `runAsync()` método de ponto de entrada.</span><span class="sxs-lookup"><span data-stu-id="54f82-135">In this tutorial, we focus on hello `runAsync()` entry point method.</span></span> <span data-ttu-id="54f82-136">É aqui que você pode começar imediatamente a executar seu código.</span><span class="sxs-lookup"><span data-stu-id="54f82-136">This is where you can immediately start running your code.</span></span>

### <a name="runasync"></a><span data-ttu-id="54f82-137">RunAsync</span><span class="sxs-lookup"><span data-stu-id="54f82-137">RunAsync</span></span>
<span data-ttu-id="54f82-138">plataforma de saudação chama este método quando uma instância de um serviço é tooexecute inserida e pronto.</span><span class="sxs-lookup"><span data-stu-id="54f82-138">hello platform calls this method when an instance of a service is placed and ready tooexecute.</span></span> <span data-ttu-id="54f82-139">Para um serviço sem monitoração de estado, que simplesmente significa que quando a instância do serviço de saudação é aberta.</span><span class="sxs-lookup"><span data-stu-id="54f82-139">For a stateless service, that simply means when hello service instance is opened.</span></span> <span data-ttu-id="54f82-140">Um token de cancelamento é fornecido toocoordinate quando toobe fechado as necessidades de sua instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="54f82-140">A cancellation token is provided toocoordinate when your service instance needs toobe closed.</span></span> <span data-ttu-id="54f82-141">Na malha do serviço, esse ciclo de abertura/fechamento de uma instância de serviço pode ocorrer muitas vezes em tempo de vida de saudação do serviço hello como um todo.</span><span class="sxs-lookup"><span data-stu-id="54f82-141">In Service Fabric, this open/close cycle of a service instance can occur many times over hello lifetime of hello service as a whole.</span></span> <span data-ttu-id="54f82-142">Isso pode ocorrer por vários motivos, incluindo:</span><span class="sxs-lookup"><span data-stu-id="54f82-142">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="54f82-143">sistema de saudação move suas instâncias de serviço de balanceamento de recursos.</span><span class="sxs-lookup"><span data-stu-id="54f82-143">hello system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="54f82-144">Ocorrem falhas no código.</span><span class="sxs-lookup"><span data-stu-id="54f82-144">Faults occur in your code.</span></span>
* <span data-ttu-id="54f82-145">aplicativo Hello ou o sistema é atualizado.</span><span class="sxs-lookup"><span data-stu-id="54f82-145">hello application or system is upgraded.</span></span>
* <span data-ttu-id="54f82-146">hardware subjacente Olá sofrer uma interrupção.</span><span class="sxs-lookup"><span data-stu-id="54f82-146">hello underlying hardware experiences an outage.</span></span>

<span data-ttu-id="54f82-147">Essa orquestração é gerenciada pelo Service Fabric tookeep seu serviço altamente disponível e adequadamente equilibrado.</span><span class="sxs-lookup"><span data-stu-id="54f82-147">This orchestration is managed by Service Fabric tookeep your service highly available and properly balanced.</span></span>

<span data-ttu-id="54f82-148">`runAsync()` não deve bloquear sincronicamente.</span><span class="sxs-lookup"><span data-stu-id="54f82-148">`runAsync()` should not block synchronously.</span></span> <span data-ttu-id="54f82-149">A implementação de runAsync deve retornar um toocontinue de tempo de execução CompletableFuture tooallow hello.</span><span class="sxs-lookup"><span data-stu-id="54f82-149">Your implementation of runAsync should return a CompletableFuture tooallow hello runtime toocontinue.</span></span> <span data-ttu-id="54f82-150">Se sua carga de trabalho precisa de uma tarefa demorada que deve ser feita dentro de tooimplement Olá CompletableFuture.</span><span class="sxs-lookup"><span data-stu-id="54f82-150">If your workload needs tooimplement a long running task that should be done inside hello CompletableFuture.</span></span>

#### <a name="cancellation"></a><span data-ttu-id="54f82-151">Cancelamento</span><span class="sxs-lookup"><span data-stu-id="54f82-151">Cancellation</span></span>
<span data-ttu-id="54f82-152">O cancelamento da sua carga de trabalho é um esforço cooperativo orquestrado pelo Olá fornecido um token de cancelamento.</span><span class="sxs-lookup"><span data-stu-id="54f82-152">Cancellation of your workload is a cooperative effort orchestrated by hello provided cancellation token.</span></span> <span data-ttu-id="54f82-153">sistema de Olá aguarda sua tarefa tooend (pela conclusão bem-sucedida, cancelamento ou falha) antes de ele prossegue.</span><span class="sxs-lookup"><span data-stu-id="54f82-153">hello system waits for your task tooend (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="54f82-154">É importante toohonor Olá cancelamento token, concluir qualquer trabalho e sair `runAsync()` assim que possível quando o sistema Olá solicitações de cancelamento.</span><span class="sxs-lookup"><span data-stu-id="54f82-154">It is important toohonor hello cancellation token, finish any work, and exit `runAsync()` as quickly as possible when hello system requests cancellation.</span></span> <span data-ttu-id="54f82-155">Olá exemplo a seguir demonstra como um evento de cancelamento de toohandle:</span><span class="sxs-lookup"><span data-stu-id="54f82-155">hello following example demonstrates how toohandle a cancellation event:</span></span>

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace hello following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a><span data-ttu-id="54f82-156">Registro do serviço</span><span class="sxs-lookup"><span data-stu-id="54f82-156">Service registration</span></span>
<span data-ttu-id="54f82-157">Tipos de serviço devem ser registrados com o tempo de execução do hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="54f82-157">Service types must be registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="54f82-158">tipo de serviço de saudação é definido em Olá `ServiceManifest.xml` e sua classe de serviço implementa `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="54f82-158">hello service type is defined in hello `ServiceManifest.xml` and your service class that implements `StatelessService`.</span></span> <span data-ttu-id="54f82-159">Registro de serviço é executado no ponto de entrada principal do processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="54f82-159">Service registration is performed in hello process main entry point.</span></span> <span data-ttu-id="54f82-160">Neste exemplo, Olá o processo de ponto de entrada principal é `HelloWorldServiceHost.java`:</span><span class="sxs-lookup"><span data-stu-id="54f82-160">In this example, hello process main entry point is `HelloWorldServiceHost.java`:</span></span>

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="run-hello-application"></a><span data-ttu-id="54f82-161">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="54f82-161">Run hello application</span></span>

<span data-ttu-id="54f82-162">Olá Yeoman scaffolding inclui um gradle script toobuild Olá aplicativo e bash scripts toodeploy e remover o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="54f82-162">hello Yeoman scaffolding includes a gradle script toobuild hello application and bash scripts toodeploy and remove the application.</span></span> <span data-ttu-id="54f82-163">aplicativo de hello toorun, primeiro aplicativo hello de compilação com gradle:</span><span class="sxs-lookup"><span data-stu-id="54f82-163">toorun hello application, first build hello application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="54f82-164">Isso produz um pacote de aplicativos do Service Fabric que poderá ser implantado usando a CLI do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="54f82-164">This produces a Service Fabric application package that can be deployed using Service Fabric CLI.</span></span>

### <a name="deploy-with-service-fabric-cli"></a><span data-ttu-id="54f82-165">Implantar com a CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="54f82-165">Deploy with Service Fabric CLI</span></span>

<span data-ttu-id="54f82-166">script de install.sh de Olá contém Olá necessário CLI de malha do serviço comandos toodeploy Olá pacote de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="54f82-166">hello install.sh script contains hello necessary Service Fabric CLI commands toodeploy hello application package.</span></span> <span data-ttu-id="54f82-167">Execute o aplicativo de hello toodeploy install.sh script.</span><span class="sxs-lookup"><span data-stu-id="54f82-167">Run the install.sh script toodeploy hello application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="54f82-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="54f82-168">Next steps</span></span>

* [<span data-ttu-id="54f82-169">Introdução à CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="54f82-169">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
