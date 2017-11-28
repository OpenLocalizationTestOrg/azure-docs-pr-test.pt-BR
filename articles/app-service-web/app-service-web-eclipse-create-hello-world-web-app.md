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
# <a name="create-a-basic-azure-web-app-using-eclipse"></a><span data-ttu-id="2e736-103">Criar um aplicativo web básico do Azure usando o Eclipse</span><span class="sxs-lookup"><span data-stu-id="2e736-103">Create a basic Azure web app using Eclipse</span></span>
<span data-ttu-id="2e736-104">Este tutorial mostra como toocreate e implantar um tooAzure de aplicativo Hello World básica como um aplicativo Web usando Olá [Kit de ferramentas do Azure para Eclipse].</span><span class="sxs-lookup"><span data-stu-id="2e736-104">This tutorial shows how toocreate and deploy a basic Hello World application tooAzure as a Web App by using hello [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="2e736-105">Mostramos um exemplo básico de JSP para manter a simplicidade, mas, para a implantação do Azure, etapas semelhantes podem ser usadas para um servlet Java.</span><span class="sxs-lookup"><span data-stu-id="2e736-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="2e736-106">Quando você concluiu este tutorial, o aplicativo ficará semelhante toohello ilustração a seguir quando você exibi-lo em um navegador da web:</span><span class="sxs-lookup"><span data-stu-id="2e736-106">When you have completed this tutorial, your application will look similar toohello following illustration when you view it in a web browser:</span></span>

![Visualização do aplicativo Hello World][01]

## <a name="prerequisites"></a><span data-ttu-id="2e736-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2e736-108">Prerequisites</span></span>
* <span data-ttu-id="2e736-109">Um JDK (Java Developer Kit) versão 1.8 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="2e736-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="2e736-110">IDE do Eclipse para desenvolvedores de Java EE, Luna ou posterior.</span><span class="sxs-lookup"><span data-stu-id="2e736-110">Eclipse IDE for Java EE Developers, Luna or later.</span></span> <span data-ttu-id="2e736-111">Isso pode ser baixado em <http://www.eclipse.org/downloads/>.</span><span class="sxs-lookup"><span data-stu-id="2e736-111">This can be downloaded from <http://www.eclipse.org/downloads/>.</span></span>
* <span data-ttu-id="2e736-112">Uma distribuição de um servidor Web ou de um servidor de aplicativo baseado em Java, como o [Apache Tomcat] ou o [Jetty].</span><span class="sxs-lookup"><span data-stu-id="2e736-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="2e736-113">Uma assinatura do Azure, que pode ser adquirida em <https://azure.microsoft.com/free/> ou <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="2e736-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="2e736-114">Olá [Kit de ferramentas do Azure para Eclipse].</span><span class="sxs-lookup"><span data-stu-id="2e736-114">hello [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="2e736-115">Para obter informações sobre como instalar Olá Kit de ferramentas do Azure, consulte [Olá instalando o Kit de ferramentas do Azure para Eclipse].</span><span class="sxs-lookup"><span data-stu-id="2e736-115">For information about installing hello Azure Toolkit, see [Installing hello Azure Toolkit for Eclipse].</span></span>

## <a name="toocreate-a-hello-world-application"></a><span data-ttu-id="2e736-116">toocreate um aplicativo Hello World</span><span class="sxs-lookup"><span data-stu-id="2e736-116">toocreate a Hello World application</span></span>
<span data-ttu-id="2e736-117">Primeiro, vamos começar com a criação de um projeto Java.</span><span class="sxs-lookup"><span data-stu-id="2e736-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="2e736-118">Inicie o Eclipse e no menu de saudação clique **arquivo**, clique em **novo**e, em seguida, clique em **projeto Web dinâmico**.</span><span class="sxs-lookup"><span data-stu-id="2e736-118">Start Eclipse, and at hello menu click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="2e736-119">(Se você não vir **projeto Web dinâmico** listado como um projeto disponível depois de clicar em **arquivo** e **novo**, em seguida, Olá a seguir: clique em **arquivo**, clique em **novo**, clique em **projeto...** , expanda **Web**, clique em **projeto Web dinâmico**e clique em **próximo**.)</span><span class="sxs-lookup"><span data-stu-id="2e736-119">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do hello following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>
2. <span data-ttu-id="2e736-120">Para fins deste tutorial, nomeie o projeto de saudação **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="2e736-120">For purposes of this tutorial, name hello project **MyWebApp**.</span></span> <span data-ttu-id="2e736-121">Sua tela será exibido a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="2e736-121">Your screen will appear similar toohello following:</span></span>
   
    ![Criando um novo projeto Web dinâmico][02]
3. <span data-ttu-id="2e736-123">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="2e736-123">Click **Finish**.</span></span>
4. <span data-ttu-id="2e736-124">No modo de exibição do Gerenciador de Projeto do Eclipse, expanda **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="2e736-124">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="2e736-125">Clique com o botão direito do mouse em **WebContent**, clique em **Novo** e, em seguida, clique em **Arquivo JSP**.</span><span class="sxs-lookup"><span data-stu-id="2e736-125">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
5. <span data-ttu-id="2e736-126">Em Olá **novo arquivo JSP** caixa de diálogo, o arquivo de saudação do nome **index.jsp**, mantenha a pasta pai Olá **MyWebApp/WebContent**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="2e736-126">In hello **New JSP File** dialog box, name hello file **index.jsp**, keep hello parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>
6. <span data-ttu-id="2e736-127">Em Olá **Selecionar modelo JSP** caixa de diálogo, para fins deste tutorial, selecione **novo arquivo JSP (html)**e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="2e736-127">In hello **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
7. <span data-ttu-id="2e736-128">Quando o arquivo index.jsp for aberto no Eclipse, adicione na exibição do texto toodynamically **Olá, mundo!**</span><span class="sxs-lookup"><span data-stu-id="2e736-128">When your index.jsp file opens in Eclipse, add in text toodynamically display **Hello World!**</span></span> <span data-ttu-id="2e736-129">dentro de saudação existente `<body>` elemento.</span><span class="sxs-lookup"><span data-stu-id="2e736-129">within hello existing `<body>` element.</span></span> <span data-ttu-id="2e736-130">Seu atualizada `<body>` conteúdo deve ser semelhante a saudação de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="2e736-130">Your updated `<body>` content should resemble hello following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. <span data-ttu-id="2e736-131">Salve o index.jsp.</span><span class="sxs-lookup"><span data-stu-id="2e736-131">Save index.jsp.</span></span>

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a><span data-ttu-id="2e736-132">toodeploy tooan seu aplicativo recipiente de aplicativo da Web do Azure</span><span class="sxs-lookup"><span data-stu-id="2e736-132">toodeploy your application tooan Azure Web App Container</span></span>
<span data-ttu-id="2e736-133">Há várias maneiras pelas quais você pode implantar um tooAzure de aplicativo web Java.</span><span class="sxs-lookup"><span data-stu-id="2e736-133">There are several ways by which you can deploy a Java web application tooAzure.</span></span> <span data-ttu-id="2e736-134">Este tutorial descreve uma saudação mais simples: o aplicativo será implantado tooan contêiner de aplicativo Web do Azure – nenhum tipo de projeto especial nem ferramentas adicionais são necessárias.</span><span class="sxs-lookup"><span data-stu-id="2e736-134">This tutorial describes one of hello simplest: your application will be deployed tooan Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="2e736-135">Olá Olá JDK e o software da web que contêiner será fornecido para você pelo Azure, portanto não há nenhuma necessidade tooupload seu próprios; tudo o que você precisa é de seu aplicativo da Web de Java.</span><span class="sxs-lookup"><span data-stu-id="2e736-135">hello JDK and hello web container software will be provided for you by Azure, so there is no need tooupload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="2e736-136">Como resultado, o processo de publicação de saudação para seu aplicativo levará segundos, minutos não.</span><span class="sxs-lookup"><span data-stu-id="2e736-136">As a result, hello publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="2e736-137">No Gerenciador de Projetos do Eclipse, clique com o botão direito do mouse em **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="2e736-137">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>
2. <span data-ttu-id="2e736-138">No menu de contexto hello, selecione **Azure**, em seguida, clique em **Publicar como um aplicativo Web do Azure...**</span><span class="sxs-lookup"><span data-stu-id="2e736-138">In hello context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
    ![Publicar como Aplicativo Web do Azure][03]
   
    <span data-ttu-id="2e736-140">Como alternativa, enquanto o projeto de aplicativo web está selecionado no Explorador de projeto do hello, você pode clicar em Olá **publicar** botão suspenso na barra de ferramentas hello e selecione **Publicar como um aplicativo Web do Azure** lá:</span><span class="sxs-lookup"><span data-stu-id="2e736-140">Alternatively, while your web application project is selected in hello Project Explorer, you can click hello **Publish** dropdown button on hello toolbar and select **Publish as Azure Web App** from there:</span></span>
   
    ![Publicar como Aplicativo Web do Azure][14]
3. <span data-ttu-id="2e736-142">Se você tiver não tiver entrado no Azure do Eclipse, será solicitado toosign em sua conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="2e736-142">If you have not already signed into Azure from Eclipse, you will be prompted toosign into your Azure account:</span></span>
   
    ![Caixa de diálogo Entrar no Azure][04]
   
    <span data-ttu-id="2e736-144">Se você tiver várias contas do Azure, alguns dos avisos Olá Olá entrar no processo pode ser exibido mais de uma vez, mesmo se eles parecem toobe Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="2e736-144">If you have multiple Azure accounts, some of hello prompts during hello sign in process may be shown more than once, even if they appear toobe hello same.</span></span> <span data-ttu-id="2e736-145">Quando isso acontece, continue seguindo as instruções de logon hello.</span><span class="sxs-lookup"><span data-stu-id="2e736-145">When this happens, continue following hello sign in instructions.</span></span>
4. <span data-ttu-id="2e736-146">Depois de ter entrado com êxito em sua conta do Azure, Olá **gerenciar assinaturas** caixa de diálogo exibirá uma lista de assinaturas que estão associados com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="2e736-146">After you have successfully signed into your Azure account, hello **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="2e736-147">Se houver várias assinaturas listadas e você desejar toowork com apenas um subconjunto específico de-los, você pode, opcionalmente, desmarque Olá aquelas que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="2e736-147">If there are multiple subscriptions listed and you want toowork with only a specific subset of them, you may optionally uncheck hello ones you do want toouse.</span></span> <span data-ttu-id="2e736-148">Depois de selecionar suas assinaturas, clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="2e736-148">When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Caixa de diálogo Gerenciar Assinaturas][05]
5. <span data-ttu-id="2e736-150">Olá quando **implantar tooAzure contêiner de aplicativo da Web** caixa de diálogo for exibida, ele exibirá qualquer contêiner de aplicativo Web que você criou anteriormente; se você não criou qualquer contêiner, a lista de saudação estará vazia.</span><span class="sxs-lookup"><span data-stu-id="2e736-150">When hello **Deploy tooAzure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, hello list will be empty.</span></span>
   
    ![Caixa de diálogo do contêiner do aplicativo da Web tooAzure implantar][06]
6. <span data-ttu-id="2e736-152">Se você não criou um contêiner de aplicativo Web do Azure antes, ou se você gostaria que toopublish seu aplicativo tooa novo contêiner, use Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="2e736-152">If you have not created an Azure Web App Container before, or if you would like toopublish your application tooa new container, use hello following steps.</span></span> <span data-ttu-id="2e736-153">Caso contrário, selecione um contêiner do aplicativo Web existente e ignorar toostep 7 abaixo.</span><span class="sxs-lookup"><span data-stu-id="2e736-153">Otherwise, select an existing Web App Container and skip toostep 7 below.</span></span>
   
   1. <span data-ttu-id="2e736-154">Clique em **Novo...**</span><span class="sxs-lookup"><span data-stu-id="2e736-154">Click **New...**</span></span>
      
       ![Caixa de diálogo do contêiner do aplicativo da Web tooAzure implantar][15]
   2. <span data-ttu-id="2e736-156">Olá **novo contêiner de aplicativo Web** caixa de diálogo será exibida:</span><span class="sxs-lookup"><span data-stu-id="2e736-156">hello **New Web App Container** dialog box will be displayed:</span></span>
      
       ![Caixa de diálogo Novo contêiner do aplicativo Web][07a]
   3. <span data-ttu-id="2e736-158">Insira um **rótulo DNS** para seu contêiner de aplicativo da Web; isso formarão o rótulo DNS Olá folha da URL de host Olá para o aplicativo web no Azure.</span><span class="sxs-lookup"><span data-stu-id="2e736-158">Enter a **DNS Label** for your Web App Container; this will form hello leaf DNS label of hello host URL for your web application in Azure.</span></span> <span data-ttu-id="2e736-159">(Observe que Olá deve estar disponível e está de acordo com requisitos de nomenclatura de aplicativo Web tooAzure).</span><span class="sxs-lookup"><span data-stu-id="2e736-159">(Note that hello name must be available and conform tooAzure Web App naming requirements.)</span></span>
   4. <span data-ttu-id="2e736-160">Em Olá **contêiner da Web** menu suspenso, selecione Olá o software apropriado para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2e736-160">In hello **Web Container** drop-down menu, select hello appropriate software for your application.</span></span>
      
       <span data-ttu-id="2e736-161">No momento, você pode escolher entre o Tomcat 8, Tomcat 7 ou Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="2e736-161">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="2e736-162">Uma distribuição recente do software de saudação selecionada será fornecida pelo Azure e ele será executado em uma distribuição recente do JDK 8 criado pela Oracle e fornecido pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="2e736-162">A recent distribution of hello selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="2e736-163">Em Olá **assinatura** menu suspenso, assinatura selecione Olá deseja toouse para essa implantação.</span><span class="sxs-lookup"><span data-stu-id="2e736-163">In hello **Subscription** drop-down menu, select hello subscription you want toouse for this deployment.</span></span>
   6. <span data-ttu-id="2e736-164">Em Olá **grupo de recursos** menu suspenso, selecione Olá grupo de recursos com o qual você deseja tooassociate seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="2e736-164">In hello **Resource Group** drop-down menu, select hello Resource Group with which you want tooassociate your Web App.</span></span> <span data-ttu-id="2e736-165">(Grupos de recursos do azure permite que você toogroup recursos relacionados juntos para que, por exemplo, pode ser excluídos em conjunto.)</span><span class="sxs-lookup"><span data-stu-id="2e736-165">(Azure Resource Groups allow you toogroup related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="2e736-166">Você pode selecionar um grupo de recursos existente (se houver) e ignorar toostep g abaixo, ou use Olá seguindo estas etapas toocreate um novo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="2e736-166">You can select an existing Resource Group (if you have any) and skip toostep g below, or use hello following these steps toocreate a new Resource Group:</span></span>
      
      * <span data-ttu-id="2e736-167">Clique em **Novo...**</span><span class="sxs-lookup"><span data-stu-id="2e736-167">Click **New...**</span></span>
      * <span data-ttu-id="2e736-168">Olá **novo grupo de recursos** caixa de diálogo será exibida:</span><span class="sxs-lookup"><span data-stu-id="2e736-168">hello **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Caixa de diálogo Novo Grupo de Recursos][08]
      * <span data-ttu-id="2e736-170">Em Olá Olá **nome** caixa de texto, especifique um nome para seu novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2e736-170">In hello hello **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="2e736-171">Em Olá Olá **região** menu suspenso, selecione Olá apropriado do Azure Datacenter local para seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2e736-171">In hello hello **Region** drop-down menu, select hello appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="2e736-172">OPCIONAL: Por padrão, uma distribuição recente de Java 8 será implantada pelo Azure automaticamente tooyour contêiner de aplicativo da web como sua JVM.</span><span class="sxs-lookup"><span data-stu-id="2e736-172">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically tooyour web app container as your JVM.</span></span> <span data-ttu-id="2e736-173">No entanto, você pode especificar uma versão diferente e a distribuição de saudação JVM se for necessário para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="2e736-173">However, you can specify a different version and distribution of hello JVM if your Web App requires it.</span></span> <span data-ttu-id="2e736-174">Olá toospecify JDK para seu aplicativo Web, clique em Olá **JDK** guia e selecione uma saudação as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="2e736-174">toospecify hello JDK for your Web App, click hello **JDK** tab, and select one of hello following options:</span></span>
        
        * <span data-ttu-id="2e736-175">**Implantar o padrão de saudação JDK oferecida pelo serviço de aplicativos Web do Azure**: essa opção implantará uma distribuição recente de Java 8.</span><span class="sxs-lookup"><span data-stu-id="2e736-175">**Deploy hello default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java 8.</span></span>
        * <span data-ttu-id="2e736-176">**Implantar um JDK disponível no Azure de terceiros 3º**: essa opção permite que você toochoose de lista de saudação de JDKs que são fornecidos pelo Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2e736-176">**Deploy a 3rd party JDK available on Azure**: This option allows you toochoose from hello list of JDKs which are provided by Microsoft Azure.</span></span>
        * <span data-ttu-id="2e736-177">**Implantar meu próprio JDK a partir deste local de download**: essa opção permite que você toospecify sua distribuição JDK, que deve ser empacotada como um arquivo ZIP e carregado tooeither um local de download disponível publicamente ou um armazenamento do Azure da conta para a qual você tem acesso.</span><span class="sxs-lookup"><span data-stu-id="2e736-177">**Deploy my own JDK from this download location**: This option allows you toospecify your own JDK distribution, which must be packaged as a ZIP file and uploaded tooeither a publicly available download location or an Azure storage account for which you have access.</span></span>
          
          ![Caixa de diálogo Novo contêiner do aplicativo Web][07b]
   7. <span data-ttu-id="2e736-179">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="2e736-179">Click **OK**.</span></span>
   8. <span data-ttu-id="2e736-180">Olá **plano do serviço de aplicativo** menu suspenso lista planos de serviço de aplicativo hello que estão associados a saudação grupo de recursos que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="2e736-180">hello **App Service Plan** drop-down menu lists hello app service plans that are associated with hello Resource Group that you selected.</span></span> <span data-ttu-id="2e736-181">(Os planos de serviço de aplicativo especificam informações como a localização de saudação do seu aplicativo Web, Olá tipo de preço e tamanho de instância de computação hello.</span><span class="sxs-lookup"><span data-stu-id="2e736-181">(App Service Plans specify information such as hello location of your Web App, hello pricing tier and hello compute instance size.</span></span> <span data-ttu-id="2e736-182">Um único Plano do Serviço de Aplicativo pode ser usado para vários Aplicativos Web, por isso, ele é mantido separadamente de uma implantação de Aplicativo Web específica.)</span><span class="sxs-lookup"><span data-stu-id="2e736-182">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="2e736-183">Você pode selecionar um plano de serviço de aplicativo existente (se houver) e ignorar toostep h abaixo, ou usar Olá toocreate essas etapas que um novo plano de serviço de aplicativo a seguir:</span><span class="sxs-lookup"><span data-stu-id="2e736-183">You can select an existing App Service Plan (if you have any) and skip toostep h below, or use hello following these steps toocreate a new App Service Plan:</span></span>
      
      * <span data-ttu-id="2e736-184">Clique em **Novo...**</span><span class="sxs-lookup"><span data-stu-id="2e736-184">Click **New...**</span></span>
      * <span data-ttu-id="2e736-185">Olá **novo plano de serviço de aplicativo** caixa de diálogo será exibida:</span><span class="sxs-lookup"><span data-stu-id="2e736-185">hello **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Caixa de diálogo Novo Plano do Serviço de Aplicativo][09]
      * <span data-ttu-id="2e736-187">Em Olá Olá **nome** caixa de texto, especifique um nome para o novo plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2e736-187">In hello hello **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="2e736-188">Em Olá Olá **local** menu suspenso, selecione Olá apropriado do Azure Datacenter local para o plano de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e736-188">In hello hello **Location** drop-down menu, select hello appropriate Azure data center location for hello plan.</span></span>
      * <span data-ttu-id="2e736-189">Em Olá Olá **preço** menu suspenso, selecione Olá apropriado de preços para o plano de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e736-189">In hello hello **Pricing Tier** drop-down menu, select hello appropriate pricing for hello plan.</span></span> <span data-ttu-id="2e736-190">Para fins de teste, é possível escolher **Gratuito**.</span><span class="sxs-lookup"><span data-stu-id="2e736-190">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="2e736-191">Em Olá Olá **tamanho da instância** menu suspenso, o tamanho de instância apropriada do hello selecione plano hello.</span><span class="sxs-lookup"><span data-stu-id="2e736-191">In hello hello **Instance Size** drop-down menu, select hello appropriate instance size for hello plan.</span></span> <span data-ttu-id="2e736-192">Para fins de teste, é possível escolher **Pequeno**.</span><span class="sxs-lookup"><span data-stu-id="2e736-192">For testing purposes you can choose **Small**.</span></span>
   9. <span data-ttu-id="2e736-193">Depois de concluir todos Olá acima etapas, caixa de diálogo novo contêiner de aplicativo Web hello deve se assemelhar Olá ilustração a seguir:</span><span class="sxs-lookup"><span data-stu-id="2e736-193">Once you have completed all of hello above steps, hello New Web App Container dialog box should resemble hello following illustration:</span></span>
      
       ![Caixa de diálogo Novo contêiner do aplicativo Web][10]
   10. <span data-ttu-id="2e736-195">Clique em **Okey** toocomplete criação de saudação do seu novo contêiner de aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="2e736-195">Click **OK** toocomplete hello creation of your new Web App container.</span></span>
       
        <span data-ttu-id="2e736-196">Aguarde alguns segundos para lista de saudação do hello toobe de contêineres de aplicativo Web atualizada e o contêiner de aplicativo web recém-criado agora deve ser selecionado na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e736-196">Wait a few seconds for hello list of hello Web App containers toobe refreshed, and your newly-created web app container should now be selected in hello list.</span></span>
7. <span data-ttu-id="2e736-197">Agora você está pronto toocomplete implantação inicial do hello de tooAzure seu aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="2e736-197">You are now ready toocomplete hello initial deployment of your Web App tooAzure:</span></span>
   
    ![Caixa de diálogo do contêiner do aplicativo da Web tooAzure implantar][11]
   
    <span data-ttu-id="2e736-199">Clique em **Okey** toodeploy sua toohello de aplicativo Java selecionado contêiner do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="2e736-199">Click **OK** toodeploy your Java application toohello selected Web App container.</span></span>
   
    <span data-ttu-id="2e736-200">Por padrão, o aplicativo será implantado como um subdiretório saudação do servidor de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2e736-200">By default, your application will be deployed as a subdirectory of hello application server.</span></span> <span data-ttu-id="2e736-201">Se quiser toobe implantado como um aplicativo raiz de hello, verifique Olá **implantar tooroot** caixa de seleção antes de clicar em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="2e736-201">If you want it toobe deployed as hello root application, check hello **Deploy tooroot** checkbox before clicking **OK**.</span></span>
8. <span data-ttu-id="2e736-202">Em seguida, você deve ver Olá **o Log de atividades do Azure** exibição, que indica o status de implantação de saudação do seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="2e736-202">Next, you should see hello **Azure Activity Log** view, which will indicate hello deployment status of your Web App.</span></span>
   
    ![Log de Atividades do Azure][12]
   
    <span data-ttu-id="2e736-204">processo de saudação de implantar seu aplicativo Web tooAzure deve levar somente alguns segundos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="2e736-204">hello process of deploying your Web App tooAzure should take only a few seconds toocomplete.</span></span> <span data-ttu-id="2e736-205">Quando pronto seu aplicativo, você verá um link chamado **publicado** em Olá **Status** coluna.</span><span class="sxs-lookup"><span data-stu-id="2e736-205">When your application ready, you will see a link named **Published** in hello **Status** column.</span></span> <span data-ttu-id="2e736-206">Quando você clica em um link de hello, levará home page do aplicativo da Web tooyour implantado.</span><span class="sxs-lookup"><span data-stu-id="2e736-206">When you click hello link, it will take you tooyour deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="2e736-207">Atualizando seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="2e736-207">Updating your web app</span></span>
<span data-ttu-id="2e736-208">A atualização de um aplicativo Web do Azure em execução é um processo rápido e fácil, e você tem duas opções de atualização:</span><span class="sxs-lookup"><span data-stu-id="2e736-208">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="2e736-209">Você pode atualizar a implantação de saudação do aplicativo Web Java existente.</span><span class="sxs-lookup"><span data-stu-id="2e736-209">You can update hello deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="2e736-210">Você pode publicar um toohello de aplicativo Java adicional mesmo contêiner de aplicativo da Web.</span><span class="sxs-lookup"><span data-stu-id="2e736-210">You can publish an additional Java application toohello same Web App Container.</span></span>

<span data-ttu-id="2e736-211">Em ambos os casos, o processo de saudação é idêntico e leva apenas alguns segundos:</span><span class="sxs-lookup"><span data-stu-id="2e736-211">In either case, hello process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="2e736-212">No Explorador de projeto do Eclipse Olá, clique no aplicativo de Java hello deseja tooupdate ou adicionar tooan existente do contêiner do aplicativo da Web.</span><span class="sxs-lookup"><span data-stu-id="2e736-212">In hello Eclipse project explorer, right-click hello Java application you want tooupdate or add tooan existing Web App Container.</span></span>
2. <span data-ttu-id="2e736-213">Quando o menu de contexto Olá for exibida, selecione **Azure** e, em seguida, **Publicar como um aplicativo Web do Azure...**</span><span class="sxs-lookup"><span data-stu-id="2e736-213">When hello context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="2e736-214">Como você já fez logon anteriormente, verá uma lista com seus contêineres de aplicativo Web existentes.</span><span class="sxs-lookup"><span data-stu-id="2e736-214">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="2e736-215">Selecione Olá um deseja toopublish ou publicar novamente o Java aplicativo tooand, clique **Okey**.</span><span class="sxs-lookup"><span data-stu-id="2e736-215">Select hello one you want toopublish or re-publish your Java application tooand click **OK**.</span></span>

<span data-ttu-id="2e736-216">Alguns segundos mais tarde, Olá **o Log de atividades do Azure** exibição mostrará sua implantação atualizada como **publicado** e você será capaz de tooverify seu aplicativo atualizado em um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="2e736-216">A few seconds later, hello **Azure Activity Log** view will show your updated deployment as **Published** and you will be able tooverify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="2e736-217">Iniciar, parar ou reiniciar o aplicativo Web existente</span><span class="sxs-lookup"><span data-stu-id="2e736-217">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="2e736-218">toostart ou interromper um contêiner existente do aplicativo Web do Azure, (incluindo todos os aplicativos do Java Olá implantado nele), você pode usar o hello **Azure Explorer** exibição.</span><span class="sxs-lookup"><span data-stu-id="2e736-218">toostart or stop an existing Azure Web App container, (including all hello deployed Java applications in it), you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="2e736-219">Se hello **Azure Explorer** exibição não ainda estiver aberta, você pode abri-lo clicando em, em seguida, **janela** menu do Eclipse, clique **exibição**, em seguida, **outros...** , em seguida, **Azure**e, em seguida, clique em **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="2e736-219">If hello **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="2e736-220">Se você não tiver conectado anteriormente, ele solicitará que você toodo assim.</span><span class="sxs-lookup"><span data-stu-id="2e736-220">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="2e736-221">Olá quando **Azure Explorer** modo de exibição, use siga essas etapas toostart ou interrompa o aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="2e736-221">When hello **Azure Explorer** view is displayed, use follow these steps toostart or stop your Web App:</span></span> 

1. <span data-ttu-id="2e736-222">Expanda Olá **Azure** nó.</span><span class="sxs-lookup"><span data-stu-id="2e736-222">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="2e736-223">Expanda Olá **aplicativos Web** nó.</span><span class="sxs-lookup"><span data-stu-id="2e736-223">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="2e736-224">Olá com o botão direito desejada do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="2e736-224">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="2e736-225">Quando o menu de contexto Olá for exibida, clique em **iniciar**, **parar**, ou **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="2e736-225">When hello context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="2e736-226">Observe que as opções de menu Olá têm reconhecimento de contexto, para que você só pode parar um aplicativo web em execução ou iniciar um aplicativo da web que não está em execução no momento.</span><span class="sxs-lookup"><span data-stu-id="2e736-226">Note that hello menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Interromper um aplicativo Web existente][13]

