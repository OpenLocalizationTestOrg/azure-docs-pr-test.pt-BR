---
title: "aaaCreate um aplicativo web do Azure básico em IntelliJ | Microsoft Docs"
description: Este tutorial mostra como toouse hello Kit de ferramentas do Azure para IntelliJ toocreate um aplicativo de Web Hello World para Azure.
services: app-service\web
documentationcenter: java
author: selvasingh
manager: erikre
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4667497213cac3ddf754d164e614c809f338cce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a>Criar um aplicativo Web do Azure básico no IntelliJ
Este tutorial mostra como toocreate e implantar um tooAzure de aplicativo Hello World básica como um aplicativo Web usando Olá [Kit de ferramentas do Azure para IntelliJ]. Mostramos um exemplo básico de JSP para manter a simplicidade, mas, para a implantação do Azure, etapas semelhantes podem ser usadas para um servlet Java.

Quando você concluiu este tutorial, o aplicativo ficará semelhante toohello ilustração a seguir quando você exibi-lo em um navegador da web:

![Página da Web de exemplo][01]

## <a name="prerequisites"></a>Pré-requisitos
* Um JDK (Java Developer Kit) versão 1.8 ou posterior.
* IntelliJ IDEA Ultimate Edition. Isso pode ser baixado de <https://www.jetbrains.com/idea/download/>.
* Uma distribuição de um servidor Web ou de um servidor de aplicativo baseado em Java, como o [Apache Tomcat] ou o [Jetty].
* Uma assinatura do Azure, que pode ser adquirida em <https://azure.microsoft.com/free/> ou <http://azure.microsoft.com/pricing/purchase-options/>.
* Olá [Kit de ferramentas do Azure para IntelliJ]. Para obter informações sobre como instalar Olá Kit de ferramentas do Azure, consulte [Olá instalando o Kit de ferramentas do Azure para IntelliJ].

## <a name="toocreate-a-hello-world-application"></a>toocreate um aplicativo Hello World
Primeiro, vamos começar com a criação de um projeto Java.

1. Iniciar IntelliJ e clique em Olá **arquivo** menu, clique em **novo**e, em seguida, clique em **projeto**.
   
    ![Arquivo Novo Projeto][02]
2. Na caixa de diálogo Novo projeto hello, selecione **Java**, em seguida, **aplicativo Web**e, em seguida, clique em **novo** tooadd um SDK de projeto.
   
    ![Caixa de diálogo Novo Projeto][03a]
   
3. Em hello Selecionar diretório base para a caixa de diálogo do JDK, selecione Olá pasta onde o seu JDK está instalado e clique **Okey**. Clique em **próximo** em Olá toocontinue de caixa de diálogo de novo projeto.
   
    ![Especificar o diretório base do JDK][03b]
4. Para fins deste tutorial, nomeie o projeto de saudação **Java aplicativo Web no Azure**e, em seguida, clique em **concluir**.
   
    ![Caixa de diálogo Novo Projeto][04]
5. Na exibição do Explorador de Projetos do IntelliJ, expanda **Java-Web-App-On-Azure**, expanda **Web** e clique duas vezes em **index.jsp**.
   
    ![Abrir Índice de Página][05c]
6. Quando o arquivo index.jsp for aberto no IntelliJ, adicionar na exibição do texto toodynamically **Olá, mundo!** dentro de saudação existente `<body>` elemento. Seu atualizada `<body>` conteúdo deve ser semelhante a saudação de exemplo a seguir:
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. Salve o index.jsp.

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a>toodeploy tooan seu aplicativo recipiente de aplicativo da Web do Azure
Há várias maneiras pelas quais você pode implantar um tooAzure de aplicativo web Java. Este tutorial descreve uma saudação mais simples: o aplicativo será implantado tooan contêiner de aplicativo Web do Azure – nenhum tipo de projeto especial nem ferramentas adicionais são necessárias. Olá Olá JDK e o software da web que contêiner será fornecido para você pelo Azure, portanto não há nenhuma necessidade tooupload seu próprios; tudo o que você precisa é de seu aplicativo da Web de Java. Como resultado, o processo de publicação de saudação para seu aplicativo levará segundos, minutos não.

Antes de publicar seu aplicativo, é necessário primeiro tooconfigure suas configurações de módulo. Assim, o toodo use Olá etapas a seguir:

1. No Explorador de projeto do IntelliJ, clique com botão direito Olá **Java aplicativo Web no Azure** projeto. Quando o menu de contexto Olá for exibida, clique em **abrir configurações de módulo**.

    ![Abrir configurações do módulo][05a]
