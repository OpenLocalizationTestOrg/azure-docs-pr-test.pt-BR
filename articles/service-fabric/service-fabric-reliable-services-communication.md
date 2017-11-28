---
title: "Visão geral da comunicação dos Reliable Services | Microsoft Docs"
description: "Visão geral do modelo de comunicação dos Reliable Services, incluindo a abertura de ouvintes, a resolução de pontos de extremidade e a comunicação entre serviços."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: 36217988-420e-409d-b0a4-e0e875b6eac8
ms.service: service-fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: b418904f50b772c12bfcdbb95beb9312c8b9fb00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-reliable-services-communication-apis"></a><span data-ttu-id="e2ed7-103">Como usar as APIs de comunicação dos Reliable Services</span><span class="sxs-lookup"><span data-stu-id="e2ed7-103">How to use the Reliable Services communication APIs</span></span>
<span data-ttu-id="e2ed7-104">O Service Fabric do Azure como uma plataforma é totalmente independente quanto às comunicações entre serviços.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-104">Azure Service Fabric as a platform is completely agnostic about communication between services.</span></span> <span data-ttu-id="e2ed7-105">Todos os protocolos e pilhas são aceitáveis, de UDP a HTTP.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-105">All protocols and stacks are acceptable, from UDP to HTTP.</span></span> <span data-ttu-id="e2ed7-106">Cabe ao desenvolvedor determinar a forma de comunicação entre os serviços.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-106">It's up to the service developer to choose how services should communicate.</span></span> <span data-ttu-id="e2ed7-107">A estrutura de aplicativo dos Reliable Services fornece algumas pilhas de comunicação internas, bem como APIs que você pode usar para criar componentes de comunicação personalizados.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-107">The Reliable Services application framework provides built-in communication stacks as well as APIs that you can use to build your custom communication components.</span></span>

## <a name="set-up-service-communication"></a><span data-ttu-id="e2ed7-108">Configurar a comunicação de serviço</span><span class="sxs-lookup"><span data-stu-id="e2ed7-108">Set up service communication</span></span>
<span data-ttu-id="e2ed7-109">A API do Reliable Services usa uma interface simples para comunicação de serviço.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-109">The Reliable Services API uses a simple interface for service communication.</span></span> <span data-ttu-id="e2ed7-110">Para abrir um ponto de extremidade para o serviço, basta implementar esta interface:</span><span class="sxs-lookup"><span data-stu-id="e2ed7-110">To open an endpoint for your service, simply implement this interface:</span></span>

```csharp

public interface ICommunicationListener
{
    Task<string> OpenAsync(CancellationToken cancellationToken);

    Task CloseAsync(CancellationToken cancellationToken);

    void Abort();
}

```

```java
public interface CommunicationListener {
    CompletableFuture<String> openAsync(CancellationToken cancellationToken);

    CompletableFuture<?> closeAsync(CancellationToken cancellationToken);

    void abort();
}
```

<span data-ttu-id="e2ed7-111">Você pode adicionar a implementação do ouvinte de comunicação, retornando-a em uma substituição do método de classe com base no serviço.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-111">You can then add your communication listener implementation by returning it in a service-based class method override.</span></span>

<span data-ttu-id="e2ed7-112">Para serviços sem estado:</span><span class="sxs-lookup"><span data-stu-id="e2ed7-112">For stateless services:</span></span>

```csharp
class MyStatelessService : StatelessService
{
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        ...
    }
    ...
}
```
```java
public class MyStatelessService extends StatelessService {

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ...
    }
    ...
}
```

<span data-ttu-id="e2ed7-113">Para serviços com estado:</span><span class="sxs-lookup"><span data-stu-id="e2ed7-113">For stateful services:</span></span>

> [!NOTE]
> <span data-ttu-id="e2ed7-114">Ainda não há suporte para Reliable Services com monitoração de estado em Java.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-114">Stateful reliable services are not supported in Java yet.</span></span>
>
>

```csharp
class MyStatefulService : StatefulService
{
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        ...
    }
    ...
}
```

