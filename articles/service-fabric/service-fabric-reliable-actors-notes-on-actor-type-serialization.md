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
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a>Observações sobre a serialização de tipo dos Reliable Actors do Service Fabric
Olá argumentos de todos os métodos, tipos de resultados de tarefas de saudação retornado por cada método em uma interface de ator e devem ser objetos armazenados no Gerenciador de estado de um ator [de contrato de dados serializáveis](https://msdn.microsoft.com/library/ms731923.aspx). Isso também se aplica a toohello argumentos de métodos Olá definidos no [interfaces de evento de ator](service-fabric-reliable-actors-events.md). (Os métodos de interface de eventos de ator sempre retornam nulo).

## <a name="custom-data-types"></a>Tipos de dados personalizados
Neste exemplo, a saudação interface ator a seguir define um método que retorna um tipo de dados personalizado chamado `VoicemailBox`:

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

Olá interface é implementada por um ator que usa Olá estado manager toostore um `VoicemailBox` objeto:

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

Neste exemplo, Olá `VoicemailBox` o objeto é serializado quando:

* objeto de saudação é transmitido entre uma instância de ator e um chamador.
* objeto Olá é salvo no Gerenciador de estado Olá onde é toodisk persistida e replicada tooother nós.

estrutura de Reliable Actor Olá usa serialização de DataContract. Olá, portanto, os objetos de dados personalizados e seus membros devem ser anotados com hello **DataContract** e **DataMember** atributos, respectivamente.

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


## <a name="next-steps"></a>Próximas etapas
* [Ciclo de vida do ator e coleta de lixo](service-fabric-reliable-actors-lifecycle.md)
* [Lembretes e temporizadores de ator](service-fabric-reliable-actors-timers-reminders.md)
* [Eventos de ator](service-fabric-reliable-actors-events.md)
* [Reentrância de ator](service-fabric-reliable-actors-reentrancy.md)
* [Polimorfismo de ator e padrões de design orientado a objeto](service-fabric-reliable-actors-polymorphism.md)
* [Diagnóstico e monitoramento de desempenho do ator](service-fabric-reliable-actors-diagnostics.md)
