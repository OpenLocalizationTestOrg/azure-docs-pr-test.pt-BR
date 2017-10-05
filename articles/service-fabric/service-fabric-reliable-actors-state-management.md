---
title: Gerenciamento de estado dos Reliable Actors | Microsoft Docs
description: "Descreve como o estado dos Reliable Actors é gerenciado, persistido e replicado para alta disponibilidade."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 37cf466a-5293-44c0-a4e0-037e5d292214
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: aca8cf2b94e8b746a5cac6af021c7221a29b7345
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-actors-state-management"></a><span data-ttu-id="5f771-103">Gerenciamento de estado dos Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="5f771-103">Reliable Actors state management</span></span>
<span data-ttu-id="5f771-104">Reliable Actors são objetos single-threaded que podem encapsular a lógica e o estado.</span><span class="sxs-lookup"><span data-stu-id="5f771-104">Reliable Actors are single-threaded objects that can encapsulate both logic and state.</span></span> <span data-ttu-id="5f771-105">Como os atores são executados nos Reliable Services, eles podem manter o estado de modo confiável usando os mesmos mecanismos de persistência e replicação usados pelos Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="5f771-105">Because actors run on Reliable Services, they can maintain state reliably by using the same persistence and replication mechanisms that Reliable Services uses.</span></span> <span data-ttu-id="5f771-106">Dessa forma, os atores não perdem seu estado após falhas, na reativação após a coleta de lixo ou quando são movidos entre nós em um cluster devido ao balanceamento de recursos ou às atualizações.</span><span class="sxs-lookup"><span data-stu-id="5f771-106">This way, actors don't lose their state after failures, upon reactivation after garbage collection, or when they are moved around between nodes in a cluster due to resource balancing or upgrades.</span></span>

## <a name="state-persistence-and-replication"></a><span data-ttu-id="5f771-107">Replicação e persistência de estado</span><span class="sxs-lookup"><span data-stu-id="5f771-107">State persistence and replication</span></span>
<span data-ttu-id="5f771-108">Todos os Reliable Actors são considerados *com estado* , pois cada instância de ator é mapeada para uma ID exclusiva.</span><span class="sxs-lookup"><span data-stu-id="5f771-108">All Reliable Actors are considered *stateful* because each actor instance maps to a unique ID.</span></span> <span data-ttu-id="5f771-109">Isso significa que as chamadas repetidas para a mesma ID de ator são encaminhadas para a mesma instância de ator.</span><span class="sxs-lookup"><span data-stu-id="5f771-109">This means that repeated calls to the same actor ID are routed to the same actor instance.</span></span> <span data-ttu-id="5f771-110">Em um sistema sem estado, por outro lado, as chamadas de cliente não têm garantia de serem encaminhadas sempre para o mesmo servidor.</span><span class="sxs-lookup"><span data-stu-id="5f771-110">In a stateless system, by contrast, client calls are not guaranteed to be routed to the same server every time.</span></span> <span data-ttu-id="5f771-111">Por esse motivo, os serviços de ator são sempre serviços com estado.</span><span class="sxs-lookup"><span data-stu-id="5f771-111">For this reason, actor services are always stateful services.</span></span>

<span data-ttu-id="5f771-112">Mesmo que os atores sejam considerados com estado, isso não significa que eles devem armazenar o estado de modo confiável.</span><span class="sxs-lookup"><span data-stu-id="5f771-112">Even though actors are considered stateful, that does not mean they must store state reliably.</span></span> <span data-ttu-id="5f771-113">Os atores podem escolher o nível de persistência de estado e replicação com base em seus requisitos de armazenamento de dados:</span><span class="sxs-lookup"><span data-stu-id="5f771-113">Actors can choose the level of state persistence and replication based on their data storage requirements:</span></span>

