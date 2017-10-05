---
title: "Reentrada nos microsserviços do Azure baseada em ator | Microsoft Docs"
description: "Introdução à reentrância para Reliable Actors do Service Fabric"
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
ms.openlocfilehash: 00fcccb379bf1ba3875fbaba57a05b00fa228622
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-actors-reentrancy"></a><span data-ttu-id="536a7-103">Reentrância de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="536a7-103">Reliable Actors reentrancy</span></span>
<span data-ttu-id="536a7-104">Por padrão, o tempo de execução do Reliable Actors permite a reentrância baseada no contexto da chamada lógica.</span><span class="sxs-lookup"><span data-stu-id="536a7-104">The Reliable Actors runtime, by default, allows logical call context-based reentrancy.</span></span> <span data-ttu-id="536a7-105">Isso possibilita que os atores sejam reentrantes se estiverem na mesma cadeia de contexto de chamada.</span><span class="sxs-lookup"><span data-stu-id="536a7-105">This allows for actors to be reentrant if they are in the same call context chain.</span></span> <span data-ttu-id="536a7-106">Por exemplo, se um Ator A envia a mensagem para o Ator B, que envia a mensagem para o Ator C. Como parte do processamento da mensagem no caso de o Ator C chamar o Ator A, a mensagem é reentrante e por isso será permitida.</span><span class="sxs-lookup"><span data-stu-id="536a7-106">For example, Actor A sends a message to Actor B, who sends a message to Actor C. As part of the message processing, if Actor C calls Actor A, the message is reentrant, so it will be allowed.</span></span> <span data-ttu-id="536a7-107">Todas as outras mensagens que fazem parte de um contexto de chamada diferente serão bloqueadas no Ator A até a conclusão do processamento.</span><span class="sxs-lookup"><span data-stu-id="536a7-107">Any other messages that are part of a different call context will be blocked on Actor A until it finishes processing.</span></span>

<span data-ttu-id="536a7-108">Há duas opções disponíveis para nova entrada de ator definida na enumeração `ActorReentrancyMode` :</span><span class="sxs-lookup"><span data-stu-id="536a7-108">There are two options available for actor reentrancy defined in the `ActorReentrancyMode` enum:</span></span>

* <span data-ttu-id="536a7-109">`LogicalCallContext` (comportamento padrão)</span><span class="sxs-lookup"><span data-stu-id="536a7-109">`LogicalCallContext` (default behavior)</span></span>
* <span data-ttu-id="536a7-110">`Disallowed` - desabilita a nova entrada</span><span class="sxs-lookup"><span data-stu-id="536a7-110">`Disallowed` - disables reentrancy</span></span>

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
<span data-ttu-id="536a7-111">A nova entrada pode ser definida nas configurações de `ActorService`durante o registro.</span><span class="sxs-lookup"><span data-stu-id="536a7-111">Reentrancy can be configured in an `ActorService`'s settings during registration.</span></span> <span data-ttu-id="536a7-112">A configuração se aplica a todas as instâncias de ator criadas no serviço de ator.</span><span class="sxs-lookup"><span data-stu-id="536a7-112">The setting applies to all actor instances created in the actor service.</span></span>

<span data-ttu-id="536a7-113">O exemplo a seguir mostra um serviço de ator que define o modo de nova entrada como `ActorReentrancyMode.Disallowed`.</span><span class="sxs-lookup"><span data-stu-id="536a7-113">The following example shows an actor service that sets the reentrancy mode to `ActorReentrancyMode.Disallowed`.</span></span> <span data-ttu-id="536a7-114">Nesse caso, se um ator envia uma mensagem reentrante para outro ator, será lançada uma exceção do tipo `FabricException` .</span><span class="sxs-lookup"><span data-stu-id="536a7-114">In this case, if an actor sends a reentrant message to another actor, an exception of type `FabricException` will be thrown.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="536a7-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="536a7-115">Next steps</span></span>
* <span data-ttu-id="536a7-116">Saiba mais sobre a reentrada na [Documentação de referência de API de Ator](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span><span class="sxs-lookup"><span data-stu-id="536a7-116">Learn more about reentrancy in the [Actor API reference documentation](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span></span>
