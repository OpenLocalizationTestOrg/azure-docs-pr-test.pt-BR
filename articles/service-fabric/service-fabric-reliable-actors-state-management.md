---
title: gerenciamento de estado de atores aaaReliable | Microsoft Docs
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
ms.openlocfilehash: 346d92426b1890617d108a9504afb179e463bded
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-state-management"></a><span data-ttu-id="f4885-103">Gerenciamento de estado dos Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="f4885-103">Reliable Actors state management</span></span>
<span data-ttu-id="f4885-104">Reliable Actors são objetos single-threaded que podem encapsular a lógica e o estado.</span><span class="sxs-lookup"><span data-stu-id="f4885-104">Reliable Actors are single-threaded objects that can encapsulate both logic and state.</span></span> <span data-ttu-id="f4885-105">Como os atores são executados em serviços confiáveis, podem manter o estado confiável usando Olá os mesmos mecanismos de persistência e replicação que usa serviços confiáveis.</span><span class="sxs-lookup"><span data-stu-id="f4885-105">Because actors run on Reliable Services, they can maintain state reliably by using hello same persistence and replication mechanisms that Reliable Services uses.</span></span> <span data-ttu-id="f4885-106">Dessa forma, os atores não percam o seu estado após falhas, após a reativação após a coleta de lixo, ou quando eles são movidos entre nós em um cluster de conclusão tooresource balanceamento ou atualizações ao redor.</span><span class="sxs-lookup"><span data-stu-id="f4885-106">This way, actors don't lose their state after failures, upon reactivation after garbage collection, or when they are moved around between nodes in a cluster due tooresource balancing or upgrades.</span></span>

## <a name="state-persistence-and-replication"></a><span data-ttu-id="f4885-107">Replicação e persistência de estado</span><span class="sxs-lookup"><span data-stu-id="f4885-107">State persistence and replication</span></span>
<span data-ttu-id="f4885-108">Todos os atores confiável são considerados *com monitoração de estado* porque cada instância de ator mapeia ID tooa exclusiva.</span><span class="sxs-lookup"><span data-stu-id="f4885-108">All Reliable Actors are considered *stateful* because each actor instance maps tooa unique ID.</span></span> <span data-ttu-id="f4885-109">Isso significa que toohello repetidas chamadas mesma ID de ator são roteadas toohello mesma instância de ator.</span><span class="sxs-lookup"><span data-stu-id="f4885-109">This means that repeated calls toohello same actor ID are routed toohello same actor instance.</span></span> <span data-ttu-id="f4885-110">Em um sistema sem monitoração de estado, por outro lado, chamadas de cliente não têm garantia de toohello toobe roteada mesmo servidor de cada vez.</span><span class="sxs-lookup"><span data-stu-id="f4885-110">In a stateless system, by contrast, client calls are not guaranteed toobe routed toohello same server every time.</span></span> <span data-ttu-id="f4885-111">Por esse motivo, os serviços de ator são sempre serviços com estado.</span><span class="sxs-lookup"><span data-stu-id="f4885-111">For this reason, actor services are always stateful services.</span></span>

<span data-ttu-id="f4885-112">Mesmo que os atores sejam considerados com estado, isso não significa que eles devem armazenar o estado de modo confiável.</span><span class="sxs-lookup"><span data-stu-id="f4885-112">Even though actors are considered stateful, that does not mean they must store state reliably.</span></span> <span data-ttu-id="f4885-113">Atores podem escolher o nível de saudação de persistência de estado e a replicação com base em seus dados, requisitos de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="f4885-113">Actors can choose hello level of state persistence and replication based on their data storage requirements:</span></span>

