---
title: Criar seu primeiro aplicativo Web Java no Azure
description: "Saiba como executar aplicativos Web no Serviço de Aplicativo implantando um aplicativo Java básico."
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 6/7/2017
ms.author: cephalin;robmcm
ms.custom: mvc
ms.openlocfilehash: b91b9bde5eb8ea0d7e2196056b635fe54095e748
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="f8ebd-103">Criar seu primeiro aplicativo Web Java no Azure</span><span class="sxs-lookup"><span data-stu-id="f8ebd-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="f8ebd-104">O recurso [aplicativos Web](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) do [Serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) fornece um serviço de hospedagem Web altamente escalonável e com aplicação de patch automática.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-104">The [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) feature of [Azure App Service](../app-service/app-service-value-prop-what-is.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="f8ebd-105">Este guia de início rápido mostra como implantar um aplicativo Web Java no Serviço de Aplicativo usando o [IDE do Eclipse para desenvolvedores Java EE](http://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="f8ebd-105">This quickstart shows how to deploy a Java web app to App Service by using the [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

!["Hello Azure"!](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a><span data-ttu-id="f8ebd-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f8ebd-108">Prerequisites</span></span>

<span data-ttu-id="f8ebd-109">Para concluir este guia de início rápido, instale:</span><span class="sxs-lookup"><span data-stu-id="f8ebd-109">To complete this quickstart, install:</span></span>

* <span data-ttu-id="f8ebd-110">O[Eclipse IDE para desenvolvedores de Java EE](http://www.eclipse.org/downloads/) gratuito.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-110">The free [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="f8ebd-111">Este guia de início rápido usa Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-111">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="f8ebd-112">O [Kit de Ferramentas do Azure para Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span><span class="sxs-lookup"><span data-stu-id="f8ebd-112">The [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="f8ebd-113">Criar um projeto Web dinâmico no Eclipse</span><span class="sxs-lookup"><span data-stu-id="f8ebd-113">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="f8ebd-114">No Eclipse, selecione **Arquivo** > **Novo** > **Projeto Web Dinâmico**.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-114">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="f8ebd-115">Na caixa de diálogo **Novo projeto Web dinâmico**, nomeie o projeto como **MyFirstJavaOnAzureWebApp** e selecione **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-115">In the **New Dynamic Web Project** dialog box, name the project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![Caixa de diálogo Novo Projeto Web Dinâmico](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="f8ebd-117">Adicionar uma página JSP</span><span class="sxs-lookup"><span data-stu-id="f8ebd-117">Add a JSP page</span></span>

<span data-ttu-id="f8ebd-118">Se o Explorador de projeto não for exibido, restaure-o.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-118">If Project Explorer is not displayed, restore it.</span></span>

![Espaço de trabalho do Java EE para Eclipse](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="f8ebd-120">No Explorador de projeto, expanda o projeto **MyFirstJavaOnAzureWebApp**.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-120">In Project Explorer, expand the **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="f8ebd-121">Clique com o botão direito do mouse em **WebContent**e selecione **Novo** > **Arquivo JSP**.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-121">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![Menu de um novo arquivo JSP no Explorador de projeto](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="f8ebd-123">Na caixa de diálogo **Novo Arquivo JSP**:</span><span class="sxs-lookup"><span data-stu-id="f8ebd-123">In the **New JSP File** dialog box:</span></span>

* <span data-ttu-id="f8ebd-124">Nomeie o arquivo **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-124">Name the file **index.jsp**.</span></span>
* <span data-ttu-id="f8ebd-125">Selecione **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-125">Select **Finish**.</span></span>

  ![Caixa de diálogo Novo Arquivo JSP](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="f8ebd-127">No arquivo index.jsp, substitua o elemento `<body></body>` pela seguinte marcação:</span><span class="sxs-lookup"><span data-stu-id="f8ebd-127">In the index.jsp file, replace the `<body></body>` element with the following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="f8ebd-128">Salve as alterações.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-128">Save the changes.</span></span>

## <a name="publish-the-web-app-to-azure"></a><span data-ttu-id="f8ebd-129">Publicar aplicativo Web no Azure</span><span class="sxs-lookup"><span data-stu-id="f8ebd-129">Publish the web app to Azure</span></span>

<span data-ttu-id="f8ebd-130">No Explorador de Projeto, clique com o botão direito do mouse e selecione **Azure** > **Publicar como aplicativo Web do Azure**.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-130">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![Publicar como menu de contexto de Aplicativo Web do Azure](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="f8ebd-132">Na caixa de diálogo **Entrar no Azure**, mantenha a opção **Interativo** e selecione **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-132">In the **Azure Sign In** dialog box, keep the **Interactive** option, and then select **Sign in**.</span></span>

<span data-ttu-id="f8ebd-133">Siga as instruções de entrada.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-133">Follow the sign-in instructions.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="f8ebd-134">Caixa de diálogo Implantar Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="f8ebd-134">Deploy Web App dialog box</span></span>

<span data-ttu-id="f8ebd-135">Depois de entrar na sua conta do Azure, a caixa de diálogo **Implantar aplicativo Web** é exibida.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-135">After you have signed in to your Azure account, the **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="f8ebd-136">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-136">Select **Create**.</span></span>

![Caixa de diálogo Implantar Aplicativo Web](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="f8ebd-138">Criar a caixa de diálogo Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="f8ebd-138">Create App Service dialog box</span></span>

<span data-ttu-id="f8ebd-139">A caixa de diálogo **Criar Serviço de Aplicativo** é exibida com valores padrão.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-139">The **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="f8ebd-140">O número **170602185241** mostrado na imagem a seguir é diferente na caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-140">The number **170602185241** shown in the following image is different in your dialog box.</span></span>

![Criar a caixa de diálogo Serviço de Aplicativo](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="f8ebd-142">Na caixa de diálogo **Criar Serviço de Aplicativo**:</span><span class="sxs-lookup"><span data-stu-id="f8ebd-142">In the **Create App Service** dialog box:</span></span>

* <span data-ttu-id="f8ebd-143">Mantenha o nome gerado para o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-143">Keep the generated name for the web app.</span></span> <span data-ttu-id="f8ebd-144">Esse nome deve ser exclusivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-144">This name must be unique across Azure.</span></span> <span data-ttu-id="f8ebd-145">O nome faz parte do endereço URL do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-145">The name is part of the URL address for the web app.</span></span> <span data-ttu-id="f8ebd-146">Por exemplo: se o nome do aplicativo Web é **MyJavaWebApp**, a URL é *myjavawebapp.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-146">For example: if the web app name is **MyJavaWebApp**, the URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="f8ebd-147">Mantenha o contêiner da Web padrão.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-147">Keep the default web container.</span></span>
* <span data-ttu-id="f8ebd-148">Selecione uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-148">Select an Azure subscription.</span></span>
* <span data-ttu-id="f8ebd-149">Na guia **Plano do serviço de aplicativo**:</span><span class="sxs-lookup"><span data-stu-id="f8ebd-149">On the **App service plan** tab:</span></span>

  * <span data-ttu-id="f8ebd-150">**Criar novo**: mantenha o padrão, que é o nome do plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-150">**Create new**: Keep the default, which is the name of the App Service plan.</span></span>
  * <span data-ttu-id="f8ebd-151">**Local**: selecione **Europa Ocidental** ou um local perto de você.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-151">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="f8ebd-152">**Tipo de preço**: selecione a opção gratuita.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-152">**Pricing tier**: Select the free option.</span></span> <span data-ttu-id="f8ebd-153">Para os recursos, consulte [Preços do Serviço de Aplicativo](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="f8ebd-153">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

   ![Criar a caixa de diálogo Serviço de Aplicativo](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="f8ebd-155">Guia Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f8ebd-155">Resource group tab</span></span>

<span data-ttu-id="f8ebd-156">Selecione a guia **Grupo de recursos**. Mantenha o valor padrão gerado para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-156">Select the **Resource group** tab. Keep the default generated value for the resource group.</span></span>

![Guia Grupo de recursos](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="f8ebd-158">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-158">Select **Create**.</span></span>

<!--
### The JDK tab

Select the **JDK** tab. Keep the default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="f8ebd-159">O Kit de ferramentas do Azure cria o aplicativo Web e exibe uma caixa de diálogo de progresso.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-159">The Azure Toolkit creates the web app and displays a progress dialog box.</span></span>

![Criar caixa de diálogo Serviço de Aplicativo](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="f8ebd-161">Caixa de diálogo Implantar Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="f8ebd-161">Deploy Web App dialog box</span></span>

<span data-ttu-id="f8ebd-162">Na caixa de diálogo **Implantar aplicativo Web**, selecione **Implantar na raiz**.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-162">In the **Deploy Web App** dialog box, select **Deploy to root**.</span></span> <span data-ttu-id="f8ebd-163">Se você tiver um serviço de aplicativo em *wingtiptoys.azurewebsites.net* e não puder implantar na raiz, o aplicativo Web chamado **MyFirstJavaOnAzureWebApp** será implantado em *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-163">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy to the root, the web app named **MyFirstJavaOnAzureWebApp** is deployed to *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![Caixa de diálogo Implantar Aplicativo Web](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="f8ebd-165">A caixa de diálogo mostra o Azure, o JDK e as seleções de contêiner da Web.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-165">The dialog box shows the Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="f8ebd-166">Selecione **Implantar** para publicar o aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-166">Select **Deploy** to publish the web app to Azure.</span></span>

<span data-ttu-id="f8ebd-167">Quando a publicação for concluída, selecione o link **Publicado** na caixa de diálogo **Log de atividades do Azure**.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-167">When the publishing finishes, select the **Published** link in the **Azure Activity Log** dialog box.</span></span>

![Caixa de diálogo Log de atividades do Azure](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="f8ebd-169">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="f8ebd-169">Congratulations!</span></span> <span data-ttu-id="f8ebd-170">Você implantou o aplicativo Web no Azure com êxito.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-170">You have successfully deployed your web app to Azure.</span></span> 

!["Hello Azure"!](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-the-web-app"></a><span data-ttu-id="f8ebd-173">Atualizar o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="f8ebd-173">Update the web app</span></span>

<span data-ttu-id="f8ebd-174">Altere o código JSP de exemplo para uma mensagem diferente.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-174">Change the sample JSP code to a different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="f8ebd-175">Salve as alterações.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-175">Save the changes.</span></span>

<span data-ttu-id="f8ebd-176">No Explorador de Projeto, clique com o botão direito do mouse e selecione **Azure** > **Publicar como aplicativo Web do Azure**.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-176">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="f8ebd-177">A caixa de diálogo **Implantar aplicativo Web** é exibida e mostra o serviço de aplicativo criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-177">The **Deploy Web App** dialog box appears and shows the app service that you previously created.</span></span> 

> [!NOTE]
> <span data-ttu-id="f8ebd-178">Selecione **Implantar na raiz** cada vez que você publicar.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-178">Select **Deploy to root** each time you publish.</span></span>
>

<span data-ttu-id="f8ebd-179">Selecione o aplicativo Web e selecione **Implantar** para publicar as alterações.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-179">Select the web app and select **Deploy**, which publishes the changes.</span></span>

<span data-ttu-id="f8ebd-180">Quando o link **Publicando** aparecer, selecione-o para navegar até o aplicativo Web e ver as alterações.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-180">When the **Publishing** link appears, select it to browse to the web app and see the changes.</span></span>

## <a name="manage-the-web-app"></a><span data-ttu-id="f8ebd-181">Gerenciar o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="f8ebd-181">Manage the web app</span></span>

<span data-ttu-id="f8ebd-182">Vá para o <a href="https://portal.azure.com" target="_blank">portal do Azure</a> a fim de ver o aplicativo Web que você criou.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-182">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to see the web app that you created.</span></span>

<span data-ttu-id="f8ebd-183">Selecione **Grupos de recursos** no painel esquerdo.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-183">From the left menu, select **Resource Groups**.</span></span>

![Navegação no portal para grupos de recursos](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="f8ebd-185">Selecione a guia Grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-185">Select the resource group.</span></span> <span data-ttu-id="f8ebd-186">A página mostra os recursos que você criou neste guia de início rápido.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-186">The page shows the resources that you created in this quickstart.</span></span>

![Grupo de recursos myResourceGroup](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="f8ebd-188">Selecione o aplicativo Web (**webapp-170602193915** na imagem anterior).</span><span class="sxs-lookup"><span data-stu-id="f8ebd-188">Select the web app (**webapp-170602193915** in the preceding image).</span></span>

<span data-ttu-id="f8ebd-189">A página **Visão geral** será exibida.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-189">The **Overview** page appears.</span></span> <span data-ttu-id="f8ebd-190">Esta página fornece uma visão de como está seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-190">This page gives you a view of how the app is doing.</span></span> <span data-ttu-id="f8ebd-191">Aqui você pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-191">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="f8ebd-192">As guias no lado esquerdo da página mostram as configuração diferentes que você pode abrir.</span><span class="sxs-lookup"><span data-stu-id="f8ebd-192">The tabs on the left side of the page show the different configurations that you can open.</span></span> 

![Página Serviço de Aplicativo no portal do Azure](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="f8ebd-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f8ebd-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f8ebd-195">Mapear domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="f8ebd-195">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
