---
title: "tutorial de retransmissão do WCF do Service Bus aaaAzure | Microsoft Docs"
description: "Compilar um serviço e um aplicativo cliente do Barramento de Serviço usando a Retransmissão WCF."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 53dfd236-97f1-4778-b376-be91aa14b842
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: sethm
ms.openlocfilehash: 78cd52ef51e9fcfcda2f13ec54bde3af50d76476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-tutorial"></a>Tutorial de Retransmissão de WCF do Azure

Este tutorial descreve como toobuild um simple WCF retransmissão aplicativo cliente e o serviço de retransmissão do Azure. Para obter um tutorial semelhante que usa o [Sistema de Mensagens do Barramento de Serviço](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), consulte a [Introdução às filas do Barramento de Serviço](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).

Trabalhando com este tutorial fornece uma compreensão das etapas Olá toocreate necessário um aplicativo de cliente e o serviço de retransmissão do WCF. Assim como suas contrapartes WCF originais, um serviço é um constructo que expõe um ou mais pontos de extremidade, cada um dos quais expõe uma ou mais operações de serviço. ponto de extremidade de saudação de um serviço Especifica um endereço onde o serviço Olá pode ser encontrado, uma associação que contém informações de saudação que um cliente deve se comunicar com o serviço de Olá e um contrato que define Olá funcionalidade fornecida por Olá serviço tooits clientes. Olá principal diferença entre o WCF e a retransmissão do WCF é que esse ponto de extremidade de saudação é exposto na nuvem de saudação em vez de localmente no seu computador.

Depois de você trabalhar com sequência de saudação de tópicos neste tutorial, você terá um serviço em execução e um cliente pode invocar operações de saudação do serviço de saudação. Olá primeiro tópico descreve como tooset uma conta. as próximas etapas Olá descrevem como toodefine um serviço que usa um contrato, como tooimplement Olá serviço e como tooconfigure Olá serviço em código. Eles também descrevem como serviço de saudação toohost e execução. Olá serviço que é criado é auto-hospedado e Olá cliente e serviço executado em Olá mesmo computador. Você pode configurar o serviço de saudação usando código ou um arquivo de configuração.

etapas de três finais Olá descrevem como toocreate um aplicativo cliente, configurar o aplicativo de cliente hello e criar e usar um cliente que pode acessar a funcionalidade de saudação do host de saudação.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete neste tutorial, você precisará Olá a seguir:

* [Microsoft Visual Studio 2015 ou superior](http://visualstudio.com). Este tutorial usa o Visual Studio 2017.
* Uma conta ativa do Azure. Se não tiver uma, você poderá criar uma conta gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/free/).

## <a name="create-a-service-namespace"></a>Criar um namespace de serviço

Olá primeira etapa é toocreate um namespace e tooobtain um [assinatura de acesso compartilhado (SAS)](../service-bus-messaging/service-bus-sas.md) chave. Um namespace fornece um limite de aplicativo para cada aplicativo exposto por meio do serviço de retransmissão hello. Uma chave SAS é gerada automaticamente pelo sistema hello quando um namespace de serviço é criado. combinação de saudação do namespace de serviço e a chave SAS fornece credenciais de saudação para aplicativo do Azure tooauthenticate access tooan. Siga Olá [as instruções aqui](relay-create-namespace-portal.md) toocreate um namespace de retransmissão.

## <a name="define-a-wcf-service-contract"></a>Definir um contrato de serviço do WCF

contrato de serviço Olá Especifica que o serviço de saudação de operações (Olá terminologia do serviço web para funções ou métodos) dá suporte. Os contratos são criados pela definição de uma interface C++, C# ou Visual Basic. Cada método na interface de saudação corresponde tooa operação de serviço específico. Cada interface deve ter Olá [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) atributo aplicado tooit e cada operação deve ter Olá [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) tooit atributo aplicado. Se um método em uma interface que tem Olá [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) atributo não tem Olá [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) de atributo, que o método não é exposto. código de saudação para essas tarefas é fornecido no exemplo hello Olá procedimento a seguir. Para obter uma discussão maior de contratos e serviços, consulte [Projetando e Implementando serviços](https://msdn.microsoft.com/library/ms729746.aspx) em Olá documentação do WCF.

### <a name="create-a-relay-contract-with-an-interface"></a>Criar um contrato de retransmissão com uma interface

