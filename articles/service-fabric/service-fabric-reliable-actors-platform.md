---
title: Reliable Actors no Service Fabric | Microsoft Docs
description: "Descreve como os Reliable Actors são dispostos em camadas nos Reliable Services e como eles usam os recursos da plataforma do Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 45839a7f-0536-46f1-ae2b-8ba3556407fb
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: 0a12da52b6e74c721cd25f89e7cde3c07153a396
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-reliable-actors-use-the-service-fabric-platform"></a><span data-ttu-id="7eb9a-103">Como Reliable Actors usam a plataforma do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7eb9a-103">How Reliable Actors use the Service Fabric platform</span></span>
<span data-ttu-id="7eb9a-104">Este artigo explica sobre o funcionamento dos Reliable Actors na plataforma do Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-104">This article explains how Reliable Actors work on the Azure Service Fabric platform.</span></span> <span data-ttu-id="7eb9a-105">Os Reliable Actors são executados em uma estrutura hospedada em uma implementação de um serviço confiável com estado chamado *serviço de ator*.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-105">Reliable Actors run in a framework that is hosted in an implementation of a stateful reliable service called the *actor service*.</span></span> <span data-ttu-id="7eb9a-106">O serviço de ator contém todos os componentes necessários para gerenciar o ciclo de vida e a expedição de mensagens para seus atores:</span><span class="sxs-lookup"><span data-stu-id="7eb9a-106">The actor service contains all the components necessary to manage the lifecycle and message dispatching for your actors:</span></span>

* <span data-ttu-id="7eb9a-107">O Tempo de Execução de Ator gerencia o ciclo de vida, a coleta de lixo e impõe o acesso single-threaded.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-107">The Actor Runtime manages lifecycle, garbage collection, and enforces single-threaded access.</span></span>
* <span data-ttu-id="7eb9a-108">Um ouvinte de comunicação remota do serviço de ator aceita chamadas de acesso remoto aos atores e as envia a um dispatcher para encaminhamento à instância de ator apropriada.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-108">An actor service remoting listener accepts remote access calls to actors and sends them to a dispatcher to route to the appropriate actor instance.</span></span>
* <span data-ttu-id="7eb9a-109">O Provedor de Estado de Ator encapsula provedores de estado (como o provedor de estado das Coleções Confiáveis) e fornece um adaptador para o gerenciamento de estado de ator.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-109">The Actor State Provider wraps state providers (such as the Reliable Collections state provider) and provides an adapter for actor state management.</span></span>

<span data-ttu-id="7eb9a-110">Juntos, esses componentes formam a estrutura do Reliable Actor.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-110">These components together form the Reliable Actor framework.</span></span>

## <a name="service-layering"></a><span data-ttu-id="7eb9a-111">Disposição em camadas de serviço</span><span class="sxs-lookup"><span data-stu-id="7eb9a-111">Service layering</span></span>
<span data-ttu-id="7eb9a-112">Como o próprio serviço de ator é um serviço confiável, todos os conceitos de [modelo de aplicativo](service-fabric-application-model.md), ciclo de vida, [empacotamento](service-fabric-package-apps.md), [implantação](service-fabric-deploy-remove-applications.md), atualização e dimensionamento dos Reliable Services aplicam-se da mesma maneira aos serviços de ator.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-112">Because the actor service itself is a reliable service, all the [application model](service-fabric-application-model.md), lifecycle, [packaging](service-fabric-package-apps.md), [deployment](service-fabric-deploy-remove-applications.md), upgrade, and scaling concepts of Reliable Services apply the same way to actor services.</span></span> 

![Disposição em camadas do serviço de ator][1]

<span data-ttu-id="7eb9a-114">O diagrama anterior mostra a relação entre as estruturas do aplicativo do Service Fabric e o código do usuário.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-114">The preceding diagram shows the relationship between the Service Fabric application frameworks and user code.</span></span> <span data-ttu-id="7eb9a-115">Os elementos em azul representam a estrutura do aplicativo dos Reliable Services, os elementos em laranja representam a estrutura do Reliable Actor e os elementos em verde representam o código do usuário.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-115">Blue elements represent the Reliable Services application framework, orange represents the Reliable Actor framework, and green represents user code.</span></span>

