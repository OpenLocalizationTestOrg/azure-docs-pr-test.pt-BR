---
title: "aaaCreate seu primeiro aplicativo de malha do serviço em c# | Microsoft Docs"
description: "Introdução toocreating um aplicativo do Microsoft Azure Service Fabric com serviços com e sem monitoração de estado."
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
ms.openlocfilehash: e95e67cc84be1b83c936b250cae9112ddc77b963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="99f25-103">Introdução aos Reliable Services</span><span class="sxs-lookup"><span data-stu-id="99f25-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="99f25-104">C# em Windows</span><span class="sxs-lookup"><span data-stu-id="99f25-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="99f25-105">Java no Linux</span><span class="sxs-lookup"><span data-stu-id="99f25-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
> 
> 

<span data-ttu-id="99f25-106">Um aplicativo do Service Fabric do Azure contém um ou mais serviços que executam seu código.</span><span class="sxs-lookup"><span data-stu-id="99f25-106">An Azure Service Fabric application contains one or more services that run your code.</span></span> <span data-ttu-id="99f25-107">Este guia mostra como toocreate com e sem monitoração aplicativos do Service Fabric com [serviços confiáveis](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="99f25-107">This guide shows you how toocreate both stateless and stateful Service Fabric applications with [Reliable Services](service-fabric-reliable-services-introduction.md).</span></span>  <span data-ttu-id="99f25-108">Este vídeo Microsoft Virtual Academy também mostra como toocreate um serviço confiável sem monitoração de estado:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span><span class="sxs-lookup"><span data-stu-id="99f25-108">This Microsoft Virtual Academy video also shows you how toocreate a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a><span data-ttu-id="99f25-109">Conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="99f25-109">Basic concepts</span></span>
<span data-ttu-id="99f25-110">tooget iniciado com serviços confiáveis, você só precisa toounderstand alguns conceitos básicos:</span><span class="sxs-lookup"><span data-stu-id="99f25-110">tooget started with Reliable Services, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="99f25-111">**Tipo de serviço**: esta é sua implementação de serviço.</span><span class="sxs-lookup"><span data-stu-id="99f25-111">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="99f25-112">Ele é definido pela classe Olá gravar que estende `StatelessService` e qualquer outro código ou dependências usadas neste documento, juntamente com um nome e um número de versão.</span><span class="sxs-lookup"><span data-stu-id="99f25-112">It is defined by hello class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="99f25-113">**Serviço de instância nomeada**: toorun seu serviço, você cria instâncias nomeadas do seu tipo de serviço, bem como criar instâncias de objeto de um tipo de classe.</span><span class="sxs-lookup"><span data-stu-id="99f25-113">**Named service instance**: toorun your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="99f25-114">Uma instância de serviço tem um nome na forma de saudação de um URI usando hello "fabric: /" esquema, como "fabric: / MyApp/MyService".</span><span class="sxs-lookup"><span data-stu-id="99f25-114">A service instance has a name in hello form of a URI using hello "fabric:/" scheme, such as "fabric:/MyApp/MyService".</span></span>
* <span data-ttu-id="99f25-115">**Host de serviço**: Olá denominado instâncias de serviço que você criar necessidade toorun dentro de um processo de host.</span><span class="sxs-lookup"><span data-stu-id="99f25-115">**Service host**: hello named service instances you create need toorun inside a host process.</span></span> <span data-ttu-id="99f25-116">host de serviço Olá é apenas um processo em que as instâncias do serviço podem executar.</span><span class="sxs-lookup"><span data-stu-id="99f25-116">hello service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="99f25-117">**Registro de serviço**: o registro reúne tudo.</span><span class="sxs-lookup"><span data-stu-id="99f25-117">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="99f25-118">Olá service type deve ser registrado com hello Service Fabric em tempo de execução em um serviço de hospedar instâncias de toocreate Service Fabric tooallow-toorun.</span><span class="sxs-lookup"><span data-stu-id="99f25-118">hello service type must be registered with hello Service Fabric runtime in a service host tooallow Service Fabric toocreate instances of it toorun.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="99f25-119">Criar um serviço sem estado</span><span class="sxs-lookup"><span data-stu-id="99f25-119">Create a stateless service</span></span>
<span data-ttu-id="99f25-120">Um serviço sem monitoração de estado é um tipo de serviço que está sendo norma Olá em aplicativos de nuvem.</span><span class="sxs-lookup"><span data-stu-id="99f25-120">A stateless service is a type of service that is currently hello norm in cloud applications.</span></span> <span data-ttu-id="99f25-121">Ele é considerado sem monitoração de estado como serviço Olá em si não contêm dados que precisa toobe armazenadas de forma confiável ou altamente disponível.</span><span class="sxs-lookup"><span data-stu-id="99f25-121">It is considered stateless because hello service itself does not contain data that needs toobe stored reliably or made highly available.</span></span> <span data-ttu-id="99f25-122">Se uma instância de um serviço sem estado for desligada, todo seu estado interno será perdido.</span><span class="sxs-lookup"><span data-stu-id="99f25-122">If an instance of a stateless service shuts down, all of its internal state is lost.</span></span> <span data-ttu-id="99f25-123">Esse tipo de serviço, o estado deve ser repositório externo tooan persistente, como tabelas do Azure ou um banco de dados SQL, para que ele toobe feitas confiável e altamente disponível.</span><span class="sxs-lookup"><span data-stu-id="99f25-123">In this type of service, state must be persisted tooan external store, such as Azure Tables or a SQL database, for it toobe made highly available and reliable.</span></span>

<span data-ttu-id="99f25-124">Inicie o Visual Studio 2015 ou 2017 como administrador e crie um novo projeto de aplicativo do Service Fabric chamado *HelloWorld*:</span><span class="sxs-lookup"><span data-stu-id="99f25-124">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project named *HelloWorld*:</span></span>

![Use Olá novo projeto caixa de diálogo caixa toocreate um novo aplicativo de serviço de malha](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

<span data-ttu-id="99f25-126">Em seguida, crie um projeto de serviço sem estado chamado *HelloWorldStateless*:</span><span class="sxs-lookup"><span data-stu-id="99f25-126">Then create a stateless service project named *HelloWorldStateless*:</span></span>

![Na segunda caixa de diálogo hello, criar um projeto de serviço sem monitoração de estado](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

<span data-ttu-id="99f25-128">Agora, sua solução contém dois projetos:</span><span class="sxs-lookup"><span data-stu-id="99f25-128">Your solution now contains two projects:</span></span>

* <span data-ttu-id="99f25-129">*HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="99f25-129">*HelloWorld*.</span></span> <span data-ttu-id="99f25-130">Isso é hello *aplicativo* projeto que contém o *serviços*.</span><span class="sxs-lookup"><span data-stu-id="99f25-130">This is hello *application* project that contains your *services*.</span></span> <span data-ttu-id="99f25-131">Ele também contém o manifesto do aplicativo hello que descreve o aplicativo hello, bem como um número de scripts do PowerShell que ajudam você a toodeploy seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99f25-131">It also contains hello application manifest that describes hello application, as well as a number of PowerShell scripts that help you toodeploy your application.</span></span>
* <span data-ttu-id="99f25-132">*HelloWorldStateless*.</span><span class="sxs-lookup"><span data-stu-id="99f25-132">*HelloWorldStateless*.</span></span> <span data-ttu-id="99f25-133">Esse é o projeto de serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="99f25-133">This is hello service project.</span></span> <span data-ttu-id="99f25-134">Ele contém a implementação de serviço sem monitoração de estado de saudação.</span><span class="sxs-lookup"><span data-stu-id="99f25-134">It contains hello stateless service implementation.</span></span>

## <a name="implement-hello-service"></a><span data-ttu-id="99f25-135">Implementar o serviço de saudação</span><span class="sxs-lookup"><span data-stu-id="99f25-135">Implement hello service</span></span>
<span data-ttu-id="99f25-136">Olá abrir **HelloWorldStateless.cs** arquivo no projeto de serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="99f25-136">Open hello **HelloWorldStateless.cs** file in hello service project.</span></span> <span data-ttu-id="99f25-137">No Service Fabric, um serviço pode executar qualquer lógica de negócios.</span><span class="sxs-lookup"><span data-stu-id="99f25-137">In Service Fabric, a service can run any business logic.</span></span> <span data-ttu-id="99f25-138">API do serviço de saudação oferece dois pontos de entrada para o seu código:</span><span class="sxs-lookup"><span data-stu-id="99f25-138">hello service API provides two entry points for your code:</span></span>

* <span data-ttu-id="99f25-139">Um método de ponto de entrada em aberto chamado *RunAsync*, em que você pode começar a executar qualquer carga de trabalho, incluindo cargas de trabalho de computação de longa duração.</span><span class="sxs-lookup"><span data-stu-id="99f25-139">An open-ended entry point method, called *RunAsync*, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* <span data-ttu-id="99f25-140">Um ponto de entrada de comunicação em que você pode conectar a pilha de comunicação de sua escolha como o ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="99f25-140">A communication entry point where you can plug in your communication stack of choice, such as ASP.NET Core.</span></span> <span data-ttu-id="99f25-141">É onde você pode começar a receber solicitações de usuários e outros serviços.</span><span class="sxs-lookup"><span data-stu-id="99f25-141">This is where you can start receiving requests from users and other services.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

<span data-ttu-id="99f25-142">Neste tutorial, vamos nos concentrar em Olá `RunAsync()` método de ponto de entrada.</span><span class="sxs-lookup"><span data-stu-id="99f25-142">In this tutorial, we will focus on hello `RunAsync()` entry point method.</span></span> <span data-ttu-id="99f25-143">É aqui que você pode começar imediatamente a executar seu código.</span><span class="sxs-lookup"><span data-stu-id="99f25-143">This is where you can immediately start running your code.</span></span>
<span data-ttu-id="99f25-144">modelo de projeto de saudação inclui um exemplo da implementação de `RunAsync()` que incrementa uma contagem sem interrupção.</span><span class="sxs-lookup"><span data-stu-id="99f25-144">hello project template includes a sample implementation of `RunAsync()` that increments a rolling count.</span></span>

> [!NOTE]
> <span data-ttu-id="99f25-145">Para obter detalhes sobre como toowork com uma comunicação de pilha, consulte [serviços de API da Web do serviço do Fabric com auto-hospedagem OWIN](service-fabric-reliable-services-communication-webapi.md)</span><span class="sxs-lookup"><span data-stu-id="99f25-145">For details about how toowork with a communication stack, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md)</span></span>
> 
> 

### <a name="runasync"></a><span data-ttu-id="99f25-146">RunAsync</span><span class="sxs-lookup"><span data-stu-id="99f25-146">RunAsync</span></span>
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
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

<span data-ttu-id="99f25-147">plataforma de saudação chama este método quando uma instância de um serviço é tooexecute inserida e pronto.</span><span class="sxs-lookup"><span data-stu-id="99f25-147">hello platform calls this method when an instance of a service is placed and ready tooexecute.</span></span> <span data-ttu-id="99f25-148">Para um serviço sem monitoração de estado, que simplesmente significa que quando a instância do serviço de saudação é aberta.</span><span class="sxs-lookup"><span data-stu-id="99f25-148">For a stateless service, that simply means when hello service instance is opened.</span></span> <span data-ttu-id="99f25-149">Um token de cancelamento é fornecido toocoordinate quando toobe fechado as necessidades de sua instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="99f25-149">A cancellation token is provided toocoordinate when your service instance needs toobe closed.</span></span> <span data-ttu-id="99f25-150">Na malha do serviço, esse ciclo de abertura/fechamento de uma instância de serviço pode ocorrer muitas vezes em tempo de vida de saudação do serviço hello como um todo.</span><span class="sxs-lookup"><span data-stu-id="99f25-150">In Service Fabric, this open/close cycle of a service instance can occur many times over hello lifetime of hello service as a whole.</span></span> <span data-ttu-id="99f25-151">Isso pode ocorrer por vários motivos, incluindo:</span><span class="sxs-lookup"><span data-stu-id="99f25-151">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="99f25-152">sistema de saudação move suas instâncias de serviço de balanceamento de recursos.</span><span class="sxs-lookup"><span data-stu-id="99f25-152">hello system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="99f25-153">Ocorrem falhas no código.</span><span class="sxs-lookup"><span data-stu-id="99f25-153">Faults occur in your code.</span></span>
* <span data-ttu-id="99f25-154">aplicativo Hello ou o sistema é atualizado.</span><span class="sxs-lookup"><span data-stu-id="99f25-154">hello application or system is upgraded.</span></span>
* <span data-ttu-id="99f25-155">hardware subjacente Olá sofrer uma interrupção.</span><span class="sxs-lookup"><span data-stu-id="99f25-155">hello underlying hardware experiences an outage.</span></span>

<span data-ttu-id="99f25-156">Essa orquestração é gerenciada pelo Olá sistema tookeep seu serviço altamente disponível e adequadamente equilibrado.</span><span class="sxs-lookup"><span data-stu-id="99f25-156">This orchestration is managed by hello system tookeep your service highly available and properly balanced.</span></span>

<span data-ttu-id="99f25-157">`RunAsync()` não deve bloquear sincronicamente.</span><span class="sxs-lookup"><span data-stu-id="99f25-157">`RunAsync()` should not block synchronously.</span></span> <span data-ttu-id="99f25-158">Sua implementação de RunAsync deve retornar uma tarefa ou await em qualquer toocontinue de tempo de execução operações demoradas ou bloqueio tooallow hello.</span><span class="sxs-lookup"><span data-stu-id="99f25-158">Your implementation of RunAsync should return a Task or await on any long-running or blocking operations tooallow hello runtime toocontinue.</span></span> <span data-ttu-id="99f25-159">Observe que, no hello `while(true)` loop no exemplo anterior de saudação, retornando uma tarefa `await Task.Delay()` é usado.</span><span class="sxs-lookup"><span data-stu-id="99f25-159">Note in hello `while(true)` loop in hello previous example, a Task-returning `await Task.Delay()` is used.</span></span> <span data-ttu-id="99f25-160">Se sua carga de trabalho deve bloquear sincronicamente, agende uma nova tarefa com `Task.Run()` na sua implementação `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="99f25-160">If your workload must block synchronously, you should schedule a new Task with `Task.Run()` in your `RunAsync` implementation.</span></span>

<span data-ttu-id="99f25-161">O cancelamento da sua carga de trabalho é um esforço cooperativo orquestrado pelo Olá fornecido um token de cancelamento.</span><span class="sxs-lookup"><span data-stu-id="99f25-161">Cancellation of your workload is a cooperative effort orchestrated by hello provided cancellation token.</span></span> <span data-ttu-id="99f25-162">sistema Olá aguardará para sua tarefa tooend (pela conclusão bem-sucedida, cancelamento ou falha) antes de ele prossegue.</span><span class="sxs-lookup"><span data-stu-id="99f25-162">hello system will wait for your task tooend (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="99f25-163">É importante toohonor Olá cancelamento token, concluir qualquer trabalho e sair `RunAsync()` assim que possível quando o sistema Olá solicitações de cancelamento.</span><span class="sxs-lookup"><span data-stu-id="99f25-163">It is important toohonor hello cancellation token, finish any work, and exit `RunAsync()` as quickly as possible when hello system requests cancellation.</span></span>

<span data-ttu-id="99f25-164">Neste exemplo de serviço sem monitoração de estado, a contagem de saudação é armazenada em uma variável local.</span><span class="sxs-lookup"><span data-stu-id="99f25-164">In this stateless service example, hello count is stored in a local variable.</span></span> <span data-ttu-id="99f25-165">Mas porque este é um serviço sem monitoração de estado, valor Olá armazenado existe somente para Olá atual do ciclo de vida da sua instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="99f25-165">But because this is a stateless service, hello value that's stored exists only for hello current lifecycle of its service instance.</span></span> <span data-ttu-id="99f25-166">Quando o serviço Olá move ou reinicia, o valor de saudação é perdido.</span><span class="sxs-lookup"><span data-stu-id="99f25-166">When hello service moves or restarts, hello value is lost.</span></span>

## <a name="create-a-stateful-service"></a><span data-ttu-id="99f25-167">Criar um serviço com estado</span><span class="sxs-lookup"><span data-stu-id="99f25-167">Create a stateful service</span></span>
<span data-ttu-id="99f25-168">O Service Fabric introduz um novo tipo de serviço que é com estado.</span><span class="sxs-lookup"><span data-stu-id="99f25-168">Service Fabric introduces a new kind of service that is stateful.</span></span> <span data-ttu-id="99f25-169">Um serviço com monitoração de estado pode manter o estado confiável no serviço de saudação em si, colocalizado com o código de saudação que ele está em uso.</span><span class="sxs-lookup"><span data-stu-id="99f25-169">A stateful service can maintain state reliably within hello service itself, co-located with hello code that's using it.</span></span> <span data-ttu-id="99f25-170">Estado é feito altamente disponível pela malha do serviço sem Olá necessidade toopersist estado tooan repositório de externo.</span><span class="sxs-lookup"><span data-stu-id="99f25-170">State is made highly available by Service Fabric without hello need toopersist state tooan external store.</span></span>

<span data-ttu-id="99f25-171">tooconvert um valor do contador de toohighly sem monitoração de estado persistente e disponível, mesmo quando o serviço de saudação move ou for reiniciado, você precisa um serviço com monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="99f25-171">tooconvert a counter value from stateless toohighly available and persistent, even when hello service moves or restarts, you need a stateful service.</span></span>

<span data-ttu-id="99f25-172">Em Olá mesmo *HelloWorld* aplicativo, você pode adicionar um novo serviço clicando nas referências de serviços Olá no projeto de aplicativo hello e selecionando **Adicionar -> novo serviço do Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="99f25-172">In hello same *HelloWorld* application, you can add a new service by right-clicking on hello Services references in hello application project and selecting **Add ->  New Service Fabric Service**.</span></span>

![Adicionar um serviço tooyour aplicativo do Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

<span data-ttu-id="99f25-174">Selecione **Serviço com Estado** e dê o nome de *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="99f25-174">Select **Stateful Service** and name it *HelloWorldStateful*.</span></span> <span data-ttu-id="99f25-175">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="99f25-175">Click **OK**.</span></span>

![Usar toocreate de caixa de diálogo do hello novo projeto um novo serviço de monitoração de estado do Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

<span data-ttu-id="99f25-177">Seu aplicativo agora deve ter dois serviços: Olá serviço sem monitoração de estado *HelloWorldStateless* e o serviço com monitoração de estado Olá *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="99f25-177">Your application should now have two services: hello stateless service *HelloWorldStateless* and hello stateful service *HelloWorldStateful*.</span></span>

<span data-ttu-id="99f25-178">Um serviço com monitoração de estado tem Olá mesmo pontos de entrada como um serviço sem monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="99f25-178">A stateful service has hello same entry points as a stateless service.</span></span> <span data-ttu-id="99f25-179">Olá principal diferença é a disponibilidade de saudação de um *provedor de estado* que pode armazenar o estado confiável.</span><span class="sxs-lookup"><span data-stu-id="99f25-179">hello main difference is hello availability of a *state provider* that can store state reliably.</span></span> <span data-ttu-id="99f25-180">Service Fabric vem com uma implementação de provedor de estado chamada [coleções confiável](service-fabric-reliable-services-reliable-collections.md), que permite que você crie estruturas de dados replicados por meio de saudação Gerenciador de estado confiável.</span><span class="sxs-lookup"><span data-stu-id="99f25-180">Service Fabric comes with a state provider implementation called [Reliable Collections](service-fabric-reliable-services-reliable-collections.md), which lets you create replicated data structures through hello Reliable State Manager.</span></span> <span data-ttu-id="99f25-181">Por padrão, um serviço confiável com estado usa esse provedor de estado.</span><span class="sxs-lookup"><span data-stu-id="99f25-181">A stateful Reliable Service uses this state provider by default.</span></span>

<span data-ttu-id="99f25-182">Abra **HelloWorldStateful.cs** na *HelloWorldStateful*, que contém a saudação RunAsync método a seguir:</span><span class="sxs-lookup"><span data-stu-id="99f25-182">Open **HelloWorldStateful.cs** in *HelloWorldStateful*, which contains hello following RunAsync method:</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
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

            // If an exception is thrown before calling CommitAsync, hello transaction aborts, all changes are
            // discarded, and nothing is saved toohello secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a><span data-ttu-id="99f25-183">RunAsync</span><span class="sxs-lookup"><span data-stu-id="99f25-183">RunAsync</span></span>
<span data-ttu-id="99f25-184">`RunAsync()` opera da mesma forma em serviços com e sem estado.</span><span class="sxs-lookup"><span data-stu-id="99f25-184">`RunAsync()` operates similarly in stateful and stateless services.</span></span> <span data-ttu-id="99f25-185">No entanto, em um serviço com monitoração de estado, plataforma Olá executa trabalho adicional em seu nome antes de executar `RunAsync()`.</span><span class="sxs-lookup"><span data-stu-id="99f25-185">However, in a stateful service, hello platform performs additional work on your behalf before it executes `RunAsync()`.</span></span> <span data-ttu-id="99f25-186">Esse trabalho pode incluir garantindo que o Gerenciador de estado confiável hello e coleções confiável são toouse pronto.</span><span class="sxs-lookup"><span data-stu-id="99f25-186">This work can include ensuring that hello Reliable State Manager and Reliable Collections are ready toouse.</span></span>

### <a name="reliable-collections-and-hello-reliable-state-manager"></a><span data-ttu-id="99f25-187">Coleções e Olá confiável Gerenciador de estado confiável</span><span class="sxs-lookup"><span data-stu-id="99f25-187">Reliable Collections and hello Reliable State Manager</span></span>
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

<span data-ttu-id="99f25-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) é uma implementação de dicionário que você pode usar tooreliably o estado do repositório no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="99f25-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) is a dictionary implementation that you can use tooreliably store state in hello service.</span></span> <span data-ttu-id="99f25-189">Com o Service Fabric e coleções confiável, você pode armazenar dados diretamente em seu serviço sem necessidade de saudação de um repositório persistente externo.</span><span class="sxs-lookup"><span data-stu-id="99f25-189">With Service Fabric and Reliable Collections, you can store data directly in your service without hello need for an external persistent store.</span></span> <span data-ttu-id="99f25-190">As Coleções Confiáveis tornam os dados altamente disponíveis.</span><span class="sxs-lookup"><span data-stu-id="99f25-190">Reliable Collections make your data highly available.</span></span> <span data-ttu-id="99f25-191">O Service Fabric consegue isso criando e gerenciando várias *réplicas* do seu serviço para você.</span><span class="sxs-lookup"><span data-stu-id="99f25-191">Service Fabric accomplishes this by creating and managing multiple *replicas* of your service for you.</span></span> <span data-ttu-id="99f25-192">Ele também fornece uma API que abstrai complexidades Olá longe de gerenciar suas transições de estado e as réplicas.</span><span class="sxs-lookup"><span data-stu-id="99f25-192">It also provides an API that abstracts away hello complexities of managing those replicas and their state transitions.</span></span>

<span data-ttu-id="99f25-193">As Reliable Collections podem armazenar qualquer tipo .NET, incluindo tipos personalizados, com algumas limitações:</span><span class="sxs-lookup"><span data-stu-id="99f25-193">Reliable Collections can store any .NET type, including your custom types, with a couple of caveats:</span></span>

* <span data-ttu-id="99f25-194">Service Fabric torna seu estado altamente disponível pelo *replicando* disco toolocal de dados de armazenamento de estado entre nós e coleções confiável em cada réplica.</span><span class="sxs-lookup"><span data-stu-id="99f25-194">Service Fabric makes your state highly available by *replicating* state across nodes, and Reliable Collections store your data toolocal disk on each replica.</span></span> <span data-ttu-id="99f25-195">Isso significa que tudo o que é armazenado nas Coleções Confiáveis deve ser *serializável*.</span><span class="sxs-lookup"><span data-stu-id="99f25-195">This means that everything that is stored in Reliable Collections must be *serializable*.</span></span> <span data-ttu-id="99f25-196">Por padrão, use coleções confiável [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) para serialização, portanto, é importante toomake-se de que seus tipos são [Olá serializador de contrato de dados com suporte](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) quando você usa o padrão de saudação serializador.</span><span class="sxs-lookup"><span data-stu-id="99f25-196">By default, Reliable Collections use [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) for serialization, so it's important toomake sure that your types are [supported by hello Data Contract Serializer](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) when you use hello default serializer.</span></span>
* <span data-ttu-id="99f25-197">Os objetos são replicados para alta disponibilidade quando você confirma uma transação nas Reliable Collections.</span><span class="sxs-lookup"><span data-stu-id="99f25-197">Objects are replicated for high availability when you commit transactions on Reliable Collections.</span></span> <span data-ttu-id="99f25-198">Objetos armazenados nas Reliable Collections são mantidos na memória local do serviço.</span><span class="sxs-lookup"><span data-stu-id="99f25-198">Objects stored in Reliable Collections are kept in local memory in your service.</span></span> <span data-ttu-id="99f25-199">Isso significa que você tenha um objeto de toohello referência local.</span><span class="sxs-lookup"><span data-stu-id="99f25-199">This means that you have a local reference toohello object.</span></span>
  
   <span data-ttu-id="99f25-200">É importante que você não modificar as instâncias locais desses objetos sem executar uma operação de atualização na coleção de saudação confiável em uma transação.</span><span class="sxs-lookup"><span data-stu-id="99f25-200">It is important that you do not mutate local instances of those objects without performing an update operation on hello reliable collection in a transaction.</span></span> <span data-ttu-id="99f25-201">Isso ocorre porque as alterações toolocal instâncias de objetos não serão replicadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="99f25-201">This is because changes toolocal instances of objects will not be replicated automatically.</span></span> <span data-ttu-id="99f25-202">Você deve inserir novamente o objeto de saudação no dicionário de saudação ou usar uma saudação *atualizar* métodos no dicionário de saudação.</span><span class="sxs-lookup"><span data-stu-id="99f25-202">You must re-insert hello object back into hello dictionary or use one of hello *update* methods on hello dictionary.</span></span>

<span data-ttu-id="99f25-203">Gerenciador de estado confiável de saudação gerencia coleções confiável para você.</span><span class="sxs-lookup"><span data-stu-id="99f25-203">hello Reliable State Manager manages Reliable Collections for you.</span></span> <span data-ttu-id="99f25-204">Você pode simplesmente pedir Olá confiável Gerenciador de estado para um conjunto confiável por nome a qualquer momento e em qualquer lugar em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="99f25-204">You can simply ask hello Reliable State Manager for a reliable collection by name at any time and at any place in your service.</span></span> <span data-ttu-id="99f25-205">Olá Gerenciador de estado confiável garante que você obtenha uma referência de volta.</span><span class="sxs-lookup"><span data-stu-id="99f25-205">hello Reliable State Manager ensures that you get a reference back.</span></span> <span data-ttu-id="99f25-206">Não recomendamos salvar referências tooreliable instâncias de coleção em variáveis de membro de classe ou propriedades.</span><span class="sxs-lookup"><span data-stu-id="99f25-206">We don't recommended that you save references tooreliable collection instances in class member variables or properties.</span></span> <span data-ttu-id="99f25-207">Deve ter especial cuidado tooensure Olá referência é definida em todos os momentos tooan instância Olá ciclo de vida do serviço.</span><span class="sxs-lookup"><span data-stu-id="99f25-207">Special care must be taken tooensure that hello reference is set tooan instance at all times in hello service lifecycle.</span></span> <span data-ttu-id="99f25-208">Olá Gerenciador de estado confiável trata esse trabalho para você, e é otimizado para visitas a repetição.</span><span class="sxs-lookup"><span data-stu-id="99f25-208">hello Reliable State Manager handles this work for you, and it's optimized for repeat visits.</span></span>

### <a name="transactional-and-asynchronous-operations"></a><span data-ttu-id="99f25-209">Operações transacionais e assíncronas</span><span class="sxs-lookup"><span data-stu-id="99f25-209">Transactional and asynchronous operations</span></span>
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

<span data-ttu-id="99f25-210">Coleções confiáveis têm muitos Olá mesmas operações que seus `System.Collections.Generic` e `System.Collections.Concurrent` equivalentes, exceto LINQ.</span><span class="sxs-lookup"><span data-stu-id="99f25-210">Reliable Collections have many of hello same operations that their `System.Collections.Generic` and `System.Collections.Concurrent` counterparts do, except LINQ.</span></span> <span data-ttu-id="99f25-211">As operações nas Coleções Confiáveis são assíncronas.</span><span class="sxs-lookup"><span data-stu-id="99f25-211">Operations on Reliable Collections are asynchronous.</span></span> <span data-ttu-id="99f25-212">Isso ocorre porque as operações de gravação com coleções confiável executam tooreplicate de operações de e/s e manter dados toodisk.</span><span class="sxs-lookup"><span data-stu-id="99f25-212">This is because write operations with Reliable Collections perform I/O operations tooreplicate and persist data toodisk.</span></span>

<span data-ttu-id="99f25-213">As operações de Coleção Confiável são *transacionais*, de modo que você pode manter o estado consistente entre várias Coleções Confiáveis e operações.</span><span class="sxs-lookup"><span data-stu-id="99f25-213">Reliable Collection operations are *transactional*, so that you can keep state consistent across multiple Reliable Collections and operations.</span></span> <span data-ttu-id="99f25-214">Por exemplo, você pode remover da fila um item de trabalho de uma fila confiável, executar uma operação sobre ele e salvar o resultado de saudação em um dicionário confiável, tudo em uma única transação.</span><span class="sxs-lookup"><span data-stu-id="99f25-214">For example, you may dequeue a work item from a Reliable Queue, perform an operation on it, and save hello result in a Reliable Dictionary, all within a single transaction.</span></span> <span data-ttu-id="99f25-215">Isso é tratado como uma operação atômica, e garante que toda a operação Olá terá êxito ou saudação de toda a operação será revertida.</span><span class="sxs-lookup"><span data-stu-id="99f25-215">This is treated as an atomic operation, and it guarantees that either hello entire operation will succeed or hello entire operation will roll back.</span></span> <span data-ttu-id="99f25-216">Se ocorrer um erro após a remoção da fila item hello, mas antes de salvar o resultado de hello, transação inteira Olá é revertida e item Olá permanece na fila de saudação para processamento.</span><span class="sxs-lookup"><span data-stu-id="99f25-216">If an error occurs after you dequeue hello item but before you save hello result, hello entire transaction is rolled back and hello item remains in hello queue for processing.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="99f25-217">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="99f25-217">Run hello application</span></span>
<span data-ttu-id="99f25-218">Agora retornamos toohello *HelloWorld* aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99f25-218">We now return toohello *HelloWorld* application.</span></span> <span data-ttu-id="99f25-219">Agora você pode criar e implantar seus serviços.</span><span class="sxs-lookup"><span data-stu-id="99f25-219">You can now build and deploy your services.</span></span> <span data-ttu-id="99f25-220">Quando você pressiona **F5**, seu aplicativo estará cluster local tooyour construído e implantado.</span><span class="sxs-lookup"><span data-stu-id="99f25-220">When you press **F5**, your application will be built and deployed tooyour local cluster.</span></span>

<span data-ttu-id="99f25-221">Depois de iniciar a execução de serviços hello, você pode exibir hello gerado eventos de rastreamento de eventos para Windows (ETW) em um **eventos de diagnóstico** janela.</span><span class="sxs-lookup"><span data-stu-id="99f25-221">After hello services start running, you can view hello generated Event Tracing for Windows (ETW) events in a **Diagnostic Events** window.</span></span> <span data-ttu-id="99f25-222">Observe que os eventos de saudação exibidos são de serviço sem monitoração de estado hello e o serviço de monitoração de estado Olá no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="99f25-222">Note that hello events displayed are from both hello stateless service and hello stateful service in hello application.</span></span> <span data-ttu-id="99f25-223">Você pode pausar Fluxo Olá clicando Olá **pausar** botão.</span><span class="sxs-lookup"><span data-stu-id="99f25-223">You can pause hello stream by clicking hello **Pause** button.</span></span> <span data-ttu-id="99f25-224">Você pode examinar os detalhes de saudação de uma mensagem expandindo essa mensagem.</span><span class="sxs-lookup"><span data-stu-id="99f25-224">You can then examine hello details of a message by expanding that message.</span></span>

> [!NOTE]
> <span data-ttu-id="99f25-225">Antes de executar o aplicativo hello, certifique-se de que você tenha um cluster de desenvolvimento local em execução.</span><span class="sxs-lookup"><span data-stu-id="99f25-225">Before you run hello application, make sure that you have a local development cluster running.</span></span> <span data-ttu-id="99f25-226">Check-out Olá [guia de Introdução](service-fabric-get-started.md) para obter informações sobre como configurar seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="99f25-226">Check out hello [getting started guide](service-fabric-get-started.md) for information on setting up your local environment.</span></span>
> 
> 

![Exibir Eventos de Diagnóstico no Visual Studio](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a><span data-ttu-id="99f25-228">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="99f25-228">Next steps</span></span>
[<span data-ttu-id="99f25-229">Depurar seu aplicativo do Service Fabric usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="99f25-229">Debug your Service Fabric application in Visual Studio</span></span>](service-fabric-debugging-your-application.md)

[<span data-ttu-id="99f25-230">Introdução aos serviços de API Web do Service Fabric com auto-hospedagem OWIN</span><span class="sxs-lookup"><span data-stu-id="99f25-230">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>](service-fabric-reliable-services-communication-webapi.md)

[<span data-ttu-id="99f25-231">Saiba mais sobre as Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="99f25-231">Learn more about Reliable Collections</span></span>](service-fabric-reliable-services-reliable-collections.md)

[<span data-ttu-id="99f25-232">Implantar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="99f25-232">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[<span data-ttu-id="99f25-233">Atualização de aplicativo</span><span class="sxs-lookup"><span data-stu-id="99f25-233">Application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="99f25-234">Referência do desenvolvedor para Reliable Services</span><span class="sxs-lookup"><span data-stu-id="99f25-234">Developer reference for Reliable Services</span></span>](https://msdn.microsoft.com/library/azure/dn706529.aspx)

