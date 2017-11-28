---
title: "aaaCreate uma função de aplicativo e implante o código de função do GitHub | Microsoft Docs"
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
ms.openlocfilehash: 4d44204b899b32af464260db51ed98bcf00eb2bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="fb4e7-103">Criar um Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="fb4e7-103">Create an App Service</span></span>

<span data-ttu-id="fb4e7-104">Esse script de exemplo cria um aplicativo de função usando Olá [plano consumo](../functions-scale.md#consumption-plan) com seus recursos relacionados e implanta continuamente seu código de função de um repositório do GitHub.</span><span class="sxs-lookup"><span data-stu-id="fb4e7-104">This sample script creates a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a GitHub repository.</span></span> <span data-ttu-id="fb4e7-105">Neste exemplo, você precisa de:</span><span class="sxs-lookup"><span data-stu-id="fb4e7-105">In this sample, you need:</span></span>

* <span data-ttu-id="fb4e7-106">Um repositório do GitHub com um código de funções, para o qual você tem permissões administrativas.</span><span class="sxs-lookup"><span data-stu-id="fb4e7-106">A GitHub repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="fb4e7-107">Um [PAT (Token de Acesso Pessoal)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) para sua conta do GitHub.</span><span class="sxs-lookup"><span data-stu-id="fb4e7-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fb4e7-108">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="fb4e7-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="fb4e7-109">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb4e7-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="fb4e7-110">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fb4e7-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="fb4e7-111">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="fb4e7-111">Sample script</span></span>

<span data-ttu-id="fb4e7-112">Este exemplo cria um Aplicativo de funções do Azure e implanta o código da função do GitHub.</span><span class="sxs-lookup"><span data-stu-id="fb4e7-112">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="fb4e7-113">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="fb4e7-113">Script explanation</span></span>

<span data-ttu-id="fb4e7-114">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="fb4e7-114">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="fb4e7-115">Esse script usa a seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="fb4e7-115">This script uses hello following:</span></span>

| <span data-ttu-id="fb4e7-116">Command</span><span class="sxs-lookup"><span data-stu-id="fb4e7-116">Command</span></span> | <span data-ttu-id="fb4e7-117">Observações</span><span class="sxs-lookup"><span data-stu-id="fb4e7-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fb4e7-118">az group create</span><span class="sxs-lookup"><span data-stu-id="fb4e7-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fb4e7-119">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="fb4e7-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fb4e7-120">az storage account create</span><span class="sxs-lookup"><span data-stu-id="fb4e7-120">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="fb4e7-121">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fb4e7-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="fb4e7-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="fb4e7-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="fb4e7-123">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="fb4e7-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="fb4e7-124">Associa um aplicativo de funções a um repositório Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="fb4e7-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fb4e7-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fb4e7-125">Next steps</span></span>

<span data-ttu-id="fb4e7-126">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fb4e7-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fb4e7-127">Exemplos de script CLI do Azure funções adicionais podem ser encontrados no hello [documentação de funções do Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fb4e7-127">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
