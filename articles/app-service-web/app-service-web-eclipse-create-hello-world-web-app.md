---
title: "aaaCreate um aplicativo de web do Azure básico usando o Eclipse | Microsoft Docs"
description: Este tutorial mostra como toouse hello Kit de ferramentas do Azure para Eclipse toocreate um aplicativo de Web Hello World para Azure.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: b2f42e0e7a5b98760ec02fab2fc38f9f07b1156b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a>Criar um aplicativo web básico do Azure usando o Eclipse
Este tutorial mostra como toocreate e implantar um tooAzure de aplicativo Hello World básica como um aplicativo Web usando Olá [Kit de ferramentas do Azure para Eclipse]. Mostramos um exemplo básico de JSP para manter a simplicidade, mas, para a implantação do Azure, etapas semelhantes podem ser usadas para um servlet Java.

Quando você concluiu este tutorial, o aplicativo ficará semelhante toohello ilustração a seguir quando você exibi-lo em um navegador da web:

![Visualização do aplicativo Hello World][01]

## <a name="prerequisites"></a>Pré-requisitos
* Um JDK (Java Developer Kit) versão 1.8 ou posterior.
* IDE do Eclipse para desenvolvedores de Java EE, Luna ou posterior. Isso pode ser baixado em <http://www.eclipse.org/downloads/>.
* Uma distribuição de um servidor Web ou de um servidor de aplicativo baseado em Java, como o [Apache Tomcat] ou o [Jetty].
* Uma assinatura do Azure, que pode ser adquirida em <https://azure.microsoft.com/free/> ou <http://azure.microsoft.com/pricing/purchase-options/>.
* Olá [Kit de ferramentas do Azure para Eclipse]. Para obter informações sobre como instalar Olá Kit de ferramentas do Azure, consulte [Olá instalando o Kit de ferramentas do Azure para Eclipse].

## <a name="toocreate-a-hello-world-application"></a>toocreate um aplicativo Hello World
Primeiro, vamos começar com a criação de um projeto Java.

1. Inicie o Eclipse e no menu de saudação clique **arquivo**, clique em **novo**e, em seguida, clique em **projeto Web dinâmico**. (Se você não vir **projeto Web dinâmico** listado como um projeto disponível depois de clicar em **arquivo** e **novo**, em seguida, Olá a seguir: clique em **arquivo**, clique em **novo**, clique em **projeto...** , expanda **Web**, clique em **projeto Web dinâmico**e clique em **próximo**.)
2. Para fins deste tutorial, nomeie o projeto de saudação **MyWebApp**. Sua tela será exibido a seguir toohello semelhante:
   
    ![Criando um novo projeto Web dinâmico][02]
3. Clique em **Concluir**.
4. No modo de exibição do Gerenciador de Projeto do Eclipse, expanda **MyWebApp**. Clique com o botão direito do mouse em **WebContent**, clique em **Novo** e, em seguida, clique em **Arquivo JSP**.
5. Em Olá **novo arquivo JSP** caixa de diálogo, o arquivo de saudação do nome **index.jsp**, mantenha a pasta pai Olá **MyWebApp/WebContent**e, em seguida, clique em **próximo**.
6. Em Olá **Selecionar modelo JSP** caixa de diálogo, para fins deste tutorial, selecione **novo arquivo JSP (html)**e, em seguida, clique em **concluir**.
7. Quando o arquivo index.jsp for aberto no Eclipse, adicione na exibição do texto toodynamically **Olá, mundo!** dentro de saudação existente `<body>` elemento. Seu atualizada `<body>` conteúdo deve ser semelhante a saudação de exemplo a seguir:
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. Salve o index.jsp.

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a>toodeploy tooan seu aplicativo recipiente de aplicativo da Web do Azure
Há várias maneiras pelas quais você pode implantar um tooAzure de aplicativo web Java. Este tutorial descreve uma saudação mais simples: o aplicativo será implantado tooan contêiner de aplicativo Web do Azure – nenhum tipo de projeto especial nem ferramentas adicionais são necessárias. Olá Olá JDK e o software da web que contêiner será fornecido para você pelo Azure, portanto não há nenhuma necessidade tooupload seu próprios; tudo o que você precisa é de seu aplicativo da Web de Java. Como resultado, o processo de publicação de saudação para seu aplicativo levará segundos, minutos não.

