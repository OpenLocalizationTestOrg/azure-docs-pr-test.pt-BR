---
title: "aaaAzure aplicativo de no local/em nuvem híbrido de retransmissão do WCF (.NET) | Microsoft Docs"
description: "Saiba como aplicativo híbrido de toocreate uma .NET no local/em nuvem usando a retransmissão do WCF do Azure."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9ed02f7c-ebfb-4f39-9c97-b7dc15bcb4c1
ms.service: service-bus-relay
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: sethm
ms.openlocfilehash: aab8b1dbdc85c4edf7b0ccef0921b69524b2d306
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a>Aplicativo híbrido .NET local/na nuvem usando a Retransmissão do WCF do Azure
## <a name="introduction"></a>Introdução

Este artigo mostra como toobuild híbridos nuvem aplicativo com o Microsoft Azure e o Visual Studio. tutorial de Olá pressupõe não que nenhuma experiência anterior com o Azure. Em menos de 30 minutos, você terá um aplicativo que utiliza vários recursos do Azure e em execução na nuvem hello.

Você aprenderá:

* Como toocreate ou adaptar um serviço da web existente para consumo por uma solução de web.
* Como toouse Olá tooshare dados do serviço de retransmissão do WCF do Azure entre um aplicativo do Azure e um serviço web hospedado em outro lugar.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a>Como a Retransmissão do Azure ajuda com soluções híbridas

Soluções de negócios são geralmente compostas de uma combinação de código personalizado escrito tootackle novo e necessidades de negócios e a funcionalidade existente fornecidas por soluções e os sistemas que já estão em vigor.

Arquitetos de solução estão começando a nuvem de saudação toouse para manipular mais fácil de reduzir os custos operacionais e de requisitos de escala. Dessa forma, eles localizam que ativos existentes do serviço eles gostariam tooleverage como blocos de construção para suas soluções estão dentro do firewall corporativo hello e fora de fácil acessar para acesso pela solução de nuvem hello. Muitos serviços internos não são criados ou hospedados de forma que eles podem ser facilmente expostos na borda da rede corporativa de saudação.