* <span data-ttu-id="f4885-114">**Estado persistente**: estado é toodisk persistente e é replicada too3 ou mais réplicas.</span><span class="sxs-lookup"><span data-stu-id="f4885-114">**Persisted state**: State is persisted toodisk and is replicated too3 or more replicas.</span></span> <span data-ttu-id="f4885-115">Isso é mais durável opção de armazenamento de estado hello, onde o estado pode persistir por meio de interrupção de conclusão de cluster.</span><span class="sxs-lookup"><span data-stu-id="f4885-115">This is hello most durable state storage option, where state can persist through complete cluster outage.</span></span>
* <span data-ttu-id="f4885-116">**Estado volátil**: estado é replicado too3 ou mais réplicas e mantido somente na memória.</span><span class="sxs-lookup"><span data-stu-id="f4885-116">**Volatile state**: State is replicated too3 or more replicas and only kept in memory.</span></span> <span data-ttu-id="f4885-117">Isso proporciona resiliência contra falhas de nó e de ator, e durante atualizações e balanceamento de recursos.</span><span class="sxs-lookup"><span data-stu-id="f4885-117">This provides resilience against node failure and actor failure, and during upgrades and resource balancing.</span></span> <span data-ttu-id="f4885-118">No entanto, o estado não é persistente toodisk.</span><span class="sxs-lookup"><span data-stu-id="f4885-118">However, state is not persisted toodisk.</span></span> <span data-ttu-id="f4885-119">Se todas as réplicas sejam perdidas ao mesmo tempo, o estado de saudação é perdido também.</span><span class="sxs-lookup"><span data-stu-id="f4885-119">So if all replicas are lost at once, hello state is lost as well.</span></span>
* <span data-ttu-id="f4885-120">**Nenhum estado persistente**: estado não foi replicado ou gravado toodisk.</span><span class="sxs-lookup"><span data-stu-id="f4885-120">**No persisted state**: State is not replicated or written toodisk.</span></span> <span data-ttu-id="f4885-121">Esse nível é para os atores que não basta toomaintain estado confiável.</span><span class="sxs-lookup"><span data-stu-id="f4885-121">This level is for actors that simply don't need toomaintain state reliably.</span></span>

<span data-ttu-id="f4885-122">Cada nível de persistência é apenas um *provedor de estado* e uma configuração de *replicação* diferentes do serviço.</span><span class="sxs-lookup"><span data-stu-id="f4885-122">Each level of persistence is simply a different *state provider* and *replication* configuration of your service.</span></span> <span data-ttu-id="f4885-123">Se o estado é gravado ou não toodisk depende do provedor de estado hello – componente Olá em um serviço confiável que armazena o estado.</span><span class="sxs-lookup"><span data-stu-id="f4885-123">Whether or not state is written toodisk depends on hello state provider--hello component in a reliable service that stores state.</span></span> <span data-ttu-id="f4885-124">A replicação depende de quantas réplicas são implantadas com um serviço.</span><span class="sxs-lookup"><span data-stu-id="f4885-124">Replication depends on how many replicas a service is deployed with.</span></span> <span data-ttu-id="f4885-125">Assim como acontece com serviços confiáveis, ambos Olá provedor de estado e contagem de réplica pode ser facilmente definida manualmente.</span><span class="sxs-lookup"><span data-stu-id="f4885-125">As with Reliable Services, both hello state provider and replica count can easily be set manually.</span></span> <span data-ttu-id="f4885-126">a estrutura de ator Olá fornece um atributo que, quando usada em um ator, seleciona automaticamente um provedor de estado padrão e gera automaticamente as configurações de réplica contagem tooachieve uma destas três configurações de persistência.</span><span class="sxs-lookup"><span data-stu-id="f4885-126">hello actor framework provides an attribute that, when used on an actor, automatically selects a default state provider and automatically generates settings for replica count tooachieve one of these three persistence settings.</span></span> <span data-ttu-id="f4885-127">atributo StatePersistence de saudação não será herdado pela classe derivada, cada tipo de ator deve fornecer seu nível de StatePersistence.</span><span class="sxs-lookup"><span data-stu-id="f4885-127">hello StatePersistence attribute is not inherited by derived class, each Actor type must provide its StatePersistence level.</span></span>

### <a name="persisted-state"></a><span data-ttu-id="f4885-128">Estado persistente</span><span class="sxs-lookup"><span data-stu-id="f4885-128">Persisted state</span></span>
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
<span data-ttu-id="f4885-129">Essa configuração usa um provedor de estado que armazena dados em disco e define automaticamente Olá too3 de contagem de réplica de serviço.</span><span class="sxs-lookup"><span data-stu-id="f4885-129">This setting uses a state provider that stores data on disk and automatically sets hello service replica count too3.</span></span>