* <span data-ttu-id="5f771-114">**Estado persistente:** o estado é persistido em disco e replicado para três ou mais réplicas.</span><span class="sxs-lookup"><span data-stu-id="5f771-114">**Persisted state**: State is persisted to disk and is replicated to 3 or more replicas.</span></span> <span data-ttu-id="5f771-115">Essa é a opção de armazenamento de estado mais duradoura, na qual o estado pode persistir após a interrupção completa do cluster.</span><span class="sxs-lookup"><span data-stu-id="5f771-115">This is the most durable state storage option, where state can persist through complete cluster outage.</span></span>
* <span data-ttu-id="5f771-116">**Estado volátil:** o estado é replicado para três ou mais réplicas e mantido apenas na memória.</span><span class="sxs-lookup"><span data-stu-id="5f771-116">**Volatile state**: State is replicated to 3 or more replicas and only kept in memory.</span></span> <span data-ttu-id="5f771-117">Isso proporciona resiliência contra falhas de nó e de ator, e durante atualizações e balanceamento de recursos.</span><span class="sxs-lookup"><span data-stu-id="5f771-117">This provides resilience against node failure and actor failure, and during upgrades and resource balancing.</span></span> <span data-ttu-id="5f771-118">No entanto, o estado não é persistido no disco.</span><span class="sxs-lookup"><span data-stu-id="5f771-118">However, state is not persisted to disk.</span></span> <span data-ttu-id="5f771-119">Portanto, se todas as réplicas forem perdidas ao mesmo tempo, o estado também será perdido.</span><span class="sxs-lookup"><span data-stu-id="5f771-119">So if all replicas are lost at once, the state is lost as well.</span></span>
* <span data-ttu-id="5f771-120">**Nenhum estado persistente:** o estado não é replicado nem é gravado em disco.</span><span class="sxs-lookup"><span data-stu-id="5f771-120">**No persisted state**: State is not replicated or written to disk.</span></span> <span data-ttu-id="5f771-121">Esse nível é para atores que simplesmente não precisam manter o estado de modo confiável.</span><span class="sxs-lookup"><span data-stu-id="5f771-121">This level is for actors that simply don't need to maintain state reliably.</span></span>

<span data-ttu-id="5f771-122">Cada nível de persistência é apenas um *provedor de estado* e uma configuração de *replicação* diferentes do serviço.</span><span class="sxs-lookup"><span data-stu-id="5f771-122">Each level of persistence is simply a different *state provider* and *replication* configuration of your service.</span></span> <span data-ttu-id="5f771-123">A decisão de gravar ou não o estado em disco depende do provedor de estado – o componente que armazena o estado em um serviço confiável.</span><span class="sxs-lookup"><span data-stu-id="5f771-123">Whether or not state is written to disk depends on the state provider--the component in a reliable service that stores state.</span></span> <span data-ttu-id="5f771-124">A replicação depende de quantas réplicas são implantadas com um serviço.</span><span class="sxs-lookup"><span data-stu-id="5f771-124">Replication depends on how many replicas a service is deployed with.</span></span> <span data-ttu-id="5f771-125">Assim como acontece com os Reliable Services, o provedor de estado e a contagem de réplicas podem ser definidos manualmente com facilidade.</span><span class="sxs-lookup"><span data-stu-id="5f771-125">As with Reliable Services, both the state provider and replica count can easily be set manually.</span></span> <span data-ttu-id="5f771-126">A estrutura de ator fornece um atributo, que, quando usado em um ator, seleciona automaticamente um provedor de estado padrão e gera automaticamente as configurações de contagem de réplicas, a fim de alcançar uma dessas três configurações de persistência.</span><span class="sxs-lookup"><span data-stu-id="5f771-126">The actor framework provides an attribute that, when used on an actor, automatically selects a default state provider and automatically generates settings for replica count to achieve one of these three persistence settings.</span></span> <span data-ttu-id="5f771-127">O atributo StatePersistence não será herdado pela classe derivada. Cada tipo de Ator deve fornecer seu nível de StatePersistence.</span><span class="sxs-lookup"><span data-stu-id="5f771-127">The StatePersistence attribute is not inherited by derived class, each Actor type must provide its StatePersistence level.</span></span>

