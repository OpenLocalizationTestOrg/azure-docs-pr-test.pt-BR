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
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="0e8ba-103">Criar um aplicativo Web do Azure básico no IntelliJ</span><span class="sxs-lookup"><span data-stu-id="0e8ba-103">Create a basic Azure web app in IntelliJ</span></span>
<span data-ttu-id="0e8ba-104">Este tutorial mostra como toocreate e implantar um tooAzure de aplicativo Hello World básica como um aplicativo Web usando Olá [Kit de ferramentas do Azure para IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="0e8ba-104">This tutorial shows how toocreate and deploy a basic Hello World application tooAzure as a Web App by using hello [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="0e8ba-105">Mostramos um exemplo básico de JSP para manter a simplicidade, mas, para a implantação do Azure, etapas semelhantes podem ser usadas para um servlet Java.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="0e8ba-106">Quando você concluiu este tutorial, o aplicativo ficará semelhante toohello ilustração a seguir quando você exibi-lo em um navegador da web:</span><span class="sxs-lookup"><span data-stu-id="0e8ba-106">When you have completed this tutorial, your application will look similar toohello following illustration when you view it in a web browser:</span></span>

![Página da Web de exemplo][01]

## <a name="prerequisites"></a><span data-ttu-id="0e8ba-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0e8ba-108">Prerequisites</span></span>
* <span data-ttu-id="0e8ba-109">Um JDK (Java Developer Kit) versão 1.8 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="0e8ba-110">IntelliJ IDEA Ultimate Edition.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-110">IntelliJ IDEA Ultimate Edition.</span></span> <span data-ttu-id="0e8ba-111">Isso pode ser baixado de <https://www.jetbrains.com/idea/download/>.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-111">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span></span>
* <span data-ttu-id="0e8ba-112">Uma distribuição de um servidor Web ou de um servidor de aplicativo baseado em Java, como o [Apache Tomcat] ou o [Jetty].</span><span class="sxs-lookup"><span data-stu-id="0e8ba-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="0e8ba-113">Uma assinatura do Azure, que pode ser adquirida em <https://azure.microsoft.com/free/> ou <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="0e8ba-114">Olá [Kit de ferramentas do Azure para IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="0e8ba-114">hello [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="0e8ba-115">Para obter informações sobre como instalar Olá Kit de ferramentas do Azure, consulte [Olá instalando o Kit de ferramentas do Azure para IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="0e8ba-115">For information about installing hello Azure Toolkit, see [Installing hello Azure Toolkit for IntelliJ].</span></span>

## <a name="toocreate-a-hello-world-application"></a><span data-ttu-id="0e8ba-116">toocreate um aplicativo Hello World</span><span class="sxs-lookup"><span data-stu-id="0e8ba-116">toocreate a Hello World application</span></span>
<span data-ttu-id="0e8ba-117">Primeiro, vamos começar com a criação de um projeto Java.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="0e8ba-118">Iniciar IntelliJ e clique em Olá **arquivo** menu, clique em **novo**e, em seguida, clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-118">Start IntelliJ and click hello **File** menu, then click **New**, and then click **Project**.</span></span>
   
    ![Arquivo Novo Projeto][02]
2. <span data-ttu-id="0e8ba-120">Na caixa de diálogo Novo projeto hello, selecione **Java**, em seguida, **aplicativo Web**e, em seguida, clique em **novo** tooadd um SDK de projeto.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-120">In hello New Project dialog box, select **Java**, then **Web Application**, and then click **New** tooadd a Project SDK.</span></span>
   
    ![Caixa de diálogo Novo Projeto][03a]
   
3. <span data-ttu-id="0e8ba-122">Em hello Selecionar diretório base para a caixa de diálogo do JDK, selecione Olá pasta onde o seu JDK está instalado e clique **Okey**.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-122">In hello Select Home Directory for JDK dialog box, select hello folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="0e8ba-123">Clique em **próximo** em Olá toocontinue de caixa de diálogo de novo projeto.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-123">Click **Next** in hello New Project dialog box toocontinue.</span></span>
   
    ![Especificar o diretório base do JDK][03b]
4. <span data-ttu-id="0e8ba-125">Para fins deste tutorial, nomeie o projeto de saudação **Java aplicativo Web no Azure**e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-125">For purposes of this tutorial, name hello project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
    ![Caixa de diálogo Novo Projeto][04]
5. <span data-ttu-id="0e8ba-127">Na exibição do Explorador de Projetos do IntelliJ, expanda **Java-Web-App-On-Azure**, expanda **Web** e clique duas vezes em **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-127">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
    ![Abrir Índice de Página][05c]
6. <span data-ttu-id="0e8ba-129">Quando o arquivo index.jsp for aberto no IntelliJ, adicionar na exibição do texto toodynamically **Olá, mundo!**</span><span class="sxs-lookup"><span data-stu-id="0e8ba-129">When your index.jsp file opens in IntelliJ, add in text toodynamically display **Hello World!**</span></span> <span data-ttu-id="0e8ba-130">dentro de saudação existente `<body>` elemento.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-130">within hello existing `<body>` element.</span></span> <span data-ttu-id="0e8ba-131">Seu atualizada `<body>` conteúdo deve ser semelhante a saudação de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="0e8ba-131">Your updated `<body>` content should resemble hello following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. <span data-ttu-id="0e8ba-132">Salve o index.jsp.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-132">Save index.jsp.</span></span>

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a><span data-ttu-id="0e8ba-133">toodeploy tooan seu aplicativo recipiente de aplicativo da Web do Azure</span><span class="sxs-lookup"><span data-stu-id="0e8ba-133">toodeploy your application tooan Azure Web App Container</span></span>
<span data-ttu-id="0e8ba-134">Há várias maneiras pelas quais você pode implantar um tooAzure de aplicativo web Java.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-134">There are several ways by which you can deploy a Java web application tooAzure.</span></span> <span data-ttu-id="0e8ba-135">Este tutorial descreve uma saudação mais simples: o aplicativo será implantado tooan contêiner de aplicativo Web do Azure – nenhum tipo de projeto especial nem ferramentas adicionais são necessárias.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-135">This tutorial describes one of hello simplest: your application will be deployed tooan Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="0e8ba-136">Olá Olá JDK e o software da web que contêiner será fornecido para você pelo Azure, portanto não há nenhuma necessidade tooupload seu próprios; tudo o que você precisa é de seu aplicativo da Web de Java.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-136">hello JDK and hello web container software will be provided for you by Azure, so there is no need tooupload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="0e8ba-137">Como resultado, o processo de publicação de saudação para seu aplicativo levará segundos, minutos não.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-137">As a result, hello publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="0e8ba-138">Antes de publicar seu aplicativo, é necessário primeiro tooconfigure suas configurações de módulo.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-138">Before you publish your application, you first need tooconfigure your module settings.</span></span> <span data-ttu-id="0e8ba-139">Assim, o toodo use Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0e8ba-139">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="0e8ba-140">No Explorador de projeto do IntelliJ, clique com botão direito Olá **Java aplicativo Web no Azure** projeto.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-140">In IntelliJ's Project Explorer, right-click hello **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="0e8ba-141">Quando o menu de contexto Olá for exibida, clique em **abrir configurações de módulo**.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-141">When hello context menu appears, click **Open Module Settings**.</span></span>

    ![Abrir configurações do módulo][05a]
2. <span data-ttu-id="0e8ba-143">Quando for exibida a caixa de diálogo Olá estrutura do projeto:</span><span class="sxs-lookup"><span data-stu-id="0e8ba-143">When hello Project Structure dialog box appears:</span></span>

   <span data-ttu-id="0e8ba-144">a.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-144">a.</span></span> <span data-ttu-id="0e8ba-145">Clique em **artefatos** na lista de saudação do **configurações de projeto**.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-145">Click **Artifacts** in hello list of **Project Settings**.</span></span>
   <span data-ttu-id="0e8ba-146">b.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-146">b.</span></span> <span data-ttu-id="0e8ba-147">Alterar nome do artefato Olá no hello **nome** caixa para que ele não contém espaço em branco ou caracteres especiais; isso é necessário pois Olá nome será usado em Olá identificador de recurso uniforme (URI).</span><span class="sxs-lookup"><span data-stu-id="0e8ba-147">Change hello artifact name in hello **Name** box so that it doesn't contain whitespace or special characters; this is necessary since hello name will be used in hello Uniform Resource Identifier (URI).</span></span>
   <span data-ttu-id="0e8ba-148">c.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-148">c.</span></span> <span data-ttu-id="0e8ba-149">Saudação de alteração **tipo** muito**aplicativo Web: arquivo**.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-149">Change hello **Type** too**Web Application: Archive**.</span></span>
   <span data-ttu-id="0e8ba-150">d.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-150">d.</span></span> <span data-ttu-id="0e8ba-151">Clique em **Okey** caixa de diálogo tooclose Olá estrutura do projeto.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-151">Click **OK** tooclose hello Project Structure dialog box.</span></span>

    ![Abrir configurações do módulo][05b]

<span data-ttu-id="0e8ba-153">Quando você tiver configurado as definições de módulo, você pode publicar seu aplicativo tooAzure usando Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0e8ba-153">When you have configured your module settings, you can publish your application tooAzure by using hello following steps:</span></span>

1. <span data-ttu-id="0e8ba-154">No Explorador de projeto do IntelliJ, clique com botão direito Olá **Java aplicativo Web no Azure** projeto.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-154">In IntelliJ's Project Explorer, right-click hello **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="0e8ba-155">Quando o menu de contexto Olá for exibida, selecione **Azure**e, em seguida, clique em **Publicar como um aplicativo Web do Azure...**</span><span class="sxs-lookup"><span data-stu-id="0e8ba-155">When hello context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
    ![Menu de Contexto de Publicação do Azure][06]
2. <span data-ttu-id="0e8ba-157">Se você tiver não tiver entrado no Azure de IntelliJ, será solicitada toosign em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-157">If you have not already signed into Azure from IntelliJ, you will be prompted toosign into your Azure account.</span></span> <span data-ttu-id="0e8ba-158">(Se você tiver várias contas do Azure, alguns dos prompts de saudação durante o processo de entrada hello podem ser mostradas mais de uma vez, mesmo se eles parecem toobe Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-158">(If you have multiple Azure accounts, some of hello prompts during hello sign in process may be shown more than once, even if they appear toobe hello same.</span></span> <span data-ttu-id="0e8ba-159">Quando isso acontece, continuar toofollow Olá sinal instruções).</span><span class="sxs-lookup"><span data-stu-id="0e8ba-159">When this happens, continue toofollow hello sign in instructions.)</span></span>
   
    ![Caixa de diálogo Login do Azure][07]
3. <span data-ttu-id="0e8ba-161">Depois de ter entrado com êxito em sua conta do Azure, Olá **gerenciar assinaturas** caixa de diálogo exibirá uma lista de assinaturas que estão associados com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-161">After you have successfully signed into your Azure account, hello **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="0e8ba-162">(Se houver várias assinaturas listadas e você desejar toowork com apenas um subconjunto específico de-los, opcionalmente pode desmarcar Olá assinaturas que não toouse.) Depois de selecionar suas assinaturas, clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-162">(If there are multiple subscriptions listed and you want toowork with only a specific subset of them, you may optionally uncheck hello subscriptions you don't want toouse.) When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Gerenciar Assinaturas][08]
4. <span data-ttu-id="0e8ba-164">Olá quando **implantar tooAzure contêiner de aplicativo da Web** caixa de diálogo for exibida, ele exibirá qualquer contêiner de aplicativo Web que você criou anteriormente; se você não criou qualquer contêiner, a lista de saudação estará vazia.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-164">When hello **Deploy tooAzure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, hello list will be empty.</span></span>
   
    ![Contêineres de Aplicativo][09]
5. <span data-ttu-id="0e8ba-166">Se você não criou um contêiner de aplicativo Web do Azure antes, ou se você gostaria que toopublish seu aplicativo tooa novo contêiner, use Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-166">If you have not created an Azure Web App Container before, or if you would like toopublish your application tooa new container, use hello following steps.</span></span> <span data-ttu-id="0e8ba-167">Caso contrário, selecione um contêiner do aplicativo Web existente e ignorar toostep 6 abaixo.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-167">Otherwise, select an existing Web App Container and skip toostep 6 below.</span></span>
   
   1. <span data-ttu-id="0e8ba-168">Clique em **+**</span><span class="sxs-lookup"><span data-stu-id="0e8ba-168">Click **+**</span></span>
      
       ![Adicionar Contêiner de Aplicativo][10]
   2. <span data-ttu-id="0e8ba-170">Olá **novo contêiner de aplicativo Web** caixa de diálogo será exibida, que será usado para Olá lado várias etapas.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-170">hello **New Web App Container** dialog box will be displayed, which will be used for hello next several steps.</span></span>
      
       ![Novo Contêiner de Aplicativo][11a]
   3. <span data-ttu-id="0e8ba-172">Insira um **rótulo DNS** para seu contêiner de aplicativo da Web; isso formarão o rótulo DNS Olá folha da URL de host Olá para o aplicativo web no Azure.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-172">Enter a **DNS Label** for your Web App Container; this will form hello leaf DNS label of hello host URL for your web application in Azure.</span></span> <span data-ttu-id="0e8ba-173">Observe que esse nome hello deve estar disponível e está de acordo com requisitos de nomenclatura de aplicativo Web tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-173">Note that hello name must be available and conform tooAzure Web App naming requirements.</span></span>
   4. <span data-ttu-id="0e8ba-174">Em Olá **contêiner da Web** menu suspenso, selecione Olá o software apropriado para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-174">In hello **Web Container** drop-down menu, select hello appropriate software for your application.</span></span>
      
       <span data-ttu-id="0e8ba-175">No momento, você pode escolher entre o Tomcat 8, Tomcat 7 ou Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-175">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="0e8ba-176">Uma distribuição recente do software de saudação selecionada será fornecida pelo Azure e ele será executado em uma distribuição recente do JDK 8 criado pela Oracle e fornecido pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-176">A recent distribution of hello selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="0e8ba-177">Em Olá **assinatura** menu suspenso, assinatura selecione Olá deseja toouse para essa implantação.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-177">In hello **Subscription** drop-down menu, select hello subscription you want toouse for this deployment.</span></span>
   6. <span data-ttu-id="0e8ba-178">Em Olá **grupo de recursos** menu suspenso, selecione Olá grupo de recursos com o qual você deseja tooassociate seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-178">In hello **Resource Group** drop-down menu, select hello Resource Group with which you want tooassociate your Web App.</span></span> <span data-ttu-id="0e8ba-179">(Grupos de recursos do azure permite que você toogroup recursos relacionados juntos para que, por exemplo, pode ser excluídos em conjunto.)</span><span class="sxs-lookup"><span data-stu-id="0e8ba-179">(Azure Resource Groups allow you toogroup related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="0e8ba-180">Você pode selecionar um grupo de recursos existente (se houver) e ignorar toostep g abaixo ou use Olá seguir etapas toocreate um novo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="0e8ba-180">You can select an existing Resource Group (if you have any) and skip toostep g below, or use hello following steps toocreate a new Resource Group:</span></span>
      
      * <span data-ttu-id="0e8ba-181">Selecione  **&lt; &lt; criar novo grupo de recursos &gt; &gt;**  em Olá **grupo de recursos** menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-181">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in hello **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="0e8ba-182">Olá **novo grupo de recursos** caixa de diálogo será exibida:</span><span class="sxs-lookup"><span data-stu-id="0e8ba-182">hello **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Novo grupo de recursos][12]
      * <span data-ttu-id="0e8ba-184">Em Olá Olá **nome** caixa de texto, especifique um nome para seu novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-184">In hello hello **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="0e8ba-185">Em Olá Olá **região** menu suspenso, selecione Olá apropriado do Azure Datacenter local para seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-185">In hello hello **Region** drop-down menu, select hello appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="0e8ba-186">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-186">Click **OK**.</span></span>
   7. <span data-ttu-id="0e8ba-187">Olá **plano do serviço de aplicativo** menu suspenso lista planos de serviço de aplicativo hello que estão associados a saudação grupo de recursos que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-187">hello **App Service Plan** drop-down menu lists hello app service plans that are associated with hello Resource Group that you selected.</span></span> <span data-ttu-id="0e8ba-188">(Um plano de serviço de aplicativo especifica informações como a localização de saudação do seu aplicativo Web, Olá tipo de preço e tamanho de instância de computação hello.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-188">(An App Service Plan specifies information such as hello location of your Web App, hello pricing tier and hello compute instance size.</span></span> <span data-ttu-id="0e8ba-189">Um único Plano do Serviço de Aplicativo pode ser usado para vários Aplicativos Web, por isso, ele é mantido separadamente de uma implantação de Aplicativo Web específica.)</span><span class="sxs-lookup"><span data-stu-id="0e8ba-189">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="0e8ba-190">Você pode selecionar um plano de serviço de aplicativo existente (se houver) e ignorar toostep h abaixo, ou usar Olá toocreate etapas um novo plano de serviço de aplicativo a seguir:</span><span class="sxs-lookup"><span data-stu-id="0e8ba-190">You can select an existing App Service Plan (if you have any) and skip toostep h below, or use hello following steps toocreate a new App Service Plan:</span></span>
      
      * <span data-ttu-id="0e8ba-191">Selecione  **&lt; &lt; criar novo plano de serviço de aplicativo &gt; &gt;**  em Olá **plano do serviço de aplicativo** menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-191">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in hello **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="0e8ba-192">Olá **novo plano de serviço de aplicativo** caixa de diálogo será exibida:</span><span class="sxs-lookup"><span data-stu-id="0e8ba-192">hello **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Novo Plano do Serviço de Aplicativo][13]
      * <span data-ttu-id="0e8ba-194">Em Olá Olá **nome** caixa de texto, especifique um nome para o novo plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-194">In hello hello **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="0e8ba-195">Em Olá Olá **local** menu suspenso, selecione Olá apropriado do Azure Datacenter local para o plano de saudação.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-195">In hello hello **Location** drop-down menu, select hello appropriate Azure data center location for hello plan.</span></span>
      * <span data-ttu-id="0e8ba-196">Em Olá Olá **preço** menu suspenso, selecione Olá apropriado de preços para o plano de saudação.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-196">In hello hello **Pricing Tier** drop-down menu, select hello appropriate pricing for hello plan.</span></span> <span data-ttu-id="0e8ba-197">Para fins de teste, é possível escolher **Gratuito**.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-197">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="0e8ba-198">Em Olá Olá **tamanho da instância** menu suspenso, o tamanho de instância apropriada do hello selecione plano hello.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-198">In hello hello **Instance Size** drop-down menu, select hello appropriate instance size for hello plan.</span></span> <span data-ttu-id="0e8ba-199">Para fins de teste, é possível escolher **Pequeno**.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-199">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="0e8ba-200">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-200">Click **OK**.</span></span>
   8. <span data-ttu-id="0e8ba-201">(Opcional) Por padrão, uma distribuição recente de Java 8 será implantada automaticamente como sua JVM pelo contêiner de aplicativo da web tooyour do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-201">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure tooyour web app container.</span></span> <span data-ttu-id="0e8ba-202">No entanto, você pode selecionar uma versão diferente e a distribuição de saudação da JVM.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-202">However, you can select a different version and distribution of hello JVM.</span></span> <span data-ttu-id="0e8ba-203">Assim, o toodo use Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0e8ba-203">toodo so, use hello following steps:</span></span>
      
      * <span data-ttu-id="0e8ba-204">Clique em Olá **JDK** guia Olá **novo contêiner de aplicativo Web** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-204">Click hello **JDK** tab in hello **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="0e8ba-205">Você pode escolher uma saudação as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="0e8ba-205">You can choose from one of hello following options:</span></span>
        
        * <span data-ttu-id="0e8ba-206">Implantar o padrão de saudação JDK oferecido pelo Azure</span><span class="sxs-lookup"><span data-stu-id="0e8ba-206">Deploy hello default JDK which is offered by Azure</span></span>
        * <span data-ttu-id="0e8ba-207">Implantar um JDK de terceiros de uma lista suspensa de JDKs adicionais que estão disponíveis no Azure</span><span class="sxs-lookup"><span data-stu-id="0e8ba-207">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
        * <span data-ttu-id="0e8ba-208">Implantar um JDK personalizado, que deve ser empacotado como um arquivo ZIP e ser publicamente disponível ou em sua conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="0e8ba-208">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
        ![Guia Novo JDK de Contêiner de Aplicativo][11b]
   9. <span data-ttu-id="0e8ba-210">Depois de concluir todos Olá acima etapas, caixa de diálogo novo contêiner de aplicativo Web hello deve se assemelhar Olá ilustração a seguir:</span><span class="sxs-lookup"><span data-stu-id="0e8ba-210">Once you have completed all of hello above steps, hello New Web App Container dialog box should resemble hello following illustration:</span></span>
      
       ![Novo Contêiner de Aplicativo][14]
   10. <span data-ttu-id="0e8ba-212">Clique em **Okey** toocomplete criação de saudação do seu novo contêiner de aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-212">Click **OK** toocomplete hello creation of your new Web App container.</span></span>
       
        <span data-ttu-id="0e8ba-213">Aguarde alguns segundos para lista de saudação do hello toobe de contêineres de aplicativo Web atualizada e o contêiner de aplicativo web recém-criado agora deve ser selecionado na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-213">Wait a few seconds for hello list of hello Web App containers toobe refreshed, and your newly-created web app container should now be selected in hello list.</span></span>
6. <span data-ttu-id="0e8ba-214">Agora você está pronto toocomplete implantação inicial do hello de tooAzure seu aplicativo Web; Clique em **Okey** toodeploy sua toohello de aplicativo Java selecionado contêiner do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-214">You are now ready toocomplete hello initial deployment of your Web App tooAzure; click **OK** toodeploy your Java application toohello selected Web App container.</span></span> <span data-ttu-id="0e8ba-215">Por padrão, o aplicativo será implantado como um subdiretório saudação do servidor de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-215">By default, your application will be deployed as a subdirectory of hello application server.</span></span> <span data-ttu-id="0e8ba-216">Se quiser toobe implantado como um aplicativo raiz de hello, verifique Olá **implantar tooroot** caixa de seleção antes de clicar em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-216">If you want it toobe deployed as hello root application, check hello **Deploy tooroot** checkbox before clicking **OK**.</span></span>
   
    ![Implantar tooAzure][15]
7. <span data-ttu-id="0e8ba-218">Em seguida, você deve ver Olá **o Log de atividades do Azure** exibição, que indica o status de implantação de saudação do seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-218">Next, you should see hello **Azure Activity Log** view, which will indicate hello deployment status of your Web App.</span></span>
   
    ![Indicador de Progresso][16]
   
    <span data-ttu-id="0e8ba-220">processo de saudação de implantar seu aplicativo Web tooAzure deve levar somente alguns segundos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-220">hello process of deploying your Web App tooAzure should take only a few seconds toocomplete.</span></span> <span data-ttu-id="0e8ba-221">Quando pronto seu aplicativo, você verá um link chamado **publicado** em Olá **Status** coluna.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-221">When your application ready, you will see a link named **Published** in hello **Status** column.</span></span> <span data-ttu-id="0e8ba-222">Quando você clica em um link de Olá, levará home page do aplicativo da Web tooyour implantado, ou você pode usar etapas Olá Olá seção toobrowse tooyour web aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-222">When you click hello link, it will take you tooyour deployed Web App's home page, or you can use hello steps in hello following section toobrowse tooyour web app.</span></span>

## <a name="browsing-tooyour-web-app-on-azure"></a><span data-ttu-id="0e8ba-223">Navegação tooyour aplicativo Web no Azure</span><span class="sxs-lookup"><span data-stu-id="0e8ba-223">Browsing tooyour Web App on Azure</span></span>
<span data-ttu-id="0e8ba-224">toobrowse tooyour aplicativo Web no Azure, você pode usar o hello **Azure Explorer** exibição.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-224">toobrowse tooyour Web App on Azure, you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="0e8ba-225">Se hello **Azure Explorer** exibição não ainda estiver aberta, você pode abri-lo clicando em, em seguida, **exibição** menu em IntelliJ, em seguida, clique em **janelas de ferramentas**e, em seguida, clique em  **Gerenciador de serviço**.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-225">If hello **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="0e8ba-226">Se você não tiver conectado anteriormente, ele solicitará que você toodo assim.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-226">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="0e8ba-227">Olá quando **Azure Explorer** modo de exibição, use execute tooyour de toobrowse essas etapas aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="0e8ba-227">When hello **Azure Explorer** view is displayed, use follow these steps toobrowse tooyour Web App:</span></span> 

1. <span data-ttu-id="0e8ba-228">Expanda Olá **Azure** nó.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-228">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="0e8ba-229">Expanda Olá **aplicativos Web** nó.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-229">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="0e8ba-230">Olá com o botão direito desejada do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-230">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="0e8ba-231">Quando o menu de contexto Olá for exibida, clique em **abrir no navegador**.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-231">When hello context menu appears, click **Open in Browser**.</span></span>
   
    ![Procurar o Aplicativo Web][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="0e8ba-233">Atualizando seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="0e8ba-233">Updating your web app</span></span>
<span data-ttu-id="0e8ba-234">A atualização de um aplicativo Web do Azure em execução é um processo rápido e fácil, e você tem duas opções de atualização:</span><span class="sxs-lookup"><span data-stu-id="0e8ba-234">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="0e8ba-235">Você pode atualizar a implantação de saudação do aplicativo Web Java existente.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-235">You can update hello deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="0e8ba-236">Você pode publicar um toohello de aplicativo Java adicional mesmo contêiner de aplicativo da Web.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-236">You can publish an additional Java application toohello same Web App Container.</span></span>

<span data-ttu-id="0e8ba-237">Em ambos os casos, o processo de saudação é idêntico e leva apenas alguns segundos:</span><span class="sxs-lookup"><span data-stu-id="0e8ba-237">In either case, hello process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="0e8ba-238">No Explorador de projeto IntelliJ Olá, clique no aplicativo de Java hello deseja tooupdate ou adicionar tooan existente do contêiner do aplicativo da Web.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-238">In hello IntelliJ project explorer, right-click hello Java application you want tooupdate or add tooan existing Web App Container.</span></span>
2. <span data-ttu-id="0e8ba-239">Quando o menu de contexto Olá for exibida, selecione **Azure** e, em seguida, **Publicar como um aplicativo Web do Azure...**</span><span class="sxs-lookup"><span data-stu-id="0e8ba-239">When hello context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="0e8ba-240">Como você já fez logon anteriormente, verá uma lista com seus contêineres de aplicativo Web existentes.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-240">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="0e8ba-241">Selecione Olá um deseja toopublish ou publicar novamente o Java aplicativo tooand, clique **Okey**.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-241">Select hello one you want toopublish or re-publish your Java application tooand click **OK**.</span></span>

<span data-ttu-id="0e8ba-242">Alguns segundos mais tarde, Olá **o Log de atividades do Azure** exibição mostrará sua implantação atualizada como **publicado** e você será capaz de tooverify seu aplicativo atualizado em um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-242">A few seconds later, hello **Azure Activity Log** view will show your updated deployment as **Published** and you will be able tooverify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="0e8ba-243">Iniciar, parar ou reiniciar o aplicativo Web existente</span><span class="sxs-lookup"><span data-stu-id="0e8ba-243">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="0e8ba-244">toostart ou interromper um contêiner existente do aplicativo Web do Azure, (incluindo todos os aplicativos do Java Olá implantado nele), você pode usar o hello **Azure Explorer** exibição.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-244">toostart or stop an existing Azure Web App container, (including all hello deployed Java applications in it), you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="0e8ba-245">Se hello **Azure Explorer** exibição não ainda estiver aberta, você pode abri-lo clicando em, em seguida, **exibição** menu em IntelliJ, em seguida, clique em **janelas de ferramentas**e, em seguida, clique em  **Gerenciador de serviço**.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-245">If hello **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="0e8ba-246">Se você não tiver conectado anteriormente, ele solicitará que você toodo assim.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-246">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="0e8ba-247">Olá quando **Azure Explorer** modo de exibição, use siga essas etapas toostart ou interrompa o aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="0e8ba-247">When hello **Azure Explorer** view is displayed, use follow these steps toostart or stop your Web App:</span></span> 

1. <span data-ttu-id="0e8ba-248">Expanda Olá **Azure** nó.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-248">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="0e8ba-249">Expanda Olá **aplicativos Web** nó.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-249">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="0e8ba-250">Olá com o botão direito desejada do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-250">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="0e8ba-251">Quando o menu de contexto Olá for exibida, clique em **iniciar**, **parar**, ou **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-251">When hello context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="0e8ba-252">Observe que as opções de menu Olá têm reconhecimento de contexto, para que você só pode parar um aplicativo web em execução ou iniciar um aplicativo da web que não está em execução no momento.</span><span class="sxs-lookup"><span data-stu-id="0e8ba-252">Note that hello menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Parar Aplicativo Web][18]

## <a name="next-steps"></a><span data-ttu-id="0e8ba-254">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0e8ba-254">Next Steps</span></span>
<span data-ttu-id="0e8ba-255">Para obter mais informações sobre Olá kits de ferramentas do Azure para Java IDEs, consulte Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="0e8ba-255">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="0e8ba-256">[Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0e8ba-256">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="0e8ba-257">[Saudação de instalar o Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0e8ba-257">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="0e8ba-258">[Criar um aplicativo Web Hello World para o Azure no Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0e8ba-258">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="0e8ba-259">[Novidades no Kit de ferramentas do Azure para Eclipse de saudação]</span><span class="sxs-lookup"><span data-stu-id="0e8ba-259">[What's New in hello Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="0e8ba-260">[Kit de ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="0e8ba-260">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="0e8ba-261">[Olá instalando o Kit de ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="0e8ba-261">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="0e8ba-262">*Criar um aplicativo Web Hello World para o Azure no IntelliJ (este artigo)*</span><span class="sxs-lookup"><span data-stu-id="0e8ba-262">*Create a Hello World Web App for Azure in IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="0e8ba-263">[Novidades no Kit de ferramentas do Azure para IntelliJ de saudação]</span><span class="sxs-lookup"><span data-stu-id="0e8ba-263">[What's New in hello Azure Toolkit for IntelliJ]</span></span>

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="0e8ba-264">Consulte também</span><span class="sxs-lookup"><span data-stu-id="0e8ba-264">See Also</span></span>
<span data-ttu-id="0e8ba-265">Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure].</span><span class="sxs-lookup"><span data-stu-id="0e8ba-265">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<span data-ttu-id="0e8ba-266">Para obter informações adicionais sobre a criação de aplicativos Web do Azure, consulte Olá [visão geral de aplicativos Web].</span><span class="sxs-lookup"><span data-stu-id="0e8ba-266">For additional information about creating Azure Web Apps, see hello [Web Apps Overview].</span></span>

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
