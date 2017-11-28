---
title: "Comunicação remota do serviço no Azure Service Fabric | Microsoft Docs"
description: "A comunicação remota do Service Fabric permite que os clientes e serviços se comuniquem com serviços que usam a chamada de procedimento remoto."
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/30/2017
ms.author: pakunapa
ms.openlocfilehash: dc4a362b5737bb424ca2c196c85f4c51b6ee5e30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="58421-103">Comunicação remota de serviço com o Reliable Services</span><span class="sxs-lookup"><span data-stu-id="58421-103">Service remoting with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="58421-104">C# em Windows</span><span class="sxs-lookup"><span data-stu-id="58421-104">C# on Windows</span></span>](service-fabric-reliable-services-communication-remoting.md)
> * [<span data-ttu-id="58421-105">Java no Linux</span><span class="sxs-lookup"><span data-stu-id="58421-105">Java on Linux</span></span>](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="58421-106">A estrutura do Reliable Services fornece um mecanismo de comunicação remota rápida para configurar de forma fácil e rápida a chamada de procedimento remoto para serviços.</span><span class="sxs-lookup"><span data-stu-id="58421-106">The Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="58421-107">Configurar a comunicação remota em um serviço</span><span class="sxs-lookup"><span data-stu-id="58421-107">Set up remoting on a service</span></span>
<span data-ttu-id="58421-108">A configuração da comunicação remota de um serviço é feita em duas etapas simples:</span><span class="sxs-lookup"><span data-stu-id="58421-108">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="58421-109">Crie uma interface para implementar o serviço.</span><span class="sxs-lookup"><span data-stu-id="58421-109">Create an interface for your service to implement.</span></span> <span data-ttu-id="58421-110">Essa interface define os métodos disponíveis para uma chamada de procedimento remoto no seu serviço.</span><span class="sxs-lookup"><span data-stu-id="58421-110">This interface defines the methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="58421-111">Os métodos devem ser métodos assíncronos que retornam tarefas.</span><span class="sxs-lookup"><span data-stu-id="58421-111">The methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="58421-112">A interface deve implementar `microsoft.serviceFabric.services.remoting.Service` para sinalizar que o serviço tem uma interface de comunicação remota.</span><span class="sxs-lookup"><span data-stu-id="58421-112">The interface must implement `microsoft.serviceFabric.services.remoting.Service` to signal that the service has a remoting interface.</span></span>
2. <span data-ttu-id="58421-113">Use um ouvinte de comunicação remota em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="58421-113">Use a remoting listener in your service.</span></span> <span data-ttu-id="58421-114">Esta é uma implementação de `CommunicationListener` que fornece recursos de comunicação remota.</span><span class="sxs-lookup"><span data-stu-id="58421-114">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="58421-115">`FabricTransportServiceRemotingListener` pode ser usado para criar um ouvinte de comunicação remota usando o protocolo de transporte de comunicação remota padrão.</span><span class="sxs-lookup"><span data-stu-id="58421-115">`FabricTransportServiceRemotingListener` can be used to create a remoting listener using the default remoting transport protocol.</span></span>

<span data-ttu-id="58421-116">Por exemplo, o serviço sem estado a seguir expõe um único método para obter "Hello World" pela chamada de procedimento remoto.</span><span class="sxs-lookup"><span data-stu-id="58421-116">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span></span>

```java
import java.util.ArrayList;
import java.util.concurrent.CompletableFuture;
import java.util.List;
import microsoft.servicefabric.services.communication.runtime.ServiceInstanceListener;
import microsoft.servicefabric.services.remoting.Service;
import microsoft.servicefabric.services.runtime.StatelessService;

public interface MyService extends Service {
    CompletableFuture<String> helloWorldAsync();
}

class MyServiceImpl extends StatelessService implements MyService {
    public MyServiceImpl(StatelessServiceContext context) {
       super(context);
    }

    public CompletableFuture<String> helloWorldAsync() {
        return CompletableFuture.completedFuture("Hello!");
    }

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
        listeners.add(new ServiceInstanceListener((context) -> {
            return new FabricTransportServiceRemotingListener(context,this);
        }));
        return listeners;
    }
}
```

> [!NOTE]
> <span data-ttu-id="58421-117">Os argumentos e os tipos de retorno na interface de serviço podem ser de tipos simples, complexos ou personalizados, mas devem ser serializáveis.</span><span class="sxs-lookup"><span data-stu-id="58421-117">The arguments and the return types in the service interface can be any simple, complex, or custom types, but they must be serializable.</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="58421-118">Chamar métodos de serviços remotos</span><span class="sxs-lookup"><span data-stu-id="58421-118">Call remote service methods</span></span>
<span data-ttu-id="58421-119">A chamada de métodos em um serviço usando a pilha de comunicação remota é feita usando um proxy local para o serviço por meio da classe `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` .</span><span class="sxs-lookup"><span data-stu-id="58421-119">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span></span> <span data-ttu-id="58421-120">O método `ServiceProxyBase` cria um proxy local usando a mesma interface que o serviço implementa.</span><span class="sxs-lookup"><span data-stu-id="58421-120">The `ServiceProxyBase` method creates a local proxy by using the same interface that the service implements.</span></span> <span data-ttu-id="58421-121">Com esse proxy, você pode simplesmente chamar métodos na interface remotamente.</span><span class="sxs-lookup"><span data-stu-id="58421-121">With that proxy, you can simply call methods on the interface remotely.</span></span>

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

<span data-ttu-id="58421-122">A estrutura remota propaga exceções lançadas no serviço para o cliente.</span><span class="sxs-lookup"><span data-stu-id="58421-122">The remoting framework propagates exceptions thrown at the service to the client.</span></span> <span data-ttu-id="58421-123">A lógica de manipulação de exceção no cliente usando `ServiceProxyBase` pode manipular diretamente as exceções que o serviço lança.</span><span class="sxs-lookup"><span data-stu-id="58421-123">So exception-handling logic at the client by using `ServiceProxyBase` can directly handle exceptions that the service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="58421-124">Tempo de vida de Proxy do Serviço</span><span class="sxs-lookup"><span data-stu-id="58421-124">Service Proxy Lifetime</span></span>
<span data-ttu-id="58421-125">A criação do ServiceProxy é uma operação simples, logo, o usuário pode criar quantos precisar.</span><span class="sxs-lookup"><span data-stu-id="58421-125">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="58421-126">O Proxy do Serviço pode ser reutilizado desde que o usuário precise.</span><span class="sxs-lookup"><span data-stu-id="58421-126">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="58421-127">O usuário pode reutilizar o mesmo proxy em caso de exceção.</span><span class="sxs-lookup"><span data-stu-id="58421-127">User can re-use the same proxy in case of Exception.</span></span> <span data-ttu-id="58421-128">Cada ServiceProxy contém um cliente de comunicação usado para enviar mensagens durante a transmissão.</span><span class="sxs-lookup"><span data-stu-id="58421-128">Each ServiceProxy contains communication client used to send messages over the wire.</span></span> <span data-ttu-id="58421-129">Ao invocar a API, temos uma verificação interna para saber se o cliente de comunicação usado é válido.</span><span class="sxs-lookup"><span data-stu-id="58421-129">While invoking API, we have internal check to see if communication client used is valid.</span></span> <span data-ttu-id="58421-130">Com base nesse resultado, recriamos o cliente da comunicação.</span><span class="sxs-lookup"><span data-stu-id="58421-130">Based on that result, we re-create the communication client.</span></span> <span data-ttu-id="58421-131">Portanto, o usuário não precisa recriar serviceproxy em caso de exceção.</span><span class="sxs-lookup"><span data-stu-id="58421-131">Hence user do not need to recreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="58421-132">Tempo de vida de ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="58421-132">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="58421-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) é um alocador que cria um proxy para interfaces remotas diferentes.</span><span class="sxs-lookup"><span data-stu-id="58421-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="58421-134">Se você usar a API `ServiceProxyBase.create` para criar um proxy, o framework cria um `FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="58421-134">If you use API `ServiceProxyBase.create` for creating proxy, then framework creates a `FabricServiceProxyFactory`.</span></span>
<span data-ttu-id="58421-135">É útil para criá-lo manualmente quando você precisa substituir propriedades [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory).</span><span class="sxs-lookup"><span data-stu-id="58421-135">It is useful to create one manually when you need to override [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) properties.</span></span>
<span data-ttu-id="58421-136">Alocador é uma operação cara.</span><span class="sxs-lookup"><span data-stu-id="58421-136">Factory is an expensive operation.</span></span> <span data-ttu-id="58421-137">`FabricServiceProxyFactory` mantém o cache dos clientes de comunicação.</span><span class="sxs-lookup"><span data-stu-id="58421-137">`FabricServiceProxyFactory` maintains cache of communication clients.</span></span>
<span data-ttu-id="58421-138">A prática recomendada é armazenar em cache `FabricServiceProxyFactory` por mais tempo possível.</span><span class="sxs-lookup"><span data-stu-id="58421-138">Best practice is to cache `FabricServiceProxyFactory` for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="58421-139">Tratamento de exceções remotas</span><span class="sxs-lookup"><span data-stu-id="58421-139">Remoting Exception Handling</span></span>
<span data-ttu-id="58421-140">Todas as exceções remotas lançadas pela API de serviço são reenviadas para o cliente como RuntimeException ou FabricException.</span><span class="sxs-lookup"><span data-stu-id="58421-140">All the remote exception thrown by service API, are sent back to the client either as RuntimeException or FabricException.</span></span>

<span data-ttu-id="58421-141">ServiceProxy trata todas as exceções de failover da partição de serviço para a qual foi criado.</span><span class="sxs-lookup"><span data-stu-id="58421-141">ServiceProxy does handle all Failover Exception for the service partition it  is created for.</span></span> <span data-ttu-id="58421-142">Ele resolverá novamente os pontos de extremidade se houver exceções de failover (exceções não transitórias) e repetirá a chamada com o ponto de extremidade correto.</span><span class="sxs-lookup"><span data-stu-id="58421-142">It re-resolves the endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries the call with the correct endpoint.</span></span> <span data-ttu-id="58421-143">O número de tentativas da exceção de failover é indefinido.</span><span class="sxs-lookup"><span data-stu-id="58421-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="58421-144">No caso de TransientExceptions, ele repete apenas a chamada.</span><span class="sxs-lookup"><span data-stu-id="58421-144">In case of TransientExceptions, it only retries the call.</span></span>

<span data-ttu-id="58421-145">Os parâmetros de repetição padrão são fornecidos por [OperationRetrySettings].</span><span class="sxs-lookup"><span data-stu-id="58421-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="58421-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) O usuário pode configurar esses valores passando o objeto OperationRetrySettings para o construtor ServiceProxyFactory.</span><span class="sxs-lookup"><span data-stu-id="58421-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) User can configure these values by passing OperationRetrySettings object to ServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58421-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="58421-147">Next steps</span></span>
* [<span data-ttu-id="58421-148">Securing communication for Reliable Services</span><span class="sxs-lookup"><span data-stu-id="58421-148">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