<span data-ttu-id="7eb9a-116">Nos Reliable Services, o serviço herda a classe `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-116">In Reliable Services, your service inherits the `StatefulService` class.</span></span> <span data-ttu-id="7eb9a-117">Essa classe é derivada de `StatefulServiceBase` (ou `StatelessService` para serviços sem estado).</span><span class="sxs-lookup"><span data-stu-id="7eb9a-117">This class is itself derived from `StatefulServiceBase` (or `StatelessService` for stateless services).</span></span> <span data-ttu-id="7eb9a-118">Nos Reliable Actors, você usa o serviço de ator.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-118">In Reliable Actors, you use the actor service.</span></span> <span data-ttu-id="7eb9a-119">O serviço de ator é uma implementação diferente da classe `StatefulServiceBase` que implementa o padrão de ator no qual seus atores são executados.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-119">The actor service is a different implementation of the `StatefulServiceBase` class that implements the actor pattern where your actors run.</span></span> <span data-ttu-id="7eb9a-120">Como o próprio serviço de ator é apenas uma implementação de `StatefulServiceBase`, é possível escrever seu próprio serviço que deriva de `ActorService` e implementar recursos no nível de serviço da mesma forma que você faria ao herdar `StatefulService`, tais como:</span><span class="sxs-lookup"><span data-stu-id="7eb9a-120">Because the actor service itself is just an implementation of `StatefulServiceBase`, you can write your own service that derives from `ActorService` and implement service-level features the same way you would when inheriting `StatefulService`, such as:</span></span>

* <span data-ttu-id="7eb9a-121">Backup e restauração do serviço.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-121">Service backup and restore.</span></span>
* <span data-ttu-id="7eb9a-122">Funcionalidade compartilhada para todos os atores, por exemplo, um disjuntor.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-122">Shared functionality for all actors, for example, a circuit breaker.</span></span>
* <span data-ttu-id="7eb9a-123">Chamadas de procedimento remotas no próprio serviço de ator, bem como em cada ator individual.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-123">Remote procedure calls on the actor service itself and on each individual actor.</span></span>

> [!NOTE]
> <span data-ttu-id="7eb9a-124">Atualmente não há suporte para os serviços com estado no Java/Linux.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-124">Stateful services are not currently supported in Java/Linux.</span></span>

### <a name="using-the-actor-service"></a><span data-ttu-id="7eb9a-125">Usando o serviço de ator</span><span class="sxs-lookup"><span data-stu-id="7eb9a-125">Using the actor service</span></span>
<span data-ttu-id="7eb9a-126">As instâncias de ator têm acesso ao serviço de ator no qual estão sendo executadas.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-126">Actor instances have access to the actor service in which they are running.</span></span> <span data-ttu-id="7eb9a-127">Por meio do serviço de ator, as instâncias de ator podem obter programaticamente o contexto de serviço.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-127">Through the actor service, actor instances can programmatically obtain the service context.</span></span> <span data-ttu-id="7eb9a-128">O contexto de serviço tem a ID da partição, o nome do serviço, o nome do aplicativo e outras informações específicas da plataforma do Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="7eb9a-128">The service context has the partition ID, service name, application name, and other Service Fabric platform-specific information:</span></span>

```csharp
Task MyActorMethod()
{
    Guid partitionId = this.ActorService.Context.PartitionId;
    string serviceTypeName = this.ActorService.Context.ServiceTypeName;
    Uri serviceInstanceName = this.ActorService.Context.ServiceName;
    string applicationInstanceName = this.ActorService.Context.CodePackageActivationContext.ApplicationName;
}
```
```Java
CompletableFuture<?> MyActorMethod()
{
    UUID partitionId = this.getActorService().getServiceContext().getPartitionId();
    String serviceTypeName = this.getActorService().getServiceContext().getServiceTypeName();
    URI serviceInstanceName = this.getActorService().getServiceContext().getServiceName();
    String applicationInstanceName = this.getActorService().getServiceContext().getCodePackageActivationContext().getApplicationName();
}
```


<span data-ttu-id="7eb9a-129">Como todos os Reliable Services, o serviço de ator deve ser registrado com um tipo de serviço no tempo de execução do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-129">Like all Reliable Services, the actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="7eb9a-130">Para que o serviço de ator seja executado em suas instâncias de ator, o tipo de ator também deve ser registrado no serviço de ator.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-130">For the actor service to run your actor instances, your actor type must also be registered with the actor service.</span></span> <span data-ttu-id="7eb9a-131">O método de registro `ActorRuntime` realiza esse trabalho para os atores.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-131">The `ActorRuntime` registration method performs this work for actors.</span></span> <span data-ttu-id="7eb9a-132">No caso mais simples, é possível apenas registrar o tipo de ator, e o serviço de ator, com as configurações padrão, será usado implicitamente:</span><span class="sxs-lookup"><span data-stu-id="7eb9a-132">In the simplest case, you can just register your actor type, and the actor service with default settings will implicitly be used:</span></span>

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>().GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```

