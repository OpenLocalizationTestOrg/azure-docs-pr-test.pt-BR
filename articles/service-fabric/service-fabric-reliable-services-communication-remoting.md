---
title: "<span data-ttu-id=\"01f32-101\">Comunicação remota do serviço no Service Fabric | Microsoft Docs</span><span class=\"sxs-lookup\"><span data-stu-id=\"01f32-101\">Service remoting in Service Fabric | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"01f32-102\">A comunicação remota do Service Fabric permite que os clientes e serviços se comuniquem com serviços que usam a chamada de procedimento remoto.</span><span class=\"sxs-lookup\"><span data-stu-id=\"01f32-102\">Service Fabric remoting allows clients and services to communicate with services by using a remote procedure call.</span></span>"
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
ms.openlocfilehash: 92a8894f24c234fbf38eda086531b524cceccfc1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="01f32-103">Comunicação remota de serviço com o Reliable Services</span><span class="sxs-lookup"><span data-stu-id="01f32-103">Service remoting with Reliable Services</span></span>
<span data-ttu-id="01f32-104">Para serviços que não estão vinculados a um protocolo de comunicação específico ou pilha, como WebAPI, WCF (Windows Communication Foundation) ou outros, a estrutura do Reliable Services fornece um mecanismo de comunicação remota para configurar a chamada de procedimento remoto para serviços de forma rápida e fácil.</span><span class="sxs-lookup"><span data-stu-id="01f32-104">For services that are not tied to a particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, the Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="01f32-105">Configurar a comunicação remota em um serviço</span><span class="sxs-lookup"><span data-stu-id="01f32-105">Set up remoting on a service</span></span>
<span data-ttu-id="01f32-106">A configuração da comunicação remota de um serviço é feita em duas etapas simples:</span><span class="sxs-lookup"><span data-stu-id="01f32-106">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="01f32-107">Crie uma interface para implementar o serviço.</span><span class="sxs-lookup"><span data-stu-id="01f32-107">Create an interface for your service to implement.</span></span> <span data-ttu-id="01f32-108">Essa interface define os métodos que estarão disponíveis para chamada de procedimento remoto no seu serviço.</span><span class="sxs-lookup"><span data-stu-id="01f32-108">This interface defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="01f32-109">Os métodos devem ser métodos assíncronos que retornam tarefas.</span><span class="sxs-lookup"><span data-stu-id="01f32-109">The methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="01f32-110">A interface deve implementar `Microsoft.ServiceFabric.Services.Remoting.IService` para sinalizar que o serviço tem uma interface de comunicação remota.</span><span class="sxs-lookup"><span data-stu-id="01f32-110">The interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` to signal that the service has a remoting interface.</span></span>
2. <span data-ttu-id="01f32-111">Use um ouvinte de comunicação remota em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="01f32-111">Use a remoting listener in your service.</span></span> <span data-ttu-id="01f32-112">Esta é uma implementação de `ICommunicationListener` que fornece recursos de comunicação remota.</span><span class="sxs-lookup"><span data-stu-id="01f32-112">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="01f32-113">O namespace `Microsoft.ServiceFabric.Services.Remoting.Runtime` contém um método de extensão, `CreateServiceRemotingListener`, para serviços com e sem estado que podem ser usados para criar um ouvinte de comunicação remota usando o protocolo de transporte remoto padrão.</span><span class="sxs-lookup"><span data-stu-id="01f32-113">The `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method,`CreateServiceRemotingListener` for both stateless and stateful services that can be used to create a remoting listener using the default remoting transport protocol.</span></span>

<span data-ttu-id="01f32-114">Observação: o namespace `Remoting` está disponível como um pacote do nuget separado chamado `Microsoft.ServiceFabric.Services.Remoting`</span><span class="sxs-lookup"><span data-stu-id="01f32-114">Note: The `Remoting` namespace is available as a seperate nuget package called `Microsoft.ServiceFabric.Services.Remoting`</span></span> 

