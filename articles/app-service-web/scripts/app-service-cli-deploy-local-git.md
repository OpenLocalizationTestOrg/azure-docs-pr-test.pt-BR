---
title: "Exemplo de Script CLI do Azure - Criar um aplicativo Web e implantar o código de um repositório Git local | Microsoft Docs"
description: "Exemplo de script da CLI do Azure - Criar um aplicativo Web e implantar o código de um repositório local Git"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 048f98aa-f708-44cb-9b9e-953f67dc6da8
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 50d69ac48438920ce59808ee79809235d8330b14
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="6c3e0-103">Criar um aplicativo Web e implantar o código de um repositório local Git</span><span class="sxs-lookup"><span data-stu-id="6c3e0-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="6c3e0-104">Este script de exemplo cria um aplicativo Web no serviço de aplicativo com seus recursos relacionados e, em seguida, implanta seu código de aplicativo da web em um repositório Git local.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6c3e0-105">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6c3e0-106">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="6c3e0-107">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6c3e0-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6c3e0-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="6c3e0-108">Sample script</span></span>

<span data-ttu-id="6c3e0-109">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Criar um aplicativo Web e implantar o código de um repositório local Git")]</span><span class="sxs-lookup"><span data-stu-id="6c3e0-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="6c3e0-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="6c3e0-110">Script explanation</span></span>

<span data-ttu-id="6c3e0-111">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-111">This script uses the following commands.</span></span> <span data-ttu-id="6c3e0-112">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6c3e0-113">Command</span><span class="sxs-lookup"><span data-stu-id="6c3e0-113">Command</span></span> | <span data-ttu-id="6c3e0-114">Observações</span><span class="sxs-lookup"><span data-stu-id="6c3e0-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6c3e0-115">az group create</span><span class="sxs-lookup"><span data-stu-id="6c3e0-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6c3e0-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6c3e0-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="6c3e0-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="6c3e0-118">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="6c3e0-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="6c3e0-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="6c3e0-120">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="6c3e0-121">az webapp deployment user set</span><span class="sxs-lookup"><span data-stu-id="6c3e0-121">az webapp deployment user set</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/user#set) | <span data-ttu-id="6c3e0-122">Define as credenciais de implantação no nível da conta de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-122">Sets the account-level deployment credentials for App Service.</span></span> |
| [<span data-ttu-id="6c3e0-123">az webapp deployment source config-local-git</span><span class="sxs-lookup"><span data-stu-id="6c3e0-123">az webapp deployment source config-local-git</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/source#config-local-git) | <span data-ttu-id="6c3e0-124">Cria uma configuração de controle de origem para um repositório Git local.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-124">Creates a source control configuration for a local Git repository.</span></span> |
| [<span data-ttu-id="6c3e0-125">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="6c3e0-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="6c3e0-126">Abra um aplicativo Web do Azure em um navegador.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-126">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6c3e0-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6c3e0-127">Next steps</span></span>

<span data-ttu-id="6c3e0-128">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6c3e0-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6c3e0-129">Os exemplos de script da CLI do Serviço de Aplicativo adicionais podem ser encontrados na [documentação do Serviço de Aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6c3e0-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