<span data-ttu-id="7eb9a-133">Como alternativa, você pode usar um lambda fornecido pelo método de registro para que você possa construir o serviço de ator por conta própria.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-133">Alternatively, you can use a lambda provided by the registration method to construct the actor service yourself.</span></span> <span data-ttu-id="7eb9a-134">Assim, você pode configurar o serviço de ator e construir explicitamente as instâncias de ator, nas quais é possível injetar dependências no ator por meio de seu construtor:</span><span class="sxs-lookup"><span data-stu-id="7eb9a-134">You can then configure the actor service and explicitly construct your actor instances, where you can inject dependencies to your actor through its constructor:</span></span>

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new ActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
static class Program
{
    private static void Main()
    {
      ActorRuntime.registerActorAsync(
              MyActor.class,
              (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
              timeout);

        Thread.sleep(Long.MAX_VALUE);
    }
}
```

### <a name="actor-service-methods"></a><span data-ttu-id="7eb9a-135">Métodos do serviço de ator</span><span class="sxs-lookup"><span data-stu-id="7eb9a-135">Actor service methods</span></span>
<span data-ttu-id="7eb9a-136">O Serviço de ator implementa `IActorService` (C#) ou `ActorService` (Java), que, por sua vez, implementa `IService` (C#) ou `Service` (Java).</span><span class="sxs-lookup"><span data-stu-id="7eb9a-136">The Actor service implements `IActorService` (C#) or `ActorService` (Java), which in turn implements `IService` (C#) or `Service` (Java).</span></span> <span data-ttu-id="7eb9a-137">Essa é a interface usada pela comunicação remota dos Reliable Services, que possibilita chamadas de procedimento remoto em métodos de serviço.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-137">This is the interface used by Reliable Services remoting, which allows remote procedure calls on service methods.</span></span> <span data-ttu-id="7eb9a-138">Ela contém métodos no nível de serviço que podem ser chamados remotamente por meio da comunicação remota do serviço.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-138">It contains service-level methods that can be called remotely via service remoting.</span></span>

#### <a name="enumerating-actors"></a><span data-ttu-id="7eb9a-139">Enumerando os atores</span><span class="sxs-lookup"><span data-stu-id="7eb9a-139">Enumerating actors</span></span>
<span data-ttu-id="7eb9a-140">O serviço de ator permite que um cliente enumere metadados sobre os atores que estão sendo hospedados pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-140">The actor service allows a client to enumerate metadata about the actors that the service is hosting.</span></span> <span data-ttu-id="7eb9a-141">Como o serviço de ator é um serviço com estado particionado, a enumeração é realizada por partição.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-141">Because the actor service is a partitioned stateful service, enumeration is performed per partition.</span></span> <span data-ttu-id="7eb9a-142">Como cada partição pode conter vários atores, a enumeração é retornada como um conjunto de resultados paginados.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-142">Because each partition might contain many actors, the enumeration is returned as a set of paged results.</span></span> <span data-ttu-id="7eb9a-143">É executado um loop das páginas até que todas as páginas sejam lidas.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-143">The pages are looped over until all pages are read.</span></span> <span data-ttu-id="7eb9a-144">O seguinte exemplo mostra como criar uma lista de todos os atores ativos em uma partição de um serviço de ator:</span><span class="sxs-lookup"><span data-stu-id="7eb9a-144">The following example shows how to create a list of all active actors in one partition of an actor service:</span></span>

```csharp
IActorService actorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new List<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = await actorServiceProxy.GetActorsAsync(continuationToken, cancellationToken);

