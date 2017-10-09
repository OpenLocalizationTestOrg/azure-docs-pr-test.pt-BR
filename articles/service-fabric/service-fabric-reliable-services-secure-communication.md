---
title: "uma comunicação segura para os serviços no Azure Service Fabric aaaHelp | Microsoft Docs"
description: "Visão geral de como toohelp proteger a comunicação de serviços confiáveis que estão em execução em um cluster do Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: vturecek
ms.assetid: fc129c1a-fbe4-4339-83ae-0e69a41654e0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: 15201eb503322b17db329b319f1f42860b0f0c6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="1be03-103">Ajudar a proteger a comunicação para serviços no Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1be03-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1be03-104">C# em Windows</span><span class="sxs-lookup"><span data-stu-id="1be03-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="1be03-105">Java no Linux</span><span class="sxs-lookup"><span data-stu-id="1be03-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

<span data-ttu-id="1be03-106">A segurança é um dos aspectos mais importantes de saudação de comunicação.</span><span class="sxs-lookup"><span data-stu-id="1be03-106">Security is one of hello most important aspects of communication.</span></span> <span data-ttu-id="1be03-107">estrutura de aplicativo de serviços confiáveis Olá fornece algumas pilhas de comunicação pré-compilada e ferramentas que você pode usar segurança tooimprove.</span><span class="sxs-lookup"><span data-stu-id="1be03-107">hello Reliable Services application framework provides a few prebuilt communication stacks and tools that you can use tooimprove security.</span></span> <span data-ttu-id="1be03-108">Este artigo fala sobre como tooimprove segurança quando você estiver usando o serviço remoto e Olá pilha de comunicação do Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="1be03-108">This article talks about how tooimprove security when you're using service remoting and hello Windows Communication Foundation (WCF) communication stack.</span></span>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="1be03-109">Ajudar a proteger um serviço quando você estiver usando a comunicação remota de serviço</span><span class="sxs-lookup"><span data-stu-id="1be03-109">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="1be03-110">Estamos usando uma existente [exemplo](service-fabric-reliable-services-communication-remoting.md) que explica como tooset a conexão remota para serviços confiáveis.</span><span class="sxs-lookup"><span data-stu-id="1be03-110">We are using an existing [example](service-fabric-reliable-services-communication-remoting.md) that explains how tooset up remoting for reliable services.</span></span> <span data-ttu-id="1be03-111">toohelp proteger um serviço quando você estiver usando a comunicação remota do serviço, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="1be03-111">toohelp secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="1be03-112">Criar uma interface `IHelloWorldStateful`, que define os métodos de saudação que estarão disponíveis para uma chamada de procedimento remoto em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="1be03-112">Create an interface, `IHelloWorldStateful`, that defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="1be03-113">O serviço usará `FabricTransportServiceRemotingListener`, que é declarada no hello `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` namespace.</span><span class="sxs-lookup"><span data-stu-id="1be03-113">Your service will use `FabricTransportServiceRemotingListener`, which is declared in hello `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` namespace.</span></span> <span data-ttu-id="1be03-114">Esta é uma implementação de `ICommunicationListener` que fornece recursos de comunicação remota.</span><span class="sxs-lookup"><span data-stu-id="1be03-114">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span>

    ```csharp
    public interface IHelloWorldStateful : IService
    {
        Task<string> GetHelloWorld();
    }

    internal class HelloWorldStateful : StatefulService, IHelloWorldStateful
    {
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]{
                    new ServiceReplicaListener(
                        (context) => new FabricTransportServiceRemotingListener(context,this))};
        }

        public Task<string> GetHelloWorld()
        {
            return Task.FromResult("Hello World!");
        }
    }
    ```
