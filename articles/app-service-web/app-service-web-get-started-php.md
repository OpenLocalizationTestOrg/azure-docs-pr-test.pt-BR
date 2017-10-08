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
# <a name="create-a-php-web-app-in-azure"></a>Criar um aplicativo Web do PHP no Azure

Os [aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches.  Este tutorial de início rápido mostra como toodeploy uma tooAzure do aplicativo PHP aplicativos Web. Criar Olá web app usando Olá [CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) no Shell de nuvem e você usar o Git toodeploy exemplo PHP código toohello web app.

![Aplicativo de exemplo em execução no Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)

Você pode seguir estas etapas hello usando um computador Mac, Windows ou Linux. Depois que a instalação dos pré-requisitos Olá, são necessárias cerca de cinco minutos toocomplete Olá etapas.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete este guia de início rápido:

* [Instalar o Git](https://git-scm.com/)
* [Instalar o PHP](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample-locally"></a>Baixe o exemplo de hello localmente

Em uma janela de terminal, execute Olá comandos a seguir. Isso clonar a máquina local do hello exemplo aplicativo tooyour e navegue toohello diretório contendo Olá exemplo de código.

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Executar o aplicativo hello localmente

Executar o aplicativo hello localmente abrindo uma janela do terminal e usando Olá `php` servidor de web do comando toolaunch Olá interno PHP.

```bash
php -S localhost:8080
```

Abra um navegador da web e navegue toohello o aplicativo de exemplo no http://localhost:8080.

Consulte Olá **Olá, mundo!** mensagem do aplicativo de exemplo hello exibida na página de saudação.

![Aplicativo de exemplo em execução local](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

Na janela de terminal, pressione **Ctrl + C** servidor de web tooexit hello.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Página de aplicativo Web vazia](media/app-service-web-get-started-php/app-service-web-service-created.png)

Você criou um novo aplicativo Web vazio no Azure.

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

## <a name="browse-toohello-app-locally"></a>Procurar toohello aplicativo localmente

Procure o aplicativo toohello implantado usando o navegador da web.

```bash
http://<app_name>.azurewebsites.net
```

Olá, código de exemplo do PHP está em execução em um aplicativo da web do serviço de aplicativo do Azure.

![Aplicativo de exemplo em execução no Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

**Parabéns!** Você implantou seu primeiro tooApp de aplicativo PHP serviço.

## <a name="update-locally-and-redeploy-hello-code"></a>Atualize localmente e reimplante o código de saudação

Usando um editor de texto local, abra Olá `index.php` arquivo no aplicativo do PHP hello e fazer com que uma pequena alteração toohello texto dentro de cadeia de caracteres de saudação Avançar muito`echo`:

```php
echo "Hello Azure!";
```

Confirmar as alterações no Git e, em seguida, enviar por push Olá tooAzure de alterações de código.

```bash
git commit -am "updated output"
git push azure master
```

Depois que a implantação for concluída, alternar toohello voltar a janela do navegador é aberto no hello **procurar toohello aplicativo** etapa e a página de atualização de saudação.

![Aplicativo de exemplo atualizado em execução no Azure](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>Gerenciar seu novo aplicativo Web do Azure

Vá toohello <a href="https://portal.azure.com" target="_blank">portal do Azure</a> toomanage Olá web aplicativo que você criou.

No menu à esquerda do hello, clique em **serviços de aplicativos**e, em seguida, clique em nome de saudação do seu aplicativo web do Azure.

![Aplicativo de web de tooAzure de navegação do Portal](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

A página Visão Geral do seu aplicativo Web é exibida. Aqui você pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir.

![Folha Serviço de Aplicativo no portal do Azure](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

menu esquerdo Olá fornece diferentes páginas para configurar seu aplicativo. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [PHP com MySQL](app-service-web-tutorial-php-mysql.md)
