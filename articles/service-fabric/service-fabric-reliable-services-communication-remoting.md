---
title: "comunicação remota do aaaService na malha do serviço | Microsoft Docs"
description: "Comunicação remota do Service Fabric permite que os clientes e serviços toocommunicate com serviços usando uma chamada de procedimento remoto."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: abfaf430-fea0-4974-afba-cfc9f9f2354b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: vturecek
ms.openlocfilehash: 14682cf8671a85e04144eccf97803ab67c258875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="a2c8b-103">Comunicação remota de serviço com o Reliable Services</span><span class="sxs-lookup"><span data-stu-id="a2c8b-103">Service remoting with Reliable Services</span></span>
<span data-ttu-id="a2c8b-104">Para serviços que não são vinculados tooa protocolo de comunicação específica ou a pilha, como WebAPI, Windows Communication Foundation (WCF) ou outras pessoas, Olá confiável Services framework fornece um tooquickly do mecanismo de comunicação remota e configurar com facilidade a chamada de procedimento remoto para serviços.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-104">For services that are not tied tooa particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, hello Reliable Services framework provides a remoting mechanism tooquickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="a2c8b-105">Configurar a comunicação remota em um serviço</span><span class="sxs-lookup"><span data-stu-id="a2c8b-105">Set up remoting on a service</span></span>
<span data-ttu-id="a2c8b-106">A configuração da comunicação remota de um serviço é feita em duas etapas simples:</span><span class="sxs-lookup"><span data-stu-id="a2c8b-106">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="a2c8b-107">Crie uma interface para o serviço tooimplement.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-107">Create an interface for your service tooimplement.</span></span> <span data-ttu-id="a2c8b-108">Essa interface define os métodos de saudação que estarão disponíveis para uma chamada de procedimento remoto em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-108">This interface defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="a2c8b-109">métodos de saudação devem ser retorno métodos assíncronos.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-109">hello methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="a2c8b-110">interface Olá deve implementar `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal que Olá serviço tem uma interface de comunicação remota.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-110">hello interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal that hello service has a remoting interface.</span></span>
2. <span data-ttu-id="a2c8b-111">Use um ouvinte de comunicação remota em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-111">Use a remoting listener in your service.</span></span> <span data-ttu-id="a2c8b-112">Esta é uma implementação de `ICommunicationListener` que fornece recursos de comunicação remota.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-112">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="a2c8b-113">Olá `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contém um método de extensão`CreateServiceRemotingListener` para com e sem monitoração de serviços que pode ser usado toocreate um ouvinte de comunicação remota usando protocolo de transporte de comunicação remota saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-113">hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method,`CreateServiceRemotingListener` for both stateless and stateful services that can be used toocreate a remoting listener using hello default remoting transport protocol.</span></span>

<span data-ttu-id="a2c8b-114">Observação: Olá `Remoting` namespace está disponível como um pacote do nuget separado chamado`Microsoft.ServiceFabric.Services.Remoting`</span><span class="sxs-lookup"><span data-stu-id="a2c8b-114">Note: hello `Remoting` namespace is available as a seperate nuget package called `Microsoft.ServiceFabric.Services.Remoting`</span></span> 

<span data-ttu-id="a2c8b-115">Por exemplo, hello seguinte serviço sem monitoração de estado expõe um único método tooget "Hello World" passar por uma chamada de procedimento remoto.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-115">For example, hello following stateless service exposes a single method tooget "Hello World" over a remote procedure call.</span></span>

```csharp
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Remoting;
using Microsoft.ServiceFabric.Services.Remoting.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

public interface IMyService : IService
{
    Task<string> HelloWorldAsync();
}

class MyService : StatelessService, IMyService
{
    public MyService(StatelessServiceContext context)
        : base (context)
    {
    }

