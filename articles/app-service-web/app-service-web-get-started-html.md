---
title: "Criar um aplicativo Web HTML estático no Azure | Microsoft Docs"
description: "Saiba como executar aplicativos Web no Serviço de Aplicativo do Azure ao implantar um aplicativo de exemplo HTML estático."
services: app-service\web
documentationcenter: 
author: rick-anderson
manager: wpickett
editor: 
ms.assetid: 60495cc5-6963-4bf0-8174-52786d226c26
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/26/2017
ms.author: riande
ms.custom: mvc
ms.openlocfilehash: 42af5b08b8d2ff0c75fd73dcfa61c861647fd2c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a><span data-ttu-id="7ad59-103">Criar um aplicativo Web HTML estático no Azure</span><span class="sxs-lookup"><span data-stu-id="7ad59-103">Create a static HTML web app in Azure</span></span>

<span data-ttu-id="7ad59-104">Os [aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches.</span><span class="sxs-lookup"><span data-stu-id="7ad59-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="7ad59-105">Este guia de início rápido mostra como implantar um site HTML+CSS básico para Aplicativos Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ad59-105">This quickstart shows how to deploy a basic HTML+CSS site to Azure Web Apps.</span></span> <span data-ttu-id="7ad59-106">Crie o aplicativo Web usando a [CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) e use o Git para implantar o conteúdo HTML de exemplo para o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="7ad59-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample HTML content to the web app.</span></span>

![Home page do aplicativo de exemplo](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="7ad59-108">Você pode seguir as etapas abaixo usando um computador Mac, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="7ad59-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="7ad59-109">A conclusão das etapas demora cerca de cinco minutos assim que os pré-requisitos são instalados.</span><span class="sxs-lookup"><span data-stu-id="7ad59-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ad59-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7ad59-110">Prerequisites</span></span>

<span data-ttu-id="7ad59-111">Para concluir este guia de início rápido:</span><span class="sxs-lookup"><span data-stu-id="7ad59-111">To complete this quickstart:</span></span>

- <span data-ttu-id="7ad59-112">[Instalar o Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span><span class="sxs-lookup"><span data-stu-id="7ad59-112">[Install Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7ad59-113">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="7ad59-113">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7ad59-114">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="7ad59-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="7ad59-115">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7ad59-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-the-sample"></a><span data-ttu-id="7ad59-116">Baixar o exemplo</span><span class="sxs-lookup"><span data-stu-id="7ad59-116">Download the sample</span></span>

<span data-ttu-id="7ad59-117">Em uma janela de terminal, execute o comando a seguir para clonar o repositório de aplicativo de exemplo para o computador local.</span><span class="sxs-lookup"><span data-stu-id="7ad59-117">In a terminal window, run the following command to clone the sample app repository to your local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

<span data-ttu-id="7ad59-118">Você pode usar essa janela de terminal para executar todos os comandos neste guia de início rápido.</span><span class="sxs-lookup"><span data-stu-id="7ad59-118">You use this terminal window to run all the commands in this quickstart.</span></span>

## <a name="view-the-html"></a><span data-ttu-id="7ad59-119">Exibir o HTML</span><span class="sxs-lookup"><span data-stu-id="7ad59-119">View the HTML</span></span>

<span data-ttu-id="7ad59-120">Navegue para o diretório que contém o HTML de exemplo.</span><span class="sxs-lookup"><span data-stu-id="7ad59-120">Navigate to the directory that contains the sample HTML.</span></span> <span data-ttu-id="7ad59-121">Abra o arquivo *index.html* em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="7ad59-121">Open the *index.html* file in your browser.</span></span>

![Home page do aplicativo de exemplo](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Página de aplicativo Web vazia](media/app-service-web-get-started-html/app-service-web-service-created.png)

<span data-ttu-id="7ad59-124">Você criou um novo aplicativo Web vazio no Azure.</span><span class="sxs-lookup"><span data-stu-id="7ad59-124">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (13/13), 2.07 KiB | 0 bytes/s, done.
Total 13 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'cc39b1e4cb'.
remote: Generating deployment script.
remote: Generating deployment script for Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="7ad59-125">Navegar até o aplicativo</span><span class="sxs-lookup"><span data-stu-id="7ad59-125">Browse to the app</span></span>

<span data-ttu-id="7ad59-126">Em um navegador, acesse a URL do aplicativo Web do Azure:</span><span class="sxs-lookup"><span data-stu-id="7ad59-126">In a browser, go to the Azure web app URL:</span></span>

```
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="7ad59-127">A página está sendo executada como um aplicativo Web do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ad59-127">The page is running as an Azure App Service web app.</span></span>

![Home page do aplicativo de exemplo](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="7ad59-129">**Parabéns!**</span><span class="sxs-lookup"><span data-stu-id="7ad59-129">**Congratulations!**</span></span> <span data-ttu-id="7ad59-130">Você implantou seu primeiro aplicativo HTML no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ad59-130">You've deployed your first HTML app to App Service.</span></span>

## <a name="update-and-redeploy-the-app"></a><span data-ttu-id="7ad59-131">Atualizar o aplicativo e reimplantar</span><span class="sxs-lookup"><span data-stu-id="7ad59-131">Update and redeploy the app</span></span>

<span data-ttu-id="7ad59-132">Abra o arquivo *index.html* em um editor de texto e faça uma alteração na marcação.</span><span class="sxs-lookup"><span data-stu-id="7ad59-132">Open the *index.html* file in a text editor, and make a change to the markup.</span></span> <span data-ttu-id="7ad59-133">Por exemplo, altere o cabeçalho H1 de "Serviço de Aplicativo do Azure – Site HTML estático de exemplo" para simplesmente "Serviço de Aplicativo do Azure'.</span><span class="sxs-lookup"><span data-stu-id="7ad59-133">For example, change the H1 heading from "Azure App Service - Sample Static HTML Site" to just "Azure App Service\`.</span></span>

<span data-ttu-id="7ad59-134">Confirme suas alterações no Git e, em seguida, envie as alterações de código por push para o Azure.</span><span class="sxs-lookup"><span data-stu-id="7ad59-134">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated HTML"
git push azure master
```

<span data-ttu-id="7ad59-135">Depois que a implantação for concluída, atualize seu navegador para ver as alterações.</span><span class="sxs-lookup"><span data-stu-id="7ad59-135">Once deployment has completed, refresh your browser to see the changes.</span></span>

![Home page do aplicativo de exemplo atualizada](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="7ad59-137">Gerenciar seu novo aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="7ad59-137">Manage your new Azure web app</span></span>

<span data-ttu-id="7ad59-138">Vá para o <a href="https://portal.azure.com" target="_blank">portal do Azure</a> para gerenciar o aplicativo Web que você criou.</span><span class="sxs-lookup"><span data-stu-id="7ad59-138">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="7ad59-139">No menu à esquerda, clique em **Serviços de Aplicativos** e então clique no nome do seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ad59-139">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Navegação do portal para o aplicativo Web do Azure](./media/app-service-web-get-started-html/portal1.png)

<span data-ttu-id="7ad59-141">A página Visão Geral do seu aplicativo Web é exibida.</span><span class="sxs-lookup"><span data-stu-id="7ad59-141">You see your web app's Overview page.</span></span> <span data-ttu-id="7ad59-142">Aqui você pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir.</span><span class="sxs-lookup"><span data-stu-id="7ad59-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Folha Serviço de Aplicativo no portal do Azure](./media/app-service-web-get-started-html/portal2.png)

<span data-ttu-id="7ad59-144">O menu à esquerda fornece páginas diferentes para configurar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ad59-144">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="7ad59-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7ad59-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7ad59-146">Mapear domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="7ad59-146">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