<span data-ttu-id="e2ed7-115">Em ambos os casos, você deve retornar uma coleção de ouvintes.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-115">In both cases, you return a collection of listeners.</span></span> <span data-ttu-id="e2ed7-116">Isso permite que o serviço ouça vários pontos de extremidade, potencialmente usando protocolos diferentes ao usar vários ouvintes.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-116">This allows your service to listen on multiple endpoints, potentially using different protocols, by using multiple listeners.</span></span> <span data-ttu-id="e2ed7-117">Por exemplo, você pode ter um ouvinte HTTP e um ouvinte WebSocket separado.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-117">For example, you may have an HTTP listener and a separate WebSocket listener.</span></span> <span data-ttu-id="e2ed7-118">Cada ouvinte recebe um nome e a coleção resultante dos pares *nome : endereço* é representada como um objeto JSON quando um cliente solicita os endereços de escuta para uma instância ou uma partição de serviço.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-118">Each listener gets a name, and the resulting collection of *name : address* pairs are represented as a JSON object when a client requests the listening addresses for a service instance or a partition.</span></span>

<span data-ttu-id="e2ed7-119">Em um serviço sem estado, a substituição retorna uma coleção de ServiceInstanceListeners.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-119">In a stateless service, the override returns a collection of ServiceInstanceListeners.</span></span> <span data-ttu-id="e2ed7-120">Um `ServiceInstanceListener` contém uma função para criar um `ICommunicationListener(C#) / CommunicationListener(Java)` e concede a ele um nome.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-120">A `ServiceInstanceListener` contains a function to create an `ICommunicationListener(C#) / CommunicationListener(Java)` and gives it a name.</span></span> <span data-ttu-id="e2ed7-121">Para os serviços com monitoração de estado, a substituição retorna uma coleção de ServiceReplicaListeners.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-121">For stateful services, the override returns a collection of ServiceReplicaListeners.</span></span> <span data-ttu-id="e2ed7-122">Isso é um pouco diferente do equivalente sem estado, pois um `ServiceReplicaListener` tem uma opção para abrir um `ICommunicationListener` em réplicas secundárias.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-122">This is slightly different from its stateless counterpart, because a `ServiceReplicaListener` has an option to open an `ICommunicationListener` on secondary replicas.</span></span> <span data-ttu-id="e2ed7-123">Você pode usar vários ouvintes de comunicação em um serviço, além de especificar aqueles que aceitem solicitações em réplicas secundárias e os que escutam apenas em réplicas primárias.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-123">Not only can you use multiple communication listeners in a service, but you can also specify which listeners accept requests on secondary replicas and which ones listen only on primary replicas.</span></span>

