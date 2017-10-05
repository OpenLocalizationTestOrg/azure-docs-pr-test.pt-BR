---
title: "Implantação contínua com o Aplicativo Web do Azure no Linux | Microsoft Docs"
description: "Como configurar a implantação contínua no Aplicativo Web do Azure no Linux."
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
ms.openlocfilehash: f8f7d51003f8a55b7f51e8cc2cea838e8e5a6196
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a><span data-ttu-id="ca040-104">Implantação contínua com o Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="ca040-104">Continuous deployment with Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="ca040-105">Neste tutorial, você configura a implantação contínua para uma imagem de contêiner personalizada de repositórios do [Registro de Contêiner do Azure](https://azure.microsoft.com/en-us/services/container-registry/) Gerenciado ou do [Hub do Docker](https://hub.docker.com).</span><span class="sxs-lookup"><span data-stu-id="ca040-105">In this tutorial, you configure continuous deployment for a custom container image from Managed [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) repositories or [Docker Hub](https://hub.docker.com).</span></span>

## <a name="step-1---sign-in-to-azure"></a><span data-ttu-id="ca040-106">Etapa 1– entrar no Azure</span><span class="sxs-lookup"><span data-stu-id="ca040-106">Step 1 - Sign in to Azure</span></span>

<span data-ttu-id="ca040-107">Entrar no Portal do Azure em http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="ca040-107">Sign in to the Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---enable-container-continuous-deployment-feature"></a><span data-ttu-id="ca040-108">Etapa 2 – Habilitar recurso de implantação contínua do contêiner</span><span class="sxs-lookup"><span data-stu-id="ca040-108">Step 2 - Enable container continuous deployment feature</span></span>

<span data-ttu-id="ca040-109">Você pode habilitar o recurso de implantação contínua usando a [CLI do Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) e executando o seguinte comando</span><span class="sxs-lookup"><span data-stu-id="ca040-109">You can enable the continuous deployment feature using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing the following command</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

<span data-ttu-id="ca040-110">No  **[portal do Azure](https://portal.azure.com/)**, clique a opção **Serviço de Aplicativo** à esquerda da página.</span><span class="sxs-lookup"><span data-stu-id="ca040-110">In the **[Azure portal](https://portal.azure.com/)**, click the **App Service** option on the left of the page.</span></span>

<span data-ttu-id="ca040-111">Clique no nome do aplicativo para o qual você deseja configurar a implantação contínua do Hub do Docker.</span><span class="sxs-lookup"><span data-stu-id="ca040-111">Click on the name of your app that you want to configure Docker Hub continuous deployment for.</span></span>

<span data-ttu-id="ca040-112">Nas **Configurações do aplicativo**, adicione uma configuração de aplicativo chamada `DOCKER_ENABLE_CI` com o valor `true`.</span><span class="sxs-lookup"><span data-stu-id="ca040-112">In the **App settings**, add an app setting called `DOCKER_ENABLE_CI` with the value `true`.</span></span>

![inserir imagem da configuração de aplicativo](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a><span data-ttu-id="ca040-114">Etapa 3 – preparar a URL do Webhook</span><span class="sxs-lookup"><span data-stu-id="ca040-114">Step 3 - Prepare Webhook URL</span></span>

<span data-ttu-id="ca040-115">Você pode obter a URL do Webhook usando a [CLI do Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) e executando o seguinte comando</span><span class="sxs-lookup"><span data-stu-id="ca040-115">You can obtain the Webhook URL using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing the following command</span></span>

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

<span data-ttu-id="ca040-116">Para a URL do Webhook, você precisa ter o seguinte ponto de extremidade: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span><span class="sxs-lookup"><span data-stu-id="ca040-116">For the Webhook URL, you need to have the following endpoint: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span></span>

<span data-ttu-id="ca040-117">Você pode obter seu `publishingusername` e `publishingpwd` baixando o perfil de publicação do aplicativo Web usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ca040-117">You can obtain your `publishingusername` and `publishingpwd` by downloading the web app publish profile using the Azure portal.</span></span>

![inserir imagem da adição do webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a><span data-ttu-id="ca040-119">Etapa 4 – adicionar um webhook</span><span class="sxs-lookup"><span data-stu-id="ca040-119">Step 4 - Add a web hook</span></span>

### <a name="azure-container-registry"></a><span data-ttu-id="ca040-120">Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="ca040-120">Azure Container Registry</span></span>

<span data-ttu-id="ca040-121">Na sua folha de portal de registro, clique em **Webhooks** e crie um novo webhook clicando em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ca040-121">In your registry portal blade, click **Webhooks**, create a new webhook by clicking **Add**.</span></span> <span data-ttu-id="ca040-122">Na folha **Criar webhook**, nomeie o webhook.</span><span class="sxs-lookup"><span data-stu-id="ca040-122">In the **Create webhook** blade, give your webhook a name.</span></span> <span data-ttu-id="ca040-123">Para o URI do Webhook, você precisa fornecer a URL obtida na **Etapa 3**</span><span class="sxs-lookup"><span data-stu-id="ca040-123">For the Webhook URI, you need to provide the URL obtained from **Step 3**</span></span>

<span data-ttu-id="ca040-124">Verifique se você definiu o escopo como o repositório que contém a imagem de contêiner.</span><span class="sxs-lookup"><span data-stu-id="ca040-124">Make sure that you define the scope as the repo that contains your container image.</span></span>

![inserir imagem de webhook](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

<span data-ttu-id="ca040-126">Quando a imagem é atualizada, o aplicativo Web é atualizado automaticamente com a nova imagem.</span><span class="sxs-lookup"><span data-stu-id="ca040-126">When the image gets updated, the web app get updated automatically with the new image.</span></span>

### <a name="docker-hub"></a><span data-ttu-id="ca040-127">Hub do Docker</span><span class="sxs-lookup"><span data-stu-id="ca040-127">Docker Hub</span></span>

<span data-ttu-id="ca040-128">Na página do Hub do Docker, clique em **Webhooks** e, em seguida, em **CRIAR UM WEBHOOK**.</span><span class="sxs-lookup"><span data-stu-id="ca040-128">In your Docker Hub page, click **Webhooks**, then **CREATE A WEBHOOK**.</span></span>

![inserir imagem da adição do webhook 1](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

<span data-ttu-id="ca040-130">Para a URL do Webhook, você precisa fornecer a URL obtida na **Etapa 3**</span><span class="sxs-lookup"><span data-stu-id="ca040-130">For the Webhook URL, you need to provide the URL obtained from **Step 3**</span></span>

![inserir imagem da adição do webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

<span data-ttu-id="ca040-132">Quando a imagem é atualizada, o aplicativo Web é atualizado automaticamente com a nova imagem.</span><span class="sxs-lookup"><span data-stu-id="ca040-132">When the image gets updated, the web app get updated automatically with the new image.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca040-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ca040-133">Next steps</span></span>
* [<span data-ttu-id="ca040-134">O que é um Aplicativo Web do Azure no Linux?</span><span class="sxs-lookup"><span data-stu-id="ca040-134">What is Azure Web App on Linux?</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="ca040-135">Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="ca040-135">Azure Container Registry</span></span>](https://azure.microsoft.com/en-us/services/container-registry/)
* [<span data-ttu-id="ca040-136">Usando a configuração de PM2 para Node.js no Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="ca040-136">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="ca040-137">Usando o .NET Core no Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="ca040-137">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="ca040-138">Usando Ruby no Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="ca040-138">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="ca040-139">Como usar uma imagem personalizada do Docker para o Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="ca040-139">How to use a custom Docker image for Azure Web App on Linux</span></span>](./app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="ca040-140">Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="ca040-140">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md) 
* [<span data-ttu-id="ca040-141">Gerenciar o aplicativo Web no Linux usando a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="ca040-141">Manage Web App on Linux using Azure CLI 2.0</span></span>](./app-service-linux-cli.md)



