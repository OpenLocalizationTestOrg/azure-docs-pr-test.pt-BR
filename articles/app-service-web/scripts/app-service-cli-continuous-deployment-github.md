---
title: "aaaAzure exemplo de Script CLI - criar um aplicativo web com implantação contínua do GitHub | Microsoft Docs"
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
ms.openlocfilehash: 6adb06a35ceea8ea64723c9887c25c50f046e280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="c64a8-103">Criar um aplicativo web com a implantação contínua do GitHub</span><span class="sxs-lookup"><span data-stu-id="c64a8-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="c64a8-104">Este script de exemplo cria um aplicativo Web no serviço de aplicativo com seus recursos relacionados e, em seguida, define a implantação contínua de um repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="c64a8-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="c64a8-105">Para implantação do GitHub sem a implantação contínua, veja [Criar um aplicativo Web e implantar o código do GitHub](app-service-cli-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="c64a8-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span></span> <span data-ttu-id="c64a8-106">Nesta amostra, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="c64a8-106">In this sample, you will need:</span></span>

* <span data-ttu-id="c64a8-107">Um repositório GitHub com um código do aplicativo para o qual você tem permissões administrativas.</span><span class="sxs-lookup"><span data-stu-id="c64a8-107">A GitHub repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="c64a8-108">Um [PAT (Token de Acesso Pessoal)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) para sua conta do GitHub.</span><span class="sxs-lookup"><span data-stu-id="c64a8-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c64a8-109">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="c64a8-109">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c64a8-110">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="c64a8-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c64a8-111">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c64a8-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c64a8-112">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="c64a8-112">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c64a8-113">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="c64a8-113">Script explanation</span></span>

<span data-ttu-id="c64a8-114">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="c64a8-114">This script uses hello following commands.</span></span> <span data-ttu-id="c64a8-115">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="c64a8-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c64a8-116">Command</span><span class="sxs-lookup"><span data-stu-id="c64a8-116">Command</span></span> | <span data-ttu-id="c64a8-117">Observações</span><span class="sxs-lookup"><span data-stu-id="c64a8-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c64a8-118">az group create</span><span class="sxs-lookup"><span data-stu-id="c64a8-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c64a8-119">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="c64a8-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c64a8-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="c64a8-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="c64a8-121">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c64a8-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="c64a8-122">az webapp create</span><span class="sxs-lookup"><span data-stu-id="c64a8-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="c64a8-123">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="c64a8-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="c64a8-124">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="c64a8-124">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="c64a8-125">Associa a um aplicativo Web do Azure com um repositório Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="c64a8-125">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="c64a8-126">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="c64a8-126">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="c64a8-127">Abra um aplicativo Web do Azure em um navegador.</span><span class="sxs-lookup"><span data-stu-id="c64a8-127">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c64a8-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c64a8-128">Next steps</span></span>

<span data-ttu-id="c64a8-129">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c64a8-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c64a8-130">Exemplos de script CLI do serviço de aplicativo adicionais podem ser encontrados no hello [documentação do serviço de aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c64a8-130">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
