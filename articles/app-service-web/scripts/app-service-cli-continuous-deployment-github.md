---
title: "Exemplo de script da CLI do Azure - Criar um aplicativo Web com a implantação contínua do GitHub | Microsoft Docs"
description: "Exemplo de script da CLI do Azure - Criar um aplicativo Web com a implantação contínua do GitHub"
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
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: a12085a7a8146c22d6b079381542d4fe3a8e6e87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="2c8a2-103">Criar um aplicativo web com a implantação contínua do GitHub</span><span class="sxs-lookup"><span data-stu-id="2c8a2-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="2c8a2-104">Este script de exemplo cria um aplicativo Web no serviço de aplicativo com seus recursos relacionados e, em seguida, define a implantação contínua de um repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="2c8a2-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="2c8a2-105">Para implantação do GitHub sem a implantação contínua, veja [Criar um aplicativo Web e implantar o código do GitHub](app-service-cli-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="2c8a2-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span></span> <span data-ttu-id="2c8a2-106">Nesta amostra, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="2c8a2-106">In this sample, you will need:</span></span>

* <span data-ttu-id="2c8a2-107">Um repositório GitHub com um código do aplicativo para o qual você tem permissões administrativas.</span><span class="sxs-lookup"><span data-stu-id="2c8a2-107">A GitHub repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="2c8a2-108">Um [PAT (Token de Acesso Pessoal)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) para sua conta do GitHub.</span><span class="sxs-lookup"><span data-stu-id="2c8a2-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2c8a2-109">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="2c8a2-109">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2c8a2-110">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="2c8a2-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="2c8a2-111">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2c8a2-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="2c8a2-112">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="2c8a2-112">Sample script</span></span>

<span data-ttu-id="2c8a2-113">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Criar um aplicativo web com a implantação contínua do GitHub")]</span><span class="sxs-lookup"><span data-stu-id="2c8a2-113">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="2c8a2-114">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="2c8a2-114">Script explanation</span></span>

<span data-ttu-id="2c8a2-115">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="2c8a2-115">This script uses the following commands.</span></span> <span data-ttu-id="2c8a2-116">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="2c8a2-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2c8a2-117">Command</span><span class="sxs-lookup"><span data-stu-id="2c8a2-117">Command</span></span> | <span data-ttu-id="2c8a2-118">Observações</span><span class="sxs-lookup"><span data-stu-id="2c8a2-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2c8a2-119">az group create</span><span class="sxs-lookup"><span data-stu-id="2c8a2-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2c8a2-120">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="2c8a2-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2c8a2-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="2c8a2-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="2c8a2-122">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2c8a2-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="2c8a2-123">az webapp create</span><span class="sxs-lookup"><span data-stu-id="2c8a2-123">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="2c8a2-124">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c8a2-124">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="2c8a2-125">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="2c8a2-125">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="2c8a2-126">Associa a um aplicativo Web do Azure com um repositório Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="2c8a2-126">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="2c8a2-127">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="2c8a2-127">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="2c8a2-128">Abra um aplicativo Web do Azure em um navegador.</span><span class="sxs-lookup"><span data-stu-id="2c8a2-128">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2c8a2-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2c8a2-129">Next steps</span></span>

<span data-ttu-id="2c8a2-130">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2c8a2-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2c8a2-131">Os exemplos de script da CLI do Serviço de Aplicativo adicionais podem ser encontrados na [documentação do Serviço de Aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2c8a2-131">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
