---
title: "aaaCreate uma função de aplicativo e implante o código de função do Visual Studio Team Services | Microsoft Docs"
description: "Criar um Aplicativo de funções e implantar o código da função do Visual Studio Team Services"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/28/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 774bee73025cc9ac46f8b2a6c10edbfa3c2d353b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="895b2-103">Criar um Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="895b2-103">Create an App Service</span></span>

<span data-ttu-id="895b2-104">Nesse cenário, você vai aprender como toocreate uma função usando o aplicativo hello [plano consumo](../functions-scale.md#consumption-plan) com seus recursos relacionados e implanta continuamente seu código de função de um repositório do Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="895b2-104">In this scenario you will learn how toocreate a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a Visual Studio Team Services (VSTS) repository.</span></span> <span data-ttu-id="895b2-105">Nesta amostra, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="895b2-105">In this sample, you will need:</span></span>

* <span data-ttu-id="895b2-106">Um repositório do VSTS com um código de funções, para o qual você tem permissões administrativas.</span><span class="sxs-lookup"><span data-stu-id="895b2-106">A VSTS repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="895b2-107">Um [PAT (Token de Acesso Pessoal)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) para sua conta do GitHub.</span><span class="sxs-lookup"><span data-stu-id="895b2-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="895b2-108">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="895b2-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="895b2-109">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="895b2-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="895b2-110">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="895b2-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="895b2-111">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="895b2-111">Sample script</span></span>

<span data-ttu-id="895b2-112">Este exemplo cria um Aplicativo de funções do Azure e implanta o código da função do Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="895b2-112">This sample creates an Azure Function app and deploys function code from Visual Studio Team Services.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="895b2-113">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="895b2-113">Script explanation</span></span>

<span data-ttu-id="895b2-114">Esse script usa Olá comandos toocreate um grupo de recursos, aplicativo web, documentos e recursos todos relacionados a seguir.</span><span class="sxs-lookup"><span data-stu-id="895b2-114">This script uses hello following commands toocreate a resource group, web app, documentdb and all related resources.</span></span> <span data-ttu-id="895b2-115">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="895b2-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="895b2-116">Command</span><span class="sxs-lookup"><span data-stu-id="895b2-116">Command</span></span> | <span data-ttu-id="895b2-117">Observações</span><span class="sxs-lookup"><span data-stu-id="895b2-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="895b2-118">az group create</span><span class="sxs-lookup"><span data-stu-id="895b2-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="895b2-119">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="895b2-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="895b2-120">az storage account create</span><span class="sxs-lookup"><span data-stu-id="895b2-120">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="895b2-121">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="895b2-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="895b2-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="895b2-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="895b2-123">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="895b2-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="895b2-124">Associa um aplicativo de funções a um repositório Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="895b2-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="895b2-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="895b2-125">Next steps</span></span>

<span data-ttu-id="895b2-126">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="895b2-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="895b2-127">Exemplos de script CLI do Azure funções adicionais podem ser encontrados no hello [documentação de funções do Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="895b2-127">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