### <a name="persisted-state"></a><span data-ttu-id="5f771-128">Estado persistente</span><span class="sxs-lookup"><span data-stu-id="5f771-128">Persisted state</span></span>
```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl  extends FabricActor implements MyActor
{
}
```  
<span data-ttu-id="5f771-129">Essa configuração usa um provedor de estado que armazena dados em disco e define automaticamente a contagem de réplicas do serviço como 3.</span><span class="sxs-lookup"><span data-stu-id="5f771-129">This setting uses a state provider that stores data on disk and automatically sets the service replica count to 3.</span></span>

### <a name="volatile-state"></a><span data-ttu-id="5f771-130">Estado volátil</span><span class="sxs-lookup"><span data-stu-id="5f771-130">Volatile state</span></span>
```csharp
[StatePersistence(StatePersistence.Volatile)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Volatile)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
<span data-ttu-id="5f771-131">Essa configuração usa um provedor de estado somente na memória e define a contagem de réplicas como 3.</span><span class="sxs-lookup"><span data-stu-id="5f771-131">This setting uses an in-memory-only state provider and sets the replica count to 3.</span></span>

### <a name="no-persisted-state"></a><span data-ttu-id="5f771-132">Nenhum estado persistente</span><span class="sxs-lookup"><span data-stu-id="5f771-132">No persisted state</span></span>
```csharp
[StatePersistence(StatePersistence.None)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.None)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
<span data-ttu-id="5f771-133">Essa configuração usa um provedor de estado somente na memória e define a contagem de réplicas como 1.</span><span class="sxs-lookup"><span data-stu-id="5f771-133">This setting uses an in-memory-only state provider and sets the replica count to 1.</span></span>

### <a name="defaults-and-generated-settings"></a><span data-ttu-id="5f771-134">Padrões e configurações geradas</span><span class="sxs-lookup"><span data-stu-id="5f771-134">Defaults and generated settings</span></span>
<span data-ttu-id="5f771-135">Ao usar o atributo `StatePersistence`, um provedor de estado será selecionado automaticamente para você em tempo de execução quando o serviço de ator for iniciado.</span><span class="sxs-lookup"><span data-stu-id="5f771-135">When you're using the `StatePersistence` attribute, a state provider is automatically selected for you at runtime when the actor service starts.</span></span> <span data-ttu-id="5f771-136">No entanto, a contagem de réplicas é definida no tempo de compilação pelas ferramentas de build de ator do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5f771-136">The replica count, however, is set at compile time by the Visual Studio actor build tools.</span></span> <span data-ttu-id="5f771-137">As ferramentas de build geram automaticamente um *serviço padrão* para o serviço de ator no ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="5f771-137">The build tools automatically generate a *default service* for the actor service in ApplicationManifest.xml.</span></span> <span data-ttu-id="5f771-138">Os parâmetros são criados para **tamanho mín. do conjunto de réplicas** e **tamanho de destino do conjunto de réplicas**.</span><span class="sxs-lookup"><span data-stu-id="5f771-138">Parameters are created for **min replica set size** and **target replica set size**.</span></span>

