---
title: "Visão geral de comunicação de serviços aaaReliable | Microsoft Docs"
description: "Visão geral de comunicação de serviços confiáveis Olá modelo, incluindo ouvintes de abertura em serviços, resolvendo os pontos de extremidade e comunicação entre serviços."
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
ms.openlocfilehash: 93a7017b50df0822969daa5ad78302c73e8ba641
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-reliable-services-communication-apis"></a><span data-ttu-id="9c26e-103">Como toouse Olá APIs de comunicação de serviços confiáveis</span><span class="sxs-lookup"><span data-stu-id="9c26e-103">How toouse hello Reliable Services communication APIs</span></span>
<span data-ttu-id="9c26e-104">O Service Fabric do Azure como uma plataforma é totalmente independente quanto às comunicações entre serviços.</span><span class="sxs-lookup"><span data-stu-id="9c26e-104">Azure Service Fabric as a platform is completely agnostic about communication between services.</span></span> <span data-ttu-id="9c26e-105">Todos os protocolos e pilhas são aceitáveis, de tooHTTP UDP.</span><span class="sxs-lookup"><span data-stu-id="9c26e-105">All protocols and stacks are acceptable, from UDP tooHTTP.</span></span> <span data-ttu-id="9c26e-106">É o toohello toochoose de desenvolvedor de serviço como serviços devem se comunicar.</span><span class="sxs-lookup"><span data-stu-id="9c26e-106">It's up toohello service developer toochoose how services should communicate.</span></span> <span data-ttu-id="9c26e-107">estrutura de aplicativo de serviços confiáveis Olá fornece comunicação interna de pilhas, bem como as APIs que você pode usar toobuild os componentes personalizados de comunicação.</span><span class="sxs-lookup"><span data-stu-id="9c26e-107">hello Reliable Services application framework provides built-in communication stacks as well as APIs that you can use toobuild your custom communication components.</span></span>

## <a name="set-up-service-communication"></a><span data-ttu-id="9c26e-108">Configurar a comunicação de serviço</span><span class="sxs-lookup"><span data-stu-id="9c26e-108">Set up service communication</span></span>
<span data-ttu-id="9c26e-109">Olá confiável API de serviços usa uma interface simples para comunicação de serviço.</span><span class="sxs-lookup"><span data-stu-id="9c26e-109">hello Reliable Services API uses a simple interface for service communication.</span></span> <span data-ttu-id="9c26e-110">tooopen um ponto de extremidade para seu serviço, basta implementar essa interface:</span><span class="sxs-lookup"><span data-stu-id="9c26e-110">tooopen an endpoint for your service, simply implement this interface:</span></span>

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

<span data-ttu-id="9c26e-111">Você pode adicionar a implementação do ouvinte de comunicação, retornando-a em uma substituição do método de classe com base no serviço.</span><span class="sxs-lookup"><span data-stu-id="9c26e-111">You can then add your communication listener implementation by returning it in a service-based class method override.</span></span>

<span data-ttu-id="9c26e-112">Para serviços sem estado:</span><span class="sxs-lookup"><span data-stu-id="9c26e-112">For stateless services:</span></span>

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

<span data-ttu-id="9c26e-113">Para serviços com estado:</span><span class="sxs-lookup"><span data-stu-id="9c26e-113">For stateful services:</span></span>

> [!NOTE]
> <span data-ttu-id="9c26e-114">Ainda não há suporte para Reliable Services com monitoração de estado em Java.</span><span class="sxs-lookup"><span data-stu-id="9c26e-114">Stateful reliable services are not supported in Java yet.</span></span>
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

