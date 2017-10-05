---
title: "Criar um Aplicativo de funções e implantar o código da função do GitHub | Microsoft Docs"
description: "Exemplo de Script da CLI do Azure - Criar um Aplicativo de funções e implantar o código da função do GitHub"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: d67e85f91c80efe464fceb1105243bedfba83a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a><span data-ttu-id="bf53a-103">Criar um Aplicativo de funções e implantar o código da função do GitHub</span><span class="sxs-lookup"><span data-stu-id="bf53a-103">Create a function app and deploy function code from GitHub</span></span>

<span data-ttu-id="bf53a-104">Este exemplo de script cria um aplicativo de funções usando o [plano de consumo](../functions-scale.md#consumption-plan) com seus recursos relacionados e, em seguida, implanta seu código de função de um repositório GitHub público (sem a implantação contínua).</span><span class="sxs-lookup"><span data-stu-id="bf53a-104">This sample script creates a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and deploys your function code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="bf53a-105">Para o fornecimento contínuo do código da função do GitHub, leia [Criar um aplicativo de funções e implantar continuamente do GitHub](functions-cli-create-function-app-github-continuous.md)</span><span class="sxs-lookup"><span data-stu-id="bf53a-105">For continuous delivery of function code from GitHub, read [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bf53a-106">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="bf53a-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="bf53a-107">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="bf53a-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="bf53a-108">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bf53a-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="bf53a-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="bf53a-109">Sample script</span></span>

<span data-ttu-id="bf53a-110">Este exemplo cria um Aplicativo de funções do Azure e implanta o código da função do GitHub.</span><span class="sxs-lookup"><span data-stu-id="bf53a-110">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

<span data-ttu-id="bf53a-111">[!code-azurecli-interactive[principal](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Criar um aplicativo de funções com implantação do GitHub")]</span><span class="sxs-lookup"><span data-stu-id="bf53a-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Create a function app with deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="bf53a-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="bf53a-112">Script explanation</span></span>

<span data-ttu-id="bf53a-113">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="bf53a-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="bf53a-114">Este script usa os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="bf53a-114">This script uses the following commands:</span></span>

| <span data-ttu-id="bf53a-115">Command</span><span class="sxs-lookup"><span data-stu-id="bf53a-115">Command</span></span> | <span data-ttu-id="bf53a-116">Observações</span><span class="sxs-lookup"><span data-stu-id="bf53a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bf53a-117">az group create</span><span class="sxs-lookup"><span data-stu-id="bf53a-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="bf53a-118">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="bf53a-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bf53a-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="bf53a-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="bf53a-120">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bf53a-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="bf53a-121">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="bf53a-121">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="bf53a-122">Cria um Aplicativo de funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf53a-122">Creates an Azure Function app.</span></span> |
| [<span data-ttu-id="bf53a-123">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="bf53a-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="bf53a-124">Associa um aplicativo de funções a um repositório Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="bf53a-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bf53a-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bf53a-125">Next steps</span></span>

<span data-ttu-id="bf53a-126">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bf53a-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="bf53a-127">Exemplos adicionais de scripts da CLI do Azure Functions podem ser encontrados na [Documentação do Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="bf53a-127">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
