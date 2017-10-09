---
title: aaaCreate um aplicativo de web Node.js no Azure | Microsoft Docs
description: "Implante seu primeiro Olá, Mundo em Node.js nos Aplicativos Web do Serviço de Aplicativo do Azure em minutos."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 582bb3c2-164b-42f5-b081-95bfcb7a502a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/05/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 163edf83b2353755fc9fa2d75aed489038cf7c81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a><span data-ttu-id="ae638-103">Criar um aplicativo Web do Node.js no Azure</span><span class="sxs-lookup"><span data-stu-id="ae638-103">Create a Node.js web app in Azure</span></span>

<span data-ttu-id="ae638-104">Os [aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches.</span><span class="sxs-lookup"><span data-stu-id="ae638-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="ae638-105">Este guia de início rápido mostra como toodeploy uma tooAzure de aplicativo Node. js aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="ae638-105">This quickstart shows how toodeploy a Node.js app tooAzure Web Apps.</span></span> <span data-ttu-id="ae638-106">Criar Olá web app usando Olá [CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), e você usa o Git toodeploy exemplo Node. js código toohello web app.</span><span class="sxs-lookup"><span data-stu-id="ae638-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample Node.js code toohello web app.</span></span>

![Aplicativo de exemplo em execução no Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="ae638-108">Você pode seguir estas etapas hello usando um computador Mac, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="ae638-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="ae638-109">Depois que a instalação dos pré-requisitos Olá, são necessárias cerca de cinco minutos toocomplete Olá etapas.</span><span class="sxs-lookup"><span data-stu-id="ae638-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a><span data-ttu-id="ae638-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ae638-110">Prerequisites</span></span>

<span data-ttu-id="ae638-111">toocomplete este guia de início rápido:</span><span class="sxs-lookup"><span data-stu-id="ae638-111">toocomplete this quickstart:</span></span>

* [<span data-ttu-id="ae638-112">Instalar o Git</span><span class="sxs-lookup"><span data-stu-id="ae638-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="ae638-113">Instalar o Node.js e o NPM</span><span class="sxs-lookup"><span data-stu-id="ae638-113">Install Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ae638-114">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="ae638-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ae638-115">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="ae638-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ae638-116">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ae638-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="ae638-117">Baixe o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="ae638-117">Download hello sample</span></span>

<span data-ttu-id="ae638-118">Em uma janela de terminal, execute Olá comando tooclone Olá aplicativo repositório tooyour local máquina de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="ae638-118">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

<span data-ttu-id="ae638-119">Use essa janela do terminal toorun todos os comandos de saudação neste guia de início rápido.</span><span class="sxs-lookup"><span data-stu-id="ae638-119">You use this terminal window toorun all hello commands in this quickstart.</span></span>

<span data-ttu-id="ae638-120">Altere o diretório de toohello que contém o código de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="ae638-120">Change toohello directory that contains hello sample code.</span></span>

```bash
cd nodejs-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="ae638-121">Executar o aplicativo hello localmente</span><span class="sxs-lookup"><span data-stu-id="ae638-121">Run hello app locally</span></span>

<span data-ttu-id="ae638-122">Executar o aplicativo hello localmente abrindo uma janela do terminal e usando Olá `npm start` Olá toolaunch de script criado no servidor HTTP Node. js.</span><span class="sxs-lookup"><span data-stu-id="ae638-122">Run hello application locally by opening a terminal window and using hello `npm start` script toolaunch hello built in Node.js HTTP server.</span></span>

```bash
npm start
```

<span data-ttu-id="ae638-123">Abra um navegador da web e navegue toohello o aplicativo de exemplo no http://localhost:1337.</span><span class="sxs-lookup"><span data-stu-id="ae638-123">Open a web browser, and navigate toohello sample app at http://localhost:1337.</span></span>

<span data-ttu-id="ae638-124">Consulte Olá **Hello World** mensagem do aplicativo de exemplo hello exibida na página de saudação.</span><span class="sxs-lookup"><span data-stu-id="ae638-124">You see hello **Hello World** message from hello sample app displayed in hello page.</span></span>

![Aplicativo de exemplo em execução local](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

<span data-ttu-id="ae638-126">Na janela de terminal, pressione **Ctrl + C** servidor de web tooexit hello.</span><span class="sxs-lookup"><span data-stu-id="ae638-126">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Página de aplicativo Web vazia](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="ae638-128">Você criou um novo aplicativo Web vazio no Azure.</span><span class="sxs-lookup"><span data-stu-id="ae638-128">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up too4 threads.
Compressing objects: 100% (21/21), done.
Writing objects: 100% (23/23), 3.71 KiB | 0 bytes/s, done.
Total 23 (delta 8), reused 7 (delta 1)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'bf114df591'.
remote: Generating deployment script.
remote: Generating deployment script for node.js Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling node.js deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.js'
remote: Copying file: 'package.json'
remote: Copying file: 'process.json'
remote: Deleting file: 'hostingstart.html'
remote: Ignoring: .git
remote: Using start-up script index.js from package.json.
remote: Node.js versions available on hello platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file toochoose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="ae638-129">Procurar toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="ae638-129">Browse toohello app</span></span>

<span data-ttu-id="ae638-130">Procure o aplicativo toohello implantado usando o navegador da web.</span><span class="sxs-lookup"><span data-stu-id="ae638-130">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="ae638-131">Olá Node. js código de exemplo está em execução em um aplicativo da web do serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae638-131">hello Node.js sample code is running in an Azure App Service web app.</span></span>

![Aplicativo de exemplo em execução no Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="ae638-133">**Parabéns!**</span><span class="sxs-lookup"><span data-stu-id="ae638-133">**Congratulations!**</span></span> <span data-ttu-id="ae638-134">Você implantou seu primeiro tooApp de aplicativo Node. js serviço.</span><span class="sxs-lookup"><span data-stu-id="ae638-134">You've deployed your first Node.js app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-code"></a><span data-ttu-id="ae638-135">Atualize e reimplante o código de saudação</span><span class="sxs-lookup"><span data-stu-id="ae638-135">Update and redeploy hello code</span></span>

<span data-ttu-id="ae638-136">Usando um editor de texto, abra Olá `index.js` arquivo no aplicativo de Node. js hello e fazer uma pequena alteração de texto toohello na chamada de saudação muito`response.end`:</span><span class="sxs-lookup"><span data-stu-id="ae638-136">Using a text editor, open hello `index.js` file in hello Node.js app, and make a small change toohello text in hello call too`response.end`:</span></span>

```nodejs
response.end("Hello Azure!");
```

<span data-ttu-id="ae638-137">Confirmar as alterações no Git e, em seguida, enviar por push Olá tooAzure de alterações de código.</span><span class="sxs-lookup"><span data-stu-id="ae638-137">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="ae638-138">Depois que a implantação for concluída, alternar toohello voltar a janela do navegador é aberto no hello **procurar toohello aplicativo** etapa e clique em Atualizar.</span><span class="sxs-lookup"><span data-stu-id="ae638-138">Once deployment has completed, switch back toohello browser window that opened in hello **Browse toohello app** step, and hit refresh.</span></span>

![Aplicativo de exemplo atualizado em execução no Azure](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="ae638-140">Gerenciar seu novo aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="ae638-140">Manage your new Azure web app</span></span>

<span data-ttu-id="ae638-141">Vá toohello <a href="https://portal.azure.com" target="_blank">portal do Azure</a> toomanage Olá web aplicativo que você criou.</span><span class="sxs-lookup"><span data-stu-id="ae638-141">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="ae638-142">No menu à esquerda do hello, clique em **serviços de aplicativos**e, em seguida, clique em nome de saudação do seu aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae638-142">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Aplicativo de web de tooAzure de navegação do Portal](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="ae638-144">A página Visão Geral do seu aplicativo Web é exibida.</span><span class="sxs-lookup"><span data-stu-id="ae638-144">You see your web app's Overview page.</span></span> <span data-ttu-id="ae638-145">Aqui você pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir.</span><span class="sxs-lookup"><span data-stu-id="ae638-145">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Folha Serviço de Aplicativo no portal do Azure](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="ae638-147">menu esquerdo Olá fornece diferentes páginas para configurar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ae638-147">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="ae638-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ae638-148">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ae638-149">Node.js com o MongoDB</span><span class="sxs-lookup"><span data-stu-id="ae638-149">Node.js with MongoDB</span></span>](app-service-web-tutorial-nodejs-mongodb-app.md)