2. Quando for exibida a caixa de diálogo Olá estrutura do projeto:

   a. Clique em **artefatos** na lista de saudação do **configurações de projeto**.
   b. Alterar nome do artefato Olá no hello **nome** caixa para que ele não contém espaço em branco ou caracteres especiais; isso é necessário pois Olá nome será usado em Olá identificador de recurso uniforme (URI).
   c. Saudação de alteração **tipo** muito**aplicativo Web: arquivo**.
   d. Clique em **Okey** caixa de diálogo tooclose Olá estrutura do projeto.

    ![Abrir configurações do módulo][05b]

Quando você tiver configurado as definições de módulo, você pode publicar seu aplicativo tooAzure usando Olá etapas a seguir:

1. No Explorador de projeto do IntelliJ, clique com botão direito Olá **Java aplicativo Web no Azure** projeto. Quando o menu de contexto Olá for exibida, selecione **Azure**e, em seguida, clique em **Publicar como um aplicativo Web do Azure...**
   
    ![Menu de Contexto de Publicação do Azure][06]
2. Se você tiver não tiver entrado no Azure de IntelliJ, será solicitada toosign em sua conta do Azure. (Se você tiver várias contas do Azure, alguns dos prompts de saudação durante o processo de entrada hello podem ser mostradas mais de uma vez, mesmo se eles parecem toobe Olá mesmo. Quando isso acontece, continuar toofollow Olá sinal instruções).
   
    ![Caixa de diálogo Login do Azure][07]
3. Depois de ter entrado com êxito em sua conta do Azure, Olá **gerenciar assinaturas** caixa de diálogo exibirá uma lista de assinaturas que estão associados com suas credenciais. (Se houver várias assinaturas listadas e você desejar toowork com apenas um subconjunto específico de-los, opcionalmente pode desmarcar Olá assinaturas que não toouse.) Depois de selecionar suas assinaturas, clique em **Fechar**.
   
    ![Gerenciar Assinaturas][08]
4. Olá quando **implantar tooAzure contêiner de aplicativo da Web** caixa de diálogo for exibida, ele exibirá qualquer contêiner de aplicativo Web que você criou anteriormente; se você não criou qualquer contêiner, a lista de saudação estará vazia.
   
    ![Contêineres de Aplicativo][09]