2. <span data-ttu-id="1be03-115">Adicionar credenciais de segurança e configurações de ouvinte.</span><span class="sxs-lookup"><span data-stu-id="1be03-115">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="1be03-116">Verifique se esse certificado Olá que você deseja toohelp toouse segura que a comunicação de serviço é instalada em todos os nós Olá cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1be03-116">Make sure that hello certificate that you want toouse toohelp secure your service communication is installed on all hello nodes in hello cluster.</span></span> <span data-ttu-id="1be03-117">Há duas maneiras de fornecer configurações de ouvinte e credenciais de segurança:</span><span class="sxs-lookup"><span data-stu-id="1be03-117">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="1be03-118">Fornecê-los diretamente no código de saudação do serviço:</span><span class="sxs-lookup"><span data-stu-id="1be03-118">Provide them directly in hello service code:</span></span>

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           FabricTransportRemotingListenerSettings  listenerSettings = new FabricTransportRemotingListenerSettings
           {
               MaxMessageSize = 10000000,
               SecurityCredentials = GetSecurityCredentials()
           };
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(context,this,listenerSettings))
           };
       }

       private static SecurityCredentials GetSecurityCredentials()
       {
           // Provide certificate details.
           var x509Credentials = new X509Credentials
           {
               FindType = X509FindType.FindByThumbprint,
               FindValue = "4FEF3950642138446CC364A396E1E881DB76B48C",
               StoreLocation = StoreLocation.LocalMachine,
               StoreName = "My",
               ProtectionLevel = ProtectionLevel.EncryptAndSign
           };
           x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
           x509Credentials.RemoteCertThumbprints.Add("9FEF3950642138446CC364A396E1E881DB76B483");
           return x509Credentials;
       }
       ```
   2. <span data-ttu-id="1be03-119">Fornecê-las usando um [pacote de configuração](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="1be03-119">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="1be03-120">Adicionar um `TransportSettings` seção no arquivo settings.xml de saudação.</span><span class="sxs-lookup"><span data-stu-id="1be03-120">Add a `TransportSettings` section in hello settings.xml file.</span></span>

       ```xml
       <Section Name="HelloWorldStatefulTransportSettings">
           <Parameter Name="MaxMessageSize" Value="10000000" />
           <Parameter Name="SecurityCredentialsType" Value="X509" />
           <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
           <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
           <Parameter Name="CertificateRemoteThumbprints" Value="9FEF3950642138446CC364A396E1E881DB76B483" />
           <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
           <Parameter Name="CertificateStoreName" Value="My" />
           <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
           <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
       </Section>
       ```

       <span data-ttu-id="1be03-121">Nesse caso, Olá `CreateServiceReplicaListeners` método terá esta aparência:</span><span class="sxs-lookup"><span data-stu-id="1be03-121">In this case, hello `CreateServiceReplicaListeners` method will look like this:</span></span>

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(
                       context,this,FabricTransportRemotingListenerSettings .LoadFrom("HelloWorldStatefulTransportSettings")))
           };
       }
       ```

        <span data-ttu-id="1be03-122">Se você adicionar um `TransportSettings` seção no arquivo settings.xml Olá `FabricTransportRemotingListenerSettings ` carregar todas as configurações de saudação desta seção por padrão.</span><span class="sxs-lookup"><span data-stu-id="1be03-122">If you add a `TransportSettings` section in hello settings.xml file , `FabricTransportRemotingListenerSettings ` will load all hello settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="1be03-123">Nesse caso, Olá `CreateServiceReplicaListeners` método terá esta aparência:</span><span class="sxs-lookup"><span data-stu-id="1be03-123">In this case, hello `CreateServiceReplicaListeners` method will look like this:</span></span>

        ```csharp
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]
            {
                return new[]{
                        new ServiceReplicaListener(
                            (context) => new FabricTransportServiceRemotingListener(context,this))};
            };
        }
        ```
