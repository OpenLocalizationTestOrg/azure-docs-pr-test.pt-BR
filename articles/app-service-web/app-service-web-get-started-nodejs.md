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
# <a name="create-a-nodejs-web-app-in-azure"></a>Criar um aplicativo Web do Node.js no Azure

Os [aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches.  Este guia de início rápido mostra como toodeploy uma tooAzure de aplicativo Node. js aplicativos Web. Criar Olá web app usando Olá [CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), e você usa o Git toodeploy exemplo Node. js código toohello web app.

![Aplicativo de exemplo em execução no Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

Você pode seguir estas etapas hello usando um computador Mac, Windows ou Linux. Depois que a instalação dos pré-requisitos Olá, são necessárias cerca de cinco minutos toocomplete Olá etapas.   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a>Pré-requisitos

toocomplete este guia de início rápido:

* [Instalar o Git](https://git-scm.com/)
* [Instalar o Node.js e o NPM](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Baixe o exemplo hello

Em uma janela de terminal, execute Olá comando tooclone Olá aplicativo repositório tooyour local máquina de exemplo a seguir.

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

Use essa janela do terminal toorun todos os comandos de saudação neste guia de início rápido.

Altere o diretório de toohello que contém o código de exemplo hello.

```bash
cd nodejs-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Executar o aplicativo hello localmente

Executar o aplicativo hello localmente abrindo uma janela do terminal e usando Olá `npm start` Olá toolaunch de script criado no servidor HTTP Node. js.

```bash
npm start
```

Abra um navegador da web e navegue toohello o aplicativo de exemplo no http://localhost:1337.

Consulte Olá **Hello World** mensagem do aplicativo de exemplo hello exibida na página de saudação.

![Aplicativo de exemplo em execução local](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

Na janela de terminal, pressione **Ctrl + C** servidor de web tooexit hello.

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Página de aplicativo Web vazia](media/app-service-web-get-started-php/app-service-web-service-created.png)

Você criou um novo aplicativo Web vazio no Azure.

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

## <a name="browse-toohello-app"></a>Procurar toohello aplicativo

Procure o aplicativo toohello implantado usando o navegador da web.

```bash
http://<app_name>.azurewebsites.net
```

Olá Node. js código de exemplo está em execução em um aplicativo da web do serviço de aplicativo do Azure.

![Aplicativo de exemplo em execução no Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

**Parabéns!** Você implantou seu primeiro tooApp de aplicativo Node. js serviço.

## <a name="update-and-redeploy-hello-code"></a>Atualize e reimplante o código de saudação

Usando um editor de texto, abra Olá `index.js` arquivo no aplicativo de Node. js hello e fazer uma pequena alteração de texto toohello na chamada de saudação muito`response.end`:

```nodejs
response.end("Hello Azure!");
```

Confirmar as alterações no Git e, em seguida, enviar por push Olá tooAzure de alterações de código.

```bash
git commit -am "updated output"
git push azure master
```

Depois que a implantação for concluída, alternar toohello voltar a janela do navegador é aberto no hello **procurar toohello aplicativo** etapa e clique em Atualizar.

![Aplicativo de exemplo atualizado em execução no Azure](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>Gerenciar seu novo aplicativo Web do Azure

Vá toohello <a href="https://portal.azure.com" target="_blank">portal do Azure</a> toomanage Olá web aplicativo que você criou.

No menu à esquerda do hello, clique em **serviços de aplicativos**e, em seguida, clique em nome de saudação do seu aplicativo web do Azure.

![Aplicativo de web de tooAzure de navegação do Portal](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

A página Visão Geral do seu aplicativo Web é exibida. Aqui você pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir. 

![Folha Serviço de Aplicativo no portal do Azure](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

menu esquerdo Olá fornece diferentes páginas para configurar seu aplicativo. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Node.js com o MongoDB](app-service-web-tutorial-nodejs-mongodb-app.md)
