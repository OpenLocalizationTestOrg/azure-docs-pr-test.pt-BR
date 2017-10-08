---
title: "aaaCreate uma função de aplicativo e implante o código de função do GitHub | Microsoft Docs"
description: "Exemplo de Script da CLI do Azure - Criar um Aplicativo de funções e implantar o código da função do GitHub"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 026886f11909149db695d9a52d0aa37f109f64e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a><span data-ttu-id="98b0e-103">Criar um Aplicativo de funções e implantar o código da função do GitHub</span><span class="sxs-lookup"><span data-stu-id="98b0e-103">Create a function app and deploy function code from GitHub</span></span>

<span data-ttu-id="98b0e-104">Esse script de exemplo cria um aplicativo de função usando Olá [plano consumo](../functions-scale.md#consumption-plan) com seus recursos relacionados e implanta seu código de função de um repositório GitHub público (sem a implantação contínua).</span><span class="sxs-lookup"><span data-stu-id="98b0e-104">This sample script creates a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and deploys your function code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="98b0e-105">Para o fornecimento contínuo do código da função do GitHub, leia [Criar um aplicativo de funções e implantar continuamente do GitHub](functions-cli-create-function-app-github-continuous.md)</span><span class="sxs-lookup"><span data-stu-id="98b0e-105">For continuous delivery of function code from GitHub, read [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="98b0e-106">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="98b0e-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="98b0e-107">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="98b0e-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="98b0e-108">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="98b0e-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="98b0e-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="98b0e-109">Sample script</span></span>

<span data-ttu-id="98b0e-110">Este exemplo cria um Aplicativo de funções do Azure e implanta o código da função do GitHub.</span><span class="sxs-lookup"><span data-stu-id="98b0e-110">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Create a function app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="98b0e-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="98b0e-111">Script explanation</span></span>

<span data-ttu-id="98b0e-112">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="98b0e-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="98b0e-113">Esse script usa Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="98b0e-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="98b0e-114">Command</span><span class="sxs-lookup"><span data-stu-id="98b0e-114">Command</span></span> | <span data-ttu-id="98b0e-115">Observações</span><span class="sxs-lookup"><span data-stu-id="98b0e-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="98b0e-116">az group create</span><span class="sxs-lookup"><span data-stu-id="98b0e-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="98b0e-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="98b0e-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="98b0e-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="98b0e-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="98b0e-119">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="98b0e-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="98b0e-120">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="98b0e-120">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="98b0e-121">Cria um Aplicativo de funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="98b0e-121">Creates an Azure Function app.</span></span> |
| [<span data-ttu-id="98b0e-122">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="98b0e-122">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="98b0e-123">Associa um aplicativo de funções a um repositório Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="98b0e-123">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="98b0e-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="98b0e-124">Next steps</span></span>

<span data-ttu-id="98b0e-125">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="98b0e-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="98b0e-126">Exemplos de script CLI do Azure funções adicionais podem ser encontrados no hello [documentação de funções do Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="98b0e-126">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