[Retransmissão do Azure](https://azure.microsoft.com/services/service-bus/) foi projetado para Olá caso de uso de executar os serviços de web do Windows Communication Foundation (WCF) existentes e tornar os serviços acessíveis com segurança toosolutions que residem fora do perímetro corporativo Olá sem a necessidade de infraestrutura de rede corporativa toohello alterações intrusiva. Esses serviços de retransmissão ainda estão hospedados dentro de seu ambiente existente, mas eles delegarem para o serviço de retransmissão hospedado na nuvem de toohello entrado de sessões e solicitações de escuta. A Retransmissão do Azure também protege esses serviços contra acesso não autorizado usando a autenticação [SAS (Assinatura de Acesso Compartilhado)](../service-bus-messaging/service-bus-sas.md).

## <a name="solution-scenario"></a>Cenário da solução
Neste tutorial, você criará um site ASP.NET que permite que você toosee uma lista de produtos na página de estoque de produto hello.

![][0]

tutorial de saudação presume que você tem informações de produto em um sistema local existente e usa o Azure retransmissão tooreach no sistema. Isso é simulado por um serviço Web executado em um aplicativo de console simples e com o suporte de um conjunto de produtos na memória. Você será capaz de toorun esse aplicativo de console em seu próprio computador e implantar a função de web Olá no Azure. Fazendo isso, você verá como função de web hello em execução no hello datacenter do Azure, na verdade, chamará em seu computador, mesmo que seu computador certamente residirá por trás de pelo menos um firewall e uma camada de conversão (NAT) do endereço de rede.

## <a name="set-up-hello-development-environment"></a>Configurar o ambiente de desenvolvimento Olá

Antes de começar a desenvolver aplicativos do Azure, baixe ferramentas hello e configurar seu ambiente de desenvolvimento:

1. Instalar hello Azure SDK para .NET de saudação SDK [página de downloads](https://azure.microsoft.com/downloads/).
2. Em Olá **.NET** coluna, clique na versão de saudação do [Visual Studio](http://www.visualstudio.com) você está usando. Olá as etapas deste tutorial usam Visual Studio 2015, mas elas também funcionam com o Visual Studio de 2017.
3. Quando solicitado toorun ou salvar instalador hello, clique em **executar**.
4. Em Olá **Web Platform Installer**, clique em **instalar** e prosseguir com a instalação de saudação.
5. Após a conclusão da instalação hello, você terá tudo necessário toostart toodevelop Olá aplicativo. Olá SDK inclui ferramentas que permitem a fácil desenvolver aplicativos do Azure no Visual Studio.

## <a name="create-a-namespace"></a>Criar um namespace

usando toobegin Olá recursos de retransmissão no Azure, você deve primeiro criar um namespace de serviço. Um namespace fornece um contêiner de escopo para endereçar recursos do Azure dentro de seu aplicativo. Siga Olá [as instruções aqui](relay-create-namespace-portal.md) toocreate um namespace de retransmissão.

## <a name="create-an-on-premises-server"></a>Criar um servidor local

Primeiro você irá criar um sistema de catálogo de produtos (fictício) local. É bem simple; Você pode ver isso como a representação de um sistema de catálogo de produto real no local com uma superfície de serviço completo que estamos tentando toointegrate.

Este projeto é um aplicativo de console do Visual Studio e usa Olá [pacote NuGet do Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude Olá bibliotecas de barramento de serviço e as definições de configuração.

### <a name="create-hello-project"></a>Criar projeto Olá

1. Utilizando privilégios do administrador, inicie o Microsoft Visual Studio. toodo então, clique no ícone de programa do Visual Studio hello e clique **executar como administrador**.
2. No Visual Studio, no hello **arquivo** menu, clique em **novo**e, em seguida, clique em **projeto**.
3. Em **Modelos Instalados**, em **Visual C#**, clique em **Aplicativo de Console (.NET Framework)**. Em Olá **nome** caixa, digite o nome de saudação **ProductsServer**:

   ![][11]
4. Clique em **Okey** toocreate Olá **ProductsServer** projeto.
5. Se você já tiver instalado o Gerenciador de pacotes do NuGet Olá para o Visual Studio, ignore toohello próxima etapa. Caso contrário, visite [NuGet][NuGet] e clique em [Instalar NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c). Siga os prompts Olá Olá tooinstall Gerenciador do pacote NuGet, em seguida, reinicie o Visual Studio.
6. No Gerenciador de soluções, clique com botão direito Olá **ProductsServer** projeto e, em seguida, clique em **gerenciar pacotes NuGet**.
7. Clique em Olá **procurar** guia e, em seguida, procurar `Microsoft Azure Service Bus`. Selecione Olá **windowsazure. ServiceBus** pacote.
8. Clique em **instalar**e aceite os termos de uso do hello.

   ![][13]

   Observe que Olá necessário assemblies de cliente agora são referenciados.
8. Adicione uma nova classe para seu contrato de produto. No Gerenciador de soluções, clique com botão direito Olá **ProductsServer** do projeto e clique em **adicionar**e, em seguida, clique em **classe**.
9. Em Olá **nome** caixa, digite o nome de saudação **ProductsContract.cs**. Clique em **Adicionar**.
10. Em **ProductsContract.cs**, substitua definição de namespace Olá Olá código, que define o contrato de saudação para serviço de saudação a seguir.

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define hello data contract for hello service
        [DataContract]
        // Declare hello serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define hello service contract.
        [ServiceContract]
        interface IProducts
        {
            [OperationContract]
            IList<ProductData> GetProducts();

        }

        interface IProductsChannel : IProducts, IClientChannel
        {
        }
    }
    ```
11. Em Program.cs, substitua definição de namespace Olá Olá seguindo o código, que adiciona o serviço de perfil hello e host Olá para ele.

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement hello IProducts interface.
        class ProductsService : IProducts
        {

            // Populate array of products for display on website
            ProductData[] products =
                new []
                    {
                        new ProductData{ Id = "1", Name = "Rock",
                                         Quantity = "1"},
                        new ProductData{ Id = "2", Name = "Paper",
                                         Quantity = "3"},
                        new ProductData{ Id = "3", Name = "Scissors",
                                         Quantity = "5"},
                        new ProductData{ Id = "4", Name = "Well",
                                         Quantity = "2500"},
                    };

            // Display a message in hello service console application
            // when hello list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define hello Main() function in hello service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER tooclose");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. No Solution Explorer, clique duas vezes em Olá **App. config** arquivo tooopen-lo no editor do Visual Studio hello. Na parte inferior de saudação do hello `<system.ServiceModel>` elemento (mas ainda dentro `<system.ServiceModel>`), adicionar Olá código XML a seguir. Ser tooreplace se *yourServiceNamespace* com o nome de saudação do seu namespace, e *yourKey* com a chave SAS Olá anteriormente, você recuperou do portal de saudação:

    ```xml
    <system.serviceModel>
    ...
      <services>
         <service name="ProductsServer.ProductsService">
           <endpoint address="sb://yourServiceNamespace.servicebus.windows.net/products" binding="netTcpRelayBinding" contract="ProductsServer.IProducts" behaviorConfiguration="products"/>
         </service>
      </services>
      <behaviors>
         <endpointBehaviors>
           <behavior name="products">
             <transportClientEndpointBehavior>
                <tokenProvider>
                   <sharedAccessSignature keyName="RootManageSharedAccessKey" key="yourKey" />
                </tokenProvider>
             </transportClientEndpointBehavior>
           </behavior>
         </endpointBehaviors>
      </behaviors>
    </system.serviceModel>
    ```
13. Ainda no App. config no hello `<appSettings>` elemento, substituir valor de cadeia de caracteres de conexão Olá com a cadeia de caracteres de conexão de saudação obtido anteriormente do portal de saudação.

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. Pressione **Ctrl + Shift + B** ou de saudação **criar** menu, clique em **compilar solução** toobuild Olá aplicativo e verificar a precisão de saudação do seu trabalho até o momento.

## <a name="create-an-aspnet-application"></a>Criar um aplicativo ASP.NET

Nesta seção você criará um aplicativo ASP.NET simples que exibe os dados recuperados do seu serviço de produto.

### <a name="create-hello-project"></a>Criar projeto Olá

1. Certifique-se de que o Visual Studio está sendo executado com os privilégios de administrador.
2. No Visual Studio, no hello **arquivo** menu, clique em **novo**e, em seguida, clique em **projeto**.
3. Em **Modelos Instalados**, em **Visual C#**, clique em **Aplicativo Web ASP.NET (.NET Framework)**. Projeto de saudação do nome **ProductsPortal**. Em seguida, clique em **OK**.

   ![][15]

4. De saudação **modelos ASP.NET** lista Olá **novo aplicativo Web ASP.NET** caixa de diálogo, clique em **MVC**.

   ![][16]

6. Clique em Olá **alterar autenticação** botão. Em Olá **alterar autenticação** caixa de diálogo caixa, certifique-se de que **sem autenticação** está selecionado e, em seguida, clique em **Okey**. Para este tutorial, você está implantando um aplicativo que não precisa de um logon de usuário.

    ![][18]

7. Em Olá **novo aplicativo Web ASP.NET** caixa de diálogo, clique em **Okey** toocreate Olá MVC aplicativo.
8. Agora você deve configurar os recursos do Azure para um novo aplicativo Web. Siga as etapas de Olá Olá [publicar tooAzure seção deste artigo](../app-service-web/app-service-web-get-started-dotnet.md). Em seguida, retorne toothis tutorial e continue toohello próxima etapa.
10. No Gerenciador de Soluções, clique com o botão direito do mouse em **Modelos**, clique em **Adicionar** e em **Classe**. Em Olá **nome** caixa, digite o nome de saudação **Product.cs**. Clique em **Adicionar**.

    ![][17]

### <a name="modify-hello-web-application"></a>Modificar o aplicativo da web hello

1. No arquivo de Product.cs Olá no Visual Studio, substitua definição de namespace existentes Olá Olá código a seguir.

   ```csharp
    // Declare properties for hello products inventory.
    namespace ProductsWeb.Models
    {
       public class Product
       {
           public string Id { get; set; }
           public string Name { get; set; }
           public string Quantity { get; set; }
       }
    }
    ```
2. No Gerenciador de soluções, expanda Olá **controladores** pasta, clique duas vezes em hello **HomeController** tooopen de arquivo no Visual Studio.
3. Em **HomeController**, substitua definição de namespace existentes Olá Olá código a seguir.

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of hello products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. No Gerenciador de soluções, expanda a pasta exibições \ compartilhadas de saudação e, em seguida, clique duas vezes em **cshtml** tooopen-lo no editor do Visual Studio hello.
5. Alterar todas as ocorrências de **meu aplicativo ASP.NET** muito**produtos da LITWARE**.
6. Remover Olá **início**, **sobre**, e **contato** links. Olá exemplo a seguir, exclua código Olá realçado.

    ![][41]

7. No Gerenciador de soluções, expanda a pasta de Views\Home de saudação e, em seguida, clique duas vezes em **cshtml** tooopen-lo no editor do Visual Studio hello. Substitua todo o conteúdo do arquivo de Olá Olá Olá código a seguir.

   ```html
   @model IEnumerable<ProductsWeb.Models.Product>

   @{
            ViewBag.Title = "Index";
   }

   <h2>Prod Inventory</h2>

   <table>
             <tr>
                 <th>
                     @Html.DisplayNameFor(model => model.Name)
                 </th>
                 <th></th>
                 <th>
                     @Html.DisplayNameFor(model => model.Quantity)
                 </th>
             </tr>

   @foreach (var item in Model) {
             <tr>
                 <td>
                     @Html.DisplayFor(modelItem => item.Name)
                 </td>
                 <td>
                     @Html.DisplayFor(modelItem => item.Quantity)
                 </td>
             </tr>
   }

   </table>
   ```
8. precisão de saudação tooverify de seu trabalho até o momento, você pode pressionar **Ctrl + Shift + B** toobuild projeto de saudação.

### <a name="run-hello-app-locally"></a>Executar o aplicativo hello localmente

Execute Olá aplicativo tooverify que ele funciona.

1. Certifique-se de que **ProductsPortal** é saudação do projeto ativo. Nome do projeto Olá no Gerenciador de soluções e selecione **definir como projeto de inicialização**.
2. No Visual Studio, pressione **F5**.
3. Seu aplicativo deve aparecer em execução em um navegador.

   ![][21]

## <a name="put-hello-pieces-together"></a>Juntar Olá peças

Olá próxima etapa é toohook servidor de produtos de local de saudação com hello aplicativo ASP.NET.

1. Se ainda não estiver aberto, no Visual Studio reabra Olá **ProductsPortal** projeto criado no hello [criar um aplicativo ASP.NET](#create-an-aspnet-application) seção.
2. Etapa de toohello semelhante na seção de "Criar um servidor de local" Olá, adicionar referências de projeto toohello do pacote de NuGet hello. No Gerenciador de soluções, clique com botão direito Olá **ProductsPortal** projeto e, em seguida, clique em **gerenciar pacotes NuGet**.
3. Pesquisa por "Service Bus" e selecione Olá **windowsazure. ServiceBus** item. Em seguida, concluir instalação hello e fechar esta caixa de diálogo.
4. No Gerenciador de soluções, clique com botão direito Olá **ProductsPortal** projeto e, em seguida, clique em **adicionar**, em seguida, **Item existente**.
5. Navegue toohello **ProductsContract.cs** arquivo hello **ProductsServer** projeto de console. Clique em toohighlight ProductsContract.cs. Clique Olá a seta para baixo próxima muito**adicionar**, em seguida, clique em **adicionar como vínculo**.

   ![][24]

6. Agora, abra Olá **HomeController** no editor do Visual Studio hello e substitua a definição de namespace Olá Olá código a seguir. Ser tooreplace se *yourServiceNamespace* com o nome de saudação do seu namespace de serviço, e *yourKey* com a sua chave SAS. Isso permitirá que o serviço Olá cliente toocall Olá local, retornando resultados de saudação da chamada de saudação.

   ```csharp
   namespace ProductsWeb.Controllers
   {
       using System.Linq;
       using System.ServiceModel;
       using System.Web.Mvc;
       using Microsoft.ServiceBus;
       using Models;
       using ProductsServer;

       public class HomeController : Controller
       {
           // Declare hello channel factory.
           static ChannelFactory<IProductsChannel> channelFactory;

           static HomeController()
           {
               // Create shared access signature token credentials for authentication.
               channelFactory = new ChannelFactory<IProductsChannel>(new NetTcpRelayBinding(),
                   "sb://yourServiceNamespace.servicebus.windows.net/products");
               channelFactory.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior {
                   TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                       "RootManageSharedAccessKey", "yourKey") });
           }

           public ActionResult Index()
           {
               using (IProductsChannel channel = channelFactory.CreateChannel())
               {
                   // Return a view of hello products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. No Gerenciador de soluções, clique com botão direito Olá **ProductsPortal** solução (certifique-se de que tooright Olá solução clique, não o projeto Olá). Clique em **Adicionar** e depois clique em **Projeto Existente**.
8. Navegue toohello **ProductsServer** de projeto, clique duas vezes Olá **ProductsServer.csproj** tooadd do arquivo de solução-lo.
9. **ProductsServer** devem ser executadas nos dados de saudação do pedido toodisplay na **ProductsPortal**. No Gerenciador de soluções, clique com botão direito Olá **ProductsPortal** solução e clique em **propriedades**. Olá **páginas de propriedade** caixa de diálogo é exibida.
10. No lado esquerdo de saudação, clique em **projeto de inicialização**. Saudação de direita, clique em **vários projetos de inicialização**. Certifique-se de que **ProductsServer** e **ProductsPortal** aparecer, em ordem, com **iniciar** definido como ação Olá para ambos.

      ![][25]

11. Ainda no hello **propriedades** caixa de diálogo, clique em **dependências do projeto** no lado esquerdo de saudação.
12. Em Olá **projetos** lista, clique em **ProductsServer**. Confirme se **ProductsPortal** não está selecionado.
13. Em Olá **projetos** lista, clique em **ProductsPortal**. Verifique se **ServidorDeProdutos** está selecionado.

    ![][26]

14. Clique em **Okey** em Olá **páginas de propriedade** caixa de diálogo.

## <a name="run-hello-project-locally"></a>Executar projeto Olá localmente

aplicativo de hello tootest localmente, no Visual Studio pressione **F5**. servidor de local de saudação (**ProductsServer**) deve iniciar primeiro, Olá **ProductsPortal** aplicativo deve ser iniciado em uma janela do navegador. Neste momento, você verá que o inventário de produto Olá lista os dados recuperados do hello produto serviço no sistema local.

![][10]

Pressione **atualizar** em Olá **ProductsPortal** página. Cada vez que você atualize a página de saudação, você verá Olá server app exibirá uma mensagem quando `GetProducts()` de **ProductsServer** é chamado.

Feche ambos os aplicativos antes da próxima etapa de toohello de continuar.

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a>Implantar o aplicativo web do Azure do hello ProductsPortal projeto tooan

Olá próxima etapa é toorepublish hello Azure Web aplicativo **ProductsPortal** front-end. Olá a seguir:

1. No Gerenciador de soluções, clique com botão direito Olá **ProductsPortal** do projeto e clique em **publicar**. Em seguida, clique em **publicar** em Olá **publicar** página.

  > [!NOTE]
  > Você verá uma mensagem de erro na janela de navegador hello quando hello **ProductsPortal** projeto da web é iniciado automaticamente após a implantação de saudação. Isso é esperado e ocorre porque Olá **ProductsServer** aplicativo não está sendo executado ainda.
>
>

2. Copiar URL de saudação do hello implantado aplicativo web, pois você precisará Olá URL na próxima etapa do hello. Você também pode obter essa URL da janela de atividade de serviço de aplicativo do Azure Olá no Visual Studio:

  ![][9]

3. Feche Olá navegador janela toostop Olá executando o aplicativo.

### <a name="set-productsportal-as-web-app"></a>Defina ProductsPortal como o aplicativo Web

Antes da aplicação de saudação em execução na nuvem hello, você deve garantir que **ProductsPortal** é iniciado a partir do Visual Studio como um aplicativo web.

1. No Visual Studio, clique com botão direito Olá **ProductsPortal** do projeto e, em seguida, clique em **propriedades**.
2. Na coluna esquerda da saudação, clique em **Web**.
3. Em Olá **iniciar ação** seção, clique em Olá **iniciar URL** botão e, na caixa de texto de saudação digite Olá URL para seu aplicativo da web implantados anteriormente; por exemplo, `http://productsportal1234567890.azurewebsites.net/`.

    ![][27]

4. De saudação **arquivo** no Visual Studio, clique em **Salvar tudo**.
5. No menu de compilação Olá no Visual Studio, clique em **recompilar solução**.

## <a name="run-hello-application"></a>Executar o aplicativo hello

1. Pressione F5 toobuild e execute o aplicativo hello. servidor de local de Hello (Olá **ProductsServer** aplicativo de console) deve iniciar primeiro, Olá **ProductsPortal** aplicativo deve ser iniciado em uma janela de navegador, conforme mostrado no hello tela a seguir captura. Observe novamente que o inventário de produto Olá lista os dados recuperados do sistema de local de serviço de produto hello e exibe esses dados de aplicativo da web de saudação. Verificar Olá URL toomake-se de que **ProductsPortal** está em execução na nuvem hello, como um aplicativo web do Azure.

   ![][1]

   > [!IMPORTANT]
   > Olá **ProductsServer** aplicativo de console deve estar em execução e é capaz de tooserve Olá dados toohello **ProductsPortal** aplicativo. Se o navegador Olá exibirá um erro, aguarde alguns segundos mais para **ProductsServer** tooload e hello de exibição a seguir da mensagem. Em seguida, pressione **atualização** no navegador de saudação.
   >
   >

   ![][37]
2. No navegador de hello, pressione **atualizar** em Olá **ProductsPortal** página. Cada vez que você atualize a página de saudação, você verá Olá server app exibirá uma mensagem quando `GetProducts()` de **ProductsServer** é chamado.

    ![][38]

## <a name="next-steps"></a>Próximas etapas

toolearn mais informações sobre a retransmissão do Azure, consulte Olá recursos a seguir:  

* [O que é Retransmissão do Azure?](relay-what-is-it.md)  
* [Como toouse de retransmissão](service-bus-dotnet-how-to-use-relay.md)  

[0]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hybrid.png
[1]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[NuGet]: http://nuget.org

[11]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-con-1.png
[13]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-13.png
[15]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-2.png
[16]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-4.png
[17]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-7.png
[18]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-5.png
[9]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-9.png
[10]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App3.png

[21]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App1.png
[24]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-12.png
[25]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-13.png
[26]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-14.png
[27]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-8.png

[36]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[37]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service1.png
[38]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service2.png
[41]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-40.png
[43]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-hybrid-43.png