<span data-ttu-id="9c26e-115">Em ambos os casos, você deve retornar uma coleção de ouvintes.</span><span class="sxs-lookup"><span data-stu-id="9c26e-115">In both cases, you return a collection of listeners.</span></span> <span data-ttu-id="9c26e-116">Isso permite que seu serviço toolisten em vários pontos de extremidade, potencialmente usando protocolos diferentes, usando vários ouvintes.</span><span class="sxs-lookup"><span data-stu-id="9c26e-116">This allows your service toolisten on multiple endpoints, potentially using different protocols, by using multiple listeners.</span></span> <span data-ttu-id="9c26e-117">Por exemplo, você pode ter um ouvinte HTTP e um ouvinte WebSocket separado.</span><span class="sxs-lookup"><span data-stu-id="9c26e-117">For example, you may have an HTTP listener and a separate WebSocket listener.</span></span> <span data-ttu-id="9c26e-118">Cada ouvinte obtém um nome e a coleção resultante de saudação do *nome: endereço* pares são representados como um objeto JSON quando um cliente solicita endereços de escuta Olá para uma instância de serviço ou uma partição.</span><span class="sxs-lookup"><span data-stu-id="9c26e-118">Each listener gets a name, and hello resulting collection of *name : address* pairs are represented as a JSON object when a client requests hello listening addresses for a service instance or a partition.</span></span>

<span data-ttu-id="9c26e-119">Em um serviço sem monitoração de estado, a substituição de saudação retorna uma coleção de ServiceInstanceListeners.</span><span class="sxs-lookup"><span data-stu-id="9c26e-119">In a stateless service, hello override returns a collection of ServiceInstanceListeners.</span></span> <span data-ttu-id="9c26e-120">Um `ServiceInstanceListener` contém uma função toocreate uma `ICommunicationListener(C#) / CommunicationListener(Java)` e concede a ele um nome.</span><span class="sxs-lookup"><span data-stu-id="9c26e-120">A `ServiceInstanceListener` contains a function toocreate an `ICommunicationListener(C#) / CommunicationListener(Java)` and gives it a name.</span></span> <span data-ttu-id="9c26e-121">Para os serviços com monitoração de estado, a substituição de saudação retorna uma coleção de ServiceReplicaListeners.</span><span class="sxs-lookup"><span data-stu-id="9c26e-121">For stateful services, hello override returns a collection of ServiceReplicaListeners.</span></span> <span data-ttu-id="9c26e-122">Isso é um pouco diferente de sua contraparte sem monitoração de estado, pois um `ServiceReplicaListener` tem uma opção tooopen um `ICommunicationListener` em réplicas secundárias.</span><span class="sxs-lookup"><span data-stu-id="9c26e-122">This is slightly different from its stateless counterpart, because a `ServiceReplicaListener` has an option tooopen an `ICommunicationListener` on secondary replicas.</span></span> <span data-ttu-id="9c26e-123">Você pode usar vários ouvintes de comunicação em um serviço, além de especificar aqueles que aceitem solicitações em réplicas secundárias e os que escutam apenas em réplicas primárias.</span><span class="sxs-lookup"><span data-stu-id="9c26e-123">Not only can you use multiple communication listeners in a service, but you can also specify which listeners accept requests on secondary replicas and which ones listen only on primary replicas.</span></span>

<span data-ttu-id="9c26e-124">Por exemplo, você pode ter um ServiceRemotingListener que faz chamadas RPC apenas em réplicas primárias e um segundo ouvinte personalizado que faz solicitações de leitura em réplicas secundárias sobre HTTP:</span><span class="sxs-lookup"><span data-stu-id="9c26e-124">For example, you can have a ServiceRemotingListener that takes RPC calls only on primary replicas, and a second, custom listener that takes read requests on secondary replicas over HTTP:</span></span>

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
> <span data-ttu-id="9c26e-125">Ao se criar vários ouvintes para um serviço, cada ouvinte **deve** receber um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9c26e-125">When creating multiple listeners for a service, each listener **must** be given a unique name.</span></span>
>
>

<span data-ttu-id="9c26e-126">Finalmente, descreva os pontos de extremidade de saudação que são necessários para o serviço Olá Olá [manifesto do serviço](service-fabric-application-model.md) na seção de saudação em pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="9c26e-126">Finally, describe hello endpoints that are required for hello service in hello [service manifest](service-fabric-application-model.md) under hello section on endpoints.</span></span>

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