<span data-ttu-id="5f771-139">Você pode alterar esses parâmetros manualmente.</span><span class="sxs-lookup"><span data-stu-id="5f771-139">You can change these parameters manually.</span></span> <span data-ttu-id="5f771-140">Mas, sempre que o atributo `StatePersistence` for alterado, os parâmetros serão definidos como os valores padrão de tamanho do conjunto de réplicas para o atributo `StatePersistence` selecionado, substituindo os valores anteriores.</span><span class="sxs-lookup"><span data-stu-id="5f771-140">But each time the `StatePersistence` attribute is changed, the parameters are set to the default replica set size values for the selected `StatePersistence` attribute, overriding any previous values.</span></span> <span data-ttu-id="5f771-141">Em outras palavras, os valores definidos em ServiceManifest.xml serão substituídos *somente* no momento do build quando você alterar o valor do atributo `StatePersistence`.</span><span class="sxs-lookup"><span data-stu-id="5f771-141">In other words, the values that you set in ServiceManifest.xml are *only* overridden at build time when you change the `StatePersistence` attribute value.</span></span>

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application12Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="MyActorService_PartitionCount" DefaultValue="10" />
      <Parameter Name="MyActorService_MinReplicaSetSize" DefaultValue="3" />
      <Parameter Name="MyActorService_TargetReplicaSetSize" DefaultValue="3" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyActorPkg" ServiceManifestVersion="1.0.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MyActorService" GeneratedIdRef="77d965dc-85fb-488c-bd06-c6c1fe29d593|Persisted">
         <StatefulService ServiceTypeName="MyActorServiceType" TargetReplicaSetSize="[MyActorService_TargetReplicaSetSize]" MinReplicaSetSize="[MyActorService_MinReplicaSetSize]">
            <UniformInt64Partition PartitionCount="[MyActorService_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
         </StatefulService>
      </Service>
   </DefaultServices>
