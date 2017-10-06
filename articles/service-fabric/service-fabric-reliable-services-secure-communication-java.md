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
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="f19fb-103">Ajudar a proteger a comunicação para serviços no Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f19fb-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f19fb-104">C# em Windows</span><span class="sxs-lookup"><span data-stu-id="f19fb-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="f19fb-105">Java no Linux</span><span class="sxs-lookup"><span data-stu-id="f19fb-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="f19fb-106">Ajudar a proteger um serviço quando você estiver usando a comunicação remota de serviço</span><span class="sxs-lookup"><span data-stu-id="f19fb-106">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="f19fb-107">Usaremos uma existente [exemplo](service-fabric-reliable-services-communication-remoting-java.md) que explica como tooset a conexão remota para serviços confiáveis.</span><span class="sxs-lookup"><span data-stu-id="f19fb-107">We'll be using an existing [example](service-fabric-reliable-services-communication-remoting-java.md) that explains how tooset up remoting for reliable services.</span></span> <span data-ttu-id="f19fb-108">toohelp proteger um serviço quando você estiver usando a comunicação remota do serviço, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="f19fb-108">toohelp secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="f19fb-109">Criar uma interface `HelloWorldStateless`, que define os métodos de saudação que estarão disponíveis para uma chamada de procedimento remoto em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="f19fb-109">Create an interface, `HelloWorldStateless`, that defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="f19fb-110">O serviço usará `FabricTransportServiceRemotingListener`, que é declarada no hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` pacote.</span><span class="sxs-lookup"><span data-stu-id="f19fb-110">Your service will use `FabricTransportServiceRemotingListener`, which is declared in hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` package.</span></span> <span data-ttu-id="f19fb-111">Esta é uma implementação de `CommunicationListener` que fornece recursos de comunicação remota.</span><span class="sxs-lookup"><span data-stu-id="f19fb-111">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span>

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
2. <span data-ttu-id="f19fb-112">Adicionar credenciais de segurança e configurações de ouvinte.</span><span class="sxs-lookup"><span data-stu-id="f19fb-112">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="f19fb-113">Verifique se esse certificado Olá que você deseja toohelp toouse segura que a comunicação de serviço é instalada em todos os nós Olá cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f19fb-113">Make sure that hello certificate that you want toouse toohelp secure your service communication is installed on all hello nodes in hello cluster.</span></span> <span data-ttu-id="f19fb-114">Há duas maneiras de fornecer configurações de ouvinte e credenciais de segurança:</span><span class="sxs-lookup"><span data-stu-id="f19fb-114">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="f19fb-115">Fornecê-las usando um [pacote de configuração](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="f19fb-115">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="f19fb-116">Adicionar um `TransportSettings` seção no arquivo settings.xml de saudação.</span><span class="sxs-lookup"><span data-stu-id="f19fb-116">Add a `TransportSettings` section in hello settings.xml file.</span></span>

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

       <span data-ttu-id="f19fb-117">Nesse caso, Olá `createServiceInstanceListeners` método terá esta aparência:</span><span class="sxs-lookup"><span data-stu-id="f19fb-117">In this case, hello `createServiceInstanceListeners` method will look like this:</span></span>

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        <span data-ttu-id="f19fb-118">Se você adicionar um `TransportSettings` seção no arquivo de settings.xml Olá sem qualquer prefixo `FabricTransportListenerSettings` carregar todas as configurações de saudação desta seção por padrão.</span><span class="sxs-lookup"><span data-stu-id="f19fb-118">If you add a `TransportSettings` section in hello settings.xml file without any prefix, `FabricTransportListenerSettings` will load all hello settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="f19fb-119">Nesse caso, Olá `CreateServiceInstanceListeners` método terá esta aparência:</span><span class="sxs-lookup"><span data-stu-id="f19fb-119">In this case, hello `CreateServiceInstanceListeners` method will look like this:</span></span>

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. <span data-ttu-id="f19fb-120">Quando você chama métodos em um serviço protegido usando a pilha de comunicação remota do hello, em vez de usar o hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` toocreate classe um proxy do serviço, use `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="f19fb-120">When you call methods on a secured service by using hello remoting stack, instead of using hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class toocreate a service proxy, use `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span></span>

    <span data-ttu-id="f19fb-121">Se o código de saudação do cliente é executado como parte de um serviço, você poderá carregar `FabricTransportSettings` do arquivo de settings.xml hello.</span><span class="sxs-lookup"><span data-stu-id="f19fb-121">If hello client code is running as part of a service, you can load `FabricTransportSettings` from hello settings.xml file.</span></span> <span data-ttu-id="f19fb-122">Crie uma seção de TransportSettings que é o código de serviço toohello semelhantes, conforme mostrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f19fb-122">Create a TransportSettings section that is similar toohello service code, as shown earlier.</span></span> <span data-ttu-id="f19fb-123">Verifique Olá alterações toohello cliente código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f19fb-123">Make hello following changes toohello client code:</span></span>

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
