---
title: "Ajudar a proteger a comunicação para serviços no Azure Service Fabric | Microsoft Docs"
description: "Visão geral de como ajudar a proteger a comunicação para os Reliable Services executados em um cluster do Azure Service Fabric."
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
ms.openlocfilehash: 53119244f8f09c0c6c43f43761af1cc074f8d0af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="5f5f4-103">Ajudar a proteger a comunicação para serviços no Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5f5f4-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5f5f4-104">C# em Windows</span><span class="sxs-lookup"><span data-stu-id="5f5f4-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="5f5f4-105">Java no Linux</span><span class="sxs-lookup"><span data-stu-id="5f5f4-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

<span data-ttu-id="5f5f4-106">A segurança é um dos aspectos mais importantes da comunicação.</span><span class="sxs-lookup"><span data-stu-id="5f5f4-106">Security is one of the most important aspects of communication.</span></span> <span data-ttu-id="5f5f4-107">A estrutura de aplicativo dos Reliable Services fornece algumas pilhas e ferramentas de comunicação predefinidas que você pode usar para aprimorar a segurança.</span><span class="sxs-lookup"><span data-stu-id="5f5f4-107">The Reliable Services application framework provides a few prebuilt communication stacks and tools that you can use to improve security.</span></span> <span data-ttu-id="5f5f4-108">Este artigo aborda como aprimorar a segurança quando você estiver usando a comunicação remota de serviço e a pilha de comunicação do WCF (Windows Communication Foundation).</span><span class="sxs-lookup"><span data-stu-id="5f5f4-108">This article talks about how to improve security when you're using service remoting and the Windows Communication Foundation (WCF) communication stack.</span></span>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="5f5f4-109">Ajudar a proteger um serviço quando você estiver usando a comunicação remota de serviço</span><span class="sxs-lookup"><span data-stu-id="5f5f4-109">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="5f5f4-110">Usamos um [exemplo](service-fabric-reliable-services-communication-remoting.md) existente que explica como configurar a comunicação remota para os Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="5f5f4-110">We are using an existing [example](service-fabric-reliable-services-communication-remoting.md) that explains how to set up remoting for reliable services.</span></span> <span data-ttu-id="5f5f4-111">Para ajudar a proteger um serviço quando você estiver usando a comunicação remota de serviço, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="5f5f4-111">To help secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="5f5f4-112">Crie uma interface, `IHelloWorldStateful`, que define os métodos que estarão disponíveis para chamada de procedimento remoto no seu serviço.</span><span class="sxs-lookup"><span data-stu-id="5f5f4-112">Create an interface, `IHelloWorldStateful`, that defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="5f5f4-113">Seu serviço usará `FabricTransportServiceRemotingListener`, que é declarado no namespace `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime`.</span><span class="sxs-lookup"><span data-stu-id="5f5f4-113">Your service will use `FabricTransportServiceRemotingListener`, which is declared in the `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` namespace.</span></span> <span data-ttu-id="5f5f4-114">Esta é uma implementação de `ICommunicationListener` que fornece recursos de comunicação remota.</span><span class="sxs-lookup"><span data-stu-id="5f5f4-114">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span>

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
2. <span data-ttu-id="5f5f4-115">Adicionar credenciais de segurança e configurações de ouvinte.</span><span class="sxs-lookup"><span data-stu-id="5f5f4-115">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="5f5f4-116">Certifique-se de que o certificado que você deseja usar para ajudar proteger a comunicação do serviço esteja instalado em todos os nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="5f5f4-116">Make sure that the certificate that you want to use to help secure your service communication is installed on all the nodes in the cluster.</span></span> <span data-ttu-id="5f5f4-117">Há duas maneiras de fornecer configurações de ouvinte e credenciais de segurança:</span><span class="sxs-lookup"><span data-stu-id="5f5f4-117">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="5f5f4-118">Fornecê-las diretamente no código do serviço:</span><span class="sxs-lookup"><span data-stu-id="5f5f4-118">Provide them directly in the service code:</span></span>

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
   2. <span data-ttu-id="5f5f4-119">Fornecê-las usando um [pacote de configuração](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="5f5f4-119">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="5f5f4-120">Adicione uma seção `TransportSettings` ao arquivo settings.xml.</span><span class="sxs-lookup"><span data-stu-id="5f5f4-120">Add a `TransportSettings` section in the settings.xml file.</span></span>

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

       <span data-ttu-id="5f5f4-121">Nesse caso, o método `CreateServiceReplicaListeners` terá esta aparência:</span><span class="sxs-lookup"><span data-stu-id="5f5f4-121">In this case, the `CreateServiceReplicaListeners` method will look like this:</span></span>

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

        <span data-ttu-id="5f5f4-122">Se você adicionar uma seção `TransportSettings` ao arquivo settings.xml, `FabricTransportRemotingListenerSettings ` carregará todas as configurações dessa seção por padrão.</span><span class="sxs-lookup"><span data-stu-id="5f5f4-122">If you add a `TransportSettings` section in the settings.xml file , `FabricTransportRemotingListenerSettings ` will load all the settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="5f5f4-123">Nesse caso, o método `CreateServiceReplicaListeners` terá esta aparência:</span><span class="sxs-lookup"><span data-stu-id="5f5f4-123">In this case, the `CreateServiceReplicaListeners` method will look like this:</span></span>

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
3. <span data-ttu-id="5f5f4-124">Ao chamar métodos em um serviço protegido usando a pilha de comunicação remota, em vez de usar a classe `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` para criar um proxy de serviço, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="5f5f4-124">When you call methods on a secured service by using the remoting stack, instead of using the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class to create a service proxy, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span></span> <span data-ttu-id="5f5f4-125">Passe `FabricTransportRemotingSettings`, que contém `SecurityCredentials`.</span><span class="sxs-lookup"><span data-stu-id="5f5f4-125">Pass in `FabricTransportRemotingSettings`, which contains `SecurityCredentials`.</span></span>

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

    <span data-ttu-id="5f5f4-126">Se o código cliente estiver sendo executado como parte de um serviço, você poderá carregar `FabricTransportRemotingSettings` do arquivo settings.xml.</span><span class="sxs-lookup"><span data-stu-id="5f5f4-126">If the client code is running as part of a service, you can load `FabricTransportRemotingSettings` from the settings.xml file.</span></span> <span data-ttu-id="5f5f4-127">Crie uma seção HelloWorldClientTransportSettings semelhante ao código de serviço, conforme mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="5f5f4-127">Create a HelloWorldClientTransportSettings section that is similar to the service code, as shown earlier.</span></span> <span data-ttu-id="5f5f4-128">Faça as alterações a seguir no código cliente:</span><span class="sxs-lookup"><span data-stu-id="5f5f4-128">Make the following changes to the client code:</span></span>

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="5f5f4-129">Se o cliente não estiver sendo executado como parte de um serviço, você poderá criar um arquivo client_name.settings.xml no mesmo local em que client_name.exe estiver.</span><span class="sxs-lookup"><span data-stu-id="5f5f4-129">If the client is not running as part of a service, you can create a client_name.settings.xml file in the same location where the client_name.exe is.</span></span> <span data-ttu-id="5f5f4-130">Em seguida, crie uma seção TransportSettings nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="5f5f4-130">Then create a TransportSettings section in that file.</span></span>

    <span data-ttu-id="5f5f4-131">De forma semelhante ao serviço, se você adicionar uma seção `TransportSettings` em client settings.xml/client_name.settings.xml, o `FabricTransportRemotingSettings` carregará por padrão todas as configurações dessa seção.</span><span class="sxs-lookup"><span data-stu-id="5f5f4-131">Similar to the service, if you add a `TransportSettings` section in client settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` loads all the settings from this section by default.</span></span>

    <span data-ttu-id="5f5f4-132">Nesse caso, o código anterior é ainda mais simplificado:</span><span class="sxs-lookup"><span data-stu-id="5f5f4-132">In that case, the earlier code is even further simplified:</span></span>  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a><span data-ttu-id="5f5f4-133">Ajudar a proteger um serviço quando você estiver usando uma pilha de comunicação baseada em WCF</span><span class="sxs-lookup"><span data-stu-id="5f5f4-133">Help secure a service when you're using a WCF-based communication stack</span></span>
<span data-ttu-id="5f5f4-134">Usamos um [exemplo](service-fabric-reliable-services-communication-wcf.md) existente que explica como configurar uma pilha de comunicação baseada em WCF para os Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="5f5f4-134">We are using an existing [example](service-fabric-reliable-services-communication-wcf.md) that explains how to set up a WCF-based communication stack for reliable services.</span></span> <span data-ttu-id="5f5f4-135">Para ajudar a proteger um serviço quando você estiver usando uma pilha de comunicação baseada em WCF, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="5f5f4-135">To help secure a service when you're using a WCF-based communication stack, follow these steps:</span></span>

1. <span data-ttu-id="5f5f4-136">Para o serviço, você precisa ajudar a proteger o ouvinte da comunicação WCF (`WcfCommunicationListener`) que você criar.</span><span class="sxs-lookup"><span data-stu-id="5f5f4-136">For the service, you need to help secure the WCF communication listener (`WcfCommunicationListener`) that you create.</span></span> <span data-ttu-id="5f5f4-137">Para fazer isso, modifique o método `CreateServiceReplicaListeners` .</span><span class="sxs-lookup"><span data-stu-id="5f5f4-137">To do this, modify the `CreateServiceReplicaListeners` method.</span></span>

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

        // Add certificate details in the ServiceHost credentials.
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
2. <span data-ttu-id="5f5f4-138">No cliente, a classe `WcfCommunicationClient` que foi criada no [exemplo](service-fabric-reliable-services-communication-wcf.md) anterior permanece inalterada.</span><span class="sxs-lookup"><span data-stu-id="5f5f4-138">In the client, the `WcfCommunicationClient` class that was created in the previous [example](service-fabric-reliable-services-communication-wcf.md) remains unchanged.</span></span> <span data-ttu-id="5f5f4-139">Mas você precisa substituir o método `CreateClientAsync` de `WcfCommunicationClientFactory`:</span><span class="sxs-lookup"><span data-stu-id="5f5f4-139">But you need to override the `CreateClientAsync` method of `WcfCommunicationClientFactory`:</span></span>

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
            // Add certificate details to the ChannelFactory credentials.
            // These credentials will be used by the clients created by
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

    <span data-ttu-id="5f5f4-140">Use `SecureWcfCommunicationClientFactory` para criar um cliente de comunicação WCF (`WcfCommunicationClient`).</span><span class="sxs-lookup"><span data-stu-id="5f5f4-140">Use `SecureWcfCommunicationClientFactory` to create a WCF communication client (`WcfCommunicationClient`).</span></span> <span data-ttu-id="5f5f4-141">Use o cliente para invocar métodos de serviço.</span><span class="sxs-lookup"><span data-stu-id="5f5f4-141">Use the client to invoke service methods.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5f5f4-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5f5f4-142">Next steps</span></span>
* [<span data-ttu-id="5f5f4-143">API Web com OWIN no Reliable Services</span><span class="sxs-lookup"><span data-stu-id="5f5f4-143">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
