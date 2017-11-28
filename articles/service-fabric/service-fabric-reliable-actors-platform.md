---
title: "aaaReliable atores na malha do serviço | Microsoft Docs"
description: "Descreve como confiável atores são colocadas em camadas em serviços confiáveis e usar recursos de saudação da plataforma do Service Fabric hello."
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
ms.openlocfilehash: ecffb54139f1171c7839b77fed0be60950881198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-reliable-actors-use-hello-service-fabric-platform"></a><span data-ttu-id="5e82a-103">Como Reliable Actors usar plataforma do Service Fabric Olá</span><span class="sxs-lookup"><span data-stu-id="5e82a-103">How Reliable Actors use hello Service Fabric platform</span></span>
<span data-ttu-id="5e82a-104">Este artigo explica como Reliable Actors funcionam na plataforma do Azure Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="5e82a-104">This article explains how Reliable Actors work on hello Azure Service Fabric platform.</span></span> <span data-ttu-id="5e82a-105">Atores confiáveis é executado em uma estrutura que é hospedada em uma implementação de um serviço confiável com monitoração de estado chamado hello *serviço de ator*.</span><span class="sxs-lookup"><span data-stu-id="5e82a-105">Reliable Actors run in a framework that is hosted in an implementation of a stateful reliable service called hello *actor service*.</span></span> <span data-ttu-id="5e82a-106">serviço de ator Olá contém todos os ciclo de vida do hello componentes necessários toomanage hello e despacho de seus agentes de mensagens:</span><span class="sxs-lookup"><span data-stu-id="5e82a-106">hello actor service contains all hello components necessary toomanage hello lifecycle and message dispatching for your actors:</span></span>

* <span data-ttu-id="5e82a-107">saudação de tempo de execução de ator gerencia o ciclo de vida, coleta de lixo e impõe o acesso de thread único.</span><span class="sxs-lookup"><span data-stu-id="5e82a-107">hello Actor Runtime manages lifecycle, garbage collection, and enforces single-threaded access.</span></span>
* <span data-ttu-id="5e82a-108">Um ouvinte de comunicação remota do serviço de ator aceita tooactors de chamadas de acesso remoto e as envia instância do tooa dispatcher tooroute toohello ator apropriado.</span><span class="sxs-lookup"><span data-stu-id="5e82a-108">An actor service remoting listener accepts remote access calls tooactors and sends them tooa dispatcher tooroute toohello appropriate actor instance.</span></span>
* <span data-ttu-id="5e82a-109">Olá provedor de estado de ator encapsula os provedores de estado (como o provedor de estado de coleções confiável Olá) e fornece um adaptador para o gerenciamento de estado de ator.</span><span class="sxs-lookup"><span data-stu-id="5e82a-109">hello Actor State Provider wraps state providers (such as hello Reliable Collections state provider) and provides an adapter for actor state management.</span></span>

<span data-ttu-id="5e82a-110">Estrutura de Reliable Actor esses componentes formulário juntos hello.</span><span class="sxs-lookup"><span data-stu-id="5e82a-110">These components together form hello Reliable Actor framework.</span></span>

## <a name="service-layering"></a><span data-ttu-id="5e82a-111">Disposição em camadas de serviço</span><span class="sxs-lookup"><span data-stu-id="5e82a-111">Service layering</span></span>
<span data-ttu-id="5e82a-112">Como o próprio serviço de ator Olá é um serviço confiável, todos os Olá [modelo de aplicativo](service-fabric-application-model.md), ciclo de vida, [empacotamento](service-fabric-package-apps.md), [implantação](service-fabric-deploy-remove-applications.md), atualizar e dimensionamento de conceitos de Serviços confiáveis aplicam Olá serviços de tooactor do mesmo modo.</span><span class="sxs-lookup"><span data-stu-id="5e82a-112">Because hello actor service itself is a reliable service, all hello [application model](service-fabric-application-model.md), lifecycle, [packaging](service-fabric-package-apps.md), [deployment](service-fabric-deploy-remove-applications.md), upgrade, and scaling concepts of Reliable Services apply hello same way tooactor services.</span></span> 