5. Se você não criou um contêiner de aplicativo Web do Azure antes, ou se você gostaria que toopublish seu aplicativo tooa novo contêiner, use Olá etapas a seguir. Caso contrário, selecione um contêiner do aplicativo Web existente e ignorar toostep 6 abaixo.
   
   1. Clique em **+**
      
       ![Adicionar Contêiner de Aplicativo][10]
   2. Olá **novo contêiner de aplicativo Web** caixa de diálogo será exibida, que será usado para Olá lado várias etapas.
      
       ![Novo Contêiner de Aplicativo][11a]
   3. Insira um **rótulo DNS** para seu contêiner de aplicativo da Web; isso formarão o rótulo DNS Olá folha da URL de host Olá para o aplicativo web no Azure. Observe que esse nome hello deve estar disponível e está de acordo com requisitos de nomenclatura de aplicativo Web tooAzure.
   4. Em Olá **contêiner da Web** menu suspenso, selecione Olá o software apropriado para seu aplicativo.
      
       No momento, você pode escolher entre o Tomcat 8, Tomcat 7 ou Jetty 9. Uma distribuição recente do software de saudação selecionada será fornecida pelo Azure e ele será executado em uma distribuição recente do JDK 8 criado pela Oracle e fornecido pelo Azure.
   5. Em Olá **assinatura** menu suspenso, assinatura selecione Olá deseja toouse para essa implantação.
   6. Em Olá **grupo de recursos** menu suspenso, selecione Olá grupo de recursos com o qual você deseja tooassociate seu aplicativo Web. (Grupos de recursos do azure permite que você toogroup recursos relacionados juntos para que, por exemplo, pode ser excluídos em conjunto.)
      
       Você pode selecionar um grupo de recursos existente (se houver) e ignorar toostep g abaixo ou use Olá seguir etapas toocreate um novo grupo de recursos:
      
      * Selecione  **&lt; &lt; criar novo grupo de recursos &gt; &gt;**  em Olá **grupo de recursos** menu suspenso.
      * Olá **novo grupo de recursos** caixa de diálogo será exibida:
        
          ![Novo grupo de recursos][12]
      * Em Olá Olá **nome** caixa de texto, especifique um nome para seu novo grupo de recursos.
      * Em Olá Olá **região** menu suspenso, selecione Olá apropriado do Azure Datacenter local para seu grupo de recursos.
      * Clique em **OK**.
   7. Olá **plano do serviço de aplicativo** menu suspenso lista planos de serviço de aplicativo hello que estão associados a saudação grupo de recursos que você selecionou. (Um plano de serviço de aplicativo especifica informações como a localização de saudação do seu aplicativo Web, Olá tipo de preço e tamanho de instância de computação hello. Um único Plano do Serviço de Aplicativo pode ser usado para vários Aplicativos Web, por isso, ele é mantido separadamente de uma implantação de Aplicativo Web específica.)
      
       Você pode selecionar um plano de serviço de aplicativo existente (se houver) e ignorar toostep h abaixo, ou usar Olá toocreate etapas um novo plano de serviço de aplicativo a seguir:
      
      * Selecione  **&lt; &lt; criar novo plano de serviço de aplicativo &gt; &gt;**  em Olá **plano do serviço de aplicativo** menu suspenso.
      * Olá **novo plano de serviço de aplicativo** caixa de diálogo será exibida:
        
          ![Novo Plano do Serviço de Aplicativo][13]
      * Em Olá Olá **nome** caixa de texto, especifique um nome para o novo plano de serviço de aplicativo.
      * Em Olá Olá **local** menu suspenso, selecione Olá apropriado do Azure Datacenter local para o plano de saudação.
      * Em Olá Olá **preço** menu suspenso, selecione Olá apropriado de preços para o plano de saudação. Para fins de teste, é possível escolher **Gratuito**.
      * Em Olá Olá **tamanho da instância** menu suspenso, o tamanho de instância apropriada do hello selecione plano hello. Para fins de teste, é possível escolher **Pequeno**.
      * Clique em **OK**.
   8. (Opcional) Por padrão, uma distribuição recente de Java 8 será implantada automaticamente como sua JVM pelo contêiner de aplicativo da web tooyour do Azure. No entanto, você pode selecionar uma versão diferente e a distribuição de saudação da JVM. Assim, o toodo use Olá etapas a seguir:
      
      * Clique em Olá **JDK** guia Olá **novo contêiner de aplicativo Web** caixa de diálogo.
      * Você pode escolher uma saudação as opções a seguir:
        
        * Implantar o padrão de saudação JDK oferecido pelo Azure
        * Implantar um JDK de terceiros de uma lista suspensa de JDKs adicionais que estão disponíveis no Azure
        * Implantar um JDK personalizado, que deve ser empacotado como um arquivo ZIP e ser publicamente disponível ou em sua conta de armazenamento do Azure
        
        ![Guia Novo JDK de Contêiner de Aplicativo][11b]
   9. Depois de concluir todos Olá acima etapas, caixa de diálogo novo contêiner de aplicativo Web hello deve se assemelhar Olá ilustração a seguir:
      
       ![Novo Contêiner de Aplicativo][14]
   10. Clique em **Okey** toocomplete criação de saudação do seu novo contêiner de aplicativo Web.
       
        Aguarde alguns segundos para lista de saudação do hello toobe de contêineres de aplicativo Web atualizada e o contêiner de aplicativo web recém-criado agora deve ser selecionado na lista de saudação.
6. Agora você está pronto toocomplete implantação inicial do hello de tooAzure seu aplicativo Web; Clique em **Okey** toodeploy sua toohello de aplicativo Java selecionado contêiner do aplicativo Web. Por padrão, o aplicativo será implantado como um subdiretório saudação do servidor de aplicativos. Se quiser toobe implantado como um aplicativo raiz de hello, verifique Olá **implantar tooroot** caixa de seleção antes de clicar em **Okey**.
   
    ![Implantar tooAzure][15]
7. Em seguida, você deve ver Olá **o Log de atividades do Azure** exibição, que indica o status de implantação de saudação do seu aplicativo Web.
   
    ![Indicador de Progresso][16]
   
    processo de saudação de implantar seu aplicativo Web tooAzure deve levar somente alguns segundos toocomplete. Quando pronto seu aplicativo, você verá um link chamado **publicado** em Olá **Status** coluna. Quando você clica em um link de Olá, levará home page do aplicativo da Web tooyour implantado, ou você pode usar etapas Olá Olá seção toobrowse tooyour web aplicativo a seguir.

## <a name="browsing-tooyour-web-app-on-azure"></a>Navegação tooyour aplicativo Web no Azure
toobrowse tooyour aplicativo Web no Azure, você pode usar o hello **Azure Explorer** exibição.

Se hello **Azure Explorer** exibição não ainda estiver aberta, você pode abri-lo clicando em, em seguida, **exibição** menu em IntelliJ, em seguida, clique em **janelas de ferramentas**e, em seguida, clique em  **Gerenciador de serviço**. Se você não tiver conectado anteriormente, ele solicitará que você toodo assim.

Olá quando **Azure Explorer** modo de exibição, use execute tooyour de toobrowse essas etapas aplicativo Web: 

