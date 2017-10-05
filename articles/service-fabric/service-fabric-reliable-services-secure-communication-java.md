---
title: "Ajudar a proteger a comunicação para serviços no Azure Service Fabric | Microsoft Docs"
description: "Visão geral de como ajudar a proteger a comunicação para os Reliable Services executados em um cluster do Azure Service Fabric."
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
ms.openlocfilehash: c4634e3d8efb1745fffcfe3e647e43d867038716
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="dd27d-103">Ajudar a proteger a comunicação para serviços no Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="dd27d-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dd27d-104">C# em Windows</span><span class="sxs-lookup"><span data-stu-id="dd27d-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="dd27d-105">Java no Linux</span><span class="sxs-lookup"><span data-stu-id="dd27d-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="dd27d-106">Ajudar a proteger um serviço quando você estiver usando a comunicação remota de serviço</span><span class="sxs-lookup"><span data-stu-id="dd27d-106">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="dd27d-107">Usaremos um [exemplo](service-fabric-reliable-services-communication-remoting-java.md) existente que explica como configurar a comunicação remota para os Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="dd27d-107">We'll be using an existing [example](service-fabric-reliable-services-communication-remoting-java.md) that explains how to set up remoting for reliable services.</span></span> <span data-ttu-id="dd27d-108">Para ajudar a proteger um serviço quando você estiver usando a comunicação remota de serviço, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="dd27d-108">To help secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="dd27d-109">Crie uma interface, `HelloWorldStateless`, que define os métodos que estarão disponíveis para chamada de procedimento remoto no seu serviço.</span><span class="sxs-lookup"><span data-stu-id="dd27d-109">Create an interface, `HelloWorldStateless`, that defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="dd27d-110">Seu serviço usará `FabricTransportServiceRemotingListener`, declarado no pacote do `microsoft.serviceFabric.services.remoting.fabricTransport.runtime`.</span><span class="sxs-lookup"><span data-stu-id="dd27d-110">Your service will use `FabricTransportServiceRemotingListener`, which is declared in the `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` package.</span></span> <span data-ttu-id="dd27d-111">Esta é uma implementação de `CommunicationListener` que fornece recursos de comunicação remota.</span><span class="sxs-lookup"><span data-stu-id="dd27d-111">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span>

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
2. <span data-ttu-id="dd27d-112">Adicionar credenciais de segurança e configurações de ouvinte.</span><span class="sxs-lookup"><span data-stu-id="dd27d-112">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="dd27d-113">Certifique-se de que o certificado que você deseja usar para ajudar proteger a comunicação do serviço esteja instalado em todos os nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="dd27d-113">Make sure that the certificate that you want to use to help secure your service communication is installed on all the nodes in the cluster.</span></span> <span data-ttu-id="dd27d-114">Há duas maneiras de fornecer configurações de ouvinte e credenciais de segurança:</span><span class="sxs-lookup"><span data-stu-id="dd27d-114">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="dd27d-115">Fornecê-las usando um [pacote de configuração](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="dd27d-115">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="dd27d-116">Adicione uma seção `TransportSettings` ao arquivo settings.xml.</span><span class="sxs-lookup"><span data-stu-id="dd27d-116">Add a `TransportSettings` section in the settings.xml file.</span></span>

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

       <span data-ttu-id="dd27d-117">Nesse caso, o método `createServiceInstanceListeners` terá esta aparência:</span><span class="sxs-lookup"><span data-stu-id="dd27d-117">In this case, the `createServiceInstanceListeners` method will look like this:</span></span>

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        <span data-ttu-id="dd27d-118">Se você adicionar uma seção `TransportSettings` ao arquivo settings.xml sem nenhum prefixo, `FabricTransportListenerSettings` carregará todas as configurações dessa seção por padrão.</span><span class="sxs-lookup"><span data-stu-id="dd27d-118">If you add a `TransportSettings` section in the settings.xml file without any prefix, `FabricTransportListenerSettings` will load all the settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="dd27d-119">Nesse caso, o método `CreateServiceInstanceListeners` terá esta aparência:</span><span class="sxs-lookup"><span data-stu-id="dd27d-119">In this case, the `CreateServiceInstanceListeners` method will look like this:</span></span>

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. <span data-ttu-id="dd27d-120">Ao chamar métodos em um serviço protegido usando a pilha de comunicação remota, em vez de usar a classe `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` para criar um proxy de serviço, use `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="dd27d-120">When you call methods on a secured service by using the remoting stack, instead of using the `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class to create a service proxy, use `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span></span>

    <span data-ttu-id="dd27d-121">Se o código cliente estiver sendo executado como parte de um serviço, você poderá carregar `FabricTransportSettings` do arquivo settings.xml.</span><span class="sxs-lookup"><span data-stu-id="dd27d-121">If the client code is running as part of a service, you can load `FabricTransportSettings` from the settings.xml file.</span></span> <span data-ttu-id="dd27d-122">Crie uma seção TransportSettings semelhante ao código de serviço, conforme mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="dd27d-122">Create a TransportSettings section that is similar to the service code, as shown earlier.</span></span> <span data-ttu-id="dd27d-123">Faça as alterações a seguir no código cliente:</span><span class="sxs-lookup"><span data-stu-id="dd27d-123">Make the following changes to the client code:</span></span>

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
