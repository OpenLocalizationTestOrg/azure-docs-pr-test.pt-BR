---
title: "Exemplo de script da CLI do Azure - Criar um aplicativo Web do ASP.NET Core em um contêiner de encaixe do registro de contêiner do Azure | Microsoft Docs"
description: "Exemplo de script da CLI do Azure - Criar um aplicativo Web do ASP.NET Core em um contêiner de encaixe do registro de contêiner do Azure"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 3a2d1983-ff7b-476a-ac44-49ec2aabb31a
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 2556947d7cdd1475ae82ac2e1d61ad30ebd0d29f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container-from-azure-container-registry"></a><span data-ttu-id="f8959-103">Criar um aplicativo Web do ASP.NET Core em um contêiner de encaixe do registro de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="f8959-103">Create an ASP.NET Core web app in a Docker container from Azure Container Registry</span></span>

<span data-ttu-id="f8959-104">Nesse cenário, você aprenderá como criar um grupo de recursos, o Plano do Serviço de Aplicativo do Linux e o aplicativo Web e implantar um aplicativo ASP.NET Core usando um contêiner de encaixe do registro do contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8959-104">In this scenario you will learn how to create a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container from the Azure Container Registry.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f8959-105">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f8959-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f8959-106">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="f8959-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="f8959-107">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f8959-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f8959-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="f8959-108">Sample script</span></span>

<span data-ttu-id="f8959-109">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/deploy-linux-acr/deploy-linux-acr.sh?highlight=6-9 "Registro de Contêiner do Azure")]</span><span class="sxs-lookup"><span data-stu-id="f8959-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-acr/deploy-linux-acr.sh?highlight=6-9 "Linux Azure Container Registry")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f8959-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="f8959-110">Script explanation</span></span>

<span data-ttu-id="f8959-111">Este script usa os seguintes comandos para criar um grupo de recursos, um aplicativo Web e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="f8959-111">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="f8959-112">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="f8959-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f8959-113">Command</span><span class="sxs-lookup"><span data-stu-id="f8959-113">Command</span></span> | <span data-ttu-id="f8959-114">Observações</span><span class="sxs-lookup"><span data-stu-id="f8959-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f8959-115">az group create</span><span class="sxs-lookup"><span data-stu-id="f8959-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f8959-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="f8959-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f8959-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="f8959-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="f8959-118">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f8959-118">Creates an App Service plan.</span></span> <span data-ttu-id="f8959-119">Isso é como um farm de servidores para seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8959-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="f8959-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="f8959-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="f8959-121">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8959-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="f8959-122">az webapp config container set</span><span class="sxs-lookup"><span data-stu-id="f8959-122">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="f8959-123">Define o contêiner do Docker para o aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8959-123">Sets the Docker container for the Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f8959-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f8959-124">Next steps</span></span>

<span data-ttu-id="f8959-125">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f8959-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f8959-126">Os exemplos de script da CLI do Serviço de Aplicativo adicionais podem ser encontrados na [documentação do Serviço de Aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f8959-126">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