    public Task HelloWorldAsync()
    {
        return Task.FromResult("Hello!");
    }

    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] { new ServiceInstanceListener(context =>            this.CreateServiceRemotingListener(context)) };
    }
}
```
> [!NOTE]
> <span data-ttu-id="a2c8b-116">Olá argumentos e hello retornam tipos na interface de serviço Olá podem ser quaisquer tipos simples, complexos ou personalizados, mas eles devem ser serializáveis por Olá .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2c8b-116">hello arguments and hello return types in hello service interface can be any simple, complex, or custom types, but they must be serializable by hello .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="a2c8b-117">Chamar métodos de serviços remotos</span><span class="sxs-lookup"><span data-stu-id="a2c8b-117">Call remote service methods</span></span>
<span data-ttu-id="a2c8b-118">Chamar métodos em um serviço usando a pilha de comunicação remota Olá é feito por meio de um serviço de toohello de proxy local por meio de saudação `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` classe.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-118">Calling methods on a service by using hello remoting stack is done by using a local proxy toohello service through hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span></span> <span data-ttu-id="a2c8b-119">Olá `ServiceProxy` método cria um proxy local usando Olá mesma interface que Olá serviço implementa.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-119">hello `ServiceProxy` method creates a local proxy by using hello same interface that hello service implements.</span></span> <span data-ttu-id="a2c8b-120">Com o proxy, você pode simplesmente chamar métodos na interface Olá remotamente.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-120">With that proxy, you can simply call methods on hello interface remotely.</span></span>

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

<span data-ttu-id="a2c8b-121">estrutura de comunicação remota Olá propaga exceções geradas no cliente do serviço de saudação toohello.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-121">hello remoting framework propagates exceptions thrown at hello service toohello client.</span></span> <span data-ttu-id="a2c8b-122">Lógica de tratamento de exceção assim no cliente hello usando `ServiceProxy` diretamente pode lidar com exceções que Olá lança de serviço.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-122">So exception-handling logic at hello client by using `ServiceProxy` can directly handle exceptions that hello service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="a2c8b-123">Tempo de vida de Proxy do Serviço</span><span class="sxs-lookup"><span data-stu-id="a2c8b-123">Service Proxy Lifetime</span></span>
<span data-ttu-id="a2c8b-124">A criação do ServiceProxy é uma operação simples, logo, o usuário pode criar quantos precisar.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-124">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="a2c8b-125">O Proxy do Serviço pode ser reutilizado desde que o usuário precise.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-125">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="a2c8b-126">Usuário possa reutilizar Olá proxy mesmo em caso de exceção.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-126">User can re-use hello same proxy in case of Exception.</span></span> <span data-ttu-id="a2c8b-127">Cada ServiceProxy contém mensagens de toosend de cliente usado de comunicação durante transmissão hello.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-127">Each ServiceProxy contains communciation client used toosend messages over hello wire.</span></span> <span data-ttu-id="a2c8b-128">Ao chamar a API, temos toosee verificação interna, se o cliente de comunicação usado é válido.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-128">While invoking API, we have internal check toosee if communication client used is valid.</span></span> <span data-ttu-id="a2c8b-129">Com base no resultado, podemos criar novamente cliente de comunicação de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-129">Based on that result, we re-create hello communication client.</span></span> <span data-ttu-id="a2c8b-130">Portanto, o usuário não precisa serviceproxy toorecreate em caso de exceção.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-130">Hence user do not need toorecreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="a2c8b-131">Tempo de vida de ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="a2c8b-131">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="a2c8b-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) é um alocador que cria um proxy para interfaces remotas diferentes.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="a2c8b-133">Se você usar a API ServiceProxy.Create para criar um proxy, o framework cria Olá singelton ServiceProxyFactory.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-133">If you use API ServiceProxy.Create for creating proxy, then framework creates hello singelton ServiceProxyFactory.</span></span>
<span data-ttu-id="a2c8b-134">É útil toocreate um manualmente quando precisar toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) propriedades.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-134">It is useful toocreate one manually when you need toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) properties.</span></span>
<span data-ttu-id="a2c8b-135">Alocador é uma operação cara.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-135">Factory is an expensive operation.</span></span> <span data-ttu-id="a2c8b-136">ServiceProxyFactory mantém o cache do cliente de comunicação.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-136">ServiceProxyFactory maintains cache of communication client.</span></span>
<span data-ttu-id="a2c8b-137">Prática recomendada é toocache ServiceProxyFactory por tempo possível.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-137">Best practice is toocache ServiceProxyFactory for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="a2c8b-138">Tratamento de exceções remotas</span><span class="sxs-lookup"><span data-stu-id="a2c8b-138">Remoting Exception Handling</span></span>
<span data-ttu-id="a2c8b-139">Todos os Olá remoto exceção pela API de serviço são enviados toohello back cliente como AggregateException.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-139">All hello remote exception thrown by service API, are sent back toohello client as AggregateException.</span></span> <span data-ttu-id="a2c8b-140">RemoteExceptions devem ser serializáveis DataContract [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) gerada toohello proxy API com o erro de serialização Olá nele.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-140">RemoteExceptions should be DataContract Serializable otherwise [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) is thrown toohello proxy API with hello serialization error in it.</span></span>

<span data-ttu-id="a2c8b-141">ServiceProxy lidar com todas as exceções de Failover para a partição de serviço de hello, ele é criado para.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-141">ServiceProxy does handle all Failover Exception for hello service partition it  is created for.</span></span> <span data-ttu-id="a2c8b-142">Novamente, ele resolve os pontos de extremidade de saudação se houver Failover Exceptions(Non-Transient Exceptions) e repetições chamada hello com ponto de extremidade correto hello.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-142">It re-resolves hello endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries hello call with hello correct endpoint.</span></span> <span data-ttu-id="a2c8b-143">O número de tentativas da exceção de failover é indefinido.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="a2c8b-144">No caso de TransientExceptions, ele repete apenas chamada hello.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-144">In case of TransientExceptions, it only retries hello call.</span></span>

<span data-ttu-id="a2c8b-145">Os parâmetros de repetição padrão são fornecidos por [OperationRetrySettings].</span><span class="sxs-lookup"><span data-stu-id="a2c8b-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="a2c8b-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Usuário pode configurar esses valores, passando o construtor de tooServiceProxyFactory OperationRetrySettings objeto.</span><span class="sxs-lookup"><span data-stu-id="a2c8b-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) User can configure these values by passing OperationRetrySettings object tooServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2c8b-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a2c8b-147">Next steps</span></span>
* [<span data-ttu-id="a2c8b-148">API Web com OWIN no Reliable Services</span><span class="sxs-lookup"><span data-stu-id="a2c8b-148">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="a2c8b-149">Comunicação WCF com o Reliable Services</span><span class="sxs-lookup"><span data-stu-id="a2c8b-149">WCF communication with Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* [<span data-ttu-id="a2c8b-150">Securing communication for Reliable Services</span><span class="sxs-lookup"><span data-stu-id="a2c8b-150">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
