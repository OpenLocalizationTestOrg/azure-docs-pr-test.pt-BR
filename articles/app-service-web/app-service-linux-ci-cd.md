---
title: "aaaContinuous implantação de aplicativo Web do Azure no Linux | Microsoft Docs"
description: "Como toosetup a implantação contínua no aplicativo Web do Azure no Linux."
keywords: "serviço de aplicativo do azure, linux, oss, acr"
services: app-service
documentationcenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: f94d837e27605da58428f507ab2b0eb3af3297e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a>Implantação contínua com o Aplicativo Web do Azure no Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

Neste tutorial, você configura a implantação contínua para uma imagem de contêiner personalizada de repositórios do [Registro de Contêiner do Azure](https://azure.microsoft.com/en-us/services/container-registry/) Gerenciado ou do [Hub do Docker](https://hub.docker.com).

## <a name="step-1---sign-in-tooazure"></a>Etapa 1: entrar tooAzure

Entrar portal do Azure em http://portal.azure.com toohello

## <a name="step-2---enable-container-continuous-deployment-feature"></a>Etapa 2 – Habilitar recurso de implantação contínua do contêiner

Você pode habilitar Olá implantação contínua usando o recurso [CLI do Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) e executar Olá comando a seguir

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

Em hello  **[portal do Azure](https://portal.azure.com/)**, clique em Olá **do serviço de aplicativo** opção esquerda Olá da página de saudação.

Clique no nome de saudação do aplicativo que você deseja tooconfigure implantação contínua do Hub do Docker para.

Em Olá **configurações do aplicativo**, adicionar um aplicativo de chamada `DOCKER_ENABLE_CI` com valor de saudação `true`.

![inserir imagem da configuração de aplicativo](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a>Etapa 3 – preparar a URL do Webhook

Você pode obter usando o URL do Webhook Olá [CLI do Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) e executar Olá comando a seguir

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

Para Olá a URL do Webhook, você precisa toohave Olá ponto de extremidade a seguir: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.

Você pode obter seu `publishingusername` e `publishingpwd` baixando Olá web app usando Olá portal do Azure de perfil de publicação.

![inserir imagem da adição do webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a>Etapa 4 – adicionar um webhook

### <a name="azure-container-registry"></a>Registro de Contêiner do Azure

Na sua folha de portal de registro, clique em **Webhooks** e crie um novo webhook clicando em **Adicionar**. Em Olá **criar webhook** folha, nomeie o webhook. Para Olá Webhook URI, você precisa tooprovide Olá URL obtido **etapa 3**

Certifique-se de que você definir o escopo de saudação como Olá repositório que contém a imagem de contêiner.

![inserir imagem de webhook](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

Quando a imagem de saudação é atualizada, Olá web aplicativo são atualizados automaticamente com a nova imagem de saudação.

### <a name="docker-hub"></a>Hub do Docker

Na página do Hub do Docker, clique em **Webhooks** e, em seguida, em **CRIAR UM WEBHOOK**.

![inserir imagem da adição do webhook 1](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

Para Olá a URL do Webhook, você precisa tooprovide Olá URL obtido **etapa 3**

![inserir imagem da adição do webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

Quando a imagem de saudação é atualizada, Olá web aplicativo são atualizados automaticamente com a nova imagem de saudação.

## <a name="next-steps"></a>Próximas etapas
* [O que é um Aplicativo Web do Azure no Linux?](./app-service-linux-intro.md)
* [Registro de Contêiner do Azure](https://azure.microsoft.com/en-us/services/container-registry/)
* [Usando a configuração de PM2 para Node.js no Aplicativo Web do Azure no Linux](app-service-linux-using-nodejs-pm2.md)
* [Usando o .NET Core no Aplicativo Web do Azure no Linux](app-service-linux-using-dotnetcore.md)
* [Usando Ruby no Aplicativo Web do Azure no Linux](app-service-linux-ruby-get-started.md)
* [Como toouse um Docker personalizado da imagem para o aplicativo Web do Azure no Linux](./app-service-linux-using-custom-docker-image.md)
* [Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux](./app-service-linux-faq.md) 
* [Gerenciar o aplicativo Web no Linux usando a CLI do Azure 2.0](./app-service-linux-cli.md)



