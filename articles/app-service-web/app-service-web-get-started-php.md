---
title: Criar um aplicativo Web PHP no Azure | Microsoft Docs
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
ms.openlocfilehash: 3a78e0b485046ad6228bf4819d3908042c298d1a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-php-web-app-in-azure"></a><span data-ttu-id="1197f-103">Criar um aplicativo Web do PHP no Azure</span><span class="sxs-lookup"><span data-stu-id="1197f-103">Create a PHP web app in Azure</span></span>

<span data-ttu-id="1197f-104">Os [aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches.</span><span class="sxs-lookup"><span data-stu-id="1197f-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="1197f-105">Este tutorial de início rápido mostra como implantar um aplicativo PHP em Aplicativos Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="1197f-105">This quickstart tutorial shows how to deploy a PHP app to Azure Web Apps.</span></span> <span data-ttu-id="1197f-106">Crie o aplicativo Web usando a [CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) no Cloud Shell e use o Git para implantar o código PHP de exemplo para o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="1197f-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud Shell, and you use Git to deploy sample PHP code to the web app.</span></span>

<span data-ttu-id="1197f-107">![Aplicativo de exemplo em execução no Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span><span class="sxs-lookup"><span data-stu-id="1197f-107">![Sample app running in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span></span>

<span data-ttu-id="1197f-108">Você pode seguir as etapas abaixo usando um computador Mac, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="1197f-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="1197f-109">A conclusão das etapas demora cerca de cinco minutos assim que os pré-requisitos são instalados.</span><span class="sxs-lookup"><span data-stu-id="1197f-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1197f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1197f-110">Prerequisites</span></span>

<span data-ttu-id="1197f-111">Para concluir este guia de início rápido:</span><span class="sxs-lookup"><span data-stu-id="1197f-111">To complete this quickstart:</span></span>

* [<span data-ttu-id="1197f-112">Instalar o Git</span><span class="sxs-lookup"><span data-stu-id="1197f-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="1197f-113">Instalar o PHP</span><span class="sxs-lookup"><span data-stu-id="1197f-113">Install PHP</span></span>](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample-locally"></a><span data-ttu-id="1197f-114">Baixar o exemplo localmente</span><span class="sxs-lookup"><span data-stu-id="1197f-114">Download the sample locally</span></span>

<span data-ttu-id="1197f-115">Em uma janela de terminal, execute os comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="1197f-115">In a terminal window, run the following commands.</span></span> <span data-ttu-id="1197f-116">Isso clonará o aplicativo de exemplo no computador local e fará com que você navegue até o diretório que contém o código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="1197f-116">This will clone the sample application to your local machine, and navigate to the directory containing the sample code.</span></span>

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="1197f-117">Executar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="1197f-117">Run the app locally</span></span>

<span data-ttu-id="1197f-118">Execute o aplicativo localmente abrindo uma janela do terminal e usando o comando `php` para iniciar o servidor interno da Web do PHP.</span><span class="sxs-lookup"><span data-stu-id="1197f-118">Run the application locally by opening a terminal window and using the `php` command to launch the built-in PHP web server.</span></span>

```bash
php -S localhost:8080
```

<span data-ttu-id="1197f-119">Abra um navegador da Web e navegue até o aplicativo de exemplo no http://localhost:8080.</span><span class="sxs-lookup"><span data-stu-id="1197f-119">Open a web browser, and navigate to the sample app at http://localhost:8080.</span></span>

<span data-ttu-id="1197f-120">Você verá o **Olá, Mundo!**</span><span class="sxs-lookup"><span data-stu-id="1197f-120">You see the **Hello World!**</span></span> <span data-ttu-id="1197f-121">mensagem do aplicativo de exemplo exibida na página.</span><span class="sxs-lookup"><span data-stu-id="1197f-121">message from the sample app displayed in the page.</span></span>

![Aplicativo de exemplo em execução local](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

<span data-ttu-id="1197f-123">Na janela do terminal, pressione **Ctrl+C** para sair do servidor Web.</span><span class="sxs-lookup"><span data-stu-id="1197f-123">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Página de aplicativo Web vazia](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="1197f-125">Você criou um novo aplicativo Web vazio no Azure.</span><span class="sxs-lookup"><span data-stu-id="1197f-125">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up to 4 threads.
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
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-to-the-app-locally"></a><span data-ttu-id="1197f-126">Navegar até o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="1197f-126">Browse to the app locally</span></span>

<span data-ttu-id="1197f-127">Navegue até o aplicativo implantado usando o navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="1197f-127">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="1197f-128">O código de exemplo do PHP está em execução em um aplicativo Web do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="1197f-128">The PHP sample code is running in an Azure App Service web app.</span></span>

![Aplicativo de exemplo em execução no Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

<span data-ttu-id="1197f-130">**Parabéns!**</span><span class="sxs-lookup"><span data-stu-id="1197f-130">**Congratulations!**</span></span> <span data-ttu-id="1197f-131">Você implantou seu primeiro aplicativo PHP no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1197f-131">You've deployed your first PHP app to App Service.</span></span>

## <a name="update-locally-and-redeploy-the-code"></a><span data-ttu-id="1197f-132">Atualizar localmente e reimplantar o código</span><span class="sxs-lookup"><span data-stu-id="1197f-132">Update locally and redeploy the code</span></span>

<span data-ttu-id="1197f-133">Usando um editor de texto local, abra o arquivo `index.php` no aplicativo do PHP e faça uma pequena alteração no texto dentro da cadeia de caracteres para `echo`:</span><span class="sxs-lookup"><span data-stu-id="1197f-133">Using a local text editor, open the `index.php` file within the PHP app, and make a small change to the text within the string next to `echo`:</span></span>

```php
echo "Hello Azure!";
```

<span data-ttu-id="1197f-134">Confirme suas alterações no Git e, em seguida, envie as alterações de código por push para o Azure.</span><span class="sxs-lookup"><span data-stu-id="1197f-134">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="1197f-135">Depois que a implantação for concluída, troque para a janela do navegador aberta na etapa **Navegar até o aplicativo** e atualize a página.</span><span class="sxs-lookup"><span data-stu-id="1197f-135">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and refresh the page.</span></span>

![Aplicativo de exemplo atualizado em execução no Azure](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="1197f-137">Gerenciar seu novo aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="1197f-137">Manage your new Azure web app</span></span>

<span data-ttu-id="1197f-138">Vá para o <a href="https://portal.azure.com" target="_blank">portal do Azure</a> para gerenciar o aplicativo Web que você criou.</span><span class="sxs-lookup"><span data-stu-id="1197f-138">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="1197f-139">No menu à esquerda, clique em **Serviços de Aplicativos** e então clique no nome do seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="1197f-139">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Navegação do portal para o aplicativo Web do Azure](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

<span data-ttu-id="1197f-141">A página Visão Geral do seu aplicativo Web é exibida.</span><span class="sxs-lookup"><span data-stu-id="1197f-141">You see your web app's Overview page.</span></span> <span data-ttu-id="1197f-142">Aqui você pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir.</span><span class="sxs-lookup"><span data-stu-id="1197f-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span>

![Folha Serviço de Aplicativo no portal do Azure](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

<span data-ttu-id="1197f-144">O menu à esquerda fornece páginas diferentes para configurar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1197f-144">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="1197f-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1197f-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1197f-146">PHP com MySQL</span><span class="sxs-lookup"><span data-stu-id="1197f-146">PHP with MySQL</span></span>](app-service-web-tutorial-php-mysql.md)