1. Abra o Visual Studio como administrador clicando com o programa Olá Olá **iniciar** menu e selecionando **executar como administrador**.
2. Crie um novo projeto de aplicativo de console. Clique em Olá **arquivo** menu e selecione **novo**, em seguida, clique em **projeto**. Em Olá **novo projeto** caixa de diálogo, clique em **Visual C#** (se **Visual C#** não aparecer, procure em **outras linguagens**). Clique em Olá **aplicativo de Console (.NET Framework)** modelo e nomeie-o **EchoService**. Clique em **Okey** toocreate projeto de saudação.

    ![][2]

3. Instale o pacote do NuGet do barramento de serviço de saudação. Esse pacote adiciona automaticamente referências toohello Service Bus bibliotecas, bem como Olá WCF **System. ServiceModel**. [System. ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) é Olá namespace que permite que recursos básicos de saudação do acesso de tooprogrammatically do WCF. Barramento de serviço usa muitos dos objetos hello e atributos de contratos de serviço do WCF toodefine.

    No Gerenciador de soluções, clique com botão direito hello e, em seguida, clique em **gerenciar pacotes NuGet...** . Clique em Olá **procurar** guia e, em seguida, procurar `Microsoft Azure Service Bus`. Certifique-se de que esse nome de projeto hello está selecionado no hello **versões** caixa. Clique em **instalar**e aceite os termos de uso do hello.

    ![][3]
4. No Solution Explorer, clique duas vezes em tooopen de arquivo Program.cs Olá-lo no editor de saudação, se ele não ainda estiver aberto.
5. Adicione Olá seguinte usando as instruções na parte superior de saudação do arquivo hello:

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. Alterar o nome de namespace de saudação de seu nome padrão de **EchoService** muito**Samples**.

   > [!IMPORTANT]
   > Este tutorial usa o namespace Olá c# **Samples**, que é o namespace de saudação do hello com base no contrato gerenciado tipo que é usado no arquivo de configuração de saudação em Olá [cliente do WCF configurar Olá](#configure-the-wcf-client) etapa. Você pode especificar qualquer namespace desejado ao criar este exemplo; No entanto, Olá tutorial não funcionará a menos que você modifique Olá namespaces de contrato hello e do serviço da mesma forma, no arquivo de configuração de aplicativo hello. Olá namespace especificado em Olá App. config arquivo deve ser Olá mesmo Olá namespace especificado em seus arquivos c#.
   >
   >
