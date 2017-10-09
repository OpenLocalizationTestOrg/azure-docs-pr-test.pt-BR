---
title: "aplicativo de várias camadas aaa.NET usando o barramento de serviço do Azure | Microsoft Docs"
description: "Um tutorial do .NET que ajuda você a desenvolver um aplicativo de várias camado no Azure que usa toocommunicate de filas do barramento de serviço entre camadas."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1b8608ca-aa5a-4700-b400-54d65b02615c
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: sethm
ms.openlocfilehash: 485910ff1d3b8b0a709ee14ede32e57cf873829a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a>Aplicativo multicamadas .NET usando filas do Barramento de Serviço do Azure
## <a name="introduction"></a>Introdução
Desenvolvendo para o Microsoft Azure é fácil de usar o Visual Studio e Olá gratuito do Azure SDK para .NET. Este tutorial orienta Olá etapas toocreate um aplicativo que usa vários recursos do Azure em execução no seu ambiente local.

Você aprenderá a seguir hello:

* Como tooenable o computador para o desenvolvimento do Azure com um único baixar e instalar.
* Como toouse toodevelop de Visual Studio para o Azure.
* Como toocreate um aplicativo de várias camado no Azure usando funções web e de trabalho.
* Como toocommunicate entre camadas usando filas do barramento de serviço.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

