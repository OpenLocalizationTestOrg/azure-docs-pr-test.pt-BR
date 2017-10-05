---
title: "Criar um aplicativo Web do Azure básico no IntelliJ | Microsoft Docs"
description: Este tutorial mostra como usar o Kit de Ferramentas do Azure para IntelliJ para criar um aplicativo Web Hello World para o Azure.
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
ms.openlocfilehash: 20b2c3d86f5bde9302647f345aa99b030d78613a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="daac6-103">Criar um aplicativo Web do Azure básico no IntelliJ</span><span class="sxs-lookup"><span data-stu-id="daac6-103">Create a basic Azure web app in IntelliJ</span></span>
<span data-ttu-id="daac6-104">Este tutorial mostra como criar e implantar um aplicativo Hello World básico para o Azure como um aplicativo Web usando o [Kit de Ferramentas do Azure para IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="daac6-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a Web App by using the [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="daac6-105">Mostramos um exemplo básico de JSP para manter a simplicidade, mas, para a implantação do Azure, etapas semelhantes podem ser usadas para um servlet Java.</span><span class="sxs-lookup"><span data-stu-id="daac6-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="daac6-106">Após a conclusão deste tutorial, seu aplicativo será semelhante à ilustração a seguir quando exibido em um navegador da Web:</span><span class="sxs-lookup"><span data-stu-id="daac6-106">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Página da Web de exemplo][01]

