---
title: "tutorial de REST de barramento aaaService usando a retransmissão do Azure | Microsoft Docs"
description: "Compile um aplicativo host simples de retransmissão do Barramento de Serviço do Azure que expõe uma interface baseada em REST."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1312b2db-94c4-4a48-b815-c5deb5b77a6a
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2017
ms.author: sethm
ms.openlocfilehash: b68650993a0390e7cef891ccb4236095cd86d4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a>Tutorial do REST de Retransmissão de WCF do Azure

Este tutorial descreve como toobuild uma retransmissão Azure simples hospedar o aplicativo que expõe uma interface baseada em REST. REST permite que um cliente da web, como um navegador da web, Olá tooaccess solicitações de APIs do barramento de serviço por meio de HTTP.

Olá tutorial usa o modelo tooconstruct programação Olá REST do Windows Communication Foundation (WCF) um serviço REST no barramento de serviço. Para obter mais informações, consulte [modelo de programação WCF REST](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) e [Projetando e Implementando serviços](/dotnet/framework/wcf/designing-and-implementing-services) em Olá documentação do WCF.

## <a name="step-1-create-a-namespace"></a>Etapa 1: criar um namespace

usando toobegin Olá recursos de retransmissão no Azure, você deve primeiro criar um namespace de serviço. Um namespace fornece um contêiner de escopo para endereçar recursos do Azure dentro de seu aplicativo. Siga Olá [as instruções aqui](relay-create-namespace-portal.md) toocreate um namespace de retransmissão.

## <a name="step-2-define-a-rest-based-wcf-service-contract-toouse-with-azure-relay"></a>Etapa 2: Definir uma toouse de contrato de serviço WCF com base em REST com retransmissão do Azure

Quando você cria um serviço WCF no estilo REST, você deve definir o contrato de saudação. contrato de saudação especifica quais operações Olá host oferece suporte a. Uma operação de serviço pode ser considerada um método de serviço Web. Os contratos são criados pela definição de uma interface C++, C# ou Visual Basic. Cada método na interface de saudação corresponde tooa operação de serviço específico. Olá [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) atributo deve ser aplicado tooeach interface e Olá [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) atributo deve ser aplicado tooeach operação. Se um método em uma interface que tem Olá [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) não tem Olá [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), tal método não será exposto. código de saudação usado para essas tarefas é mostrado no exemplo de Olá Olá procedimento a seguir.

