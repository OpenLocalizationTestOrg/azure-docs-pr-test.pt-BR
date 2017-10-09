---
title: "comunicação remota do aaaService no Azure Service Fabric | Microsoft Docs"
description: "Comunicação remota do Service Fabric permite que os clientes e serviços toocommunicate com serviços usando uma chamada de procedimento remoto."
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
ms.openlocfilehash: 1177a5ede91352dc61422f2df7424b0d5645147d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="17b8c-103">Comunicação remota de serviço com o Reliable Services</span><span class="sxs-lookup"><span data-stu-id="17b8c-103">Service remoting with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="17b8c-104">C# em Windows</span><span class="sxs-lookup"><span data-stu-id="17b8c-104">C# on Windows</span></span>](service-fabric-reliable-services-communication-remoting.md)
> * [<span data-ttu-id="17b8c-105">Java no Linux</span><span class="sxs-lookup"><span data-stu-id="17b8c-105">Java on Linux</span></span>](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="17b8c-106">Olá confiável Services framework fornece um tooquickly do mecanismo de comunicação remota e configurar com facilidade a chamada de procedimento remoto de serviços.</span><span class="sxs-lookup"><span data-stu-id="17b8c-106">hello Reliable Services framework provides a remoting mechanism tooquickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="17b8c-107">Configurar a comunicação remota em um serviço</span><span class="sxs-lookup"><span data-stu-id="17b8c-107">Set up remoting on a service</span></span>
<span data-ttu-id="17b8c-108">A configuração da comunicação remota de um serviço é feita em duas etapas simples:</span><span class="sxs-lookup"><span data-stu-id="17b8c-108">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="17b8c-109">Crie uma interface para o serviço tooimplement.</span><span class="sxs-lookup"><span data-stu-id="17b8c-109">Create an interface for your service tooimplement.</span></span> <span data-ttu-id="17b8c-110">Essa interface define os métodos de saudação que estão disponíveis para uma chamada de procedimento remoto em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="17b8c-110">This interface defines hello methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="17b8c-111">métodos de saudação devem ser retorno métodos assíncronos.</span><span class="sxs-lookup"><span data-stu-id="17b8c-111">hello methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="17b8c-112">interface Olá deve implementar `microsoft.serviceFabric.services.remoting.Service` toosignal que Olá serviço tem uma interface de comunicação remota.</span><span class="sxs-lookup"><span data-stu-id="17b8c-112">hello interface must implement `microsoft.serviceFabric.services.remoting.Service` toosignal that hello service has a remoting interface.</span></span>
2. <span data-ttu-id="17b8c-113">Use um ouvinte de comunicação remota em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="17b8c-113">Use a remoting listener in your service.</span></span> <span data-ttu-id="17b8c-114">Esta é uma implementação de `CommunicationListener` que fornece recursos de comunicação remota.</span><span class="sxs-lookup"><span data-stu-id="17b8c-114">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="17b8c-115">`FabricTransportServiceRemotingListener`pode ser usado toocreate um ouvinte de comunicação remota usando o protocolo de transporte de comunicação remota saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="17b8c-115">`FabricTransportServiceRemotingListener` can be used toocreate a remoting listener using hello default remoting transport protocol.</span></span>

<span data-ttu-id="17b8c-116">Por exemplo, hello seguinte serviço sem monitoração de estado expõe um único método tooget "Hello World" passar por uma chamada de procedimento remoto.</span><span class="sxs-lookup"><span data-stu-id="17b8c-116">For example, hello following stateless service exposes a single method tooget "Hello World" over a remote procedure call.</span></span>

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
> <span data-ttu-id="17b8c-117">Olá e argumentos Olá retornam tipos na interface de serviço Olá podem ser qualquer tipo simple, complexo ou personalizado, mas eles devem ser serializáveis.</span><span class="sxs-lookup"><span data-stu-id="17b8c-117">hello arguments and hello return types in hello service interface can be any simple, complex, or custom types, but they must be serializable.</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="17b8c-118">Chamar métodos de serviços remotos</span><span class="sxs-lookup"><span data-stu-id="17b8c-118">Call remote service methods</span></span>
<span data-ttu-id="17b8c-119">Chamar métodos em um serviço usando a pilha de comunicação remota Olá é feito por meio de um serviço de toohello de proxy local por meio de saudação `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` classe.</span><span class="sxs-lookup"><span data-stu-id="17b8c-119">Calling methods on a service by using hello remoting stack is done by using a local proxy toohello service through hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span></span> <span data-ttu-id="17b8c-120">Olá `ServiceProxyBase` método cria um proxy local usando Olá mesma interface que Olá serviço implementa.</span><span class="sxs-lookup"><span data-stu-id="17b8c-120">hello `ServiceProxyBase` method creates a local proxy by using hello same interface that hello service implements.</span></span> <span data-ttu-id="17b8c-121">Com o proxy, você pode simplesmente chamar métodos na interface Olá remotamente.</span><span class="sxs-lookup"><span data-stu-id="17b8c-121">With that proxy, you can simply call methods on hello interface remotely.</span></span>

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

<span data-ttu-id="17b8c-122">estrutura de comunicação remota Olá propaga exceções geradas no cliente do serviço de saudação toohello.</span><span class="sxs-lookup"><span data-stu-id="17b8c-122">hello remoting framework propagates exceptions thrown at hello service toohello client.</span></span> <span data-ttu-id="17b8c-123">Lógica de tratamento de exceção assim no cliente hello usando `ServiceProxyBase` diretamente pode lidar com exceções que Olá lança de serviço.</span><span class="sxs-lookup"><span data-stu-id="17b8c-123">So exception-handling logic at hello client by using `ServiceProxyBase` can directly handle exceptions that hello service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="17b8c-124">Tempo de vida de Proxy do Serviço</span><span class="sxs-lookup"><span data-stu-id="17b8c-124">Service Proxy Lifetime</span></span>
<span data-ttu-id="17b8c-125">A criação do ServiceProxy é uma operação simples, logo, o usuário pode criar quantos precisar.</span><span class="sxs-lookup"><span data-stu-id="17b8c-125">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="17b8c-126">O Proxy do Serviço pode ser reutilizado desde que o usuário precise.</span><span class="sxs-lookup"><span data-stu-id="17b8c-126">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="17b8c-127">Usuário possa reutilizar Olá proxy mesmo em caso de exceção.</span><span class="sxs-lookup"><span data-stu-id="17b8c-127">User can re-use hello same proxy in case of Exception.</span></span> <span data-ttu-id="17b8c-128">Cada ServiceProxy contém mensagens de toosend de cliente usado de comunicação durante transmissão hello.</span><span class="sxs-lookup"><span data-stu-id="17b8c-128">Each ServiceProxy contains communication client used toosend messages over hello wire.</span></span> <span data-ttu-id="17b8c-129">Ao chamar a API, temos toosee verificação interna, se o cliente de comunicação usado é válido.</span><span class="sxs-lookup"><span data-stu-id="17b8c-129">While invoking API, we have internal check toosee if communication client used is valid.</span></span> <span data-ttu-id="17b8c-130">Com base no resultado, podemos criar novamente cliente de comunicação de saudação.</span><span class="sxs-lookup"><span data-stu-id="17b8c-130">Based on that result, we re-create hello communication client.</span></span> <span data-ttu-id="17b8c-131">Portanto, o usuário não precisa serviceproxy toorecreate em caso de exceção.</span><span class="sxs-lookup"><span data-stu-id="17b8c-131">Hence user do not need toorecreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="17b8c-132">Tempo de vida de ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="17b8c-132">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="17b8c-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) é um alocador que cria um proxy para interfaces remotas diferentes.</span><span class="sxs-lookup"><span data-stu-id="17b8c-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="17b8c-134">Se você usar a API `ServiceProxyBase.create` para criar um proxy, o framework cria um `FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="17b8c-134">If you use API `ServiceProxyBase.create` for creating proxy, then framework creates a `FabricServiceProxyFactory`.</span></span>
<span data-ttu-id="17b8c-135">É útil toocreate um manualmente quando precisar toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) propriedades.</span><span class="sxs-lookup"><span data-stu-id="17b8c-135">It is useful toocreate one manually when you need toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) properties.</span></span>
<span data-ttu-id="17b8c-136">Alocador é uma operação cara.</span><span class="sxs-lookup"><span data-stu-id="17b8c-136">Factory is an expensive operation.</span></span> <span data-ttu-id="17b8c-137">`FabricServiceProxyFactory` mantém o cache dos clientes de comunicação.</span><span class="sxs-lookup"><span data-stu-id="17b8c-137">`FabricServiceProxyFactory` maintains cache of communication clients.</span></span>
<span data-ttu-id="17b8c-138">A prática recomendada é toocache `FabricServiceProxyFactory` por tempo possível.</span><span class="sxs-lookup"><span data-stu-id="17b8c-138">Best practice is toocache `FabricServiceProxyFactory` for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="17b8c-139">Tratamento de exceções remotas</span><span class="sxs-lookup"><span data-stu-id="17b8c-139">Remoting Exception Handling</span></span>
<span data-ttu-id="17b8c-140">Todos os Olá remoto exceção pela API de serviço, são enviadas como RuntimeException ou FabricException toohello back cliente.</span><span class="sxs-lookup"><span data-stu-id="17b8c-140">All hello remote exception thrown by service API, are sent back toohello client either as RuntimeException or FabricException.</span></span>

<span data-ttu-id="17b8c-141">ServiceProxy lidar com todas as exceções de Failover para a partição de serviço de hello, ele é criado para.</span><span class="sxs-lookup"><span data-stu-id="17b8c-141">ServiceProxy does handle all Failover Exception for hello service partition it  is created for.</span></span> <span data-ttu-id="17b8c-142">Novamente, ele resolve os pontos de extremidade de saudação se houver Failover Exceptions(Non-Transient Exceptions) e repetições chamada hello com ponto de extremidade correto hello.</span><span class="sxs-lookup"><span data-stu-id="17b8c-142">It re-resolves hello endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries hello call with hello correct endpoint.</span></span> <span data-ttu-id="17b8c-143">O número de tentativas da exceção de failover é indefinido.</span><span class="sxs-lookup"><span data-stu-id="17b8c-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="17b8c-144">No caso de TransientExceptions, ele repete apenas chamada hello.</span><span class="sxs-lookup"><span data-stu-id="17b8c-144">In case of TransientExceptions, it only retries hello call.</span></span>

<span data-ttu-id="17b8c-145">Os parâmetros de repetição padrão são fornecidos por [OperationRetrySettings].</span><span class="sxs-lookup"><span data-stu-id="17b8c-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="17b8c-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) Usuário pode configurar esses valores, passando o construtor de tooServiceProxyFactory OperationRetrySettings objeto.</span><span class="sxs-lookup"><span data-stu-id="17b8c-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) User can configure these values by passing OperationRetrySettings object tooServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17b8c-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="17b8c-147">Next steps</span></span>
* [<span data-ttu-id="17b8c-148">Securing communication for Reliable Services</span><span class="sxs-lookup"><span data-stu-id="17b8c-148">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