</ApplicationManifest>
```

## <a name="state-manager"></a><span data-ttu-id="5f771-142">Gerenciador de estado</span><span class="sxs-lookup"><span data-stu-id="5f771-142">State manager</span></span>
<span data-ttu-id="5f771-143">Cada instância de ator tem seu próprio gerenciador de estado: uma estrutura de dados semelhante a um dicionário que armazena pares chave-valor de forma confiável.</span><span class="sxs-lookup"><span data-stu-id="5f771-143">Every actor instance has its own state manager: a dictionary-like data structure that reliably stores key/value pairs.</span></span> <span data-ttu-id="5f771-144">O gerenciador de estado é um wrapper em torno de um provedor de estado.</span><span class="sxs-lookup"><span data-stu-id="5f771-144">The state manager is a wrapper around a state provider.</span></span> <span data-ttu-id="5f771-145">Você pode usá-lo para armazenar dados, independentemente da configuração de persistência utilizada.</span><span class="sxs-lookup"><span data-stu-id="5f771-145">You can use it to store data regardless of which persistence setting is used.</span></span> <span data-ttu-id="5f771-146">Ele não dá nenhuma garantia de que um serviço de ator em execução poderá ser alterado de uma configuração de estado volátil (somente na memória) para uma configuração de estado persistente por meio de uma atualização sem interrupção, ao mesmo tempo que preserva os dados.</span><span class="sxs-lookup"><span data-stu-id="5f771-146">It does not provide any guarantees that a running actor service can be changed from a volatile (in-memory-only) state setting to a persisted state setting through a rolling upgrade while preserving data.</span></span> <span data-ttu-id="5f771-147">No entanto, é possível alterar a contagem de réplicas de um serviço em execução.</span><span class="sxs-lookup"><span data-stu-id="5f771-147">However, it is possible to change replica count for a running service.</span></span>

<span data-ttu-id="5f771-148">As chaves do gerenciador de estado devem ser cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="5f771-148">State manager keys must be strings.</span></span> <span data-ttu-id="5f771-149">Os valores são genéricos e podem ser de qualquer tipo, incluindo tipos personalizados.</span><span class="sxs-lookup"><span data-stu-id="5f771-149">Values are generic and can be any type, including custom types.</span></span> <span data-ttu-id="5f771-150">Os valores armazenados no gerenciador de estado devem ser serializáveis pelo contrato de dados, pois poderão ser transmitidos pela rede a outros nós durante a replicação e gravados em disco, dependendo da configuração de persistência de estado de um ator.</span><span class="sxs-lookup"><span data-stu-id="5f771-150">Values stored in the state manager must be data contract serializable because they might be transmitted over the network to other nodes during replication and might be written to disk, depending on an actor's state persistence setting.</span></span>

<span data-ttu-id="5f771-151">O gerenciador de estado expõe métodos comuns de dicionário para o gerenciamento do estado, semelhantes àqueles encontrados no Dicionário Confiável.</span><span class="sxs-lookup"><span data-stu-id="5f771-151">The state manager exposes common dictionary methods for managing state, similar to those found in Reliable Dictionary.</span></span>

### <a name="accessing-state"></a><span data-ttu-id="5f771-152">Acessando o estado</span><span class="sxs-lookup"><span data-stu-id="5f771-152">Accessing state</span></span>
<span data-ttu-id="5f771-153">O estado pode ser acessado por chave por meio do gerenciador de estado.</span><span class="sxs-lookup"><span data-stu-id="5f771-153">State can be accessed through the state manager by key.</span></span> <span data-ttu-id="5f771-154">Os métodos do gerenciador de estado são todos assíncronos, pois podem exigir E/S de disco quando os atores têm um estado persistente.</span><span class="sxs-lookup"><span data-stu-id="5f771-154">State manager methods are all asynchronous because they might require disk I/O when actors have persisted state.</span></span> <span data-ttu-id="5f771-155">No primeiro acesso, os objetos de estado são armazenados em cache na memória.</span><span class="sxs-lookup"><span data-stu-id="5f771-155">Upon first access, state objects are cached in memory.</span></span> <span data-ttu-id="5f771-156">As operações de acesso repetidas acessam os objetos diretamente da memória e são retornadas de forma síncrona sem incorrer em E/S de disco ou sobrecarga de troca de contexto assíncrona.</span><span class="sxs-lookup"><span data-stu-id="5f771-156">Repeat access operations access objects directly from memory and return synchronously without incurring disk I/O or asynchronous context-switching overhead.</span></span> <span data-ttu-id="5f771-157">Um objeto de estado é removido do cache nos seguintes casos:</span><span class="sxs-lookup"><span data-stu-id="5f771-157">A state object is removed from the cache in the following cases:</span></span>

* <span data-ttu-id="5f771-158">Um método de ator gera uma exceção sem tratamento depois de recuperar um objeto do gerenciador de estado.</span><span class="sxs-lookup"><span data-stu-id="5f771-158">An actor method throws an unhandled exception after it retrieves an object from the state manager.</span></span>
* <span data-ttu-id="5f771-159">Um ator é reativado depois de ser desativado ou depois de uma falha.</span><span class="sxs-lookup"><span data-stu-id="5f771-159">An actor is reactivated, either after being deactivated or after failure.</span></span>
* <span data-ttu-id="5f771-160">O provedor de estado efetua a paginação do estado em disco.</span><span class="sxs-lookup"><span data-stu-id="5f771-160">The state provider pages state to disk.</span></span> <span data-ttu-id="5f771-161">Esse comportamento depende da implementação do provedor de estado.</span><span class="sxs-lookup"><span data-stu-id="5f771-161">This behavior depends on the state provider implementation.</span></span> <span data-ttu-id="5f771-162">O provedor de estado padrão para a configuração `Persisted` apresenta esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="5f771-162">The default state provider for the `Persisted` setting has this behavior.</span></span>

<span data-ttu-id="5f771-163">Você poderá recuperar o estado usando uma operação *Get* padrão, que gera `KeyNotFoundException` (C#) ou `NoSuchElementException` (Java) se não existir uma entrada para a chave:</span><span class="sxs-lookup"><span data-stu-id="5f771-163">You can retrieve state by using a standard *Get* operation that throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) if an entry does not exist for the key:</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<int> GetCountAsync()
    {
        return this.StateManager.GetStateAsync<int>("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().getStateAsync("MyState");
    }
}
```

<span data-ttu-id="5f771-164">O estado também pode ser recuperado usando um método *TryGet* que não gera exceção, caso não exista uma entrada para uma chave:</span><span class="sxs-lookup"><span data-stu-id="5f771-164">You can also retrieve state by using a *TryGet* method that does not throw if an entry does not exist for a key:</span></span>

```csharp
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task<int> GetCountAsync()
    {
        ConditionalValue<int> result = await this.StateManager.TryGetStateAsync<int>("MyState");
        if (result.HasValue)
        {
            return result.Value;
        }

        return 0;
    }
}
```
```Java
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().<Integer>tryGetStateAsync("MyState").thenApply(result -> {
            if (result.hasValue()) {
                return result.getValue();
            } else {
                return 0;
            });
    }
}
```

