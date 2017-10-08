---
title: "aaaAzure exemplo de Script CLI - criar um aplicativo web do ASP.NET Core em um contêiner de Docker de registro de contêiner do Azure | Microsoft Docs"
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
ms.openlocfilehash: 0d4b1e706c2401ef813f48ef4de3d17fa2b6c9e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container-from-azure-container-registry"></a><span data-ttu-id="6f592-103">Criar um aplicativo Web do ASP.NET Core em um contêiner de encaixe do registro de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="6f592-103">Create an ASP.NET Core web app in a Docker container from Azure Container Registry</span></span>

<span data-ttu-id="6f592-104">Nesse cenário, você aprenderá como toocreate um grupo de recursos, o aplicativo Linux plano e o aplicativo web de serviço e implantar um aplicativo do ASP.NET Core usando um contêiner do Docker de saudação do registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="6f592-104">In this scenario you will learn how toocreate a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container from hello Azure Container Registry.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6f592-105">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="6f592-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6f592-106">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="6f592-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6f592-107">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6f592-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6f592-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="6f592-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-acr/deploy-linux-acr.sh?highlight=6-9 "Linux Azure Container Registry")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="6f592-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="6f592-109">Script explanation</span></span>

<span data-ttu-id="6f592-110">Esse script usa Olá comandos toocreate um grupo de recursos, aplicativo web e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="6f592-110">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="6f592-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="6f592-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6f592-112">Command</span><span class="sxs-lookup"><span data-stu-id="6f592-112">Command</span></span> | <span data-ttu-id="6f592-113">Observações</span><span class="sxs-lookup"><span data-stu-id="6f592-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6f592-114">az group create</span><span class="sxs-lookup"><span data-stu-id="6f592-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6f592-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="6f592-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6f592-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="6f592-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="6f592-117">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6f592-117">Creates an App Service plan.</span></span> <span data-ttu-id="6f592-118">Isso é como um farm de servidores para seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="6f592-118">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="6f592-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="6f592-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="6f592-120">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="6f592-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="6f592-121">az webapp config container set</span><span class="sxs-lookup"><span data-stu-id="6f592-121">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="6f592-122">Define o contêiner do Docker Olá para o aplicativo da web do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="6f592-122">Sets hello Docker container for hello Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6f592-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6f592-123">Next steps</span></span>

<span data-ttu-id="6f592-124">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6f592-124">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6f592-125">Exemplos de script CLI do serviço de aplicativo adicionais podem ser encontrados no hello [documentação do serviço de aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6f592-125">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