Neste tutorial você compilar e executar o aplicativo de várias camadas hello em um serviço de nuvem do Azure. Olá front-end é uma função web do ASP.NET MVC e back-end Olá é uma função de trabalho que usa uma fila do barramento de serviço. Você pode criar hello mesmo aplicativo de várias camado com o front-end hello como um projeto da web, que é implantado tooan site do Azure, em vez de um serviço de nuvem. Você também pode testar Olá [aplicativo do .NET no local/em nuvem híbrida](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.

Olá, captura de tela a seguir mostra aplicativo hello concluída.

![][0]

## <a name="scenario-overview-inter-role-communication"></a>Visão geral de cenário: comunicação interfunções
toosubmit um pedido para processamento, o componente da UI front-end que hello, em execução na função de web hello, deve interagir com a lógica de camada intermediária Olá em execução na função de trabalho de saudação. Este exemplo usa o barramento de serviço do sistema de mensagens para comunicação de saudação entre camadas de saudação.

Usando o barramento de serviço de mensagens entre camadas intermediários e Olá web separam os dois componentes. Em contraste toodirect mensagens (ou seja, TCP ou HTTP), Olá camada da web não se conecta camada intermediária toohello diretamente. em vez disso, ele envia unidades de trabalho, como mensagens, para o barramento de serviço, que retém até que seja de camada intermediária Olá tooconsume pronto e processá-los de maneira confiável.

Barramento de serviço fornece dois toosupport orientada de entidades de mensagens: filas e tópicos. Com as filas, cada mensagem enviada toohello fila é consumida por um único destinatário. O padrão de publicação/assinatura de saudação em que cada mensagem publicada é feita tooa disponível assinatura registrada com o tópico de saudação os tópicos oferecem suporte. Cada assinatura mantém logicamente sua própria fila de mensagens. As assinaturas também podem ser configuradas com as regras de filtro que restringem Olá conjunto de mensagens passado para Olá toothose de fila de assinatura que correspondem ao filtro de saudação. Olá, exemplo a seguir usa filas do barramento de serviço.

![][1]

Esse mecanismo de comunicação oferece diversas vantagens sobre mensagens diretas:

* **Desacoplamento temporal.** Com o padrão de mensagens assíncronas hello, produtores e consumidores não precisam ser online em Olá simultaneamente. Barramento de serviço confiável armazena as mensagens até a parte consumidora hello está pronta para recebê-los. Isso permite que os componentes de saudação do hello distribuída application toobe desconectados ou voluntariamente, por exemplo, para manutenção, ou devido a falha do componente tooa, sem afetar o sistema como um todo. Além disso, Olá consumindo o aplicativo pode precisar apenas de toocome online durante determinadas horas do dia de saudação.
* **Nivelamento de carga.** Em muitos aplicativos, a carga do sistema varia ao longo do tempo, enquanto o tempo de processamento de saudação necessário para cada unidade de trabalho é normalmente constante. A intermediação dos produtores e consumidores com uma fila significa que Olá consumindo aplicativo (trabalho Olá) somente necessidades toobe provisionado carga média tooaccommodate em vez de picos de carga. profundidade de saudação da fila de saudação aumenta e diminui conforme a carga de entrada hello varia. Isso economiza o dinheiro em relação à quantidade de saudação infraestrutura necessária tooservice Olá de carregamento de aplicativo diretamente.
* **Balanceamento de carga.** Conforme a carga aumenta, mais processos de trabalho podem ser adicionados tooread da fila de saudação. Cada mensagem é processada por apenas um dos processos de trabalho hello. Além disso, esse balanceamento de carga baseado em pull permite o uso ideal de máquinas de trabalho Olá mesmo se as máquinas de trabalho diferem em termos de capacidade de processamento, como eles efetuarão pull das mensagens em sua própria velocidade máxima. Esse padrão é geralmente denominado hello *consumidor concorrente* padrão.
  
  ![][2]

Olá seções a seguir discutem código Olá que implementa essa arquitetura.

## <a name="set-up-hello-development-environment"></a>Configurar o ambiente de desenvolvimento Olá
Antes de começar a desenvolver aplicativos do Azure, obter ferramentas hello e configurar seu ambiente de desenvolvimento.

1. Instalar hello Azure SDK para .NET de saudação SDK [página de downloads](https://azure.microsoft.com/downloads/).
2. Em Olá **.NET** coluna, clique na versão de saudação do [Visual Studio](http://www.visualstudio.com) você está usando. Olá as etapas deste tutorial usam Visual Studio 2015, mas elas também funcionam com o Visual Studio de 2017.
3. Quando solicitado toorun ou salvar instalador hello, clique em **executar**.
4. Em Olá **Web Platform Installer**, clique em **instalar** e prosseguir com a instalação de saudação.
5. Após a conclusão da instalação hello, você terá tudo necessário toostart toodevelop Olá aplicativo. Olá SDK inclui ferramentas que permitem a fácil desenvolver aplicativos do Azure no Visual Studio.

## <a name="create-a-namespace"></a>Criar um namespace
Olá próxima etapa é toocreate um namespace de serviço e obter uma chave de assinatura de acesso compartilhado (SAS). Um namespace fornece um limite de aplicativo para cada aplicativo exposto por meio do Barramento de Serviço. Uma chave SAS é gerada pelo sistema hello quando um namespace é criado. combinação de saudação do namespace e a chave SAS fornece credenciais de saudação para aplicativo do barramento de serviço tooauthenticate access tooan.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a>Criar uma função Web
Nesta seção, você deve criar front-end do seu aplicativo hello. Primeiro, crie páginas de saudação que exibe seu aplicativo.
Depois disso, adicione o código que envia a fila do barramento de serviço de tooa de itens e exibe informações de status sobre a fila de saudação.

### <a name="create-hello-project"></a>Criar projeto Olá
1. Usando privilégios de administrador, inicie o Visual Studio: Olá atalho **Visual Studio** ícone do programa e, em seguida, clique em **executar como administrador**. emulador de computação do Azure Hello, discutido posteriormente neste artigo, exige que o Visual Studio seja iniciado com privilégios de administrador.
   
   No Visual Studio, no hello **arquivo** menu, clique em **novo**e, em seguida, clique em **projeto**.
2. Em **Modelos Instalados**, em **Visual C#**, clique em **Nuvem** e em **Serviço de Nuvem do Azure**. Projeto de saudação do nome **MultiTierApp**. Em seguida, clique em **OK**.
   
   ![][9]
3. Em funções do **.NET Framework 4.5**, clique duas vezes em **Função Web do ASP.NET**.
   
   ![][10]
4. Passe o mouse sobre **WebRole1** em **solução de serviço de nuvem do Azure**, clique o ícone de lápis hello e renomeie a função da web de saudação muito**FrontendWebRole**. Em seguida, clique em **OK**. (Certifique-se de inserir "Frontend" com "e" minúsculo, não "FrontEnd".)
   
   ![][11]
5. De saudação **novo projeto ASP.NET** caixa de diálogo Olá **selecionar um modelo de** lista, clique em **MVC**.
   
   ![][12]
6. Ainda no hello **novo projeto ASP.NET** caixa de diálogo, clique em Olá **alterar autenticação** botão. Em Olá **alterar autenticação** caixa de diálogo, clique em **sem autenticação**e, em seguida, clique em **Okey**. Para este tutorial, você está implantando um aplicativo que não precisa de um logon de usuário.
   
    ![][16]
7. Em Olá **novo projeto ASP.NET** caixa de diálogo, clique em **Okey** toocreate projeto de saudação.
8. No **Gerenciador de soluções**, em hello **FrontendWebRole** do projeto, clique no **referências**, em seguida, clique em **gerenciar pacotes NuGet**.
9. Clique em Olá **procurar** guia e, em seguida, procurar `Microsoft Azure Service Bus`. Selecione Olá **windowsazure. ServiceBus** do pacote, clique em **instalar**e aceite os termos de uso do hello.
   
   ![][13]
   
   Observe que Olá necessário assemblies de cliente agora são referenciados e adicionou alguns novos arquivos de código.
10. Em **Gerenciador de Soluções**, clique com o botão direito do mouse em **Modelos**, **Adicionar** e **Classe**. Em Olá **nome** caixa, digite o nome de saudação **Onlineorder**. Clique em **Adicionar**.

### <a name="write-hello-code-for-your-web-role"></a>Escrever código Olá para sua função web
Nesta seção, você criará Olá várias páginas que seu aplicativo é exibido.

1. No arquivo de Onlineorder Olá no Visual Studio, substitua a definição de namespace existentes Olá código a seguir:
   
   ```csharp
   namespace FrontendWebRole.Models
   {
       public class OnlineOrder
       {
           public string Customer { get; set; }
           public string Product { get; set; }
       }
   }
   ```
2. No **Gerenciador de Soluções**, clique duas vezes em **Controllers\HomeController.cs**. Adicione o seguinte Olá **usando** instruções na parte superior de saudação do hello tooinclude Olá namespaces para o modelo que você acabou de criar, bem como o barramento de serviço de arquivo.
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. Também no arquivo de HomeController Olá no Visual Studio, substitua a definição de namespace existentes Olá código a seguir. Este código contém métodos para manipular o envio de saudação da fila de toohello de itens.
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect tooSubmit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for hello submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from hello submission
           // form.
           [HttpPost]
           // Attribute toohelp prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting tooqueue here.
   
                   return RedirectToAction("Submit");
               }
               else
               {
                   return View(order);
               }
           }
       }
   }
   ```
4. De saudação **criar** menu, clique em **compilar solução** tootest precisão de saudação do seu trabalho até o momento.
5. Agora, crie exibição Olá Olá `Submit()` método que você criou anteriormente. Clique com botão direito em Olá `Submit()` método (sobrecarga de saudação do `Submit()` que não usa nenhum parâmetro) e, em seguida, escolha **adicionar exibição**.
   
   ![][14]
6. Uma caixa de diálogo é exibida para a criação de exibição de saudação. Em Olá **modelo** , escolha **criar**. Em Olá **classe modelo** lista, clique em Olá **OnlineOrder** classe.
   
   ![][15]
7. Clique em **Adicionar**.
8. Agora, altere o nome de saudação exibida do seu aplicativo. Em **Gerenciador de soluções**, clique duas vezes o **exibições \ compartilhadas\\cshtml** arquivo tooopen-lo no editor do Visual Studio hello.
9. Substitua todas as ocorrências de **Meu Aplicativo ASP.NET** para **Produtos da LITWARE**.
10. Remover Olá **início**, **sobre**, e **contato** links. Exclua o código de saudação realçado:
    
    ![][28]
11. Finalmente, modifique algumas informações sobre a fila de Olá Olá tooinclude de página de envio. Em **Solution Explorer**, clique duas vezes o **Views\Home\Submit.cshtml** arquivo tooopen-lo no editor do Visual Studio hello. Olá seguinte linha depois de adicionar `<h2>Submit</h2>`. Por enquanto, Olá `ViewBag.MessageCount` está vazio. Você irá preenchê-lo mais tarde.
    
    ```html
    <p>Current number of orders in queue waiting toobe processed: @ViewBag.MessageCount</p>
    ```
12. Você agora implementou a interface do usuário. Você pode pressionar **F5** toorun seu aplicativo e confirme que parece conforme o esperado.
    
    ![][17]

### <a name="write-hello-code-for-submitting-items-tooa-service-bus-queue"></a>Escrever código hello para enviar a fila de barramento de serviço tooa itens
Agora, adicione código para enviar itens tooa fila. Primeiro, você cria uma classe que contém as informações de conexão de fila do Barramento de Serviço. Em seguida, você inicializa a conexão do Global.aspx.cs. Por fim, atualize o código de envio de saudação que você criou anteriormente na fila do barramento de serviço do HomeController tooactually enviar itens tooa.

1. Em **Solution Explorer**, clique com botão direito **FrontendWebRole** (projeto de saudação do botão direito do mouse, não a função de saudação). Clique em **Adicionar** e depois em **Classe**.
2. Nome de classe Olá **QueueConnector.cs**. Clique em **adicionar** toocreate classe de saudação.
3. Agora, adicione o código que encapsula as informações de conexão hello e inicializa a fila de barramento de serviço do hello conexão tooa. Substitua todo o conteúdo de QueueConnector.cs Olá Olá código a seguir e insira valores para `your Service Bus namespace` (seu nome de namespace) e `yourKey`, que é hello **chave primária** obtido anteriormente saudação do Azure Portal.
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Web;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   
   namespace FrontendWebRole
   {
       public static class QueueConnector
       {
           // Thread-safe. Recommended that you cache rather than recreating it
           // on every request.
           public static QueueClient OrdersQueueClient;
   
           // Obtain these values from hello portal.
           public const string Namespace = "your Service Bus namespace";
   
           // hello name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create hello namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http toobe friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create hello namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create hello queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client toohello queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. Agora, garanta que o método **Initialize** seja chamado. No **Gerenciador de Soluções**, clique duas vezes em **Global.asax\Global.asax.cs**.
5. Adicionar Olá a seguinte linha de código final Olá Olá **Application_Start** método.
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. Por fim, atualize o código de web de saudação criado anteriormente, para enviar itens toohello fila. No **Gerenciador de Soluções**, clique duas vezes em **Controllers\HomeController.cs**.
7. Saudação de atualização `Submit()` método (sobrecarga de saudação sem parâmetros) da seguinte maneira mensagem de saudação tooget contagem para fila de saudação.
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you tooperform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get hello queue, and obtain hello message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. Saudação de atualização `Submit(OnlineOrder order)` método (sobrecarga de saudação que usa um parâmetro) da seguinte maneira toosubmit ordem de fila de toohello de informações.
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from hello order.
           var message = new BrokeredMessage(order);
   
           // Submit hello order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. Agora você pode executar o aplicativo hello novamente. Cada vez que você enviar um pedido, aumenta a contagem de mensagens de saudação.
   
   ![][18]

## <a name="create-hello-worker-role"></a>Criar função de trabalho Olá
Agora você irá criar função de trabalho Olá que processa o envio de pedidos de saudação. Este exemplo usa Olá **função de trabalho com fila do barramento de serviço** modelo de projeto do Visual Studio. Você já obtido credenciais Olá necessário do portal de saudação.

1. Verifique se que você conectou tooyour do Visual Studio conta do Azure.
2. No Visual Studio, no **Solution Explorer** com o botão direito do **funções** pasta sob Olá **MultiTierApp** projeto.
3. Clique em **Adicionar** e clique em **Novo Projeto da Função de Trabalho**. Olá **adicionar novo projeto de função** caixa de diálogo é exibida.
   
   ![][26]
4. Em Olá **adicionar novo projeto de função** caixa de diálogo, clique em **função de trabalho com fila do barramento de serviço**.
   
   ![][23]
5. Em Olá **nome** caixa, projeto de saudação do nome **OrderProcessingRole**. Clique em **Adicionar**.
6. Copie a cadeia de caracteres de conexão de saudação que você obteve na etapa 9 da área de transferência do hello "Criar um namespace de barramento de serviço" seção toohello.
7. Em **Solution Explorer**, Olá do botão direito do mouse **OrderProcessingRole** criado na etapa 5 (certifique-se de que você clique **OrderProcessingRole** em **Funções**, e não Olá classe). Clique em **Propriedades**.
8. Em Olá **configurações** guia da saudação **propriedades** caixa de diálogo, clique em Olá **valor** caixa **Microsoft.ServiceBus.ConnectionString**e, em seguida, cole o valor de ponto de extremidade de saudação você copiou na etapa 6.
   
   ![][25]
9. Criar um **OnlineOrder** toorepresent Olá pedidos de classe como processá-los da fila de saudação. Você pode reutilizar uma classe já criada. No **Solution Explorer**, Olá atalho **OrderProcessingRole** classe (ícone de classe com o botão direito hello, não a função de saudação). Clique em **Adicionar** e clique em **Item Existente**.
10. Procure a subpasta toohello para **FrontendWebRole\Models**e, em seguida, clique duas vezes em **Onlineorder** tooadd-toothis projeto.
11. Em **WorkerRole.cs**, alterar o valor Olá Olá **QueueName** variável do `"ProcessingQueue"` muito`"OrdersQueue"` conforme Olá código a seguir.
    
    ```csharp
    // hello name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. Adicione o seguinte Olá usando a instrução na parte superior de saudação do arquivo WorkerRole.cs de saudação.
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. Em Olá `Run()` função dentro de saudação `OnMessage()` chamar, substitua o conteúdo de saudação do hello `try` cláusula com hello código a seguir.
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View hello message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. Você concluiu o aplicativo hello. Você pode testar o aplicativo completo hello clicando com o projeto de MultiTierApp Olá no Gerenciador de soluções, selecionando **definir como projeto de inicialização**e, em seguida, pressionando F5. Observe que a contagem de mensagens não aumenta, porque a função de trabalho Olá processa os itens da fila de saudação e as marca como concluída. Você pode ver a saída do rastreamento Olá sua função de trabalho exibindo Olá interface do usuário de emulador de computação do Azure. Você pode fazer isso clicando duas vezes o ícone do emulador Olá na área de notificação de saudação da barra de tarefas e selecionando **Mostrar UI do emulador de computação**.
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre o barramento de serviço, consulte Olá recursos a seguir:  

* [Documentação do Barramento de Serviço do Azure][sbdocs]  
* [Página de serviço do Barramento de Serviço][sbacom]  
* [Como tooUse filas do barramento de serviço][sbacomqhowto]  

toolearn mais informações sobre cenários de várias camados, consulte:  

* [Aplicativo de várias camadas .NET usando tabelas de armazenamento, filas e blobs][mutitierstorage]  

[0]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbdocs]: /azure/service-bus-messaging/  
[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36
