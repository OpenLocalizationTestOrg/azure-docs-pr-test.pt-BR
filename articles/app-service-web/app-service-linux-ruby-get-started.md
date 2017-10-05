---
title: Criar um aplicativo Ruby com aplicativos Web no Linux | Microsoft Docs
description: Saiba como criar aplicativos Ruby com o aplicativo Web do Azure no Linux.
keywords: "serviço de aplicativo do azure, linux, oss, ruby"
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 6d00c73c-13cb-446f-8926-923db4101afa
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: wesmc;rachelap
ms.openlocfilehash: 17f3f1a2122c508501134a0c43ab6abce412fb44
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a><span data-ttu-id="b76d3-104">Criar um aplicativo Ruby com aplicativos Web no Linux</span><span class="sxs-lookup"><span data-stu-id="b76d3-104">Create a Ruby App with Web Apps on Linux</span></span> 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="b76d3-105">Os [aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches.</span><span class="sxs-lookup"><span data-stu-id="b76d3-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="b76d3-106">Este guia de início rápido mostra como criar um aplicativo Ruby on Rails básico e implantá-lo no Azure como um aplicativo Web no Linux.</span><span class="sxs-lookup"><span data-stu-id="b76d3-106">This quickstart shows you how to create a basic Ruby on Rails application you then deploy it to Azure as a Web App on Linux.</span></span>

![Olá, Mundo](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a><span data-ttu-id="b76d3-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b76d3-108">Prerequisites</span></span>

* <span data-ttu-id="b76d3-109">[Ruby 2.4.1 ou superior](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span><span class="sxs-lookup"><span data-stu-id="b76d3-109">[Ruby 2.4.1 or higher](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span></span>
* <span data-ttu-id="b76d3-110">[Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="b76d3-110">[Git](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="b76d3-111">Uma [assinatura ativa do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b76d3-111">An [active Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample"></a><span data-ttu-id="b76d3-112">Baixar o exemplo</span><span class="sxs-lookup"><span data-stu-id="b76d3-112">Download the sample</span></span>

<span data-ttu-id="b76d3-113">Em uma janela de terminal, execute o comando a seguir para clonar o repositório do aplicativo de exemplo para o computador local:</span><span class="sxs-lookup"><span data-stu-id="b76d3-113">In a terminal window, run the following command to clone the sample app repository to your local machine:</span></span>

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-the-application-locally"></a><span data-ttu-id="b76d3-114">Executar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="b76d3-114">Run the application locally</span></span>

<span data-ttu-id="b76d3-115">Execute o servidor de trilhos para que o aplicativo funcione.</span><span class="sxs-lookup"><span data-stu-id="b76d3-115">Run the rails server in order for the application to work.</span></span> <span data-ttu-id="b76d3-116">Altere para o diretório *hello-world* e o comando `rails server` iniciará o servidor.</span><span class="sxs-lookup"><span data-stu-id="b76d3-116">Change to the *hello-world* directory, and the `rails server` command starts the server.</span></span>

```bash
cd hello-world\bin
rails server
```
    
<span data-ttu-id="b76d3-117">Usando o navegador da Web, navegue até `http://localhost:3000` para testar o aplicativo localmente.</span><span class="sxs-lookup"><span data-stu-id="b76d3-117">Using your web browser, navigate to `http://localhost:3000` to test the app locally.</span></span>    

![Olá, Mundo](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-to-display-welcome-message"></a><span data-ttu-id="b76d3-119">Modificar o aplicativo para exibir a mensagem de boas-vindas</span><span class="sxs-lookup"><span data-stu-id="b76d3-119">Modify app to display welcome message</span></span>

<span data-ttu-id="b76d3-120">Modifique o aplicativo para que ele exiba uma mensagem de boas-vindas.</span><span class="sxs-lookup"><span data-stu-id="b76d3-120">Modify the application so it displays a welcome message.</span></span> <span data-ttu-id="b76d3-121">Altere o controlador do aplicativo para que ele retorne a mensagem como HTML para o navegador.</span><span class="sxs-lookup"><span data-stu-id="b76d3-121">Change the application's controller so it returns the message as HTML to the browser.</span></span> 

<span data-ttu-id="b76d3-122">Abra *~/workspace/hello-world/app/controllers/application_controller.rb* para edição.</span><span class="sxs-lookup"><span data-stu-id="b76d3-122">Open *~/workspace/hello-world/app/controllers/application_controller.rb* for editing.</span></span> <span data-ttu-id="b76d3-123">Modifique a classe `ApplicationController` para que ela se assemelhe ao seguinte exemplo de código:</span><span class="sxs-lookup"><span data-stu-id="b76d3-123">Modify the `ApplicationController` class to look like the following code sample:</span></span>

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

<span data-ttu-id="b76d3-124">Seu aplicativo está configurado.</span><span class="sxs-lookup"><span data-stu-id="b76d3-124">Your app is now configured.</span></span> <span data-ttu-id="b76d3-125">Usando o navegador da Web, navegue até `http://localhost:3000` para confirmar a página inicial de raiz.</span><span class="sxs-lookup"><span data-stu-id="b76d3-125">Using your web browser, navigate to `http://localhost:3000` to confirm the root landing page.</span></span>

![Olá, Mundo configurado](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a><span data-ttu-id="b76d3-127">Criar um aplicativo Web Ruby no Azure</span><span class="sxs-lookup"><span data-stu-id="b76d3-127">Create a Ruby web app on Azure</span></span>

<span data-ttu-id="b76d3-128">Use o comando [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) para criar um plano de serviço de aplicativo para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="b76d3-128">Use the [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) command to create an app service plan for your web app.</span></span> 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

<span data-ttu-id="b76d3-129">Em seguida, execute o comando [az webapp create](https://docs.microsoft.com/cli/azure/webapp) para criar o aplicativo Web que usa o plano de serviço recém-criado.</span><span class="sxs-lookup"><span data-stu-id="b76d3-129">Next, issue the [az webapp create](https://docs.microsoft.com/cli/azure/webapp) command to create the web app that uses the newly created service plan.</span></span> <span data-ttu-id="b76d3-130">Observe que o tempo de execução é definido como `ruby|2.3`.</span><span class="sxs-lookup"><span data-stu-id="b76d3-130">Notice that the runtime is set to `ruby|2.3`.</span></span> <span data-ttu-id="b76d3-131">Não se esqueça de substituir `<app name>` por um nome exclusivo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b76d3-131">Don't forget to replace `<app name>` with a unique app name.</span></span>

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

<span data-ttu-id="b76d3-132">Após um aplicativo Web ser criado, uma página de **Visão geral** ficará disponível para exibição.</span><span class="sxs-lookup"><span data-stu-id="b76d3-132">Once the web app is created, an **Overview** page is available to view.</span></span> <span data-ttu-id="b76d3-133">Navegue até ela.</span><span class="sxs-lookup"><span data-stu-id="b76d3-133">Navigate to it.</span></span> <span data-ttu-id="b76d3-134">A seguinte página inicial é exibida:</span><span class="sxs-lookup"><span data-stu-id="b76d3-134">The following splash page is displayed:</span></span>

![Página inicial](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a><span data-ttu-id="b76d3-136">Implantar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="b76d3-136">Deploy your application</span></span>

<span data-ttu-id="b76d3-137">Use o Git para implantar o aplicativo Ruby no Azure.</span><span class="sxs-lookup"><span data-stu-id="b76d3-137">Use Git to deploy the Ruby application to Azure.</span></span> <span data-ttu-id="b76d3-138">O aplicativo Web já tem uma implantação do Git configurada.</span><span class="sxs-lookup"><span data-stu-id="b76d3-138">The web app already has a Git deployment configured.</span></span> <span data-ttu-id="b76d3-139">Você pode recuperar a URL de implantação emitindo um comando [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment).</span><span class="sxs-lookup"><span data-stu-id="b76d3-139">You can retrieve the deployment URL by issuing an [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment) command.</span></span>  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="b76d3-140">Observe que a URL do Git tem o seguinte formato, com base no nome do seu aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="b76d3-140">Notice that the Git URL has the following form based on your web app name:</span></span>

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

<span data-ttu-id="b76d3-141">Execute os seguintes comandos para implantar o aplicativo local em seu site do Azure:</span><span class="sxs-lookup"><span data-stu-id="b76d3-141">Run the following commands to deploy the local application to your Azure website:</span></span>

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="b76d3-142">Confirme que as operações de implantação remota relatam êxito.</span><span class="sxs-lookup"><span data-stu-id="b76d3-142">Confirm that the remote deployment operations report success.</span></span> <span data-ttu-id="b76d3-143">Os comandos produzem uma saída semelhante ao texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="b76d3-143">The commands produce output similar to the following text:</span></span>

```bash
remote: Using sass-rails 5.0.6
remote: Updating files in vendor/cache
remote: Bundle gems are installed into ./vendor/bundle
remote: Updating files in vendor/cache
remote: ~site/repository
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
  579ccb....2ca5f31  master -> master
myuser@ubuntu1234:~workspace/<app name>$
```

<span data-ttu-id="b76d3-144">Depois que a implantação for concluída, reinicie o aplicativo Web para a implantação entrar em vigor usando o comando [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart), conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="b76d3-144">Once the deployment has completed, restart your web app for the deployment to take effect by using the [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart) command, as shown here:</span></span>

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="b76d3-145">Navegue até o site e verifique os resultados.</span><span class="sxs-lookup"><span data-stu-id="b76d3-145">Navigate to your site and verify the results.</span></span>

```bash
http://<your web app name>.azurewebsites.net
```
![aplicativo web atualizado](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> <span data-ttu-id="b76d3-147">Enquanto o aplicativo estiver reiniciando, tentar navegar pelo site leva a um código de status HTTP `Error 503 Server unavailable`.</span><span class="sxs-lookup"><span data-stu-id="b76d3-147">While the app is restarting, attempting to browse the site results in an HTTP status code `Error 503 Server unavailable`.</span></span> <span data-ttu-id="b76d3-148">Pode levar alguns minutos para reiniciar completamente.</span><span class="sxs-lookup"><span data-stu-id="b76d3-148">It may take a few minutes to fully restart.</span></span>
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a><span data-ttu-id="b76d3-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b76d3-149">Next steps</span></span>

[<span data-ttu-id="b76d3-150">Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="b76d3-150">Azure App Service Web App on Linux FAQ</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)