<span data-ttu-id="01f32-115">Por exemplo, o serviço sem estado a seguir expõe um único método para obter "Hello World" pela chamada de procedimento remoto.</span><span class="sxs-lookup"><span data-stu-id="01f32-115">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span></span>

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
> <span data-ttu-id="01f32-116">Os argumentos e os tipos de retorno na interface de serviço podem ser tipos simples, complexos ou personalizados, mas devem ser serializáveis pelo [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx)do .NET.</span><span class="sxs-lookup"><span data-stu-id="01f32-116">The arguments and the return types in the service interface can be any simple, complex, or custom types, but they must be serializable by the .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="01f32-117">Chamar métodos de serviços remotos</span><span class="sxs-lookup"><span data-stu-id="01f32-117">Call remote service methods</span></span>
<span data-ttu-id="01f32-118">A chamada de métodos em um serviço usando a pilha de comunicação remota é feita usando um proxy local para o serviço por meio da classe `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` .</span><span class="sxs-lookup"><span data-stu-id="01f32-118">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span></span> <span data-ttu-id="01f32-119">O método `ServiceProxy` cria um proxy local usando a mesma interface que o serviço implementa.</span><span class="sxs-lookup"><span data-stu-id="01f32-119">The `ServiceProxy` method creates a local proxy by using the same interface that the service implements.</span></span> <span data-ttu-id="01f32-120">Com esse proxy, você pode simplesmente chamar métodos na interface remotamente.</span><span class="sxs-lookup"><span data-stu-id="01f32-120">With that proxy, you can simply call methods on the interface remotely.</span></span>

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

<span data-ttu-id="01f32-121">A estrutura remota propaga exceções lançadas no serviço para o cliente.</span><span class="sxs-lookup"><span data-stu-id="01f32-121">The remoting framework propagates exceptions thrown at the service to the client.</span></span> <span data-ttu-id="01f32-122">A lógica de manipulação de exceção no cliente usando `ServiceProxy` pode manipular diretamente as exceções que o serviço lança.</span><span class="sxs-lookup"><span data-stu-id="01f32-122">So exception-handling logic at the client by using `ServiceProxy` can directly handle exceptions that the service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="01f32-123">Tempo de vida de Proxy do Serviço</span><span class="sxs-lookup"><span data-stu-id="01f32-123">Service Proxy Lifetime</span></span>
<span data-ttu-id="01f32-124">A criação do ServiceProxy é uma operação simples, logo, o usuário pode criar quantos precisar.</span><span class="sxs-lookup"><span data-stu-id="01f32-124">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="01f32-125">O Proxy do Serviço pode ser reutilizado desde que o usuário precise.</span><span class="sxs-lookup"><span data-stu-id="01f32-125">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="01f32-126">O usuário pode reutilizar o mesmo proxy em caso de exceção.</span><span class="sxs-lookup"><span data-stu-id="01f32-126">User can re-use the same proxy in case of Exception.</span></span> <span data-ttu-id="01f32-127">Cada ServiceProxy contém um cliente de comunicação usado para enviar mensagens durante a transmissão.</span><span class="sxs-lookup"><span data-stu-id="01f32-127">Each ServiceProxy contains communciation client used to send messages over the wire.</span></span> <span data-ttu-id="01f32-128">Ao invocar a API, temos uma verificação interna para saber se o cliente de comunicação usado é válido.</span><span class="sxs-lookup"><span data-stu-id="01f32-128">While invoking API, we have internal check to see if communication client used is valid.</span></span> <span data-ttu-id="01f32-129">Com base nesse resultado, recriamos o cliente da comunicação.</span><span class="sxs-lookup"><span data-stu-id="01f32-129">Based on that result, we re-create the communication client.</span></span> <span data-ttu-id="01f32-130">Portanto, o usuário não precisa recriar serviceproxy em caso de exceção.</span><span class="sxs-lookup"><span data-stu-id="01f32-130">Hence user do not need to recreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="01f32-131">Tempo de vida de ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="01f32-131">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="01f32-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) é um alocador que cria um proxy para interfaces remotas diferentes.</span><span class="sxs-lookup"><span data-stu-id="01f32-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="01f32-133">Se você usar a API ServiceProxy.Create na criação de proxy, a estrutura criará o singelton ServiceProxyFactory.</span><span class="sxs-lookup"><span data-stu-id="01f32-133">If you use API ServiceProxy.Create for creating proxy, then framework creates the singelton ServiceProxyFactory.</span></span>
<span data-ttu-id="01f32-134">É útil para criá-lo manualmente quando você precisa substituir propriedades [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory).</span><span class="sxs-lookup"><span data-stu-id="01f32-134">It is useful to create one manually when you need to override [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) properties.</span></span>
<span data-ttu-id="01f32-135">Alocador é uma operação cara.</span><span class="sxs-lookup"><span data-stu-id="01f32-135">Factory is an expensive operation.</span></span> <span data-ttu-id="01f32-136">ServiceProxyFactory mantém o cache do cliente de comunicação.</span><span class="sxs-lookup"><span data-stu-id="01f32-136">ServiceProxyFactory maintains cache of communication client.</span></span>
<span data-ttu-id="01f32-137">A prática recomendada é armazenar em cache ServiceProxyFactory por mais tempo possível.</span><span class="sxs-lookup"><span data-stu-id="01f32-137">Best practice is to cache ServiceProxyFactory for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="01f32-138">Tratamento de exceções remotas</span><span class="sxs-lookup"><span data-stu-id="01f32-138">Remoting Exception Handling</span></span>
<span data-ttu-id="01f32-139">Todas as exceções remotas lançadas pela API de serviço são reenviadas para o cliente como AggregateException.</span><span class="sxs-lookup"><span data-stu-id="01f32-139">All the remote exception thrown by service API, are sent back to the client as AggregateException.</span></span> <span data-ttu-id="01f32-140">RemoteExceptions deve ser serializáveis DataContract serializável, ou [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) é lançada para a API do proxy com o erro de serialização.</span><span class="sxs-lookup"><span data-stu-id="01f32-140">RemoteExceptions should be DataContract Serializable otherwise [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) is thrown to the proxy API with the serialization error in it.</span></span>