    activeActors.AddRange(page.Items.Where(x => x.IsActive));

    continuationToken = page.ContinuationToken;
}
while (continuationToken != null);
```

```Java
ActorService actorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new ArrayList<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = actorServiceProxy.getActorsAsync(continuationToken);

    while(ActorInformation x: page.getItems())
    {
         if(x.isActive()){
              activeActors.add(x);
         }
    }

    continuationToken = page.getContinuationToken();
}
while (continuationToken != null);
```

#### <a name="deleting-actors"></a><span data-ttu-id="7eb9a-145">Excluindo atores</span><span class="sxs-lookup"><span data-stu-id="7eb9a-145">Deleting actors</span></span>
<span data-ttu-id="7eb9a-146">O serviço de ator também fornece uma função para a exclusão de atores:</span><span class="sxs-lookup"><span data-stu-id="7eb9a-146">The actor service also provides a function for deleting actors:</span></span>

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

<span data-ttu-id="7eb9a-147">Para obter mais informações sobre como excluir atores e seu estado, consulte a [documentação de ciclo de vida do ator](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="7eb9a-147">For more information on deleting actors and their state, see the [actor lifecycle documentation](service-fabric-reliable-actors-lifecycle.md).</span></span>

### <a name="custom-actor-service"></a><span data-ttu-id="7eb9a-148">Serviço de ator personalizado</span><span class="sxs-lookup"><span data-stu-id="7eb9a-148">Custom actor service</span></span>
<span data-ttu-id="7eb9a-149">Usando o lambda de registro do ator, você pode registrar seu próprio serviço de ator personalizado que deriva de `ActorService` (C#) e `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="7eb9a-149">By using the actor registration lambda, you can register your own custom actor service that derives from `ActorService` (C#) and `FabricActorService` (Java).</span></span> <span data-ttu-id="7eb9a-150">Neste serviço de ator personalizado, você pode implementar sua própria funcionalidade de nível de serviço, escrevendo uma classe de serviço que herda `ActorService` (C#) ou `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="7eb9a-150">In this custom actor service, you can implement your own service-level functionality by writing a service class that inherits `ActorService` (C#) or `FabricActorService` (Java).</span></span> <span data-ttu-id="7eb9a-151">Um serviço de ator personalizado herda toda a funcionalidade de tempo de execução do ator de `ActorService` (C#) ou `FabricActorService` (Java) e pode ser usado para implementar seus próprios métodos de serviço.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-151">A custom actor service inherits all the actor runtime functionality from `ActorService` (C#) or `FabricActorService` (Java) and can be used to implement your own service methods.</span></span>

```csharp
class MyActorService : ActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }
}
```
```Java
class MyActorService extends FabricActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, BiFunction<FabricActorService, ActorId, ActorBase> newActor)
    {
         super(context, typeInfo, newActor);
    }
}
```

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new MyActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
public class Program
{
    public static void main(String[] args)
    {
        ActorRuntime.registerActorAsync(
                MyActor.class,
                (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
                timeout);
        Thread.sleep(Long.MAX_VALUE);
    }
}
```

#### <a name="implementing-actor-backup-and-restore"></a><span data-ttu-id="7eb9a-152">Implementando o backup e a restauração de ator</span><span class="sxs-lookup"><span data-stu-id="7eb9a-152">Implementing actor backup and restore</span></span>
 <span data-ttu-id="7eb9a-153">No seguinte exemplo, o serviço de ator personalizado expõe um método para fazer backup dos dados do ator, aproveitando o ouvinte de comunicação remota já presente em `ActorService`:</span><span class="sxs-lookup"><span data-stu-id="7eb9a-153">In the following example, the custom actor service exposes a method to back up actor data by taking advantage of the remoting listener already present in `ActorService`:</span></span>

```csharp
public interface IMyActorService : IService
{
    Task BackupActorsAsync();
}

class MyActorService : ActorService, IMyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }

    public Task BackupActorsAsync()
    {
        return this.BackupAsync(new BackupDescription(PerformBackupAsync));
    }

    private async Task<bool> PerformBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store the contents of backupInfo.Directory
           return true;
        }
        finally
        {
           Directory.Delete(backupInfo.Directory, recursive: true);
        }
    }
}
```
```Java
public interface MyActorService extends Service
{
    CompletableFuture<?> backupActorsAsync();
}

