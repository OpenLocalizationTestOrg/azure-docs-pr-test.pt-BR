---
title: "Exemplo de Script CLI do Azure - Criar um aplicativo Web e implantar o código em um ambiente de preparo | Microsoft Docs"
description: "Exemplo de Script da CLI do Azure - Criar um aplicativo web e implantar o código em um ambiente de preparo"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 2b995dcd-e471-4355-9fda-00babcdb156e
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: d586b50258c32e44f55859aad0a89475e9e4d2eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-and-deploy-code-to-a-staging-environment"></a><span data-ttu-id="52d3b-103">Criar um aplicativo web e implantar o código em um ambiente de preparo</span><span class="sxs-lookup"><span data-stu-id="52d3b-103">Create a web app and deploy code to a staging environment</span></span>

<span data-ttu-id="52d3b-104">Este script de exemplo cria um aplicativo Web no serviço de aplicativo com um slot de implantação adicional chamado "teste" e, em seguida, implanta um aplicativo de exemplo para o slot de "teste".</span><span class="sxs-lookup"><span data-stu-id="52d3b-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="52d3b-105">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="52d3b-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="52d3b-106">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="52d3b-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="52d3b-107">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="52d3b-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="52d3b-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="52d3b-108">Sample script</span></span>

<span data-ttu-id="52d3b-109">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Criar um aplicativo web e implantar o código em um ambiente de preparo")]</span><span class="sxs-lookup"><span data-stu-id="52d3b-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Create a web app and deploy code to a staging environment")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="52d3b-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="52d3b-110">Script explanation</span></span>

<span data-ttu-id="52d3b-111">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="52d3b-111">This script uses the following commands.</span></span> <span data-ttu-id="52d3b-112">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="52d3b-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="52d3b-113">Command</span><span class="sxs-lookup"><span data-stu-id="52d3b-113">Command</span></span> | <span data-ttu-id="52d3b-114">Observações</span><span class="sxs-lookup"><span data-stu-id="52d3b-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="52d3b-115">az group create</span><span class="sxs-lookup"><span data-stu-id="52d3b-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="52d3b-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="52d3b-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="52d3b-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="52d3b-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="52d3b-118">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="52d3b-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="52d3b-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="52d3b-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="52d3b-120">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="52d3b-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="52d3b-121">az webapp deployment slot create</span><span class="sxs-lookup"><span data-stu-id="52d3b-121">az webapp deployment slot create</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#create) | <span data-ttu-id="52d3b-122">Crie um slot de implantação.</span><span class="sxs-lookup"><span data-stu-id="52d3b-122">Create a deployment slot.</span></span> |
| [<span data-ttu-id="52d3b-123">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="52d3b-123">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="52d3b-124">Associa a um aplicativo Web do Azure com um repositório Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="52d3b-124">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="52d3b-125">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="52d3b-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="52d3b-126">Abra um aplicativo Web do Azure em um navegador.</span><span class="sxs-lookup"><span data-stu-id="52d3b-126">Open an Azure web app in a browser.</span></span> |
| [<span data-ttu-id="52d3b-127">az webapp deployment slot swap</span><span class="sxs-lookup"><span data-stu-id="52d3b-127">az webapp deployment slot swap</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#swap) | <span data-ttu-id="52d3b-128">Troca um slot de implantação especificado para produção.</span><span class="sxs-lookup"><span data-stu-id="52d3b-128">Swap a specified deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="52d3b-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="52d3b-129">Next steps</span></span>

<span data-ttu-id="52d3b-130">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="52d3b-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="52d3b-131">Os exemplos de script da CLI do Serviço de Aplicativo adicionais podem ser encontrados na [documentação do Serviço de Aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="52d3b-131">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
