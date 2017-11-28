---
title: "aplicativo web de aaaCreate uma HTML estática no Azure | Microsoft Docs"
description: "Saiba como o aplicativo de exemplo toorun aplicativos de web no serviço de aplicativo do Azure Implantando uma HTML estático."
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
ms.openlocfilehash: efd8c8189a3aa1ac35602b688eeb31bff6f5a373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a><span data-ttu-id="b7723-103">Criar um aplicativo Web HTML estático no Azure</span><span class="sxs-lookup"><span data-stu-id="b7723-103">Create a static HTML web app in Azure</span></span>

<span data-ttu-id="b7723-104">Os [aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches.</span><span class="sxs-lookup"><span data-stu-id="b7723-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="b7723-105">Este guia de início rápido mostra como toodeploy básica HTML + CSS site tooAzure os aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="b7723-105">This quickstart shows how toodeploy a basic HTML+CSS site tooAzure Web Apps.</span></span> <span data-ttu-id="b7723-106">Criar Olá web app usando Olá [CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), e você usar o aplicativo de web de conteúdo toohello Git toodeploy exemplo HTML.</span><span class="sxs-lookup"><span data-stu-id="b7723-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample HTML content toohello web app.</span></span>

![Home page do aplicativo de exemplo](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="b7723-108">Você pode seguir estas etapas hello usando um computador Mac, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="b7723-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="b7723-109">Depois que a instalação dos pré-requisitos Olá, são necessárias cerca de cinco minutos toocomplete Olá etapas.</span><span class="sxs-lookup"><span data-stu-id="b7723-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7723-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b7723-110">Prerequisites</span></span>

<span data-ttu-id="b7723-111">toocomplete este guia de início rápido:</span><span class="sxs-lookup"><span data-stu-id="b7723-111">toocomplete this quickstart:</span></span>

- <span data-ttu-id="b7723-112">[Instalar o Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span><span class="sxs-lookup"><span data-stu-id="b7723-112">[Install Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b7723-113">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b7723-113">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b7723-114">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7723-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="b7723-115">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b7723-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="b7723-116">Baixe o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="b7723-116">Download hello sample</span></span>

<span data-ttu-id="b7723-117">Em uma janela de terminal, execute Olá comando tooclone Olá aplicativo repositório tooyour local máquina de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="b7723-117">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

<span data-ttu-id="b7723-118">Use essa janela do terminal toorun todos os comandos de saudação neste guia de início rápido.</span><span class="sxs-lookup"><span data-stu-id="b7723-118">You use this terminal window toorun all hello commands in this quickstart.</span></span>

## <a name="view-hello-html"></a><span data-ttu-id="b7723-119">Saudação de exibição HTML</span><span class="sxs-lookup"><span data-stu-id="b7723-119">View hello HTML</span></span>

<span data-ttu-id="b7723-120">Navegue toohello diretório que contém o exemplo hello HTML.</span><span class="sxs-lookup"><span data-stu-id="b7723-120">Navigate toohello directory that contains hello sample HTML.</span></span> <span data-ttu-id="b7723-121">Olá abrir *index.html* arquivo no seu navegador.</span><span class="sxs-lookup"><span data-stu-id="b7723-121">Open hello *index.html* file in your browser.</span></span>

![Home page do aplicativo de exemplo](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Página de aplicativo Web vazia](media/app-service-web-get-started-html/app-service-web-service-created.png)

<span data-ttu-id="b7723-124">Você criou um novo aplicativo Web vazio no Azure.</span><span class="sxs-lookup"><span data-stu-id="b7723-124">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up too4 threads.
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
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="b7723-125">Procurar toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="b7723-125">Browse toohello app</span></span>

<span data-ttu-id="b7723-126">Em um navegador, acesse a URL do aplicativo web do Azure toohello:</span><span class="sxs-lookup"><span data-stu-id="b7723-126">In a browser, go toohello Azure web app URL:</span></span>

```
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="b7723-127">página Hello está sendo executado como um aplicativo da web do serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="b7723-127">hello page is running as an Azure App Service web app.</span></span>

![Home page do aplicativo de exemplo](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="b7723-129">**Parabéns!**</span><span class="sxs-lookup"><span data-stu-id="b7723-129">**Congratulations!**</span></span> <span data-ttu-id="b7723-130">Você implantou seu primeiro tooApp de aplicativo HTML Service.</span><span class="sxs-lookup"><span data-stu-id="b7723-130">You've deployed your first HTML app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-app"></a><span data-ttu-id="b7723-131">Atualize e reimplante o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="b7723-131">Update and redeploy hello app</span></span>

<span data-ttu-id="b7723-132">Olá abrir *index* do arquivo em um editor de texto e fazer uma marcação de toohello de alteração.</span><span class="sxs-lookup"><span data-stu-id="b7723-132">Open hello *index.html* file in a text editor, and make a change toohello markup.</span></span> <span data-ttu-id="b7723-133">Por exemplo, altere o título do hello H1 de "Azure aplicativo de serviço – exemplo estático HTML Site" toojust "serviço de aplicativo do Azure'.</span><span class="sxs-lookup"><span data-stu-id="b7723-133">For example, change hello H1 heading from "Azure App Service - Sample Static HTML Site" toojust "Azure App Service\`.</span></span>

<span data-ttu-id="b7723-134">Confirmar as alterações no Git e, em seguida, enviar por push Olá tooAzure de alterações de código.</span><span class="sxs-lookup"><span data-stu-id="b7723-134">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated HTML"
git push azure master
```

<span data-ttu-id="b7723-135">Depois que a implantação for concluída, atualize as alterações de saudação do navegador toosee.</span><span class="sxs-lookup"><span data-stu-id="b7723-135">Once deployment has completed, refresh your browser toosee hello changes.</span></span>

![Home page do aplicativo de exemplo atualizada](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="b7723-137">Gerenciar seu novo aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="b7723-137">Manage your new Azure web app</span></span>

<span data-ttu-id="b7723-138">Vá toohello <a href="https://portal.azure.com" target="_blank">portal do Azure</a> toomanage Olá web aplicativo que você criou.</span><span class="sxs-lookup"><span data-stu-id="b7723-138">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="b7723-139">No menu à esquerda do hello, clique em **serviços de aplicativos**e, em seguida, clique em nome de saudação do seu aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="b7723-139">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Aplicativo de web de tooAzure de navegação do Portal](./media/app-service-web-get-started-html/portal1.png)

<span data-ttu-id="b7723-141">A página Visão Geral do seu aplicativo Web é exibida.</span><span class="sxs-lookup"><span data-stu-id="b7723-141">You see your web app's Overview page.</span></span> <span data-ttu-id="b7723-142">Aqui você pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir.</span><span class="sxs-lookup"><span data-stu-id="b7723-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Folha Serviço de Aplicativo no portal do Azure](./media/app-service-web-get-started-html/portal2.png)

<span data-ttu-id="b7723-144">menu esquerdo Olá fornece diferentes páginas para configurar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b7723-144">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="b7723-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b7723-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b7723-146">Mapear domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="b7723-146">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
