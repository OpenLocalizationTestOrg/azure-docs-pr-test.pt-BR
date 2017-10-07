---
title: aaaReentrancy em microservices do Azure baseado em ator | Microsoft Docs
description: "Introdução tooreentrancy para atores confiável do serviço de malha"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: be23464a-0eea-4eca-ae5a-2e1b650d365e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 61c69bcf0f100e075d19ba155954c05789b71761
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-reentrancy"></a>Reentrância de Reliable Actors
Olá Reliable Actors em tempo de execução, por padrão, permite que chamadas lógicas com base em contexto reentrada. Isso permite reentrante de toobe atores se eles estiverem em Olá mesma chamada de cadeia de contexto. Por exemplo, o ator A envia um tooActor mensagem B, que envia uma mensagem tooActor C. Como parte do processamento de mensagem de saudação, se ator C chama ator A, mensagem de saudação é reentrante, para que ele poderá ser. Todas as outras mensagens que fazem parte de um contexto de chamada diferente serão bloqueadas no Ator A até a conclusão do processamento.

Há duas opções disponíveis para reentrada ator definida no hello `ActorReentrancyMode` enum:

* `LogicalCallContext` (comportamento padrão)
* `Disallowed` - desabilita a nova entrada

```csharp
public enum ActorReentrancyMode
{
    LogicalCallContext = 1,
    Disallowed = 2
}
```
```Java
public enum ActorReentrancyMode
{
    LogicalCallContext(1),
    Disallowed(2)
}
```
A nova entrada pode ser definida nas configurações de `ActorService`durante o registro. configuração de saudação se aplica a instâncias de ator tooall criadas no serviço de ator hello.

Olá, exemplo a seguir mostra um serviço de ator que define o modo de reentrada Olá muito`ActorReentrancyMode.Disallowed`. Nesse caso, se um ator envia um ator de tooanother reentrante mensagem, uma exceção do tipo `FabricException` será lançada.

```csharp
static class Program
{
    static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<Actor1>(
                (context, actorType) => new ActorService(
                    context,
                    actorType, () => new Actor1(),
                    settings: new ActorServiceSettings()
                    {
                        ActorConcurrencySettings = new ActorConcurrencySettings()
                        {
                            ReentrancyMode = ActorReentrancyMode.Disallowed
                        }
                    }))
                .GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}
```
```Java
static class Program
{
    static void Main()
    {
        try
        {
            ActorConcurrencySettings actorConcurrencySettings = new ActorConcurrencySettings();
            actorConcurrencySettings.setReentrancyMode(ActorReentrancyMode.Disallowed);

            ActorServiceSettings actorServiceSettings = new ActorServiceSettings();
            actorServiceSettings.setActorConcurrencySettings(actorConcurrencySettings);

            ActorRuntime.registerActorAsync(
                Actor1.getClass(),
                (context, actorType) -> new FabricActorService(
                    context,
                    actorType, () -> new Actor1(),
                    null,
                    stateProvider,
                    actorServiceSettings, timeout);

            Thread.sleep(Long.MAX_VALUE);
        }
        catch (Exception e)
        {
            throw e;
        }
    }
}
```


## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre a reentrada em Olá [documentação de referência de API de ator](https://msdn.microsoft.com/library/azure/dn971626.aspx)
