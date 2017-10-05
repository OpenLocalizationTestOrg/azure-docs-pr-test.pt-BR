---
title: Como criar um aplicativo Web ASP.NET no Azure | Microsoft Docs
description: "Saiba como executar aplicativos Web no Serviço de Aplicativo do Azure com a implantação do aplicativo Web do ASP.NET padrão."
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/14/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 0f0035f6fef03ddcbb500b78f3445ced5b749808
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a><span data-ttu-id="adc85-103">Criar um aplicativo Web ASP.NET no Azure</span><span class="sxs-lookup"><span data-stu-id="adc85-103">Create an ASP.NET web app in Azure</span></span>

<span data-ttu-id="adc85-104">Os [aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches.</span><span class="sxs-lookup"><span data-stu-id="adc85-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="adc85-105">Este guia de início rápido mostra como implantar seu primeiro aplicativo web ASP.NET em aplicativos Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="adc85-105">This quickstart shows how to deploy your first ASP.NET web app to Azure Web Apps.</span></span> <span data-ttu-id="adc85-106">Quando terminar, você terá um grupo de recursos que consiste em um plano do Serviço de Aplicativo e um aplicativo Web do Azure com um aplicativo Web implantado.</span><span class="sxs-lookup"><span data-stu-id="adc85-106">When you're finished, you'll have a resource group that consists of an App Service plan and an Azure web app with a deployed web application.</span></span>

<span data-ttu-id="adc85-107">Assista ao vídeo para ver este início rápido em ação e, depois, execute as etapas para publicar seu primeiro aplicativo .NET no Azure.</span><span class="sxs-lookup"><span data-stu-id="adc85-107">Watch the video to see this quickstart in action and then follow the steps yourself to publish your first .NET app on Azure.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a><span data-ttu-id="adc85-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="adc85-108">Prerequisites</span></span>

<span data-ttu-id="adc85-109">Para concluir este tutorial:</span><span class="sxs-lookup"><span data-stu-id="adc85-109">To complete this tutorial:</span></span>

* <span data-ttu-id="adc85-110">Instale o [Visual Studio 2017](https://www.visualstudio.com/downloads/) com as cargas de trabalho a seguir:</span><span class="sxs-lookup"><span data-stu-id="adc85-110">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span></span>
    - <span data-ttu-id="adc85-111">**Desenvolvimento Web e do ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="adc85-111">**ASP.NET and web development**</span></span>
    - <span data-ttu-id="adc85-112">**Desenvolvimento do Azure**</span><span class="sxs-lookup"><span data-stu-id="adc85-112">**Azure development**</span></span>

    ![ASP.NET, desenvolvimento Web e desenvolvimento do Azure (na Web e na nuvem)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="adc85-114">Criar um aplicativo Web ASP .NET</span><span class="sxs-lookup"><span data-stu-id="adc85-114">Create an ASP.NET web app</span></span>

<span data-ttu-id="adc85-115">No Visual Studio, crie um projeto selecionando **Arquivo > Novo > Projeto**.</span><span class="sxs-lookup"><span data-stu-id="adc85-115">In Visual Studio, create a project by selecting **File > New > Project**.</span></span> 

<span data-ttu-id="adc85-116">Na caixa de diálogo **Novo Projeto**, clique em **Visual C# > Web > Aplicativo Web ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="adc85-116">In the **New Project** dialog, select **Visual C# > Web > ASP.NET Web Application (.NET Framework)**.</span></span>

<span data-ttu-id="adc85-117">Nomeie o aplicativo como _myFirstAzureWebApp_ e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="adc85-117">Name the application _myFirstAzureWebApp_, and then select **OK**.</span></span>
   
![Caixa de diálogo Novo Projeto](./media/app-service-web-get-started-dotnet/new-project.png)

<span data-ttu-id="adc85-119">Você pode implantar qualquer tipo de aplicativo Web ASP.NET no Azure.</span><span class="sxs-lookup"><span data-stu-id="adc85-119">You can deploy any type of ASP.NET web app to Azure.</span></span> <span data-ttu-id="adc85-120">Para este início rapido, selecione o modelo **MVC** e verifique se a autenticação está definida para **Sem Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="adc85-120">For this quickstart, select the **MVC** template, and make sure authentication is set to **No Authentication**.</span></span>
      
<span data-ttu-id="adc85-121">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="adc85-121">Select **OK**.</span></span>

![Caixa de diálogo Novo Projeto ASP .NET](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

<span data-ttu-id="adc85-123">No menu, selecione **Depurar > Iniciar sem depuração** para executar o aplicativo Web localmente.</span><span class="sxs-lookup"><span data-stu-id="adc85-123">From the menu, select **Debug > Start without Debugging** to run the web app locally.</span></span>

![Executar o aplicativo localmente](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-to-azure"></a><span data-ttu-id="adc85-125">Publicar no Azure</span><span class="sxs-lookup"><span data-stu-id="adc85-125">Publish to Azure</span></span>

<span data-ttu-id="adc85-126">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto **myFirstAzureWebApp** e selecione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="adc85-126">In the **Solution Explorer**, right-click the **myFirstAzureWebApp** project and select **Publish**.</span></span>

![Publicar no Gerenciador de Soluções](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

<span data-ttu-id="adc85-128">Verifique se o **Serviço de Aplicativo do Microsoft Azure** está selecionado e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="adc85-128">Make sure that **Microsoft Azure App Service** is selected and select **Publish**.</span></span>

![Publicar na página de visão geral do projeto](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

<span data-ttu-id="adc85-130">Isso abre a caixa de diálogo **Criar Serviço de Aplicativo**, o que ajuda a criar todos os recursos do Azure necessários para executar seu aplicativo Web ASP.NET no Azure.</span><span class="sxs-lookup"><span data-stu-id="adc85-130">This opens the **Create App Service** dialog, which helps you create all the necessary Azure resources to run the ASP.NET web app in Azure.</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="adc85-131">Entrar no Azure</span><span class="sxs-lookup"><span data-stu-id="adc85-131">Sign in to Azure</span></span>

<span data-ttu-id="adc85-132">Na caixa de diálogo **Criar Serviço de Aplicativo**, selecione **Adicionar uma conta** e entre com sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="adc85-132">In the **Create App Service** dialog, select **Add an account**, and sign in to your Azure subscription.</span></span> <span data-ttu-id="adc85-133">Se você já estiver conectado, selecione a conta que contém a assinatura desejada na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="adc85-133">If you're already signed in, select the account containing the desired subscription from the dropdown.</span></span>

> [!NOTE]
> <span data-ttu-id="adc85-134">Se você já estiver conectado, não selecione **Criar** ainda.</span><span class="sxs-lookup"><span data-stu-id="adc85-134">If you're already signed in, don't select **Create** yet.</span></span>
>
>
   
![Entrar no Azure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a><span data-ttu-id="adc85-136">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="adc85-136">Create a resource group</span></span>

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

<span data-ttu-id="adc85-137">Ao lado de **Grupo de recursos**, selecione **Novo**.</span><span class="sxs-lookup"><span data-stu-id="adc85-137">Next to **Resource Group**, select **New**.</span></span>

<span data-ttu-id="adc85-138">Nomeie o grupo de recursos **myResourceGroup** e selecione **Ok**.</span><span class="sxs-lookup"><span data-stu-id="adc85-138">Name the resource group **myResourceGroup** and select **OK**.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="adc85-139">Criar um plano de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="adc85-139">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="adc85-140">Ao lado de **Plano do Serviço de Aplicativo**, selecione **Novo**.</span><span class="sxs-lookup"><span data-stu-id="adc85-140">Next to **App Service Plan**, select **New**.</span></span> 

<span data-ttu-id="adc85-141">Na caixa de diálogo **Configurar Plano do Serviço de Aplicativo**, use as configurações na tabela de acordo com a captura de tela.</span><span class="sxs-lookup"><span data-stu-id="adc85-141">In the **Configure App Service Plan** dialog, use the settings in the table following the screenshot.</span></span>

![Criar plano de Serviço de Aplicativo](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| <span data-ttu-id="adc85-143">Configuração</span><span class="sxs-lookup"><span data-stu-id="adc85-143">Setting</span></span> | <span data-ttu-id="adc85-144">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="adc85-144">Suggested Value</span></span> | <span data-ttu-id="adc85-145">Descrição</span><span class="sxs-lookup"><span data-stu-id="adc85-145">Description</span></span> |
|-|-|-|
|<span data-ttu-id="adc85-146">Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="adc85-146">App Service Plan</span></span>| <span data-ttu-id="adc85-147">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="adc85-147">myAppServicePlan</span></span> | <span data-ttu-id="adc85-148">O nome do plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="adc85-148">Name of the App Service plan.</span></span> |
| <span data-ttu-id="adc85-149">Local</span><span class="sxs-lookup"><span data-stu-id="adc85-149">Location</span></span> | <span data-ttu-id="adc85-150">Europa Ocidental</span><span class="sxs-lookup"><span data-stu-id="adc85-150">West Europe</span></span> | <span data-ttu-id="adc85-151">O datacenter onde o aplicativo Web está hospedado.</span><span class="sxs-lookup"><span data-stu-id="adc85-151">The datacenter where the web app is hosted.</span></span> |
| <span data-ttu-id="adc85-152">Tamanho</span><span class="sxs-lookup"><span data-stu-id="adc85-152">Size</span></span> | <span data-ttu-id="adc85-153">Grátis</span><span class="sxs-lookup"><span data-stu-id="adc85-153">Free</span></span> | <span data-ttu-id="adc85-154">O [Tipo de preço](https://azure.microsoft.com/pricing/details/app-service/) determina os recursos de hospedagem.</span><span class="sxs-lookup"><span data-stu-id="adc85-154">[Pricing tier](https://azure.microsoft.com/pricing/details/app-service/) determines hosting features.</span></span> |

<span data-ttu-id="adc85-155">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="adc85-155">Select **OK**.</span></span>

## <a name="create-and-publish-the-web-app"></a><span data-ttu-id="adc85-156">Publicar e publicar o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="adc85-156">Create and publish the web app</span></span>

<span data-ttu-id="adc85-157">Em **Nome do Aplicativo Web**, digite um nome exclusivo do aplicativo (os caracteres válidos são `a-z`, `0-9`, e `-`), ou aceite o nome exclusivo gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="adc85-157">In **Web App Name**, type a unique app name (valid characters are `a-z`, `0-9`, and `-`), or accept the automatically generated unique name.</span></span> <span data-ttu-id="adc85-158">A URL do aplicativo Web é `http://<app_name>.azurewebsites.net`, onde `<app_name>` é o nome do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="adc85-158">The URL of the web app is `http://<app_name>.azurewebsites.net`, where `<app_name>` is your web app name.</span></span>

<span data-ttu-id="adc85-159">Clique em **Criar** para começar a criar os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="adc85-159">Select **Create** to start creating the Azure resources.</span></span>

![Configurar o nome do aplicativo Web](./media/app-service-web-get-started-dotnet/web-app-name.png)

<span data-ttu-id="adc85-161">Depois que o assistente é concluído, ele publica o aplicativo Web ASP.NET no Azure e, em seguida, inicia o aplicativo no navegador padrão.</span><span class="sxs-lookup"><span data-stu-id="adc85-161">Once the wizard completes, it publishes the ASP.NET web app to Azure, and then launches the app in the default browser.</span></span>

![Aplicativo Web ASP.NET publicado no Azure](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

<span data-ttu-id="adc85-163">O nome do aplicativo Web especificado na [etapa criar e publicar](#create-and-publish-the-web-app) é usado como o prefixo de URL no formato `http://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="adc85-163">The web app name specified in the [create and publish step](#create-and-publish-the-web-app) is used as the URL prefix in the format `http://<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="adc85-164">Parabéns, seu primeiro aplicativo Web ASP.NET está em execução no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="adc85-164">Congratulations, your ASP.NET web app is running live in Azure App Service.</span></span>

## <a name="update-the-app-and-redeploy"></a><span data-ttu-id="adc85-165">Atualizar o aplicativo e reimplantar</span><span class="sxs-lookup"><span data-stu-id="adc85-165">Update the app and redeploy</span></span>

<span data-ttu-id="adc85-166">No **Gerenciador de Soluções**, abra _Views\Home\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="adc85-166">From the **Solution Explorer**, open _Views\Home\Index.cshtml_.</span></span>

<span data-ttu-id="adc85-167">Encontre o rótulo HTML `<div class="jumbotron">` próximo à parte superior e substitua o elemento inteiro pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="adc85-167">Find the `<div class="jumbotron">` HTML tag near the top, and replace the entire element with the following code:</span></span>

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how to deploy a .NET app to Azure App Service.</p>
</div>
```

<span data-ttu-id="adc85-168">Para implantar novamente no Azure, clique com o botão direito do mouse no projeto **myFirstAzureWebApp**, no **Gerenciador de Soluções** e selecione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="adc85-168">To redeploy to Azure, right-click the **myFirstAzureWebApp** project in **Solution Explorer** and select **Publish**.</span></span>

<span data-ttu-id="adc85-169">Na página de publicação, selecione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="adc85-169">In the publish page, select **Publish**.</span></span>

<span data-ttu-id="adc85-170">Quando a publicação está concluída, o Visual Studio inicia um navegador para a URL do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="adc85-170">When publishing completes, Visual Studio launches a browser to the URL of the web app.</span></span>

![Aplicativo Web ASP.NET atualizado no Azure](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-the-azure-web-app"></a><span data-ttu-id="adc85-172">Gestão do aplicativo web do Azure</span><span class="sxs-lookup"><span data-stu-id="adc85-172">Manage the Azure web app</span></span>

<span data-ttu-id="adc85-173">Acesse o <a href="https://portal.azure.com" target="_blank">portal do Azure</a> para gerenciar o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="adc85-173">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app.</span></span>

<span data-ttu-id="adc85-174">No menu à esquerda, selecione **Serviços de Aplicativos** e, em seguida, selecione o nome do seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="adc85-174">From the left menu, select **App Services**, and then select the name of your Azure web app.</span></span>

![Navegação do portal para o aplicativo Web do Azure](./media/app-service-web-get-started-dotnet/access-portal.png)

<span data-ttu-id="adc85-176">A página Visão Geral do seu aplicativo Web é exibida.</span><span class="sxs-lookup"><span data-stu-id="adc85-176">You see your web app's Overview page.</span></span> <span data-ttu-id="adc85-177">Aqui você pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir.</span><span class="sxs-lookup"><span data-stu-id="adc85-177">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Folha Serviço de Aplicativo no portal do Azure](./media/app-service-web-get-started-dotnet/web-app-blade.png)

<span data-ttu-id="adc85-179">O menu à esquerda fornece páginas diferentes para configurar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="adc85-179">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="adc85-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="adc85-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="adc85-181">ASP.NET com o Banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="adc85-181">ASP.NET with SQL Database</span></span>](app-service-web-tutorial-dotnet-sqldatabase.md)