1. Expanda Olá **Azure** nó.
2. Expanda Olá **aplicativos Web** nó. 
3. Olá com o botão direito desejada do aplicativo Web.
4. Quando o menu de contexto Olá for exibida, clique em **abrir no navegador**.
   
    ![Procurar o Aplicativo Web][17]

## <a name="updating-your-web-app"></a>Atualizando seu aplicativo Web
A atualização de um aplicativo Web do Azure em execução é um processo rápido e fácil, e você tem duas opções de atualização:

* Você pode atualizar a implantação de saudação do aplicativo Web Java existente.
* Você pode publicar um toohello de aplicativo Java adicional mesmo contêiner de aplicativo da Web.

Em ambos os casos, o processo de saudação é idêntico e leva apenas alguns segundos:

1. No Explorador de projeto IntelliJ Olá, clique no aplicativo de Java hello deseja tooupdate ou adicionar tooan existente do contêiner do aplicativo da Web.
2. Quando o menu de contexto Olá for exibida, selecione **Azure** e, em seguida, **Publicar como um aplicativo Web do Azure...**
3. Como você já fez logon anteriormente, verá uma lista com seus contêineres de aplicativo Web existentes. Selecione Olá um deseja toopublish ou publicar novamente o Java aplicativo tooand, clique **Okey**.

Alguns segundos mais tarde, Olá **o Log de atividades do Azure** exibição mostrará sua implantação atualizada como **publicado** e você será capaz de tooverify seu aplicativo atualizado em um navegador da web.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Iniciar, parar ou reiniciar o aplicativo Web existente
toostart ou interromper um contêiner existente do aplicativo Web do Azure, (incluindo todos os aplicativos do Java Olá implantado nele), você pode usar o hello **Azure Explorer** exibição.

Se hello **Azure Explorer** exibição não ainda estiver aberta, você pode abri-lo clicando em, em seguida, **exibição** menu em IntelliJ, em seguida, clique em **janelas de ferramentas**e, em seguida, clique em  **Gerenciador de serviço**. Se você não tiver conectado anteriormente, ele solicitará que você toodo assim.

Olá quando **Azure Explorer** modo de exibição, use siga essas etapas toostart ou interrompa o aplicativo Web: 

1. Expanda Olá **Azure** nó.
2. Expanda Olá **aplicativos Web** nó. 
3. Olá com o botão direito desejada do aplicativo Web.
4. Quando o menu de contexto Olá for exibida, clique em **iniciar**, **parar**, ou **reiniciar**. Observe que as opções de menu Olá têm reconhecimento de contexto, para que você só pode parar um aplicativo web em execução ou iniciar um aplicativo da web que não está em execução no momento.
   
    ![Parar Aplicativo Web][18]

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre Olá kits de ferramentas do Azure para Java IDEs, consulte Olá links a seguir:

* [Kit de ferramentas do Azure para Eclipse]
  * [Saudação de instalar o Kit de ferramentas do Azure para Eclipse]
  * [Criar um aplicativo Web Hello World para o Azure no Eclipse]
  * [Novidades no Kit de ferramentas do Azure para Eclipse de saudação]
* [Kit de ferramentas do Azure para IntelliJ]
  * [Olá instalando o Kit de ferramentas do Azure para IntelliJ]
  * *Criar um aplicativo Web Hello World para o Azure no IntelliJ (este artigo)*
  * [Novidades no Kit de ferramentas do Azure para IntelliJ de saudação]

<a name="see-also"></a>

## <a name="see-also"></a>Consulte também
Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure].

Para obter informações adicionais sobre a criação de aplicativos Web do Azure, consulte Olá [visão geral de aplicativos Web].

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Kit de ferramentas do Azure para Eclipse]: ../azure-toolkit-for-eclipse.md
[Kit de ferramentas do Azure para IntelliJ]: ../azure-toolkit-for-intellij.md
[Criar um aplicativo Web Hello World para o Azure no Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Saudação de instalar o Kit de ferramentas do Azure para Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[Olá instalando o Kit de ferramentas do Azure para IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Novidades no Kit de ferramentas do Azure para Eclipse de saudação]: ../azure-toolkit-for-eclipse-whats-new.md
[Novidades no Kit de ferramentas do Azure para IntelliJ de saudação]: ../azure-toolkit-for-intellij-whats-new.md

[Centro de desenvolvedores de Java do Azure]: https://azure.microsoft.com/develop/java/
[visão geral de aplicativos Web]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/app-service-web-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/app-service-web-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/app-service-web-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/app-service-web-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/app-service-web-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/app-service-web-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/app-service-web-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/app-service-web-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/app-service-web-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/app-service-web-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/app-service-web-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/app-service-web-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/app-service-web-intellij-create-hello-world-web-app/18-Stop-Web-App.png
