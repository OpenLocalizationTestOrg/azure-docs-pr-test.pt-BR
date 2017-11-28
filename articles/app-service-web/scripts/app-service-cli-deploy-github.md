---
title: "aaaAzure exemplo de Script CLI - criar um aplicativo web com a implantação do GitHub | Microsoft Docs"
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
ms.openlocfilehash: eb7231aa5c6a7e23d76885107e733008382f7487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="8582f-103">Criar um aplicativo Web com a implantação do GitHub</span><span class="sxs-lookup"><span data-stu-id="8582f-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="8582f-104">Este script de exemplo cria um aplicativo Web no serviço de aplicativo com seus recursos relacionados e, em seguida, implanta seu código de aplicativo Web de um repositório GitHub público (sem a implantação contínua).</span><span class="sxs-lookup"><span data-stu-id="8582f-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="8582f-105">Para implantação do GitHub com implantação contínua, confira [Como criar um aplicativo Web com implantação contínua do GitHub](app-service-cli-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="8582f-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8582f-106">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="8582f-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8582f-107">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="8582f-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8582f-108">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8582f-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="8582f-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="8582f-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="8582f-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="8582f-110">Script explanation</span></span> 

<span data-ttu-id="8582f-111">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="8582f-111">This script uses hello following commands.</span></span> <span data-ttu-id="8582f-112">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="8582f-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8582f-113">Command</span><span class="sxs-lookup"><span data-stu-id="8582f-113">Command</span></span> | <span data-ttu-id="8582f-114">Observações</span><span class="sxs-lookup"><span data-stu-id="8582f-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8582f-115">az group create</span><span class="sxs-lookup"><span data-stu-id="8582f-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8582f-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="8582f-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8582f-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="8582f-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="8582f-118">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8582f-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="8582f-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="8582f-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="8582f-120">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="8582f-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="8582f-121">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="8582f-121">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="8582f-122">Associa a um aplicativo Web do Azure com um repositório Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="8582f-122">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="8582f-123">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="8582f-123">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="8582f-124">Abra um aplicativo Web do Azure em um navegador.</span><span class="sxs-lookup"><span data-stu-id="8582f-124">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8582f-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8582f-125">Next steps</span></span>

<span data-ttu-id="8582f-126">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8582f-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8582f-127">Exemplos de script CLI do serviço de aplicativo adicionais podem ser encontrados no hello [documentação do serviço de aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8582f-127">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