### <a name="volatile-state"></a><span data-ttu-id="f4885-130">Estado volátil</span><span class="sxs-lookup"><span data-stu-id="f4885-130">Volatile state</span></span>
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
<span data-ttu-id="f4885-131">Essa configuração usa um provedor de estado na memória-somente e conjuntos de Olá too3 de contagem de réplica.</span><span class="sxs-lookup"><span data-stu-id="f4885-131">This setting uses an in-memory-only state provider and sets hello replica count too3.</span></span>

### <a name="no-persisted-state"></a><span data-ttu-id="f4885-132">Nenhum estado persistente</span><span class="sxs-lookup"><span data-stu-id="f4885-132">No persisted state</span></span>
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
<span data-ttu-id="f4885-133">Essa configuração usa um provedor de estado na memória-somente e conjuntos de Olá too1 de contagem de réplica.</span><span class="sxs-lookup"><span data-stu-id="f4885-133">This setting uses an in-memory-only state provider and sets hello replica count too1.</span></span>

### <a name="defaults-and-generated-settings"></a><span data-ttu-id="f4885-134">Padrões e configurações geradas</span><span class="sxs-lookup"><span data-stu-id="f4885-134">Defaults and generated settings</span></span>
<span data-ttu-id="f4885-135">Quando você estiver usando Olá `StatePersistence` atributo, um provedor de estado é selecionado automaticamente para você em tempo de execução quando o serviço de ator Olá é iniciado.</span><span class="sxs-lookup"><span data-stu-id="f4885-135">When you're using hello `StatePersistence` attribute, a state provider is automatically selected for you at runtime when hello actor service starts.</span></span> <span data-ttu-id="f4885-136">Contagem de réplicas Hello, no entanto, é definida em tempo de compilação por Olá ator do Visual Studio ferramentas de compilação.</span><span class="sxs-lookup"><span data-stu-id="f4885-136">hello replica count, however, is set at compile time by hello Visual Studio actor build tools.</span></span> <span data-ttu-id="f4885-137">Olá ferramentas de compilação geram automaticamente um *serviço padrão* para serviço de ator Olá applicationmanifest.XML.</span><span class="sxs-lookup"><span data-stu-id="f4885-137">hello build tools automatically generate a *default service* for hello actor service in ApplicationManifest.xml.</span></span> <span data-ttu-id="f4885-138">Os parâmetros são criados para **tamanho mín. do conjunto de réplicas** e **tamanho de destino do conjunto de réplicas**.</span><span class="sxs-lookup"><span data-stu-id="f4885-138">Parameters are created for **min replica set size** and **target replica set size**.</span></span>

<span data-ttu-id="f4885-139">Você pode alterar esses parâmetros manualmente.</span><span class="sxs-lookup"><span data-stu-id="f4885-139">You can change these parameters manually.</span></span> <span data-ttu-id="f4885-140">Saudação de cada vez, mas `StatePersistence` atributo é alterado, os parâmetros de saudação são definidos valores de tamanho de conjunto toohello padrão réplica para Olá selecionado `StatePersistence` atributo, substituindo qualquer valor anterior.</span><span class="sxs-lookup"><span data-stu-id="f4885-140">But each time hello `StatePersistence` attribute is changed, hello parameters are set toohello default replica set size values for hello selected `StatePersistence` attribute, overriding any previous values.</span></span> <span data-ttu-id="f4885-141">Em outras palavras, os valores hello definidos em ServiceManifest.xml são *somente* substituído em tempo de compilação quando você altera Olá `StatePersistence` valor do atributo.</span><span class="sxs-lookup"><span data-stu-id="f4885-141">In other words, hello values that you set in ServiceManifest.xml are *only* overridden at build time when you change hello `StatePersistence` attribute value.</span></span>

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

