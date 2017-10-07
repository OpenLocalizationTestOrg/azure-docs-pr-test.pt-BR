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
# <a name="reliable-actors-state-management"></a>Gerenciamento de estado dos Reliable Actors
Reliable Actors são objetos single-threaded que podem encapsular a lógica e o estado. Como os atores são executados em serviços confiáveis, podem manter o estado confiável usando Olá os mesmos mecanismos de persistência e replicação que usa serviços confiáveis. Dessa forma, os atores não percam o seu estado após falhas, após a reativação após a coleta de lixo, ou quando eles são movidos entre nós em um cluster de conclusão tooresource balanceamento ou atualizações ao redor.

## <a name="state-persistence-and-replication"></a>Replicação e persistência de estado
Todos os atores confiável são considerados *com monitoração de estado* porque cada instância de ator mapeia ID tooa exclusiva. Isso significa que toohello repetidas chamadas mesma ID de ator são roteadas toohello mesma instância de ator. Em um sistema sem monitoração de estado, por outro lado, chamadas de cliente não têm garantia de toohello toobe roteada mesmo servidor de cada vez. Por esse motivo, os serviços de ator são sempre serviços com estado.

Mesmo que os atores sejam considerados com estado, isso não significa que eles devem armazenar o estado de modo confiável. Atores podem escolher o nível de saudação de persistência de estado e a replicação com base em seus dados, requisitos de armazenamento:

* **Estado persistente**: estado é toodisk persistente e é replicada too3 ou mais réplicas. Isso é mais durável opção de armazenamento de estado hello, onde o estado pode persistir por meio de interrupção de conclusão de cluster.
* **Estado volátil**: estado é replicado too3 ou mais réplicas e mantido somente na memória. Isso proporciona resiliência contra falhas de nó e de ator, e durante atualizações e balanceamento de recursos. No entanto, o estado não é persistente toodisk. Se todas as réplicas sejam perdidas ao mesmo tempo, o estado de saudação é perdido também.
* **Nenhum estado persistente**: estado não foi replicado ou gravado toodisk. Esse nível é para os atores que não basta toomaintain estado confiável.

Cada nível de persistência é apenas um *provedor de estado* e uma configuração de *replicação* diferentes do serviço. Se o estado é gravado ou não toodisk depende do provedor de estado hello – componente Olá em um serviço confiável que armazena o estado. A replicação depende de quantas réplicas são implantadas com um serviço. Assim como acontece com serviços confiáveis, ambos Olá provedor de estado e contagem de réplica pode ser facilmente definida manualmente. a estrutura de ator Olá fornece um atributo que, quando usada em um ator, seleciona automaticamente um provedor de estado padrão e gera automaticamente as configurações de réplica contagem tooachieve uma destas três configurações de persistência. atributo StatePersistence de saudação não será herdado pela classe derivada, cada tipo de ator deve fornecer seu nível de StatePersistence.

### <a name="persisted-state"></a>Estado persistente
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
Essa configuração usa um provedor de estado que armazena dados em disco e define automaticamente Olá too3 de contagem de réplica de serviço.

### <a name="volatile-state"></a>Estado volátil
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
Essa configuração usa um provedor de estado na memória-somente e conjuntos de Olá too3 de contagem de réplica.

### <a name="no-persisted-state"></a>Nenhum estado persistente
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
Essa configuração usa um provedor de estado na memória-somente e conjuntos de Olá too1 de contagem de réplica.

### <a name="defaults-and-generated-settings"></a>Padrões e configurações geradas
Quando você estiver usando Olá `StatePersistence` atributo, um provedor de estado é selecionado automaticamente para você em tempo de execução quando o serviço de ator Olá é iniciado. Contagem de réplicas Hello, no entanto, é definida em tempo de compilação por Olá ator do Visual Studio ferramentas de compilação. Olá ferramentas de compilação geram automaticamente um *serviço padrão* para serviço de ator Olá applicationmanifest.XML. Os parâmetros são criados para **tamanho mín. do conjunto de réplicas** e **tamanho de destino do conjunto de réplicas**.

Você pode alterar esses parâmetros manualmente. Saudação de cada vez, mas `StatePersistence` atributo é alterado, os parâmetros de saudação são definidos valores de tamanho de conjunto toohello padrão réplica para Olá selecionado `StatePersistence` atributo, substituindo qualquer valor anterior. Em outras palavras, os valores hello definidos em ServiceManifest.xml são *somente* substituído em tempo de compilação quando você altera Olá `StatePersistence` valor do atributo.

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

