---
title: "comunicação remota do aaaService na malha do serviço | Microsoft Docs"
description: "Comunicação remota do Service Fabric permite que os clientes e serviços toocommunicate com serviços usando uma chamada de procedimento remoto."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: abfaf430-fea0-4974-afba-cfc9f9f2354b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: vturecek
ms.openlocfilehash: 14682cf8671a85e04144eccf97803ab67c258875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a>Comunicação remota de serviço com o Reliable Services
Para serviços que não são vinculados tooa protocolo de comunicação específica ou a pilha, como WebAPI, Windows Communication Foundation (WCF) ou outras pessoas, Olá confiável Services framework fornece um tooquickly do mecanismo de comunicação remota e configurar com facilidade a chamada de procedimento remoto para serviços.

## <a name="set-up-remoting-on-a-service"></a>Configurar a comunicação remota em um serviço
A configuração da comunicação remota de um serviço é feita em duas etapas simples:

1. Crie uma interface para o serviço tooimplement. Essa interface define os métodos de saudação que estarão disponíveis para uma chamada de procedimento remoto em seu serviço. métodos de saudação devem ser retorno métodos assíncronos. interface Olá deve implementar `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal que Olá serviço tem uma interface de comunicação remota.
2. Use um ouvinte de comunicação remota em seu serviço. Esta é uma implementação de `ICommunicationListener` que fornece recursos de comunicação remota. Olá `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contém um método de extensão`CreateServiceRemotingListener` para com e sem monitoração de serviços que pode ser usado toocreate um ouvinte de comunicação remota usando protocolo de transporte de comunicação remota saudação padrão.

Observação: Olá `Remoting` namespace está disponível como um pacote do nuget separado chamado`Microsoft.ServiceFabric.Services.Remoting` 

Por exemplo, hello seguinte serviço sem monitoração de estado expõe um único método tooget "Hello World" passar por uma chamada de procedimento remoto.

```csharp
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Remoting;
using Microsoft.ServiceFabric.Services.Remoting.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

public interface IMyService : IService
{
    Task<string> HelloWorldAsync();
}

class MyService : StatelessService, IMyService
{
    public MyService(StatelessServiceContext context)
        : base (context)
    {
    }

    public Task HelloWorldAsync()
    {
        return Task.FromResult("Hello!");
    }

    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] { new ServiceInstanceListener(context =>            this.CreateServiceRemotingListener(context)) };
    }
}
```
> [!NOTE]
> Olá argumentos e hello retornam tipos na interface de serviço Olá podem ser quaisquer tipos simples, complexos ou personalizados, mas eles devem ser serializáveis por Olá .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).
>
>

## <a name="call-remote-service-methods"></a>Chamar métodos de serviços remotos
Chamar métodos em um serviço usando a pilha de comunicação remota Olá é feito por meio de um serviço de toohello de proxy local por meio de saudação `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` classe. Olá `ServiceProxy` método cria um proxy local usando Olá mesma interface que Olá serviço implementa. Com o proxy, você pode simplesmente chamar métodos na interface Olá remotamente.

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

estrutura de comunicação remota Olá propaga exceções geradas no cliente do serviço de saudação toohello. Lógica de tratamento de exceção assim no cliente hello usando `ServiceProxy` diretamente pode lidar com exceções que Olá lança de serviço.

## <a name="service-proxy-lifetime"></a>Tempo de vida de Proxy do Serviço
A criação do ServiceProxy é uma operação simples, logo, o usuário pode criar quantos precisar. O Proxy do Serviço pode ser reutilizado desde que o usuário precise. Usuário possa reutilizar Olá proxy mesmo em caso de exceção. Cada ServiceProxy contém mensagens de toosend de cliente usado de comunicação durante transmissão hello. Ao chamar a API, temos toosee verificação interna, se o cliente de comunicação usado é válido. Com base no resultado, podemos criar novamente cliente de comunicação de saudação. Portanto, o usuário não precisa serviceproxy toorecreate em caso de exceção.

### <a name="serviceproxyfactory-lifetime"></a>Tempo de vida de ServiceProxyFactory
[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) é um alocador que cria um proxy para interfaces remotas diferentes. Se você usar a API ServiceProxy.Create para criar um proxy, o framework cria Olá singelton ServiceProxyFactory.
É útil toocreate um manualmente quando precisar toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) propriedades.
Alocador é uma operação cara. ServiceProxyFactory mantém o cache do cliente de comunicação.
Prática recomendada é toocache ServiceProxyFactory por tempo possível.

## <a name="remoting-exception-handling"></a>Tratamento de exceções remotas
Todos os Olá remoto exceção pela API de serviço são enviados toohello back cliente como AggregateException. RemoteExceptions devem ser serializáveis DataContract [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) gerada toohello proxy API com o erro de serialização Olá nele.

ServiceProxy lidar com todas as exceções de Failover para a partição de serviço de hello, ele é criado para. Novamente, ele resolve os pontos de extremidade de saudação se houver Failover Exceptions(Non-Transient Exceptions) e repetições chamada hello com ponto de extremidade correto hello. O número de tentativas da exceção de failover é indefinido.
No caso de TransientExceptions, ele repete apenas chamada hello.

Os parâmetros de repetição padrão são fornecidos por [OperationRetrySettings]. (https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Usuário pode configurar esses valores, passando o construtor de tooServiceProxyFactory OperationRetrySettings objeto.

## <a name="next-steps"></a>Próximas etapas
* [API Web com OWIN no Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Comunicação WCF com o Reliable Services](service-fabric-reliable-services-communication-wcf.md)
* [Securing communication for Reliable Services](service-fabric-reliable-services-secure-communication.md)