class MyActorServiceImpl extends ActorService implements MyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<FabricActorService, ActorId, ActorBase> newActor)
    {
       super(context, typeInfo, newActor);
    }

    public CompletableFuture backupActorsAsync()
    {
        return this.backupAsync(new BackupDescription((backupInfo, cancellationToken) -> performBackupAsync(backupInfo, cancellationToken)));
    }

    private CompletableFuture<Boolean> performBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store the contents of backupInfo.Directory
           return true;
        }
        finally
        {
           deleteDirectory(backupInfo.Directory)
        }
    }

    void deleteDirectory(File file) {
        File[] contents = file.listFiles();
        if (contents != null) {
            for (File f : contents) {
               deleteDirectory(f);
             }
        }
        file.delete();
    }
}
```


<span data-ttu-id="7eb9a-154">Neste exemplo, o `IMyActorService` é um contrato de comunicação remota que implementa `IService` (C#) e `Service` (Java) e que, em seguida, é implementado por `MyActorService`.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-154">In this example, `IMyActorService` is a remoting contract that implements `IService` (C#) and `Service` (Java), and is then implemented by `MyActorService`.</span></span> <span data-ttu-id="7eb9a-155">Ao adicionar esse contrato de comunicação remota, os métodos em `IMyActorService` agora também ficam disponíveis para um cliente, por meio da criação de um proxy de comunicação remota através do `ActorServiceProxy`:</span><span class="sxs-lookup"><span data-stu-id="7eb9a-155">By adding this remoting contract, methods on `IMyActorService` are now also available to a client by creating a remoting proxy via `ActorServiceProxy`:</span></span>

```csharp
IMyActorService myActorServiceProxy = ActorServiceProxy.Create<IMyActorService>(
    new Uri("fabric:/MyApp/MyService"), ActorId.CreateRandom());

await myActorServiceProxy.BackupActorsAsync();
```
```Java
MyActorService myActorServiceProxy = ActorServiceProxy.create(MyActorService.class,
    new URI("fabric:/MyApp/MyService"), actorId);

