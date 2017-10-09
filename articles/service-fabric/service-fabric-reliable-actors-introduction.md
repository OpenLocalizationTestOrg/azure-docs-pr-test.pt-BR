---
title: "aaaService visão geral de atores confiável malha | Microsoft Docs"
description: "Introdução toohello Service Fabric Reliable Actors modelo de programação."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 7fdad07f-f2d6-4c74-804d-e0d56131f060
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab010cbf936c6cf723b3d453ef95a9bf51f76c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooservice-fabric-reliable-actors"></a>Introdução tooService malha Reliable Actors
Atores confiáveis é uma estrutura de aplicativo de malha do serviço com base em Olá [ator Virtual](http://research.microsoft.com/en-us/projects/orleans/) padrão. Olá confiável API de atores fornece um modelo de programação thread único, criado em garantias de escalabilidade e confiabilidade de saudação fornecidas pela malha do serviço.

## <a name="what-are-actors"></a>O que são Atores?
Um ator é uma unidade isolada e independente de computação e de estado com execução single-threaded. Olá [padrão ator](https://en.wikipedia.org/wiki/Actor_model) é um modelo de computação para sistemas simultâneos ou distribuídos em que um grande número desses atores pode ser executadas simultaneamente e independentemente uns dos outros. Os atores podem se comunicar entre si e criar outros atores.

### <a name="when-toouse-reliable-actors"></a>Quando toouse Reliable Actors
Atores confiável do serviço de malha é uma implementação do padrão de design de ator hello. Assim como acontece com qualquer padrão de design de software, decisão Olá se toouse um padrão específico é feito com base em se um software criar problema correspondam padrão de saudação.

Embora o design de ator Olá padrão pode ser que uma boa opção tooa número de problemas de sistemas distribuídos e cenários de cuidadosos consideração das restrições de saudação do padrão de saudação e framework Olá implementá-lo deve ser feita. Como orientação geral, considere Olá ator padrão toomodel seu problema ou cenário se:

* Seu problema de espaço envolve um grande número (milhares ou milhões) de pequenas unidades de estado e lógica que, além de serem independentes, são isoladas.
* Você deseja toowork com objetos de thread único que não exigem interação significativa de componentes externos, incluindo consultando o estado em um conjunto de atores.
* Suas instâncias de ator não bloquearão chamadores com atrasos imprevisíveis emitindo operações de E/S.

## <a name="actors-in-service-fabric"></a>Atores no Service Fabric
No Service Fabric atores são implementados no framework de Reliable Actors Olá: uma estrutura de aplicativo com base no padrão de ator criada na parte superior do [serviços confiável do serviço do Fabric](service-fabric-reliable-services-introduction.md). Cada serviço escrito do Reliable Actor é, de fato, um Reliable Service com estado particionado.

Cada ator é definido como uma instância de um tipo de ator, toohello idênticos maneira um objeto .NET é uma instância de um tipo .NET. Por exemplo, pode haver um tipo de ator que implementa a funcionalidade de saudação de uma calculadora e pode haver muitos atores desse tipo que são distribuídos em vários nós em um cluster. Cada ator desse é exclusivamente identificado por uma ID de ator.

### <a name="actor-lifetime"></a>Tempo de vida do ator
Atores Service Fabric são virtuais, o que significa que seu tempo de vida não é a representação em memória tootheir associado. Como resultado, eles não precisarem toobe explicitamente criado ou destruído. tempo de execução do Hello Reliable Actors ativa automaticamente Olá um ator primeira vez que ele receber uma solicitação para esse ID de ator. Se um ator não for usado por um período de tempo, o tempo de execução do hello Reliable Actors lixo-coleta objetos em memória de saudação. Ele também mantêm Conhecimento da existência do ator Olá caso seja necessário toobe reativado mais tarde. Para obter mais detalhes, veja [Ciclo de vida do ator e coleta de lixo](service-fabric-reliable-actors-lifecycle.md).

Essa abstração de tempo de vida de ator virtual executa algumas restrições como resultado do modelo de ator virtual hello e, em seguida, na verdade Olá implementação Reliable Actors às vezes desvia deste modelo.

* Um ator é ativado automaticamente (fazendo com que um ator toobe objeto construído) Olá a primeira vez que uma mensagem é enviada a ID de ator tooits. Após um período de tempo, o objeto de ator de saudação é coletado como lixo. Em Olá futuro, usando uma ID de ator Olá novamente, faz com que um novo ator toobe objeto construído. Estado de um ator superam o tempo de vida do objeto hello quando armazenado no Gerenciador de estado de saudação.
* A chamada a qualquer método de ator para obter uma ID de ator ativa esse ator. Por esse motivo, os tipos de ator têm seu construtor chamado implicitamente pelo tempo de execução de saudação. Portanto, o código do cliente não pode passar construtor do tipo de ator toohello parâmetros, embora parâmetros podem ser passados construtor toohello ator pelo serviço de saudação em si. resultado de saudação é que os atores podem ser construídos em um estado parcialmente inicializado pelo tempo de saudação que outros métodos são chamados, se ator Olá requer parâmetros de inicialização do cliente de saudação. Não há nenhum ponto de entrada único para a ativação de saudação de um ator do cliente hello.
* Embora Reliable Actors implicitamente criar objetos de ator. Você tem Olá capacidade tooexplicitly excluir um ator e seu estado.

### <a name="distribution-and-failover"></a>Distribuição e failover
tooprovide escalabilidade e confiabilidade, o Service Fabric distribui atores em todo o cluster hello e automaticamente migra de nós com falhas toohealthy aqueles conforme necessário. Essa é uma abstração de um [Reliable Service com estado particionado](service-fabric-concepts-partitioning.md). Distribuição, escalabilidade, confiabilidade e o failover automático são fornecidos por meio de fatos Olá que atores são executados dentro de um serviço confiável com monitoração de estado chamado hello *serviço de ator*.

Atores são distribuídos em partições Olá Olá serviço ator, e essas partições são distribuídas entre os nós de saudação em um cluster do Service Fabric. Cada partição de serviço contém um conjunto de atores. Service Fabric gerencia a distribuição e o failover de partições de serviço hello.

Por exemplo, um serviço de ator com nove partições implantado toothree nós usando a colocação de partição de ator saudação padrão serão distribuídos, deste modo:

![Distribuição dos Reliable Actors][2]

Olá ator Framework gerencia configurações de intervalo esquema e a chave de partição para você. Isso simplifica algumas escolhas, mas também traz algumas considerações:

* Serviços confiáveis permite que você toochoose um esquema de particionamento, intervalo de chave (ao usar um esquema de particionamento de intervalo) e a contagem de partição. Atores confiáveis é o esquema de particionamento toohello restrito intervalo (esquema uniforme Int64 Olá) e requer que você usar a gama completa de chave de Int64 hello.
* Por padrão, os atores são colocados aleatoriamente em partições, resultando em uma distribuição uniforme.
* Como os atores são colocados aleatoriamente, deve-se esperar que as operações de ator sempre exijam a comunicação de rede, incluindo a serialização e desserialização de dados de chamada de método, incorrendo em latência e sobrecarga.
* Em cenários avançados, é possível toocontrol posicionamento de partição de ator usando Int64 ator IDs que mapear partições toospecific. No entanto, isso poderá resultar em uma distribuição desbalanceada de atores nas partições.

Para obter mais informações sobre como os serviços de ator são particionados, consulte muito[particionamento conceitos para atores](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors).

### <a name="actor-communication"></a>Comunicação do ator
Interações de ator são definidas em uma interface que é compartilhada por ator Olá que implementa a interface hello e cliente Olá que obtém um proxy ator tooan via Olá mesma interface. Como essa interface é usada tooinvoke ator métodos assincronamente, cada método na interface de saudação deve ser de retorno.

Chamadas de método e suas respostas finalmente resultam em solicitações de rede em cluster hello, portanto argumentos de saudação e tipos de resultados de saudação de tarefas de saudação que elas retornam devem ser serializadas por plataforma de saudação. Em particular, eles devem ser [contrato de dados serializáveis](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).

#### <a name="hello-actor-proxy"></a>proxy de ator Olá
API de cliente Reliable Actors Olá fornece comunicação entre uma instância de ator e um cliente de ator. toocommunicate com um ator, um cliente cria um objeto de proxy de ator que implementa a interface de ator hello. cliente Olá interage com o ator hello, chamar métodos no objeto de proxy de saudação. proxy de ator Olá pode ser usado para comunicação de cliente para ator e ator de ator.

```csharp
// Create a randomly distributed actor ID
ActorId actorId = ActorId.CreateRandom();

// This only creates a proxy object, it does not activate an actor or invoke any methods yet.
IMyActor myActor = ActorProxy.Create<IMyActor>(actorId, new Uri("fabric:/MyApp/MyActorService"));

// This will invoke a method on hello actor. If an actor with hello given ID does not exist, it will be activated by this method call.
await myActor.DoWorkAsync();
```

```java
// Create actor ID with some name
ActorId actorId = new ActorId("Actor1");

// This only creates a proxy object, it does not activate an actor or invoke any methods yet.
MyActor myActor = ActorProxyBase.create(actorId, new URI("fabric:/MyApp/MyActorService"), MyActor.class);

// This will invoke a method on hello actor. If an actor with hello given ID does not exist, it will be activated by this method call.
myActor.DoWorkAsync().get();
```


Observe que informações Olá dois usadas objeto de proxy de ator toocreate Olá são Olá ator ID e nome do aplicativo hello. ID de ator Olá identifica exclusivamente ator hello, enquanto o nome do aplicativo hello identifica Olá [aplicativo do Service Fabric](service-fabric-reliable-actors-platform.md#application-model) onde ator Olá é implantado.

Olá `ActorProxy`(c#) / `ActorProxyBase`classe (Java) no lado do cliente Olá executa ator do hello resolução necessário toolocate Olá por ID e abrir um canal de comunicação com ele. Ele também tenta novamente toolocate ator de saudação em casos de saudação de failovers e falhas de comunicação. Como resultado, a entrega de mensagens tem Olá características a seguir:

* A entrega de mensagem é o melhor esforço.
* Atores podem receber mensagens duplicadas de saudação mesmo cliente.

### <a name="concurrency"></a>Simultaneidade
Olá Reliable Actors em tempo de execução fornece um modelo de acesso simples com base em Ativar para acessar os métodos de ator. Isso significa que não é permitido mais de um thread ativo no código do objeto de um ator a qualquer momento. O acesso baseado em turno simplifica consideravelmente os sistemas simultâneos, pois não há necessidade de mecanismos de sincronização para o acesso a dados. Isso também significa que os sistemas devem ser criados com considerações especiais sobre a natureza do acesso de thread único saudação de cada instância de ator.

* Uma única instância de ator não pode processar mais de uma solicitação por vez. Uma instância de ator pode causar um gargalo se trata de solicitações simultâneas toohandle esperado.
* Atores podem acarretar deadlock em si, se houver uma solicitação circular entre dois atores enquanto uma solicitação externa é feita tooone de atores Olá simultaneamente. Olá ator tempo de execução será automaticamente uma vez no ator chama e lançar um toointerrupt de chamador exceção toohello possíveis situações de deadlock.

![Comunicação dos Reliable Actors][3]

#### <a name="turn-based-access"></a>Acesso com base em vez
Uma vez consiste em concluir a execução de um método de ator na solicitação de tooa de resposta de outros clientes ou atores hello, ou concluir a execução da saudação um [timer/lembrete](service-fabric-reliable-actors-timers-reminders.md) retorno de chamada. Mesmo que esses métodos e retornos de chamada assíncronos, o tempo de execução do hello atores não intercalá-los. Um turno deve ser totalmente concluído antes que um novo turno seja permitido. Em outras palavras, um ator timer/lembrete ou método retorno de chamada que está sendo executado deve ser totalmente concluído antes de um novo método tooa chamada ou retorno de chamada é permitido. Um método ou o retorno de chamada é considerado toohave concluído se execução Olá foi retornado de método hello ou tarefa de retorno de chamada e hello retornada pelo método hello ou retorno de chamada é concluída. Vale enfatizar que a simultaneidade baseada em turno é respeitada mesmo entre métodos, temporizadores e retornos de chamada diferentes.

tempo de execução de atores Olá impõe simultaneidade baseada em vez ao adquirir um bloqueio por ator no início de uma curva hello e liberar bloqueio Olá final Olá Olá ativar. Desse modo, a simultaneidade baseada em turno é imposta por ator e não entre atores. Os métodos de ator e retornos de chamada de temporizador/lembrete podem ser executados simultaneamente em nome de diferentes atores.

saudação de exemplo a seguir ilustra Olá acima conceitos. Considere um tipo de ator que implementa dois métodos assíncronos (digamos, *Method1* e *Method2*), um temporizador e um lembrete. Olá diagrama a seguir mostra um exemplo de uma linha do tempo de execução Olá desses métodos e retornos de chamada em nome de duas atores (*ActorId1* e *ActorId2*) que pertencem a tipo de ator toothis.

![Simultaneidade e acesso com base em turno do Reliable Actors][1]

O diagrama segue as seguintes convenções:

* Cada linha vertical mostra o fluxo lógico de saudação da execução de um método ou um retorno de chamada em nome de um ator específico.
* eventos de saudação marcados em cada linha vertical ocorrem em ordem cronológica, com os eventos mais recentes ocorre abaixo os mais antigos.
* Cores diferentes são usadas para linhas de tempo correspondente toodifferent atores.
* Realce é a duração de saudação do tooindicate usado para qual Olá bloqueio por ator é mantido em nome de um método ou o retorno de chamada.

Tooconsider alguns pontos importantes:

* Enquanto *Method1* está em execução em nome de *ActorId2* na solicitação de tooclient resposta *xyz789*, outra solicitação de cliente (*abc123*) chega que também requer *Method1* toobe executado por *ActorId2*. No entanto, Olá segunda execução da *Method1* não começa até concluir a execução anterior hello. Da mesma forma, um lembrete registrados por *ActorId2* é acionado ao *Method1* está sendo executado na solicitação de tooclient resposta *xyz789*. Olá retorno de chamada de lembrete é executado somente depois de ambas as execuções de *Method1* forem concluídas. Tudo isso é devido a simultaneidade baseada em tooturn que está sendo imposta para *ActorId2*.
* Da mesma forma, também for aplicada a simultaneidade baseada em vez de *ActorId1*, conforme demonstrado pela execução de saudação do *Method1*, *Method2*, e Olá chamada timer em nome de *ActorId1* acontece de maneira serial.
* A execução de *Method1* em nome de *ActorId1* é sobreposta por sua execução em nome de *ActorId2*. Isso porque a simultaneidade baseada em turno é imposta apenas em um ator, e não entre atores.
* Em algumas das execuções de retorno de chamada/método hello, Olá `Task`(c#) / `CompletableFuture`(Java) retornado pela conclusão de retorno de chamada/método hello depois que o método hello retorna. Em alguns outros, operação assíncrona Olá já foi concluída por tempo Olá Olá método/retorno. Em ambos os casos, do bloqueio por ator Olá é liberado somente depois que ambos os Olá método/retorno e conclusão da operação assíncrona hello.

#### <a name="reentrancy"></a>Reentrada
tempo de execução de atores Olá permite reentrada por padrão. Isso significa que, se um método de ator *ator A* chama um método em *ator B*, que por sua vez chama outro método em *ator A*, que o método é permitido toorun. Isso ocorre porque ele faz parte da saudação mesmo contexto de lógica de cadeia de chamadas. Todas as chamadas de timer e lembrete iniciar com novo contexto de chamada lógico hello. Consulte Olá [reentrada Reliable Actors](service-fabric-reliable-actors-reentrancy.md) para obter mais detalhes.

#### <a name="scope-of-concurrency-guarantees"></a>Escopo de garantias de simultaneidade
tempo de execução de atores Olá fornece essas garantias de simultaneidade em situações em que ele controla invocação Olá desses métodos. Por exemplo, ele fornece essas garantias para invocações de método hello que são feitas na solicitação do cliente tooa resposta, bem como para retornos de chamada timer e lembretes. No entanto, se o código de ator Olá invoca diretamente esses métodos fora de mecanismos de Olá fornecidos pelo tempo de execução de atores hello, Olá runtime não pode fornecer qualquer garantia de simultaneidade. Por exemplo, se o método hello é invocado no contexto de saudação de alguma tarefa que não está associado à tarefa Olá retornada pelos métodos de ator Olá, Olá runtime não pode fornecer garantias de simultaneidade. Se Olá método é chamado de um thread que ator Olá cria por conta própria, Olá runtime não pode fornecer garantia de simultaneidade. Portanto, as operações do plano de fundo tooperform, atores devem usar [temporizadores de ator e lembretes de ator](service-fabric-reliable-actors-timers-reminders.md) que respeita simultaneidade baseada em Ativar.

## <a name="next-steps"></a>Próximas etapas
* Comece criando seu primeiro serviço de Reliable Actors:
   * [Introdução aos Reliable Actors no .NET](service-fabric-reliable-actors-get-started.md)
   * [Introdução aos Reliable Actors em Java](service-fabric-reliable-actors-get-started-java.md)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-introduction/concurrency.png
[2]: ./media/service-fabric-reliable-actors-introduction/distribution.png
[3]: ./media/service-fabric-reliable-actors-introduction/actor-communication.png
