---
title: "comunicação remota do aaaService no Azure Service Fabric | Microsoft Docs"
description: "Comunicação remota do Service Fabric permite que os clientes e serviços toocommunicate com serviços usando uma chamada de procedimento remoto."
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/30/2017
ms.author: pakunapa
ms.openlocfilehash: 1177a5ede91352dc61422f2df7424b0d5645147d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a>Comunicação remota de serviço com o Reliable Services
> [!div class="op_single_selector"]
> * [C# em Windows](service-fabric-reliable-services-communication-remoting.md)
> * [Java no Linux](service-fabric-reliable-services-communication-remoting-java.md)
>
>

Olá confiável Services framework fornece um tooquickly do mecanismo de comunicação remota e configurar com facilidade a chamada de procedimento remoto de serviços.

## <a name="set-up-remoting-on-a-service"></a>Configurar a comunicação remota em um serviço
A configuração da comunicação remota de um serviço é feita em duas etapas simples:

1. Crie uma interface para o serviço tooimplement. Essa interface define os métodos de saudação que estão disponíveis para uma chamada de procedimento remoto em seu serviço. métodos de saudação devem ser retorno métodos assíncronos. interface Olá deve implementar `microsoft.serviceFabric.services.remoting.Service` toosignal que Olá serviço tem uma interface de comunicação remota.
2. Use um ouvinte de comunicação remota em seu serviço. Esta é uma implementação de `CommunicationListener` que fornece recursos de comunicação remota. `FabricTransportServiceRemotingListener`pode ser usado toocreate um ouvinte de comunicação remota usando o protocolo de transporte de comunicação remota saudação padrão.

Por exemplo, hello seguinte serviço sem monitoração de estado expõe um único método tooget "Hello World" passar por uma chamada de procedimento remoto.

```java
import java.util.ArrayList;
import java.util.concurrent.CompletableFuture;
import java.util.List;
import microsoft.servicefabric.services.communication.runtime.ServiceInstanceListener;
import microsoft.servicefabric.services.remoting.Service;
import microsoft.servicefabric.services.runtime.StatelessService;

public interface MyService extends Service {
    CompletableFuture<String> helloWorldAsync();
}

class MyServiceImpl extends StatelessService implements MyService {
    public MyServiceImpl(StatelessServiceContext context) {
       super(context);
    }

    public CompletableFuture<String> helloWorldAsync() {
        return CompletableFuture.completedFuture("Hello!");
    }

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
        listeners.add(new ServiceInstanceListener((context) -> {
            return new FabricTransportServiceRemotingListener(context,this);
        }));
        return listeners;
    }
}
```

> [!NOTE]
> Olá e argumentos Olá retornam tipos na interface de serviço Olá podem ser qualquer tipo simple, complexo ou personalizado, mas eles devem ser serializáveis.
>
>

## <a name="call-remote-service-methods"></a>Chamar métodos de serviços remotos
Chamar métodos em um serviço usando a pilha de comunicação remota Olá é feito por meio de um serviço de toohello de proxy local por meio de saudação `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` classe. Olá `ServiceProxyBase` método cria um proxy local usando Olá mesma interface que Olá serviço implementa. Com o proxy, você pode simplesmente chamar métodos na interface Olá remotamente.

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

estrutura de comunicação remota Olá propaga exceções geradas no cliente do serviço de saudação toohello. Lógica de tratamento de exceção assim no cliente hello usando `ServiceProxyBase` diretamente pode lidar com exceções que Olá lança de serviço.

## <a name="service-proxy-lifetime"></a>Tempo de vida de Proxy do Serviço
A criação do ServiceProxy é uma operação simples, logo, o usuário pode criar quantos precisar. O Proxy do Serviço pode ser reutilizado desde que o usuário precise. Usuário possa reutilizar Olá proxy mesmo em caso de exceção. Cada ServiceProxy contém mensagens de toosend de cliente usado de comunicação durante transmissão hello. Ao chamar a API, temos toosee verificação interna, se o cliente de comunicação usado é válido. Com base no resultado, podemos criar novamente cliente de comunicação de saudação. Portanto, o usuário não precisa serviceproxy toorecreate em caso de exceção.

### <a name="serviceproxyfactory-lifetime"></a>Tempo de vida de ServiceProxyFactory
[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) é um alocador que cria um proxy para interfaces remotas diferentes. Se você usar a API `ServiceProxyBase.create` para criar um proxy, o framework cria um `FabricServiceProxyFactory`.
É útil toocreate um manualmente quando precisar toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) propriedades.
Alocador é uma operação cara. `FabricServiceProxyFactory` mantém o cache dos clientes de comunicação.
A prática recomendada é toocache `FabricServiceProxyFactory` por tempo possível.

## <a name="remoting-exception-handling"></a>Tratamento de exceções remotas
Todos os Olá remoto exceção pela API de serviço, são enviadas como RuntimeException ou FabricException toohello back cliente.

ServiceProxy lidar com todas as exceções de Failover para a partição de serviço de hello, ele é criado para. Novamente, ele resolve os pontos de extremidade de saudação se houver Failover Exceptions(Non-Transient Exceptions) e repetições chamada hello com ponto de extremidade correto hello. O número de tentativas da exceção de failover é indefinido.
No caso de TransientExceptions, ele repete apenas chamada hello.

Os parâmetros de repetição padrão são fornecidos por [OperationRetrySettings]. (https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) Usuário pode configurar esses valores, passando o construtor de tooServiceProxyFactory OperationRetrySettings objeto.

## <a name="next-steps"></a>Próximas etapas
* [Securing communication for Reliable Services](service-fabric-reliable-services-secure-communication.md)
