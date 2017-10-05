---
title: "Criar um Aplicativo de funções e implantar o código da função do GitHub | Microsoft Docs"
description: "Criar um Aplicativo de funções e implantar o código da função do GitHub"
services: functions
ms.service: functions
keywords: 
ms.devlang: azurecli
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.custom: mvc
ms.openlocfilehash: 67eb41d89328ab57741c419d8b718e19b947dab1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="2567a-103">Criar um Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="2567a-103">Create an App Service</span></span>

<span data-ttu-id="2567a-104">Este exemplo de script cria um aplicativo de funções usando o [plano de consumo](../functions-scale.md#consumption-plan) com seus recursos relacionados e, em seguida, implanta continuamente o código de sua função de um repositório do GitHub.</span><span class="sxs-lookup"><span data-stu-id="2567a-104">This sample script creates a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a GitHub repository.</span></span> <span data-ttu-id="2567a-105">Neste exemplo, você precisa de:</span><span class="sxs-lookup"><span data-stu-id="2567a-105">In this sample, you need:</span></span>

* <span data-ttu-id="2567a-106">Um repositório do GitHub com um código de funções, para o qual você tem permissões administrativas.</span><span class="sxs-lookup"><span data-stu-id="2567a-106">A GitHub repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="2567a-107">Um [PAT (Token de Acesso Pessoal)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) para sua conta do GitHub.</span><span class="sxs-lookup"><span data-stu-id="2567a-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2567a-108">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="2567a-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2567a-109">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="2567a-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="2567a-110">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2567a-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="2567a-111">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="2567a-111">Sample script</span></span>

<span data-ttu-id="2567a-112">Este exemplo cria um Aplicativo de funções do Azure e implanta o código da função do GitHub.</span><span class="sxs-lookup"><span data-stu-id="2567a-112">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

<span data-ttu-id="2567a-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "Serviço do Azure")]</span><span class="sxs-lookup"><span data-stu-id="2567a-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "Azure Service")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="2567a-114">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="2567a-114">Script explanation</span></span>

<span data-ttu-id="2567a-115">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="2567a-115">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="2567a-116">Este script usa o seguinte:</span><span class="sxs-lookup"><span data-stu-id="2567a-116">This script uses the following:</span></span>

| <span data-ttu-id="2567a-117">Command</span><span class="sxs-lookup"><span data-stu-id="2567a-117">Command</span></span> | <span data-ttu-id="2567a-118">Observações</span><span class="sxs-lookup"><span data-stu-id="2567a-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2567a-119">az group create</span><span class="sxs-lookup"><span data-stu-id="2567a-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2567a-120">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="2567a-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2567a-121">az storage account create</span><span class="sxs-lookup"><span data-stu-id="2567a-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="2567a-122">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2567a-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="2567a-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="2567a-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="2567a-124">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="2567a-124">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="2567a-125">Associa um aplicativo de funções a um repositório Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="2567a-125">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2567a-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2567a-126">Next steps</span></span>

<span data-ttu-id="2567a-127">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2567a-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2567a-128">Exemplos adicionais de scripts da CLI do Azure Functions podem ser encontrados na [Documentação do Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2567a-128">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