![Disposição em camadas do serviço de ator][1]

<span data-ttu-id="5e82a-114">Olá, diagrama anterior mostra Olá relação entre as estruturas de aplicativo do Service Fabric hello e código do usuário.</span><span class="sxs-lookup"><span data-stu-id="5e82a-114">hello preceding diagram shows hello relationship between hello Service Fabric application frameworks and user code.</span></span> <span data-ttu-id="5e82a-115">Elementos azuis representam a estrutura de aplicativo de serviços confiáveis hello, laranja representa a estrutura de Reliable Actor hello e verde representa o código do usuário.</span><span class="sxs-lookup"><span data-stu-id="5e82a-115">Blue elements represent hello Reliable Services application framework, orange represents hello Reliable Actor framework, and green represents user code.</span></span>

<span data-ttu-id="5e82a-116">Em serviços confiáveis, o serviço herda Olá `StatefulService` classe.</span><span class="sxs-lookup"><span data-stu-id="5e82a-116">In Reliable Services, your service inherits hello `StatefulService` class.</span></span> <span data-ttu-id="5e82a-117">Essa classe é derivada de `StatefulServiceBase` (ou `StatelessService` para serviços sem estado).</span><span class="sxs-lookup"><span data-stu-id="5e82a-117">This class is itself derived from `StatefulServiceBase` (or `StatelessService` for stateless services).</span></span> <span data-ttu-id="5e82a-118">Atores confiável, você usa o serviço de ator hello.</span><span class="sxs-lookup"><span data-stu-id="5e82a-118">In Reliable Actors, you use hello actor service.</span></span> <span data-ttu-id="5e82a-119">serviço de ator Olá é uma implementação diferente da saudação `StatefulServiceBase` classe esse padrão de ator implementa Olá onde seus atores executam.</span><span class="sxs-lookup"><span data-stu-id="5e82a-119">hello actor service is a different implementation of hello `StatefulServiceBase` class that implements hello actor pattern where your actors run.</span></span> <span data-ttu-id="5e82a-120">Porque o próprio serviço de ator Olá é apenas uma implementação de `StatefulServiceBase`, você pode escrever seu próprio serviço que deriva de `ActorService` e implementar recursos de nível de serviço Olá mesma maneira que faria ao herdar `StatefulService`, como:</span><span class="sxs-lookup"><span data-stu-id="5e82a-120">Because hello actor service itself is just an implementation of `StatefulServiceBase`, you can write your own service that derives from `ActorService` and implement service-level features hello same way you would when inheriting `StatefulService`, such as:</span></span>

* <span data-ttu-id="5e82a-121">Backup e restauração do serviço.</span><span class="sxs-lookup"><span data-stu-id="5e82a-121">Service backup and restore.</span></span>
* <span data-ttu-id="5e82a-122">Funcionalidade compartilhada para todos os atores, por exemplo, um disjuntor.</span><span class="sxs-lookup"><span data-stu-id="5e82a-122">Shared functionality for all actors, for example, a circuit breaker.</span></span>
* <span data-ttu-id="5e82a-123">Chamadas de procedimento remoto no próprio serviço de ator hello e em cada ator individual.</span><span class="sxs-lookup"><span data-stu-id="5e82a-123">Remote procedure calls on hello actor service itself and on each individual actor.</span></span>

> [!NOTE]
> <span data-ttu-id="5e82a-124">Atualmente não há suporte para os serviços com estado no Java/Linux.</span><span class="sxs-lookup"><span data-stu-id="5e82a-124">Stateful services are not currently supported in Java/Linux.</span></span>

