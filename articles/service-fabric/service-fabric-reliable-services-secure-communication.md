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
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a>Ajudar a proteger a comunicação para serviços no Azure Service Fabric
> [!div class="op_single_selector"]
> * [C# em Windows](service-fabric-reliable-services-secure-communication.md)
> * [Java no Linux](service-fabric-reliable-services-secure-communication-java.md)
>
>

A segurança é um dos aspectos mais importantes de saudação de comunicação. estrutura de aplicativo de serviços confiáveis Olá fornece algumas pilhas de comunicação pré-compilada e ferramentas que você pode usar segurança tooimprove. Este artigo fala sobre como tooimprove segurança quando você estiver usando o serviço remoto e Olá pilha de comunicação do Windows Communication Foundation (WCF).

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a>Ajudar a proteger um serviço quando você estiver usando a comunicação remota de serviço
Estamos usando uma existente [exemplo](service-fabric-reliable-services-communication-remoting.md) que explica como tooset a conexão remota para serviços confiáveis. toohelp proteger um serviço quando você estiver usando a comunicação remota do serviço, siga estas etapas:

1. Criar uma interface `IHelloWorldStateful`, que define os métodos de saudação que estarão disponíveis para uma chamada de procedimento remoto em seu serviço. O serviço usará `FabricTransportServiceRemotingListener`, que é declarada no hello `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` namespace. Esta é uma implementação de `ICommunicationListener` que fornece recursos de comunicação remota.

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
2. Adicionar credenciais de segurança e configurações de ouvinte.

    Verifique se esse certificado Olá que você deseja toohelp toouse segura que a comunicação de serviço é instalada em todos os nós Olá cluster hello. Há duas maneiras de fornecer configurações de ouvinte e credenciais de segurança:

   1. Fornecê-los diretamente no código de saudação do serviço:

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
   2. Fornecê-las usando um [pacote de configuração](service-fabric-application-model.md):

       Adicionar um `TransportSettings` seção no arquivo settings.xml de saudação.

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

       Nesse caso, Olá `CreateServiceReplicaListeners` método terá esta aparência:

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

        Se você adicionar um `TransportSettings` seção no arquivo settings.xml Olá `FabricTransportRemotingListenerSettings ` carregar todas as configurações de saudação desta seção por padrão.

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        Nesse caso, Olá `CreateServiceReplicaListeners` método terá esta aparência:

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
3. Quando você chama métodos em um serviço protegido usando a pilha de comunicação remota do hello, em vez de usar o hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` toocreate classe um proxy do serviço, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`. Passe `FabricTransportRemotingSettings`, que contém `SecurityCredentials`.

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

    Se o código de saudação do cliente é executado como parte de um serviço, você poderá carregar `FabricTransportRemotingSettings` do arquivo de settings.xml hello. Crie uma seção de HelloWorldClientTransportSettings que é o código de serviço toohello semelhantes, conforme mostrado anteriormente. Verifique Olá alterações toohello cliente código a seguir:

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    Se o cliente Olá não está em execução como parte de um serviço, você pode criar um arquivo de client_name.settings.xml em Olá mesmo local onde client_name.exe hello. Em seguida, crie uma seção TransportSettings nesse arquivo.

    Serviço toohello semelhante, se você adicionar um `TransportSettings` seção cliente settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` carrega todas as configurações de saudação nesta seção por padrão.

    Nesse caso, hello código anterior é ainda mais simplificado:  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a>Ajudar a proteger um serviço quando você estiver usando uma pilha de comunicação baseada em WCF
Estamos usando uma existente [exemplo](service-fabric-reliable-services-communication-wcf.md) que explica como tooset uma comunicação baseada em WCF de pilha para serviços confiáveis. toohelp proteger um serviço quando você estiver usando uma pilha de comunicação WCF, siga estas etapas:

1. Para serviço hello, você precisa de ouvinte de comunicação de WCF toohelp Olá seguro (`WcfCommunicationListener`) que você criar. toodo isso, modifique Olá `CreateServiceReplicaListeners` método.

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
2. No cliente de Olá Olá `WcfCommunicationClient` classe que foi criado no hello anterior [exemplo](service-fabric-reliable-services-communication-wcf.md) permanece inalterado. Mas você precisa Olá toooverride `CreateClientAsync` método `WcfCommunicationClientFactory`:

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

    Use `SecureWcfCommunicationClientFactory` toocreate um cliente de comunicação WCF (`WcfCommunicationClient`). Use métodos de serviço de tooinvoke do saudação do cliente.

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

## <a name="next-steps"></a>Próximas etapas
* [API Web com OWIN no Reliable Services](service-fabric-reliable-services-communication-webapi.md)
