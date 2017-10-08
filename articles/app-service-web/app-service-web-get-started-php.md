---
title: aplicativo no Azure da web aaaCreate um PHP | Microsoft Docs
description: "Implante seu primeiro Olá, Mundo em PHP no aplicativo Web do Serviço de Aplicativo do Azure em minutos."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 07/21/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 8e1022889ca162f8f15ce7435cc9393cc6efef06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-web-app-in-azure"></a><span data-ttu-id="52c2a-103">Criar um aplicativo Web do PHP no Azure</span><span class="sxs-lookup"><span data-stu-id="52c2a-103">Create a PHP web app in Azure</span></span>

<span data-ttu-id="52c2a-104">Os [aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches.</span><span class="sxs-lookup"><span data-stu-id="52c2a-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="52c2a-105">Este tutorial de início rápido mostra como toodeploy uma tooAzure do aplicativo PHP aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="52c2a-105">This quickstart tutorial shows how toodeploy a PHP app tooAzure Web Apps.</span></span> <span data-ttu-id="52c2a-106">Criar Olá web app usando Olá [CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) no Shell de nuvem e você usar o Git toodeploy exemplo PHP código toohello web app.</span><span class="sxs-lookup"><span data-stu-id="52c2a-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud Shell, and you use Git toodeploy sample PHP code toohello web app.</span></span>

<span data-ttu-id="52c2a-107">![Aplicativo de exemplo em execução no Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span><span class="sxs-lookup"><span data-stu-id="52c2a-107">![Sample app running in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span></span>

<span data-ttu-id="52c2a-108">Você pode seguir estas etapas hello usando um computador Mac, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="52c2a-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="52c2a-109">Depois que a instalação dos pré-requisitos Olá, são necessárias cerca de cinco minutos toocomplete Olá etapas.</span><span class="sxs-lookup"><span data-stu-id="52c2a-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52c2a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="52c2a-110">Prerequisites</span></span>

<span data-ttu-id="52c2a-111">toocomplete este guia de início rápido:</span><span class="sxs-lookup"><span data-stu-id="52c2a-111">toocomplete this quickstart:</span></span>

* [<span data-ttu-id="52c2a-112">Instalar o Git</span><span class="sxs-lookup"><span data-stu-id="52c2a-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="52c2a-113">Instalar o PHP</span><span class="sxs-lookup"><span data-stu-id="52c2a-113">Install PHP</span></span>](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample-locally"></a><span data-ttu-id="52c2a-114">Baixe o exemplo de hello localmente</span><span class="sxs-lookup"><span data-stu-id="52c2a-114">Download hello sample locally</span></span>

<span data-ttu-id="52c2a-115">Em uma janela de terminal, execute Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="52c2a-115">In a terminal window, run hello following commands.</span></span> <span data-ttu-id="52c2a-116">Isso clonar a máquina local do hello exemplo aplicativo tooyour e navegue toohello diretório contendo Olá exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="52c2a-116">This will clone hello sample application tooyour local machine, and navigate toohello directory containing hello sample code.</span></span>

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="52c2a-117">Executar o aplicativo hello localmente</span><span class="sxs-lookup"><span data-stu-id="52c2a-117">Run hello app locally</span></span>

<span data-ttu-id="52c2a-118">Executar o aplicativo hello localmente abrindo uma janela do terminal e usando Olá `php` servidor de web do comando toolaunch Olá interno PHP.</span><span class="sxs-lookup"><span data-stu-id="52c2a-118">Run hello application locally by opening a terminal window and using hello `php` command toolaunch hello built-in PHP web server.</span></span>

```bash
php -S localhost:8080
```

<span data-ttu-id="52c2a-119">Abra um navegador da web e navegue toohello o aplicativo de exemplo no http://localhost:8080.</span><span class="sxs-lookup"><span data-stu-id="52c2a-119">Open a web browser, and navigate toohello sample app at http://localhost:8080.</span></span>

<span data-ttu-id="52c2a-120">Consulte Olá **Olá, mundo!**</span><span class="sxs-lookup"><span data-stu-id="52c2a-120">You see hello **Hello World!**</span></span> <span data-ttu-id="52c2a-121">mensagem do aplicativo de exemplo hello exibida na página de saudação.</span><span class="sxs-lookup"><span data-stu-id="52c2a-121">message from hello sample app displayed in hello page.</span></span>

![Aplicativo de exemplo em execução local](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

<span data-ttu-id="52c2a-123">Na janela de terminal, pressione **Ctrl + C** servidor de web tooexit hello.</span><span class="sxs-lookup"><span data-stu-id="52c2a-123">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Página de aplicativo Web vazia](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="52c2a-125">Você criou um novo aplicativo Web vazio no Azure.</span><span class="sxs-lookup"><span data-stu-id="52c2a-125">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up too4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 352 bytes | 0 bytes/s, done.
Total 2 (delta 1), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '25f18051e9'.
remote: Generating deployment script.
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.php'
remote: Ignoring: .git
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-toohello-app-locally"></a><span data-ttu-id="52c2a-126">Procurar toohello aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="52c2a-126">Browse toohello app locally</span></span>

<span data-ttu-id="52c2a-127">Procure o aplicativo toohello implantado usando o navegador da web.</span><span class="sxs-lookup"><span data-stu-id="52c2a-127">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="52c2a-128">Olá, código de exemplo do PHP está em execução em um aplicativo da web do serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="52c2a-128">hello PHP sample code is running in an Azure App Service web app.</span></span>

![Aplicativo de exemplo em execução no Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

<span data-ttu-id="52c2a-130">**Parabéns!**</span><span class="sxs-lookup"><span data-stu-id="52c2a-130">**Congratulations!**</span></span> <span data-ttu-id="52c2a-131">Você implantou seu primeiro tooApp de aplicativo PHP serviço.</span><span class="sxs-lookup"><span data-stu-id="52c2a-131">You've deployed your first PHP app tooApp Service.</span></span>

## <a name="update-locally-and-redeploy-hello-code"></a><span data-ttu-id="52c2a-132">Atualize localmente e reimplante o código de saudação</span><span class="sxs-lookup"><span data-stu-id="52c2a-132">Update locally and redeploy hello code</span></span>

<span data-ttu-id="52c2a-133">Usando um editor de texto local, abra Olá `index.php` arquivo no aplicativo do PHP hello e fazer com que uma pequena alteração toohello texto dentro de cadeia de caracteres de saudação Avançar muito`echo`:</span><span class="sxs-lookup"><span data-stu-id="52c2a-133">Using a local text editor, open hello `index.php` file within hello PHP app, and make a small change toohello text within hello string next too`echo`:</span></span>

```php
echo "Hello Azure!";
```

<span data-ttu-id="52c2a-134">Confirmar as alterações no Git e, em seguida, enviar por push Olá tooAzure de alterações de código.</span><span class="sxs-lookup"><span data-stu-id="52c2a-134">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="52c2a-135">Depois que a implantação for concluída, alternar toohello voltar a janela do navegador é aberto no hello **procurar toohello aplicativo** etapa e a página de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="52c2a-135">Once deployment has completed, switch back toohello browser window that opened in hello **Browse toohello app** step, and refresh hello page.</span></span>

![Aplicativo de exemplo atualizado em execução no Azure](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="52c2a-137">Gerenciar seu novo aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="52c2a-137">Manage your new Azure web app</span></span>

<span data-ttu-id="52c2a-138">Vá toohello <a href="https://portal.azure.com" target="_blank">portal do Azure</a> toomanage Olá web aplicativo que você criou.</span><span class="sxs-lookup"><span data-stu-id="52c2a-138">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="52c2a-139">No menu à esquerda do hello, clique em **serviços de aplicativos**e, em seguida, clique em nome de saudação do seu aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="52c2a-139">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Aplicativo de web de tooAzure de navegação do Portal](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

<span data-ttu-id="52c2a-141">A página Visão Geral do seu aplicativo Web é exibida.</span><span class="sxs-lookup"><span data-stu-id="52c2a-141">You see your web app's Overview page.</span></span> <span data-ttu-id="52c2a-142">Aqui você pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir.</span><span class="sxs-lookup"><span data-stu-id="52c2a-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span>

![Folha Serviço de Aplicativo no portal do Azure](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

<span data-ttu-id="52c2a-144">menu esquerdo Olá fornece diferentes páginas para configurar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="52c2a-144">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="52c2a-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="52c2a-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="52c2a-146">PHP com MySQL</span><span class="sxs-lookup"><span data-stu-id="52c2a-146">PHP with MySQL</span></span>](app-service-web-tutorial-php-mysql.md)
