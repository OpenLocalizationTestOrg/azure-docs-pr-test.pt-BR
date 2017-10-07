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
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a>Criar um aplicativo Ruby com aplicativos Web no Linux 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

Os [aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches. Este guia de início rápido mostra como toocreate um básico aplicativo Ruby on Rails, em seguida, implantá-lo tooAzure como um aplicativo Web no Linux.

![Olá, Mundo](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a>Pré-requisitos

* [Ruby 2.4.1 ou superior](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).
* [Git](https://git-scm.com/downloads).
* Uma [assinatura ativa do Azure](https://azure.microsoft.com/pricing/free-trial/).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a>Baixe o exemplo hello

Em uma janela de terminal, execute Olá comando tooclone Olá aplicativo repositório tooyour local máquina de exemplo a seguir:

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-hello-application-locally"></a>Executar o aplicativo hello localmente

Servidor de trilhos de saudação são executados na ordem para toowork de aplicativo hello. Alterar toohello *Olá mundo* diretório e hello `rails server` comando inicia Olá server.

```bash
cd hello-world\bin
rails server
```
    
Usando o navegador da web, navegue muito`http://localhost:3000` tootest aplicativo de saudação localmente.  

![Olá, Mundo](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-toodisplay-welcome-message"></a>Modifique a mensagem de boas-vindas do aplicativo toodisplay

Modificar o aplicativo hello para ele exibe uma mensagem de boas-vinda. Altere controlador do aplicativo hello para que ela retorne a mensagem de saudação toohello como HTML. 

Abra *~/workspace/hello-world/app/controllers/application_controller.rb* para edição. Modificar Olá `ApplicationController` toolook de classe como Olá exemplo de código a seguir:

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

Seu aplicativo está configurado. Usando o navegador da web, navegue muito`http://localhost:3000` página de aterrissagem do tooconfirm Olá raiz.

![Olá, Mundo configurado](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a>Criar um aplicativo Web Ruby no Azure

Saudação de uso [criar plano de serviço de aplicativo az](https://docs.microsoft.com/cli/azure/appservice/plan#create) comando toocreate um plano de serviço de aplicativo para seu aplicativo web. 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

Em seguida, emitir Olá [az webapp criar](https://docs.microsoft.com/cli/azure/webapp) comando toocreate Olá web aplicativo que usa o plano de serviço Olá recém-criado. Observe que tempo de execução hello está definido muito`ruby|2.3`. Não se esqueça de tooreplace `<app name>` com um nome exclusivo do aplicativo.

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

Depois de criar aplicativo web de saudação, um **visão geral** página é tooview disponível. Navegue tooit. Olá após a página inicial é exibida:

![Página inicial](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a>Implantar seu aplicativo

Use Git toodeploy Olá aplicativo Ruby tooAzure. aplicativo web de saudação já tem uma implantação do Git configurada. Você pode recuperar a URL de implantação Olá emitindo um [implantação de aplicativo Web az](https://docs.microsoft.com/cli/azure/webapp/deployment) comando.  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

Observe que Olá URL de Git tem Olá formulário com base no nome do aplicativo da web a seguir:

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

Execute Olá comandos toodeploy Olá aplicativo local tooyour site do Azure a seguir:

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

Confirme que o relatório de operações de implantação remota Olá sucesso. Olá comandos produzir saída semelhante toohello texto a seguir:

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

Após a conclusão da implantação hello, reinicie seu aplicativo web para efeito de tootake implantação hello usando Olá [reinicialização do webapp az](https://docs.microsoft.com/cli/azure/webapp#restart) de comando, conforme mostrado aqui:

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

Navegue tooyour site e verificar os resultados de saudação.

```bash
http://<your web app name>.azurewebsites.net
```
![aplicativo web atualizado](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> Enquanto o aplicativo hello está reiniciando, tentativa de resultados de site Olá toobrowse em um código de status HTTP `Error 503 Server unavailable`. Pode levar alguns minutos toofully reinicialização.
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a>Próximas etapas

[Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)