Olá, principal diferença entre um contrato WCF e um contrato estilo REST é Olá adição de uma propriedade toohello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx). Essa propriedade permite que você toomap um método em seu método tooa de interface em hello outro lado da interface de saudação. Nesse caso, usaremos [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink tooHTTP um método GET. Isso permite que o barramento de serviço tooaccurately recuperar e interprete os comandos enviados toohello interface.

### <a name="toocreate-a-contract-with-an-interface"></a>toocreate um contrato com uma interface

1. Abra o Visual Studio como administrador: programa de saudação com o botão direito no hello **iniciar** menu e clique **executar como administrador**.
2. Crie um novo projeto de aplicativo de console. Clique em Olá **arquivo** menu e selecione **novo**, em seguida, selecione **projeto**. Em Olá **novo projeto** caixa de diálogo, clique em **Visual C#**, selecione Olá **aplicativo de Console** modelo e nomeie-o **ImageListener**. Usar saudação padrão **local**. Clique em **Okey** toocreate projeto de saudação.
3. Para um projeto C#, o Visual Studio cria um arquivo `Program.cs`. Essa classe contém vazio `Main()` método, necessário para um toobuild de projeto de aplicativo de console corretamente.
4. Adicionar referências tooService barramento e **System.ServiceModel.dll** toohello projeto instalando o pacote do NuGet do barramento de serviço hello. Esse pacote adiciona automaticamente referências toohello Service Bus bibliotecas, bem como Olá WCF **System. ServiceModel**. No Gerenciador de soluções, clique com botão direito Olá **ImageListener** do projeto e, em seguida, clique em **gerenciar pacotes NuGet**. Clique em Olá **procurar** guia e, em seguida, procurar `Microsoft Azure Service Bus`. Clique em **instalar**e aceite os termos de uso do hello.
5. Você deve adicionar explicitamente uma referência muito**System** toohello projeto:
   
    a. No Gerenciador de soluções, clique com botão direito Olá **referências** pasta sob a pasta do projeto hello e depois clique em **adicionar referência**.
   
    b. Em Olá **adicionar referência** caixa de diálogo, clique em Olá **Framework** guia no lado esquerdo da saudação e em Olá **pesquisa** , digite **System.ServiceModel.Web** . Selecione Olá **System.ServiceModel.Web** caixa de seleção e, em seguida, clique em **Okey**.
6. Adicione o seguinte Olá `using` instruções na parte superior de saudação do arquivo Program.cs de saudação.
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    [System. ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) é namespace Olá que habilita os recursos de toobasic acesso programático do WCF. Retransmissão do WCF usa muitos dos objetos hello e atributos de contratos de serviço do WCF toodefine. Você usará este namespace na maioria dos seus aplicativos de retransmissão. Da mesma forma, [Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) ajuda a definir canal hello, que é o objeto Olá por meio do qual você se comunica com o navegador de cliente de retransmissão do Azure e hello. Por fim, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contém tipos de saudação que permitem a você aplicativos toocreate da web.
7. Renomear Olá `ImageListener` namespace muito**Samples**.
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. Diretamente após Olá chave de abertura da declaração de namespace hello, definir uma nova interface chamada **IImageContract** e aplicar Olá **ServiceContractAttribute** interface de toohello de atributo com um valor de `http://samples.microsoft.com/ServiceModel/Relay/`. valor de namespace Olá difere do namespace Olá que você usa em todo o escopo de saudação do seu código. valor de namespace Olá é usado como um identificador exclusivo para este contrato e deve ter informações de versão. Para saber mais, veja [Controle de Versão do Serviço](http://go.microsoft.com/fwlink/?LinkID=180498). Especificar explicitamente o namespace de saudação impede que o valor de namespace padrão Olá seja adicionado a toohello do nome do contrato.
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. Dentro de saudação `IImageContract` interface, declare um método para Olá Olá de única operação `IImageContract` expõe contrato em Olá interface e aplique Olá `OperationContractAttribute` toohello método que você deseja tooexpose como parte do serviço de público Olá barramento de atributo contrato.
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. Em Olá **OperationContract** atributo, adicionar Olá **WebGet** valor.
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    Isso permite Olá tooroute do serviço de retransmissão solicitações HTTP GET muito`GetImage`e tootranslate hello retornar valores de `GetImage` em uma resposta HTTP GETRESPONSE. Posteriormente no tutorial hello, você usará um tooaccess do navegador da web este método e imagem de saudação toodisplay no navegador de saudação.
11. Depois de saudação `IImageContract` definição, declare um canal que herda de ambos os Olá `IImageContract` e `IClientChannel` interfaces.
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    Um canal é o objeto WCF de saudação por meio do qual cliente e serviço Olá passam informações tooeach outros. Posteriormente, você criará o canal Olá em seu aplicativo de host. Retransmissão do Azure, em seguida, usa esse canal toopass Olá das solicitações HTTP GET do hello navegador tooyour **GetImage** implementação. retransmissão de saudação também usa Olá Olá de tootake de canal **GetImage** valor de retorno e convertê-lo em uma GETRESPONSE HTTP para o navegador de saudação do cliente.
12. De saudação **criar** menu, clique em **compilar solução** tooconfirm precisão de saudação do seu trabalho até o momento.

### <a name="example"></a>Exemplo
saudação de código a seguir mostra uma interface básica que define um contrato de retransmissão do WCF.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="step-3-implement-a-rest-based-wcf-service-contract-toouse-service-bus"></a>Etapa 3: Implementar uma toouse de contrato de serviço WCF com base em REST do barramento do serviço
Criar um serviço de retransmissão do WCF no estilo REST requer que você primeiro crie contrato hello, que é definido por meio de uma interface. Olá próxima etapa é a interface de saudação tooimplement. Isso envolve a criação de uma classe denominada **ImageService** que implementa Olá definidos pelo usuário **IImageContract** interface. Depois de implementar o contrato hello, você configura Olá interface usando um arquivo App. config. arquivo de configuração de saudação contém as informações necessárias para o aplicativo hello, como nome de saudação do serviço Olá, nome de saudação do contrato hello e tipo de saudação do protocolo é toocommunicate usado com o serviço de retransmissão hello. código de saudação usado para essas tarefas é fornecido no exemplo hello Olá procedimento a seguir.

Como com as etapas anteriores do hello, há muito pouca diferença entre implementar um contrato estilo REST e um contrato de retransmissão do WCF.

### <a name="tooimplement-a-rest-style-service-bus-contract"></a>contrato do barramento de serviço tooimplement um estilo REST
1. Criar uma nova classe chamada **ImageService** diretamente após a definição de saudação do hello **IImageContract** interface. Olá **ImageService** classe implementa Olá **IImageContract** interface.
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    Implementações de interface tooother semelhante, você pode implementar definição Olá em um arquivo diferente. No entanto, para este tutorial, implementação Olá aparece no hello mesmo arquivo como definição de interface hello e `Main()` método.
2. Aplicar Olá [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) atributo toohello **IImageService** tooindicate de classe que Olá classe é uma implementação de um contrato WCF.
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    Conforme mencionado anteriormente, esse namespace não é um namespace tradicional. Em vez disso, ele faz parte da saudação arquitetura do WCF que identifica o contrato de saudação. Para obter mais informações, consulte Olá [nomes de contrato de dados](https://msdn.microsoft.com/library/ms731045.aspx) tópico Olá documentação do WCF.
3. Adicione um projeto de tooyour de imagem. jpg.  
   
    Esta é uma imagem que exibe serviço Olá Olá recebendo o navegador. Clique com o botão direito do mouse em seu projeto e clique em **Adicionar**. Em seguida, clique em **Item Existente**. Saudação de uso **Add Existing Item** tooan de toobrowse de caixa de diálogo apropriado. jpg e, em seguida, clique em **adicionar**.
   
    Ao adicionar arquivo hello, certifique-se de que **todos os arquivos** está selecionado no hello lista suspensa próxima toohello **nome do arquivo:** campo. rest Olá deste tutorial presume que Olá nome da imagem de saudação é "image.jpg". Se você tiver um arquivo diferente, você será ter toorename Olá imagem ou alterar toocompensate seu código.
4. toomake-se de que Olá executando o serviço pode encontrar o arquivo de imagem de hello, em **Solution Explorer** clique com o arquivo de imagem hello e clique em **propriedades**. Em Olá **propriedades** painel, defina **copiar tooOutput diretório** muito**copiar se mais recente**.
5. Adicionar uma referência toohello **System.Drawing.dll** toohello de assembly do projeto e também adicionar seguintes Olá `using` instruções.  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. Em Olá **ImageService** de classe, adicione Olá seguinte construtor que carrega Olá bitmap e prepara toosend-toohello o navegador do cliente.
   
    ```csharp
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";
   
        Image bitmap;
   
        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }
    }
    ```
7. Diretamente após o código anterior do hello, adicione o seguinte de saudação **GetImage** método hello **ImageService** mensagem tooreturn um HTTP de classe que contém a imagem de saudação.
   
    ```csharp
    public Stream GetImage()
    {
        MemoryStream stream = new MemoryStream();
        this.bitmap.Save(stream, ImageFormat.Jpeg);
   
        stream.Position = 0;
        WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
   
        return stream;
    }
    ```
   
    Essa implementação usa **MemoryStream** tooretrieve Olá imagem e prepará-la para streaming toohello navegador. Inicia a posição de fluxo de saudação em zero, declara o conteúdo de fluxo hello como jpeg e transmite informações hello.
8. De saudação **criar** menu, clique em **compilar solução**.

### <a name="toodefine-hello-configuration-for-running-hello-web-service-on-service-bus"></a>configuração de saudação toodefine para executar o serviço da web de saudação no barramento de serviço
1. Em **Solution Explorer**, clique duas vezes em **App. config** tooopen-lo no editor do Visual Studio hello.
   
    Olá **App. config** arquivo inclui Olá nome, o ponto de extremidade (ou seja, local Olá retransmissão Azure expõe para clientes e hosts toocommunicate uns com os outros) e associação (tipo de saudação do protocolo é usado toocommunicate). Olá diferença principal aqui é aquele ponto de extremidade de serviço Olá configurado refere-se tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) associação.
2. Olá `<system.serviceModel>` XML é um elemento WCF que define um ou mais serviços. Aqui, é o ponto de extremidade e o nome de serviço de saudação toodefine usado. Na parte inferior de saudação do hello `<system.serviceModel>` elemento (mas ainda dentro `<system.serviceModel>`), adicione um `<bindings>` elemento que tem Olá conteúdo a seguir. Isso define associações de saudação usadas no aplicativo hello. É possível definir várias associações, mas para este tutorial você definirá apenas uma.
   
    ```xml
    <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
            <binding name="default">
                <security relayClientAuthenticationType="None" />
            </binding>
        </webHttpRelayBinding>
    </bindings>
    ```
   
    código anterior Olá define uma retransmissão WCF [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) associação com **relayClientAuthenticationType** definido muito**nenhum**. Essa configuração indica que um ponto de extremidade usando essa associação não exige uma credencial de cliente.
3. Depois de saudação `<bindings>` elemento, adicionar um `<services>` elemento. Associações toohello semelhante, você pode definir vários serviços em um único arquivo de configuração. No entanto, para este tutorial, você definirá apenas um.
   
    ```xml
    <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
            <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IImageContract"
                    binding="webHttpRelayBinding"
                    bindingConfiguration="default"
                    behaviorConfiguration="sbTokenProvider"
                    address="" />
        </service>
    </services>
    ```
   
    Esta etapa configura um serviço que usa o padrão de saudação definida anteriormente **webHttpRelayBinding**. Ele também usa o padrão de saudação **sbTokenProvider**, que é definida na próxima etapa do hello.
4. Depois de saudação `<services>` elemento, criar um `<behaviors>` elemento com hello conteúdo a seguir, substituindo "SAS_KEY" com hello *assinatura de acesso compartilhado* chave (SAS) obtido anteriormente Olá [portal do Azure ][Azure portal].
   
    ```xml
    <behaviors>
        <endpointBehaviors>
            <behavior name="sbTokenProvider">
                <transportClientEndpointBehavior>
                    <tokenProvider>
                        <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
                    </tokenProvider>
                </transportClientEndpointBehavior>
            </behavior>
            </endpointBehaviors>
            <serviceBehaviors>
                <behavior name="default">
                    <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
                </behavior>
            </serviceBehaviors>
    </behaviors>
    ```
5. Ainda no App. config no hello `<appSettings>` elemento, substituir valor de cadeia de caracteres de conexão inteira Olá com a cadeia de caracteres de conexão de saudação obtido anteriormente do portal de saudação. 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. De saudação **criar** menu, clique em **compilar solução** toobuild Olá toda a solução.

### <a name="example"></a>Exemplo
Olá, código seguinte mostra Olá implementação de contrato e serviço para um serviço baseado em REST que está em execução no barramento de serviço usando Olá **WebHttpRelayBinding** associação.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{


    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

Olá, exemplo a seguir mostra arquivo App. config de saudação associado ao serviço de saudação.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove hello ones they don't need. -->
            <behaviorExtensions>
                <add name="connectionStatusBehavior"
                    type="Microsoft.ServiceBus.Configuration.ConnectionStatusElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="transportClientEndpointBehavior"
                    type="Microsoft.ServiceBus.Configuration.TransportClientEndpointBehaviorElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="serviceRegistrySettings"
                    type="Microsoft.ServiceBus.Configuration.ServiceRegistrySettingsElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </behaviorExtensions>
            <bindingElementExtensions>
                <add name="netMessagingTransport"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingTransportExtensionElement, Microsoft.ServiceBus,  Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="tcpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.TcpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpsRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpsRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="onewayRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.RelayedOnewayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingElementExtensions>
            <bindingExtensions>
                <add name="basicHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.BasicHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="webHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WebHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="ws2007HttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WS2007HttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netOnewayRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetOnewayRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netEventRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetEventRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netMessagingBinding"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingExtensions>
        </extensions>
      <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
          <binding name="default">
            <security relayClientAuthenticationType="None" />
          </binding>
        </webHttpRelayBinding>
      </bindings>
      <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
          <endpoint name="RelayEndpoint"
                  contract="Microsoft.ServiceBus.Samples.IImageContract"
                  binding="webHttpRelayBinding"
                  bindingConfiguration="default"
                  behaviorConfiguration="sbTokenProvider"
                  address="" />
        </service>
      </services>
      <behaviors>
        <endpointBehaviors>
          <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
        <serviceBehaviors>
          <behavior name="default">
            <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
          </behavior>
        </serviceBehaviors>
      </behaviors>
    </system.serviceModel>
    <appSettings>
        <!-- Service Bus specific app setings for messaging connections -->
        <add key="Microsoft.ServiceBus.ConnectionString"
            value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey="YOUR_SAS_KEY"/>
    </appSettings>
</configuration>
```

## <a name="step-4-host-hello-rest-based-wcf-service-toouse-azure-relay"></a>Etapa 4: Host Olá WCF com base em REST serviço toouse retransmissão do Azure
Essa etapa descreve como toorun um web serviço usando um aplicativo de console com retransmissão do WCF. Uma lista completa de código Olá gravado nesta etapa é fornecida no exemplo hello Olá procedimento a seguir.

### <a name="toocreate-a-base-address-for-hello-service"></a>um endereço base para o serviço de saudação do toocreate
1. Em Olá `Main()` declaração de função, criar um namespace de saudação toostore variável do seu projeto. Certifique-se de que tooreplace `yourNamespace` com o nome de saudação do namespace de retransmissão Olá criado anteriormente.
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    Barramento de serviço usa o nome de saudação do seu namespace de toocreate um URI exclusivo.
2. Criar um `Uri` instância para endereço básico de saudação do serviço de saudação que é baseado no namespace de saudação.
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="toocreate-and-configure-hello-web-service-host"></a>toocreate e configurar o host de serviço da web hello
* Crie o host de serviço web hello, usando o endereço URI Olá criado anteriormente nesta seção.
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    host de serviço de saudação é objeto WCF Olá que instancia o aplicativo de host hello. Este exemplo passa o tipo de saudação de host que você deseja toocreate (um **ImageService**), e também Olá endereço no qual você deseja que o aplicativo de host tooexpose hello.

### <a name="toorun-hello-web-service-host"></a>host de serviço toorun Olá web
1. Abra o serviço de saudação.
   
    ```csharp
    host.Open();
    ```
    serviço de saudação agora está em execução.
2. Exiba uma mensagem indicando que o serviço hello está sendo executado e como toostop Olá serviço.
   
    ```csharp
    Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. Quando terminar, feche o host de serviço hello.
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a>Exemplo
saudação de exemplo a seguir inclui o contrato de serviço hello e a implementação de etapas anteriores no serviço de saudação tutorial e hosts de saudação em um aplicativo de console. Compile Olá código a seguir em um executável chamado ImageListener.exe.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string serviceNamespace = "InsertServiceNamespaceHere";
            Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");

            WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
            host.Open();

            Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-hello-code"></a>Compilando o código de saudação
Depois de criar a solução hello, Olá toorun Olá aplicativos a seguir:

1. Pressione **F5**, ou procure o local do arquivo executável toohello (ImageListener\bin\Debug\ImageListener.exe), serviço de saudação toorun. Lembre-Olá aplicativo em execução, pois ela será necessária a próxima etapa do tooperform Olá.
2. Copie e cole o endereço de saudação do prompt de comando de saudação em uma imagem de saudação do navegador toosee.
3. Quando tiver terminado, pressione **Enter** no aplicativo de Olá Olá prompt de comando janela tooclose.

## <a name="next-steps"></a>Próximas etapas
Agora que você construiu um aplicativo que usa o serviço de retransmissão do barramento de serviço hello, consulte Olá toolearn artigos mais sobre Azure retransmissão a seguir:

* [Visão geral da arquitetura de Barramento de Serviço do Azure](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [Visão geral da Retransmissão do Azure](relay-what-is-it.md)
* [Como o serviço com o .NET de retransmissão toouse Olá WCF](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