1. No Gerenciador de Projetos do Eclipse, clique com o botão direito do mouse em **MyWebApp**.
2. No menu de contexto hello, selecione **Azure**, em seguida, clique em **Publicar como um aplicativo Web do Azure...**
   
    ![Publicar como Aplicativo Web do Azure][03]
   
    Como alternativa, enquanto o projeto de aplicativo web está selecionado no Explorador de projeto do hello, você pode clicar em Olá **publicar** botão suspenso na barra de ferramentas hello e selecione **Publicar como um aplicativo Web do Azure** lá:
   
    ![Publicar como Aplicativo Web do Azure][14]
3. Se você tiver não tiver entrado no Azure do Eclipse, será solicitado toosign em sua conta do Azure:
   
    ![Caixa de diálogo Entrar no Azure][04]
   
    Se você tiver várias contas do Azure, alguns dos avisos Olá Olá entrar no processo pode ser exibido mais de uma vez, mesmo se eles parecem toobe Olá mesmo. Quando isso acontece, continue seguindo as instruções de logon hello.
4. Depois de ter entrado com êxito em sua conta do Azure, Olá **gerenciar assinaturas** caixa de diálogo exibirá uma lista de assinaturas que estão associados com suas credenciais. Se houver várias assinaturas listadas e você desejar toowork com apenas um subconjunto específico de-los, você pode, opcionalmente, desmarque Olá aquelas que você deseja toouse. Depois de selecionar suas assinaturas, clique em **Fechar**.
   
    ![Caixa de diálogo Gerenciar Assinaturas][05]
5. Olá quando **implantar tooAzure contêiner de aplicativo da Web** caixa de diálogo for exibida, ele exibirá qualquer contêiner de aplicativo Web que você criou anteriormente; se você não criou qualquer contêiner, a lista de saudação estará vazia.
   
    ![Caixa de diálogo do contêiner do aplicativo da Web tooAzure implantar][06]
