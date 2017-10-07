---
title: aaaCreate um aplicativo Ruby com aplicativos Web no Linux | Microsoft Docs
description: Saiba toocreate Ruby aplicativos com wpp web do Azure no Linux.
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
ms.openlocfilehash: 99ce3b5ee16703a147787387bb02973defce8190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a><span data-ttu-id="bf95c-104">Criar um aplicativo Ruby com aplicativos Web no Linux</span><span class="sxs-lookup"><span data-stu-id="bf95c-104">Create a Ruby App with Web Apps on Linux</span></span> 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="bf95c-105">Os [aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches.</span><span class="sxs-lookup"><span data-stu-id="bf95c-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="bf95c-106">Este guia de início rápido mostra como toocreate um básico aplicativo Ruby on Rails, em seguida, implantá-lo tooAzure como um aplicativo Web no Linux.</span><span class="sxs-lookup"><span data-stu-id="bf95c-106">This quickstart shows you how toocreate a basic Ruby on Rails application you then deploy it tooAzure as a Web App on Linux.</span></span>

![Olá, Mundo](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a><span data-ttu-id="bf95c-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bf95c-108">Prerequisites</span></span>

* <span data-ttu-id="bf95c-109">[Ruby 2.4.1 ou superior](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span><span class="sxs-lookup"><span data-stu-id="bf95c-109">[Ruby 2.4.1 or higher](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span></span>
* <span data-ttu-id="bf95c-110">[Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="bf95c-110">[Git](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="bf95c-111">Uma [assinatura ativa do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bf95c-111">An [active Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a><span data-ttu-id="bf95c-112">Baixe o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="bf95c-112">Download hello sample</span></span>

<span data-ttu-id="bf95c-113">Em uma janela de terminal, execute Olá comando tooclone Olá aplicativo repositório tooyour local máquina de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf95c-113">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine:</span></span>

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-hello-application-locally"></a><span data-ttu-id="bf95c-114">Executar o aplicativo hello localmente</span><span class="sxs-lookup"><span data-stu-id="bf95c-114">Run hello application locally</span></span>

<span data-ttu-id="bf95c-115">Servidor de trilhos de saudação são executados na ordem para toowork de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="bf95c-115">Run hello rails server in order for hello application toowork.</span></span> <span data-ttu-id="bf95c-116">Alterar toohello *Olá mundo* diretório e hello `rails server` comando inicia Olá server.</span><span class="sxs-lookup"><span data-stu-id="bf95c-116">Change toohello *hello-world* directory, and hello `rails server` command starts hello server.</span></span>

```bash
cd hello-world\bin
rails server
```
    
<span data-ttu-id="bf95c-117">Usando o navegador da web, navegue muito`http://localhost:3000` tootest aplicativo de saudação localmente.</span><span class="sxs-lookup"><span data-stu-id="bf95c-117">Using your web browser, navigate too`http://localhost:3000` tootest hello app locally.</span></span>  

![Olá, Mundo](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-toodisplay-welcome-message"></a><span data-ttu-id="bf95c-119">Modifique a mensagem de boas-vindas do aplicativo toodisplay</span><span class="sxs-lookup"><span data-stu-id="bf95c-119">Modify app toodisplay welcome message</span></span>

<span data-ttu-id="bf95c-120">Modificar o aplicativo hello para ele exibe uma mensagem de boas-vinda.</span><span class="sxs-lookup"><span data-stu-id="bf95c-120">Modify hello application so it displays a welcome message.</span></span> <span data-ttu-id="bf95c-121">Altere controlador do aplicativo hello para que ela retorne a mensagem de saudação toohello como HTML.</span><span class="sxs-lookup"><span data-stu-id="bf95c-121">Change hello application's controller so it returns hello message as HTML toohello browser.</span></span> 

<span data-ttu-id="bf95c-122">Abra *~/workspace/hello-world/app/controllers/application_controller.rb* para edição.</span><span class="sxs-lookup"><span data-stu-id="bf95c-122">Open *~/workspace/hello-world/app/controllers/application_controller.rb* for editing.</span></span> <span data-ttu-id="bf95c-123">Modificar Olá `ApplicationController` toolook de classe como Olá exemplo de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf95c-123">Modify hello `ApplicationController` class toolook like hello following code sample:</span></span>

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

<span data-ttu-id="bf95c-124">Seu aplicativo está configurado.</span><span class="sxs-lookup"><span data-stu-id="bf95c-124">Your app is now configured.</span></span> <span data-ttu-id="bf95c-125">Usando o navegador da web, navegue muito`http://localhost:3000` página de aterrissagem do tooconfirm Olá raiz.</span><span class="sxs-lookup"><span data-stu-id="bf95c-125">Using your web browser, navigate too`http://localhost:3000` tooconfirm hello root landing page.</span></span>

![Olá, Mundo configurado](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a><span data-ttu-id="bf95c-127">Criar um aplicativo Web Ruby no Azure</span><span class="sxs-lookup"><span data-stu-id="bf95c-127">Create a Ruby web app on Azure</span></span>

<span data-ttu-id="bf95c-128">Saudação de uso [criar plano de serviço de aplicativo az](https://docs.microsoft.com/cli/azure/appservice/plan#create) comando toocreate um plano de serviço de aplicativo para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="bf95c-128">Use hello [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) command toocreate an app service plan for your web app.</span></span> 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

<span data-ttu-id="bf95c-129">Em seguida, emitir Olá [az webapp criar](https://docs.microsoft.com/cli/azure/webapp) comando toocreate Olá web aplicativo que usa o plano de serviço Olá recém-criado.</span><span class="sxs-lookup"><span data-stu-id="bf95c-129">Next, issue hello [az webapp create](https://docs.microsoft.com/cli/azure/webapp) command toocreate hello web app that uses hello newly created service plan.</span></span> <span data-ttu-id="bf95c-130">Observe que tempo de execução hello está definido muito`ruby|2.3`.</span><span class="sxs-lookup"><span data-stu-id="bf95c-130">Notice that hello runtime is set too`ruby|2.3`.</span></span> <span data-ttu-id="bf95c-131">Não se esqueça de tooreplace `<app name>` com um nome exclusivo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bf95c-131">Don't forget tooreplace `<app name>` with a unique app name.</span></span>

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

<span data-ttu-id="bf95c-132">Depois de criar aplicativo web de saudação, um **visão geral** página é tooview disponível.</span><span class="sxs-lookup"><span data-stu-id="bf95c-132">Once hello web app is created, an **Overview** page is available tooview.</span></span> <span data-ttu-id="bf95c-133">Navegue tooit.</span><span class="sxs-lookup"><span data-stu-id="bf95c-133">Navigate tooit.</span></span> <span data-ttu-id="bf95c-134">Olá após a página inicial é exibida:</span><span class="sxs-lookup"><span data-stu-id="bf95c-134">hello following splash page is displayed:</span></span>

![Página inicial](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a><span data-ttu-id="bf95c-136">Implantar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="bf95c-136">Deploy your application</span></span>

<span data-ttu-id="bf95c-137">Use Git toodeploy Olá aplicativo Ruby tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bf95c-137">Use Git toodeploy hello Ruby application tooAzure.</span></span> <span data-ttu-id="bf95c-138">aplicativo web de saudação já tem uma implantação do Git configurada.</span><span class="sxs-lookup"><span data-stu-id="bf95c-138">hello web app already has a Git deployment configured.</span></span> <span data-ttu-id="bf95c-139">Você pode recuperar a URL de implantação Olá emitindo um [implantação de aplicativo Web az](https://docs.microsoft.com/cli/azure/webapp/deployment) comando.</span><span class="sxs-lookup"><span data-stu-id="bf95c-139">You can retrieve hello deployment URL by issuing an [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment) command.</span></span>  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="bf95c-140">Observe que Olá URL de Git tem Olá formulário com base no nome do aplicativo da web a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf95c-140">Notice that hello Git URL has hello following form based on your web app name:</span></span>

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

<span data-ttu-id="bf95c-141">Execute Olá comandos toodeploy Olá aplicativo local tooyour site do Azure a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf95c-141">Run hello following commands toodeploy hello local application tooyour Azure website:</span></span>

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="bf95c-142">Confirme que o relatório de operações de implantação remota Olá sucesso.</span><span class="sxs-lookup"><span data-stu-id="bf95c-142">Confirm that hello remote deployment operations report success.</span></span> <span data-ttu-id="bf95c-143">Olá comandos produzir saída semelhante toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf95c-143">hello commands produce output similar toohello following text:</span></span>

```bash
remote: Using sass-rails 5.0.6
remote: Updating files in vendor/cache
remote: Bundle gems are installed into ./vendor/bundle
remote: Updating files in vendor/cache
remote: ~site/repository
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<your web app name>.scm.azurewebsites.net/<your web app name>.git
  579ccb....2ca5f31  master -> master
myuser@ubuntu1234:~workspace/<app name>$
```

<span data-ttu-id="bf95c-144">Após a conclusão da implantação hello, reinicie seu aplicativo web para efeito de tootake implantação hello usando Olá [reinicialização do webapp az](https://docs.microsoft.com/cli/azure/webapp#restart) de comando, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="bf95c-144">Once hello deployment has completed, restart your web app for hello deployment tootake effect by using hello [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart) command, as shown here:</span></span>

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="bf95c-145">Navegue tooyour site e verificar os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf95c-145">Navigate tooyour site and verify hello results.</span></span>

```bash
http://<your web app name>.azurewebsites.net
```
![aplicativo web atualizado](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> <span data-ttu-id="bf95c-147">Enquanto o aplicativo hello está reiniciando, tentativa de resultados de site Olá toobrowse em um código de status HTTP `Error 503 Server unavailable`.</span><span class="sxs-lookup"><span data-stu-id="bf95c-147">While hello app is restarting, attempting toobrowse hello site results in an HTTP status code `Error 503 Server unavailable`.</span></span> <span data-ttu-id="bf95c-148">Pode levar alguns minutos toofully reinicialização.</span><span class="sxs-lookup"><span data-stu-id="bf95c-148">It may take a few minutes toofully restart.</span></span>
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a><span data-ttu-id="bf95c-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bf95c-149">Next steps</span></span>

[<span data-ttu-id="bf95c-150">Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="bf95c-150">Azure App Service Web App on Linux FAQ</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)