### <a name="using-hello-actor-service"></a><span data-ttu-id="5e82a-125">Usando o serviço de ator Olá</span><span class="sxs-lookup"><span data-stu-id="5e82a-125">Using hello actor service</span></span>
<span data-ttu-id="5e82a-126">Instâncias de ator têm o serviço de ator toohello de acesso no qual eles estão em execução.</span><span class="sxs-lookup"><span data-stu-id="5e82a-126">Actor instances have access toohello actor service in which they are running.</span></span> <span data-ttu-id="5e82a-127">Por meio do serviço de ator Olá, instâncias de ator programaticamente podem obter o contexto de serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="5e82a-127">Through hello actor service, actor instances can programmatically obtain hello service context.</span></span> <span data-ttu-id="5e82a-128">contexto do serviço Olá possui ID de partição Olá, nome do serviço, nome do aplicativo e outras informações de específico da plataforma do Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="5e82a-128">hello service context has hello partition ID, service name, application name, and other Service Fabric platform-specific information:</span></span>

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


<span data-ttu-id="5e82a-129">Como todos os serviços confiável, o serviço de ator Olá deve ser registrado com um tipo de serviço em tempo de execução do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="5e82a-129">Like all Reliable Services, hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="5e82a-130">Para saudação do serviço de ator toorun suas instâncias de ator, seu tipo de ator também deve ser registrado com o serviço de ator hello.</span><span class="sxs-lookup"><span data-stu-id="5e82a-130">For hello actor service toorun your actor instances, your actor type must also be registered with hello actor service.</span></span> <span data-ttu-id="5e82a-131">Olá `ActorRuntime` método de registro executa essa tarefa para atores.</span><span class="sxs-lookup"><span data-stu-id="5e82a-131">hello `ActorRuntime` registration method performs this work for actors.</span></span> <span data-ttu-id="5e82a-132">No caso mais simples de saudação, assim, você pode registrar o tipo de ator e implicitamente será usado o serviço de ator Olá com as configurações padrão:</span><span class="sxs-lookup"><span data-stu-id="5e82a-132">In hello simplest case, you can just register your actor type, and hello actor service with default settings will implicitly be used:</span></span>

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

<span data-ttu-id="5e82a-133">Como alternativa, você pode usar uma expressão lambda fornecida pelo serviço de ator do hello registro método tooconstruct hello.</span><span class="sxs-lookup"><span data-stu-id="5e82a-133">Alternatively, you can use a lambda provided by hello registration method tooconstruct hello actor service yourself.</span></span> <span data-ttu-id="5e82a-134">Você pode configurar o serviço de ator hello e construir explicitamente suas instâncias de ator, onde você pode injetar ator de tooyour dependências por meio de seu construtor:</span><span class="sxs-lookup"><span data-stu-id="5e82a-134">You can then configure hello actor service and explicitly construct your actor instances, where you can inject dependencies tooyour actor through its constructor:</span></span>

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

