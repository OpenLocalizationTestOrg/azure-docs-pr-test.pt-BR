---
title: "aaaAzure exemplo de Script CLI - criar um aplicativo web com implantação contínua do Visual Studio Team Services | Microsoft Docs"
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
ms.openlocfilehash: f8d0c2645ec5311296ca9b2df20f97e77bab2283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-visual-studio-team-services"></a><span data-ttu-id="5630e-103">Criar um aplicativo Web com a implantação contínua do Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="5630e-103">Create a web app with continuous deployment from Visual Studio Team Services</span></span>

<span data-ttu-id="5630e-104">Esse script de exemplo cria um aplicativo Web no Serviço de Aplicativo com recursos relacionados e, em seguida, configura a implantação contínua por meio de um repositório do Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="5630e-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span></span> <span data-ttu-id="5630e-105">Para esta amostra, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="5630e-105">For this sample, you will need:</span></span>

* <span data-ttu-id="5630e-106">Um repositório do Visual Studio Team Services com um código do aplicativo para o qual você tem permissões administrativas.</span><span class="sxs-lookup"><span data-stu-id="5630e-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="5630e-107">Um [PAT (Token de Acesso Pessoal)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) para sua conta do Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="5630e-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5630e-108">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="5630e-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5630e-109">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="5630e-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="5630e-110">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5630e-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5630e-111">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="5630e-111">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Visual Studio Team Services")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="5630e-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="5630e-112">Script explanation</span></span>

<span data-ttu-id="5630e-113">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="5630e-113">This script uses hello following commands.</span></span> <span data-ttu-id="5630e-114">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="5630e-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5630e-115">Command</span><span class="sxs-lookup"><span data-stu-id="5630e-115">Command</span></span> | <span data-ttu-id="5630e-116">Observações</span><span class="sxs-lookup"><span data-stu-id="5630e-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5630e-117">az group create</span><span class="sxs-lookup"><span data-stu-id="5630e-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5630e-118">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="5630e-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5630e-119">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="5630e-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="5630e-120">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5630e-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="5630e-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="5630e-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="5630e-122">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="5630e-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="5630e-123">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="5630e-123">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="5630e-124">Associa a um aplicativo Web do Azure com um repositório Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="5630e-124">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="5630e-125">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="5630e-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="5630e-126">Abra um aplicativo Web do Azure em um navegador.</span><span class="sxs-lookup"><span data-stu-id="5630e-126">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5630e-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5630e-127">Next steps</span></span>

<span data-ttu-id="5630e-128">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5630e-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5630e-129">Exemplos de script CLI do serviço de aplicativo adicionais podem ser encontrados no hello [documentação do serviço de aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5630e-129">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