<span data-ttu-id="01f32-141">ServiceProxy trata todas as exceções de failover da partição de serviço para a qual foi criado.</span><span class="sxs-lookup"><span data-stu-id="01f32-141">ServiceProxy does handle all Failover Exception for the service partition it  is created for.</span></span> <span data-ttu-id="01f32-142">Ele resolverá novamente os pontos de extremidade se houver exceções de failover (exceções não transitórias) e repetirá a chamada com o ponto de extremidade correto.</span><span class="sxs-lookup"><span data-stu-id="01f32-142">It re-resolves the endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries the call with the correct endpoint.</span></span> <span data-ttu-id="01f32-143">O número de tentativas da exceção de failover é indefinido.</span><span class="sxs-lookup"><span data-stu-id="01f32-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="01f32-144">No caso de TransientExceptions, ele repete apenas a chamada.</span><span class="sxs-lookup"><span data-stu-id="01f32-144">In case of TransientExceptions, it only retries the call.</span></span>

<span data-ttu-id="01f32-145">Os parâmetros de repetição padrão são fornecidos por [OperationRetrySettings].</span><span class="sxs-lookup"><span data-stu-id="01f32-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="01f32-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) O usuário pode configurar esses valores passando o objeto OperationRetrySettings para ServiceProxyFactory construtor.</span><span class="sxs-lookup"><span data-stu-id="01f32-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) User can configure these values by passing OperationRetrySettings object to ServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01f32-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="01f32-147">Next steps</span></span>
* [<span data-ttu-id="01f32-148">API Web com OWIN no Reliable Services</span><span class="sxs-lookup"><span data-stu-id="01f32-148">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="01f32-149">Comunicação WCF com o Reliable Services</span><span class="sxs-lookup"><span data-stu-id="01f32-149">WCF communication with Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* [<span data-ttu-id="01f32-150">Securing communication for Reliable Services</span><span class="sxs-lookup"><span data-stu-id="01f32-150">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