## <a name="state-manager"></a><span data-ttu-id="f4885-142">Gerenciador de estado</span><span class="sxs-lookup"><span data-stu-id="f4885-142">State manager</span></span>
<span data-ttu-id="f4885-143">Cada instância de ator tem seu próprio gerenciador de estado: uma estrutura de dados semelhante a um dicionário que armazena pares chave-valor de forma confiável.</span><span class="sxs-lookup"><span data-stu-id="f4885-143">Every actor instance has its own state manager: a dictionary-like data structure that reliably stores key/value pairs.</span></span> <span data-ttu-id="f4885-144">Gerenciador de estado de saudação é um wrapper em torno de um provedor de estado.</span><span class="sxs-lookup"><span data-stu-id="f4885-144">hello state manager is a wrapper around a state provider.</span></span> <span data-ttu-id="f4885-145">Você pode usá-lo toostore dados independentemente de qual configuração de persistência é usada.</span><span class="sxs-lookup"><span data-stu-id="f4885-145">You can use it toostore data regardless of which persistence setting is used.</span></span> <span data-ttu-id="f4885-146">Ele não fornece nenhuma garantia de que um serviço de ator em execução pode ser alterado de um tooa de configuração de estado volátil (na memória-somente) persistentes configuração de estado por meio de uma atualização sem interrupção enquanto preserva os dados.</span><span class="sxs-lookup"><span data-stu-id="f4885-146">It does not provide any guarantees that a running actor service can be changed from a volatile (in-memory-only) state setting tooa persisted state setting through a rolling upgrade while preserving data.</span></span> <span data-ttu-id="f4885-147">No entanto, é possível toochange contagem da réplica para um serviço em execução.</span><span class="sxs-lookup"><span data-stu-id="f4885-147">However, it is possible toochange replica count for a running service.</span></span>

<span data-ttu-id="f4885-148">As chaves do gerenciador de estado devem ser cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="f4885-148">State manager keys must be strings.</span></span> <span data-ttu-id="f4885-149">Os valores são genéricos e podem ser de qualquer tipo, incluindo tipos personalizados.</span><span class="sxs-lookup"><span data-stu-id="f4885-149">Values are generic and can be any type, including custom types.</span></span> <span data-ttu-id="f4885-150">Os valores armazenados no Gerenciador de estado de saudação devem ser serializável de contrato de dados porque eles podem ser transmitidos através de nós da saudação rede tooother durante a replicação e podem ser gravados toodisk, dependendo da configuração de persistência de estado de um ator.</span><span class="sxs-lookup"><span data-stu-id="f4885-150">Values stored in hello state manager must be data contract serializable because they might be transmitted over hello network tooother nodes during replication and might be written toodisk, depending on an actor's state persistence setting.</span></span>

<span data-ttu-id="f4885-151">Gerenciador de estado Olá expõe métodos comuns de dicionário de estado de gerenciamento, semelhante toothose encontrado no dicionário confiável.</span><span class="sxs-lookup"><span data-stu-id="f4885-151">hello state manager exposes common dictionary methods for managing state, similar toothose found in Reliable Dictionary.</span></span>

### <a name="accessing-state"></a><span data-ttu-id="f4885-152">Acessando o estado</span><span class="sxs-lookup"><span data-stu-id="f4885-152">Accessing state</span></span>
<span data-ttu-id="f4885-153">Estado pode ser acessado por meio do Gerenciador de estado Olá por chave.</span><span class="sxs-lookup"><span data-stu-id="f4885-153">State can be accessed through hello state manager by key.</span></span> <span data-ttu-id="f4885-154">Os métodos do gerenciador de estado são todos assíncronos, pois podem exigir E/S de disco quando os atores têm um estado persistente.</span><span class="sxs-lookup"><span data-stu-id="f4885-154">State manager methods are all asynchronous because they might require disk I/O when actors have persisted state.</span></span> <span data-ttu-id="f4885-155">No primeiro acesso, os objetos de estado são armazenados em cache na memória.</span><span class="sxs-lookup"><span data-stu-id="f4885-155">Upon first access, state objects are cached in memory.</span></span> <span data-ttu-id="f4885-156">As operações de acesso repetidas acessam os objetos diretamente da memória e são retornadas de forma síncrona sem incorrer em E/S de disco ou sobrecarga de troca de contexto assíncrona.</span><span class="sxs-lookup"><span data-stu-id="f4885-156">Repeat access operations access objects directly from memory and return synchronously without incurring disk I/O or asynchronous context-switching overhead.</span></span> <span data-ttu-id="f4885-157">Um objeto de estado é removido do cache de saudação em Olá casos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f4885-157">A state object is removed from hello cache in hello following cases:</span></span>

