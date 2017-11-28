---
title: "Criar seu primeiro microsserviço confiável do Azure em Java | Microsoft Docs"
description: "Introdução à criação de um aplicativo do Service Fabric do Microsoft Azure com serviços com e sem estado."
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
ms.openlocfilehash: 1ebabe4844732412e04bab8c277f7ebbc4a5737c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="8aaec-103">Introdução aos Reliable Services</span><span class="sxs-lookup"><span data-stu-id="8aaec-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8aaec-104">C# em Windows</span><span class="sxs-lookup"><span data-stu-id="8aaec-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="8aaec-105">Java no Linux</span><span class="sxs-lookup"><span data-stu-id="8aaec-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
>
>

<span data-ttu-id="8aaec-106">Este artigo explica os conceitos básicos dos Reliable Services do Azure Service Fabric e o orienta você durante a criação e a implantação de um aplicativo Reliable Service simples escrito em Java.</span><span class="sxs-lookup"><span data-stu-id="8aaec-106">This article explains the basics of Azure Service Fabric Reliable Services and walks you through creating and deploying a simple Reliable Service application written in Java.</span></span> <span data-ttu-id="8aaec-107">Este vídeo da Microsoft Virtual Academy mostra como criar um serviço confiável sem estado: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span><span class="sxs-lookup"><span data-stu-id="8aaec-107">This Microsoft Virtual Academy video also shows you how to create a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a><span data-ttu-id="8aaec-108">Instalação e configuração</span><span class="sxs-lookup"><span data-stu-id="8aaec-108">Installation and setup</span></span>
<span data-ttu-id="8aaec-109">Antes de começar, verifique se há um ambiente de desenvolvimento do Service Fabric configurado no seu computador.</span><span class="sxs-lookup"><span data-stu-id="8aaec-109">Before you start, make sure you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="8aaec-110">Se precisar configurá-lo, vá para o [guia de introdução ao Mac](service-fabric-get-started-mac.md) ou o [guia de introdução ao Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="8aaec-110">If you need to set it up, go to [getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="8aaec-111">Conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="8aaec-111">Basic concepts</span></span>
<span data-ttu-id="8aaec-112">Para começar a usar os Reliable Services, você só precisa entender alguns conceitos básicos:</span><span class="sxs-lookup"><span data-stu-id="8aaec-112">To get started with Reliable Services, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="8aaec-113">**Tipo de serviço**: esta é sua implementação de serviço.</span><span class="sxs-lookup"><span data-stu-id="8aaec-113">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="8aaec-114">Ele é definido pela classe que você escreve que estende `StatelessService` e qualquer outro código ou dependências usadas nele, juntamente com um nome e um número de versão.</span><span class="sxs-lookup"><span data-stu-id="8aaec-114">It is defined by the class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="8aaec-115">**Instância de serviço nomeada**: para executar seu serviço, criar instâncias nomeadas do tipo de serviço, bem como criar instâncias de objeto de um tipo de classe.</span><span class="sxs-lookup"><span data-stu-id="8aaec-115">**Named service instance**: To run your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="8aaec-116">Instâncias de serviço são, na verdade, as instâncias de objeto de sua classe de serviço que você escreve.</span><span class="sxs-lookup"><span data-stu-id="8aaec-116">Service instances are in fact object instantiations of your service class that you write.</span></span>
* <span data-ttu-id="8aaec-117">**Host de serviço**: as instâncias de serviço nomeado que você cria precisam executar dentro de um host.</span><span class="sxs-lookup"><span data-stu-id="8aaec-117">**Service host**: The named service instances you create need to run inside a host.</span></span> <span data-ttu-id="8aaec-118">O host de serviço é apenas um processo em que instâncias do serviço podem ser executadas.</span><span class="sxs-lookup"><span data-stu-id="8aaec-118">The service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="8aaec-119">**Registro de serviço**: o registro reúne tudo.</span><span class="sxs-lookup"><span data-stu-id="8aaec-119">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="8aaec-120">O tipo de serviço deve ser registrado com o tempo de execução do Service Fabric em um host de serviço para permitir que o Service Fabric crie instâncias para executar.</span><span class="sxs-lookup"><span data-stu-id="8aaec-120">The service type must be registered with the Service Fabric runtime in a service host to allow Service Fabric to create instances of it to run.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="8aaec-121">Criar um serviço sem estado</span><span class="sxs-lookup"><span data-stu-id="8aaec-121">Create a stateless service</span></span>
<span data-ttu-id="8aaec-122">Comece criando um aplicativo de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8aaec-122">Start by creating a Service Fabric application.</span></span> <span data-ttu-id="8aaec-123">O SDK do Service Fabric para Linux inclui um gerador Yeoman para fornecer o scaffolding de um aplicativo de Service Fabric com um serviço sem estado.</span><span class="sxs-lookup"><span data-stu-id="8aaec-123">The Service Fabric SDK for Linux includes a Yeoman generator to provide the scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="8aaec-124">Comece executando o seguinte comando Yeoman:</span><span class="sxs-lookup"><span data-stu-id="8aaec-124">Start by running the following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="8aaec-125">Siga as instruções para criar um **Serviço Confiável Sem Estado**.</span><span class="sxs-lookup"><span data-stu-id="8aaec-125">Follow the instructions to create a **Reliable Stateless Service**.</span></span> <span data-ttu-id="8aaec-126">Para este tutorial, nomeie o aplicativo "HelloWorldApplication" e o serviço "HelloWorld".</span><span class="sxs-lookup"><span data-stu-id="8aaec-126">For this tutorial, name the application "HelloWorldApplication" and the service "HelloWorld".</span></span> <span data-ttu-id="8aaec-127">O resultado inclui os diretórios para `HelloWorldApplication` e `HelloWorld`.</span><span class="sxs-lookup"><span data-stu-id="8aaec-127">The result includes directories for the `HelloWorldApplication` and `HelloWorld`.</span></span>

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

## <a name="implement-the-service"></a><span data-ttu-id="8aaec-128">Implementar o serviço</span><span class="sxs-lookup"><span data-stu-id="8aaec-128">Implement the service</span></span>
<span data-ttu-id="8aaec-129">Abra **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span><span class="sxs-lookup"><span data-stu-id="8aaec-129">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span></span> <span data-ttu-id="8aaec-130">Essa classe define o tipo de serviço e pode executar qualquer código.</span><span class="sxs-lookup"><span data-stu-id="8aaec-130">This class defines the service type, and can run any code.</span></span> <span data-ttu-id="8aaec-131">A API de serviço fornece dois pontos de entrada para seu código:</span><span class="sxs-lookup"><span data-stu-id="8aaec-131">The service API provides two entry points for your code:</span></span>

* <span data-ttu-id="8aaec-132">Um método de ponto de entrada em aberto chamado `runAsync()`, em que você pode começar a executar qualquer carga de trabalho, incluindo cargas de trabalho de computação de longa duração.</span><span class="sxs-lookup"><span data-stu-id="8aaec-132">An open-ended entry point method, called `runAsync()`, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* <span data-ttu-id="8aaec-133">Um ponto de entrada de comunicação no qual você pode conectar a pilha de comunicação de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="8aaec-133">A communication entry point where you can plug in your communication stack of choice.</span></span> <span data-ttu-id="8aaec-134">É onde você pode começar a receber solicitações de usuários e outros serviços.</span><span class="sxs-lookup"><span data-stu-id="8aaec-134">This is where you can start receiving requests from users and other services.</span></span>

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

<span data-ttu-id="8aaec-135">Neste tutorial, enfatizaremos o método de ponto de entrada `runAsync()` .</span><span class="sxs-lookup"><span data-stu-id="8aaec-135">In this tutorial, we focus on the `runAsync()` entry point method.</span></span> <span data-ttu-id="8aaec-136">É aqui que você pode começar imediatamente a executar seu código.</span><span class="sxs-lookup"><span data-stu-id="8aaec-136">This is where you can immediately start running your code.</span></span>

### <a name="runasync"></a><span data-ttu-id="8aaec-137">RunAsync</span><span class="sxs-lookup"><span data-stu-id="8aaec-137">RunAsync</span></span>
<span data-ttu-id="8aaec-138">A plataforma chama esse método quando uma instância de um serviço é estabelecida e está pronta para execução.</span><span class="sxs-lookup"><span data-stu-id="8aaec-138">The platform calls this method when an instance of a service is placed and ready to execute.</span></span> <span data-ttu-id="8aaec-139">Para um serviço sem estado, isso simplesmente significa quando a instância do serviço é aberta.</span><span class="sxs-lookup"><span data-stu-id="8aaec-139">For a stateless service, that simply means when the service instance is opened.</span></span> <span data-ttu-id="8aaec-140">Um token de cancelamento é fornecido para coordenar quando sua instância de serviço deve ser fechada.</span><span class="sxs-lookup"><span data-stu-id="8aaec-140">A cancellation token is provided to coordinate when your service instance needs to be closed.</span></span> <span data-ttu-id="8aaec-141">No Service Fabric, esse ciclo de abertura/fechamento de uma instância de serviço pode ocorrer várias vezes durante a vida útil do serviço como um todo.</span><span class="sxs-lookup"><span data-stu-id="8aaec-141">In Service Fabric, this open/close cycle of a service instance can occur many times over the lifetime of the service as a whole.</span></span> <span data-ttu-id="8aaec-142">Isso pode ocorrer por vários motivos, incluindo:</span><span class="sxs-lookup"><span data-stu-id="8aaec-142">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="8aaec-143">O sistema move as instâncias de serviço para balanceamento de recursos.</span><span class="sxs-lookup"><span data-stu-id="8aaec-143">The system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="8aaec-144">Ocorrem falhas no código.</span><span class="sxs-lookup"><span data-stu-id="8aaec-144">Faults occur in your code.</span></span>
* <span data-ttu-id="8aaec-145">O aplicativo ou sistema é atualizado.</span><span class="sxs-lookup"><span data-stu-id="8aaec-145">The application or system is upgraded.</span></span>
* <span data-ttu-id="8aaec-146">O hardware subjacente sofre uma interrupção.</span><span class="sxs-lookup"><span data-stu-id="8aaec-146">The underlying hardware experiences an outage.</span></span>

<span data-ttu-id="8aaec-147">Essa orquestração é gerenciada pelo Service Fabric para manter o serviço altamente disponível e devidamente balanceado.</span><span class="sxs-lookup"><span data-stu-id="8aaec-147">This orchestration is managed by Service Fabric to keep your service highly available and properly balanced.</span></span>

<span data-ttu-id="8aaec-148">`runAsync()` não deve bloquear sincronicamente.</span><span class="sxs-lookup"><span data-stu-id="8aaec-148">`runAsync()` should not block synchronously.</span></span> <span data-ttu-id="8aaec-149">A implementação de runAsync deve retornar um CompletableFuture para permitir que o tempo de execução continue.</span><span class="sxs-lookup"><span data-stu-id="8aaec-149">Your implementation of runAsync should return a CompletableFuture to allow the runtime to continue.</span></span> <span data-ttu-id="8aaec-150">Se sua carga de trabalho precisar implementar uma tarefa demorada que deve ser executada dentro do CompletableFuture.</span><span class="sxs-lookup"><span data-stu-id="8aaec-150">If your workload needs to implement a long running task that should be done inside the CompletableFuture.</span></span>

#### <a name="cancellation"></a><span data-ttu-id="8aaec-151">Cancelamento</span><span class="sxs-lookup"><span data-stu-id="8aaec-151">Cancellation</span></span>
<span data-ttu-id="8aaec-152">O cancelamento da sua carga de trabalho é um esforço cooperativo orquestrado pelo token de cancelamento fornecido.</span><span class="sxs-lookup"><span data-stu-id="8aaec-152">Cancellation of your workload is a cooperative effort orchestrated by the provided cancellation token.</span></span> <span data-ttu-id="8aaec-153">O sistema aguarda o encerramento da tarefa (por conclusão bem-sucedida, cancelamento ou falha) antes de prosseguir.</span><span class="sxs-lookup"><span data-stu-id="8aaec-153">The system waits for your task to end (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="8aaec-154">É importante honrar o token de cancelamento, concluir qualquer trabalho e sair do `runAsync()` o mais rapidamente possível quando o sistema solicita o cancelamento.</span><span class="sxs-lookup"><span data-stu-id="8aaec-154">It is important to honor the cancellation token, finish any work, and exit `runAsync()` as quickly as possible when the system requests cancellation.</span></span> <span data-ttu-id="8aaec-155">O exemplo a seguir demonstra como processar um evento de cancelamento:</span><span class="sxs-lookup"><span data-stu-id="8aaec-155">The following example demonstrates how to handle a cancellation event:</span></span>

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace the following sample code with your own logic
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

### <a name="service-registration"></a><span data-ttu-id="8aaec-156">Registro do serviço</span><span class="sxs-lookup"><span data-stu-id="8aaec-156">Service registration</span></span>
<span data-ttu-id="8aaec-157">Os tipos de serviço devem ser registrados com o tempo de execução do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8aaec-157">Service types must be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="8aaec-158">O tipo de serviço é definido na `ServiceManifest.xml` e sua classe de serviço que implementa `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="8aaec-158">The service type is defined in the `ServiceManifest.xml` and your service class that implements `StatelessService`.</span></span> <span data-ttu-id="8aaec-159">O registro de serviço é executado no ponto de entrada principal do processo.</span><span class="sxs-lookup"><span data-stu-id="8aaec-159">Service registration is performed in the process main entry point.</span></span> <span data-ttu-id="8aaec-160">Neste exemplo, o ponto de entrada principal do processo é `HelloWorldServiceHost.java`:</span><span class="sxs-lookup"><span data-stu-id="8aaec-160">In this example, the process main entry point is `HelloWorldServiceHost.java`:</span></span>

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

## <a name="run-the-application"></a><span data-ttu-id="8aaec-161">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="8aaec-161">Run the application</span></span>

<span data-ttu-id="8aaec-162">O scaffolding Yeoman inclui um script gradle para compilar o aplicativo e os scripts bash para implantar e remover o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8aaec-162">The Yeoman scaffolding includes a gradle script to build the application and bash scripts to deploy and remove the application.</span></span> <span data-ttu-id="8aaec-163">Para executar o aplicativo, primeiro compile o aplicativo com gradle:</span><span class="sxs-lookup"><span data-stu-id="8aaec-163">To run the application, first build the application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="8aaec-164">Isso produz um pacote de aplicativos do Service Fabric que poderá ser implantado usando a CLI do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8aaec-164">This produces a Service Fabric application package that can be deployed using Service Fabric CLI.</span></span>

### <a name="deploy-with-service-fabric-cli"></a><span data-ttu-id="8aaec-165">Implantar com a CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8aaec-165">Deploy with Service Fabric CLI</span></span>

<span data-ttu-id="8aaec-166">O script install.sh contém os comandos da CLI do Service Fabric necessários para implantar o pacote de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="8aaec-166">The install.sh script contains the necessary Service Fabric CLI commands to deploy the application package.</span></span> <span data-ttu-id="8aaec-167">Execute o script install.sh para implantar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8aaec-167">Run the install.sh script to deploy the application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="8aaec-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8aaec-168">Next steps</span></span>

* [<span data-ttu-id="8aaec-169">Introdução à CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8aaec-169">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
