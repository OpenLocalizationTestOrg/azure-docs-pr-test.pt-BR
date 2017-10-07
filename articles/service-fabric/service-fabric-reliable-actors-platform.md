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
# <a name="how-reliable-actors-use-hello-service-fabric-platform"></a>Como Reliable Actors usar plataforma do Service Fabric Olá
Este artigo explica como Reliable Actors funcionam na plataforma do Azure Service Fabric hello. Atores confiáveis é executado em uma estrutura que é hospedada em uma implementação de um serviço confiável com monitoração de estado chamado hello *serviço de ator*. serviço de ator Olá contém todos os ciclo de vida do hello componentes necessários toomanage hello e despacho de seus agentes de mensagens:

* saudação de tempo de execução de ator gerencia o ciclo de vida, coleta de lixo e impõe o acesso de thread único.
* Um ouvinte de comunicação remota do serviço de ator aceita tooactors de chamadas de acesso remoto e as envia instância do tooa dispatcher tooroute toohello ator apropriado.
* Olá provedor de estado de ator encapsula os provedores de estado (como o provedor de estado de coleções confiável Olá) e fornece um adaptador para o gerenciamento de estado de ator.

Estrutura de Reliable Actor esses componentes formulário juntos hello.

## <a name="service-layering"></a>Disposição em camadas de serviço
Como o próprio serviço de ator Olá é um serviço confiável, todos os Olá [modelo de aplicativo](service-fabric-application-model.md), ciclo de vida, [empacotamento](service-fabric-package-apps.md), [implantação](service-fabric-deploy-remove-applications.md), atualizar e dimensionamento de conceitos de Serviços confiáveis aplicam Olá serviços de tooactor do mesmo modo. 

![Disposição em camadas do serviço de ator][1]

Olá, diagrama anterior mostra Olá relação entre as estruturas de aplicativo do Service Fabric hello e código do usuário. Elementos azuis representam a estrutura de aplicativo de serviços confiáveis hello, laranja representa a estrutura de Reliable Actor hello e verde representa o código do usuário.

Em serviços confiáveis, o serviço herda Olá `StatefulService` classe. Essa classe é derivada de `StatefulServiceBase` (ou `StatelessService` para serviços sem estado). Atores confiável, você usa o serviço de ator hello. serviço de ator Olá é uma implementação diferente da saudação `StatefulServiceBase` classe esse padrão de ator implementa Olá onde seus atores executam. Porque o próprio serviço de ator Olá é apenas uma implementação de `StatefulServiceBase`, você pode escrever seu próprio serviço que deriva de `ActorService` e implementar recursos de nível de serviço Olá mesma maneira que faria ao herdar `StatefulService`, como:

* Backup e restauração do serviço.
* Funcionalidade compartilhada para todos os atores, por exemplo, um disjuntor.
* Chamadas de procedimento remoto no próprio serviço de ator hello e em cada ator individual.

> [!NOTE]
> Atualmente não há suporte para os serviços com estado no Java/Linux.

### <a name="using-hello-actor-service"></a>Usando o serviço de ator Olá
Instâncias de ator têm o serviço de ator toohello de acesso no qual eles estão em execução. Por meio do serviço de ator Olá, instâncias de ator programaticamente podem obter o contexto de serviço de saudação. contexto do serviço Olá possui ID de partição Olá, nome do serviço, nome do aplicativo e outras informações de específico da plataforma do Service Fabric:

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


Como todos os serviços confiável, o serviço de ator Olá deve ser registrado com um tipo de serviço em tempo de execução do Service Fabric hello. Para saudação do serviço de ator toorun suas instâncias de ator, seu tipo de ator também deve ser registrado com o serviço de ator hello. Olá `ActorRuntime` método de registro executa essa tarefa para atores. No caso mais simples de saudação, assim, você pode registrar o tipo de ator e implicitamente será usado o serviço de ator Olá com as configurações padrão:

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

Como alternativa, você pode usar uma expressão lambda fornecida pelo serviço de ator do hello registro método tooconstruct hello. Você pode configurar o serviço de ator hello e construir explicitamente suas instâncias de ator, onde você pode injetar ator de tooyour dependências por meio de seu construtor:

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