7. Depois de saudação `Microsoft.ServiceBus.Samples` declaração de namespace, mas no namespace hello, definir uma nova interface chamada `IEchoContract` e aplicar Olá `ServiceContractAttribute` interface de toohello de atributo com um valor de namespace de `http://samples.microsoft.com/ServiceModel/Relay/`. valor de namespace Olá difere do namespace Olá que você usa em todo o escopo de saudação do seu código. Em vez disso, o valor do namespace Olá é usado como um identificador exclusivo para este contrato. Especificar explicitamente o namespace de saudação impede que o valor de namespace padrão Olá seja adicionado a toohello do nome do contrato. Cole Olá código a seguir após a declaração de namespace hello:

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > Normalmente, o namespace de contrato de serviço Olá contém um esquema de nomenclatura que inclui informações de versão. Incluindo informações de versão no namespace de contrato de serviço Olá permite alterações principais do serviços tooisolate definindo um novo contrato de serviço com um novo namespace e expondo-o em um novo ponto de extremidade. Dessa maneira, os clientes podem continuar toouse Olá antigo contrato de serviço sem ter que toobe atualizado. Informações de versão podem consistir de uma data ou um número da versão. Para saber mais, veja [Controle de Versão do Serviço](http://go.microsoft.com/fwlink/?LinkID=180498). Para fins de saudação deste tutorial, Olá esquema do namespace de contrato de serviço de saudação de nomenclatura não contém informações de versão.
   >
   >
8. Dentro de saudação `IEchoContract` interface, declare um método para Olá Olá de única operação `IEchoContract` expõe contrato em Olá interface e aplique Olá `OperationContractAttribute` método toohello de atributo que você deseja tooexpose como parte do hello pública retransmissão do WCF contrato, da seguinte maneira:

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. Depois de saudação `IEchoContract` definição de interface, declare um canal que herde das `IEchoContract` e também toohello `IClientChannel` interface, conforme mostrado aqui:

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    Um canal é o objeto WCF de saudação por meio do qual clientes e host Olá passam informações tooeach outros. Posteriormente, você escreverá código em relação às informações de tooecho Olá canal entre dois aplicativos de saudação.
10. De saudação **criar** menu, clique em **compilar solução** ou pressione **Ctrl + Shift + B** tooconfirm precisão de saudação do seu trabalho até o momento.

### <a name="example"></a>Exemplo

saudação de código a seguir mostra uma interface básica que define um contrato de retransmissão do WCF.

```csharp
using System;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

Agora que hello interface foi criada, você pode implementar a interface de saudação.

## <a name="implement-hello-wcf-contract"></a>Contrato de implementar saudação do WCF

Criar um relé do Azure requer que você primeiro crie contrato hello, que é definido por meio de uma interface. Para obter mais informações sobre como criar interface hello, consulte a etapa anterior de saudação. Olá próxima etapa é a interface de saudação tooimplement. Isso envolve a criação de uma classe denominada `EchoService` que implementa Olá definidos pelo usuário `IEchoContract` interface. Depois de implementar a interface hello, você configura Olá interface usando um arquivo de configuração App. config. arquivo de configuração de saudação contém as informações necessárias para o aplicativo hello, como nome de saudação do serviço Olá, nome de saudação do contrato hello e tipo de saudação do protocolo é toocommunicate usado com o serviço de retransmissão hello. código de saudação usado para essas tarefas é fornecido no exemplo hello Olá procedimento a seguir. Para obter uma discussão mais geral sobre como tooimplement um serviço de contrato, consulte [implementando contratos de serviço](https://msdn.microsoft.com/library/ms733764.aspx) em Olá documentação do WCF.

1. Criar uma nova classe chamada `EchoService` diretamente após a definição de saudação do hello `IEchoContract` interface. Olá `EchoService` classe implementa Olá `IEchoContract` interface.

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    Implementações de interface tooother semelhante, você pode implementar definição Olá em um arquivo diferente. No entanto, para este tutorial, implementação hello está localizada no hello mesmo arquivo como definição de interface hello e hello `Main` método.
2. Aplicar Olá [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) atributo toohello `IEchoContract` interface. atributo Olá Especifica o namespace e o nome do serviço de saudação. Depois de fazer isso, Olá `EchoService` classe aparece da seguinte maneira:

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. Saudação de implementar `Echo` método definido no hello `IEchoContract` interface Olá `EchoService` classe.

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. Clique em **criar**, em seguida, clique em **compilar solução** tooconfirm precisão de saudação de seu trabalho.

### <a name="define-hello-configuration-for-hello-service-host"></a>Definir a configuração de saudação para o host de serviço Olá

1. arquivo de configuração de saudação é muito semelhante arquivo de configuração do WCF tooa. Ele inclui o nome do serviço hello, ponto de extremidade (ou seja, a localização de saudação que expõe a retransmissão do Azure para clientes e hosts toocommunicate uns com os outros) e Olá associação (tipo de saudação do protocolo é usado toocommunicate). Olá principal diferença é que este ponto de extremidade de serviço configurado refere-se tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) associação, que não faz parte de saudação do .NET Framework. [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) é uma das associações de saudação definidas pelo serviço de saudação.
2. Em **Solution Explorer**, clique duas vezes em Olá App. config arquivo tooopen-lo no editor do Visual Studio hello.
3. Em Olá `<appSettings>` elemento, substitua os espaços reservados de saudação pelo nome de Olá do seu namespace de serviço e Olá chave SAS que você copiou em uma etapa anterior.
4. Dentro de saudação `<system.serviceModel>` marcas, adicione um `<services>` elemento. Assim como nas associações, você pode definir vários aplicativos de retransmissão em um único arquivo de configuração. Este tutorial, porém, define apenas um.

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. Dentro de saudação `<services>` elemento, adicionar um `<service>` nome do elemento toodefine saudação do serviço de saudação.

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. Dentro de saudação `<service>` elemento, definir local de saudação do contrato de ponto de extremidade hello e Olá também o tipo de associação para o ponto de extremidade de saudação.

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    ponto de extremidade Olá define onde Olá cliente procurará o aplicativo de host hello. Posteriormente, o tutorial Olá usa toocreate esta etapa um URI que expõe totalmente host Olá por meio de retransmissão do Azure. associação de saudação declara que estamos usando TCP como Olá toocommunicate de protocolo com o serviço de retransmissão hello.
7. De saudação **criar** menu, clique em **compilar solução** tooconfirm precisão de saudação de seu trabalho.

### <a name="example"></a>Exemplo

Olá código a seguir mostra a implementação Olá Olá do contrato de serviço.

```csharp
[ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]

    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }
