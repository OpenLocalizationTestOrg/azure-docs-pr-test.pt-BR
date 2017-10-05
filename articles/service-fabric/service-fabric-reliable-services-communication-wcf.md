---
title: "Pilha de comunicação WCF do Reliable Services | Microsoft Docs"
description: "A comunicação de serviço WCF interna no Service Fabric fornece a comunicação WCF cliente-serviço para o Reliable Services."
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
ms.openlocfilehash: 7037620ebdc26a9f18531064bf45d058f5060e39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="wcf-based-communication-stack-for-reliable-services"></a><span data-ttu-id="78668-103">Pilha de comunicação baseada no WCF para Reliable Services</span><span class="sxs-lookup"><span data-stu-id="78668-103">WCF-based communication stack for Reliable Services</span></span>
<span data-ttu-id="78668-104">A estrutura de Serviços confiáveis permite que os autores do serviço escolham qual pilha de comunicação desejam usar para seu serviço.</span><span class="sxs-lookup"><span data-stu-id="78668-104">The Reliable Services framework allows service authors to choose the communication stack that they want to use for their service.</span></span> <span data-ttu-id="78668-105">Eles podem ligar a pilha de comunicação de sua escolha por meio do **ICommunicationListener** retornado dos métodos [CreateServiceReplicaListeners ou CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) .</span><span class="sxs-lookup"><span data-stu-id="78668-105">They can plug in the communication stack of their choice via the **ICommunicationListener** returned from the [CreateServiceReplicaListeners or CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methods.</span></span> <span data-ttu-id="78668-106">A estrutura fornece uma implementação da pilha de comunicação baseada no WCF (Windows Communication Foundation) da pilha de comunicação para autores de serviço que desejam usar comunicação baseada no WCF.</span><span class="sxs-lookup"><span data-stu-id="78668-106">The framework provides an implementation of the communication stack based on the Windows Communication Foundation (WCF) for service authors who want to use WCF-based communication.</span></span>

## <a name="wcf-communication-listener"></a><span data-ttu-id="78668-107">Ouvinte de comunicação do WCF</span><span class="sxs-lookup"><span data-stu-id="78668-107">WCF Communication Listener</span></span>
<span data-ttu-id="78668-108">A implementação específica do WCF do **ICommunicationListener** é fornecida pela classe **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener**.</span><span class="sxs-lookup"><span data-stu-id="78668-108">The WCF-specific implementation of **ICommunicationListener** is provided by the **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** class.</span></span>

<span data-ttu-id="78668-109">Digamos que temos um contrato de serviço do tipo `ICalculator`</span><span class="sxs-lookup"><span data-stu-id="78668-109">Lest say we have a service contract of type `ICalculator`</span></span>

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

<span data-ttu-id="78668-110">Podemos criar um ouvinte de comunicação do WCF no serviço da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="78668-110">We can create a WCF communication listener in the service the following manner.</span></span>

```csharp

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[] { new ServiceReplicaListener((context) =>
        new WcfCommunicationListener<ICalculator>(
            wcfServiceObject:this,
            serviceContext:context,
            //
            // The name of the endpoint configured in the ServiceManifest under the Endpoints section
            // that identifies the endpoint that the WCF ServiceHost should listen on.
            //
            endpointResourceName: "WcfServiceEndpoint",

            //
            // Populate the binding information that you want the service to use.
            //
            listenerBinding: WcfUtility.CreateTcpListenerBinding()
        )
    )};
}

```

## <a name="writing-clients-for-the-wcf-communication-stack"></a><span data-ttu-id="78668-111">Desenvolvimento de clientes para a pilha de comunicação do WCF</span><span class="sxs-lookup"><span data-stu-id="78668-111">Writing clients for the WCF communication stack</span></span>
<span data-ttu-id="78668-112">Para o desenvolvimento de clientes que se comuniquem com serviços usando o WCF, a estrutura fornece **WcfClientCommunicationFactory**, que é a implementação específica do WCF do [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="78668-112">For writing clients to communicate with services by using WCF, the framework provides **WcfClientCommunicationFactory**, which is the WCF-specific implementation of [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span></span>

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

<span data-ttu-id="78668-113">O canal de comunicação do WCF pode ser acessado do **WcfCommunicationClient** criado pelo **WcfCommunicationClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="78668-113">The WCF communication channel can be accessed from the **WcfCommunicationClient** created by the **WcfCommunicationClientFactory**.</span></span>

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

<span data-ttu-id="78668-114">O código do cliente pode usar o **WcfCommunicationClientFactory** com o **WcfCommunicationClient** que implementa o **ServicePartitionClient** para determinar o ponto de extremidade de serviço e se comunicar com o serviço.</span><span class="sxs-lookup"><span data-stu-id="78668-114">Client code can use the **WcfCommunicationClientFactory** along with the **WcfCommunicationClient** which implements **ServicePartitionClient** to determine the service endpoint and communicate with the service.</span></span>

```csharp
// Create binding
Binding binding = WcfUtility.CreateTcpClientBinding();
// Create a partition resolver
IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();
// create a  WcfCommunicationClientFactory object.
var wcfClientFactory = new WcfCommunicationClientFactory<ICalculator>
    (clientBinding: binding, servicePartitionResolver: partitionResolver);

//
// Create a client for communicating with the ICalculator service that has been created with the
// Singleton partition scheme.
//
var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
                wcfClientFactory,
                ServiceUri,
                ServicePartitionKey.Singleton);

//
// Call the service to perform the operation.
//
var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
                client => client.Channel.Add(2, 3)).Result;

```
> [!NOTE]
> <span data-ttu-id="78668-115">O ServicePartitionResolver padrão supõe que o cliente está em execução no mesmo cluster que o serviço.</span><span class="sxs-lookup"><span data-stu-id="78668-115">The default ServicePartitionResolver assumes that the client is running in same cluster as the service.</span></span> <span data-ttu-id="78668-116">Se este não for o caso, crie um objeto ServicePartitionResolver e passe os pontos de extremidade de conexão do cluster.</span><span class="sxs-lookup"><span data-stu-id="78668-116">If that is not the case, create a ServicePartitionResolver object and pass in the cluster connection endpoints.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="78668-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="78668-117">Next steps</span></span>
* [<span data-ttu-id="78668-118">Chamada de procedimento remoto com Reliable Services remoto</span><span class="sxs-lookup"><span data-stu-id="78668-118">Remote procedure call with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="78668-119">API Web com OWIN no Reliable Services</span><span class="sxs-lookup"><span data-stu-id="78668-119">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="78668-120">Securing communication for Reliable Services</span><span class="sxs-lookup"><span data-stu-id="78668-120">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)