<span data-ttu-id="e2ed7-124">Por exemplo, você pode ter um ServiceRemotingListener que faz chamadas RPC apenas em réplicas primárias e um segundo ouvinte personalizado que faz solicitações de leitura em réplicas secundárias sobre HTTP:</span><span class="sxs-lookup"><span data-stu-id="e2ed7-124">For example, you can have a ServiceRemotingListener that takes RPC calls only on primary replicas, and a second, custom listener that takes read requests on secondary replicas over HTTP:</span></span>

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[]
    {
        new ServiceReplicaListener(context =>
            new MyCustomHttpListener(context),
            "HTTPReadonlyEndpoint",
            true),

        new ServiceReplicaListener(context =>
            this.CreateServiceRemotingListener(context),
            "rpcPrimaryEndpoint",
            false)
    };
}
```

> [!NOTE]
> <span data-ttu-id="e2ed7-125">Ao se criar vários ouvintes para um serviço, cada ouvinte **deve** receber um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-125">When creating multiple listeners for a service, each listener **must** be given a unique name.</span></span>
>
>

<span data-ttu-id="e2ed7-126">Por fim, você pode descrever os pontos de extremidade necessários para o serviço no [manifesto do serviço](service-fabric-application-model.md) , na seção sobre pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-126">Finally, describe the endpoints that are required for the service in the [service manifest](service-fabric-application-model.md) under the section on endpoints.</span></span>

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

<span data-ttu-id="e2ed7-127">O ouvinte de comunicação pode acessar os recursos do ponto de extremidade alocados para ele no `CodePackageActivationContext`, no `ServiceContext`.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-127">The communication listener can access the endpoint resources allocated to it from the `CodePackageActivationContext` in the `ServiceContext`.</span></span> <span data-ttu-id="e2ed7-128">O ouvinte pode então começar a escutar solicitações quando é aberto.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-128">The listener can then start listening for requests when it is opened.</span></span>

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> <span data-ttu-id="e2ed7-129">Os recursos do ponto de extremidade são comuns a todo o pacote de serviço e são alocados pelo Service Fabric quando o pacote de serviço é ativado.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-129">Endpoint resources are common to the entire service package, and they are allocated by Service Fabric when the service package is activated.</span></span> <span data-ttu-id="e2ed7-130">Várias réplicas de serviço hospedadas no mesmo ServiceHost podem compartilhar a mesma porta.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-130">Multiple service replicas hosted in the same ServiceHost may share the same port.</span></span> <span data-ttu-id="e2ed7-131">Isso significa que o ouvinte de comunicação deve oferecer suporte ao compartilhamento de porta.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-131">This means that the communication listener should support port sharing.</span></span> <span data-ttu-id="e2ed7-132">A maneira recomendada de fazer isso é que o ouvinte de comunicação use a ID da partição e a ID de réplica/instância ao gerar o endereço de escuta.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-132">The recommended way of doing this is for the communication listener to use the partition ID and replica/instance ID when it generates the listen address.</span></span>
>
>

### <a name="service-address-registration"></a><span data-ttu-id="e2ed7-133">Registro de endereço do serviço</span><span class="sxs-lookup"><span data-stu-id="e2ed7-133">Service address registration</span></span>
<span data-ttu-id="e2ed7-134">Um serviço do sistema chamado de *Serviço de Nomenclatura* é executado em clusters do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-134">A system service called the *Naming Service* runs on Service Fabric clusters.</span></span> <span data-ttu-id="e2ed7-135">O Serviço de Nomenclatura é um registrador para os serviços e seus endereços que cada instância ou réplica do serviço está escutando.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-135">The Naming Service is a registrar for services and their addresses that each instance or replica of the service is listening on.</span></span> <span data-ttu-id="e2ed7-136">Quando o método `OpenAsync(C#) / openAsync(Java)` de um `ICommunicationListener(C#) / CommunicationListener(Java)` é concluído, seu valor retornado é registrado no Serviço de Nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-136">When the `OpenAsync(C#) / openAsync(Java)` method of an `ICommunicationListener(C#) / CommunicationListener(Java)` completes, its return value gets registered in the Naming Service.</span></span> <span data-ttu-id="e2ed7-137">Esse valor retornado que é publicado no Serviço de Nomenclatura é uma cadeia de caracteres cujo valor pode ser absolutamente qualquer coisa.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-137">This return value that gets published in the Naming Service is a string whose value can be anything at all.</span></span> <span data-ttu-id="e2ed7-138">Esse valor de cadeia de caracteres é o que os clientes verão quando perguntarem o endereço do Serviço de Nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-138">This string value is what clients see when they ask for an address for the service from the Naming Service.</span></span>

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.CodePackageActivationContext.GetEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.Port;

    this.listeningAddress = string.Format(
                CultureInfo.InvariantCulture,
                "http://+:{0}/",
                port);

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

    // the string returned here will be published in the Naming Service.
    return Task.FromResult(this.publishAddress);
}
```
```java
public CompletableFuture<String> openAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.getCodePackageActivationContext.getEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.getPort();

    this.publishAddress = String.format("http://%s:%d/", FabricRuntime.getNodeContext().getIpAddressOrFQDN(), port);

    this.webApp = new WebApp(port);
    this.webApp.start();

    /* the string returned here will be published in the Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

<span data-ttu-id="e2ed7-139">O Service Fabric fornece uma API que permite aos clientes e outros serviços perguntarem esse endereço pelo nome do serviço.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-139">Service Fabric provides APIs that allow clients and other services to then ask for this address by service name.</span></span> <span data-ttu-id="e2ed7-140">Isso é importante porque o endereço do serviço não é estático.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-140">This is important because the service address is not static.</span></span> <span data-ttu-id="e2ed7-141">Os serviços são movimentados no cluster para fins de disponibilidade e balanceamento de recursos.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-141">Services are moved around in the cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="e2ed7-142">Esse é o mecanismo que permite aos clientes resolver o endereço de escuta de um serviço.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-142">This is the mechanism that allow clients to resolve the listening address for a service.</span></span>

> [!NOTE]
> <span data-ttu-id="e2ed7-143">Para obter uma explicação completa de como escrever um ouvinte de comunicação, consulte [Serviços de API Web do Service Fabric com auto-hospedagem OWIN](service-fabric-reliable-services-communication-webapi.md) para C#, enquanto para Java você pode escrever sua própria implementação do servidor HTTP; consulte o exemplo de aplicativo EchoServer em https://github.com/Azure-Samples/service-fabric-java-getting-started.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-143">For a complete walk-through of how to write a communication listener, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) for C#, whereas for Java you can write your own HTTP server implementation, see EchoServer application example at https://github.com/Azure-Samples/service-fabric-java-getting-started.</span></span>
>
>

## <a name="communicating-with-a-service"></a><span data-ttu-id="e2ed7-144">Comunicando-se com um serviço</span><span class="sxs-lookup"><span data-stu-id="e2ed7-144">Communicating with a service</span></span>
<span data-ttu-id="e2ed7-145">A API dos Reliable Services fornece as bibliotecas a seguir para escrever clientes que se comunicam com serviços.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-145">The Reliable Services API provides the following libraries to write clients that communicate with services.</span></span>

### <a name="service-endpoint-resolution"></a><span data-ttu-id="e2ed7-146">Resolução de ponto de extremidade de serviço</span><span class="sxs-lookup"><span data-stu-id="e2ed7-146">Service endpoint resolution</span></span>
<span data-ttu-id="e2ed7-147">A primeira etapa para a comunicação com um serviço é resolver um endereço do ponto de extremidade da partição ou instância do serviço com o qual você deseja falar.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-147">The first step to communication with a service is to resolve an endpoint address of the partition or instance of the service you want to talk to.</span></span> <span data-ttu-id="e2ed7-148">A classe de utilitário `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` é um primitivo básico que ajuda os clientes a determinar o ponto de extremidade de um serviço no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-148">The `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` utility class is a basic primitive that helps clients determine the endpoint of a service at runtime.</span></span> <span data-ttu-id="e2ed7-149">Na terminologia do Service Fabric, o processo de determinar o ponto de extremidade de um serviço é conhecido como *resolução do ponto de extremidade de serviço*.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-149">In Service Fabric terminology, the process of determining the endpoint of a service is referred to as the *service endpoint resolution*.</span></span>

<span data-ttu-id="e2ed7-150">Para se conectar aos serviços em um cluster, ServicePartitionResolver pode ser criado usando as configurações padrão.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-150">To connect to services within a cluster, ServicePartitionResolver can be created using default settings.</span></span> <span data-ttu-id="e2ed7-151">Este é o uso recomendado na maioria das situações:</span><span class="sxs-lookup"><span data-stu-id="e2ed7-151">This is the recommended usage for most situations:</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

<span data-ttu-id="e2ed7-152">Para se conectar aos serviços em um cluster diferente, um ServicePartitionResolver pode ser criado com um conjunto de pontos de extremidade de gateway do cluster.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-152">To connect to services in a different cluster, a ServicePartitionResolver can be created with a set of cluster gateway endpoints.</span></span> <span data-ttu-id="e2ed7-153">Observe que os pontos de extremidade de gateway são apenas pontos de extremidade diferentes para se conectar ao mesmo cluster.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-153">Note that gateway endpoints are just different endpoints for connecting to the same cluster.</span></span> <span data-ttu-id="e2ed7-154">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e2ed7-154">For example:</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

<span data-ttu-id="e2ed7-155">Como alternativa, um `ServicePartitionResolver` pode receber uma função para criar um `FabricClient` para uso interno:</span><span class="sxs-lookup"><span data-stu-id="e2ed7-155">Alternatively, `ServicePartitionResolver` can be given a function for creating a `FabricClient` to use internally:</span></span>

```csharp
public delegate FabricClient CreateFabricClientDelegate();
```
```java
public FabricServicePartitionResolver(CreateFabricClient createFabricClient) {
...
}

public interface CreateFabricClient {
    public FabricClient getFabricClient();
}
```

<span data-ttu-id="e2ed7-156">`FabricClient` é o objeto usado para se comunicar com o cluster do Service Fabric em várias operações de gerenciamento no cluster.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-156">`FabricClient` is the object that is used to communicate with the Service Fabric cluster for various management operations on the cluster.</span></span> <span data-ttu-id="e2ed7-157">Isso é útil quando você quiser mais controle sobre como um resolvedor de partição de serviço interage com o cluster.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-157">This is useful when you want more control over how a service partition resolver interacts with your cluster.</span></span> <span data-ttu-id="e2ed7-158">O `FabricClient` realiza armazenamento em cache internamente e é geralmente caro de criar, portanto, é importante reutilizar instâncias do `FabricClient` tanto quanto possível.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-158">`FabricClient` performs caching internally and is generally expensive to create, so it is important to reuse `FabricClient` instances as much as possible.</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

<span data-ttu-id="e2ed7-159">Um método de resolução é então usado para recuperar o endereço de um serviço ou uma partição de serviço para serviços particionados.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-159">A resolve method is then used to retrieve the address of a service or a service partition for partitioned services.</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();

ResolvedServicePartition partition =
    await resolver.ResolveAsync(new Uri("fabric:/MyApp/MyService"), new ServicePartitionKey(), cancellationToken);
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();

CompletableFuture<ResolvedServicePartition> partition =
    resolver.resolveAsync(new URI("fabric:/MyApp/MyService"), new ServicePartitionKey());
```

<span data-ttu-id="e2ed7-160">Um endereço de serviço pode ser resolvido facilmente usando um ServicePartitionResolver, porém é necessário mais trabalho para garantir que o endereço resolvido possa ser usado corretamente.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-160">A service address can be resolved easily using a ServicePartitionResolver, but more work is required to ensure the resolved address can be used correctly.</span></span> <span data-ttu-id="e2ed7-161">O cliente precisa detectar se a tentativa de conexão falhou devido a um erro transitório e pode ser repetida (por exemplo, o serviço foi movido ou está temporariamente indisponível) ou a um erro permanente (por exemplo, o serviço foi excluído ou o recurso solicitado não existe mais).</span><span class="sxs-lookup"><span data-stu-id="e2ed7-161">Your client needs to detect whether the connection attempt failed because of a transient error and can be retried (e.g., service moved or is temporarily unavailable), or a permanent error (e.g., service was deleted or the requested resource no longer exists).</span></span> <span data-ttu-id="e2ed7-162">Réplicas ou instâncias de serviço podem se mover de nó para nó a qualquer momento por várias razões.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-162">Service instances or replicas can move around from node to node at any time for multiple reasons.</span></span> <span data-ttu-id="e2ed7-163">O endereço de serviço resolvido por meio de ServicePartitionResolver pode estar obsoleto no momento em seu código de cliente tentar se conectar.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-163">The service address resolved through ServicePartitionResolver may be stale by the time your client code attempts to connect.</span></span> <span data-ttu-id="e2ed7-164">Nesse caso, o cliente precisa resolver o endereço novamente.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-164">In that case again the client needs to re-resolve the address.</span></span> <span data-ttu-id="e2ed7-165">Fornecer o `ResolvedServicePartition` anterior indica que o resolvedor deve tentar novamente em vez de simplesmente recuperar um endereço armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-165">Providing the previous `ResolvedServicePartition` indicates that the resolver needs to try again rather than simply retrieve a cached address.</span></span>

<span data-ttu-id="e2ed7-166">Normalmente o código do cliente não precisa trabalhar diretamente com o ServicePartitionResolver.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-166">Typically, the client code need not work with the ServicePartitionResolver directly.</span></span> <span data-ttu-id="e2ed7-167">Ele é criado e passado fábricas clientes de comunicação na API dos Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-167">It is created and passed on to communication client factories in the Reliable Services API.</span></span> <span data-ttu-id="e2ed7-168">As fábricas usam o resolvedor internamente para gerar um objeto cliente que pode ser usado para se comunicar com os serviços.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-168">The factories use the resolver internally to generate a client object that can be used to communicate with services.</span></span>

### <a name="communication-clients-and-factories"></a><span data-ttu-id="e2ed7-169">Fábricas e clientes de comunicação</span><span class="sxs-lookup"><span data-stu-id="e2ed7-169">Communication clients and factories</span></span>
<span data-ttu-id="e2ed7-170">A biblioteca de fábrica de comunicação implementa um padrão típico de repetição de manipulação de falhas que facilita a repetição de novas tentativas de conexão para pontos de extremidade de serviço resolvidos.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-170">The communication factory library implements a typical fault-handling retry pattern that makes retrying connections to resolved service endpoints easier.</span></span> <span data-ttu-id="e2ed7-171">A biblioteca de fábrica fornece o mecanismo de repetição enquanto você fornece os manipuladores de erro.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-171">The factory library provides the retry mechanism while you provide the error handlers.</span></span>

<span data-ttu-id="e2ed7-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` define a interface base implementada por uma fábrica de cliente de comunicação que produz clientes que podem se comunicar com um serviço do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` defines the base interface implemented by a communication client factory that produces clients that can talk to a Service Fabric service.</span></span> <span data-ttu-id="e2ed7-173">A implementação de CommunicationClientFactory dependerá da pilha de comunicação usada pelo serviço do Service Fabric em que o cliente quer se comunicar.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-173">The implementation of the CommunicationClientFactory depends on the communication stack used by the Service Fabric service where the client wants to communicate.</span></span> <span data-ttu-id="e2ed7-174">A API dos Reliable Services fornece um `CommunicationClientFactoryBase<TCommunicationClient>`.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-174">The Reliable Services API provides a `CommunicationClientFactoryBase<TCommunicationClient>`.</span></span> <span data-ttu-id="e2ed7-175">Ele fornece uma implementação básica da interface do CommunicationClientFactory e executa as tarefas comuns a todas as pilhas de comunicação.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-175">This provides a base implementation of the CommunicationClientFactory interface and performs tasks that are common to all the communication stacks.</span></span> <span data-ttu-id="e2ed7-176">(Essas tarefas incluem o uso de um ServicePartitionResolver para determinar o ponto de extremidade de serviço).</span><span class="sxs-lookup"><span data-stu-id="e2ed7-176">(These tasks include using a ServicePartitionResolver to determine the service endpoint).</span></span> <span data-ttu-id="e2ed7-177">Os clientes geralmente implementam a classe abstrata CommunicationClientFactoryBase para tratar da lógica específica da pilha de comunicação.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-177">Clients usually implement the abstract CommunicationClientFactoryBase class to handle logic that is specific to the communication stack.</span></span>

<span data-ttu-id="e2ed7-178">O cliente de comunicação apenas recebe um endereço e o utiliza para se conectar a um serviço.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-178">The communication client just receives an address and uses it to connect to a service.</span></span> <span data-ttu-id="e2ed7-179">O cliente pode usar qualquer protocolo que desejar.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-179">The client can use whatever protocol it wants.</span></span>

```csharp
class MyCommunicationClient : ICommunicationClient
{
    public ResolvedServiceEndpoint Endpoint { get; set; }

    public string ListenerName { get; set; }

    public ResolvedServicePartition ResolvedServicePartition { get; set; }
}
```
```java
public class MyCommunicationClient implements CommunicationClient {

    private ResolvedServicePartition resolvedServicePartition;
    private String listenerName;
    private ResolvedServiceEndpoint endPoint;

    /*
     * Getters and Setters
     */
}
```

<span data-ttu-id="e2ed7-180">A fábrica do cliente é responsável principalmente pela criação de clientes de comunicação.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-180">The client factory is primarily responsible for creating communication clients.</span></span> <span data-ttu-id="e2ed7-181">Para clientes que não mantém uma conexão persistente, tal como um cliente HTTP, a fábrica só precisa criar e retornar o cliente.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-181">For clients that don't maintain a persistent connection, such as an HTTP client, the factory only needs to create and return the client.</span></span> <span data-ttu-id="e2ed7-182">Outros protocolos que mantêm uma conexão persistente, tais como alguns protocolos binários, também devem ser validados pela fábrica para determinar se a conexão precisa ou não ser criada novamente.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-182">Other protocols that maintain a persistent connection, such as some binary protocols, should also be validated by the factory to determine whether the connection needs to be re-created.</span></span>  

```csharp
public class MyCommunicationClientFactory : CommunicationClientFactoryBase<MyCommunicationClient>
{
    protected override void AbortClient(MyCommunicationClient client)
    {
    }