<span data-ttu-id="9c26e-127">ouvinte de comunicação Olá pode acessar os recursos de ponto de extremidade Olá alocados tooit de saudação `CodePackageActivationContext` em Olá `ServiceContext`.</span><span class="sxs-lookup"><span data-stu-id="9c26e-127">hello communication listener can access hello endpoint resources allocated tooit from hello `CodePackageActivationContext` in hello `ServiceContext`.</span></span> <span data-ttu-id="9c26e-128">Olá pode, em seguida, iniciar o ouvinte escuta solicitações de quando ele é aberto.</span><span class="sxs-lookup"><span data-stu-id="9c26e-128">hello listener can then start listening for requests when it is opened.</span></span>

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> <span data-ttu-id="9c26e-129">Recursos de ponto de extremidade são o pacote de serviço inteiro toohello comuns e são alocados pela malha do serviço quando o pacote de serviço Olá é ativado.</span><span class="sxs-lookup"><span data-stu-id="9c26e-129">Endpoint resources are common toohello entire service package, and they are allocated by Service Fabric when hello service package is activated.</span></span> <span data-ttu-id="9c26e-130">Várias réplicas de serviço hospedadas no hello pode compartilhar a mesma ServiceHost Olá mesma porta.</span><span class="sxs-lookup"><span data-stu-id="9c26e-130">Multiple service replicas hosted in hello same ServiceHost may share hello same port.</span></span> <span data-ttu-id="9c26e-131">Isso significa que esse ouvinte de comunicação Olá deve dar suporte a compartilhamento de porta.</span><span class="sxs-lookup"><span data-stu-id="9c26e-131">This means that hello communication listener should support port sharing.</span></span> <span data-ttu-id="9c26e-132">Olá recomendado maneira de fazer isso é para Olá comunicação ouvinte toouse Olá partição ID e a ID de instância/réplica ao gerar o endereço de escuta hello.</span><span class="sxs-lookup"><span data-stu-id="9c26e-132">hello recommended way of doing this is for hello communication listener toouse hello partition ID and replica/instance ID when it generates hello listen address.</span></span>
>
>

