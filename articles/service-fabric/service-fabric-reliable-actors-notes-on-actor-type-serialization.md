---
title: "serialização de tipo de anotações de atores aaaReliable em ator | Microsoft Docs"
description: "Discute os requisitos básicos para a definição de interfaces e classes serializáveis que podem ser usado toodefine estados atores confiável do serviço de malha"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 6e50e4dc-969a-4a1c-b36c-b292d964c7e3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: d8584e7d90fe1c68af38983e71e5d0a7554689bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a><span data-ttu-id="46e82-103">Observações sobre a serialização de tipo dos Reliable Actors do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="46e82-103">Notes on Service Fabric Reliable Actors type serialization</span></span>
<span data-ttu-id="46e82-104">Olá argumentos de todos os métodos, tipos de resultados de tarefas de saudação retornado por cada método em uma interface de ator e devem ser objetos armazenados no Gerenciador de estado de um ator [de contrato de dados serializáveis](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="46e82-104">hello arguments of all methods, result types of hello tasks returned by each method in an actor interface, and objects stored in an actor's state manager must be [data contract serializable](https://msdn.microsoft.com/library/ms731923.aspx).</span></span> <span data-ttu-id="46e82-105">Isso também se aplica a toohello argumentos de métodos Olá definidos no [interfaces de evento de ator](service-fabric-reliable-actors-events.md).</span><span class="sxs-lookup"><span data-stu-id="46e82-105">This also applies toohello arguments of hello methods defined in [actor event interfaces](service-fabric-reliable-actors-events.md).</span></span> <span data-ttu-id="46e82-106">(Os métodos de interface de eventos de ator sempre retornam nulo).</span><span class="sxs-lookup"><span data-stu-id="46e82-106">(Actor event interface methods always return void.)</span></span>

## <a name="custom-data-types"></a><span data-ttu-id="46e82-107">Tipos de dados personalizados</span><span class="sxs-lookup"><span data-stu-id="46e82-107">Custom data types</span></span>
<span data-ttu-id="46e82-108">Neste exemplo, a saudação interface ator a seguir define um método que retorna um tipo de dados personalizado chamado `VoicemailBox`:</span><span class="sxs-lookup"><span data-stu-id="46e82-108">In this example, hello following actor interface defines a method that returns a custom data type called `VoicemailBox`:</span></span>

```csharp
public interface IVoiceMailBoxActor : IActor
{
    Task<VoicemailBox> GetMailBoxAsync();
}
```

```Java
public interface VoiceMailBoxActor extends Actor
{
    CompletableFuture<VoicemailBox> getMailBoxAsync();
}
```

<span data-ttu-id="46e82-109">Olá interface é implementada por um ator que usa Olá estado manager toostore um `VoicemailBox` objeto:</span><span class="sxs-lookup"><span data-stu-id="46e82-109">hello interface is implemented by an actor that uses hello state manager toostore a `VoicemailBox` object:</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
public class VoiceMailBoxActor : Actor, IVoicemailBoxActor
{
    public VoiceMailBoxActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<VoicemailBox> GetMailboxAsync()
    {
        return this.StateManager.GetStateAsync<VoicemailBox>("Mailbox");
    }
}

```

```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class VoiceMailBoxActorImpl extends FabricActor implements VoicemailBoxActor
{
    public VoiceMailBoxActorImpl(ActorService actorService, ActorId actorId)
    {
         super(actorService, actorId);
    }

    public CompletableFuture<VoicemailBox> getMailBoxAsync()
    {
         return this.stateManager().getStateAsync("Mailbox");
    }
}

```

<span data-ttu-id="46e82-110">Neste exemplo, Olá `VoicemailBox` o objeto é serializado quando:</span><span class="sxs-lookup"><span data-stu-id="46e82-110">In this example, hello `VoicemailBox` object is serialized when:</span></span>

* <span data-ttu-id="46e82-111">objeto de saudação é transmitido entre uma instância de ator e um chamador.</span><span class="sxs-lookup"><span data-stu-id="46e82-111">hello object is transmitted between an actor instance and a caller.</span></span>
* <span data-ttu-id="46e82-112">objeto Olá é salvo no Gerenciador de estado Olá onde é toodisk persistida e replicada tooother nós.</span><span class="sxs-lookup"><span data-stu-id="46e82-112">hello object is saved in hello state manager where it is persisted toodisk and replicated tooother nodes.</span></span>

<span data-ttu-id="46e82-113">estrutura de Reliable Actor Olá usa serialização de DataContract.</span><span class="sxs-lookup"><span data-stu-id="46e82-113">hello Reliable Actor framework uses DataContract serialization.</span></span> <span data-ttu-id="46e82-114">Olá, portanto, os objetos de dados personalizados e seus membros devem ser anotados com hello **DataContract** e **DataMember** atributos, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="46e82-114">Therefore, hello custom data objects and their members must be annotated with hello **DataContract** and **DataMember** attributes, respectively.</span></span>

```csharp
[DataContract]
public class Voicemail
{
    [DataMember]
    public Guid Id { get; set; }

    [DataMember]
    public string Message { get; set; }

    [DataMember]
    public DateTime ReceivedAt { get; set; }
}
```
```Java
public class Voicemail implements Serializable
{
    private static final long serialVersionUID = 42L;

    private UUID id;                    //getUUID() and setUUID()

    private String message;             //getMessage() and setMessage()

    private GregorianCalendar receivedAt; //getReceivedAt() and setReceivedAt()
}
```


```csharp
[DataContract]
public class VoicemailBox
{
    public VoicemailBox()
    {
        this.MessageList = new List<Voicemail>();
    }

    [DataMember]
    public List<Voicemail> MessageList { get; set; }

    [DataMember]
    public string Greeting { get; set; }
}
```
```Java
public class VoicemailBox implements Serializable
{
    static final long serialVersionUID = 42L;
    
    public VoicemailBox()
    {
        this.messageList = new ArrayList<Voicemail>();
    }

    private List<Voicemail> messageList;   //getMessageList() and setMessageList()

    private String greeting;               //getGreeting() and setGreeting()
}
```


## <a name="next-steps"></a><span data-ttu-id="46e82-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="46e82-115">Next steps</span></span>
* [<span data-ttu-id="46e82-116">Ciclo de vida do ator e coleta de lixo</span><span class="sxs-lookup"><span data-stu-id="46e82-116">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="46e82-117">Lembretes e temporizadores de ator</span><span class="sxs-lookup"><span data-stu-id="46e82-117">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="46e82-118">Eventos de ator</span><span class="sxs-lookup"><span data-stu-id="46e82-118">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="46e82-119">Reentrância de ator</span><span class="sxs-lookup"><span data-stu-id="46e82-119">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="46e82-120">Polimorfismo de ator e padrões de design orientado a objeto</span><span class="sxs-lookup"><span data-stu-id="46e82-120">Actor polymorphism and object-oriented design patterns</span></span>](service-fabric-reliable-actors-polymorphism.md)
* [<span data-ttu-id="46e82-121">Diagnóstico e monitoramento de desempenho do ator</span><span class="sxs-lookup"><span data-stu-id="46e82-121">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