3. <span data-ttu-id="1be03-124">Quando você chama métodos em um serviço protegido usando a pilha de comunicação remota do hello, em vez de usar o hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` toocreate classe um proxy do serviço, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="1be03-124">When you call methods on a secured service by using hello remoting stack, instead of using hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class toocreate a service proxy, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span></span> <span data-ttu-id="1be03-125">Passe `FabricTransportRemotingSettings`, que contém `SecurityCredentials`.</span><span class="sxs-lookup"><span data-stu-id="1be03-125">Pass in `FabricTransportRemotingSettings`, which contains `SecurityCredentials`.</span></span>

    ```csharp

    var x509Credentials = new X509Credentials
    {
        FindType = X509FindType.FindByThumbprint,
        FindValue = "9FEF3950642138446CC364A396E1E881DB76B483",
        StoreLocation = StoreLocation.LocalMachine,
        StoreName = "My",
        ProtectionLevel = ProtectionLevel.EncryptAndSign
    };
    x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
    x509Credentials.RemoteCertThumbprints.Add("4FEF3950642138446CC364A396E1E881DB76B48C");

    FabricTransportRemotingSettings transportSettings = new FabricTransportRemotingSettings
    {
        SecurityCredentials = x509Credentials,
    };

    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(transportSettings));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="1be03-126">Se o código de saudação do cliente é executado como parte de um serviço, você poderá carregar `FabricTransportRemotingSettings` do arquivo de settings.xml hello.</span><span class="sxs-lookup"><span data-stu-id="1be03-126">If hello client code is running as part of a service, you can load `FabricTransportRemotingSettings` from hello settings.xml file.</span></span> <span data-ttu-id="1be03-127">Crie uma seção de HelloWorldClientTransportSettings que é o código de serviço toohello semelhantes, conforme mostrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1be03-127">Create a HelloWorldClientTransportSettings section that is similar toohello service code, as shown earlier.</span></span> <span data-ttu-id="1be03-128">Verifique Olá alterações toohello cliente código a seguir:</span><span class="sxs-lookup"><span data-stu-id="1be03-128">Make hello following changes toohello client code:</span></span>

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="1be03-129">Se o cliente Olá não está em execução como parte de um serviço, você pode criar um arquivo de client_name.settings.xml em Olá mesmo local onde client_name.exe hello.</span><span class="sxs-lookup"><span data-stu-id="1be03-129">If hello client is not running as part of a service, you can create a client_name.settings.xml file in hello same location where hello client_name.exe is.</span></span> <span data-ttu-id="1be03-130">Em seguida, crie uma seção TransportSettings nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="1be03-130">Then create a TransportSettings section in that file.</span></span>

    <span data-ttu-id="1be03-131">Serviço toohello semelhante, se você adicionar um `TransportSettings` seção cliente settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` carrega todas as configurações de saudação nesta seção por padrão.</span><span class="sxs-lookup"><span data-stu-id="1be03-131">Similar toohello service, if you add a `TransportSettings` section in client settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` loads all hello settings from this section by default.</span></span>

    <span data-ttu-id="1be03-132">Nesse caso, hello código anterior é ainda mais simplificado:</span><span class="sxs-lookup"><span data-stu-id="1be03-132">In that case, hello earlier code is even further simplified:</span></span>  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a><span data-ttu-id="1be03-133">Ajudar a proteger um serviço quando você estiver usando uma pilha de comunicação baseada em WCF</span><span class="sxs-lookup"><span data-stu-id="1be03-133">Help secure a service when you're using a WCF-based communication stack</span></span>
<span data-ttu-id="1be03-134">Estamos usando uma existente [exemplo](service-fabric-reliable-services-communication-wcf.md) que explica como tooset uma comunicação baseada em WCF de pilha para serviços confiáveis.</span><span class="sxs-lookup"><span data-stu-id="1be03-134">We are using an existing [example](service-fabric-reliable-services-communication-wcf.md) that explains how tooset up a WCF-based communication stack for reliable services.</span></span> <span data-ttu-id="1be03-135">toohelp proteger um serviço quando você estiver usando uma pilha de comunicação WCF, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="1be03-135">toohelp secure a service when you're using a WCF-based communication stack, follow these steps:</span></span>

1. <span data-ttu-id="1be03-136">Para serviço hello, você precisa de ouvinte de comunicação de WCF toohelp Olá seguro (`WcfCommunicationListener`) que você criar.</span><span class="sxs-lookup"><span data-stu-id="1be03-136">For hello service, you need toohelp secure hello WCF communication listener (`WcfCommunicationListener`) that you create.</span></span> <span data-ttu-id="1be03-137">toodo isso, modifique Olá `CreateServiceReplicaListeners` método.</span><span class="sxs-lookup"><span data-stu-id="1be03-137">toodo this, modify hello `CreateServiceReplicaListeners` method.</span></span>

    ```csharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        return new[]
        {
            new ServiceReplicaListener(
                this.CreateWcfCommunicationListener)
        };
    }

    private WcfCommunicationListener<ICalculator> CreateWcfCommunicationListener(StatefulServiceContext context)
    {
       var wcfCommunicationListener = new WcfCommunicationListener<ICalculator>(
            serviceContext:context,
            wcfServiceObject:this,
            // For this example, we will be using NetTcpBinding.
            listenerBinding: GetNetTcpBinding(),
            endpointResourceName:"WcfServiceEndpoint");

        // Add certificate details in hello ServiceHost credentials.
        wcfCommunicationListener.ServiceHost.Credentials.ServiceCertificate.SetCertificate(
            StoreLocation.LocalMachine,
            StoreName.My,
            X509FindType.FindByThumbprint,
            "9DC906B169DC4FAFFD1697AC781E806790749D2F");
        return wcfCommunicationListener;
    }

    private static NetTcpBinding GetNetTcpBinding()
    {
        NetTcpBinding b = new NetTcpBinding(SecurityMode.TransportWithMessageCredential);
        b.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;
        return b;
    }
    ```
