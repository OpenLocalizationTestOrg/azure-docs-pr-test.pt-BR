---
title: "aplicativo web de aaaCreate uma HTML estática no Azure | Microsoft Docs"
description: "Saiba como o aplicativo de exemplo toorun aplicativos de web no serviço de aplicativo do Azure Implantando uma HTML estático."
services: app-service\web
documentationcenter: 
author: rick-anderson
manager: wpickett
editor: 
ms.assetid: 60495cc5-6963-4bf0-8174-52786d226c26
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/26/2017
ms.author: riande
ms.custom: mvc
ms.openlocfilehash: efd8c8189a3aa1ac35602b688eeb31bff6f5a373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a>Criar um aplicativo Web HTML estático no Azure

Os [aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches.  Este guia de início rápido mostra como toodeploy básica HTML + CSS site tooAzure os aplicativos Web. Criar Olá web app usando Olá [CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), e você usar o aplicativo de web de conteúdo toohello Git toodeploy exemplo HTML.

![Home page do aplicativo de exemplo](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

Você pode seguir estas etapas hello usando um computador Mac, Windows ou Linux. Depois que a instalação dos pré-requisitos Olá, são necessárias cerca de cinco minutos toocomplete Olá etapas.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete este guia de início rápido:

- [Instalar o Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Baixe o exemplo hello

Em uma janela de terminal, execute Olá comando tooclone Olá aplicativo repositório tooyour local máquina de exemplo a seguir.

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

Use essa janela do terminal toorun todos os comandos de saudação neste guia de início rápido.

## <a name="view-hello-html"></a>Saudação de exibição HTML

Navegue toohello diretório que contém o exemplo hello HTML. Olá abrir *index.html* arquivo no seu navegador.

![Home page do aplicativo de exemplo](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Página de aplicativo Web vazia](media/app-service-web-get-started-html/app-service-web-service-created.png)

Você criou um novo aplicativo Web vazio no Azure.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up too4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (13/13), 2.07 KiB | 0 bytes/s, done.
Total 13 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'cc39b1e4cb'.
remote: Generating deployment script.
remote: Generating deployment script for Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a>Procurar toohello aplicativo

Em um navegador, acesse a URL do aplicativo web do Azure toohello:

```
http://<app_name>.azurewebsites.net
```

página Hello está sendo executado como um aplicativo da web do serviço de aplicativo do Azure.

![Home page do aplicativo de exemplo](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

**Parabéns!** Você implantou seu primeiro tooApp de aplicativo HTML Service.

## <a name="update-and-redeploy-hello-app"></a>Atualize e reimplante o aplicativo hello

Olá abrir *index* do arquivo em um editor de texto e fazer uma marcação de toohello de alteração. Por exemplo, altere o título do hello H1 de "Azure aplicativo de serviço – exemplo estático HTML Site" toojust "serviço de aplicativo do Azure'.

Confirmar as alterações no Git e, em seguida, enviar por push Olá tooAzure de alterações de código.

```bash
git commit -am "updated HTML"
git push azure master
```

Depois que a implantação for concluída, atualize as alterações de saudação do navegador toosee.

![Home page do aplicativo de exemplo atualizada](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a>Gerenciar seu novo aplicativo Web do Azure

Vá toohello <a href="https://portal.azure.com" target="_blank">portal do Azure</a> toomanage Olá web aplicativo que você criou.

No menu à esquerda do hello, clique em **serviços de aplicativos**e, em seguida, clique em nome de saudação do seu aplicativo web do Azure.

![Aplicativo de web de tooAzure de navegação do Portal](./media/app-service-web-get-started-html/portal1.png)

A página Visão Geral do seu aplicativo Web é exibida. Aqui você pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir. 

![Folha Serviço de Aplicativo no portal do Azure](./media/app-service-web-get-started-html/portal2.png)

menu esquerdo Olá fornece diferentes páginas para configurar seu aplicativo. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Mapear domínio personalizado](app-service-web-tutorial-custom-domain.md)
