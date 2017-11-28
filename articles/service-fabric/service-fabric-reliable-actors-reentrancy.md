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
# <a name="reliable-actors-reentrancy"></a><span data-ttu-id="42f66-103">Reentrância de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="42f66-103">Reliable Actors reentrancy</span></span>
<span data-ttu-id="42f66-104">Olá Reliable Actors em tempo de execução, por padrão, permite que chamadas lógicas com base em contexto reentrada.</span><span class="sxs-lookup"><span data-stu-id="42f66-104">hello Reliable Actors runtime, by default, allows logical call context-based reentrancy.</span></span> <span data-ttu-id="42f66-105">Isso permite reentrante de toobe atores se eles estiverem em Olá mesma chamada de cadeia de contexto.</span><span class="sxs-lookup"><span data-stu-id="42f66-105">This allows for actors toobe reentrant if they are in hello same call context chain.</span></span> <span data-ttu-id="42f66-106">Por exemplo, o ator A envia um tooActor mensagem B, que envia uma mensagem tooActor C. Como parte do processamento de mensagem de saudação, se ator C chama ator A, mensagem de saudação é reentrante, para que ele poderá ser.</span><span class="sxs-lookup"><span data-stu-id="42f66-106">For example, Actor A sends a message tooActor B, who sends a message tooActor C. As part of hello message processing, if Actor C calls Actor A, hello message is reentrant, so it will be allowed.</span></span> <span data-ttu-id="42f66-107">Todas as outras mensagens que fazem parte de um contexto de chamada diferente serão bloqueadas no Ator A até a conclusão do processamento.</span><span class="sxs-lookup"><span data-stu-id="42f66-107">Any other messages that are part of a different call context will be blocked on Actor A until it finishes processing.</span></span>

<span data-ttu-id="42f66-108">Há duas opções disponíveis para reentrada ator definida no hello `ActorReentrancyMode` enum:</span><span class="sxs-lookup"><span data-stu-id="42f66-108">There are two options available for actor reentrancy defined in hello `ActorReentrancyMode` enum:</span></span>

* <span data-ttu-id="42f66-109">`LogicalCallContext` (comportamento padrão)</span><span class="sxs-lookup"><span data-stu-id="42f66-109">`LogicalCallContext` (default behavior)</span></span>
* <span data-ttu-id="42f66-110">`Disallowed` - desabilita a nova entrada</span><span class="sxs-lookup"><span data-stu-id="42f66-110">`Disallowed` - disables reentrancy</span></span>

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
<span data-ttu-id="42f66-111">A nova entrada pode ser definida nas configurações de `ActorService`durante o registro.</span><span class="sxs-lookup"><span data-stu-id="42f66-111">Reentrancy can be configured in an `ActorService`'s settings during registration.</span></span> <span data-ttu-id="42f66-112">configuração de saudação se aplica a instâncias de ator tooall criadas no serviço de ator hello.</span><span class="sxs-lookup"><span data-stu-id="42f66-112">hello setting applies tooall actor instances created in hello actor service.</span></span>

<span data-ttu-id="42f66-113">Olá, exemplo a seguir mostra um serviço de ator que define o modo de reentrada Olá muito`ActorReentrancyMode.Disallowed`.</span><span class="sxs-lookup"><span data-stu-id="42f66-113">hello following example shows an actor service that sets hello reentrancy mode too`ActorReentrancyMode.Disallowed`.</span></span> <span data-ttu-id="42f66-114">Nesse caso, se um ator envia um ator de tooanother reentrante mensagem, uma exceção do tipo `FabricException` será lançada.</span><span class="sxs-lookup"><span data-stu-id="42f66-114">In this case, if an actor sends a reentrant message tooanother actor, an exception of type `FabricException` will be thrown.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="42f66-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="42f66-115">Next steps</span></span>
* <span data-ttu-id="42f66-116">Saiba mais sobre a reentrada em Olá [documentação de referência de API de ator](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span><span class="sxs-lookup"><span data-stu-id="42f66-116">Learn more about reentrancy in hello [Actor API reference documentation](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span></span>