6. Se você não criou um contêiner de aplicativo Web do Azure antes, ou se você gostaria que toopublish seu aplicativo tooa novo contêiner, use Olá etapas a seguir. Caso contrário, selecione um contêiner do aplicativo Web existente e ignorar toostep 7 abaixo.
   
   1. Clique em **Novo...**
      
       ![Caixa de diálogo do contêiner do aplicativo da Web tooAzure implantar][15]
   2. Olá **novo contêiner de aplicativo Web** caixa de diálogo será exibida:
      
       ![Caixa de diálogo Novo contêiner do aplicativo Web][07a]
   3. Insira um **rótulo DNS** para seu contêiner de aplicativo da Web; isso formarão o rótulo DNS Olá folha da URL de host Olá para o aplicativo web no Azure. (Observe que Olá deve estar disponível e está de acordo com requisitos de nomenclatura de aplicativo Web tooAzure).
   4. Em Olá **contêiner da Web** menu suspenso, selecione Olá o software apropriado para seu aplicativo.
      
       No momento, você pode escolher entre o Tomcat 8, Tomcat 7 ou Jetty 9. Uma distribuição recente do software de saudação selecionada será fornecida pelo Azure e ele será executado em uma distribuição recente do JDK 8 criado pela Oracle e fornecido pelo Azure.
   5. Em Olá **assinatura** menu suspenso, assinatura selecione Olá deseja toouse para essa implantação.
   6. Em Olá **grupo de recursos** menu suspenso, selecione Olá grupo de recursos com o qual você deseja tooassociate seu aplicativo Web. (Grupos de recursos do azure permite que você toogroup recursos relacionados juntos para que, por exemplo, pode ser excluídos em conjunto.)
      
       Você pode selecionar um grupo de recursos existente (se houver) e ignorar toostep g abaixo, ou use Olá seguindo estas etapas toocreate um novo grupo de recursos:
      
      * Clique em **Novo...**
      * Olá **novo grupo de recursos** caixa de diálogo será exibida:
        
          ![Caixa de diálogo Novo Grupo de Recursos][08]
      * Em Olá Olá **nome** caixa de texto, especifique um nome para seu novo grupo de recursos.
      * Em Olá Olá **região** menu suspenso, selecione Olá apropriado do Azure Datacenter local para seu grupo de recursos.
      * OPCIONAL: Por padrão, uma distribuição recente de Java 8 será implantada pelo Azure automaticamente tooyour contêiner de aplicativo da web como sua JVM. No entanto, você pode especificar uma versão diferente e a distribuição de saudação JVM se for necessário para seu aplicativo Web. Olá toospecify JDK para seu aplicativo Web, clique em Olá **JDK** guia e selecione uma saudação as opções a seguir:
        
        * **Implantar o padrão de saudação JDK oferecida pelo serviço de aplicativos Web do Azure**: essa opção implantará uma distribuição recente de Java 8.
        * **Implantar um JDK disponível no Azure de terceiros 3º**: essa opção permite que você toochoose de lista de saudação de JDKs que são fornecidos pelo Microsoft Azure.
        * **Implantar meu próprio JDK a partir deste local de download**: essa opção permite que você toospecify sua distribuição JDK, que deve ser empacotada como um arquivo ZIP e carregado tooeither um local de download disponível publicamente ou um armazenamento do Azure da conta para a qual você tem acesso.
          
          ![Caixa de diálogo Novo contêiner do aplicativo Web][07b]
   7. Clique em **OK**.
   8. Olá **plano do serviço de aplicativo** menu suspenso lista planos de serviço de aplicativo hello que estão associados a saudação grupo de recursos que você selecionou. (Os planos de serviço de aplicativo especificam informações como a localização de saudação do seu aplicativo Web, Olá tipo de preço e tamanho de instância de computação hello. Um único Plano do Serviço de Aplicativo pode ser usado para vários Aplicativos Web, por isso, ele é mantido separadamente de uma implantação de Aplicativo Web específica.)
      
       Você pode selecionar um plano de serviço de aplicativo existente (se houver) e ignorar toostep h abaixo, ou usar Olá toocreate essas etapas que um novo plano de serviço de aplicativo a seguir:
      
      * Clique em **Novo...**
      * Olá **novo plano de serviço de aplicativo** caixa de diálogo será exibida:
        
          ![Caixa de diálogo Novo Plano do Serviço de Aplicativo][09]
      * Em Olá Olá **nome** caixa de texto, especifique um nome para o novo plano de serviço de aplicativo.
      * Em Olá Olá **local** menu suspenso, selecione Olá apropriado do Azure Datacenter local para o plano de saudação.
      * Em Olá Olá **preço** menu suspenso, selecione Olá apropriado de preços para o plano de saudação. Para fins de teste, é possível escolher **Gratuito**.
      * Em Olá Olá **tamanho da instância** menu suspenso, o tamanho de instância apropriada do hello selecione plano hello. Para fins de teste, é possível escolher **Pequeno**.
   9. Depois de concluir todos Olá acima etapas, caixa de diálogo novo contêiner de aplicativo Web hello deve se assemelhar Olá ilustração a seguir:
      
       ![Caixa de diálogo Novo contêiner do aplicativo Web][10]
   10. Clique em **Okey** toocomplete criação de saudação do seu novo contêiner de aplicativo Web.
       
        Aguarde alguns segundos para lista de saudação do hello toobe de contêineres de aplicativo Web atualizada e o contêiner de aplicativo web recém-criado agora deve ser selecionado na lista de saudação.
7. Agora você está pronto toocomplete implantação inicial do hello de tooAzure seu aplicativo Web:
   
    ![Caixa de diálogo do contêiner do aplicativo da Web tooAzure implantar][11]
   
    Clique em **Okey** toodeploy sua toohello de aplicativo Java selecionado contêiner do aplicativo Web.
   
    Por padrão, o aplicativo será implantado como um subdiretório saudação do servidor de aplicativos. Se quiser toobe implantado como um aplicativo raiz de hello, verifique Olá **implantar tooroot** caixa de seleção antes de clicar em **Okey**.
8. Em seguida, você deve ver Olá **o Log de atividades do Azure** exibição, que indica o status de implantação de saudação do seu aplicativo Web.
   
    ![Log de Atividades do Azure][12]
   
    processo de saudação de implantar seu aplicativo Web tooAzure deve levar somente alguns segundos toocomplete. Quando pronto seu aplicativo, você verá um link chamado **publicado** em Olá **Status** coluna. Quando você clica em um link de hello, levará home page do aplicativo da Web tooyour implantado.