### <a name="service-address-registration"></a><span data-ttu-id="9c26e-133">Registro de endereço do serviço</span><span class="sxs-lookup"><span data-stu-id="9c26e-133">Service address registration</span></span>
<span data-ttu-id="9c26e-134">Um serviço de sistema chamado hello *Naming Service* é executado em clusters de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="9c26e-134">A system service called hello *Naming Service* runs on Service Fabric clusters.</span></span> <span data-ttu-id="9c26e-135">Olá, serviço de nomes é um registrador para serviços e seus endereços de cada instância ou a réplica de serviço hello está escutando.</span><span class="sxs-lookup"><span data-stu-id="9c26e-135">hello Naming Service is a registrar for services and their addresses that each instance or replica of hello service is listening on.</span></span> <span data-ttu-id="9c26e-136">Olá quando `OpenAsync(C#) / openAsync(Java)` método de um `ICommunicationListener(C#) / CommunicationListener(Java)` for concluído, o retorno de valor é registrado no hello Naming Service.</span><span class="sxs-lookup"><span data-stu-id="9c26e-136">When hello `OpenAsync(C#) / openAsync(Java)` method of an `ICommunicationListener(C#) / CommunicationListener(Java)` completes, its return value gets registered in hello Naming Service.</span></span> <span data-ttu-id="9c26e-137">Isso retorna o valor que obtém Olá publicado no serviço de nomes é uma cadeia de caracteres cujo valor pode ser qualquer coisa alguma.</span><span class="sxs-lookup"><span data-stu-id="9c26e-137">This return value that gets published in hello Naming Service is a string whose value can be anything at all.</span></span> <span data-ttu-id="9c26e-138">Esse valor de cadeia de caracteres é o que os clientes verão quando eles solicitam um endereço para o serviço de saudação do hello Naming Service.</span><span class="sxs-lookup"><span data-stu-id="9c26e-138">This string value is what clients see when they ask for an address for hello service from hello Naming Service.</span></span>

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

    // hello string returned here will be published in hello Naming Service.
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

    /* hello string returned here will be published in hello Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

<span data-ttu-id="9c26e-139">Serviço de malha fornece APIs que permitem que os clientes e outros serviços toothen peça para este endereço por nome de serviço.</span><span class="sxs-lookup"><span data-stu-id="9c26e-139">Service Fabric provides APIs that allow clients and other services toothen ask for this address by service name.</span></span> <span data-ttu-id="9c26e-140">Isso é importante porque o endereço do serviço Olá não é estático.</span><span class="sxs-lookup"><span data-stu-id="9c26e-140">This is important because hello service address is not static.</span></span> <span data-ttu-id="9c26e-141">Os serviços são movidos em torno de cluster Olá para fins de disponibilidade e balanceamento de recursos.</span><span class="sxs-lookup"><span data-stu-id="9c26e-141">Services are moved around in hello cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="9c26e-142">Esse é o mecanismo de saudação que permite que clientes tooresolve Olá endereço para um serviço de escuta.</span><span class="sxs-lookup"><span data-stu-id="9c26e-142">This is hello mechanism that allow clients tooresolve hello listening address for a service.</span></span>

> [!NOTE]
> <span data-ttu-id="9c26e-143">Para uma passo a passo completa de como toowrite um ouvinte de comunicação, consulte [serviços de API da Web do serviço do Fabric com OWIN auto-hospedagem](service-fabric-reliable-services-communication-webapi.md) para c#, enquanto para Java, você pode escrever sua própria implementação do servidor HTTP, consulte EchoServer aplicativo exemplo em https://github.com/Azure-Samples/service-fabric-java-getting-started.</span><span class="sxs-lookup"><span data-stu-id="9c26e-143">For a complete walk-through of how toowrite a communication listener, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) for C#, whereas for Java you can write your own HTTP server implementation, see EchoServer application example at https://github.com/Azure-Samples/service-fabric-java-getting-started.</span></span>
>
>

## <a name="communicating-with-a-service"></a><span data-ttu-id="9c26e-144">Comunicando-se com um serviço</span><span class="sxs-lookup"><span data-stu-id="9c26e-144">Communicating with a service</span></span>
<span data-ttu-id="9c26e-145">Olá confiável API de serviços fornece Olá clientes toowrite de bibliotecas que se comunicam com os serviços a seguir.</span><span class="sxs-lookup"><span data-stu-id="9c26e-145">hello Reliable Services API provides hello following libraries toowrite clients that communicate with services.</span></span>

### <a name="service-endpoint-resolution"></a><span data-ttu-id="9c26e-146">Resolução de ponto de extremidade de serviço</span><span class="sxs-lookup"><span data-stu-id="9c26e-146">Service endpoint resolution</span></span>
<span data-ttu-id="9c26e-147">Olá primeira etapa toocommunication com um serviço é tooresolve um endereço de ponto de extremidade de partição hello ou instância de serviço Olá para que deseja tootalk.</span><span class="sxs-lookup"><span data-stu-id="9c26e-147">hello first step toocommunication with a service is tooresolve an endpoint address of hello partition or instance of hello service you want tootalk to.</span></span> <span data-ttu-id="9c26e-148">Olá `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` classe de utilitário é uma primitiva básico que ajuda os clientes a determinar o ponto de extremidade de saudação de um serviço em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="9c26e-148">hello `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` utility class is a basic primitive that helps clients determine hello endpoint of a service at runtime.</span></span> <span data-ttu-id="9c26e-149">Na terminologia de malha do serviço, o processo de Olá de determinar o ponto de extremidade de saudação de um serviço é chamado tooas Olá *resolução do ponto de extremidade de serviço*.</span><span class="sxs-lookup"><span data-stu-id="9c26e-149">In Service Fabric terminology, hello process of determining hello endpoint of a service is referred tooas hello *service endpoint resolution*.</span></span>

<span data-ttu-id="9c26e-150">tooconnect tooservices dentro de um cluster, ServicePartitionResolver pode ser criado usando as configurações padrão.</span><span class="sxs-lookup"><span data-stu-id="9c26e-150">tooconnect tooservices within a cluster, ServicePartitionResolver can be created using default settings.</span></span> <span data-ttu-id="9c26e-151">Isso é recomendada o uso para a maioria das situações de saudação:</span><span class="sxs-lookup"><span data-stu-id="9c26e-151">This is hello recommended usage for most situations:</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

<span data-ttu-id="9c26e-152">tooconnect tooservices em um cluster diferente, um ServicePartitionResolver pode ser criado com um conjunto de pontos de extremidade de gateway do cluster.</span><span class="sxs-lookup"><span data-stu-id="9c26e-152">tooconnect tooservices in a different cluster, a ServicePartitionResolver can be created with a set of cluster gateway endpoints.</span></span> <span data-ttu-id="9c26e-153">Observe que os pontos de extremidade do gateway são diferentes apenas pontos de extremidade de conexão toohello mesmo cluster.</span><span class="sxs-lookup"><span data-stu-id="9c26e-153">Note that gateway endpoints are just different endpoints for connecting toohello same cluster.</span></span> <span data-ttu-id="9c26e-154">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9c26e-154">For example:</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

<span data-ttu-id="9c26e-155">Como alternativa, `ServicePartitionResolver` pode receber uma função para a criação de um `FabricClient` toouse internamente:</span><span class="sxs-lookup"><span data-stu-id="9c26e-155">Alternatively, `ServicePartitionResolver` can be given a function for creating a `FabricClient` toouse internally:</span></span>

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

<span data-ttu-id="9c26e-156">`FabricClient`é objeto Olá toocommunicate usado com cluster do Service Fabric Olá para várias operações de gerenciamento no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9c26e-156">`FabricClient` is hello object that is used toocommunicate with hello Service Fabric cluster for various management operations on hello cluster.</span></span> <span data-ttu-id="9c26e-157">Isso é útil quando você quiser mais controle sobre como um resolvedor de partição de serviço interage com o cluster.</span><span class="sxs-lookup"><span data-stu-id="9c26e-157">This is useful when you want more control over how a service partition resolver interacts with your cluster.</span></span> <span data-ttu-id="9c26e-158">`FabricClient`armazena em cache internamente e é geralmente caro toocreate, portanto, é importante tooreuse `FabricClient` instâncias tanto quanto possíveis.</span><span class="sxs-lookup"><span data-stu-id="9c26e-158">`FabricClient` performs caching internally and is generally expensive toocreate, so it is important tooreuse `FabricClient` instances as much as possible.</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

<span data-ttu-id="9c26e-159">Um método de resolução é usada tooretrieve Olá endereço de um serviço ou uma partição de serviço para serviços particionadas.</span><span class="sxs-lookup"><span data-stu-id="9c26e-159">A resolve method is then used tooretrieve hello address of a service or a service partition for partitioned services.</span></span>

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

<span data-ttu-id="9c26e-160">Um endereço de serviço pode ser resolvido facilmente usando um ServicePartitionResolver, mas é mais trabalhoso tooensure Olá resolvido endereço pode ser usado corretamente.</span><span class="sxs-lookup"><span data-stu-id="9c26e-160">A service address can be resolved easily using a ServicePartitionResolver, but more work is required tooensure hello resolved address can be used correctly.</span></span> <span data-ttu-id="9c26e-161">O cliente precisa toodetect se a tentativa de conexão Olá falhou devido a um erro transitório e pode ser repetida (por exemplo, serviço movido ou está temporariamente indisponível), ou um erro permanente (por exemplo, o serviço foi excluído ou hello recurso solicitado não existe mais).</span><span class="sxs-lookup"><span data-stu-id="9c26e-161">Your client needs toodetect whether hello connection attempt failed because of a transient error and can be retried (e.g., service moved or is temporarily unavailable), or a permanent error (e.g., service was deleted or hello requested resource no longer exists).</span></span> <span data-ttu-id="9c26e-162">Instâncias de serviço ou réplicas podem se mover de nó toonode a qualquer momento por vários motivos.</span><span class="sxs-lookup"><span data-stu-id="9c26e-162">Service instances or replicas can move around from node toonode at any time for multiple reasons.</span></span> <span data-ttu-id="9c26e-163">endereço do serviço Olá resolvido por meio de ServicePartitionResolver pode ficar obsoleto pelo tempo de saudação que tooconnect tentativas de código do cliente.</span><span class="sxs-lookup"><span data-stu-id="9c26e-163">hello service address resolved through ServicePartitionResolver may be stale by hello time your client code attempts tooconnect.</span></span> <span data-ttu-id="9c26e-164">Nesse caso novamente cliente Olá precisa de resolução toore Olá endereço.</span><span class="sxs-lookup"><span data-stu-id="9c26e-164">In that case again hello client needs toore-resolve hello address.</span></span> <span data-ttu-id="9c26e-165">Fornecendo Olá anterior `ResolvedServicePartition` indica que Olá resolvedor necessidades tootry novamente, em vez de simplesmente recuperar um endereço armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="9c26e-165">Providing hello previous `ResolvedServicePartition` indicates that hello resolver needs tootry again rather than simply retrieve a cached address.</span></span>

<span data-ttu-id="9c26e-166">Normalmente, o código de cliente Olá necessário trabalhar com hello ServicePartitionResolver não diretamente.</span><span class="sxs-lookup"><span data-stu-id="9c26e-166">Typically, hello client code need not work with hello ServicePartitionResolver directly.</span></span> <span data-ttu-id="9c26e-167">Ele é criado e repassado toocommunication fábricas de cliente em Olá confiável API de serviços.</span><span class="sxs-lookup"><span data-stu-id="9c26e-167">It is created and passed on toocommunication client factories in hello Reliable Services API.</span></span> <span data-ttu-id="9c26e-168">fábricas de saudação usam resolvedor Olá internamente toogenerate um objeto cliente que pode ser usado toocommunicate com os serviços.</span><span class="sxs-lookup"><span data-stu-id="9c26e-168">hello factories use hello resolver internally toogenerate a client object that can be used toocommunicate with services.</span></span>

### <a name="communication-clients-and-factories"></a><span data-ttu-id="9c26e-169">Fábricas e clientes de comunicação</span><span class="sxs-lookup"><span data-stu-id="9c26e-169">Communication clients and factories</span></span>
<span data-ttu-id="9c26e-170">biblioteca de fábrica de comunicação Olá implementa um padrão típico de repetição de tratamento de falhas que facilita tentando novamente conexões tooresolved pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="9c26e-170">hello communication factory library implements a typical fault-handling retry pattern that makes retrying connections tooresolved service endpoints easier.</span></span> <span data-ttu-id="9c26e-171">biblioteca de fábrica Olá fornece mecanismo de repetição Olá enquanto você fornece manipuladores de erro hello.</span><span class="sxs-lookup"><span data-stu-id="9c26e-171">hello factory library provides hello retry mechanism while you provide hello error handlers.</span></span>

<span data-ttu-id="9c26e-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`Define a interface base hello, implementada por uma fábrica de cliente de comunicação que produz os clientes que podem se comunicar tooa serviço de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="9c26e-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` defines hello base interface implemented by a communication client factory that produces clients that can talk tooa Service Fabric service.</span></span> <span data-ttu-id="9c26e-173">Olá implementação de saudação que communicationclientfactory depende Olá pilha de comunicação usada pelo serviço de malha do serviço de Olá onde o cliente Olá quer toocommunicate.</span><span class="sxs-lookup"><span data-stu-id="9c26e-173">hello implementation of hello CommunicationClientFactory depends on hello communication stack used by hello Service Fabric service where hello client wants toocommunicate.</span></span> <span data-ttu-id="9c26e-174">Olá confiável API de serviços fornece um `CommunicationClientFactoryBase<TCommunicationClient>`.</span><span class="sxs-lookup"><span data-stu-id="9c26e-174">hello Reliable Services API provides a `CommunicationClientFactoryBase<TCommunicationClient>`.</span></span> <span data-ttu-id="9c26e-175">Isso fornece uma implementação básica da interface de CommunicationClientFactory hello e executa tarefas que são comuns pilhas de comunicação de saudação tooall.</span><span class="sxs-lookup"><span data-stu-id="9c26e-175">This provides a base implementation of hello CommunicationClientFactory interface and performs tasks that are common tooall hello communication stacks.</span></span> <span data-ttu-id="9c26e-176">(Essas tarefas incluem o uso de um ponto de extremidade de serviço do ServicePartitionResolver toodetermine Olá).</span><span class="sxs-lookup"><span data-stu-id="9c26e-176">(These tasks include using a ServicePartitionResolver toodetermine hello service endpoint).</span></span> <span data-ttu-id="9c26e-177">Os clientes normalmente implementar Olá abstrata CommunicationClientFactoryBase classe toohandle lógica de pilha de comunicação toohello específico.</span><span class="sxs-lookup"><span data-stu-id="9c26e-177">Clients usually implement hello abstract CommunicationClientFactoryBase class toohandle logic that is specific toohello communication stack.</span></span>

<span data-ttu-id="9c26e-178">cliente de comunicação Olá apenas recebe um endereço e usa tooconnect tooa service.</span><span class="sxs-lookup"><span data-stu-id="9c26e-178">hello communication client just receives an address and uses it tooconnect tooa service.</span></span> <span data-ttu-id="9c26e-179">cliente Olá pode usar qualquer protocolo ele deseja.</span><span class="sxs-lookup"><span data-stu-id="9c26e-179">hello client can use whatever protocol it wants.</span></span>

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

<span data-ttu-id="9c26e-180">fábrica de saudação do cliente é basicamente responsável pela criação de clientes de comunicação.</span><span class="sxs-lookup"><span data-stu-id="9c26e-180">hello client factory is primarily responsible for creating communication clients.</span></span> <span data-ttu-id="9c26e-181">Para clientes que não mantêm uma conexão persistente, como um cliente HTTP, fábrica Olá só precisa toocreate e cliente Olá retorno.</span><span class="sxs-lookup"><span data-stu-id="9c26e-181">For clients that don't maintain a persistent connection, such as an HTTP client, hello factory only needs toocreate and return hello client.</span></span> <span data-ttu-id="9c26e-182">Outros protocolos que mantêm uma conexão persistente, como alguns protocolos binários, também devem ser validados pelo Olá fábrica toodetermine se conexão Olá precisa toobe criado novamente.</span><span class="sxs-lookup"><span data-stu-id="9c26e-182">Other protocols that maintain a persistent connection, such as some binary protocols, should also be validated by hello factory toodetermine whether hello connection needs toobe re-created.</span></span>  

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

<span data-ttu-id="9c26e-183">Por fim, um manipulador de exceção é responsável por determinar quais tootake ação quando ocorre uma exceção.</span><span class="sxs-lookup"><span data-stu-id="9c26e-183">Finally, an exception handler is responsible for determining what action tootake when an exception occurs.</span></span> <span data-ttu-id="9c26e-184">Exceções são categorizadas como **repetíveis** e **não repetíveis**.</span><span class="sxs-lookup"><span data-stu-id="9c26e-184">Exceptions are categorized into **retryable** and **non retryable**.</span></span>

* <span data-ttu-id="9c26e-185">**Sem nova tentativa** exceções simplesmente obtenham relançadas toohello back chamador.</span><span class="sxs-lookup"><span data-stu-id="9c26e-185">**Non retryable** exceptions simply get rethrown back toohello caller.</span></span>
* <span data-ttu-id="9c26e-186">Exceções **repetíveis** são categorizadas novamente em **transitórias** e **não transitórias**.</span><span class="sxs-lookup"><span data-stu-id="9c26e-186">**retryable** exceptions are further categorized into **transient** and **non-transient**.</span></span>
  * <span data-ttu-id="9c26e-187">**Transitório** exceções são aqueles que simplesmente pode ser repetida sem resolver novamente o endereço de ponto de extremidade de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="9c26e-187">**Transient** exceptions are those that can simply be retried without re-resolving hello service endpoint address.</span></span> <span data-ttu-id="9c26e-188">Isso incluirá os problemas de rede temporários ou respostas de erro de serviço que não sejam aqueles que indicam o endereço do ponto de extremidade de serviço de saudação não existe.</span><span class="sxs-lookup"><span data-stu-id="9c26e-188">These will include transient network problems or service error responses other than those that indicate hello service endpoint address does not exist.</span></span>
  * <span data-ttu-id="9c26e-189">**Não transitório** exceções são aqueles que exigem um ponto de extremidade de serviço de Olá endereço toobe resolvido novamente.</span><span class="sxs-lookup"><span data-stu-id="9c26e-189">**Non-transient** exceptions are those that require hello service endpoint address toobe re-resolved.</span></span> <span data-ttu-id="9c26e-190">Elas incluem exceções que indicam o ponto de extremidade de serviço de saudação não pôde ser alcançado, indicando que o serviço Olá moveu tooa outro nó.</span><span class="sxs-lookup"><span data-stu-id="9c26e-190">These include exceptions that indicate hello service endpoint could not be reached, indicating hello service has moved tooa different node.</span></span>

<span data-ttu-id="9c26e-191">Olá `TryHandleException` toma uma decisão sobre uma determinada exceção.</span><span class="sxs-lookup"><span data-stu-id="9c26e-191">hello `TryHandleException` makes a decision about a given exception.</span></span> <span data-ttu-id="9c26e-192">Se ele **não sabe** que toomake decisões sobre uma exceção, ele deverá retornar **false**.</span><span class="sxs-lookup"><span data-stu-id="9c26e-192">If it **does not know** what decisions toomake about an exception, it should return **false**.</span></span> <span data-ttu-id="9c26e-193">Se ele **saber** que toomake de decisão, deve definir o resultado de saudação adequadamente e retornar **true**.</span><span class="sxs-lookup"><span data-stu-id="9c26e-193">If it **does know** what decision toomake, it should set hello result accordingly and return **true**.</span></span>

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

        // if exceptionInformation.Exception is unknown (let hello next IExceptionHandler attempt toohandle it)
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

        /* if exceptionInformation.getException() is unknown (let hello next ExceptionHandler attempt toohandle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a><span data-ttu-id="9c26e-194">Juntando as peças</span><span class="sxs-lookup"><span data-stu-id="9c26e-194">Putting it all together</span></span>
<span data-ttu-id="9c26e-195">Com um `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, e `IExceptionHandler(C#) / ExceptionHandler(Java)` criadas em torno de um protocolo de comunicação, um `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` encapsula todos juntos e fornece tratamento de falhas de saudação e loop de resolução de endereço de partição de serviço em torno desses componentes.</span><span class="sxs-lookup"><span data-stu-id="9c26e-195">With an `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, and `IExceptionHandler(C#) / ExceptionHandler(Java)` built around a communication protocol, a `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` wraps it all together and provides hello fault-handling and service partition address resolution loop around these components.</span></span>

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with hello service using hello client.
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
      /* Communicate with hello service using hello client.
       */
   });

```

## <a name="next-steps"></a><span data-ttu-id="9c26e-196">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9c26e-196">Next steps</span></span>
* <span data-ttu-id="9c26e-197">Confira um exemplo de comunicação HTTP entre serviços em um [projeto de exemplo C# no GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) ou [Projeto de exemplo Java no GitHub](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span><span class="sxs-lookup"><span data-stu-id="9c26e-197">See an example of HTTP communication between services in a [C# sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) or [Java sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span></span>
* [<span data-ttu-id="9c26e-198">Comunicação remota de serviço com os Reliable Services</span><span class="sxs-lookup"><span data-stu-id="9c26e-198">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="9c26e-199">API Web que usa o OWIN nos Reliable Services</span><span class="sxs-lookup"><span data-stu-id="9c26e-199">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="9c26e-200">Comunicação WCF usando os Reliable Services</span><span class="sxs-lookup"><span data-stu-id="9c26e-200">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