```

Olá código a seguir mostra formato básico de Olá Olá App. config arquivo associado ao host de serviço hello.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceBus.Samples.EchoService">
        <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding" />
      </service>
    </services>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="host-and-run-a-basic-web-service-tooregister-with-hello-relay-service"></a>Hospedar e executar um tooregister de serviço web básico com o serviço de retransmissão Olá

Essa etapa descreve como toorun um Azure retransmissão serviço.

### <a name="create-hello-relay-credentials"></a>Criar hello credenciais de retransmissão

1. Em `Main()`, crie duas variáveis no namespace de saudação quais toostore e Olá chave SAS que são lidos da janela de console hello.

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    a chave de SAS Olá será usado tooaccess posterior seu projeto. Olá namespace também é passado como um parâmetro`CreateServiceUri` toocreate um URI de serviço.
2. Usando um [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) de objeto, declare que você usando uma chave SAS como tipo de credencial de saudação. Adicione Olá código a seguir diretamente após Olá código adicionado na última etapa de saudação.

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-hello-service"></a>Criar um endereço base para serviço Olá

Depois de código Olá você adicionou na última etapa do hello, crie um `Uri` instância para o endereço de base de saudação do serviço de saudação. Esse URI especifica esquema de barramento de serviço de hello, Olá namespace e o caminho de saudação da interface de serviço hello.

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

"sb" é uma abreviação para o esquema de barramento de serviço hello e indica que estamos usando TCP como protocolo de saudação. Isso também foi indicado no arquivo de configuração hello, quando [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) foi especificado como associação de saudação.

Para este tutorial, hello URI é `sb://putServiceNamespaceHere.windows.net/EchoService`.

### <a name="create-and-configure-hello-service-host"></a>Criar e configurar o host de serviço Olá

