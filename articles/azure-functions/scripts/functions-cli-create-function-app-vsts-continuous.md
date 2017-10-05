---
title: "Criar um Aplicativo de funções e implantar o código da função do Visual Studio Team Services | Microsoft Docs"
description: "Criar um Aplicativo de funções e implantar o código da função do Visual Studio Team Services"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/28/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 2ef177b55ad7ffd351156821f429e6ff8fbeccc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="0026f-103">Criar um Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="0026f-103">Create an App Service</span></span>

<span data-ttu-id="0026f-104">Nesse cenário, você aprenderá a criar um Aplicativo de funções usando o [plano consumo](../functions-scale.md#consumption-plan) com seus recursos relacionados, e a implantar continuamente o código de sua função de um repositório do VSTS (Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="0026f-104">In this scenario you will learn how to create a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a Visual Studio Team Services (VSTS) repository.</span></span> <span data-ttu-id="0026f-105">Nesta amostra, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="0026f-105">In this sample, you will need:</span></span>

* <span data-ttu-id="0026f-106">Um repositório do VSTS com um código de funções, para o qual você tem permissões administrativas.</span><span class="sxs-lookup"><span data-stu-id="0026f-106">A VSTS repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="0026f-107">Um [PAT (Token de Acesso Pessoal)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) para sua conta do GitHub.</span><span class="sxs-lookup"><span data-stu-id="0026f-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0026f-108">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="0026f-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0026f-109">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="0026f-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="0026f-110">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0026f-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="0026f-111">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="0026f-111">Sample script</span></span>

<span data-ttu-id="0026f-112">Este exemplo cria um Aplicativo de funções do Azure e implanta o código da função do Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="0026f-112">This sample creates an Azure Function app and deploys function code from Visual Studio Team Services.</span></span>

<span data-ttu-id="0026f-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Serviço do Azure")]</span><span class="sxs-lookup"><span data-stu-id="0026f-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Azure Service")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="0026f-114">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="0026f-114">Script explanation</span></span>

<span data-ttu-id="0026f-115">Este script usa os seguintes comandos para criar um grupo de recursos, um aplicativo Web, o DocumentDB e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="0026f-115">This script uses the following commands to create a resource group, web app, documentdb and all related resources.</span></span> <span data-ttu-id="0026f-116">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="0026f-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0026f-117">Command</span><span class="sxs-lookup"><span data-stu-id="0026f-117">Command</span></span> | <span data-ttu-id="0026f-118">Observações</span><span class="sxs-lookup"><span data-stu-id="0026f-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0026f-119">az group create</span><span class="sxs-lookup"><span data-stu-id="0026f-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="0026f-120">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="0026f-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0026f-121">az storage account create</span><span class="sxs-lookup"><span data-stu-id="0026f-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="0026f-122">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0026f-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="0026f-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="0026f-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="0026f-124">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="0026f-124">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="0026f-125">Associa um aplicativo de funções a um repositório Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="0026f-125">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0026f-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0026f-126">Next steps</span></span>

<span data-ttu-id="0026f-127">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0026f-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0026f-128">Exemplos adicionais de scripts da CLI do Azure Functions podem ser encontrados na [Documentação do Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0026f-128">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
