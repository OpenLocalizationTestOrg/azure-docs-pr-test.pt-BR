---
title: "uma comunicação segura para os serviços no Azure Service Fabric aaaHelp | Microsoft Docs"
description: "Visão geral de como toohelp proteger a comunicação de serviços confiáveis que estão em execução em um cluster do Azure Service Fabric."
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
ms.openlocfilehash: 14db54d50c35478c1f2c156de0dba36f1427c8cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a>Ajudar a proteger a comunicação para serviços no Azure Service Fabric
> [!div class="op_single_selector"]
> * [C# em Windows](service-fabric-reliable-services-secure-communication.md)
> * [Java no Linux](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a>Ajudar a proteger um serviço quando você estiver usando a comunicação remota de serviço
Usaremos uma existente [exemplo](service-fabric-reliable-services-communication-remoting-java.md) que explica como tooset a conexão remota para serviços confiáveis. toohelp proteger um serviço quando você estiver usando a comunicação remota do serviço, siga estas etapas:

1. Criar uma interface `HelloWorldStateless`, que define os métodos de saudação que estarão disponíveis para uma chamada de procedimento remoto em seu serviço. O serviço usará `FabricTransportServiceRemotingListener`, que é declarada no hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` pacote. Esta é uma implementação de `CommunicationListener` que fornece recursos de comunicação remota.

    ```java
    public interface HelloWorldStateless extends Service {
        CompletableFuture<String> getHelloWorld();
    }

    class HelloWorldStatelessImpl extends StatelessService implements HelloWorldStateless {
        @Override
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
        return listeners;
        }

        public CompletableFuture<String> getHelloWorld() {
            return CompletableFuture.completedFuture("Hello World!");
        }
    }
    ```
2. Adicionar credenciais de segurança e configurações de ouvinte.

    Verifique se esse certificado Olá que você deseja toohelp toouse segura que a comunicação de serviço é instalada em todos os nós Olá cluster hello. Há duas maneiras de fornecer configurações de ouvinte e credenciais de segurança:

   1. Fornecê-las usando um [pacote de configuração](service-fabric-application-model.md):

       Adicionar um `TransportSettings` seção no arquivo settings.xml de saudação.

       ```xml
       <!--Section name should always end with "TransportSettings".-->
       <!--Here we are using a prefix "HelloWorldStateless".-->
        <Section Name="HelloWorldStatelessTransportSettings">
            <Parameter Name="MaxMessageSize" Value="10000000" />
            <Parameter Name="SecurityCredentialsType" Value="X509_2" />
            <Parameter Name="CertificatePath" Value="/path/to/cert/BD1C71E248B8C6834C151174DECDBDC02DE1D954.crt" />
            <Parameter Name="CertificateProtectionLevel" Value="EncryptandSign" />
            <Parameter Name="CertificateRemoteThumbprints" Value="BD1C71E248B8C6834C151174DECDBDC02DE1D954" />
        </Section>

       ```

       Nesse caso, Olá `createServiceInstanceListeners` método terá esta aparência:

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        Se você adicionar um `TransportSettings` seção no arquivo de settings.xml Olá sem qualquer prefixo `FabricTransportListenerSettings` carregar todas as configurações de saudação desta seção por padrão.

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        Nesse caso, Olá `CreateServiceInstanceListeners` método terá esta aparência:

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. Quando você chama métodos em um serviço protegido usando a pilha de comunicação remota do hello, em vez de usar o hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` toocreate classe um proxy do serviço, use `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.

    Se o código de saudação do cliente é executado como parte de um serviço, você poderá carregar `FabricTransportSettings` do arquivo de settings.xml hello. Crie uma seção de TransportSettings que é o código de serviço toohello semelhantes, conforme mostrado anteriormente. Verifique Olá alterações toohello cliente código a seguir:

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