2. <span data-ttu-id="1be03-138">No cliente de Olá Olá `WcfCommunicationClient` classe que foi criado no hello anterior [exemplo](service-fabric-reliable-services-communication-wcf.md) permanece inalterado.</span><span class="sxs-lookup"><span data-stu-id="1be03-138">In hello client, hello `WcfCommunicationClient` class that was created in hello previous [example](service-fabric-reliable-services-communication-wcf.md) remains unchanged.</span></span> <span data-ttu-id="1be03-139">Mas você precisa Olá toooverride `CreateClientAsync` método `WcfCommunicationClientFactory`:</span><span class="sxs-lookup"><span data-stu-id="1be03-139">But you need toooverride hello `CreateClientAsync` method of `WcfCommunicationClientFactory`:</span></span>

    ```csharp
    public class SecureWcfCommunicationClientFactory<TServiceContract> : WcfCommunicationClientFactory<TServiceContract> where TServiceContract : class
    {
        private readonly Binding clientBinding;
        private readonly object callbackObject;
        public SecureWcfCommunicationClientFactory(
            Binding clientBinding,
            IEnumerable<IExceptionHandler> exceptionHandlers = null,
            IServicePartitionResolver servicePartitionResolver = null,
            string traceId = null,
            object callback = null)
            : base(clientBinding, exceptionHandlers, servicePartitionResolver,traceId,callback)
        {
            this.clientBinding = clientBinding;
            this.callbackObject = callback;
        }

        protected override Task<WcfCommunicationClient<TServiceContract>> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
        {
            var endpointAddress = new EndpointAddress(new Uri(endpoint));
            ChannelFactory<TServiceContract> channelFactory;
            if (this.callbackObject != null)
            {
                channelFactory = new DuplexChannelFactory<TServiceContract>(
                this.callbackObject,
                this.clientBinding,
                endpointAddress);
            }
            else
            {
                channelFactory = new ChannelFactory<TServiceContract>(this.clientBinding, endpointAddress);
            }
            // Add certificate details toohello ChannelFactory credentials.
            // These credentials will be used by hello clients created by
            // SecureWcfCommunicationClientFactory.  
            channelFactory.Credentials.ClientCertificate.SetCertificate(
                StoreLocation.LocalMachine,
                StoreName.My,
                X509FindType.FindByThumbprint,
                "9DC906B169DC4FAFFD1697AC781E806790749D2F");
            var channel = channelFactory.CreateChannel();
            var clientChannel = ((IClientChannel)channel);
            clientChannel.OperationTimeout = this.clientBinding.ReceiveTimeout;
            return Task.FromResult(this.CreateWcfCommunicationClient(channel));
        }
    }
    ```

    <span data-ttu-id="1be03-140">Use `SecureWcfCommunicationClientFactory` toocreate um cliente de comunicação WCF (`WcfCommunicationClient`).</span><span class="sxs-lookup"><span data-stu-id="1be03-140">Use `SecureWcfCommunicationClientFactory` toocreate a WCF communication client (`WcfCommunicationClient`).</span></span> <span data-ttu-id="1be03-141">Use métodos de serviço de tooinvoke do saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="1be03-141">Use hello client tooinvoke service methods.</span></span>

    ```csharp
    IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();

    var wcfClientFactory = new SecureWcfCommunicationClientFactory<ICalculator>(clientBinding: GetNetTcpBinding(), servicePartitionResolver: partitionResolver);

    var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
        wcfClientFactory,
        ServiceUri,
        ServicePartitionKey.Singleton);

    var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
        client => client.Channel.Add(2, 3)).Result;
    ```

## <a name="next-steps"></a><span data-ttu-id="1be03-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1be03-142">Next steps</span></span>
* [<span data-ttu-id="1be03-143">API Web com OWIN no Reliable Services</span><span class="sxs-lookup"><span data-stu-id="1be03-143">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