    protected override Task<MyCommunicationClient> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
    {
    }

    protected override bool ValidateClient(MyCommunicationClient clientChannel)
    {
    }

    protected override bool ValidateClient(string endpoint, MyCommunicationClient client)
    {
    }
}
```
```java
public class MyCommunicationClientFactory extends CommunicationClientFactoryBase<MyCommunicationClient> {

    @Override
    protected boolean validateClient(MyCommunicationClient clientChannel) {
    }

    @Override
    protected boolean validateClient(String endpoint, MyCommunicationClient client) {
    }

    @Override
    protected CompletableFuture<MyCommunicationClient> createClientAsync(String endpoint) {
    }

    @Override
    protected void abortClient(MyCommunicationClient client) {
    }
}
```

<span data-ttu-id="e2ed7-183">Por fim, um manipulador de exceção é responsável por determinar a ação a ser executada quando uma exceção ocorre.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-183">Finally, an exception handler is responsible for determining what action to take when an exception occurs.</span></span> <span data-ttu-id="e2ed7-184">Exceções são categorizadas como **repetíveis** e **não repetíveis**.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-184">Exceptions are categorized into **retryable** and **non retryable**.</span></span>

* <span data-ttu-id="e2ed7-185">Exceções **não repetíveis** simplesmente são retornadas para o chamador.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-185">**Non retryable** exceptions simply get rethrown back to the caller.</span></span>
* <span data-ttu-id="e2ed7-186">Exceções **repetíveis** são categorizadas novamente em **transitórias** e **não transitórias**.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-186">**retryable** exceptions are further categorized into **transient** and **non-transient**.</span></span>
  * <span data-ttu-id="e2ed7-187">**transitórias** são aquelas que podem ser recuperadas simplesmente sem resolver novamente o endereço do ponto de extremidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-187">**Transient** exceptions are those that can simply be retried without re-resolving the service endpoint address.</span></span> <span data-ttu-id="e2ed7-188">Elas incluem problemas de rede transitórios ou respostas de erros de serviço diferentes daqueles que indicam que o endereço do ponto de extremidade de serviço não existe.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-188">These will include transient network problems or service error responses other than those that indicate the service endpoint address does not exist.</span></span>
  * <span data-ttu-id="e2ed7-189">**Non-transient** são aquelas que exigem que o endereço do ponto de extremidade de serviço seja resolvido novamente.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-189">**Non-transient** exceptions are those that require the service endpoint address to be re-resolved.</span></span> <span data-ttu-id="e2ed7-190">Elas incluem exceções que indicam que não foi possível alcançar o ponto de extremidade de serviço, indicando que o serviço foi movido para outro nó.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-190">These include exceptions that indicate the service endpoint could not be reached, indicating the service has moved to a different node.</span></span>

<span data-ttu-id="e2ed7-191">O `TryHandleException` toma uma decisão sobre uma determinada exceção.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-191">The `TryHandleException` makes a decision about a given exception.</span></span> <span data-ttu-id="e2ed7-192">Se ele **não souber** quais decisões devem ser tomadas sobre uma exceção, ele deverá retornar **false**.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-192">If it **does not know** what decisions to make about an exception, it should return **false**.</span></span> <span data-ttu-id="e2ed7-193">Se ele **souber** qual decisão tomar, deverá definir o resultado corretamente e retornar **true**.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-193">If it **does know** what decision to make, it should set the result accordingly and return **true**.</span></span>

```csharp
class MyExceptionHandler : IExceptionHandler
{
    public bool TryHandleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings, out ExceptionHandlingResult result)
    {
        // if exceptionInformation.Exception is known and is transient (can be retried without re-resolving)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, true, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;


        // if exceptionInformation.Exception is known and is not transient (indicates a new service endpoint address must be resolved)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, false, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;

        // if exceptionInformation.Exception is unknown (let the next IExceptionHandler attempt to handle it)
        result = null;
        return false;
    }
}
```
```java
public class MyExceptionHandler implements ExceptionHandler {