### <a name="actor-service-methods"></a>Métodos do serviço de ator
Olá implementa do serviço de ator `IActorService` (c#) ou `ActorService` (Java), que por sua vez de implementa `IService` (c#) ou `Service` (Java). Isso é usado por serviços confiáveis a comunicação remota, que permite chamadas de procedimento remoto em métodos de serviço de interface de saudação. Ela contém métodos no nível de serviço que podem ser chamados remotamente por meio da comunicação remota do serviço.

#### <a name="enumerating-actors"></a>Enumerando os atores
serviço de ator Olá permite que um cliente tooenumerate metadados sobre atores Olá que está hospedando o serviço de saudação. Porque Olá ator é um serviço com monitoração de estado particionado, a enumeração é executada por partição. Como cada partição pode conter muitos atores, enumeração Olá é retornada como um conjunto de resultados paginados. páginas de saudação são loop até que todas as páginas são lidas. Olá mostrado no exemplo a seguir como toocreate uma lista de todos os atores ativas em uma partição de um serviço de ator:

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

#### <a name="deleting-actors"></a>Excluindo atores
serviço de ator Olá também fornece uma função para a exclusão de atores:

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

Para obter mais informações sobre como excluir atores e seu estado, consulte Olá [documentação do ciclo de vida de ator](service-fabric-reliable-actors-lifecycle.md).

### <a name="custom-actor-service"></a>Serviço de ator personalizado
Usando lambda de registro de ator hello, você pode registrar seu próprio serviço de ator personalizado que deriva de `ActorService` (c#) e `FabricActorService` (Java). Neste serviço de ator personalizado, você pode implementar sua própria funcionalidade de nível de serviço, escrevendo uma classe de serviço que herda `ActorService` (C#) ou `FabricActorService` (Java). Um serviço de ator personalizada herda todas as funcionalidades de tempo de execução de ator saudação do `ActorService` (c#) ou `FabricActorService` (Java) e pode ser usado tooimplement seus próprios métodos de serviço.

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

#### <a name="implementing-actor-backup-and-restore"></a>Implementando o backup e a restauração de ator
 Em Olá exemplo a seguir, serviço de ator personalizado Olá expõe tooback um método os dados de ator, aproveitando o ouvinte de comunicação remota Olá já está presente no `ActorService`:

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


Neste exemplo, o `IMyActorService` é um contrato de comunicação remota que implementa `IService` (C#) e `Service` (Java) e que, em seguida, é implementado por `MyActorService`. Adicionando este contrato de comunicação remota, métodos em `IMyActorService` agora também estão disponíveis tooa cliente, criando um proxy de comunicação remota por meio de `ActorServiceProxy`:

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

## <a name="application-model"></a>Modelo de aplicativo
Ator serviços são confiáveis, para que o modelo de aplicativo hello é Olá mesmo. No entanto, ferramentas de compilação do framework de ator Olá geram alguns dos arquivos de modelo de aplicativo hello para você.

### <a name="service-manifest"></a>Manifesto do serviço
ferramentas de compilação do framework de ator Olá geram automaticamente o conteúdo de saudação do arquivo de ServiceManifest.xml do seu serviço de ator. Este arquivo inclui:

* O tipo de serviço de ator. nome do tipo Hello é gerado com base no nome do projeto do ator. Com base no atributo de persistência de saudação em seu ator, Olá HasPersistedState sinalizador também será definido adequadamente.
* Pacote de códigos.
* Pacote de configuração.
* Recursos e pontos de extremidade.

### <a name="application-manifest"></a>Manifesto do aplicativo
ferramentas de compilação do framework de ator Olá criam automaticamente uma definição de serviço padrão para o serviço de ator. ferramentas de compilação Olá preenchem propriedades do serviço de saudação padrão:

* Contagem de conjunto de réplicas é determinada pelo atributo de persistência de saudação em seu ator. Cada atributo de persistência de saudação de tempo em seu ator é alterado, contagem de conjunto de réplica Olá na definição de serviço padrão Olá é redefinida adequadamente.
* Intervalo e o esquema de partição são definidos tooUniform Int64 com intervalo completo de chave de Int64 hello.

## <a name="service-fabric-partition-concepts-for-actors"></a>Conceitos de partição de Malha do Serviço para atores
Serviços de ator são serviços com estado particionados. Cada partição de um serviço de ator contém um conjunto de atores. As partições de serviço são distribuídas automaticamente em vários nós no Service Fabric. As instâncias de ator são distribuídas como resultado disso.

![Particionamento e distribuição de ator][5]

Os Reliable Services podem ser criados com esquemas de partição diferentes e intervalos de chaves de partição. serviço de ator Olá usa o esquema de particionamento Olá Int64 com hello completo Int64 intervalo de chave toomap atores toopartitions.

### <a name="actor-id"></a>ID de ator
Cada ator que é criado no serviço de saudação tem uma ID exclusiva associada a ele, representado pelo Olá `ActorId` classe. `ActorId`é um valor de ID opaco que pode ser usado para distribuição uniforme de atores em partições de serviço Olá gerando IDs aleatórias:

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


Cada `ActorId` é tooan hash Int64. Este é o motivo pelo qual o serviço de ator Olá deve usar um esquema de particionamento Int64 com intervalo completo de chave de Int64 hello. No entanto, valores de ID personalizados podem ser usados para uma `ActorID`, incluindo GUIDs/UUIDs, cadeias de caracteres e Int64s.

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

Quando você estiver usando o GUID/UUIDs e cadeias de caracteres, valores de saudação são hash tooan Int64. No entanto, quando você está explicitamente fornecendo um tooan Int64 `ActorId`, Olá Int64 mapeará diretamente tooa partição sem hash adicional. Você pode usar este toocontrol técnica que atores de saudação de partição são colocados em.

## <a name="next-steps"></a>Próximas etapas
* [Gerenciamento de estado do ator](service-fabric-reliable-actors-state-management.md)
* [Ciclo de vida do ator e coleta de lixo](service-fabric-reliable-actors-lifecycle.md)
* [Documentação de referência da API dos Atores](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Código de exemplo do .NET](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Código de exemplo de Java](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