## <a name="prerequisites"></a><span data-ttu-id="daac6-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="daac6-108">Prerequisites</span></span>
* <span data-ttu-id="daac6-109">Um JDK (Java Developer Kit) versão 1.8 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="daac6-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="daac6-110">IntelliJ IDEA Ultimate Edition.</span><span class="sxs-lookup"><span data-stu-id="daac6-110">IntelliJ IDEA Ultimate Edition.</span></span> <span data-ttu-id="daac6-111">Isso pode ser baixado de <https://www.jetbrains.com/idea/download/>.</span><span class="sxs-lookup"><span data-stu-id="daac6-111">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span></span>
* <span data-ttu-id="daac6-112">Uma distribuição de um servidor Web ou de um servidor de aplicativo baseado em Java, como o [Apache Tomcat] ou o [Jetty].</span><span class="sxs-lookup"><span data-stu-id="daac6-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="daac6-113">Uma assinatura do Azure, que pode ser adquirida em <https://azure.microsoft.com/free/> ou <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="daac6-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="daac6-114">O [Kit de Ferramentas do Azure para IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="daac6-114">The [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="daac6-115">Para saber informações sobre a instalação do Kit de ferramentas do Azure para, veja [Instalando o Kit de ferramentas do Azure para IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="daac6-115">For information about installing the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ].</span></span>

## <a name="to-create-a-hello-world-application"></a><span data-ttu-id="daac6-116">Para criar um aplicativo Hello World</span><span class="sxs-lookup"><span data-stu-id="daac6-116">To create a Hello World application</span></span>
<span data-ttu-id="daac6-117">Primeiro, vamos começar com a criação de um projeto Java.</span><span class="sxs-lookup"><span data-stu-id="daac6-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="daac6-118">Inicie o IntelliJ e clique no menu **Arquivo**, depois em **Novo** e em **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="daac6-118">Start IntelliJ and click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
    ![Arquivo Novo Projeto][02]
2. <span data-ttu-id="daac6-120">Na caixa de diálogo Novo Projeto, selecione **Java**, **Aplicativo Web** e clique em **Avançar** para adicionar um Project SDK.</span><span class="sxs-lookup"><span data-stu-id="daac6-120">In the New Project dialog box, select **Java**, then **Web Application**, and then click **New** to add a Project SDK.</span></span>
   
    ![Caixa de diálogo Novo Projeto][03a]
   
3. <span data-ttu-id="daac6-122">Na caixa de diálogo Selecionar o Diretório Base para o JDK, selecione a pasta onde o JDK está instalado e clique **OK**.</span><span class="sxs-lookup"><span data-stu-id="daac6-122">In the Select Home Directory for JDK dialog box, select the folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="daac6-123">Clique em **Avançar** na caixa de diálogo Novo Projeto para continuar.</span><span class="sxs-lookup"><span data-stu-id="daac6-123">Click **Next** in the New Project dialog box to continue.</span></span>
   
    ![Especificar o diretório base do JDK][03b]
4. <span data-ttu-id="daac6-125">Para a finalidade deste tutorial, nomeie o projeto como **Java-Web-App-On-Azure** e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="daac6-125">For purposes of this tutorial, name the project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
    ![Caixa de diálogo Novo Projeto][04]
5. <span data-ttu-id="daac6-127">Na exibição do Explorador de Projetos do IntelliJ, expanda **Java-Web-App-On-Azure**, expanda **Web** e clique duas vezes em **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="daac6-127">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
    ![Abrir Índice de Página][05c]
6. <span data-ttu-id="daac6-129">Quando o arquivo index.jsp for aberto no IntelliJ, adicione o texto para exibir dinamicamente **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="daac6-129">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="daac6-130">dentro do elemento existente `<body>`.</span><span class="sxs-lookup"><span data-stu-id="daac6-130">within the existing `<body>` element.</span></span> <span data-ttu-id="daac6-131">Seu conteúdo do `<body>` atualizado deve ser parecido com o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="daac6-131">Your updated `<body>` content should resemble the following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. <span data-ttu-id="daac6-132">Salve o index.jsp.</span><span class="sxs-lookup"><span data-stu-id="daac6-132">Save index.jsp.</span></span>

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a><span data-ttu-id="daac6-133">Para implantar seu aplicativo em um contêiner de aplicativos Web do Azure</span><span class="sxs-lookup"><span data-stu-id="daac6-133">To deploy your application to an Azure Web App Container</span></span>
<span data-ttu-id="daac6-134">Há várias maneiras pelas quais você pode implantar um aplicativo Web Java no Azure.</span><span class="sxs-lookup"><span data-stu-id="daac6-134">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="daac6-135">Este tutorial descreve uma das mais simples: o aplicativo será implantado em um contêiner de aplicativos Web do Azure, e não há a necessidade de qualquer tipo de projeto especial nem de ferramentas adicionais.</span><span class="sxs-lookup"><span data-stu-id="daac6-135">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="daac6-136">O JDK e o software do contêiner da Web serão fornecidos a você pelo Azure, portanto, não é necessário carregar seu próprio; tudo o que você precisa é de seu aplicativo Web Java.</span><span class="sxs-lookup"><span data-stu-id="daac6-136">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="daac6-137">Como resultado, o processo de publicação de seu aplicativo demorará segundos, e não minutos.</span><span class="sxs-lookup"><span data-stu-id="daac6-137">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="daac6-138">Antes de publicar seu aplicativo, você precisa definir as configurações de módulo.</span><span class="sxs-lookup"><span data-stu-id="daac6-138">Before you publish your application, you first need to configure your module settings.</span></span> <span data-ttu-id="daac6-139">Para fazer isso, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="daac6-139">To do so, use the following steps:</span></span>

1. <span data-ttu-id="daac6-140">No Explorador de Projetos do IntelliJ, clique com o botão direito do mouse no projeto **Java-Web-App-On-Azure** .</span><span class="sxs-lookup"><span data-stu-id="daac6-140">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="daac6-141">Quando o menu de contexto for exibido, clique em **Abrir Configurações do Módulo**.</span><span class="sxs-lookup"><span data-stu-id="daac6-141">When the context menu appears, click **Open Module Settings**.</span></span>

    ![Abrir configurações do módulo][05a]
2. <span data-ttu-id="daac6-143">Quando a caixa de diálogo Estrutura do Projeto aparece:</span><span class="sxs-lookup"><span data-stu-id="daac6-143">When the Project Structure dialog box appears:</span></span>

   <span data-ttu-id="daac6-144">a.</span><span class="sxs-lookup"><span data-stu-id="daac6-144">a.</span></span> <span data-ttu-id="daac6-145">Clique em **Artefatos** na lista de **Configurações do Projeto**.</span><span class="sxs-lookup"><span data-stu-id="daac6-145">Click **Artifacts** in the list of **Project Settings**.</span></span>
   <span data-ttu-id="daac6-146">b.</span><span class="sxs-lookup"><span data-stu-id="daac6-146">b.</span></span> <span data-ttu-id="daac6-147">Altere o nome do artefato na caixa **Nome** de modo que ele não contenha caracteres especiais ou espaços em branco. Isso é necessário porque o nome será usado no URI (Uniform Resource Identifier).</span><span class="sxs-lookup"><span data-stu-id="daac6-147">Change the artifact name in the **Name** box so that it doesn't contain whitespace or special characters; this is necessary since the name will be used in the Uniform Resource Identifier (URI).</span></span>
   <span data-ttu-id="daac6-148">c.</span><span class="sxs-lookup"><span data-stu-id="daac6-148">c.</span></span> <span data-ttu-id="daac6-149">Altere o **Tipo** para **Aplicativo Web: arquivo**.</span><span class="sxs-lookup"><span data-stu-id="daac6-149">Change the **Type** to **Web Application: Archive**.</span></span>
   <span data-ttu-id="daac6-150">d.</span><span class="sxs-lookup"><span data-stu-id="daac6-150">d.</span></span> <span data-ttu-id="daac6-151">Clique em **OK** para fechar a caixa de diálogo Estrutura de Projeto.</span><span class="sxs-lookup"><span data-stu-id="daac6-151">Click **OK** to close the Project Structure dialog box.</span></span>

    ![Abrir configurações do módulo][05b]

<span data-ttu-id="daac6-153">Quando você tiver definido suas configurações de módulo, poderá publicar seu aplicativo no Azure usando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="daac6-153">When you have configured your module settings, you can publish your application to Azure by using the following steps:</span></span>

1. <span data-ttu-id="daac6-154">No Explorador de Projetos do IntelliJ, clique com o botão direito do mouse no projeto **Java-Web-App-On-Azure** .</span><span class="sxs-lookup"><span data-stu-id="daac6-154">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="daac6-155">Quando o menu de contexto for exibido, selecione **Azure** e clique em **Publicar como Aplicativo Web do Azure...**</span><span class="sxs-lookup"><span data-stu-id="daac6-155">When the context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
    ![Menu de Contexto de Publicação do Azure][06]
2. <span data-ttu-id="daac6-157">Se você ainda não tiver entrado no Azure por meio do IntelliJ, será solicitada a entrada em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="daac6-157">If you have not already signed into Azure from IntelliJ, you will be prompted to sign into your Azure account.</span></span> <span data-ttu-id="daac6-158">(Se você tiver várias contas do Azure, alguns dos avisos mostrados durante o processo de entrada poderão ser exibidos mais de uma vez, mesmo se forem aparentemente os mesmos.</span><span class="sxs-lookup"><span data-stu-id="daac6-158">(If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="daac6-159">Quando isso acontecer, continue seguindo as instruções de entrada.)</span><span class="sxs-lookup"><span data-stu-id="daac6-159">When this happens, continue to follow the sign in instructions.)</span></span>
   
    ![Caixa de diálogo Login do Azure][07]
3. <span data-ttu-id="daac6-161">Após o logon bem-sucedido em sua conta do Azure, a caixa de diálogo **Gerenciar Assinaturas** exibirá uma lista de assinaturas associadas às suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="daac6-161">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="daac6-162">(Se houver várias assinaturas listadas e você quiser trabalhar com apenas um subconjunto específico, será possível desmarcar as que não deseja usar.) Depois de selecionar suas assinaturas, clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="daac6-162">(If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the subscriptions you don't want to use.) When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Gerenciar Assinaturas][08]
4. <span data-ttu-id="daac6-164">Quando a caixa de diálogo **Implantar no Contêiner do Aplicativo Web do Azure** for mostrada, ela exibirá todos os contêineres do Aplicativo Web criados anteriormente por você; se você não tiver criado nenhum contêiner, a lista estará vazia.</span><span class="sxs-lookup"><span data-stu-id="daac6-164">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
    ![Contêineres de Aplicativo][09]
5. <span data-ttu-id="daac6-166">Se você nunca tiver criado um contêiner de aplicativos Web do Azure, ou se quiser publicar seu aplicativo em um novo contêiner, use as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="daac6-166">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="daac6-167">Caso contrário, selecione um Contêiner de Aplicativo Web existente e pule para a etapa 6 abaixo.</span><span class="sxs-lookup"><span data-stu-id="daac6-167">Otherwise, select an existing Web App Container and skip to step 6 below.</span></span>
   
   1. <span data-ttu-id="daac6-168">Clique em **+**</span><span class="sxs-lookup"><span data-stu-id="daac6-168">Click **+**</span></span>
      
       ![Adicionar Contêiner de Aplicativo][10]
   2. <span data-ttu-id="daac6-170">A caixa de diálogo **Novo Contêiner de Aplicativo Web** será exibida e será usada nas próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="daac6-170">The **New Web App Container** dialog box will be displayed, which will be used for the next several steps.</span></span>
      
       ![Novo Contêiner de Aplicativo][11a]
   3. <span data-ttu-id="daac6-172">Insira um **Rótulo DNS** para seu Contêiner do Aplicativo Web; isso formará o rótulo DNS folha da URL do host de seu aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="daac6-172">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="daac6-173">Observe que o nome deve estar disponível e de acordo com os requisitos de nomenclatura de aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="daac6-173">Note that the name must be available and conform to Azure Web App naming requirements.</span></span>
   4. <span data-ttu-id="daac6-174">No menu suspenso **Contêiner da Web** , selecione o software apropriado ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="daac6-174">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
       <span data-ttu-id="daac6-175">No momento, você pode escolher entre o Tomcat 8, Tomcat 7 ou Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="daac6-175">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="daac6-176">Uma distribuição recente do software selecionado será fornecida pelo Azure e ele será executado em uma distribuição recente do JDK 8 criado pela Oracle e fornecido pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="daac6-176">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="daac6-177">No menu suspenso **Assinatura** , selecione a assinatura que deseja usar para essa implantação.</span><span class="sxs-lookup"><span data-stu-id="daac6-177">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>
   6. <span data-ttu-id="daac6-178">No menu suspenso **Grupo de Recursos** , selecione o Grupo de Recursos com o qual deseja associar seu Aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="daac6-178">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="daac6-179">(Os Grupos de Recursos do Azure lhe permitem agrupar recursos relacionados para que, por exemplo, possam ser excluídos juntos.)</span><span class="sxs-lookup"><span data-stu-id="daac6-179">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="daac6-180">Você pode selecionar um Grupo de Recursos existente (se houver) e ignorar a etapa g abaixo ou usar as seguintes etapas para criar um novo Grupo de Recursos:</span><span class="sxs-lookup"><span data-stu-id="daac6-180">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="daac6-181">Selecione **&lt;&lt; Criar novo grupo de recursos &gt;&gt;** no menu suspenso **Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="daac6-181">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in the **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="daac6-182">A caixa de diálogo **Novo Grupo de Recursos** será exibida:</span><span class="sxs-lookup"><span data-stu-id="daac6-182">The **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Novo grupo de recursos][12]
      * <span data-ttu-id="daac6-184">Na caixa de texto **Nome** , especifique um nome para o novo Grupo de Recursos.</span><span class="sxs-lookup"><span data-stu-id="daac6-184">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="daac6-185">No menu suspenso **Região** , selecione a localização do data center do Azure apropriada ao Grupo de Recursos.</span><span class="sxs-lookup"><span data-stu-id="daac6-185">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="daac6-186">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="daac6-186">Click **OK**.</span></span>
   7. <span data-ttu-id="daac6-187">O menu suspenso **Plano do Serviço de Aplicativo** lista os planos do serviço de aplicativo associados ao Grupo de Recursos selecionado.</span><span class="sxs-lookup"><span data-stu-id="daac6-187">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="daac6-188">(Um Plano do Serviço de Aplicativo especifica informações como o local de seu Aplicativo Web, o tipo de preço e o tamanho da instância de computação.</span><span class="sxs-lookup"><span data-stu-id="daac6-188">(An App Service Plan specifies information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="daac6-189">Um único Plano do Serviço de Aplicativo pode ser usado para vários Aplicativos Web, por isso, ele é mantido separadamente de uma implantação de Aplicativo Web específica.)</span><span class="sxs-lookup"><span data-stu-id="daac6-189">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="daac6-190">Você pode selecionar um Plano do Serviço de Aplicativo existente (se houver) e ignorar a etapa h abaixo ou usar as seguintes etapas para criar um novo Plano do Serviço de Aplicativo:</span><span class="sxs-lookup"><span data-stu-id="daac6-190">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="daac6-191">Selecione **&lt;&lt; Criar novo plano do Serviço de Aplicativo &gt;&gt;** no menu suspenso **Plano do Serviço de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="daac6-191">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in the **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="daac6-192">A caixa de diálogo **Novo Plano do Serviço de Aplicativo** será exibida:</span><span class="sxs-lookup"><span data-stu-id="daac6-192">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Novo Plano do Serviço de Aplicativo][13]
      * <span data-ttu-id="daac6-194">Na caixa de texto **Nome** , especifique um nome para o novo Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="daac6-194">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="daac6-195">No menu suspenso **Localização** , selecione a localização do data center do Azure apropriada ao plano.</span><span class="sxs-lookup"><span data-stu-id="daac6-195">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="daac6-196">No menu suspenso **Tipo de Preço** , selecione o preço apropriado ao plano.</span><span class="sxs-lookup"><span data-stu-id="daac6-196">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="daac6-197">Para fins de teste, é possível escolher **Gratuito**.</span><span class="sxs-lookup"><span data-stu-id="daac6-197">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="daac6-198">No menu suspenso **Tamanho da Instância** , selecione o tamanho de instância apropriado ao plano.</span><span class="sxs-lookup"><span data-stu-id="daac6-198">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="daac6-199">Para fins de teste, é possível escolher **Pequeno**.</span><span class="sxs-lookup"><span data-stu-id="daac6-199">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="daac6-200">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="daac6-200">Click **OK**.</span></span>
   8. <span data-ttu-id="daac6-201">(Opcional) Por padrão, uma distribuição recente de Java 8 será implantada automaticamente como sua JVM pelo Azure no contêiner do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="daac6-201">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure to your web app container.</span></span> <span data-ttu-id="daac6-202">No entanto, você pode selecionar uma versão diferente e uma distribuição da JVM.</span><span class="sxs-lookup"><span data-stu-id="daac6-202">However, you can select a different version and distribution of the JVM.</span></span> <span data-ttu-id="daac6-203">Para fazer isso, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="daac6-203">To do so, use the following steps:</span></span>
      
      * <span data-ttu-id="daac6-204">Clique na guia **JDK** na caixa de diálogo **Novo Contêiner do Aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="daac6-204">Click the **JDK** tab in the **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="daac6-205">Você pode escolher entre uma das duas seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="daac6-205">You can choose from one of the following options:</span></span>
        
        * <span data-ttu-id="daac6-206">Implantar o JDK padrão, que é oferecido pelo Azure</span><span class="sxs-lookup"><span data-stu-id="daac6-206">Deploy the default JDK which is offered by Azure</span></span>
        * <span data-ttu-id="daac6-207">Implantar um JDK de terceiros de uma lista suspensa de JDKs adicionais que estão disponíveis no Azure</span><span class="sxs-lookup"><span data-stu-id="daac6-207">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
        * <span data-ttu-id="daac6-208">Implantar um JDK personalizado, que deve ser empacotado como um arquivo ZIP e ser publicamente disponível ou em sua conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="daac6-208">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
        ![Guia Novo JDK de Contêiner de Aplicativo][11b]
   9. <span data-ttu-id="daac6-210">Depois de concluir todas as etapas acima, a caixa de diálogo New Web App Container (Novo Contêiner de Aplicativos Web) deve ser semelhante à ilustração a seguir:</span><span class="sxs-lookup"><span data-stu-id="daac6-210">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
       ![Novo Contêiner de Aplicativo][14]
   10. <span data-ttu-id="daac6-212">Clique em **OK** para concluir a criação do novo contêiner do Aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="daac6-212">Click **OK** to complete the creation of your new Web App container.</span></span>
       
        <span data-ttu-id="daac6-213">Aguarde alguns segundos para a lista de contêineres de Aplicativo Web ser atualizada. O contêiner do aplicativo Web recém-criado agora deve ser selecionado na lista.</span><span class="sxs-lookup"><span data-stu-id="daac6-213">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>
6. <span data-ttu-id="daac6-214">Agora você está pronto para concluir a implantação inicial do seu aplicativo Web no Azure. Clique em **OK** para implantar seu aplicativo Java no contêiner do aplicativo Web selecionado.</span><span class="sxs-lookup"><span data-stu-id="daac6-214">You are now ready to complete the initial deployment of your Web App to Azure; click **OK** to deploy your Java application to the selected Web App container.</span></span> <span data-ttu-id="daac6-215">Por padrão, o aplicativo será implantado como um subdiretório do servidor de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="daac6-215">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="daac6-216">Se desejar implantá-lo como o aplicativo raiz, marque a caixa de seleção **Implantar na raiz** antes de clicar em **OK**.</span><span class="sxs-lookup"><span data-stu-id="daac6-216">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
   
    ![Implantar no Azure][15]
7. <span data-ttu-id="daac6-218">Em seguida, você deverá ver o modo de exibição do **Log de Atividades do Azure** , que indicará o status da implantação de seu Aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="daac6-218">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
    ![Indicador de Progresso][16]
   
    <span data-ttu-id="daac6-220">O processo de implantação de seu aplicativo Web no Azure deve demorar apenas alguns segundos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="daac6-220">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="daac6-221">Quando seu aplicativo estiver pronto, você verá um link chamado **Publicada** in the **Status** .</span><span class="sxs-lookup"><span data-stu-id="daac6-221">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="daac6-222">Quando você clicar no link, ele o levará à página inicial do seu aplicativo Web implantado, ou você pode usar as etapas da seção a seguir para navegar até o seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="daac6-222">When you click the link, it will take you to your deployed Web App's home page, or you can use the steps in the following section to browse to your web app.</span></span>

## <a name="browsing-to-your-web-app-on-azure"></a><span data-ttu-id="daac6-223">Navegando até seu aplicativo Web no Azure</span><span class="sxs-lookup"><span data-stu-id="daac6-223">Browsing to your Web App on Azure</span></span>
<span data-ttu-id="daac6-224">Para navegar até o aplicativo Web no Azure, você poderá usar o modo de exibição do **Azure Explorer** .</span><span class="sxs-lookup"><span data-stu-id="daac6-224">To browse to your Web App on Azure, you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="daac6-225">Se o modo de exibição do **Azure Explorer** ainda não estiver aberto, você poderá abri-lo clicando no menu **Exibir** no IntelliJ, clicando em **Janelas de Ferramentas** e em **Service Explorer**.</span><span class="sxs-lookup"><span data-stu-id="daac6-225">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="daac6-226">Se você não tiver feito logon anteriormente, receberá uma solicitação para fazê-lo.</span><span class="sxs-lookup"><span data-stu-id="daac6-226">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="daac6-227">Quando o modo de exibição do **Azure Explorer** for exibido, use estas etapas para navegar pelo aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="daac6-227">When the **Azure Explorer** view is displayed, use follow these steps to browse to your Web App:</span></span> 

1. <span data-ttu-id="daac6-228">Expanda o nó **Azure** .</span><span class="sxs-lookup"><span data-stu-id="daac6-228">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="daac6-229">Expanda o nó **Aplicativos Web** .</span><span class="sxs-lookup"><span data-stu-id="daac6-229">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="daac6-230">Clique com botão direito do mouse no Aplicativo Web desejado.</span><span class="sxs-lookup"><span data-stu-id="daac6-230">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="daac6-231">Quando o menu de contexto for exibido, clique em **Abrir no Navegador**.</span><span class="sxs-lookup"><span data-stu-id="daac6-231">When the context menu appears, click **Open in Browser**.</span></span>
   
    ![Procurar o Aplicativo Web][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="daac6-233">Atualizando seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="daac6-233">Updating your web app</span></span>
<span data-ttu-id="daac6-234">A atualização de um aplicativo Web do Azure em execução é um processo rápido e fácil, e você tem duas opções de atualização:</span><span class="sxs-lookup"><span data-stu-id="daac6-234">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="daac6-235">Você pode atualizar a implantação de um aplicativo Web Java existente.</span><span class="sxs-lookup"><span data-stu-id="daac6-235">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="daac6-236">Você pode publicar um aplicativo Java adicional no mesmo contêiner de aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="daac6-236">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="daac6-237">Em ambos os casos, o processo é idêntico e demora apenas alguns segundos:</span><span class="sxs-lookup"><span data-stu-id="daac6-237">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="daac6-238">No explorador de projetos do IntelliJ, clique com o botão direito do mouse no aplicativo Java que você deseja atualizar ou adicionar a um contêiner de aplicativos Web existente.</span><span class="sxs-lookup"><span data-stu-id="daac6-238">In the IntelliJ project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="daac6-239">Quando o menu de contexto for exibido, selecione **Azure** e, em seguida, **Publicar como Aplicativo Web do Azure...**</span><span class="sxs-lookup"><span data-stu-id="daac6-239">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="daac6-240">Como você já fez logon anteriormente, verá uma lista com seus contêineres de aplicativo Web existentes.</span><span class="sxs-lookup"><span data-stu-id="daac6-240">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="daac6-241">Selecione aquele no qual deseja publicar ou publicar novamente o aplicativo Java e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="daac6-241">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="daac6-242">Após alguns segundos, o modo de exibição do **Log de Atividades do Azure** mostrará a implantação atualizada como **Publicada** e será possível verificar o aplicativo atualizado em um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="daac6-242">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="daac6-243">Iniciar, parar ou reiniciar o aplicativo Web existente</span><span class="sxs-lookup"><span data-stu-id="daac6-243">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="daac6-244">Para iniciar ou parar um contêiner do Aplicativo Web do Azure existente, (incluindo todos os aplicativos Java implantados nele), é possível usar o modo de exibição do **Azure Explorer** .</span><span class="sxs-lookup"><span data-stu-id="daac6-244">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="daac6-245">Se o modo de exibição do **Azure Explorer** ainda não estiver aberto, você poderá abri-lo clicando no menu **Exibir** no IntelliJ, clicando em **Janelas de Ferramentas** e em **Service Explorer**.</span><span class="sxs-lookup"><span data-stu-id="daac6-245">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="daac6-246">Se você não tiver feito logon anteriormente, receberá uma solicitação para fazê-lo.</span><span class="sxs-lookup"><span data-stu-id="daac6-246">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="daac6-247">Quando o modo de exibição do **Azure Explorer** for exibido, use estas etapas para iniciar ou parar o Aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="daac6-247">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="daac6-248">Expanda o nó **Azure** .</span><span class="sxs-lookup"><span data-stu-id="daac6-248">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="daac6-249">Expanda o nó **Aplicativos Web** .</span><span class="sxs-lookup"><span data-stu-id="daac6-249">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="daac6-250">Clique com botão direito do mouse no Aplicativo Web desejado.</span><span class="sxs-lookup"><span data-stu-id="daac6-250">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="daac6-251">Quando o menu de contexto for exibido, clique em **Iniciar**, **Parar** ou **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="daac6-251">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="daac6-252">Observe que as opções de menu são sensíveis ao contexto, para que você só possa parar um aplicativo Web que esteja em execução ou iniciar um aplicativo Web que não esteja em execução no momento.</span><span class="sxs-lookup"><span data-stu-id="daac6-252">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Parar Aplicativo Web][18]

## <a name="next-steps"></a><span data-ttu-id="daac6-254">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="daac6-254">Next Steps</span></span>
<span data-ttu-id="daac6-255">Para obter mais informações sobre os kits de ferramentas do Azure para Java IDEs, confira os links a seguir:</span><span class="sxs-lookup"><span data-stu-id="daac6-255">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="daac6-256">[Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="daac6-256">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="daac6-257">[Instalação do Kit de Ferramentas do Azure para o Eclipse]</span><span class="sxs-lookup"><span data-stu-id="daac6-257">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="daac6-258">[Criar um aplicativo Web Hello World para o Azure no Eclipse]</span><span class="sxs-lookup"><span data-stu-id="daac6-258">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="daac6-259">[Novidades no Kit de Ferramentas do Azure para o Eclipse]</span><span class="sxs-lookup"><span data-stu-id="daac6-259">[What's New in the Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="daac6-260">[Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="daac6-260">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="daac6-261">[Instalando o Kit de ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="daac6-261">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="daac6-262">*Criar um aplicativo Web Hello World para o Azure no IntelliJ (este artigo)*</span><span class="sxs-lookup"><span data-stu-id="daac6-262">*Create a Hello World Web App for Azure in IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="daac6-263">[Novidades no Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="daac6-263">[What's New in the Azure Toolkit for IntelliJ]</span></span>

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="daac6-264">Consulte também</span><span class="sxs-lookup"><span data-stu-id="daac6-264">See Also</span></span>
<span data-ttu-id="daac6-265">Para obter mais informações sobre como usar o Azure com o Java, confira a [Central de desenvolvimento Java do Azure].</span><span class="sxs-lookup"><span data-stu-id="daac6-265">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<span data-ttu-id="daac6-266">Para obter mais informações sobre como criar aplicativos Web do Azure, confira a [Visão geral de Aplicativos Web].</span><span class="sxs-lookup"><span data-stu-id="daac6-266">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Kit de ferramentas do Azure para Eclipse]: ../azure-toolkit-for-eclipse.md
[Kit de Ferramentas do Azure para IntelliJ]: ../azure-toolkit-for-intellij.md
[Criar um aplicativo Web Hello World para o Azure no Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Instalação do Kit de Ferramentas do Azure para o Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[Instalando o Kit de ferramentas do Azure para IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Novidades no Kit de Ferramentas do Azure para o Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md
[Novidades no Kit de Ferramentas do Azure para IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[Central de desenvolvimento Java do Azure]: https://azure.microsoft.com/develop/java/
[Visão geral de Aplicativos Web]: ./app-service-web-overview.md
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
