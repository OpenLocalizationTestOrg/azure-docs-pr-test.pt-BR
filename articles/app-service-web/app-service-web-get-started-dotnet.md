---
title: aaaCreate uma ASP.NET web aplicativo no Azure | Microsoft Docs
description: "Saiba como aplicativo da web de aplicativos web de toorun no serviço de aplicativo do Azure com a implantação padrão de saudação ASP.NET."
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
ms.openlocfilehash: eec916b3c32b6c8b68083177938c5c822a9782b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a><span data-ttu-id="8f5cc-103">Criar um aplicativo Web ASP.NET no Azure</span><span class="sxs-lookup"><span data-stu-id="8f5cc-103">Create an ASP.NET web app in Azure</span></span>

<span data-ttu-id="8f5cc-104">Os [aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="8f5cc-105">Este guia de início rápido mostra como toodeploy primeiro ASP.NET web aplicativo tooAzure aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-105">This quickstart shows how toodeploy your first ASP.NET web app tooAzure Web Apps.</span></span> <span data-ttu-id="8f5cc-106">Quando terminar, você terá um grupo de recursos que consiste em um plano do Serviço de Aplicativo e um aplicativo Web do Azure com um aplicativo Web implantado.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-106">When you're finished, you'll have a resource group that consists of an App Service plan and an Azure web app with a deployed web application.</span></span>

<span data-ttu-id="8f5cc-107">Assista a este guia de início rápido na ação toosee vídeo hello e, em seguida, execute Olá etapas por conta própria toopublish seu primeiro aplicativo .NET no Azure.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-107">Watch hello video toosee this quickstart in action and then follow hello steps yourself toopublish your first .NET app on Azure.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a><span data-ttu-id="8f5cc-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8f5cc-108">Prerequisites</span></span>

<span data-ttu-id="8f5cc-109">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="8f5cc-109">toocomplete this tutorial:</span></span>

* <span data-ttu-id="8f5cc-110">Instalar [2017 do Visual Studio](https://www.visualstudio.com/downloads/) com hello cargas de trabalho a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f5cc-110">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello following workloads:</span></span>
    - <span data-ttu-id="8f5cc-111">**Desenvolvimento Web e do ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="8f5cc-111">**ASP.NET and web development**</span></span>
    - <span data-ttu-id="8f5cc-112">**Desenvolvimento do Azure**</span><span class="sxs-lookup"><span data-stu-id="8f5cc-112">**Azure development**</span></span>

    ![ASP.NET, desenvolvimento Web e desenvolvimento do Azure (na Web e na nuvem)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="8f5cc-114">Criar um aplicativo Web ASP .NET</span><span class="sxs-lookup"><span data-stu-id="8f5cc-114">Create an ASP.NET web app</span></span>

<span data-ttu-id="8f5cc-115">No Visual Studio, crie um projeto selecionando **Arquivo > Novo > Projeto**.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-115">In Visual Studio, create a project by selecting **File > New > Project**.</span></span> 

<span data-ttu-id="8f5cc-116">Em Olá **novo projeto** caixa de diálogo, selecione **Visual C# > Web > aplicativo Web do ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-116">In hello **New Project** dialog, select **Visual C# > Web > ASP.NET Web Application (.NET Framework)**.</span></span>

<span data-ttu-id="8f5cc-117">Nome do aplicativo hello _myFirstAzureWebApp_e, em seguida, selecione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-117">Name hello application _myFirstAzureWebApp_, and then select **OK**.</span></span>
   
![Caixa de diálogo Novo Projeto](./media/app-service-web-get-started-dotnet/new-project.png)

<span data-ttu-id="8f5cc-119">Você pode implantar qualquer tipo de tooAzure de aplicativo web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-119">You can deploy any type of ASP.NET web app tooAzure.</span></span> <span data-ttu-id="8f5cc-120">Para este guia de início rápido, selecione Olá **MVC** modelo e certifique-se de autenticação está definida muito**sem autenticação**.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-120">For this quickstart, select hello **MVC** template, and make sure authentication is set too**No Authentication**.</span></span>
      
<span data-ttu-id="8f5cc-121">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-121">Select **OK**.</span></span>

![Caixa de diálogo Novo Projeto ASP .NET](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

<span data-ttu-id="8f5cc-123">No menu de saudação, selecione **Depurar > Iniciar sem depuração** toorun Olá web aplicativo localmente.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-123">From hello menu, select **Debug > Start without Debugging** toorun hello web app locally.</span></span>

![Executar o aplicativo localmente](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-tooazure"></a><span data-ttu-id="8f5cc-125">Publicar tooAzure</span><span class="sxs-lookup"><span data-stu-id="8f5cc-125">Publish tooAzure</span></span>

<span data-ttu-id="8f5cc-126">Em Olá **Solution Explorer**, Olá do botão direito do mouse **myFirstAzureWebApp** do projeto e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-126">In hello **Solution Explorer**, right-click hello **myFirstAzureWebApp** project and select **Publish**.</span></span>

![Publicar no Gerenciador de Soluções](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

<span data-ttu-id="8f5cc-128">Verifique se o **Serviço de Aplicativo do Microsoft Azure** está selecionado e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-128">Make sure that **Microsoft Azure App Service** is selected and select **Publish**.</span></span>

![Publicar na página de visão geral do projeto](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

<span data-ttu-id="8f5cc-130">Isso abre o hello **criar serviço de aplicativo** caixa de diálogo, o que ajuda a criar todos os Olá recursos do Azure necessários toorun Olá ASP.NET web aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-130">This opens hello **Create App Service** dialog, which helps you create all hello necessary Azure resources toorun hello ASP.NET web app in Azure.</span></span>

## <a name="sign-in-tooazure"></a><span data-ttu-id="8f5cc-131">Entrar tooAzure</span><span class="sxs-lookup"><span data-stu-id="8f5cc-131">Sign in tooAzure</span></span>

<span data-ttu-id="8f5cc-132">Em Olá **criar serviço de aplicativo** caixa de diálogo, selecione **adicionar uma conta**e entre tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-132">In hello **Create App Service** dialog, select **Add an account**, and sign in tooyour Azure subscription.</span></span> <span data-ttu-id="8f5cc-133">Se você já entrou, conta de saudação select contendo Olá desejado assinatura na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-133">If you're already signed in, select hello account containing hello desired subscription from hello dropdown.</span></span>

> [!NOTE]
> <span data-ttu-id="8f5cc-134">Se você já estiver conectado, não selecione **Criar** ainda.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-134">If you're already signed in, don't select **Create** yet.</span></span>
>
>
   
![Entrar tooAzure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a><span data-ttu-id="8f5cc-136">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8f5cc-136">Create a resource group</span></span>

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

<span data-ttu-id="8f5cc-137">Avançar muito**grupo de recursos**, selecione **novo**.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-137">Next too**Resource Group**, select **New**.</span></span>

<span data-ttu-id="8f5cc-138">Grupo de recursos do nome hello **myResourceGroup** e selecione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-138">Name hello resource group **myResourceGroup** and select **OK**.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="8f5cc-139">Criar um plano de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="8f5cc-139">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="8f5cc-140">Avançar muito**plano do serviço de aplicativo**, selecione **novo**.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-140">Next too**App Service Plan**, select **New**.</span></span> 

<span data-ttu-id="8f5cc-141">Em Olá **configurar o plano de serviço de aplicativo** caixa de diálogo, use Olá configurações na tabela Olá Olá captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-141">In hello **Configure App Service Plan** dialog, use hello settings in hello table following hello screenshot.</span></span>

![Criar plano de Serviço de Aplicativo](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| <span data-ttu-id="8f5cc-143">Configuração</span><span class="sxs-lookup"><span data-stu-id="8f5cc-143">Setting</span></span> | <span data-ttu-id="8f5cc-144">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="8f5cc-144">Suggested Value</span></span> | <span data-ttu-id="8f5cc-145">Descrição</span><span class="sxs-lookup"><span data-stu-id="8f5cc-145">Description</span></span> |
|-|-|-|
|<span data-ttu-id="8f5cc-146">Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="8f5cc-146">App Service Plan</span></span>| <span data-ttu-id="8f5cc-147">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="8f5cc-147">myAppServicePlan</span></span> | <span data-ttu-id="8f5cc-148">Nome da saudação plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-148">Name of hello App Service plan.</span></span> |
| <span data-ttu-id="8f5cc-149">Local</span><span class="sxs-lookup"><span data-stu-id="8f5cc-149">Location</span></span> | <span data-ttu-id="8f5cc-150">Europa Ocidental</span><span class="sxs-lookup"><span data-stu-id="8f5cc-150">West Europe</span></span> | <span data-ttu-id="8f5cc-151">Olá datacenter onde o aplicativo da web de saudação está hospedado.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-151">hello datacenter where hello web app is hosted.</span></span> |
| <span data-ttu-id="8f5cc-152">Tamanho</span><span class="sxs-lookup"><span data-stu-id="8f5cc-152">Size</span></span> | <span data-ttu-id="8f5cc-153">Grátis</span><span class="sxs-lookup"><span data-stu-id="8f5cc-153">Free</span></span> | <span data-ttu-id="8f5cc-154">O [Tipo de preço](https://azure.microsoft.com/pricing/details/app-service/) determina os recursos de hospedagem.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-154">[Pricing tier](https://azure.microsoft.com/pricing/details/app-service/) determines hosting features.</span></span> |

<span data-ttu-id="8f5cc-155">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-155">Select **OK**.</span></span>

## <a name="create-and-publish-hello-web-app"></a><span data-ttu-id="8f5cc-156">Criar e publicar o aplicativo da web de saudação</span><span class="sxs-lookup"><span data-stu-id="8f5cc-156">Create and publish hello web app</span></span>

<span data-ttu-id="8f5cc-157">Em **nome do aplicativo Web**, digite um nome exclusivo do aplicativo (os caracteres válidos são `a-z`, `0-9`, e `-`), ou aceite Olá nome exclusivo gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-157">In **Web App Name**, type a unique app name (valid characters are `a-z`, `0-9`, and `-`), or accept hello automatically generated unique name.</span></span> <span data-ttu-id="8f5cc-158">Olá URL do aplicativo web de saudação é `http://<app_name>.azurewebsites.net`, onde `<app_name>` é o nome do aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-158">hello URL of hello web app is `http://<app_name>.azurewebsites.net`, where `<app_name>` is your web app name.</span></span>

<span data-ttu-id="8f5cc-159">Selecione **criar** toostart criando Olá recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-159">Select **Create** toostart creating hello Azure resources.</span></span>

![Configurar o nome do aplicativo Web](./media/app-service-web-get-started-dotnet/web-app-name.png)

<span data-ttu-id="8f5cc-161">Após a conclusão do assistente Olá, ela publica Olá ASP.NET web aplicativo tooAzure e, em seguida, inicia Olá aplicativo no navegador padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-161">Once hello wizard completes, it publishes hello ASP.NET web app tooAzure, and then launches hello app in hello default browser.</span></span>

![Aplicativo Web ASP.NET publicado no Azure](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

<span data-ttu-id="8f5cc-163">nome do aplicativo web Hello especificado no hello [criar e publicar etapa](#create-and-publish-the-web-app) é usado como Olá prefixo de URL no formato Olá `http://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-163">hello web app name specified in hello [create and publish step](#create-and-publish-the-web-app) is used as hello URL prefix in hello format `http://<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="8f5cc-164">Parabéns, seu primeiro aplicativo Web ASP.NET está em execução no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-164">Congratulations, your ASP.NET web app is running live in Azure App Service.</span></span>

## <a name="update-hello-app-and-redeploy"></a><span data-ttu-id="8f5cc-165">Aplicativo de saudação de atualização e reimplantação</span><span class="sxs-lookup"><span data-stu-id="8f5cc-165">Update hello app and redeploy</span></span>

<span data-ttu-id="8f5cc-166">De saudação **Solution Explorer**, abra _Views\Home\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-166">From hello **Solution Explorer**, open _Views\Home\Index.cshtml_.</span></span>

<span data-ttu-id="8f5cc-167">Localize Olá `<div class="jumbotron">` HTML marca superior hello e substitua todo o elemento Olá Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f5cc-167">Find hello `<div class="jumbotron">` HTML tag near hello top, and replace hello entire element with hello following code:</span></span>

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how toodeploy a .NET app tooAzure App Service.</p>
</div>
```

<span data-ttu-id="8f5cc-168">tooredeploy tooAzure, Olá atalho **myFirstAzureWebApp** project no **Solution Explorer** e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-168">tooredeploy tooAzure, right-click hello **myFirstAzureWebApp** project in **Solution Explorer** and select **Publish**.</span></span>

<span data-ttu-id="8f5cc-169">Olá página de publicação, selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-169">In hello publish page, select **Publish**.</span></span>

<span data-ttu-id="8f5cc-170">Quando a publicação for concluído, o Visual Studio inicia uma URL de toohello do navegador do aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-170">When publishing completes, Visual Studio launches a browser toohello URL of hello web app.</span></span>

![Aplicativo Web ASP.NET atualizado no Azure](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-hello-azure-web-app"></a><span data-ttu-id="8f5cc-172">Gerenciar o aplicativo da web do Azure de saudação</span><span class="sxs-lookup"><span data-stu-id="8f5cc-172">Manage hello Azure web app</span></span>

<span data-ttu-id="8f5cc-173">Vá toohello <a href="https://portal.azure.com" target="_blank">portal do Azure</a> toomanage Olá web app.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-173">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app.</span></span>

<span data-ttu-id="8f5cc-174">No menu à esquerda do hello, selecione **serviços de aplicativos**e, em seguida, selecione o nome de saudação do seu aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-174">From hello left menu, select **App Services**, and then select hello name of your Azure web app.</span></span>

![Aplicativo de web de tooAzure de navegação do Portal](./media/app-service-web-get-started-dotnet/access-portal.png)

<span data-ttu-id="8f5cc-176">A página Visão Geral do seu aplicativo Web é exibida.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-176">You see your web app's Overview page.</span></span> <span data-ttu-id="8f5cc-177">Aqui você pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-177">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Folha Serviço de Aplicativo no portal do Azure](./media/app-service-web-get-started-dotnet/web-app-blade.png)

<span data-ttu-id="8f5cc-179">menu esquerdo Olá fornece diferentes páginas para configurar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f5cc-179">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="8f5cc-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8f5cc-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8f5cc-181">ASP.NET com o Banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="8f5cc-181">ASP.NET with SQL Database</span></span>](app-service-web-tutorial-dotnet-sqldatabase.md)
