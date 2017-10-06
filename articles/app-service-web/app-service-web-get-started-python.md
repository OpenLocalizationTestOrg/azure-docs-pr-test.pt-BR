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
# <a name="create-a-python-web-app-in-azure"></a>Criar um aplicativo Web do Python no Azure

Os [aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches.  Este guia de início rápido orienta como toodevelop e implantar um aplicativo de Python tooAzure aplicativos Web. Criar Olá web app usando Olá [CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), e você usar o aplicativo de web toohello de código Python de exemplo toodeploy de Git.

![Aplicativo de exemplo em execução no Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

Você pode seguir estas etapas hello usando um computador Mac, Windows ou Linux. Depois que a instalação dos pré-requisitos Olá, são necessárias cerca de cinco minutos toocomplete Olá etapas.
## <a name="prerequisites"></a>Pré-requisitos

toocomplete este tutorial:

1. [Instalar o Git](https://git-scm.com/)
1. [Instalar o Python](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Baixe o exemplo hello

Em uma janela de terminal, execute Olá comando tooclone Olá aplicativo repositório tooyour local máquina de exemplo a seguir.

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

Use essa janela do terminal toorun todos os comandos de saudação neste guia de início rápido.

Altere o diretório de toohello que contém o código de exemplo hello.

```bash
cd Python-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Executar o aplicativo hello localmente

Instalar pacotes de saudação necessária usando `pip`.

```bash
pip install -r requirements.txt
```

Executar o aplicativo hello localmente abrindo uma janela do terminal e usando Olá `Python` servidor de web do comando toolaunch Olá interno Python.

```bash
python main.py
```

Abra um navegador da web e navegue toohello o aplicativo de exemplo em http://localhost:5000/.

Você pode ver Olá **Hello World** mensagem do aplicativo de exemplo hello exibida na página de saudação.

![Aplicativo de exemplo em execução local](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

Na janela de terminal, pressione **Ctrl + C** servidor de web tooexit hello.

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Página de aplicativo Web vazia](media/app-service-web-get-started-python/app-service-web-service-created.png)

Você criou um novo aplicativo Web vazio no Azure.

## <a name="configure-toouse-python"></a>Configurar toouse Python

Saudação de uso [az webapp config conjunto](/cli/azure/webapp/config#set) versão do Python comando tooconfigure Olá web aplicativo toouse `3.4`.

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


Definindo a versão do Python Olá dessa maneira usa um contêiner padrão fornecido pela plataforma de saudação. toouse seu próprio contêiner, consulte Olá referência CLI para Olá [az webapp config contêiner conjunto](/cli/azure/webapp/config/container#set) comando.

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

## <a name="browse-toohello-app"></a>Procurar toohello aplicativo

Procure o aplicativo toohello implantado usando o navegador da web.

```bash
http://<app_name>.azurewebsites.net
```

Olá, código de exemplo do Python está em execução em um aplicativo da web do serviço de aplicativo do Azure.

![Aplicativo de exemplo em execução no Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

**Parabéns!** Você implantou seu primeiro tooApp de aplicativo Python serviço.

## <a name="update-and-redeploy-hello-code"></a>Atualize e reimplante o código de saudação

Usando um editor de texto local, abra Olá `main.py` arquivo no aplicativo de Python hello e faça toohello de Avançar texto uma pequena alteração toohello `return` instrução:

```python
return 'Hello, Azure!'
```

Confirmar as alterações no Git e, em seguida, enviar por push Olá tooAzure de alterações de código.

```bash
git commit -am "updated output"
git push azure master
```

Depois que a implantação for concluída, alternar toohello voltar a janela do navegador é aberto no hello [procurar toohello aplicativo](#browse-to-the-app) etapa e a página de atualização de saudação.

![Aplicativo de exemplo atualizado em execução no Azure](media/app-service-web-get-started-python/hello-azure-in-browser.png)

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
> [Python com PostgreSQL](app-service-web-tutorial-docker-python-postgresql-app.md)