### <a name="saving-state"></a><span data-ttu-id="5f771-165">Salvando o estado</span><span class="sxs-lookup"><span data-stu-id="5f771-165">Saving state</span></span>
<span data-ttu-id="5f771-166">Os métodos de recuperação do gerenciador de estado retornam uma referência a um objeto na memória local.</span><span class="sxs-lookup"><span data-stu-id="5f771-166">The state manager retrieval methods return a reference to an object in local memory.</span></span> <span data-ttu-id="5f771-167">A modificação desse objeto na memória local por si só não faz com que ele seja salvo permanentemente.</span><span class="sxs-lookup"><span data-stu-id="5f771-167">Modifying this object in local memory alone does not cause it to be saved durably.</span></span> <span data-ttu-id="5f771-168">Quando um objeto é recuperado do gerenciador de estado e é modificado, ele deve ser reinserido no gerenciador de estado para ser salvo permanentemente.</span><span class="sxs-lookup"><span data-stu-id="5f771-168">When an object is retrieved from the state manager and modified, it must be reinserted into the state manager to be saved durably.</span></span>

<span data-ttu-id="5f771-169">O estado pode ser inserido usando um *Set* incondicional, que é o equivalente da sintaxe `dictionary["key"] = value`:</span><span class="sxs-lookup"><span data-stu-id="5f771-169">You can insert state by using an unconditional *Set*, which is the equivalent of the `dictionary["key"] = value` syntax:</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task SetCountAsync(int value)
    {
        return this.StateManager.SetStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture setCountAsync(int value)
    {
        return this.stateManager().setStateAsync("MyState", value);
    }
}
```

<span data-ttu-id="5f771-170">Você pode adicionar estado usando um método *Add*.</span><span class="sxs-lookup"><span data-stu-id="5f771-170">You can add state by using an *Add* method.</span></span> <span data-ttu-id="5f771-171">Este método lança `InvalidOperationException` (C#) ou `IllegalStateException` (Java) ao tentar adicionar uma chave que já exista.</span><span class="sxs-lookup"><span data-stu-id="5f771-171">This method throws `InvalidOperationException`(C#) or `IllegalStateException`(Java) when it tries to add a key that already exists.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task AddCountAsync(int value)
    {
        return this.StateManager.AddStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().addOrUpdateStateAsync("MyState", value, (key, old_value) -> old_value + value);
    }
}
```

