---
title: aaaOverview do ciclo de vida baseado em ator microservices do Azure | Microsoft Docs
description: "Explica o ciclo de vida, a coleta de lixo e a exclusão manual de atores e seu estado de Reliable Actor do Service Fabric"
services: service-fabric
documentationcenter: .net
author: amanbha
manager: timlt
editor: vturecek
ms.assetid: b91384cc-804c-49d6-a6cb-f3f3d7d65a8e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: a7926e372449048f0a579c2c58573754a4a82363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a>Ciclo de vida, coleta automática de lixo e exclusão manual do ator
Um ator é ativado Olá a primeira vez que é feita uma chamada tooany de seus métodos. Um ator é desativado (lixo coletado pelo tempo de execução do hello atores) se ele não for usado por um período configurável. Um ator e seu estado também podem ser excluídos manualmente a qualquer momento.

## <a name="actor-activation"></a>Ativação do ator
Quando um ator é ativado, a seguir Olá ocorre:

* Quando uma chamada chega para um ator e ele ainda não está ativo, é criado um novo ator.
* estado de saudação do ator é carregado se ele mantém o estado.
* Olá `OnActivateAsync` (c#) ou `onActivateAsync` método (Java) (que pode ser substituído na implementação de ator Olá) é chamado.
* ator Olá agora é considerado ativo.

## <a name="actor-deactivation"></a>Desativação do ator
Quando um ator é desativado, ocorre a seguinte hello:

* Quando um ator não é usado por um período de tempo, ele será removido da tabela de atores Active hello.
* Olá `OnDeactivateAsync` (c#) ou `onDeactivateAsync` método (Java) (que pode ser substituído na implementação de ator Olá) é chamado. Isso limpará todos os timers de saudação de ator hello. Operações de ator, como alterações de estado, não devem ser chamadas por meio desse método.

> [!TIP]
> Olá atores Fabric runtime emite alguns [eventos relacionados tooactor ativação e desativação](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters). Eles são úteis para diagnóstico e monitoramento de desempenho.
>
>

### <a name="actor-garbage-collection"></a>Coleta de Lixo de Ator
Quando um ator é desativado, objeto de ator toohello referências são liberados e pode ser coletada como lixo normalmente por Olá common language runtime (CLR) ou o coletor de lixo do java (JVM) de VM. Coleta de lixo só limpa o objeto de ator Olá; ele faz **não** remover o estado armazenado no Gerenciador de estado do ator hello. Olá próximo tempo Olá ator é ativado, um novo objeto de ator é criado e seu estado é restaurado.

O que conta como "é usada" para fins de saudação de desativação e coleta de lixo?

* Recebimento de chamadas
* `IRemindable.ReceiveReminderAsync`método que está sendo invocado (aplicável somente se o ator Olá usa lembretes)

> [!NOTE]
> Se o ator Olá usa temporizadores e seu retorno de chamada timer é invocado, ele não **não** contagem como "é usada".
>
>

Antes de entrarmos em detalhes de saudação de desativação, é importante toodefine Olá termos a seguir:

* *Intervalo de verificação*. Esse é o intervalo de saudação no qual Olá atores em tempo de execução verifica sua tabela de atores Active atores que podem ser desativados e coletado como lixo. valor padrão de saudação para isso é 1 minuto.
* *Tempo limite de ociosidade*. Isso é Olá tempo que um ator precisa tooremain não utilizados (ocioso) antes que ele pode ser desativado e coletado como lixo. valor padrão de saudação para isso é 60 minutos.

Normalmente, não é necessário toochange esses padrões. No entanto, se necessário, esses intervalos podem ser alterados por meio de `ActorServiceSettings` ao registrar seu [Serviço de Ator](service-fabric-reliable-actors-platform.md):

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        ActorRuntime.RegisterActorAsync<MyActor>((context, actorType) =>
                new ActorService(context, actorType,
                    settings:
                        new ActorServiceSettings()
                        {
                            ActorGarbageCollectionSettings =
                                new ActorGarbageCollectionSettings(10, 2)
                        }))
            .GetAwaiter()
            .GetResult();
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
    }
}
```
Para cada ativo ator, tempo de execução de ator Olá controla de Olá período de tempo que ele ficar ocioso (ou seja, não usado). tempo de execução de ator Olá verifica cada atores Olá cada `ScanIntervalInSeconds` toosee se ele puder ser lixo coletado e coleta-lo se ele estiver inativo por `IdleTimeoutInSeconds`.

Sempre que um ator é usado, o tempo ocioso é too0 de redefinição. Depois disso, ator Olá pode ser limpos somente se ele permanecerá ocioso novamente `IdleTimeoutInSeconds`. Lembre-se de que um ator é considerado toohave foi usado se um método de interface de ator ou um retorno de chamada de lembrete de ator é executado. Um ator é **não** considerado toohave foi usado se seu retorno de chamada timer é executado.

Olá diagrama a seguir mostra Olá ciclo de vida de um único ator tooillustrate esses conceitos.

![Exemplo de tempo ocioso][1]

exemplo Hello mostra o impacto de saudação de chamadas de método de ator, lembretes e temporizadores no tempo de vida de saudação deste ator. Olá seguintes pontos sobre o exemplo hello é vale a pena mencionar:

* ScanInterval e IdleTimeout são definidos too5 e 10 respectivamente. (Unidades não importa aqui, desde que o nosso objetivo é o conceito de saudação de tooillustrate somente.)
* verificação de saudação para atores coletado como lixo toobe acontece em T = 0, 5, 10, 15, 20, 25, conforme definido pelo intervalo de verificação de saudação de 5.
* Um medidor de tempo periódico é acionado em T = 4, 8, 12, 16, 20, 24 e executa seu retorno de chamada. Ele não afeta o tempo ocioso de saudação do ator hello.
* Uma chamada de método de ator em T = 7 redefine Olá tempo ocioso too0 e adia a coleta de lixo de saudação do ator hello.
* Executa um retorno de chamada de lembrete de ator em T = 14 e mais atrasos Olá coleta de lixo de ator hello.
* Durante a verificação de coleta de lixo Olá T = 25, tempo ocioso do ator Olá finalmente excede o tempo limite de ociosidade de saudação de 10 e ator Olá é coletado como lixo.

Um ator nunca terá o lixo coletado durante a execução de um de seus métodos, não importa quanto tempo seja gasto na execução do método. Como mencionado anteriormente, execução de saudação de métodos de interface de ator e retornos de chamada de lembrete impede que a coleta de lixo redefinindo too0 de tempo ocioso do ator hello. execução de saudação de retornos de chamada timer não redefine Olá too0 de tempo ocioso. No entanto, coleta de lixo de saudação do ator Olá é adiada até que a chamada de timer Olá concluiu a execução.

## <a name="deleting-actors-and-their-state"></a>Excluindo atores e seu estado
Coleta de lixo de atores desativados só limpa o objeto de ator hello, mas não remove os dados armazenados no Gerenciador de estado de um ator. Quando um ator é reativado, os dados novamente são feitos tooit disponível por meio do Gerenciador de estado de saudação. Em casos onde atores armazenar dados no Gerenciador de estado e são desativados, mas nunca ativados novamente, pode ser necessário tooclean backup de seus dados.

Olá [serviço de ator](service-fabric-reliable-actors-platform.md) fornece uma função para excluir os atores de um chamador remoto:

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

Excluir um ator tem Olá efeitos dependendo se ou não está ativo no momento ator Olá a seguir:

* **Ator ativo**
  * O ator é removido da lista de atores ativos e é desativado.
  * Seu estado é excluído permanentemente.
* **Ator inativo**
  * Seu estado é excluído permanentemente.

Observe que não é possível chamar um ator excluir no próprio de um dos seus métodos de ator porque não é possível excluir o ator Olá ao ser executado em um contexto de chamada de ator, no qual Olá runtime obteve um bloqueio em torno de acesso de thread único tooenforce chamada ator hello.

## <a name="next-steps"></a>Próximas etapas
* [Lembretes e temporizadores de ator](service-fabric-reliable-actors-timers-reminders.md)
* [Eventos de ator](service-fabric-reliable-actors-events.md)
* [Reentrância de ator](service-fabric-reliable-actors-reentrancy.md)
* [Diagnóstico e monitoramento de desempenho do ator](service-fabric-reliable-actors-diagnostics.md)
* [Documentação de referência da API do Ator](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Código de exemplo C#](https://github.com/Azure/servicefabric-samples)
* [Código de exemplo Java](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