## <a name="next-steps"></a><span data-ttu-id="2e736-228">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2e736-228">Next Steps</span></span>
<span data-ttu-id="2e736-229">Para obter mais informações sobre Olá kits de ferramentas do Azure para Java IDEs, consulte Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="2e736-229">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="2e736-230">[Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2e736-230">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="2e736-231">[Olá instalando o Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2e736-231">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="2e736-232">*Criar uma aplicativo Web Hello World para o Azure no Eclipse (este artigo)*</span><span class="sxs-lookup"><span data-stu-id="2e736-232">*Create a Hello World Web App for Azure in Eclipse (This Article)*</span></span>
  * <span data-ttu-id="2e736-233">[Novidades no Kit de ferramentas do Azure para Eclipse de saudação]</span><span class="sxs-lookup"><span data-stu-id="2e736-233">[What's New in hello Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="2e736-234">[Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="2e736-234">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="2e736-235">[Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="2e736-235">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="2e736-236">[Criar um aplicativo Web Hello World para o Azure no IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="2e736-236">[Create a Hello World Web App for Azure in IntelliJ]</span></span>
  * <span data-ttu-id="2e736-237">[Novidades no Kit de ferramentas do Azure para IntelliJ de saudação]</span><span class="sxs-lookup"><span data-stu-id="2e736-237">[What's New in hello Azure Toolkit for IntelliJ]</span></span>

<span data-ttu-id="2e736-238">Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure].</span><span class="sxs-lookup"><span data-stu-id="2e736-238">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<span data-ttu-id="2e736-239">Para obter informações adicionais sobre a criação de aplicativos Web do Azure, consulte Olá [visão geral de aplicativos Web].</span><span class="sxs-lookup"><span data-stu-id="2e736-239">For additional information about creating Azure Web Apps, see hello [Web Apps Overview].</span></span>

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