<span data-ttu-id="5f771-172">Você também pode adicionar estado usando um método *TryAdd*.</span><span class="sxs-lookup"><span data-stu-id="5f771-172">You can also add state by using a *TryAdd* method.</span></span> <span data-ttu-id="5f771-173">Esse método não lançará exceção ao tentar adicionar uma chave que já exista.</span><span class="sxs-lookup"><span data-stu-id="5f771-173">This method does not throw when it tries to add a key that already exists.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task AddCountAsync(int value)
    {
        bool result = await this.StateManager.TryAddStateAsync<int>("MyState", value);

        if (result)
        {
            // Added successfully!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().tryAddStateAsync("MyState", value).thenApply((result)->{
            if(result)
            {
                // Added successfully!
            }
        });
    }
}
```

<span data-ttu-id="5f771-174">No final de um método de ator, o gerenciador de estado salva automaticamente todos os valores que foram adicionados ou modificados por uma operação de inserção ou de atualização.</span><span class="sxs-lookup"><span data-stu-id="5f771-174">At the end of an actor method, the state manager automatically saves any values that have been added or modified by an insert or update operation.</span></span> <span data-ttu-id="5f771-175">A operação “salvar” pode incluir a persistência em disco e a replicação, dependendo das configurações utilizadas.</span><span class="sxs-lookup"><span data-stu-id="5f771-175">A "save" can include persisting to disk and replication, depending on the settings used.</span></span> <span data-ttu-id="5f771-176">Valores que não foram modificados não serão persistentes nem replicados.</span><span class="sxs-lookup"><span data-stu-id="5f771-176">Values that have not been modified are not persisted or replicated.</span></span> <span data-ttu-id="5f771-177">Caso nenhum valor tenha sido modificado, a operação salvar não terá nenhum efeito.</span><span class="sxs-lookup"><span data-stu-id="5f771-177">If no values have been modified, the save operation does nothing.</span></span> <span data-ttu-id="5f771-178">Se houver uma falha na operação salvar, o estado modificado será descartado e o estado original será recarregado.</span><span class="sxs-lookup"><span data-stu-id="5f771-178">If saving fails, the modified state is discarded and the original state is reloaded.</span></span>

<span data-ttu-id="5f771-179">Você também pode salvar o estado manualmente ao chamar o método `SaveStateAsync` na base de ator:</span><span class="sxs-lookup"><span data-stu-id="5f771-179">You can also save state manually by calling the `SaveStateAsync` method on the actor base:</span></span>

```csharp
async Task IMyActor.SetCountAsync(int count)
{
    await this.StateManager.AddOrUpdateStateAsync("count", count, (key, value) => count > value ? count : value);

    await this.SaveStateAsync();
}
```
```Java
interface MyActor {
    CompletableFuture setCountAsync(int count)
    {
        this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value).thenApply();

        this.stateManager().saveStateAsync().thenApply();
    }
}
```

### <a name="removing-state"></a><span data-ttu-id="5f771-180">Removendo o estado</span><span class="sxs-lookup"><span data-stu-id="5f771-180">Removing state</span></span>
<span data-ttu-id="5f771-181">O estado pode ser removido permanentemente do gerenciador de estado de um ator com a chamada do método *Remove*.</span><span class="sxs-lookup"><span data-stu-id="5f771-181">You can remove state permanently from an actor's state manager by calling the *Remove* method.</span></span> <span data-ttu-id="5f771-182">Este método lança `KeyNotFoundException` (C#) ou `NoSuchElementException` (Java) ao tentar remover uma chave que não exista.</span><span class="sxs-lookup"><span data-stu-id="5f771-182">This method throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) when it tries to remove a key that doesn't exist.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task RemoveCountAsync()
    {
        return this.StateManager.RemoveStateAsync("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().removeStateAsync("MyState");
    }
}
```

<span data-ttu-id="5f771-183">Você também pode remover o estado permanentemente usando o método *TryRemove*.</span><span class="sxs-lookup"><span data-stu-id="5f771-183">You can also remove state permanently by using the *TryRemove* method.</span></span> <span data-ttu-id="5f771-184">Esse método não lançará exceção ao tentar remover uma chave que não exista.</span><span class="sxs-lookup"><span data-stu-id="5f771-184">This method does not throw when it tries to remove a key that does not exist.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task RemoveCountAsync()
    {
        bool result = await this.StateManager.TryRemoveStateAsync("MyState");

        if (result)
        {
            // State removed!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().tryRemoveStateAsync("MyState").thenApply((result)->{
            if(result)
            {
                // State removed!
            }
        });
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="5f771-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5f771-185">Next steps</span></span>

<span data-ttu-id="5f771-186">O estado que é armazenado no Reliable Actors deve ser serializado antes de ser gravado no disco e replicado para alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="5f771-186">State that's stored in Reliable Actors must be serialized before its written to disk and replicated for high availability.</span></span> <span data-ttu-id="5f771-187">Saiba mais sobre a [Serialização de tipo de ator](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="5f771-187">Learn more about [Actor type serialization](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span>

<span data-ttu-id="5f771-188">Em seguida, saiba mais sobre [Diagnóstico e monitoramento de desempenho do ator](service-fabric-reliable-actors-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="5f771-188">Next, learn more about [Actor diagnostics and performance monitoring](service-fabric-reliable-actors-diagnostics.md).</span></span>
