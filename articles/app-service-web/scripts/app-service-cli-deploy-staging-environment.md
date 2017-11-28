---
title: "aaaAzure exemplo de Script CLI - criar um aplicativo web e implantar código tooa ambiente de preparo | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - criar um aplicativo web e implantar código tooa ambiente de preparo"
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
ms.openlocfilehash: cd07f5eda31041effd7b7334f5ecc04e6c1a0514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a><span data-ttu-id="759fd-103">Criar um aplicativo web e implantar código tooa ambiente de preparo</span><span class="sxs-lookup"><span data-stu-id="759fd-103">Create a web app and deploy code tooa staging environment</span></span>

<span data-ttu-id="759fd-104">Esse script de exemplo cria um aplicativo web no serviço de aplicativo com um slot de implantação adicional chamado "preparação" e, em seguida, implanta um toohello do aplicativo de exemplo "preparação" slot.</span><span class="sxs-lookup"><span data-stu-id="759fd-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app toohello "staging" slot.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="759fd-105">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="759fd-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="759fd-106">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="759fd-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="759fd-107">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="759fd-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="759fd-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="759fd-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Create a web app and deploy code tooa staging environment")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="759fd-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="759fd-109">Script explanation</span></span>

<span data-ttu-id="759fd-110">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="759fd-110">This script uses hello following commands.</span></span> <span data-ttu-id="759fd-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="759fd-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="759fd-112">Command</span><span class="sxs-lookup"><span data-stu-id="759fd-112">Command</span></span> | <span data-ttu-id="759fd-113">Observações</span><span class="sxs-lookup"><span data-stu-id="759fd-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="759fd-114">az group create</span><span class="sxs-lookup"><span data-stu-id="759fd-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="759fd-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="759fd-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="759fd-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="759fd-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="759fd-117">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="759fd-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="759fd-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="759fd-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="759fd-119">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="759fd-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="759fd-120">az webapp deployment slot create</span><span class="sxs-lookup"><span data-stu-id="759fd-120">az webapp deployment slot create</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#create) | <span data-ttu-id="759fd-121">Crie um slot de implantação.</span><span class="sxs-lookup"><span data-stu-id="759fd-121">Create a deployment slot.</span></span> |
| [<span data-ttu-id="759fd-122">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="759fd-122">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="759fd-123">Associa a um aplicativo Web do Azure com um repositório Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="759fd-123">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="759fd-124">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="759fd-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="759fd-125">Abra um aplicativo Web do Azure em um navegador.</span><span class="sxs-lookup"><span data-stu-id="759fd-125">Open an Azure web app in a browser.</span></span> |
| [<span data-ttu-id="759fd-126">az webapp deployment slot swap</span><span class="sxs-lookup"><span data-stu-id="759fd-126">az webapp deployment slot swap</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#swap) | <span data-ttu-id="759fd-127">Troca um slot de implantação especificado para produção.</span><span class="sxs-lookup"><span data-stu-id="759fd-127">Swap a specified deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="759fd-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="759fd-128">Next steps</span></span>

<span data-ttu-id="759fd-129">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="759fd-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="759fd-130">Exemplos de script CLI do serviço de aplicativo adicionais podem ser encontrados no hello [documentação do serviço de aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="759fd-130">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