1. Definir o modo de conectividade de saudação muito`AutoDetect`.

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    modo de conectividade Olá descreve Olá protocolo hello serviço usa toocommunicate com serviço de retransmissão Olá; HTTP ou TCP. Usando a configuração padrão de saudação `AutoDetect`, serviço de saudação tenta tooconnect tooAzure retransmissão via TCP se estiver disponível e HTTP se TCP não está disponível. Observe que isso é diferente do serviço de saudação do protocolo de saudação especifica para comunicação do cliente. Esse protocolo é determinado pela associação Olá usada. Por exemplo, um serviço pode usar Olá [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) associação, que especifica que seu ponto de extremidade se comunica com os clientes por HTTP. Se o mesmo serviço pode especificar **Connectivitymode** para que o serviço de saudação se comunica com Azure retransmissão por TCP.
2. Crie saudação do host de serviço, usando Olá que URI criado anteriormente nesta seção.

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    host de serviço de saudação é objeto WCF Olá que instancia o serviço de saudação. Aqui, você passá-lo tipo hello de serviço que você deseja toocreate (um `EchoService` tipo) e também endereço toohello no qual você deseja que o serviço de saudação tooexpose.
3. Na parte superior de saudação do arquivo do hello Program.cs, adicione referências muito[ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) e [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. Em `Main()`, configurar o acesso do hello ponto de extremidade tooenable público.

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    Essa etapa informa ao serviço de retransmissão Olá que seu aplicativo pode ser encontrado publicamente ao examinar Olá ATOM feed para seu projeto. Se você definir **DiscoveryType** muito**privada**, um cliente ainda será capaz de tooaccess serviço de saudação. No entanto, o serviço de saudação não seria exibido, quando ele procura Olá retransmissão namespace. Em vez disso, Olá cliente terá tooknow caminho de ponto de extremidade de saudação com antecedência.
5. Aplicar pontos de extremidade do serviço toohello definidos no arquivo App. config de saudação de credenciais do serviço de saudação:

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    Conforme mencionado na etapa anterior hello, você poderia ter declarado vários serviços e pontos de extremidade no arquivo de configuração de saudação. Se você tivesse, esse código percorreria o arquivo de configuração de saudação e pesquisa para cada ponto de extremidade toowhich deveria aplicar suas credenciais. No entanto, para este tutorial, o arquivo de configuração de saudação tem apenas um ponto de extremidade.

### <a name="open-hello-service-host"></a>Host de serviço abrir Olá

1. Abra o serviço de saudação.

    ```csharp
    host.Open();
    ```
2. Informar usuário Olá Olá serviço está em execução e explique como tooshut para baixo serviço hello.

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. Quando terminar, feche o host de serviço hello.

    ```csharp
    host.Close();
    ```
4. Pressione **Ctrl + Shift + B** toobuild projeto de saudação.

### <a name="example"></a>Exemplo

O código de serviço concluído deve aparecer conforme demonstrado a seguir. código de saudação inclui o contrato de serviço hello e a implementação de etapas anteriores no tutorial Olá e hosts Olá serviço em um aplicativo de console.

```csharp
using System;
using System.ServiceModel;
using System.ServiceModel.Description;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Description;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { };

    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {

            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;         

            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS key: ");
            string sasKey = Console.ReadLine();

           // Create hello credentials object for hello endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create hello service URI based on hello service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create hello service host reading hello configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create hello ServiceRegistrySettings behavior for hello endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add hello Relay credentials tooall endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open hello service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            // Close hello service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-hello-service-contract"></a>Criar um cliente WCF Olá contrato de serviço

Olá próxima etapa é toocreate um aplicativo cliente e definir Olá contrato de serviço você implementará em etapas posteriores. Observe que muitas dessas etapas são semelhantes a etapas Olá usado toocreate um serviço: definir um contrato, edição de um App. config arquivo, usando o serviço de retransmissão do credenciais tooconnect toohello e assim por diante. código de saudação usado para essas tarefas é fornecido no exemplo hello Olá procedimento a seguir.

1. Crie um novo projeto na solução atual de Visual Studio Olá para cliente Olá Olá seguinte:

   1. No Solution Explorer, no hello mesma solução que contém o serviço de saudação, clique a solução atual da saudação (não projeto Olá) e clique em **adicionar**. Em seguida, clique em **Novo Projeto**.
   2. Em Olá **adicionar novo projeto** caixa de diálogo, clique em **Visual C#** (se **Visual C#** não aparecer, procure em **outras linguagens**), selecione Olá **Aplicativo de console (.NET Framework)** modelo e nomeie-o **EchoClient**.
   3. Clique em **OK**.
      <br />
2. No Solution Explorer, clique duas vezes no arquivo Program.cs Olá Olá **EchoClient** projeto tooopen-lo no editor de saudação, se ele não ainda estiver aberto.
3. Alterar o nome de namespace de saudação de seu nome padrão de `EchoClient` muito`Microsoft.ServiceBus.Samples`.
4. Instalar Olá [pacote NuGet do barramento de serviço](https://www.nuget.org/packages/WindowsAzure.ServiceBus): no Solution Explorer, clique com botão direito Olá **EchoClient** do projeto e, em seguida, clique em **gerenciar pacotes NuGet**. Clique em Olá **procurar** guia e, em seguida, procurar `Microsoft Azure Service Bus`. Clique em **instalar**e aceite os termos de uso do hello.

    ![][3]
5. Adicionar um `using` instrução Olá [System. ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace no arquivo Program.cs de saudação.

    ```csharp
    using System.ServiceModel;
    ```
6. Adicione o namespace de toohello definição do contrato de serviço hello, conforme mostrado no exemplo a seguir de saudação. Observe que essa definição é toohello idênticos definição usada no hello **Service** projeto. Você deve adicionar esse código na parte superior de saudação do hello `Microsoft.ServiceBus.Samples` namespace.

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. Pressione **Ctrl + Shift + B** toobuild cliente de saudação.

### <a name="example"></a>Exemplo

Olá código a seguir mostra Olá status atual do arquivo Program.cs de saudação em hello **EchoClient** projeto.

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }


    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="configure-hello-wcf-client"></a>Configurar o cliente do WCF Olá

Nesta etapa, você deve criar um arquivo App. config para um aplicativo cliente básico que acessa o serviço de saudação criado anteriormente neste tutorial. Esse arquivo App. config define o contrato hello, associação e o nome do ponto de extremidade de saudação. código de saudação usado para essas tarefas é fornecido no exemplo hello Olá procedimento a seguir.

1. No Solution Explorer, no hello **EchoClient** de projeto, clique duas vezes em **App. config** tooopen arquivo de saudação no editor do Visual Studio hello.
2. Em Olá `<appSettings>` elemento, substitua os espaços reservados de saudação pelo nome de Olá do seu namespace de serviço e Olá chave SAS que você copiou em uma etapa anterior.
3. Dentro do elemento de System. ServiceModel hello, adicione um `<client>` elemento.

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    Essa etapa declara que você está definindo um aplicativo de cliente no estilo WCF.
4. Dentro de saudação `client` elemento, definir nome hello, contrato e o tipo de associação para o ponto de extremidade de saudação.

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    Esta etapa define o nome de saudação do ponto de extremidade hello, contrato de saudação definido no serviço hello e fatos Olá que o aplicativo de cliente de saudação usa TCP toocommunicate com retransmissão do Azure. Olá nome de ponto de extremidade é usado em Olá próxima etapa toolink essa configuração de ponto de extremidade com o URI do serviço de saudação.
5. Clique em **Arquivo**, depois em **Salvar Tudo**.

## <a name="example"></a>Exemplo

Olá código a seguir mostra arquivo App. config de saudação para cliente de eco de saudação.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <client>
      <endpoint name="RelayEndpoint"
                      contract="Microsoft.ServiceBus.Samples.IEchoContract"
                      binding="netTcpRelayBinding"/>
    </client>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="implement-hello-wcf-client"></a>Cliente WCF implementar Olá
Nesta etapa, você deve implementar um aplicativo cliente básico que acessa o serviço de saudação criado anteriormente neste tutorial. Serviço toohello semelhante, o cliente de saudação executa muitas das Olá mesmo operações tooaccess retransmissão do Azure:

1. Define o modo de conectividade de saudação.
2. Cria Olá URI que localiza o serviço de host de saudação.
3. Define as credenciais de segurança de saudação.
4. Aplica-se a conexão do hello credenciais toohello.
5. Abre a conexão de saudação.
6. Executa tarefas específicas do aplicativo de saudação.
7. Fecha a conexão de saudação.

No entanto, uma das principais diferenças de saudação é que o aplicativo de cliente hello usa um serviço de retransmissão do canal tooconnect toohello, enquanto o serviço de saudação usa uma chamada muito**ServiceHost**. código de saudação usado para essas tarefas é fornecido no exemplo hello Olá procedimento a seguir.

### <a name="implement-a-client-application"></a>Implementar um aplicativo cliente
1. Definir o modo de conectividade de saudação muito**detecção automática**. Adicionar Olá seguindo o código dentro de saudação `Main()` método hello **EchoClient** aplicativo.

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. Defina variáveis toohold Olá valores para namespace de serviço Olá e a chave SAS que são lidos a partir do console de saudação.

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. Crie hello URI que define o local de saudação do host de saudação em seu projeto de retransmissão.

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. Crie objeto de credencial de saudação para seu ponto de extremidade do namespace de serviço.

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. Crie a fábrica de canais de saudação que carrega a configuração de saudação descrita no arquivo App. config de saudação.

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    Uma fábrica de canais é um objeto WCF que cria um canal por meio do qual os aplicativos de serviço e cliente Olá se comunicar.
6. Aplique as credenciais de saudação.

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. Crie e abra Olá canal toohello serviço.

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. Grave a interface do usuário básica hello e funcionalidade de eco de saudação.

    ```csharp
    Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
    string input = Console.ReadLine();
    while (input != String.Empty)
    {
        try
        {
            Console.WriteLine("Server echoed: {0}", channel.Echo(input));
        }
        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.Message);
        }
        input = Console.ReadLine();
    }
    ```

    Observe que o código Olá usa instância de saudação do objeto do canal de saudação como um proxy para o serviço de saudação.
9. Feche o canal hello e fábrica Olá fechar.

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a>Exemplo

O código completo deve aparecer como segue, mostrar como toocreate um aplicativo cliente, como toocall Olá operações do serviço de saudação e como tooclose Olá cliente após a operação de saudação chamam é concluída.

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;


            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS Key: ");
            string sasKey = Console.ReadLine();



            Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));

            channelFactory.Endpoint.Behaviors.Add(sasCredential);

            IEchoChannel channel = channelFactory.CreateChannel();
            channel.Open();

            Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
            string input = Console.ReadLine();
            while (input != String.Empty)
            {
                try
                {
                    Console.WriteLine("Server echoed: {0}", channel.Echo(input));
                }
                catch (Exception e)
                {
                    Console.WriteLine("Error: " + e.Message);
                }
                input = Console.ReadLine();
            }

            channel.Close();
            channelFactory.Close();

        }
    }
}
```

