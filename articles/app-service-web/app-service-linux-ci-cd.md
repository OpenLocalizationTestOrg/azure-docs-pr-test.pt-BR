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
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a><span data-ttu-id="9245e-104">Implantação contínua com o Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="9245e-104">Continuous deployment with Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="9245e-105">Neste tutorial, você configura a implantação contínua para uma imagem de contêiner personalizada de repositórios do [Registro de Contêiner do Azure](https://azure.microsoft.com/en-us/services/container-registry/) Gerenciado ou do [Hub do Docker](https://hub.docker.com).</span><span class="sxs-lookup"><span data-stu-id="9245e-105">In this tutorial, you configure continuous deployment for a custom container image from Managed [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) repositories or [Docker Hub](https://hub.docker.com).</span></span>

## <a name="step-1---sign-in-tooazure"></a><span data-ttu-id="9245e-106">Etapa 1: entrar tooAzure</span><span class="sxs-lookup"><span data-stu-id="9245e-106">Step 1 - Sign in tooAzure</span></span>

<span data-ttu-id="9245e-107">Entrar portal do Azure em http://portal.azure.com toohello</span><span class="sxs-lookup"><span data-stu-id="9245e-107">Sign in toohello Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---enable-container-continuous-deployment-feature"></a><span data-ttu-id="9245e-108">Etapa 2 – Habilitar recurso de implantação contínua do contêiner</span><span class="sxs-lookup"><span data-stu-id="9245e-108">Step 2 - Enable container continuous deployment feature</span></span>

<span data-ttu-id="9245e-109">Você pode habilitar Olá implantação contínua usando o recurso [CLI do Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) e executar Olá comando a seguir</span><span class="sxs-lookup"><span data-stu-id="9245e-109">You can enable hello continuous deployment feature using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

<span data-ttu-id="9245e-110">Em hello  **[portal do Azure](https://portal.azure.com/)**, clique em Olá **do serviço de aplicativo** opção esquerda Olá da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="9245e-110">In hello **[Azure portal](https://portal.azure.com/)**, click hello **App Service** option on hello left of hello page.</span></span>

<span data-ttu-id="9245e-111">Clique no nome de saudação do aplicativo que você deseja tooconfigure implantação contínua do Hub do Docker para.</span><span class="sxs-lookup"><span data-stu-id="9245e-111">Click on hello name of your app that you want tooconfigure Docker Hub continuous deployment for.</span></span>

<span data-ttu-id="9245e-112">Em Olá **configurações do aplicativo**, adicionar um aplicativo de chamada `DOCKER_ENABLE_CI` com valor de saudação `true`.</span><span class="sxs-lookup"><span data-stu-id="9245e-112">In hello **App settings**, add an app setting called `DOCKER_ENABLE_CI` with hello value `true`.</span></span>

![inserir imagem da configuração de aplicativo](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a><span data-ttu-id="9245e-114">Etapa 3 – preparar a URL do Webhook</span><span class="sxs-lookup"><span data-stu-id="9245e-114">Step 3 - Prepare Webhook URL</span></span>

<span data-ttu-id="9245e-115">Você pode obter usando o URL do Webhook Olá [CLI do Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) e executar Olá comando a seguir</span><span class="sxs-lookup"><span data-stu-id="9245e-115">You can obtain hello Webhook URL using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

<span data-ttu-id="9245e-116">Para Olá a URL do Webhook, você precisa toohave Olá ponto de extremidade a seguir: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span><span class="sxs-lookup"><span data-stu-id="9245e-116">For hello Webhook URL, you need toohave hello following endpoint: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span></span>

<span data-ttu-id="9245e-117">Você pode obter seu `publishingusername` e `publishingpwd` baixando Olá web app usando Olá portal do Azure de perfil de publicação.</span><span class="sxs-lookup"><span data-stu-id="9245e-117">You can obtain your `publishingusername` and `publishingpwd` by downloading hello web app publish profile using hello Azure portal.</span></span>

![inserir imagem da adição do webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a><span data-ttu-id="9245e-119">Etapa 4 – adicionar um webhook</span><span class="sxs-lookup"><span data-stu-id="9245e-119">Step 4 - Add a web hook</span></span>

### <a name="azure-container-registry"></a><span data-ttu-id="9245e-120">Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="9245e-120">Azure Container Registry</span></span>

<span data-ttu-id="9245e-121">Na sua folha de portal de registro, clique em **Webhooks** e crie um novo webhook clicando em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9245e-121">In your registry portal blade, click **Webhooks**, create a new webhook by clicking **Add**.</span></span> <span data-ttu-id="9245e-122">Em Olá **criar webhook** folha, nomeie o webhook.</span><span class="sxs-lookup"><span data-stu-id="9245e-122">In hello **Create webhook** blade, give your webhook a name.</span></span> <span data-ttu-id="9245e-123">Para Olá Webhook URI, você precisa tooprovide Olá URL obtido **etapa 3**</span><span class="sxs-lookup"><span data-stu-id="9245e-123">For hello Webhook URI, you need tooprovide hello URL obtained from **Step 3**</span></span>

<span data-ttu-id="9245e-124">Certifique-se de que você definir o escopo de saudação como Olá repositório que contém a imagem de contêiner.</span><span class="sxs-lookup"><span data-stu-id="9245e-124">Make sure that you define hello scope as hello repo that contains your container image.</span></span>

![inserir imagem de webhook](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

<span data-ttu-id="9245e-126">Quando a imagem de saudação é atualizada, Olá web aplicativo são atualizados automaticamente com a nova imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="9245e-126">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

### <a name="docker-hub"></a><span data-ttu-id="9245e-127">Hub do Docker</span><span class="sxs-lookup"><span data-stu-id="9245e-127">Docker Hub</span></span>

<span data-ttu-id="9245e-128">Na página do Hub do Docker, clique em **Webhooks** e, em seguida, em **CRIAR UM WEBHOOK**.</span><span class="sxs-lookup"><span data-stu-id="9245e-128">In your Docker Hub page, click **Webhooks**, then **CREATE A WEBHOOK**.</span></span>

![inserir imagem da adição do webhook 1](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

<span data-ttu-id="9245e-130">Para Olá a URL do Webhook, você precisa tooprovide Olá URL obtido **etapa 3**</span><span class="sxs-lookup"><span data-stu-id="9245e-130">For hello Webhook URL, you need tooprovide hello URL obtained from **Step 3**</span></span>

![inserir imagem da adição do webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

<span data-ttu-id="9245e-132">Quando a imagem de saudação é atualizada, Olá web aplicativo são atualizados automaticamente com a nova imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="9245e-132">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9245e-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9245e-133">Next steps</span></span>
* [<span data-ttu-id="9245e-134">O que é um Aplicativo Web do Azure no Linux?</span><span class="sxs-lookup"><span data-stu-id="9245e-134">What is Azure Web App on Linux?</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="9245e-135">Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="9245e-135">Azure Container Registry</span></span>](https://azure.microsoft.com/en-us/services/container-registry/)
* [<span data-ttu-id="9245e-136">Usando a configuração de PM2 para Node.js no Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="9245e-136">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="9245e-137">Usando o .NET Core no Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="9245e-137">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="9245e-138">Usando Ruby no Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="9245e-138">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="9245e-139">Como toouse um Docker personalizado da imagem para o aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="9245e-139">How toouse a custom Docker image for Azure Web App on Linux</span></span>](./app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="9245e-140">Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="9245e-140">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md) 
* [<span data-ttu-id="9245e-141">Gerenciar o aplicativo Web no Linux usando a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="9245e-141">Manage Web App on Linux using Azure CLI 2.0</span></span>](./app-service-linux-cli.md)



