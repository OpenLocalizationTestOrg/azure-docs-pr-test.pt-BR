---
title: aaaManage Web App no Linux usando o Azure CLI 2.0 | Microsoft Docs
description: Gerenciar o aplicativo Web no Linux usando a CLI do Azure.
keywords: "serviço de aplicativo do azure, aplicativo web, cli, linux, oss"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: aelnably
ms.openlocfilehash: 5e8e0da8a362450c56d2e87e087f77598ec874ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a><span data-ttu-id="637c3-104">Gerenciar o aplicativo Web no Linux usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="637c3-104">Manage Web App on Linux using Azure CLI</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="637c3-105">Usando os comandos de saudação neste artigo são toocreate capaz e gerenciar um aplicativo Web no Linux usando 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="637c3-105">Using hello commands in this article you are able toocreate and manage a Web App on Linux using Azure CLI 2.0.</span></span>
<span data-ttu-id="637c3-106">Você pode começar a usar a nova versão Olá de saudação CLI de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="637c3-106">You can start using hello new version of hello CLI in two ways:</span></span>

* <span data-ttu-id="637c3-107">[Instalando a CLI do Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) em seu computador.</span><span class="sxs-lookup"><span data-stu-id="637c3-107">[Installing Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span>
* <span data-ttu-id="637c3-108">Usando o [Azure Cloud Shell (versão prévia)](../cloud-shell/overview.md)</span><span class="sxs-lookup"><span data-stu-id="637c3-108">Using [Azure Cloud Shell (Preview)](../cloud-shell/overview.md)</span></span>


## <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="637c3-109">Criar um Plano do Serviço de Aplicativo do Linux</span><span class="sxs-lookup"><span data-stu-id="637c3-109">Create a Linux App Service Plan</span></span>

<span data-ttu-id="637c3-110">toocreate um plano de serviço de aplicativo do Linux, você pode usar o hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="637c3-110">toocreate a Linux App Service Plan, you can use hello following command:</span></span>

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a><span data-ttu-id="637c3-111">Criar um aplicativo Web de contêiner do Docker personalizado</span><span class="sxs-lookup"><span data-stu-id="637c3-111">Create a custom Docker container Web App</span></span>

<span data-ttu-id="637c3-112">toocreate um aplicativo web e configurá-lo toorun um contêiner do Docker personalizado, você pode usar o hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="637c3-112">toocreate a web app and configuring it toorun a custom Docker container, you can use hello following command:</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-hello-docker-container-logging"></a><span data-ttu-id="637c3-113">Ativar o log de contêiner do Docker Olá</span><span class="sxs-lookup"><span data-stu-id="637c3-113">Activate hello Docker container logging</span></span>

<span data-ttu-id="637c3-114">tooactivate Olá log do contêiner Docker, você pode usar o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="637c3-114">tooactivate hello Docker container logging, you can use hello following command:</span></span>

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-hello-custom-docker-container-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="637c3-115">Alterar o contêiner de Docker Olá personalizado para um aplicativo Web existente no Linux App</span><span class="sxs-lookup"><span data-stu-id="637c3-115">Change hello custom Docker container for an existing Web App on Linux App</span></span>

<span data-ttu-id="637c3-116">toochange um aplicativo criado anteriormente, de saudação atual Docker imagem tooa nova imagem, você pode usar o hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="637c3-116">toochange a previously created app, from hello current Docker image tooa new image, you can use hello following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a><span data-ttu-id="637c3-117">Usando imagens do Docker de um registro particular</span><span class="sxs-lookup"><span data-stu-id="637c3-117">Using Docker images from a private registry</span></span>

<span data-ttu-id="637c3-118">Você pode configurar suas imagens de toouse do aplicativo de um registro particular.</span><span class="sxs-lookup"><span data-stu-id="637c3-118">You can configure your app toouse images from a private registry.</span></span> <span data-ttu-id="637c3-119">Você precisa tooprovide Olá url para o registro, o nome de usuário e a senha.</span><span class="sxs-lookup"><span data-stu-id="637c3-119">You need tooprovide hello url for your registry, user name, and password.</span></span> <span data-ttu-id="637c3-120">Isso pode ser obtido usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="637c3-120">This can be achieved using hello following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a><span data-ttu-id="637c3-121">Habilitar implantações contínuas para imagens personalizadas do Docker</span><span class="sxs-lookup"><span data-stu-id="637c3-121">Enable continuous deployments for custom Docker images</span></span>

<span data-ttu-id="637c3-122">Com o comando a seguir de saudação habilitar a funcionalidade de CD hello e obter a url do webhook hello.</span><span class="sxs-lookup"><span data-stu-id="637c3-122">With hello following command you can enable hello CD functionality, and get hello webhook url.</span></span> <span data-ttu-id="637c3-123">Essa url pode ser usado tooconfigure você DockerHub ou registro de contêiner do Azure repositórios.</span><span class="sxs-lookup"><span data-stu-id="637c3-123">This url can be used tooconfigure you DockerHub or Azure Container Registry repos.</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a><span data-ttu-id="637c3-124">Criar um aplicativo Web no aplicativo Linux usando uma de nossas estruturas de tempo de execução internas</span><span class="sxs-lookup"><span data-stu-id="637c3-124">Create a Web App on Linux App using one of our built-in runtime frameworks</span></span>

<span data-ttu-id="637c3-125">toocreate um aplicativo de Web PHP 5.6 na App Linux que, você pode usar o hello comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="637c3-125">toocreate a PHP 5.6 Web App on Linux App that, you can use hello following command.</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="637c3-126">Alterar a versão da estrutura de um aplicativo Web existente no aplicativo Linux</span><span class="sxs-lookup"><span data-stu-id="637c3-126">Change framework version for an existing Web App on Linux App</span></span>

<span data-ttu-id="637c3-127">toochange um aplicativo criado anteriormente, de saudação atual do framework versão tooNode.js 6.11, você pode usar o hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="637c3-127">toochange a previously created app, from hello current framework version tooNode.js 6.11, you can use hello following command:</span></span>

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a><span data-ttu-id="637c3-128">Configurar implantações do Git para seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="637c3-128">Set up Git deployments for your Web App</span></span>

<span data-ttu-id="637c3-129">tooset as implantações do Git para seu aplicativo, você pode usar o hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="637c3-129">tooset up Git deployments for your app, you can use hello following command:</span></span>

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a><span data-ttu-id="637c3-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="637c3-130">Next steps</span></span>
* [<span data-ttu-id="637c3-131">O que é um Aplicativo Web do Azure no Linux?</span><span class="sxs-lookup"><span data-stu-id="637c3-131">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="637c3-132">Instalar a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="637c3-132">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [<span data-ttu-id="637c3-133">Azure Cloud Shell (versão prévia)</span><span class="sxs-lookup"><span data-stu-id="637c3-133">Azure Cloud Shell (Preview)</span></span>](../cloud-shell/overview.md)
* [<span data-ttu-id="637c3-134">Configurar ambientes de preparo no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="637c3-134">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="637c3-135">Implantação contínua com o Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="637c3-135">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