## <a name="run-hello-applications"></a>Executar aplicativos Olá

1. Pressione **Ctrl + Shift + B** toobuild solução de saudação. Isso cria o projeto de saudação do cliente e o projeto de serviço de saudação que você criou nas etapas anteriores Olá.
2. Antes da aplicação de cliente Olá em execução, você deve se certificar que o aplicativo de serviço hello está sendo executado. No Gerenciador de soluções no Visual Studio, clique com botão direito Olá **EchoService** solução, em seguida, clique em **propriedades**.
3. Na caixa de diálogo de propriedades de solução de saudação, clique em **projeto de inicialização**, em seguida, clique em Olá **vários projetos de inicialização** botão. Certifique-se de **EchoService** aparece primeiro na lista de saudação.
4. Saudação de conjunto **ação** caixa para ambos os Olá **EchoService** e **EchoClient** projetos muito**iniciar**.

    ![][5]
5. Clique em **Dependências do Projeto**. Em Olá **projetos** selecione **EchoClient**. Em Olá **depende** caixa, certifique-se de **EchoService** é verificada.

    ![][6]
6. Clique em **Okey** toodismiss Olá **propriedades** caixa de diálogo.
7. Pressione **F5** toorun os dois projetos.
8. Ambas as janelas do console abrirem e solicitar o nome do namespace hello. Olá serviço deve ser executado pela primeira vez, isso em Olá **EchoService** janela de console, digite Olá namespace e, em seguida, pressione **Enter**.
9. Em seguida, será solicitado que você informe a sua chave de SAS. Insira a chave de SAS hello e pressione ENTER.

    Aqui está o exemplo de saída da janela de console hello. Observe que os valores hello fornecidos aqui são apenas para fins de por exemplo.

    `Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`

    aplicativo de serviço Hello imprime o endereço de saudação do toohello console janela na qual ele está escutando, como visto no exemplo a seguir de saudação.

    `Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`
