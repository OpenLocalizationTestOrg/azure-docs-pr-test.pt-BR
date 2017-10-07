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
# <a name="wcf-based-communication-stack-for-reliable-services"></a>Pilha de comunicação baseada no WCF para Reliable Services
Serviços confiáveis de saudação estrutura permite que serviço pilha de comunicação autores toochoose Olá que quiserem toouse para seu serviço. Eles podem ser conectadas na pilha de comunicação de saudação de sua escolha por meio de saudação **ICommunicationListener** retornado de saudação [CreateServiceReplicaListeners ou CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) métodos. estrutura Olá fornece uma implementação da pilha de comunicação de saudação com base em Olá Windows Communication Foundation (WCF) para autores de serviço que deseja toouse comunicação baseada em WCF.

## <a name="wcf-communication-listener"></a>Ouvinte de comunicação do WCF
implementação de saudação específicas do WCF de **ICommunicationListener** é fornecido pelo Olá **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** classe.

Digamos que temos um contrato de serviço do tipo `ICalculator`

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

Podemos criar um ouvinte de comunicação WCF em Olá Olá do serviço seguinte maneira.

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

## <a name="writing-clients-for-hello-wcf-communication-stack"></a>Gravação de clientes para a pilha de comunicação WCF Olá
Para gravar clientes toocommunicate com serviços usando o WCF, framework Olá fornece **WcfClientCommunicationFactory**, que é a implementação Olá específicas do WCF do [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

canal de comunicação WCF Olá pode ser acessado de saudação **WcfCommunicationClient** criado pelo Olá **WcfCommunicationClientFactory**.

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

Código do cliente pode usar o hello **WcfCommunicationClientFactory** juntamente com hello **WcfCommunicationClient** que implementa **ServicePartitionClient** toodetermine Olá ponto de extremidade de serviço e se comunicar com o serviço de saudação.

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
> padrão Olá ServicePartitionResolver supõe que o cliente hello está sendo executado no mesmo cluster como serviço hello. Se este não for Olá caso, crie um objeto de ServicePartitionResolver e passar nos pontos de extremidade de conexão de cluster hello.
> 
> 

## <a name="next-steps"></a>Próximas etapas
* [Chamada de procedimento remoto com Reliable Services remoto](service-fabric-reliable-services-communication-remoting.md)
* [API Web com OWIN no Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Securing communication for Reliable Services](service-fabric-reliable-services-secure-communication.md)