## <a name="updating-your-web-app"></a>Atualizando seu aplicativo Web
A atualização de um aplicativo Web do Azure em execução é um processo rápido e fácil, e você tem duas opções de atualização:

* Você pode atualizar a implantação de saudação do aplicativo Web Java existente.
* Você pode publicar um toohello de aplicativo Java adicional mesmo contêiner de aplicativo da Web.

Em ambos os casos, o processo de saudação é idêntico e leva apenas alguns segundos:

1. No Explorador de projeto do Eclipse Olá, clique no aplicativo de Java hello deseja tooupdate ou adicionar tooan existente do contêiner do aplicativo da Web.
2. Quando o menu de contexto Olá for exibida, selecione **Azure** e, em seguida, **Publicar como um aplicativo Web do Azure...**
3. Como você já fez logon anteriormente, verá uma lista com seus contêineres de aplicativo Web existentes. Selecione Olá um deseja toopublish ou publicar novamente o Java aplicativo tooand, clique **Okey**.

Alguns segundos mais tarde, Olá **o Log de atividades do Azure** exibição mostrará sua implantação atualizada como **publicado** e você será capaz de tooverify seu aplicativo atualizado em um navegador da web.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Iniciar, parar ou reiniciar o aplicativo Web existente
toostart ou interromper um contêiner existente do aplicativo Web do Azure, (incluindo todos os aplicativos do Java Olá implantado nele), você pode usar o hello **Azure Explorer** exibição.

Se hello **Azure Explorer** exibição não ainda estiver aberta, você pode abri-lo clicando em, em seguida, **janela** menu do Eclipse, clique **exibição**, em seguida, **outros...** , em seguida, **Azure**e, em seguida, clique em **Azure Explorer**. Se você não tiver conectado anteriormente, ele solicitará que você toodo assim.

Olá quando **Azure Explorer** modo de exibição, use siga essas etapas toostart ou interrompa o aplicativo Web: 

1. Expanda Olá **Azure** nó.
2. Expanda Olá **aplicativos Web** nó. 
3. Olá com o botão direito desejada do aplicativo Web.
4. Quando o menu de contexto Olá for exibida, clique em **iniciar**, **parar**, ou **reiniciar**. Observe que as opções de menu Olá têm reconhecimento de contexto, para que você só pode parar um aplicativo web em execução ou iniciar um aplicativo da web que não está em execução no momento.
   
    ![Interromper um aplicativo Web existente][13]

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre Olá kits de ferramentas do Azure para Java IDEs, consulte Olá links a seguir:

* [Kit de ferramentas do Azure para Eclipse]
  * [Olá instalando o Kit de ferramentas do Azure para Eclipse]
  * *Criar uma aplicativo Web Hello World para o Azure no Eclipse (este artigo)*
  * [Novidades no Kit de ferramentas do Azure para Eclipse de saudação]
* [Kit de Ferramentas do Azure para IntelliJ]
  * [Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]
  * [Criar um aplicativo Web Hello World para o Azure no IntelliJ]
  * [Novidades no Kit de ferramentas do Azure para IntelliJ de saudação]

Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure].

Para obter informações adicionais sobre a criação de aplicativos Web do Azure, consulte Olá [visão geral de aplicativos Web].

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Kit de ferramentas do Azure para Eclipse]: ../azure-toolkit-for-eclipse.md
[Kit de Ferramentas do Azure para IntelliJ]: ../azure-toolkit-for-intellij.md
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Criar um aplicativo Web Hello World para o Azure no IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Olá instalando o Kit de ferramentas do Azure para Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Novidades no Kit de ferramentas do Azure para Eclipse de saudação]: ../azure-toolkit-for-eclipse-whats-new.md
[Novidades no Kit de ferramentas do Azure para IntelliJ de saudação]: ../azure-toolkit-for-intellij-whats-new.md

[Centro de desenvolvedores de Java do Azure]: https://azure.microsoft.com/develop/java/
[visão geral de aplicativos Web]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/app-service-web-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/app-service-web-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/app-service-web-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/app-service-web-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/app-service-web-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/app-service-web-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: ./media/app-service-web-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/app-service-web-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/app-service-web-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/app-service-web-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/app-service-web-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/app-service-web-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/app-service-web-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/app-service-web-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
