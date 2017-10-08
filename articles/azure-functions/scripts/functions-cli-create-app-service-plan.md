---
title: "aaaAzure exemplo de Script CLI - criar um aplicativo de função em um plano de serviço de aplicativo | Microsoft Docs"
description: "Exemplo de script da CLI do Azure - Criar um Aplicativo de funções em um Plano do Serviço de Aplicativo"
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
ms.openlocfilehash: c0ffbbbf022e5680e5ae3141e784e7c7bced0bc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-in-an-app-service-plan"></a><span data-ttu-id="46322-103">Criar um Aplicativo de funções em um Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="46322-103">Create a Function App in an App Service plan</span></span>

<span data-ttu-id="46322-104">Este exemplo de script cria um Aplicativo de funções do Azure, que é um contêiner para suas funções.</span><span class="sxs-lookup"><span data-stu-id="46322-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="46322-105">saudação de função de aplicativo é criada usando um plano de serviço de aplicativo dedicado, que significa que os recursos do servidor estão sempre ativados.</span><span class="sxs-lookup"><span data-stu-id="46322-105">hello Function App is created using a dedicated App Service plan, which means your server resources are always on.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="46322-106">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="46322-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="46322-107">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="46322-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="46322-108">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="46322-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="46322-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="46322-109">Sample script</span></span>

<span data-ttu-id="46322-110">Esse script cria um Aplicativo de funções do Azure usando um [plano do Serviço de Aplicativo](../functions-scale.md#app-service-plan) dedicado.</span><span class="sxs-lookup"><span data-stu-id="46322-110">This script creates an Azure Function app using a dedicated [App Service plan](../functions-scale.md#app-service-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Create an Azure Function on an App Service plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="46322-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="46322-111">Script explanation</span></span>

<span data-ttu-id="46322-112">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="46322-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="46322-113">Esse script usa Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="46322-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="46322-114">Command</span><span class="sxs-lookup"><span data-stu-id="46322-114">Command</span></span> | <span data-ttu-id="46322-115">Observações</span><span class="sxs-lookup"><span data-stu-id="46322-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="46322-116">az group create</span><span class="sxs-lookup"><span data-stu-id="46322-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="46322-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="46322-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="46322-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="46322-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="46322-119">Cria uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="46322-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="46322-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="46322-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appserviceplan#create) | <span data-ttu-id="46322-121">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46322-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="46322-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="46322-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#delete) | <span data-ttu-id="46322-123">Cria um Aplicativo de funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="46322-123">Creates an Azure Function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="46322-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="46322-124">Next steps</span></span>

<span data-ttu-id="46322-125">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="46322-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="46322-126">Exemplos de script CLI do Azure funções adicionais podem ser encontrados no hello [documentação de funções do Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="46322-126">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
