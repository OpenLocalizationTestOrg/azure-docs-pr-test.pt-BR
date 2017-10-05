---
title: "Exemplo de script da CLI do Azure - Criar um aplicativo de função para execução sem servidor | Microsoft Docs"
description: "Exemplo de script da CLI do Azure - Criar um Aplicativo de funções para execução sem servidor"
services: functions
documentationcenter: functions
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 04/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 37046967bd5ab0d797d1c66690db7200fb4805e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a><span data-ttu-id="b5faa-103">Criar um Aplicativo de funções para execução sem servidor</span><span class="sxs-lookup"><span data-stu-id="b5faa-103">Create a Function App for serverless execution</span></span>

<span data-ttu-id="b5faa-104">Este exemplo de script cria um Aplicativo de funções do Azure, que é um contêiner para suas funções.</span><span class="sxs-lookup"><span data-stu-id="b5faa-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="b5faa-105">O Aplicativo de funções é criado usando o [plano de consumo](../functions-scale.md#consumption-plan), que é ideal para cargas de trabalho sem servidor controladas por evento.</span><span class="sxs-lookup"><span data-stu-id="b5faa-105">The Function App is created using the [consumption plan](../functions-scale.md#consumption-plan), which is ideal for event-driven serverless workloads.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b5faa-106">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b5faa-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b5faa-107">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="b5faa-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="b5faa-108">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b5faa-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b5faa-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="b5faa-109">Sample script</span></span>

<span data-ttu-id="b5faa-110">Esse script cria um Aplicativo de funções do Azure usando o [plano de consumo](../functions-scale.md#consumption-plan).</span><span class="sxs-lookup"><span data-stu-id="b5faa-110">This script creates an Azure Function app using the [consumption plan](../functions-scale.md#consumption-plan).</span></span>

<span data-ttu-id="b5faa-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Criar uma função do Azure em um plano de consumo")]</span><span class="sxs-lookup"><span data-stu-id="b5faa-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="b5faa-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="b5faa-112">Script explanation</span></span>

<span data-ttu-id="b5faa-113">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="b5faa-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="b5faa-114">Este script usa os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="b5faa-114">This script uses the following commands:</span></span>

| <span data-ttu-id="b5faa-115">Command</span><span class="sxs-lookup"><span data-stu-id="b5faa-115">Command</span></span> | <span data-ttu-id="b5faa-116">Observações</span><span class="sxs-lookup"><span data-stu-id="b5faa-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b5faa-117">az group create</span><span class="sxs-lookup"><span data-stu-id="b5faa-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b5faa-118">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="b5faa-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b5faa-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="b5faa-119">az storage account create</span></span>](/cli/azure/storage/account#create) | <span data-ttu-id="b5faa-120">Cria uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b5faa-120">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="b5faa-121">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="b5faa-121">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="b5faa-122">Cria um Azure Function.</span><span class="sxs-lookup"><span data-stu-id="b5faa-122">Creates an Azure Function.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b5faa-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b5faa-123">Next steps</span></span>

<span data-ttu-id="b5faa-124">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b5faa-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b5faa-125">Exemplos adicionais de scripts da CLI do Azure Functions podem ser encontrados na [Documentação do Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b5faa-125">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