myActorServiceProxy.backupActorsAsync();
```

## <a name="application-model"></a><span data-ttu-id="7eb9a-156">Modelo de aplicativo</span><span class="sxs-lookup"><span data-stu-id="7eb9a-156">Application model</span></span>
<span data-ttu-id="7eb9a-157">Os serviços de ator são Reliable Services; portanto, o modelo do aplicativo é o mesmo.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-157">Actor services are Reliable Services, so the application model is the same.</span></span> <span data-ttu-id="7eb9a-158">No entanto, as ferramentas de build da estrutura de ator geram alguns dos arquivos de modelo do aplicativo para você.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-158">However, the actor framework build tools generate some of the application model files for you.</span></span>

### <a name="service-manifest"></a><span data-ttu-id="7eb9a-159">Manifesto do serviço</span><span class="sxs-lookup"><span data-stu-id="7eb9a-159">Service manifest</span></span>
<span data-ttu-id="7eb9a-160">As ferramentas de build da estrutura de ator geram automaticamente o conteúdo do arquivo ServiceManifest.xml do serviço de ator.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-160">The actor framework build tools automatically generate the contents of your actor service's ServiceManifest.xml file.</span></span> <span data-ttu-id="7eb9a-161">Este arquivo inclui:</span><span class="sxs-lookup"><span data-stu-id="7eb9a-161">This file includes:</span></span>

* <span data-ttu-id="7eb9a-162">O tipo de serviço de ator.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-162">Actor service type.</span></span> <span data-ttu-id="7eb9a-163">O nome do tipo é gerado de acordo com o nome de projeto do ator.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-163">The type name is generated based on your actor's project name.</span></span> <span data-ttu-id="7eb9a-164">Com base no atributo de persistência do ator, o sinalizador HasPersistedState também é definido de acordo.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-164">Based on the persistence attribute on your actor, the HasPersistedState flag is also set accordingly.</span></span>
* <span data-ttu-id="7eb9a-165">Pacote de códigos.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-165">Code package.</span></span>
* <span data-ttu-id="7eb9a-166">Pacote de configuração.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-166">Config package.</span></span>
* <span data-ttu-id="7eb9a-167">Recursos e pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-167">Resources and endpoints.</span></span>

### <a name="application-manifest"></a><span data-ttu-id="7eb9a-168">Manifesto do aplicativo</span><span class="sxs-lookup"><span data-stu-id="7eb9a-168">Application manifest</span></span>
<span data-ttu-id="7eb9a-169">As ferramentas de build da estrutura de ator criam automaticamente uma definição de serviço padrão para o serviço de ator.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-169">The actor framework build tools automatically create a default service definition for your actor service.</span></span> <span data-ttu-id="7eb9a-170">As ferramentas de build preenchem as propriedades padrão do serviço:</span><span class="sxs-lookup"><span data-stu-id="7eb9a-170">The build tools populate the default service properties:</span></span>

* <span data-ttu-id="7eb9a-171">A contagem de conjuntos de réplicas é determinada pelo atributo de persistência no ator.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-171">Replica set count is determined by the persistence attribute on your actor.</span></span> <span data-ttu-id="7eb9a-172">Sempre que o atributo de persistência no ator é alterado, a contagem de conjuntos de réplicas na definição de serviço padrão é redefinida de acordo.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-172">Each time the persistence attribute on your actor is changed, the replica set count in the default service definition is reset accordingly.</span></span>
* <span data-ttu-id="7eb9a-173">O esquema de partição e o intervalo são definidos como Int64 Uniforme com o intervalo de chaves Int64 completo.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-173">Partition scheme and range are set to Uniform Int64 with the full Int64 key range.</span></span>

## <a name="service-fabric-partition-concepts-for-actors"></a><span data-ttu-id="7eb9a-174">Conceitos de partição de Malha do Serviço para atores</span><span class="sxs-lookup"><span data-stu-id="7eb9a-174">Service Fabric partition concepts for actors</span></span>
<span data-ttu-id="7eb9a-175">Serviços de ator são serviços com estado particionados.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-175">Actor services are partitioned stateful services.</span></span> <span data-ttu-id="7eb9a-176">Cada partição de um serviço de ator contém um conjunto de atores.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-176">Each partition of an actor service contains a set of actors.</span></span> <span data-ttu-id="7eb9a-177">As partições de serviço são distribuídas automaticamente em vários nós no Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-177">Service partitions are automatically distributed over multiple nodes in Service Fabric.</span></span> <span data-ttu-id="7eb9a-178">As instâncias de ator são distribuídas como resultado disso.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-178">Actor instances are distributed as a result.</span></span>

![Particionamento e distribuição de ator][5]

<span data-ttu-id="7eb9a-180">Os Reliable Services podem ser criados com esquemas de partição diferentes e intervalos de chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-180">Reliable Services can be created with different partition schemes and partition key ranges.</span></span> <span data-ttu-id="7eb9a-181">O serviço de ator usa o esquema de particionamento Int64 com o intervalo de chaves Int64 completo para mapear os atores para as partições.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-181">The actor service uses the Int64 partitioning scheme with the full Int64 key range to map actors to partitions.</span></span>

### <a name="actor-id"></a><span data-ttu-id="7eb9a-182">ID de ator</span><span class="sxs-lookup"><span data-stu-id="7eb9a-182">Actor ID</span></span>
<span data-ttu-id="7eb9a-183">Cada ator criado no serviço tem uma ID exclusiva associada, representada pela classe `ActorId` .</span><span class="sxs-lookup"><span data-stu-id="7eb9a-183">Each actor that's created in the service has a unique ID associated with it, represented by the `ActorId` class.</span></span> <span data-ttu-id="7eb9a-184">A `ActorId` é um valor de ID opaco que pode ser usado para a distribuição uniforme de atores nas partições de serviço por meio da geração de IDs aleatórias:</span><span class="sxs-lookup"><span data-stu-id="7eb9a-184">`ActorId` is an opaque ID value that can be used for uniform distribution of actors across the service partitions by generating random IDs:</span></span>

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


<span data-ttu-id="7eb9a-185">Cada `ActorId` é codificada em hash para um Int64.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-185">Every `ActorId` is hashed to an Int64.</span></span> <span data-ttu-id="7eb9a-186">É por esse motivo que o serviço de ator deve usar um esquema de particionamento Int64 com o intervalo de chaves Int64 completo.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-186">This is why the actor service must use an Int64 partitioning scheme with the full Int64 key range.</span></span> <span data-ttu-id="7eb9a-187">No entanto, valores de ID personalizados podem ser usados para uma `ActorID`, incluindo GUIDs/UUIDs, cadeias de caracteres e Int64s.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-187">However, custom ID values can be used for an `ActorID`, including GUIDs/UUIDs, strings, and Int64s.</span></span>

```csharp
ActorProxy.Create<IMyActor>(new ActorId(Guid.NewGuid()));
ActorProxy.Create<IMyActor>(new ActorId("myActorId"));
ActorProxy.Create<IMyActor>(new ActorId(1234));
```
```Java
ActorProxyBase.create(MyActor.class, new ActorId(UUID.randomUUID()));
ActorProxyBase.create(MyActor.class, new ActorId("myActorId"));
ActorProxyBase.create(MyActor.class, new ActorId(1234));
```

<span data-ttu-id="7eb9a-188">Ao usar GUIDs/UUIDs e cadeias de caracteres, os valores são codificados em hash para um Int64.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-188">When you're using GUIDs/UUIDs and strings, the values are hashed to an Int64.</span></span> <span data-ttu-id="7eb9a-189">No entanto, ao fornecer explicitamente um Int64 para uma `ActorId`, o Int64 será mapeado diretamente para uma partição sem hash adicional.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-189">However, when you're explicitly providing an Int64 to an `ActorId`, the Int64 will map directly to a partition without further hashing.</span></span> <span data-ttu-id="7eb9a-190">Você pode usar essa técnica para controlar em qual partição os atores serão colocados.</span><span class="sxs-lookup"><span data-stu-id="7eb9a-190">You can use this technique to control which partition the actors are placed in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7eb9a-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7eb9a-191">Next steps</span></span>
* [<span data-ttu-id="7eb9a-192">Gerenciamento de estado do ator</span><span class="sxs-lookup"><span data-stu-id="7eb9a-192">Actor state management</span></span>](service-fabric-reliable-actors-state-management.md)
* [<span data-ttu-id="7eb9a-193">Ciclo de vida do ator e coleta de lixo</span><span class="sxs-lookup"><span data-stu-id="7eb9a-193">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="7eb9a-194">Documentação de referência da API dos Atores</span><span class="sxs-lookup"><span data-stu-id="7eb9a-194">Actors API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="7eb9a-195">Código de exemplo do .NET</span><span class="sxs-lookup"><span data-stu-id="7eb9a-195">.NET sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="7eb9a-196">Código de exemplo de Java</span><span class="sxs-lookup"><span data-stu-id="7eb9a-196">Java sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
