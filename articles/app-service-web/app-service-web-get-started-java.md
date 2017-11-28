---
title: aaaCreate seu primeiro aplicativo web Java no Azure
description: "Saiba como toorun aplicativos web no serviço de aplicativo ao implantar um aplicativo Java básico."
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
ms.openlocfilehash: 81315c07b5aa84cbec50a17b2cb3914927b19c00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="597a8-103">Criar seu primeiro aplicativo Web Java no Azure</span><span class="sxs-lookup"><span data-stu-id="597a8-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="597a8-104">Olá [aplicativos Web](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) recurso de [do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) fornece um serviço de hospedagem web altamente escalonável, aplicação de patch automática.</span><span class="sxs-lookup"><span data-stu-id="597a8-104">hello [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) feature of [Azure App Service](../app-service/app-service-value-prop-what-is.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="597a8-105">Este guia de início rápido mostra como toodeploy um Java web aplicativo tooApp Service usando Olá [IDE do Eclipse para desenvolvedores Java EE](http://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="597a8-105">This quickstart shows how toodeploy a Java web app tooApp Service by using hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

!["Hello Azure"!](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a><span data-ttu-id="597a8-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="597a8-108">Prerequisites</span></span>

<span data-ttu-id="597a8-109">toocomplete este guia de início rápido, instalar:</span><span class="sxs-lookup"><span data-stu-id="597a8-109">toocomplete this quickstart, install:</span></span>

* <span data-ttu-id="597a8-110">Olá livre [IDE do Eclipse para desenvolvedores Java EE](http://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="597a8-110">hello free [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="597a8-111">Este guia de início rápido usa Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="597a8-111">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="597a8-112">Olá [Kit de ferramentas do Azure para Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span><span class="sxs-lookup"><span data-stu-id="597a8-112">hello [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="597a8-113">Criar um projeto Web dinâmico no Eclipse</span><span class="sxs-lookup"><span data-stu-id="597a8-113">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="597a8-114">No Eclipse, selecione **Arquivo** > **Novo** > **Projeto Web Dinâmico**.</span><span class="sxs-lookup"><span data-stu-id="597a8-114">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="597a8-115">Em Olá **novo projeto Web dinâmico** caixa de diálogo, o projeto de saudação do nome **MyFirstJavaOnAzureWebApp**e selecione **concluir**.</span><span class="sxs-lookup"><span data-stu-id="597a8-115">In hello **New Dynamic Web Project** dialog box, name hello project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![Caixa de diálogo Novo Projeto Web Dinâmico](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="597a8-117">Adicionar uma página JSP</span><span class="sxs-lookup"><span data-stu-id="597a8-117">Add a JSP page</span></span>

<span data-ttu-id="597a8-118">Se o Explorador de projeto não for exibido, restaure-o.</span><span class="sxs-lookup"><span data-stu-id="597a8-118">If Project Explorer is not displayed, restore it.</span></span>

![Espaço de trabalho do Java EE para Eclipse](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="597a8-120">No Explorador de projeto, expanda Olá **MyFirstJavaOnAzureWebApp** projeto.</span><span class="sxs-lookup"><span data-stu-id="597a8-120">In Project Explorer, expand hello **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="597a8-121">Clique com o botão direito do mouse em **WebContent**e selecione **Novo** > **Arquivo JSP**.</span><span class="sxs-lookup"><span data-stu-id="597a8-121">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![Menu de um novo arquivo JSP no Explorador de projeto](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="597a8-123">Em Olá **novo arquivo JSP** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="597a8-123">In hello **New JSP File** dialog box:</span></span>

* <span data-ttu-id="597a8-124">Arquivo de saudação do nome **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="597a8-124">Name hello file **index.jsp**.</span></span>
* <span data-ttu-id="597a8-125">Selecione **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="597a8-125">Select **Finish**.</span></span>

  ![Caixa de diálogo Novo Arquivo JSP](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="597a8-127">No arquivo JSP Olá substitua Olá `<body></body>` elemento com hello marcação a seguir:</span><span class="sxs-lookup"><span data-stu-id="597a8-127">In hello index.jsp file, replace hello `<body></body>` element with hello following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="597a8-128">Salve alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="597a8-128">Save hello changes.</span></span>

## <a name="publish-hello-web-app-tooazure"></a><span data-ttu-id="597a8-129">Publicar Olá web aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="597a8-129">Publish hello web app tooAzure</span></span>

<span data-ttu-id="597a8-130">No Explorador de projeto, clique com botão direito hello e, em seguida, selecione **Azure** > **Publicar como um aplicativo Web do Azure**.</span><span class="sxs-lookup"><span data-stu-id="597a8-130">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![Publicar como menu de contexto de Aplicativo Web do Azure](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="597a8-132">Em Olá **Azure entrar** caixa de diálogo, mantenha Olá **interativo** opção e, em seguida, selecione **entrar**.</span><span class="sxs-lookup"><span data-stu-id="597a8-132">In hello **Azure Sign In** dialog box, keep hello **Interactive** option, and then select **Sign in**.</span></span>

<span data-ttu-id="597a8-133">Siga Olá entrar instruções.</span><span class="sxs-lookup"><span data-stu-id="597a8-133">Follow hello sign-in instructions.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="597a8-134">Caixa de diálogo Implantar Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="597a8-134">Deploy Web App dialog box</span></span>

<span data-ttu-id="597a8-135">Depois de ter entrado tooyour conta do Azure, Olá **implantar aplicativo da Web** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="597a8-135">After you have signed in tooyour Azure account, hello **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="597a8-136">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="597a8-136">Select **Create**.</span></span>

![Caixa de diálogo Implantar Aplicativo Web](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="597a8-138">Criar a caixa de diálogo Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="597a8-138">Create App Service dialog box</span></span>

<span data-ttu-id="597a8-139">Olá **criar serviço de aplicativo** caixa de diálogo é exibida com valores padrão.</span><span class="sxs-lookup"><span data-stu-id="597a8-139">hello **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="597a8-140">Olá número **170602185241** mostrado no hello seguinte imagem é diferente na caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="597a8-140">hello number **170602185241** shown in hello following image is different in your dialog box.</span></span>

![Criar a caixa de diálogo Serviço de Aplicativo](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="597a8-142">Em Olá **criar serviço de aplicativo** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="597a8-142">In hello **Create App Service** dialog box:</span></span>

* <span data-ttu-id="597a8-143">Mantenha o nome de saudação gerada para o aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="597a8-143">Keep hello generated name for hello web app.</span></span> <span data-ttu-id="597a8-144">Esse nome deve ser exclusivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="597a8-144">This name must be unique across Azure.</span></span> <span data-ttu-id="597a8-145">nome de saudação faz parte do endereço da URL Olá Olá web app.</span><span class="sxs-lookup"><span data-stu-id="597a8-145">hello name is part of hello URL address for hello web app.</span></span> <span data-ttu-id="597a8-146">Por exemplo: se o nome do aplicativo web hello é **MyJavaWebApp**, Olá URL é *myjavawebapp.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="597a8-146">For example: if hello web app name is **MyJavaWebApp**, hello URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="597a8-147">Manter o contêiner do saudação padrão da web.</span><span class="sxs-lookup"><span data-stu-id="597a8-147">Keep hello default web container.</span></span>
* <span data-ttu-id="597a8-148">Selecione uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="597a8-148">Select an Azure subscription.</span></span>
* <span data-ttu-id="597a8-149">Em Olá **plano do serviço de aplicativo** guia:</span><span class="sxs-lookup"><span data-stu-id="597a8-149">On hello **App service plan** tab:</span></span>

  * <span data-ttu-id="597a8-150">**Criar um novo**: mantenha saudação padrão, que é o nome de saudação do hello plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="597a8-150">**Create new**: Keep hello default, which is hello name of hello App Service plan.</span></span>
  * <span data-ttu-id="597a8-151">**Local**: selecione **Europa Ocidental** ou um local perto de você.</span><span class="sxs-lookup"><span data-stu-id="597a8-151">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="597a8-152">**Tipo de preço**: selecione Olá opção livre.</span><span class="sxs-lookup"><span data-stu-id="597a8-152">**Pricing tier**: Select hello free option.</span></span> <span data-ttu-id="597a8-153">Para os recursos, consulte [Preços do Serviço de Aplicativo](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="597a8-153">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

   ![Criar a caixa de diálogo Serviço de Aplicativo](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="597a8-155">Guia Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="597a8-155">Resource group tab</span></span>

<span data-ttu-id="597a8-156">Selecione Olá **grupo de recursos** guia. Mantenha o valor de padrão gerado de Olá Olá para grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="597a8-156">Select hello **Resource group** tab. Keep hello default generated value for hello resource group.</span></span>

![Guia Grupo de recursos](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="597a8-158">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="597a8-158">Select **Create**.</span></span>

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="597a8-159">Olá Kit de ferramentas do Azure cria Olá web app e exibe uma caixa de diálogo de progresso.</span><span class="sxs-lookup"><span data-stu-id="597a8-159">hello Azure Toolkit creates hello web app and displays a progress dialog box.</span></span>

![Criar caixa de diálogo Serviço de Aplicativo](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="597a8-161">Caixa de diálogo Implantar Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="597a8-161">Deploy Web App dialog box</span></span>

<span data-ttu-id="597a8-162">Em Olá **implantar aplicativo da Web** caixa de diálogo, selecione **implantar tooroot**.</span><span class="sxs-lookup"><span data-stu-id="597a8-162">In hello **Deploy Web App** dialog box, select **Deploy tooroot**.</span></span> <span data-ttu-id="597a8-163">Se você tiver um aplicativo de serviço no *wingtiptoys.azurewebsites.net* e você não implanta toohello raiz, Olá web aplicativo chamado **MyFirstJavaOnAzureWebApp** é implantado muito *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span><span class="sxs-lookup"><span data-stu-id="597a8-163">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy toohello root, hello web app named **MyFirstJavaOnAzureWebApp** is deployed too*wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![Caixa de diálogo Implantar Aplicativo Web](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="597a8-165">caixa de diálogo Olá mostra hello Azure JDK e as seleções de contêiner da web.</span><span class="sxs-lookup"><span data-stu-id="597a8-165">hello dialog box shows hello Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="597a8-166">Selecione **implantar** toopublish Olá web aplicativo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="597a8-166">Select **Deploy** toopublish hello web app tooAzure.</span></span>

<span data-ttu-id="597a8-167">Quando termina de publicação hello, selecione Olá **publicado** link no hello **o Log de atividades do Azure** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="597a8-167">When hello publishing finishes, select hello **Published** link in hello **Azure Activity Log** dialog box.</span></span>

![Caixa de diálogo Log de atividades do Azure](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="597a8-169">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="597a8-169">Congratulations!</span></span> <span data-ttu-id="597a8-170">Você implantou seu tooAzure de aplicativo web com êxito.</span><span class="sxs-lookup"><span data-stu-id="597a8-170">You have successfully deployed your web app tooAzure.</span></span> 

!["Hello Azure"!](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a><span data-ttu-id="597a8-173">Atualizar o aplicativo web de saudação</span><span class="sxs-lookup"><span data-stu-id="597a8-173">Update hello web app</span></span>

<span data-ttu-id="597a8-174">Alterar Olá exemplo JSP código tooa mensagem diferente.</span><span class="sxs-lookup"><span data-stu-id="597a8-174">Change hello sample JSP code tooa different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="597a8-175">Salve alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="597a8-175">Save hello changes.</span></span>

<span data-ttu-id="597a8-176">No Explorador de projeto, clique com botão direito hello e, em seguida, selecione **Azure** > **Publicar como um aplicativo Web do Azure**.</span><span class="sxs-lookup"><span data-stu-id="597a8-176">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="597a8-177">Olá **implantar aplicativo da Web** caixa de diálogo é exibida e mostra Olá do serviço de aplicativo que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="597a8-177">hello **Deploy Web App** dialog box appears and shows hello app service that you previously created.</span></span> 

> [!NOTE]
> <span data-ttu-id="597a8-178">Selecione **implantar tooroot** cada vez que você publicar.</span><span class="sxs-lookup"><span data-stu-id="597a8-178">Select **Deploy tooroot** each time you publish.</span></span>
>

<span data-ttu-id="597a8-179">Selecione o aplicativo web de saudação e selecione **implantar**, que publica as alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="597a8-179">Select hello web app and select **Deploy**, which publishes hello changes.</span></span>

<span data-ttu-id="597a8-180">Olá quando **publicação** link for exibida, selecione-o aplicativo de web toohello toobrowse e ver as alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="597a8-180">When hello **Publishing** link appears, select it toobrowse toohello web app and see hello changes.</span></span>

## <a name="manage-hello-web-app"></a><span data-ttu-id="597a8-181">Gerenciar o aplicativo da web de saudação</span><span class="sxs-lookup"><span data-stu-id="597a8-181">Manage hello web app</span></span>

<span data-ttu-id="597a8-182">Vá toohello <a href="https://portal.azure.com" target="_blank">portal do Azure</a> toosee Olá web aplicativo que você criou.</span><span class="sxs-lookup"><span data-stu-id="597a8-182">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toosee hello web app that you created.</span></span>

<span data-ttu-id="597a8-183">No menu à esquerda do hello, selecione **grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="597a8-183">From hello left menu, select **Resource Groups**.</span></span>

![Grupos de tooresource de navegação do Portal](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="597a8-185">Selecione o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="597a8-185">Select hello resource group.</span></span> <span data-ttu-id="597a8-186">página Olá mostra os recursos de saudação que você criou neste guia de início rápido.</span><span class="sxs-lookup"><span data-stu-id="597a8-186">hello page shows hello resources that you created in this quickstart.</span></span>

![Grupo de recursos myResourceGroup](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="597a8-188">Selecione Olá web app (**170602193915 webapp** em Olá anterior imagem).</span><span class="sxs-lookup"><span data-stu-id="597a8-188">Select hello web app (**webapp-170602193915** in hello preceding image).</span></span>

<span data-ttu-id="597a8-189">Olá **visão geral** página será exibida.</span><span class="sxs-lookup"><span data-stu-id="597a8-189">hello **Overview** page appears.</span></span> <span data-ttu-id="597a8-190">Esta página fornece uma exibição como o aplicativo hello está fazendo.</span><span class="sxs-lookup"><span data-stu-id="597a8-190">This page gives you a view of how hello app is doing.</span></span> <span data-ttu-id="597a8-191">Aqui você pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir.</span><span class="sxs-lookup"><span data-stu-id="597a8-191">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="597a8-192">guias de saudação no lado esquerdo de saudação da página Olá mostram Olá configurações diferentes que você pode abrir.</span><span class="sxs-lookup"><span data-stu-id="597a8-192">hello tabs on hello left side of hello page show hello different configurations that you can open.</span></span> 

![Página Serviço de Aplicativo no portal do Azure](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="597a8-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="597a8-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="597a8-195">Mapear domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="597a8-195">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
