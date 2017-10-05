---
title: "Exemplo de script da CLI do Azure - Criar um aplicativo Web com a implantação contínua do Visual Studio Team Services | Microsoft Docs"
description: "Exemplo de script da CLI do Azure - Criar um aplicativo Web com a implantação contínua do Visual Studio Team Services"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 389d3bd3-cd8e-4715-a3a1-031ec061d385
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 2b983616757ca3c4226c12876f5fd4c285067318
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-visual-studio-team-services"></a><span data-ttu-id="2649e-103">Criar um aplicativo Web com a implantação contínua do Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="2649e-103">Create a web app with continuous deployment from Visual Studio Team Services</span></span>

<span data-ttu-id="2649e-104">Esse script de exemplo cria um aplicativo Web no Serviço de Aplicativo com recursos relacionados e, em seguida, configura a implantação contínua por meio de um repositório do Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="2649e-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span></span> <span data-ttu-id="2649e-105">Para esta amostra, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="2649e-105">For this sample, you will need:</span></span>

* <span data-ttu-id="2649e-106">Um repositório do Visual Studio Team Services com um código do aplicativo para o qual você tem permissões administrativas.</span><span class="sxs-lookup"><span data-stu-id="2649e-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="2649e-107">Um [PAT (Token de Acesso Pessoal)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) para sua conta do Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="2649e-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2649e-108">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="2649e-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2649e-109">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="2649e-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="2649e-110">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2649e-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="2649e-111">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="2649e-111">Sample script</span></span>

<span data-ttu-id="2649e-112">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "criar um aplicativo Web com a implantação contínua do Visual Studio Team Services")]</span><span class="sxs-lookup"><span data-stu-id="2649e-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Visual Studio Team Services")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="2649e-113">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="2649e-113">Script explanation</span></span>

<span data-ttu-id="2649e-114">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="2649e-114">This script uses the following commands.</span></span> <span data-ttu-id="2649e-115">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="2649e-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2649e-116">Command</span><span class="sxs-lookup"><span data-stu-id="2649e-116">Command</span></span> | <span data-ttu-id="2649e-117">Observações</span><span class="sxs-lookup"><span data-stu-id="2649e-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2649e-118">az group create</span><span class="sxs-lookup"><span data-stu-id="2649e-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2649e-119">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="2649e-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2649e-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="2649e-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="2649e-121">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2649e-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="2649e-122">az webapp create</span><span class="sxs-lookup"><span data-stu-id="2649e-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="2649e-123">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="2649e-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="2649e-124">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="2649e-124">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="2649e-125">Associa a um aplicativo Web do Azure com um repositório Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="2649e-125">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="2649e-126">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="2649e-126">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="2649e-127">Abra um aplicativo Web do Azure em um navegador.</span><span class="sxs-lookup"><span data-stu-id="2649e-127">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2649e-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2649e-128">Next steps</span></span>

<span data-ttu-id="2649e-129">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2649e-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2649e-130">Os exemplos de script da CLI do Serviço de Aplicativo adicionais podem ser encontrados na [documentação do Serviço de Aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2649e-130">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
