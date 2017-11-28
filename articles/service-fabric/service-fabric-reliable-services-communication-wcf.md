---
title: "pilha de comunicação de serviços WCF aaaReliable | Microsoft Docs"
description: "Olá internos comunicação pilha do WCF no serviço de malha fornece comunicação do serviço de cliente WCF para serviços confiáveis."
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 75516e1e-ee57-4bc7-95fe-71ec42d452b2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/07/2017
ms.author: bharatn
ms.openlocfilehash: 7feebef4d46a6ae66d05129f47f9b5911e82aec9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="wcf-based-communication-stack-for-reliable-services"></a><span data-ttu-id="d8ce7-103">Pilha de comunicação baseada no WCF para Reliable Services</span><span class="sxs-lookup"><span data-stu-id="d8ce7-103">WCF-based communication stack for Reliable Services</span></span>
<span data-ttu-id="d8ce7-104">Serviços confiáveis de saudação estrutura permite que serviço pilha de comunicação autores toochoose Olá que quiserem toouse para seu serviço.</span><span class="sxs-lookup"><span data-stu-id="d8ce7-104">hello Reliable Services framework allows service authors toochoose hello communication stack that they want toouse for their service.</span></span> <span data-ttu-id="d8ce7-105">Eles podem ser conectadas na pilha de comunicação de saudação de sua escolha por meio de saudação **ICommunicationListener** retornado de saudação [CreateServiceReplicaListeners ou CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) métodos.</span><span class="sxs-lookup"><span data-stu-id="d8ce7-105">They can plug in hello communication stack of their choice via hello **ICommunicationListener** returned from hello [CreateServiceReplicaListeners or CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methods.</span></span> <span data-ttu-id="d8ce7-106">estrutura Olá fornece uma implementação da pilha de comunicação de saudação com base em Olá Windows Communication Foundation (WCF) para autores de serviço que deseja toouse comunicação baseada em WCF.</span><span class="sxs-lookup"><span data-stu-id="d8ce7-106">hello framework provides an implementation of hello communication stack based on hello Windows Communication Foundation (WCF) for service authors who want toouse WCF-based communication.</span></span>

## <a name="wcf-communication-listener"></a><span data-ttu-id="d8ce7-107">Ouvinte de comunicação do WCF</span><span class="sxs-lookup"><span data-stu-id="d8ce7-107">WCF Communication Listener</span></span>
<span data-ttu-id="d8ce7-108">implementação de saudação específicas do WCF de **ICommunicationListener** é fornecido pelo Olá **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** classe.</span><span class="sxs-lookup"><span data-stu-id="d8ce7-108">hello WCF-specific implementation of **ICommunicationListener** is provided by hello **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** class.</span></span>

<span data-ttu-id="d8ce7-109">Digamos que temos um contrato de serviço do tipo `ICalculator`</span><span class="sxs-lookup"><span data-stu-id="d8ce7-109">Lest say we have a service contract of type `ICalculator`</span></span>

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

<span data-ttu-id="d8ce7-110">Podemos criar um ouvinte de comunicação WCF em Olá Olá do serviço seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="d8ce7-110">We can create a WCF communication listener in hello service hello following manner.</span></span>

```csharp

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[] { new ServiceReplicaListener((context) =>
        new WcfCommunicationListener<ICalculator>(
            wcfServiceObject:this,
            serviceContext:context,
            //
            // hello name of hello endpoint configured in hello ServiceManifest under hello Endpoints section
            // that identifies hello endpoint that hello WCF ServiceHost should listen on.
            //
            endpointResourceName: "WcfServiceEndpoint",

            //
            // Populate hello binding information that you want hello service toouse.
            //
            listenerBinding: WcfUtility.CreateTcpListenerBinding()
        )
    )};
}

```

## <a name="writing-clients-for-hello-wcf-communication-stack"></a><span data-ttu-id="d8ce7-111">Gravação de clientes para a pilha de comunicação WCF Olá</span><span class="sxs-lookup"><span data-stu-id="d8ce7-111">Writing clients for hello WCF communication stack</span></span>
<span data-ttu-id="d8ce7-112">Para gravar clientes toocommunicate com serviços usando o WCF, framework Olá fornece **WcfClientCommunicationFactory**, que é a implementação Olá específicas do WCF do [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="d8ce7-112">For writing clients toocommunicate with services by using WCF, hello framework provides **WcfClientCommunicationFactory**, which is hello WCF-specific implementation of [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span></span>

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

<span data-ttu-id="d8ce7-113">canal de comunicação WCF Olá pode ser acessado de saudação **WcfCommunicationClient** criado pelo Olá **WcfCommunicationClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="d8ce7-113">hello WCF communication channel can be accessed from hello **WcfCommunicationClient** created by hello **WcfCommunicationClientFactory**.</span></span>

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

<span data-ttu-id="d8ce7-114">Código do cliente pode usar o hello **WcfCommunicationClientFactory** juntamente com hello **WcfCommunicationClient** que implementa **ServicePartitionClient** toodetermine Olá ponto de extremidade de serviço e se comunicar com o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8ce7-114">Client code can use hello **WcfCommunicationClientFactory** along with hello **WcfCommunicationClient** which implements **ServicePartitionClient** toodetermine hello service endpoint and communicate with hello service.</span></span>

```csharp
// Create binding
Binding binding = WcfUtility.CreateTcpClientBinding();
// Create a partition resolver
IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();
// create a  WcfCommunicationClientFactory object.
var wcfClientFactory = new WcfCommunicationClientFactory<ICalculator>
    (clientBinding: binding, servicePartitionResolver: partitionResolver);

//
// Create a client for communicating with hello ICalculator service that has been created with the
// Singleton partition scheme.
//
var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
                wcfClientFactory,
                ServiceUri,
                ServicePartitionKey.Singleton);

//
// Call hello service tooperform hello operation.
//
var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
                client => client.Channel.Add(2, 3)).Result;

```
> [!NOTE]
> <span data-ttu-id="d8ce7-115">padrão Olá ServicePartitionResolver supõe que o cliente hello está sendo executado no mesmo cluster como serviço hello.</span><span class="sxs-lookup"><span data-stu-id="d8ce7-115">hello default ServicePartitionResolver assumes that hello client is running in same cluster as hello service.</span></span> <span data-ttu-id="d8ce7-116">Se este não for Olá caso, crie um objeto de ServicePartitionResolver e passar nos pontos de extremidade de conexão de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d8ce7-116">If that is not hello case, create a ServicePartitionResolver object and pass in hello cluster connection endpoints.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d8ce7-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d8ce7-117">Next steps</span></span>
* [<span data-ttu-id="d8ce7-118">Chamada de procedimento remoto com Reliable Services remoto</span><span class="sxs-lookup"><span data-stu-id="d8ce7-118">Remote procedure call with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="d8ce7-119">API Web com OWIN no Reliable Services</span><span class="sxs-lookup"><span data-stu-id="d8ce7-119">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="d8ce7-120">Securing communication for Reliable Services</span><span class="sxs-lookup"><span data-stu-id="d8ce7-120">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)