## <a name="state-manager"></a>Gerenciador de estado
Cada instância de ator tem seu próprio gerenciador de estado: uma estrutura de dados semelhante a um dicionário que armazena pares chave-valor de forma confiável. Gerenciador de estado de saudação é um wrapper em torno de um provedor de estado. Você pode usá-lo toostore dados independentemente de qual configuração de persistência é usada. Ele não fornece nenhuma garantia de que um serviço de ator em execução pode ser alterado de um tooa de configuração de estado volátil (na memória-somente) persistentes configuração de estado por meio de uma atualização sem interrupção enquanto preserva os dados. No entanto, é possível toochange contagem da réplica para um serviço em execução.

As chaves do gerenciador de estado devem ser cadeias de caracteres. Os valores são genéricos e podem ser de qualquer tipo, incluindo tipos personalizados. Os valores armazenados no Gerenciador de estado de saudação devem ser serializável de contrato de dados porque eles podem ser transmitidos através de nós da saudação rede tooother durante a replicação e podem ser gravados toodisk, dependendo da configuração de persistência de estado de um ator.

Gerenciador de estado Olá expõe métodos comuns de dicionário de estado de gerenciamento, semelhante toothose encontrado no dicionário confiável.

### <a name="accessing-state"></a>Acessando o estado
Estado pode ser acessado por meio do Gerenciador de estado Olá por chave. Os métodos do gerenciador de estado são todos assíncronos, pois podem exigir E/S de disco quando os atores têm um estado persistente. No primeiro acesso, os objetos de estado são armazenados em cache na memória. As operações de acesso repetidas acessam os objetos diretamente da memória e são retornadas de forma síncrona sem incorrer em E/S de disco ou sobrecarga de troca de contexto assíncrona. Um objeto de estado é removido do cache de saudação em Olá casos a seguir:

* Um método de ator lança uma exceção sem tratamento depois de recuperar um objeto do Gerenciador de estado de saudação.
* Um ator é reativado depois de ser desativado ou depois de uma falha.
* páginas de provedor de estado de saudação do estado toodisk. Esse comportamento depende da implementação de provedor de estado de saudação. provedor de estado de padrão de saudação para Olá `Persisted` configuração tem esse comportamento.

Você pode recuperar o estado usando um padrão *obter* operação gera `KeyNotFoundException`(c#) ou `NoSuchElementException`(Java) se não existir uma entrada para a chave de saudação:

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

O estado também pode ser recuperado usando um método *TryGet* que não gera exceção, caso não exista uma entrada para uma chave:

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

### <a name="saving-state"></a>Salvando o estado
métodos de recuperação do Gerenciador de estado de saudação retornam um objeto de tooan de referência na memória local. Modificar esse objeto na memória local sozinho não faz com que ele toobe salvo permanentemente. Quando um objeto é recuperado do Gerenciador de estado hello e modificado, ele deve ser reinserido Olá toobe de Gerenciador de estado salvo permanentemente.

Você pode inserir o estado usando um incondicional *definir*, que é Olá equivalente de saudação `dictionary["key"] = value` sintaxe:

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

Você pode adicionar estado usando um método *Add*. Este método lança `InvalidOperationException`(c#) ou `IllegalStateException`(Java) quando ele tenta tooadd uma chave que já existe.

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

Você também pode adicionar estado usando um método *TryAdd*. Esse método não lançará quando ele tenta tooadd uma chave que já existe.

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

No final de saudação de um método de ator, o Gerenciador de estado de saudação salva automaticamente quaisquer valores que foram adicionados ou modificados por uma operação de inserção ou atualização. "Salvar" pode incluir toodisk persistente e replicação, dependendo das configurações de saudação usado. Valores que não foram modificados não serão persistentes nem replicados. Se nenhum valor tiver sido modificado, Olá operação de salvamento não fará nada. Se salvar falhas, hello estado modificado será descartado e estado original Olá é recarregado.

Você também pode salvar estado manualmente pela chamada hello `SaveStateAsync` método na base de ator hello:

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

### <a name="removing-state"></a>Removendo o estado
Você pode remover estado permanentemente do Gerenciador de estado de um ator Olá chamada *remover* método. Este método lança `KeyNotFoundException`(c#) ou `NoSuchElementException`(Java) quando ele tenta tooremove uma chave que não existe.

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

Você também pode remover estado permanentemente usando Olá *TryRemove* método. Esse método não lançará quando ele tenta tooremove uma chave que não existe.

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

## <a name="next-steps"></a>Próximas etapas

Estado que é armazenado no Reliable Actors deve ser serializado antes de sua toodisk escrito e replicado para alta disponibilidade. Saiba mais sobre a [Serialização de tipo de ator](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).

Em seguida, saiba mais sobre [Diagnóstico e monitoramento de desempenho do ator](service-fabric-reliable-actors-diagnostics.md).
