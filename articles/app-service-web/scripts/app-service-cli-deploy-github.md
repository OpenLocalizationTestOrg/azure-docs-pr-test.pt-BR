---
title: "Exemplo de script da CLI do Azure - Criar um aplicativo Web com a implantação do GitHub | Microsoft Docs"
description: "Exemplo de script da CLI do Azure - Criar um aplicativo Web com a implantação do GitHub"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0205c991-0989-4ca3-bb41-237dcc964460
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: sample
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 61e9d65319cecf3ea4e9152ebdf1035566aad74c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="74397-103">Criar um aplicativo Web com a implantação do GitHub</span><span class="sxs-lookup"><span data-stu-id="74397-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="74397-104">Este script de exemplo cria um aplicativo Web no serviço de aplicativo com seus recursos relacionados e, em seguida, implanta seu código de aplicativo Web de um repositório GitHub público (sem a implantação contínua).</span><span class="sxs-lookup"><span data-stu-id="74397-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="74397-105">Para implantação do GitHub com implantação contínua, confira [Como criar um aplicativo Web com implantação contínua do GitHub](app-service-cli-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="74397-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="74397-106">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="74397-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="74397-107">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="74397-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="74397-108">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="74397-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="74397-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="74397-109">Sample script</span></span>

<span data-ttu-id="74397-110">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Criar um aplicativo Web com a implantação do GitHub")]</span><span class="sxs-lookup"><span data-stu-id="74397-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="74397-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="74397-111">Script explanation</span></span> 

<span data-ttu-id="74397-112">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="74397-112">This script uses the following commands.</span></span> <span data-ttu-id="74397-113">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="74397-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="74397-114">Command</span><span class="sxs-lookup"><span data-stu-id="74397-114">Command</span></span> | <span data-ttu-id="74397-115">Observações</span><span class="sxs-lookup"><span data-stu-id="74397-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="74397-116">az group create</span><span class="sxs-lookup"><span data-stu-id="74397-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="74397-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="74397-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="74397-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="74397-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="74397-119">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74397-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="74397-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="74397-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="74397-121">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="74397-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="74397-122">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="74397-122">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="74397-123">Associa a um aplicativo Web do Azure com um repositório Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="74397-123">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="74397-124">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="74397-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="74397-125">Abra um aplicativo Web do Azure em um navegador.</span><span class="sxs-lookup"><span data-stu-id="74397-125">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="74397-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="74397-126">Next steps</span></span>

<span data-ttu-id="74397-127">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="74397-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="74397-128">Os exemplos de script da CLI do Serviço de Aplicativo adicionais podem ser encontrados na [documentação do Serviço de Aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="74397-128">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