10. Em Olá **EchoClient** janela de console, digite Olá as mesmas informações que você inseriu anteriormente para o aplicativo de serviço hello. Siga Olá Olá de tooenter etapas anteriores mesmo namespace de serviço e a SAS valores para o aplicativo de cliente hello de chave.
11. Depois de inserir esses valores, o cliente de saudação abre um canal toohello serviço e solicita que você tooenter algum texto, como visto no hello exemplo de saída do console a seguir.

    `Enter text tooecho (or [Enter] tooexit):`

    Insira algum aplicativo de serviço do texto toosend toohello e pressione Enter. Esse texto é enviado toohello serviço por meio de operação de serviço de eco de saudação e aparece na janela de console de serviço hello como Olá saída de exemplo a seguir.

    `Echoing: My sample text`

    aplicativo de cliente Hello recebe o valor de retorno de saudação do hello `Echo` operação, que é o texto de saudação original e a imprime tooits janela de console. a seguir Olá é exemplo de saída da janela de console de cliente hello.

    `Server echoed: My sample text`
12. Você pode continuar a enviar mensagens de texto do serviço de toohello cliente Olá dessa maneira. Quando tiver terminado, pressione Enter no hello cliente e serviço console windows tooend ambos os aplicativos.

## <a name="next-steps"></a>Próximas etapas

Este tutorial mostrou como toobuild um aplicativo de cliente de retransmissão do Azure e o serviço usando Olá recursos de retransmissão do WCF do barramento de serviço. Para obter um tutorial semelhante que usa o [Sistema de Mensagens do Barramento de Serviço](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), consulte a [Introdução às filas do Barramento de Serviço](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).

toolearn mais informações sobre a retransmissão do Azure, consulte Olá tópicos a seguir.

* [Visão geral da arquitetura de Barramento de Serviço do Azure](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [Visão geral da Retransmissão do Azure](relay-what-is-it.md)
* [Como o serviço com o .NET de retransmissão toouse Olá WCF](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
