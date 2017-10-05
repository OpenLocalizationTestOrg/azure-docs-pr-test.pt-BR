---
title: "Observações de Reliable Actors sobre a serialização do tipo de ator | Microsoft Docs"
description: "Discute os requisitos básicos para definir as classes serializáveis que podem ser usadas para estabelecer as interfaces e o estado dos Reliable Actors do Service Fabric"
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
ms.openlocfilehash: 4b48b893e5a3bf5620f00a336576efe1ad63def8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a><span data-ttu-id="7da0f-103">Observações sobre a serialização de tipo dos Reliable Actors do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7da0f-103">Notes on Service Fabric Reliable Actors type serialization</span></span>
<span data-ttu-id="7da0f-104">Os argumentos de todos os métodos, os tipos de resultado das tarefas retornados por cada método em uma interface de ator e os objetos armazenados no gerenciador de estado de um ator devem ser [serializáveis por contrato de dados](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="7da0f-104">The arguments of all methods, result types of the tasks returned by each method in an actor interface, and objects stored in an actor's state manager must be [data contract serializable](https://msdn.microsoft.com/library/ms731923.aspx).</span></span> <span data-ttu-id="7da0f-105">Isso também se aplica aos argumentos dos métodos definidos nas [interfaces de evento de ator](service-fabric-reliable-actors-events.md).</span><span class="sxs-lookup"><span data-stu-id="7da0f-105">This also applies to the arguments of the methods defined in [actor event interfaces](service-fabric-reliable-actors-events.md).</span></span> <span data-ttu-id="7da0f-106">(Os métodos de interface de eventos de ator sempre retornam nulo).</span><span class="sxs-lookup"><span data-stu-id="7da0f-106">(Actor event interface methods always return void.)</span></span>

## <a name="custom-data-types"></a><span data-ttu-id="7da0f-107">Tipos de dados personalizados</span><span class="sxs-lookup"><span data-stu-id="7da0f-107">Custom data types</span></span>
<span data-ttu-id="7da0f-108">Neste exemplo, a interface de ator a seguir define um método que retorna um tipo de dados personalizado chamado `VoicemailBox`:</span><span class="sxs-lookup"><span data-stu-id="7da0f-108">In this example, the following actor interface defines a method that returns a custom data type called `VoicemailBox`:</span></span>

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

<span data-ttu-id="7da0f-109">A interface é implementada por um ator que usa o gerenciador de estado para armazenar um objeto `VoicemailBox`:</span><span class="sxs-lookup"><span data-stu-id="7da0f-109">The interface is implemented by an actor that uses the state manager to store a `VoicemailBox` object:</span></span>

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

<span data-ttu-id="7da0f-110">Neste exemplo, o objeto `VoicemailBox` é serializado quando:</span><span class="sxs-lookup"><span data-stu-id="7da0f-110">In this example, the `VoicemailBox` object is serialized when:</span></span>

* <span data-ttu-id="7da0f-111">O objeto é transmitido entre uma instância do ator e um chamador.</span><span class="sxs-lookup"><span data-stu-id="7da0f-111">The object is transmitted between an actor instance and a caller.</span></span>
* <span data-ttu-id="7da0f-112">O objeto é salvo no gerenciador de estado, local em que é mantido no disco e replicado para outros nós.</span><span class="sxs-lookup"><span data-stu-id="7da0f-112">The object is saved in the state manager where it is persisted to disk and replicated to other nodes.</span></span>

<span data-ttu-id="7da0f-113">A estrutura Reliable Actor usa a serialização DataContract.</span><span class="sxs-lookup"><span data-stu-id="7da0f-113">The Reliable Actor framework uses DataContract serialization.</span></span> <span data-ttu-id="7da0f-114">Portanto, os objetos de dados personalizados e seus membros devem ser anotados com os atributos **DataContract** e **DataMember**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="7da0f-114">Therefore, the custom data objects and their members must be annotated with the **DataContract** and **DataMember** attributes, respectively.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="7da0f-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7da0f-115">Next steps</span></span>
* [<span data-ttu-id="7da0f-116">Ciclo de vida do ator e coleta de lixo</span><span class="sxs-lookup"><span data-stu-id="7da0f-116">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="7da0f-117">Lembretes e temporizadores de ator</span><span class="sxs-lookup"><span data-stu-id="7da0f-117">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="7da0f-118">Eventos de ator</span><span class="sxs-lookup"><span data-stu-id="7da0f-118">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="7da0f-119">Reentrância de ator</span><span class="sxs-lookup"><span data-stu-id="7da0f-119">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="7da0f-120">Polimorfismo de ator e padrões de design orientado a objeto</span><span class="sxs-lookup"><span data-stu-id="7da0f-120">Actor polymorphism and object-oriented design patterns</span></span>](service-fabric-reliable-actors-polymorphism.md)
* [<span data-ttu-id="7da0f-121">Diagnóstico e monitoramento de desempenho do ator</span><span class="sxs-lookup"><span data-stu-id="7da0f-121">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
