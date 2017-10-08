---
title: "aaaAzure exemplo de Script CLI - criar um aplicativo web e implantar o código de um repositório Git local | Microsoft Docs"
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
ms.openlocfilehash: 5ad75394c40025d8941282eabeaf34c19c72ee1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="df28f-103">Criar um aplicativo Web e implantar o código de um repositório local Git</span><span class="sxs-lookup"><span data-stu-id="df28f-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="df28f-104">Este script de exemplo cria um aplicativo Web no serviço de aplicativo com seus recursos relacionados e, em seguida, implanta seu código de aplicativo da web em um repositório Git local.</span><span class="sxs-lookup"><span data-stu-id="df28f-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="df28f-105">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="df28f-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="df28f-106">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="df28f-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="df28f-107">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="df28f-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="df28f-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="df28f-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="df28f-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="df28f-109">Script explanation</span></span>

<span data-ttu-id="df28f-110">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="df28f-110">This script uses hello following commands.</span></span> <span data-ttu-id="df28f-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="df28f-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="df28f-112">Command</span><span class="sxs-lookup"><span data-stu-id="df28f-112">Command</span></span> | <span data-ttu-id="df28f-113">Observações</span><span class="sxs-lookup"><span data-stu-id="df28f-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="df28f-114">az group create</span><span class="sxs-lookup"><span data-stu-id="df28f-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="df28f-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="df28f-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="df28f-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="df28f-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="df28f-117">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="df28f-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="df28f-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="df28f-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="df28f-119">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="df28f-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="df28f-120">az webapp deployment user set</span><span class="sxs-lookup"><span data-stu-id="df28f-120">az webapp deployment user set</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/user#set) | <span data-ttu-id="df28f-121">Define as credenciais de implantação de nível de conta Olá para serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="df28f-121">Sets hello account-level deployment credentials for App Service.</span></span> |
| [<span data-ttu-id="df28f-122">az webapp deployment source config-local-git</span><span class="sxs-lookup"><span data-stu-id="df28f-122">az webapp deployment source config-local-git</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/source#config-local-git) | <span data-ttu-id="df28f-123">Cria uma configuração de controle de origem para um repositório Git local.</span><span class="sxs-lookup"><span data-stu-id="df28f-123">Creates a source control configuration for a local Git repository.</span></span> |
| [<span data-ttu-id="df28f-124">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="df28f-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="df28f-125">Abra um aplicativo Web do Azure em um navegador.</span><span class="sxs-lookup"><span data-stu-id="df28f-125">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="df28f-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="df28f-126">Next steps</span></span>

<span data-ttu-id="df28f-127">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="df28f-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="df28f-128">Exemplos de script CLI do serviço de aplicativo adicionais podem ser encontrados no hello [documentação do serviço de aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="df28f-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
