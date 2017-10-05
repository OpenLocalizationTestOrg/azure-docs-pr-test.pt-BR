---
title: Criar seu primeiro aplicativo do Service Fabric em C# | Microsoft Docs
description: "Introdução à criação de um aplicativo do Service Fabric do Microsoft Azure com serviços com e sem estado."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d9b44d75-e905-468e-b867-2190ce97379a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: vturecek
ms.openlocfilehash: 813021d6239ae3cf79bb84b78f77e39c9e0783f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="cd07d-103">Introdução aos Reliable Services</span><span class="sxs-lookup"><span data-stu-id="cd07d-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cd07d-104">C# em Windows</span><span class="sxs-lookup"><span data-stu-id="cd07d-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="cd07d-105">Java no Linux</span><span class="sxs-lookup"><span data-stu-id="cd07d-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
> 
> 

<span data-ttu-id="cd07d-106">Um aplicativo do Service Fabric do Azure contém um ou mais serviços que executam seu código.</span><span class="sxs-lookup"><span data-stu-id="cd07d-106">An Azure Service Fabric application contains one or more services that run your code.</span></span> <span data-ttu-id="cd07d-107">Este guia mostra como criar aplicativos Service Fabric com e sem estado usando os [Reliable Services](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cd07d-107">This guide shows you how to create both stateless and stateful Service Fabric applications with [Reliable Services](service-fabric-reliable-services-introduction.md).</span></span>  <span data-ttu-id="cd07d-108">Este vídeo da Microsoft Virtual Academy mostra como criar um serviço confiável sem estado: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span><span class="sxs-lookup"><span data-stu-id="cd07d-108">This Microsoft Virtual Academy video also shows you how to create a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a><span data-ttu-id="cd07d-109">Conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="cd07d-109">Basic concepts</span></span>
<span data-ttu-id="cd07d-110">Para começar a usar os Reliable Services, você só precisa entender alguns conceitos básicos:</span><span class="sxs-lookup"><span data-stu-id="cd07d-110">To get started with Reliable Services, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="cd07d-111">**Tipo de serviço**: esta é sua implementação de serviço.</span><span class="sxs-lookup"><span data-stu-id="cd07d-111">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="cd07d-112">Ele é definido pela classe que você escreve que estende `StatelessService` e qualquer outro código ou dependências usadas nele, juntamente com um nome e um número de versão.</span><span class="sxs-lookup"><span data-stu-id="cd07d-112">It is defined by the class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="cd07d-113">**Instância de serviço nomeada**: para executar seu serviço, criar instâncias nomeadas do tipo de serviço, bem como criar instâncias de objeto de um tipo de classe.</span><span class="sxs-lookup"><span data-stu-id="cd07d-113">**Named service instance**: To run your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="cd07d-114">Uma instância de serviço tem um nome na forma de um URI usando o esquema "fabric: /", por exemplo, "fabric:/MyApp/MyService".</span><span class="sxs-lookup"><span data-stu-id="cd07d-114">A service instance has a name in the form of a URI using the "fabric:/" scheme, such as "fabric:/MyApp/MyService".</span></span>
* <span data-ttu-id="cd07d-115">**Host de serviço**: as instâncias de serviço nomeado que você cria precisam executar dentro de um processo de host.</span><span class="sxs-lookup"><span data-stu-id="cd07d-115">**Service host**: The named service instances you create need to run inside a host process.</span></span> <span data-ttu-id="cd07d-116">O host de serviço é apenas um processo em que instâncias do serviço podem ser executadas.</span><span class="sxs-lookup"><span data-stu-id="cd07d-116">The service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="cd07d-117">**Registro de serviço**: o registro reúne tudo.</span><span class="sxs-lookup"><span data-stu-id="cd07d-117">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="cd07d-118">O tipo de serviço deve ser registrado com o tempo de execução do Service Fabric em um host de serviço para permitir que o Service Fabric crie instâncias para executar.</span><span class="sxs-lookup"><span data-stu-id="cd07d-118">The service type must be registered with the Service Fabric runtime in a service host to allow Service Fabric to create instances of it to run.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="cd07d-119">Criar um serviço sem estado</span><span class="sxs-lookup"><span data-stu-id="cd07d-119">Create a stateless service</span></span>
<span data-ttu-id="cd07d-120">Um serviço sem estado é um tipo de serviço que atualmente está na norma dos aplicativos em nuvem.</span><span class="sxs-lookup"><span data-stu-id="cd07d-120">A stateless service is a type of service that is currently the norm in cloud applications.</span></span> <span data-ttu-id="cd07d-121">Ele é considerado sem estado porque o serviço em si não contém dados que precisam ser armazenados de modo confiável nem altamente disponibilizados.</span><span class="sxs-lookup"><span data-stu-id="cd07d-121">It is considered stateless because the service itself does not contain data that needs to be stored reliably or made highly available.</span></span> <span data-ttu-id="cd07d-122">Se uma instância de um serviço sem estado for desligada, todo seu estado interno será perdido.</span><span class="sxs-lookup"><span data-stu-id="cd07d-122">If an instance of a stateless service shuts down, all of its internal state is lost.</span></span> <span data-ttu-id="cd07d-123">Nesse tipo de serviço, o estado deve ser mantido em um repositório externo, como em Tabelas do Azure ou um banco de dados SQL, para que ele se torne altamente disponível e confiável.</span><span class="sxs-lookup"><span data-stu-id="cd07d-123">In this type of service, state must be persisted to an external store, such as Azure Tables or a SQL database, for it to be made highly available and reliable.</span></span>

<span data-ttu-id="cd07d-124">Inicie o Visual Studio 2015 ou 2017 como administrador e crie um novo projeto de aplicativo do Service Fabric chamado *HelloWorld*:</span><span class="sxs-lookup"><span data-stu-id="cd07d-124">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project named *HelloWorld*:</span></span>

![Usar a caixa de diálogo Novo Projeto para criar um novo aplicativo do Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

<span data-ttu-id="cd07d-126">Em seguida, crie um projeto de serviço sem estado chamado *HelloWorldStateless*:</span><span class="sxs-lookup"><span data-stu-id="cd07d-126">Then create a stateless service project named *HelloWorldStateless*:</span></span>

![Na segunda caixa de diálogo, criar um projeto de serviço sem estado](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

<span data-ttu-id="cd07d-128">Agora, sua solução contém dois projetos:</span><span class="sxs-lookup"><span data-stu-id="cd07d-128">Your solution now contains two projects:</span></span>

* <span data-ttu-id="cd07d-129">*HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="cd07d-129">*HelloWorld*.</span></span> <span data-ttu-id="cd07d-130">Esse é o projeto de *aplicativo* que contém seus *serviços*.</span><span class="sxs-lookup"><span data-stu-id="cd07d-130">This is the *application* project that contains your *services*.</span></span> <span data-ttu-id="cd07d-131">Ele também contém o manifesto do aplicativo que descreve o aplicativo, bem como diversos scripts do PowerShell que ajudam a implantar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cd07d-131">It also contains the application manifest that describes the application, as well as a number of PowerShell scripts that help you to deploy your application.</span></span>
* <span data-ttu-id="cd07d-132">*HelloWorldStateless*.</span><span class="sxs-lookup"><span data-stu-id="cd07d-132">*HelloWorldStateless*.</span></span> <span data-ttu-id="cd07d-133">Esse é o projeto de serviço.</span><span class="sxs-lookup"><span data-stu-id="cd07d-133">This is the service project.</span></span> <span data-ttu-id="cd07d-134">Ele contém a implementação do serviço sem estado.</span><span class="sxs-lookup"><span data-stu-id="cd07d-134">It contains the stateless service implementation.</span></span>

## <a name="implement-the-service"></a><span data-ttu-id="cd07d-135">Implementar o serviço</span><span class="sxs-lookup"><span data-stu-id="cd07d-135">Implement the service</span></span>
<span data-ttu-id="cd07d-136">Abra o arquivo **HelloWorldStateless.cs** no projeto de serviço.</span><span class="sxs-lookup"><span data-stu-id="cd07d-136">Open the **HelloWorldStateless.cs** file in the service project.</span></span> <span data-ttu-id="cd07d-137">No Service Fabric, um serviço pode executar qualquer lógica de negócios.</span><span class="sxs-lookup"><span data-stu-id="cd07d-137">In Service Fabric, a service can run any business logic.</span></span> <span data-ttu-id="cd07d-138">A API de serviço fornece dois pontos de entrada para seu código:</span><span class="sxs-lookup"><span data-stu-id="cd07d-138">The service API provides two entry points for your code:</span></span>

* <span data-ttu-id="cd07d-139">Um método de ponto de entrada em aberto chamado *RunAsync*, em que você pode começar a executar qualquer carga de trabalho, incluindo cargas de trabalho de computação de longa duração.</span><span class="sxs-lookup"><span data-stu-id="cd07d-139">An open-ended entry point method, called *RunAsync*, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* <span data-ttu-id="cd07d-140">Um ponto de entrada de comunicação em que você pode conectar a pilha de comunicação de sua escolha como o ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="cd07d-140">A communication entry point where you can plug in your communication stack of choice, such as ASP.NET Core.</span></span> <span data-ttu-id="cd07d-141">É onde você pode começar a receber solicitações de usuários e outros serviços.</span><span class="sxs-lookup"><span data-stu-id="cd07d-141">This is where you can start receiving requests from users and other services.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

<span data-ttu-id="cd07d-142">Neste tutorial, enfatizaremos o método de ponto de entrada `RunAsync()` .</span><span class="sxs-lookup"><span data-stu-id="cd07d-142">In this tutorial, we will focus on the `RunAsync()` entry point method.</span></span> <span data-ttu-id="cd07d-143">É aqui que você pode começar imediatamente a executar seu código.</span><span class="sxs-lookup"><span data-stu-id="cd07d-143">This is where you can immediately start running your code.</span></span>
<span data-ttu-id="cd07d-144">O modelo de projeto inclui um exemplo de implementação de `RunAsync()` que incrementa uma contagem progressiva.</span><span class="sxs-lookup"><span data-stu-id="cd07d-144">The project template includes a sample implementation of `RunAsync()` that increments a rolling count.</span></span>

> [!NOTE]
> <span data-ttu-id="cd07d-145">Para obter detalhes sobre como trabalhar com uma pilha de comunicação, confira [Serviços de API do Service Fabric com auto-hospedagem do OWIN](service-fabric-reliable-services-communication-webapi.md)</span><span class="sxs-lookup"><span data-stu-id="cd07d-145">For details about how to work with a communication stack, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md)</span></span>
> 
> 

### <a name="runasync"></a><span data-ttu-id="cd07d-146">RunAsync</span><span class="sxs-lookup"><span data-stu-id="cd07d-146">RunAsync</span></span>
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace the following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    long iterations = 0;

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        ServiceEventSource.Current.ServiceMessage(this, "Working-{0}", ++iterations);

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

<span data-ttu-id="cd07d-147">A plataforma chama esse método quando uma instância de um serviço é estabelecida e está pronta para execução.</span><span class="sxs-lookup"><span data-stu-id="cd07d-147">The platform calls this method when an instance of a service is placed and ready to execute.</span></span> <span data-ttu-id="cd07d-148">Para um serviço sem estado, isso simplesmente significa quando a instância do serviço é aberta.</span><span class="sxs-lookup"><span data-stu-id="cd07d-148">For a stateless service, that simply means when the service instance is opened.</span></span> <span data-ttu-id="cd07d-149">Um token de cancelamento é fornecido para coordenar quando sua instância de serviço deve ser fechada.</span><span class="sxs-lookup"><span data-stu-id="cd07d-149">A cancellation token is provided to coordinate when your service instance needs to be closed.</span></span> <span data-ttu-id="cd07d-150">No Service Fabric, esse ciclo de abertura/fechamento de uma instância de serviço pode ocorrer várias vezes durante a vida útil do serviço como um todo.</span><span class="sxs-lookup"><span data-stu-id="cd07d-150">In Service Fabric, this open/close cycle of a service instance can occur many times over the lifetime of the service as a whole.</span></span> <span data-ttu-id="cd07d-151">Isso pode ocorrer por vários motivos, incluindo:</span><span class="sxs-lookup"><span data-stu-id="cd07d-151">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="cd07d-152">O sistema move as instâncias de serviço para balanceamento de recursos.</span><span class="sxs-lookup"><span data-stu-id="cd07d-152">The system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="cd07d-153">Ocorrem falhas no código.</span><span class="sxs-lookup"><span data-stu-id="cd07d-153">Faults occur in your code.</span></span>
* <span data-ttu-id="cd07d-154">O aplicativo ou sistema é atualizado.</span><span class="sxs-lookup"><span data-stu-id="cd07d-154">The application or system is upgraded.</span></span>
* <span data-ttu-id="cd07d-155">O hardware subjacente sofre uma interrupção.</span><span class="sxs-lookup"><span data-stu-id="cd07d-155">The underlying hardware experiences an outage.</span></span>

<span data-ttu-id="cd07d-156">Essa orquestração é gerenciada pelo sistema a fim de manter o serviço altamente disponível e devidamente balanceado.</span><span class="sxs-lookup"><span data-stu-id="cd07d-156">This orchestration is managed by the system to keep your service highly available and properly balanced.</span></span>

<span data-ttu-id="cd07d-157">`RunAsync()` não deve bloquear sincronicamente.</span><span class="sxs-lookup"><span data-stu-id="cd07d-157">`RunAsync()` should not block synchronously.</span></span> <span data-ttu-id="cd07d-158">Sua implementação de RunAsync deve retornar uma tarefa ou esperar operações de execução longa ou de bloqueio para permitir que o tempo de execução continue.</span><span class="sxs-lookup"><span data-stu-id="cd07d-158">Your implementation of RunAsync should return a Task or await on any long-running or blocking operations to allow the runtime to continue.</span></span> <span data-ttu-id="cd07d-159">Observe que no loop `while(true)` no exemplo anterior, um retorno de tarefa `await Task.Delay()` é usado.</span><span class="sxs-lookup"><span data-stu-id="cd07d-159">Note in the `while(true)` loop in the previous example, a Task-returning `await Task.Delay()` is used.</span></span> <span data-ttu-id="cd07d-160">Se sua carga de trabalho deve bloquear sincronicamente, agende uma nova tarefa com `Task.Run()` na sua implementação `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="cd07d-160">If your workload must block synchronously, you should schedule a new Task with `Task.Run()` in your `RunAsync` implementation.</span></span>

<span data-ttu-id="cd07d-161">O cancelamento da sua carga de trabalho é um esforço cooperativo orquestrado pelo token de cancelamento fornecido.</span><span class="sxs-lookup"><span data-stu-id="cd07d-161">Cancellation of your workload is a cooperative effort orchestrated by the provided cancellation token.</span></span> <span data-ttu-id="cd07d-162">O sistema aguardará o encerramento da tarefa (por conclusão bem-sucedida, cancelamento ou falha) antes de prosseguir.</span><span class="sxs-lookup"><span data-stu-id="cd07d-162">The system will wait for your task to end (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="cd07d-163">É importante honrar o token de cancelamento, concluir qualquer trabalho e sair do `RunAsync()` o mais rapidamente possível quando o sistema solicita o cancelamento.</span><span class="sxs-lookup"><span data-stu-id="cd07d-163">It is important to honor the cancellation token, finish any work, and exit `RunAsync()` as quickly as possible when the system requests cancellation.</span></span>

<span data-ttu-id="cd07d-164">Neste exemplo de serviço sem estado, a contagem é armazenada em uma variável local.</span><span class="sxs-lookup"><span data-stu-id="cd07d-164">In this stateless service example, the count is stored in a local variable.</span></span> <span data-ttu-id="cd07d-165">Mas como esse é um serviço sem estado, o valor que é armazenado existe apenas para o ciclo de vida atual da sua instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="cd07d-165">But because this is a stateless service, the value that's stored exists only for the current lifecycle of its service instance.</span></span> <span data-ttu-id="cd07d-166">Quando o serviço se move ou é reiniciado, o valor é perdido.</span><span class="sxs-lookup"><span data-stu-id="cd07d-166">When the service moves or restarts, the value is lost.</span></span>

## <a name="create-a-stateful-service"></a><span data-ttu-id="cd07d-167">Criar um serviço com estado</span><span class="sxs-lookup"><span data-stu-id="cd07d-167">Create a stateful service</span></span>
<span data-ttu-id="cd07d-168">O Service Fabric introduz um novo tipo de serviço que é com estado.</span><span class="sxs-lookup"><span data-stu-id="cd07d-168">Service Fabric introduces a new kind of service that is stateful.</span></span> <span data-ttu-id="cd07d-169">Um serviço com estado pode manter o estado de maneira confiável dentro do próprio serviço, localizado em conjunto com o código que o está usando.</span><span class="sxs-lookup"><span data-stu-id="cd07d-169">A stateful service can maintain state reliably within the service itself, co-located with the code that's using it.</span></span> <span data-ttu-id="cd07d-170">O estado é altamente disponibilizado pelo Service Fabric sem a necessidade de persistir o estado em um repositório externo.</span><span class="sxs-lookup"><span data-stu-id="cd07d-170">State is made highly available by Service Fabric without the need to persist state to an external store.</span></span>

<span data-ttu-id="cd07d-171">Para converter o valor de contador de sem estado para altamente disponível e persistente, mesmo quando o serviço for movido ou reiniciado, você precisa de um serviço com estado.</span><span class="sxs-lookup"><span data-stu-id="cd07d-171">To convert a counter value from stateless to highly available and persistent, even when the service moves or restarts, you need a stateful service.</span></span>

<span data-ttu-id="cd07d-172">No mesmo aplicativo *HelloWorld*, é possível adicionar um novo serviço clicando com o botão direito do mouse nas referências Serviços no projeto de aplicativo e selecionando **Adicionar -> Novo Serviço Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="cd07d-172">In the same *HelloWorld* application, you can add a new service by right-clicking on the Services references in the application project and selecting **Add ->  New Service Fabric Service**.</span></span>

![Adicione um serviço ao aplicativo da Malha de Serviços](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

<span data-ttu-id="cd07d-174">Selecione **Serviço com Estado** e dê o nome de *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="cd07d-174">Select **Stateful Service** and name it *HelloWorldStateful*.</span></span> <span data-ttu-id="cd07d-175">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="cd07d-175">Click **OK**.</span></span>

![Usar a caixa de diálogo Novo Projeto para criar um novo serviço com estado do Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

<span data-ttu-id="cd07d-177">Seu aplicativo agora deve ter dois serviços: o serviço sem estado *HelloWorldStateless* e o serviço com estado *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="cd07d-177">Your application should now have two services: the stateless service *HelloWorldStateless* and the stateful service *HelloWorldStateful*.</span></span>

<span data-ttu-id="cd07d-178">Um serviço com estado tem os mesmos pontos de entrada que um serviço sem estado.</span><span class="sxs-lookup"><span data-stu-id="cd07d-178">A stateful service has the same entry points as a stateless service.</span></span> <span data-ttu-id="cd07d-179">A principal diferença é a disponibilidade de um *provedor de estado* que pode armazenar estados de maneira confiável.</span><span class="sxs-lookup"><span data-stu-id="cd07d-179">The main difference is the availability of a *state provider* that can store state reliably.</span></span> <span data-ttu-id="cd07d-180">O Service Fabric é fornecido com uma implementação de provedor de estado chamada [Coleções Confiáveis](service-fabric-reliable-services-reliable-collections.md), que permite que você crie estruturas de dados replicados por meio do Gerenciador de Estado Confiável.</span><span class="sxs-lookup"><span data-stu-id="cd07d-180">Service Fabric comes with a state provider implementation called [Reliable Collections](service-fabric-reliable-services-reliable-collections.md), which lets you create replicated data structures through the Reliable State Manager.</span></span> <span data-ttu-id="cd07d-181">Por padrão, um serviço confiável com estado usa esse provedor de estado.</span><span class="sxs-lookup"><span data-stu-id="cd07d-181">A stateful Reliable Service uses this state provider by default.</span></span>

<span data-ttu-id="cd07d-182">Abra **HelloWorldStateful.cs** em *HelloWorldStateful*, que contém o método RunAsync a seguir:</span><span class="sxs-lookup"><span data-stu-id="cd07d-182">Open **HelloWorldStateful.cs** in *HelloWorldStateful*, which contains the following RunAsync method:</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace the following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");

            ServiceEventSource.Current.ServiceMessage(this, "Current Counter Value: {0}",
                result.HasValue ? result.Value.ToString() : "Value does not exist.");

            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, the transaction aborts, all changes are
            // discarded, and nothing is saved to the secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a><span data-ttu-id="cd07d-183">RunAsync</span><span class="sxs-lookup"><span data-stu-id="cd07d-183">RunAsync</span></span>
<span data-ttu-id="cd07d-184">`RunAsync()` opera da mesma forma em serviços com e sem estado.</span><span class="sxs-lookup"><span data-stu-id="cd07d-184">`RunAsync()` operates similarly in stateful and stateless services.</span></span> <span data-ttu-id="cd07d-185">No entanto, em um serviço com estado, a plataforma executa trabalho adicional em seu nome antes de executar `RunAsync()`.</span><span class="sxs-lookup"><span data-stu-id="cd07d-185">However, in a stateful service, the platform performs additional work on your behalf before it executes `RunAsync()`.</span></span> <span data-ttu-id="cd07d-186">Esse trabalho pode incluir garantir que o Gerenciador de Estado Confiável e as Coleções Confiáveis estejam prontos para uso.</span><span class="sxs-lookup"><span data-stu-id="cd07d-186">This work can include ensuring that the Reliable State Manager and Reliable Collections are ready to use.</span></span>

### <a name="reliable-collections-and-the-reliable-state-manager"></a><span data-ttu-id="cd07d-187">Coleções Confiáveis e Gerenciador de Estado Confiável</span><span class="sxs-lookup"><span data-stu-id="cd07d-187">Reliable Collections and the Reliable State Manager</span></span>
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

<span data-ttu-id="cd07d-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) é uma implementação de dicionário que você pode usar para armazenar o estado no serviço de forma confiável.</span><span class="sxs-lookup"><span data-stu-id="cd07d-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) is a dictionary implementation that you can use to reliably store state in the service.</span></span> <span data-ttu-id="cd07d-189">Com o Service Fabric e as Reliable Collections, você agora pode armazenar dados diretamente em seu serviço sem a necessidade de um repositório persistente externo.</span><span class="sxs-lookup"><span data-stu-id="cd07d-189">With Service Fabric and Reliable Collections, you can store data directly in your service without the need for an external persistent store.</span></span> <span data-ttu-id="cd07d-190">As Coleções Confiáveis tornam os dados altamente disponíveis.</span><span class="sxs-lookup"><span data-stu-id="cd07d-190">Reliable Collections make your data highly available.</span></span> <span data-ttu-id="cd07d-191">O Service Fabric consegue isso criando e gerenciando várias *réplicas* do seu serviço para você.</span><span class="sxs-lookup"><span data-stu-id="cd07d-191">Service Fabric accomplishes this by creating and managing multiple *replicas* of your service for you.</span></span> <span data-ttu-id="cd07d-192">Ele também fornece uma API que abstrai as complexidades de gerenciar essas réplicas e as respectivas transições de estado.</span><span class="sxs-lookup"><span data-stu-id="cd07d-192">It also provides an API that abstracts away the complexities of managing those replicas and their state transitions.</span></span>

<span data-ttu-id="cd07d-193">As Reliable Collections podem armazenar qualquer tipo .NET, incluindo tipos personalizados, com algumas limitações:</span><span class="sxs-lookup"><span data-stu-id="cd07d-193">Reliable Collections can store any .NET type, including your custom types, with a couple of caveats:</span></span>

* <span data-ttu-id="cd07d-194">O Service Fabric torna seu estado altamente disponível *replicando* o estado entre nós, e as Coleções Confiáveis armazenam seus dados no disco local em cada réplica.</span><span class="sxs-lookup"><span data-stu-id="cd07d-194">Service Fabric makes your state highly available by *replicating* state across nodes, and Reliable Collections store your data to local disk on each replica.</span></span> <span data-ttu-id="cd07d-195">Isso significa que tudo o que é armazenado nas Coleções Confiáveis deve ser *serializável*.</span><span class="sxs-lookup"><span data-stu-id="cd07d-195">This means that everything that is stored in Reliable Collections must be *serializable*.</span></span> <span data-ttu-id="cd07d-196">Por padrão, as Coleções Confiáveis usam [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) para serialização, de modo que é importante verificar se seus tipos têm [suporte do Serializador de Contrato de Dados](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) quando você usa o serializador padrão.</span><span class="sxs-lookup"><span data-stu-id="cd07d-196">By default, Reliable Collections use [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) for serialization, so it's important to make sure that your types are [supported by the Data Contract Serializer](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) when you use the default serializer.</span></span>
* <span data-ttu-id="cd07d-197">Os objetos são replicados para alta disponibilidade quando você confirma uma transação nas Reliable Collections.</span><span class="sxs-lookup"><span data-stu-id="cd07d-197">Objects are replicated for high availability when you commit transactions on Reliable Collections.</span></span> <span data-ttu-id="cd07d-198">Objetos armazenados nas Reliable Collections são mantidos na memória local do serviço.</span><span class="sxs-lookup"><span data-stu-id="cd07d-198">Objects stored in Reliable Collections are kept in local memory in your service.</span></span> <span data-ttu-id="cd07d-199">Isso significa que você tem uma referência local para o objeto.</span><span class="sxs-lookup"><span data-stu-id="cd07d-199">This means that you have a local reference to the object.</span></span>
  
   <span data-ttu-id="cd07d-200">É importante que você não modifique instâncias locais desses objetos sem executar uma operação de atualização na coleção confiável em uma transação.</span><span class="sxs-lookup"><span data-stu-id="cd07d-200">It is important that you do not mutate local instances of those objects without performing an update operation on the reliable collection in a transaction.</span></span> <span data-ttu-id="cd07d-201">Isso ocorre porque as mudanças para instâncias de objetos locais não serão replicadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="cd07d-201">This is because changes to local instances of objects will not be replicated automatically.</span></span> <span data-ttu-id="cd07d-202">Você deve inserir novamente o objeto de volta no dicionário ou usar um dos métodos *atualizar* do dicionário.</span><span class="sxs-lookup"><span data-stu-id="cd07d-202">You must re-insert the object back into the dictionary or use one of the *update* methods on the dictionary.</span></span>

<span data-ttu-id="cd07d-203">O Gerenciador De Estado Confiável gerencia as Coleções Confiáveis para você.</span><span class="sxs-lookup"><span data-stu-id="cd07d-203">The Reliable State Manager manages Reliable Collections for you.</span></span> <span data-ttu-id="cd07d-204">Basta solicitar ao Gerenciador de Estado Confiável uma coleção confiável por nome a qualquer momento e em qualquer lugar no seu serviço.</span><span class="sxs-lookup"><span data-stu-id="cd07d-204">You can simply ask the Reliable State Manager for a reliable collection by name at any time and at any place in your service.</span></span> <span data-ttu-id="cd07d-205">O Gerenciador de Estado Confiável assegura que você obtenha uma referência de volta.</span><span class="sxs-lookup"><span data-stu-id="cd07d-205">The Reliable State Manager ensures that you get a reference back.</span></span> <span data-ttu-id="cd07d-206">Não é recomendável salvar referências nas instâncias de coleção confiável em propriedades ou variáveis de membro de classe.</span><span class="sxs-lookup"><span data-stu-id="cd07d-206">We don't recommended that you save references to reliable collection instances in class member variables or properties.</span></span> <span data-ttu-id="cd07d-207">É preciso tomar muito cuidado para garantir que a referência seja definida para uma instância o tempo todo no ciclo de vida do serviço.</span><span class="sxs-lookup"><span data-stu-id="cd07d-207">Special care must be taken to ensure that the reference is set to an instance at all times in the service lifecycle.</span></span> <span data-ttu-id="cd07d-208">O Gerenciador de Estado Confiável faz esse trabalho para você e jé otimizado para repetir visitas.</span><span class="sxs-lookup"><span data-stu-id="cd07d-208">The Reliable State Manager handles this work for you, and it's optimized for repeat visits.</span></span>

### <a name="transactional-and-asynchronous-operations"></a><span data-ttu-id="cd07d-209">Operações transacionais e assíncronas</span><span class="sxs-lookup"><span data-stu-id="cd07d-209">Transactional and asynchronous operations</span></span>
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

<span data-ttu-id="cd07d-210">As Coleções Confiáveis têm muitas das mesmas operações que suas correspondentes `System.Collections.Generic` e `System.Collections.Concurrent`, incluindo o LINQ.</span><span class="sxs-lookup"><span data-stu-id="cd07d-210">Reliable Collections have many of the same operations that their `System.Collections.Generic` and `System.Collections.Concurrent` counterparts do, except LINQ.</span></span> <span data-ttu-id="cd07d-211">As operações nas Coleções Confiáveis são assíncronas.</span><span class="sxs-lookup"><span data-stu-id="cd07d-211">Operations on Reliable Collections are asynchronous.</span></span> <span data-ttu-id="cd07d-212">Isso ocorre porque as operações de gravação nas Coleções Confiáveis executam operações de E/S para replicar e manter os dados no disco.</span><span class="sxs-lookup"><span data-stu-id="cd07d-212">This is because write operations with Reliable Collections perform I/O operations to replicate and persist data to disk.</span></span>

<span data-ttu-id="cd07d-213">As operações de Coleção Confiável são *transacionais*, de modo que você pode manter o estado consistente entre várias Coleções Confiáveis e operações.</span><span class="sxs-lookup"><span data-stu-id="cd07d-213">Reliable Collection operations are *transactional*, so that you can keep state consistent across multiple Reliable Collections and operations.</span></span> <span data-ttu-id="cd07d-214">Por exemplo, você pode remover um item de trabalho de uma Fila Confiável, executar uma operação nele e salvar o resultado em um Dicionário Confiável, tudo em uma única transação.</span><span class="sxs-lookup"><span data-stu-id="cd07d-214">For example, you may dequeue a work item from a Reliable Queue, perform an operation on it, and save the result in a Reliable Dictionary, all within a single transaction.</span></span> <span data-ttu-id="cd07d-215">Trata-se de uma operação atômica e ela garante que toda a operação seja bem-sucedida ou revertida.</span><span class="sxs-lookup"><span data-stu-id="cd07d-215">This is treated as an atomic operation, and it guarantees that either the entire operation will succeed or the entire operation will roll back.</span></span> <span data-ttu-id="cd07d-216">Se ocorrer um erro depois de remover o item da fila, mas antes de salvar o resultado, toda a transação será revertida e o item permanecerá na fila para processamento.</span><span class="sxs-lookup"><span data-stu-id="cd07d-216">If an error occurs after you dequeue the item but before you save the result, the entire transaction is rolled back and the item remains in the queue for processing.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="cd07d-217">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="cd07d-217">Run the application</span></span>
<span data-ttu-id="cd07d-218">Agora retornamos ao aplicativo *HelloWorld* .</span><span class="sxs-lookup"><span data-stu-id="cd07d-218">We now return to the *HelloWorld* application.</span></span> <span data-ttu-id="cd07d-219">Agora você pode criar e implantar seus serviços.</span><span class="sxs-lookup"><span data-stu-id="cd07d-219">You can now build and deploy your services.</span></span> <span data-ttu-id="cd07d-220">Quando você pressionar **F5**, seu aplicativo será criado e implantado no cluster local.</span><span class="sxs-lookup"><span data-stu-id="cd07d-220">When you press **F5**, your application will be built and deployed to your local cluster.</span></span>

<span data-ttu-id="cd07d-221">Depois que os serviços começaram a ser executados, você poderá exibir os eventos ETW (Rastreamento de Eventos para Windows) gerados em uma janela **Eventos de Diagnóstico** .</span><span class="sxs-lookup"><span data-stu-id="cd07d-221">After the services start running, you can view the generated Event Tracing for Windows (ETW) events in a **Diagnostic Events** window.</span></span> <span data-ttu-id="cd07d-222">Observe que os eventos exibidos são dos serviços sem e com estado do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cd07d-222">Note that the events displayed are from both the stateless service and the stateful service in the application.</span></span> <span data-ttu-id="cd07d-223">Você pode pausar o fluxo clicando no botão **Pausar** .</span><span class="sxs-lookup"><span data-stu-id="cd07d-223">You can pause the stream by clicking the **Pause** button.</span></span> <span data-ttu-id="cd07d-224">Assim, você pode examinar os detalhes de uma mensagem expandindo-a.</span><span class="sxs-lookup"><span data-stu-id="cd07d-224">You can then examine the details of a message by expanding that message.</span></span>

> [!NOTE]
> <span data-ttu-id="cd07d-225">Antes de executar o aplicativo, verifique a existência de um cluster de desenvolvimento local em execução.</span><span class="sxs-lookup"><span data-stu-id="cd07d-225">Before you run the application, make sure that you have a local development cluster running.</span></span> <span data-ttu-id="cd07d-226">Confira o [guia de introdução](service-fabric-get-started.md) para obter informações sobre como configurar o ambiente local.</span><span class="sxs-lookup"><span data-stu-id="cd07d-226">Check out the [getting started guide](service-fabric-get-started.md) for information on setting up your local environment.</span></span>
> 
> 

![Exibir Eventos de Diagnóstico no Visual Studio](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a><span data-ttu-id="cd07d-228">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cd07d-228">Next steps</span></span>
[<span data-ttu-id="cd07d-229">Depurar seu aplicativo do Service Fabric usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cd07d-229">Debug your Service Fabric application in Visual Studio</span></span>](service-fabric-debugging-your-application.md)

[<span data-ttu-id="cd07d-230">Introdução aos serviços de API Web do Service Fabric com auto-hospedagem OWIN</span><span class="sxs-lookup"><span data-stu-id="cd07d-230">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>](service-fabric-reliable-services-communication-webapi.md)

[<span data-ttu-id="cd07d-231">Saiba mais sobre as Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="cd07d-231">Learn more about Reliable Collections</span></span>](service-fabric-reliable-services-reliable-collections.md)

[<span data-ttu-id="cd07d-232">Implantar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="cd07d-232">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[<span data-ttu-id="cd07d-233">Atualização de aplicativo</span><span class="sxs-lookup"><span data-stu-id="cd07d-233">Application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="cd07d-234">Referência do desenvolvedor para Reliable Services</span><span class="sxs-lookup"><span data-stu-id="cd07d-234">Developer reference for Reliable Services</span></span>](https://msdn.microsoft.com/library/azure/dn706529.aspx)