    @Override
    public ExceptionHandlingResult handleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings) {        

        /* if exceptionInformation.getException() is known and is transient (can be retried without re-resolving)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), true, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;


        /* if exceptionInformation.getException() is known and is not transient (indicates a new service endpoint address must be resolved)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), false, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;

        /* if exceptionInformation.getException() is unknown (let the next ExceptionHandler attempt to handle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a><span data-ttu-id="e2ed7-194">Juntando as peças</span><span class="sxs-lookup"><span data-stu-id="e2ed7-194">Putting it all together</span></span>
<span data-ttu-id="e2ed7-195">Com um `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` e `IExceptionHandler(C#) / ExceptionHandler(Java)` criados em torno de um protocolo de comunicação, um `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` reúne tudo isso e fornece o loop de manipulação de falhas e de resolução de endereço da partição de serviço em torno desses componentes.</span><span class="sxs-lookup"><span data-stu-id="e2ed7-195">With an `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, and `IExceptionHandler(C#) / ExceptionHandler(Java)` built around a communication protocol, a `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` wraps it all together and provides the fault-handling and service partition address resolution loop around these components.</span></span>

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with the service using the client.
   },
   CancellationToken.None);

```
```java
private MyCommunicationClientFactory myCommunicationClientFactory;
private URI myServiceUri;

FabricServicePartitionClient myServicePartitionClient = new FabricServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

CompletableFuture<?> result = myServicePartitionClient.invokeWithRetryAsync(client -> {
      /* Communicate with the service using the client.
       */
   });

```

## <a name="next-steps"></a><span data-ttu-id="e2ed7-196">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e2ed7-196">Next steps</span></span>
* <span data-ttu-id="e2ed7-197">Confira um exemplo de comunicação HTTP entre serviços em um [projeto de exemplo C# no GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) ou [Projeto de exemplo Java no GitHub](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span><span class="sxs-lookup"><span data-stu-id="e2ed7-197">See an example of HTTP communication between services in a [C# sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) or [Java sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span></span>
* [<span data-ttu-id="e2ed7-198">Comunicação remota de serviço com os Reliable Services</span><span class="sxs-lookup"><span data-stu-id="e2ed7-198">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="e2ed7-199">API Web que usa o OWIN nos Reliable Services</span><span class="sxs-lookup"><span data-stu-id="e2ed7-199">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="e2ed7-200">Comunicação WCF usando os Reliable Services</span><span class="sxs-lookup"><span data-stu-id="e2ed7-200">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