* <span data-ttu-id="f4885-158">Um método de ator lança uma exceção sem tratamento depois de recuperar um objeto do Gerenciador de estado de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4885-158">An actor method throws an unhandled exception after it retrieves an object from hello state manager.</span></span>
* <span data-ttu-id="f4885-159">Um ator é reativado depois de ser desativado ou depois de uma falha.</span><span class="sxs-lookup"><span data-stu-id="f4885-159">An actor is reactivated, either after being deactivated or after failure.</span></span>
* <span data-ttu-id="f4885-160">páginas de provedor de estado de saudação do estado toodisk.</span><span class="sxs-lookup"><span data-stu-id="f4885-160">hello state provider pages state toodisk.</span></span> <span data-ttu-id="f4885-161">Esse comportamento depende da implementação de provedor de estado de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4885-161">This behavior depends on hello state provider implementation.</span></span> <span data-ttu-id="f4885-162">provedor de estado de padrão de saudação para Olá `Persisted` configuração tem esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="f4885-162">hello default state provider for hello `Persisted` setting has this behavior.</span></span>

<span data-ttu-id="f4885-163">Você pode recuperar o estado usando um padrão *obter* operação gera `KeyNotFoundException`(c#) ou `NoSuchElementException`(Java) se não existir uma entrada para a chave de saudação:</span><span class="sxs-lookup"><span data-stu-id="f4885-163">You can retrieve state by using a standard *Get* operation that throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) if an entry does not exist for hello key:</span></span>

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

<span data-ttu-id="f4885-164">O estado também pode ser recuperado usando um método *TryGet* que não gera exceção, caso não exista uma entrada para uma chave:</span><span class="sxs-lookup"><span data-stu-id="f4885-164">You can also retrieve state by using a *TryGet* method that does not throw if an entry does not exist for a key:</span></span>

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

### <a name="saving-state"></a><span data-ttu-id="f4885-165">Salvando o estado</span><span class="sxs-lookup"><span data-stu-id="f4885-165">Saving state</span></span>
<span data-ttu-id="f4885-166">métodos de recuperação do Gerenciador de estado de saudação retornam um objeto de tooan de referência na memória local.</span><span class="sxs-lookup"><span data-stu-id="f4885-166">hello state manager retrieval methods return a reference tooan object in local memory.</span></span> <span data-ttu-id="f4885-167">Modificar esse objeto na memória local sozinho não faz com que ele toobe salvo permanentemente.</span><span class="sxs-lookup"><span data-stu-id="f4885-167">Modifying this object in local memory alone does not cause it toobe saved durably.</span></span> <span data-ttu-id="f4885-168">Quando um objeto é recuperado do Gerenciador de estado hello e modificado, ele deve ser reinserido Olá toobe de Gerenciador de estado salvo permanentemente.</span><span class="sxs-lookup"><span data-stu-id="f4885-168">When an object is retrieved from hello state manager and modified, it must be reinserted into hello state manager toobe saved durably.</span></span>

<span data-ttu-id="f4885-169">Você pode inserir o estado usando um incondicional *definir*, que é Olá equivalente de saudação `dictionary["key"] = value` sintaxe:</span><span class="sxs-lookup"><span data-stu-id="f4885-169">You can insert state by using an unconditional *Set*, which is hello equivalent of hello `dictionary["key"] = value` syntax:</span></span>

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

<span data-ttu-id="f4885-170">Você pode adicionar estado usando um método *Add*.</span><span class="sxs-lookup"><span data-stu-id="f4885-170">You can add state by using an *Add* method.</span></span> <span data-ttu-id="f4885-171">Este método lança `InvalidOperationException`(c#) ou `IllegalStateException`(Java) quando ele tenta tooadd uma chave que já existe.</span><span class="sxs-lookup"><span data-stu-id="f4885-171">This method throws `InvalidOperationException`(C#) or `IllegalStateException`(Java) when it tries tooadd a key that already exists.</span></span>

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

<span data-ttu-id="f4885-172">Você também pode adicionar estado usando um método *TryAdd*.</span><span class="sxs-lookup"><span data-stu-id="f4885-172">You can also add state by using a *TryAdd* method.</span></span> <span data-ttu-id="f4885-173">Esse método não lançará quando ele tenta tooadd uma chave que já existe.</span><span class="sxs-lookup"><span data-stu-id="f4885-173">This method does not throw when it tries tooadd a key that already exists.</span></span>

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

<span data-ttu-id="f4885-174">No final de saudação de um método de ator, o Gerenciador de estado de saudação salva automaticamente quaisquer valores que foram adicionados ou modificados por uma operação de inserção ou atualização.</span><span class="sxs-lookup"><span data-stu-id="f4885-174">At hello end of an actor method, hello state manager automatically saves any values that have been added or modified by an insert or update operation.</span></span> <span data-ttu-id="f4885-175">"Salvar" pode incluir toodisk persistente e replicação, dependendo das configurações de saudação usado.</span><span class="sxs-lookup"><span data-stu-id="f4885-175">A "save" can include persisting toodisk and replication, depending on hello settings used.</span></span> <span data-ttu-id="f4885-176">Valores que não foram modificados não serão persistentes nem replicados.</span><span class="sxs-lookup"><span data-stu-id="f4885-176">Values that have not been modified are not persisted or replicated.</span></span> <span data-ttu-id="f4885-177">Se nenhum valor tiver sido modificado, Olá operação de salvamento não fará nada.</span><span class="sxs-lookup"><span data-stu-id="f4885-177">If no values have been modified, hello save operation does nothing.</span></span> <span data-ttu-id="f4885-178">Se salvar falhas, hello estado modificado será descartado e estado original Olá é recarregado.</span><span class="sxs-lookup"><span data-stu-id="f4885-178">If saving fails, hello modified state is discarded and hello original state is reloaded.</span></span>

<span data-ttu-id="f4885-179">Você também pode salvar estado manualmente pela chamada hello `SaveStateAsync` método na base de ator hello:</span><span class="sxs-lookup"><span data-stu-id="f4885-179">You can also save state manually by calling hello `SaveStateAsync` method on hello actor base:</span></span>

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

### <a name="removing-state"></a><span data-ttu-id="f4885-180">Removendo o estado</span><span class="sxs-lookup"><span data-stu-id="f4885-180">Removing state</span></span>
<span data-ttu-id="f4885-181">Você pode remover estado permanentemente do Gerenciador de estado de um ator Olá chamada *remover* método.</span><span class="sxs-lookup"><span data-stu-id="f4885-181">You can remove state permanently from an actor's state manager by calling hello *Remove* method.</span></span> <span data-ttu-id="f4885-182">Este método lança `KeyNotFoundException`(c#) ou `NoSuchElementException`(Java) quando ele tenta tooremove uma chave que não existe.</span><span class="sxs-lookup"><span data-stu-id="f4885-182">This method throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) when it tries tooremove a key that doesn't exist.</span></span>

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

<span data-ttu-id="f4885-183">Você também pode remover estado permanentemente usando Olá *TryRemove* método.</span><span class="sxs-lookup"><span data-stu-id="f4885-183">You can also remove state permanently by using hello *TryRemove* method.</span></span> <span data-ttu-id="f4885-184">Esse método não lançará quando ele tenta tooremove uma chave que não existe.</span><span class="sxs-lookup"><span data-stu-id="f4885-184">This method does not throw when it tries tooremove a key that does not exist.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f4885-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f4885-185">Next steps</span></span>

<span data-ttu-id="f4885-186">Estado que é armazenado no Reliable Actors deve ser serializado antes de sua toodisk escrito e replicado para alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="f4885-186">State that's stored in Reliable Actors must be serialized before its written toodisk and replicated for high availability.</span></span> <span data-ttu-id="f4885-187">Saiba mais sobre a [Serialização de tipo de ator](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="f4885-187">Learn more about [Actor type serialization](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span>

<span data-ttu-id="f4885-188">Em seguida, saiba mais sobre [Diagnóstico e monitoramento de desempenho do ator](service-fabric-reliable-actors-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="f4885-188">Next, learn more about [Actor diagnostics and performance monitoring](service-fabric-reliable-actors-diagnostics.md).</span></span>
