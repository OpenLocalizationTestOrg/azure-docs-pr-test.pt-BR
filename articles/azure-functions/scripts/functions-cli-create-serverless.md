---
title: "aaaAzure exemplo de Script CLI - criar um aplicativo de função de execução sem servidor | Microsoft Docs"
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
ms.openlocfilehash: 7ec872b642e50827896a73a9e43bcc87233e15c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a><span data-ttu-id="b81dd-103">Criar um Aplicativo de funções para execução sem servidor</span><span class="sxs-lookup"><span data-stu-id="b81dd-103">Create a Function App for serverless execution</span></span>

<span data-ttu-id="b81dd-104">Este exemplo de script cria um Aplicativo de funções do Azure, que é um contêiner para suas funções.</span><span class="sxs-lookup"><span data-stu-id="b81dd-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="b81dd-105">Olá função de aplicativo é criado usando Olá [plano consumo](../functions-scale.md#consumption-plan), que é ideal para cargas de trabalho sem servidor controlada por evento.</span><span class="sxs-lookup"><span data-stu-id="b81dd-105">hello Function App is created using hello [consumption plan](../functions-scale.md#consumption-plan), which is ideal for event-driven serverless workloads.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b81dd-106">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b81dd-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b81dd-107">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="b81dd-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="b81dd-108">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b81dd-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b81dd-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="b81dd-109">Sample script</span></span>

<span data-ttu-id="b81dd-110">Esse script cria um aplicativo de função do Azure usando Olá [plano consumo](../functions-scale.md#consumption-plan).</span><span class="sxs-lookup"><span data-stu-id="b81dd-110">This script creates an Azure Function app using hello [consumption plan](../functions-scale.md#consumption-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="b81dd-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="b81dd-111">Script explanation</span></span>

<span data-ttu-id="b81dd-112">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="b81dd-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="b81dd-113">Esse script usa Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b81dd-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="b81dd-114">Command</span><span class="sxs-lookup"><span data-stu-id="b81dd-114">Command</span></span> | <span data-ttu-id="b81dd-115">Observações</span><span class="sxs-lookup"><span data-stu-id="b81dd-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b81dd-116">az group create</span><span class="sxs-lookup"><span data-stu-id="b81dd-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b81dd-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="b81dd-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b81dd-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="b81dd-118">az storage account create</span></span>](/cli/azure/storage/account#create) | <span data-ttu-id="b81dd-119">Cria uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b81dd-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="b81dd-120">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="b81dd-120">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="b81dd-121">Cria um Azure Function.</span><span class="sxs-lookup"><span data-stu-id="b81dd-121">Creates an Azure Function.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b81dd-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b81dd-122">Next steps</span></span>

<span data-ttu-id="b81dd-123">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b81dd-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b81dd-124">Exemplos de script CLI do Azure funções adicionais podem ser encontrados no hello [documentação de funções do Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b81dd-124">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