### <a name="actor-service-methods"></a><span data-ttu-id="5e82a-135">Métodos do serviço de ator</span><span class="sxs-lookup"><span data-stu-id="5e82a-135">Actor service methods</span></span>
<span data-ttu-id="5e82a-136">Olá implementa do serviço de ator `IActorService` (c#) ou `ActorService` (Java), que por sua vez de implementa `IService` (c#) ou `Service` (Java).</span><span class="sxs-lookup"><span data-stu-id="5e82a-136">hello Actor service implements `IActorService` (C#) or `ActorService` (Java), which in turn implements `IService` (C#) or `Service` (Java).</span></span> <span data-ttu-id="5e82a-137">Isso é usado por serviços confiáveis a comunicação remota, que permite chamadas de procedimento remoto em métodos de serviço de interface de saudação.</span><span class="sxs-lookup"><span data-stu-id="5e82a-137">This is hello interface used by Reliable Services remoting, which allows remote procedure calls on service methods.</span></span> <span data-ttu-id="5e82a-138">Ela contém métodos no nível de serviço que podem ser chamados remotamente por meio da comunicação remota do serviço.</span><span class="sxs-lookup"><span data-stu-id="5e82a-138">It contains service-level methods that can be called remotely via service remoting.</span></span>

#### <a name="enumerating-actors"></a><span data-ttu-id="5e82a-139">Enumerando os atores</span><span class="sxs-lookup"><span data-stu-id="5e82a-139">Enumerating actors</span></span>
<span data-ttu-id="5e82a-140">serviço de ator Olá permite que um cliente tooenumerate metadados sobre atores Olá que está hospedando o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="5e82a-140">hello actor service allows a client tooenumerate metadata about hello actors that hello service is hosting.</span></span> <span data-ttu-id="5e82a-141">Porque Olá ator é um serviço com monitoração de estado particionado, a enumeração é executada por partição.</span><span class="sxs-lookup"><span data-stu-id="5e82a-141">Because hello actor service is a partitioned stateful service, enumeration is performed per partition.</span></span> <span data-ttu-id="5e82a-142">Como cada partição pode conter muitos atores, enumeração Olá é retornada como um conjunto de resultados paginados.</span><span class="sxs-lookup"><span data-stu-id="5e82a-142">Because each partition might contain many actors, hello enumeration is returned as a set of paged results.</span></span> <span data-ttu-id="5e82a-143">páginas de saudação são loop até que todas as páginas são lidas.</span><span class="sxs-lookup"><span data-stu-id="5e82a-143">hello pages are looped over until all pages are read.</span></span> <span data-ttu-id="5e82a-144">Olá mostrado no exemplo a seguir como toocreate uma lista de todos os atores ativas em uma partição de um serviço de ator:</span><span class="sxs-lookup"><span data-stu-id="5e82a-144">hello following example shows how toocreate a list of all active actors in one partition of an actor service:</span></span>

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

#### <a name="deleting-actors"></a><span data-ttu-id="5e82a-145">Excluindo atores</span><span class="sxs-lookup"><span data-stu-id="5e82a-145">Deleting actors</span></span>
<span data-ttu-id="5e82a-146">serviço de ator Olá também fornece uma função para a exclusão de atores:</span><span class="sxs-lookup"><span data-stu-id="5e82a-146">hello actor service also provides a function for deleting actors:</span></span>

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

<span data-ttu-id="5e82a-147">Para obter mais informações sobre como excluir atores e seu estado, consulte Olá [documentação do ciclo de vida de ator](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="5e82a-147">For more information on deleting actors and their state, see hello [actor lifecycle documentation](service-fabric-reliable-actors-lifecycle.md).</span></span>

### <a name="custom-actor-service"></a><span data-ttu-id="5e82a-148">Serviço de ator personalizado</span><span class="sxs-lookup"><span data-stu-id="5e82a-148">Custom actor service</span></span>
<span data-ttu-id="5e82a-149">Usando lambda de registro de ator hello, você pode registrar seu próprio serviço de ator personalizado que deriva de `ActorService` (c#) e `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="5e82a-149">By using hello actor registration lambda, you can register your own custom actor service that derives from `ActorService` (C#) and `FabricActorService` (Java).</span></span> <span data-ttu-id="5e82a-150">Neste serviço de ator personalizado, você pode implementar sua própria funcionalidade de nível de serviço, escrevendo uma classe de serviço que herda `ActorService` (C#) ou `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="5e82a-150">In this custom actor service, you can implement your own service-level functionality by writing a service class that inherits `ActorService` (C#) or `FabricActorService` (Java).</span></span> <span data-ttu-id="5e82a-151">Um serviço de ator personalizada herda todas as funcionalidades de tempo de execução de ator saudação do `ActorService` (c#) ou `FabricActorService` (Java) e pode ser usado tooimplement seus próprios métodos de serviço.</span><span class="sxs-lookup"><span data-stu-id="5e82a-151">A custom actor service inherits all hello actor runtime functionality from `ActorService` (C#) or `FabricActorService` (Java) and can be used tooimplement your own service methods.</span></span>

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

#### <a name="implementing-actor-backup-and-restore"></a><span data-ttu-id="5e82a-152">Implementando o backup e a restauração de ator</span><span class="sxs-lookup"><span data-stu-id="5e82a-152">Implementing actor backup and restore</span></span>
 <span data-ttu-id="5e82a-153">Em Olá exemplo a seguir, serviço de ator personalizado Olá expõe tooback um método os dados de ator, aproveitando o ouvinte de comunicação remota Olá já está presente no `ActorService`:</span><span class="sxs-lookup"><span data-stu-id="5e82a-153">In hello following example, hello custom actor service exposes a method tooback up actor data by taking advantage of hello remoting listener already present in `ActorService`:</span></span>

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
           // store hello contents of backupInfo.Directory
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
           // store hello contents of backupInfo.Directory
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


<span data-ttu-id="5e82a-154">Neste exemplo, o `IMyActorService` é um contrato de comunicação remota que implementa `IService` (C#) e `Service` (Java) e que, em seguida, é implementado por `MyActorService`.</span><span class="sxs-lookup"><span data-stu-id="5e82a-154">In this example, `IMyActorService` is a remoting contract that implements `IService` (C#) and `Service` (Java), and is then implemented by `MyActorService`.</span></span> <span data-ttu-id="5e82a-155">Adicionando este contrato de comunicação remota, métodos em `IMyActorService` agora também estão disponíveis tooa cliente, criando um proxy de comunicação remota por meio de `ActorServiceProxy`:</span><span class="sxs-lookup"><span data-stu-id="5e82a-155">By adding this remoting contract, methods on `IMyActorService` are now also available tooa client by creating a remoting proxy via `ActorServiceProxy`:</span></span>

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

## <a name="application-model"></a><span data-ttu-id="5e82a-156">Modelo de aplicativo</span><span class="sxs-lookup"><span data-stu-id="5e82a-156">Application model</span></span>
<span data-ttu-id="5e82a-157">Ator serviços são confiáveis, para que o modelo de aplicativo hello é Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="5e82a-157">Actor services are Reliable Services, so hello application model is hello same.</span></span> <span data-ttu-id="5e82a-158">No entanto, ferramentas de compilação do framework de ator Olá geram alguns dos arquivos de modelo de aplicativo hello para você.</span><span class="sxs-lookup"><span data-stu-id="5e82a-158">However, hello actor framework build tools generate some of hello application model files for you.</span></span>

### <a name="service-manifest"></a><span data-ttu-id="5e82a-159">Manifesto do serviço</span><span class="sxs-lookup"><span data-stu-id="5e82a-159">Service manifest</span></span>
<span data-ttu-id="5e82a-160">ferramentas de compilação do framework de ator Olá geram automaticamente o conteúdo de saudação do arquivo de ServiceManifest.xml do seu serviço de ator.</span><span class="sxs-lookup"><span data-stu-id="5e82a-160">hello actor framework build tools automatically generate hello contents of your actor service's ServiceManifest.xml file.</span></span> <span data-ttu-id="5e82a-161">Este arquivo inclui:</span><span class="sxs-lookup"><span data-stu-id="5e82a-161">This file includes:</span></span>

* <span data-ttu-id="5e82a-162">O tipo de serviço de ator.</span><span class="sxs-lookup"><span data-stu-id="5e82a-162">Actor service type.</span></span> <span data-ttu-id="5e82a-163">nome do tipo Hello é gerado com base no nome do projeto do ator.</span><span class="sxs-lookup"><span data-stu-id="5e82a-163">hello type name is generated based on your actor's project name.</span></span> <span data-ttu-id="5e82a-164">Com base no atributo de persistência de saudação em seu ator, Olá HasPersistedState sinalizador também será definido adequadamente.</span><span class="sxs-lookup"><span data-stu-id="5e82a-164">Based on hello persistence attribute on your actor, hello HasPersistedState flag is also set accordingly.</span></span>
* <span data-ttu-id="5e82a-165">Pacote de códigos.</span><span class="sxs-lookup"><span data-stu-id="5e82a-165">Code package.</span></span>
* <span data-ttu-id="5e82a-166">Pacote de configuração.</span><span class="sxs-lookup"><span data-stu-id="5e82a-166">Config package.</span></span>
* <span data-ttu-id="5e82a-167">Recursos e pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="5e82a-167">Resources and endpoints.</span></span>

### <a name="application-manifest"></a><span data-ttu-id="5e82a-168">Manifesto do aplicativo</span><span class="sxs-lookup"><span data-stu-id="5e82a-168">Application manifest</span></span>
<span data-ttu-id="5e82a-169">ferramentas de compilação do framework de ator Olá criam automaticamente uma definição de serviço padrão para o serviço de ator.</span><span class="sxs-lookup"><span data-stu-id="5e82a-169">hello actor framework build tools automatically create a default service definition for your actor service.</span></span> <span data-ttu-id="5e82a-170">ferramentas de compilação Olá preenchem propriedades do serviço de saudação padrão:</span><span class="sxs-lookup"><span data-stu-id="5e82a-170">hello build tools populate hello default service properties:</span></span>

* <span data-ttu-id="5e82a-171">Contagem de conjunto de réplicas é determinada pelo atributo de persistência de saudação em seu ator.</span><span class="sxs-lookup"><span data-stu-id="5e82a-171">Replica set count is determined by hello persistence attribute on your actor.</span></span> <span data-ttu-id="5e82a-172">Cada atributo de persistência de saudação de tempo em seu ator é alterado, contagem de conjunto de réplica Olá na definição de serviço padrão Olá é redefinida adequadamente.</span><span class="sxs-lookup"><span data-stu-id="5e82a-172">Each time hello persistence attribute on your actor is changed, hello replica set count in hello default service definition is reset accordingly.</span></span>
* <span data-ttu-id="5e82a-173">Intervalo e o esquema de partição são definidos tooUniform Int64 com intervalo completo de chave de Int64 hello.</span><span class="sxs-lookup"><span data-stu-id="5e82a-173">Partition scheme and range are set tooUniform Int64 with hello full Int64 key range.</span></span>

## <a name="service-fabric-partition-concepts-for-actors"></a><span data-ttu-id="5e82a-174">Conceitos de partição de Malha do Serviço para atores</span><span class="sxs-lookup"><span data-stu-id="5e82a-174">Service Fabric partition concepts for actors</span></span>
<span data-ttu-id="5e82a-175">Serviços de ator são serviços com estado particionados.</span><span class="sxs-lookup"><span data-stu-id="5e82a-175">Actor services are partitioned stateful services.</span></span> <span data-ttu-id="5e82a-176">Cada partição de um serviço de ator contém um conjunto de atores.</span><span class="sxs-lookup"><span data-stu-id="5e82a-176">Each partition of an actor service contains a set of actors.</span></span> <span data-ttu-id="5e82a-177">As partições de serviço são distribuídas automaticamente em vários nós no Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5e82a-177">Service partitions are automatically distributed over multiple nodes in Service Fabric.</span></span> <span data-ttu-id="5e82a-178">As instâncias de ator são distribuídas como resultado disso.</span><span class="sxs-lookup"><span data-stu-id="5e82a-178">Actor instances are distributed as a result.</span></span>

![Particionamento e distribuição de ator][5]

<span data-ttu-id="5e82a-180">Os Reliable Services podem ser criados com esquemas de partição diferentes e intervalos de chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="5e82a-180">Reliable Services can be created with different partition schemes and partition key ranges.</span></span> <span data-ttu-id="5e82a-181">serviço de ator Olá usa o esquema de particionamento Olá Int64 com hello completo Int64 intervalo de chave toomap atores toopartitions.</span><span class="sxs-lookup"><span data-stu-id="5e82a-181">hello actor service uses hello Int64 partitioning scheme with hello full Int64 key range toomap actors toopartitions.</span></span>

### <a name="actor-id"></a><span data-ttu-id="5e82a-182">ID de ator</span><span class="sxs-lookup"><span data-stu-id="5e82a-182">Actor ID</span></span>
<span data-ttu-id="5e82a-183">Cada ator que é criado no serviço de saudação tem uma ID exclusiva associada a ele, representado pelo Olá `ActorId` classe.</span><span class="sxs-lookup"><span data-stu-id="5e82a-183">Each actor that's created in hello service has a unique ID associated with it, represented by hello `ActorId` class.</span></span> <span data-ttu-id="5e82a-184">`ActorId`é um valor de ID opaco que pode ser usado para distribuição uniforme de atores em partições de serviço Olá gerando IDs aleatórias:</span><span class="sxs-lookup"><span data-stu-id="5e82a-184">`ActorId` is an opaque ID value that can be used for uniform distribution of actors across hello service partitions by generating random IDs:</span></span>

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


<span data-ttu-id="5e82a-185">Cada `ActorId` é tooan hash Int64.</span><span class="sxs-lookup"><span data-stu-id="5e82a-185">Every `ActorId` is hashed tooan Int64.</span></span> <span data-ttu-id="5e82a-186">Este é o motivo pelo qual o serviço de ator Olá deve usar um esquema de particionamento Int64 com intervalo completo de chave de Int64 hello.</span><span class="sxs-lookup"><span data-stu-id="5e82a-186">This is why hello actor service must use an Int64 partitioning scheme with hello full Int64 key range.</span></span> <span data-ttu-id="5e82a-187">No entanto, valores de ID personalizados podem ser usados para uma `ActorID`, incluindo GUIDs/UUIDs, cadeias de caracteres e Int64s.</span><span class="sxs-lookup"><span data-stu-id="5e82a-187">However, custom ID values can be used for an `ActorID`, including GUIDs/UUIDs, strings, and Int64s.</span></span>

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

<span data-ttu-id="5e82a-188">Quando você estiver usando o GUID/UUIDs e cadeias de caracteres, valores de saudação são hash tooan Int64.</span><span class="sxs-lookup"><span data-stu-id="5e82a-188">When you're using GUIDs/UUIDs and strings, hello values are hashed tooan Int64.</span></span> <span data-ttu-id="5e82a-189">No entanto, quando você está explicitamente fornecendo um tooan Int64 `ActorId`, Olá Int64 mapeará diretamente tooa partição sem hash adicional.</span><span class="sxs-lookup"><span data-stu-id="5e82a-189">However, when you're explicitly providing an Int64 tooan `ActorId`, hello Int64 will map directly tooa partition without further hashing.</span></span> <span data-ttu-id="5e82a-190">Você pode usar este toocontrol técnica que atores de saudação de partição são colocados em.</span><span class="sxs-lookup"><span data-stu-id="5e82a-190">You can use this technique toocontrol which partition hello actors are placed in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e82a-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5e82a-191">Next steps</span></span>
* [<span data-ttu-id="5e82a-192">Gerenciamento de estado do ator</span><span class="sxs-lookup"><span data-stu-id="5e82a-192">Actor state management</span></span>](service-fabric-reliable-actors-state-management.md)
* [<span data-ttu-id="5e82a-193">Ciclo de vida do ator e coleta de lixo</span><span class="sxs-lookup"><span data-stu-id="5e82a-193">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="5e82a-194">Documentação de referência da API dos Atores</span><span class="sxs-lookup"><span data-stu-id="5e82a-194">Actors API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="5e82a-195">Código de exemplo do .NET</span><span class="sxs-lookup"><span data-stu-id="5e82a-195">.NET sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="5e82a-196">Código de exemplo de Java</span><span class="sxs-lookup"><span data-stu-id="5e82a-196">Java sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
