---
title: aaaCreate um aplicativo web do Python no Azure | Microsoft Docs
description: "Implante seu primeiro Olá, Mundo em Python no aplicativo Web do Serviço de Aplicativo do Azure em minutos."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 928ee2e5-6143-4c0c-8546-366f5a3d80ce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 03/17/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 42178d490d8aa8eaf93710667aad598794c62c8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-python-web-app-in-azure"></a><span data-ttu-id="1b00b-103">Criar um aplicativo Web do Python no Azure</span><span class="sxs-lookup"><span data-stu-id="1b00b-103">Create a Python web app in Azure</span></span>

<span data-ttu-id="1b00b-104">Os [aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches.</span><span class="sxs-lookup"><span data-stu-id="1b00b-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="1b00b-105">Este guia de início rápido orienta como toodevelop e implantar um aplicativo de Python tooAzure aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="1b00b-105">This quickstart walks through how toodevelop and deploy a Python app tooAzure Web Apps.</span></span> <span data-ttu-id="1b00b-106">Criar Olá web app usando Olá [CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), e você usar o aplicativo de web toohello de código Python de exemplo toodeploy de Git.</span><span class="sxs-lookup"><span data-stu-id="1b00b-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample Python code toohello web app.</span></span>

![Aplicativo de exemplo em execução no Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="1b00b-108">Você pode seguir estas etapas hello usando um computador Mac, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="1b00b-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="1b00b-109">Depois que a instalação dos pré-requisitos Olá, são necessárias cerca de cinco minutos toocomplete Olá etapas.</span><span class="sxs-lookup"><span data-stu-id="1b00b-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="1b00b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1b00b-110">Prerequisites</span></span>

<span data-ttu-id="1b00b-111">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="1b00b-111">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="1b00b-112">Instalar o Git</span><span class="sxs-lookup"><span data-stu-id="1b00b-112">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="1b00b-113">Instalar o Python</span><span class="sxs-lookup"><span data-stu-id="1b00b-113">Install Python</span></span>](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1b00b-114">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="1b00b-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="1b00b-115">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="1b00b-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1b00b-116">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1b00b-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="1b00b-117">Baixe o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="1b00b-117">Download hello sample</span></span>

<span data-ttu-id="1b00b-118">Em uma janela de terminal, execute Olá comando tooclone Olá aplicativo repositório tooyour local máquina de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="1b00b-118">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

<span data-ttu-id="1b00b-119">Use essa janela do terminal toorun todos os comandos de saudação neste guia de início rápido.</span><span class="sxs-lookup"><span data-stu-id="1b00b-119">You use this terminal window toorun all hello commands in this quickstart.</span></span>

<span data-ttu-id="1b00b-120">Altere o diretório de toohello que contém o código de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="1b00b-120">Change toohello directory that contains hello sample code.</span></span>

```bash
cd Python-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="1b00b-121">Executar o aplicativo hello localmente</span><span class="sxs-lookup"><span data-stu-id="1b00b-121">Run hello app locally</span></span>

<span data-ttu-id="1b00b-122">Instalar pacotes de saudação necessária usando `pip`.</span><span class="sxs-lookup"><span data-stu-id="1b00b-122">Install hello required packages using `pip`.</span></span>

```bash
pip install -r requirements.txt
```

<span data-ttu-id="1b00b-123">Executar o aplicativo hello localmente abrindo uma janela do terminal e usando Olá `Python` servidor de web do comando toolaunch Olá interno Python.</span><span class="sxs-lookup"><span data-stu-id="1b00b-123">Run hello application locally by opening a terminal window and using hello `Python` command toolaunch hello built-in Python web server.</span></span>

```bash
python main.py
```

<span data-ttu-id="1b00b-124">Abra um navegador da web e navegue toohello o aplicativo de exemplo em http://localhost:5000/.</span><span class="sxs-lookup"><span data-stu-id="1b00b-124">Open a web browser, and navigate toohello sample app at http://localhost:5000.</span></span>

<span data-ttu-id="1b00b-125">Você pode ver Olá **Hello World** mensagem do aplicativo de exemplo hello exibida na página de saudação.</span><span class="sxs-lookup"><span data-stu-id="1b00b-125">You can see hello **Hello World** message from hello sample app displayed in hello page.</span></span>

![Aplicativo de exemplo em execução local](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

<span data-ttu-id="1b00b-127">Na janela de terminal, pressione **Ctrl + C** servidor de web tooexit hello.</span><span class="sxs-lookup"><span data-stu-id="1b00b-127">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Página de aplicativo Web vazia](media/app-service-web-get-started-python/app-service-web-service-created.png)

<span data-ttu-id="1b00b-129">Você criou um novo aplicativo Web vazio no Azure.</span><span class="sxs-lookup"><span data-stu-id="1b00b-129">You’ve created an empty new web app in Azure.</span></span>

## <a name="configure-toouse-python"></a><span data-ttu-id="1b00b-130">Configurar toouse Python</span><span class="sxs-lookup"><span data-stu-id="1b00b-130">Configure toouse Python</span></span>

<span data-ttu-id="1b00b-131">Saudação de uso [az webapp config conjunto](/cli/azure/webapp/config#set) versão do Python comando tooconfigure Olá web aplicativo toouse `3.4`.</span><span class="sxs-lookup"><span data-stu-id="1b00b-131">Use hello [az webapp config set](/cli/azure/webapp/config#set) command tooconfigure hello web app toouse Python version `3.4`.</span></span>

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


<span data-ttu-id="1b00b-132">Definindo a versão do Python Olá dessa maneira usa um contêiner padrão fornecido pela plataforma de saudação.</span><span class="sxs-lookup"><span data-stu-id="1b00b-132">Setting hello Python version this way uses a default container provided by hello platform.</span></span> <span data-ttu-id="1b00b-133">toouse seu próprio contêiner, consulte Olá referência CLI para Olá [az webapp config contêiner conjunto](/cli/azure/webapp/config/container#set) comando.</span><span class="sxs-lookup"><span data-stu-id="1b00b-133">toouse your own container, see hello CLI reference for hello [az webapp config container set](/cli/azure/webapp/config/container#set) command.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 18, done.
Delta compression using up too4 threads.
Compressing objects: 100% (16/16), done.
Writing objects: 100% (18/18), 4.31 KiB | 0 bytes/s, done.
Total 18 (delta 4), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '44e74fe7dd'.
remote: Generating deployment script.
remote: Generating deployment script for python Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling python deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'main.py'
remote: Copying file: 'README.md'
remote: Copying file: 'requirements.txt'
remote: Copying file: 'virtualenv_proxy.py'
remote: Copying file: 'web.2.7.config'
remote: Copying file: 'web.3.4.config'
remote: Detected requirements.txt.  You can skip Python specific steps with a .skipPythonDeployment file.
remote: Detecting Python runtime from site configuration
remote: Detected python-3.4
remote: Creating python-3.4 virtual environment.
remote: .................................
remote: Pip install requirements.
remote: Successfully installed Flask click itsdangerous Jinja2 Werkzeug MarkupSafe
remote: Cleaning up...
remote: .
remote: Overwriting web.config with web.3.4.config
remote:         1 file(s) copied.
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="1b00b-134">Procurar toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="1b00b-134">Browse toohello app</span></span>

<span data-ttu-id="1b00b-135">Procure o aplicativo toohello implantado usando o navegador da web.</span><span class="sxs-lookup"><span data-stu-id="1b00b-135">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="1b00b-136">Olá, código de exemplo do Python está em execução em um aplicativo da web do serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b00b-136">hello Python sample code is running in an Azure App Service web app.</span></span>

![Aplicativo de exemplo em execução no Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="1b00b-138">**Parabéns!**</span><span class="sxs-lookup"><span data-stu-id="1b00b-138">**Congratulations!**</span></span> <span data-ttu-id="1b00b-139">Você implantou seu primeiro tooApp de aplicativo Python serviço.</span><span class="sxs-lookup"><span data-stu-id="1b00b-139">You've deployed your first Python app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-code"></a><span data-ttu-id="1b00b-140">Atualize e reimplante o código de saudação</span><span class="sxs-lookup"><span data-stu-id="1b00b-140">Update and redeploy hello code</span></span>

<span data-ttu-id="1b00b-141">Usando um editor de texto local, abra Olá `main.py` arquivo no aplicativo de Python hello e faça toohello de Avançar texto uma pequena alteração toohello `return` instrução:</span><span class="sxs-lookup"><span data-stu-id="1b00b-141">Using a local text editor, open hello `main.py` file in hello Python app, and make a small change toohello text next toohello `return` statement:</span></span>

```python
return 'Hello, Azure!'
```

<span data-ttu-id="1b00b-142">Confirmar as alterações no Git e, em seguida, enviar por push Olá tooAzure de alterações de código.</span><span class="sxs-lookup"><span data-stu-id="1b00b-142">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="1b00b-143">Depois que a implantação for concluída, alternar toohello voltar a janela do navegador é aberto no hello [procurar toohello aplicativo](#browse-to-the-app) etapa e a página de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="1b00b-143">Once deployment has completed, switch back toohello browser window that opened in hello [Browse toohello app](#browse-to-the-app) step, and refresh hello page.</span></span>

![Aplicativo de exemplo atualizado em execução no Azure](media/app-service-web-get-started-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="1b00b-145">Gerenciar seu novo aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="1b00b-145">Manage your new Azure web app</span></span>

<span data-ttu-id="1b00b-146">Vá toohello <a href="https://portal.azure.com" target="_blank">portal do Azure</a> toomanage Olá web aplicativo que você criou.</span><span class="sxs-lookup"><span data-stu-id="1b00b-146">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="1b00b-147">No menu à esquerda do hello, clique em **serviços de aplicativos**e, em seguida, clique em nome de saudação do seu aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b00b-147">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Aplicativo de web de tooAzure de navegação do Portal](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="1b00b-149">A página Visão Geral do seu aplicativo Web é exibida.</span><span class="sxs-lookup"><span data-stu-id="1b00b-149">You see your web app's Overview page.</span></span> <span data-ttu-id="1b00b-150">Aqui você pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir.</span><span class="sxs-lookup"><span data-stu-id="1b00b-150">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Folha Serviço de Aplicativo no portal do Azure](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="1b00b-152">menu esquerdo Olá fornece diferentes páginas para configurar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1b00b-152">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="1b00b-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1b00b-153">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1b00b-154">Python com PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1b00b-154">Python with PostgreSQL</span></span>](app-service-web-tutorial-docker-python-postgresql-app.md)
