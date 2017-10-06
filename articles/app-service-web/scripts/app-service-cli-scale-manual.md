---
title: aaaAzure exemplo de Script CLI - dimensionar um aplicativo Web manualmente usando o Azure CLI 2.0 | Microsoft Docs
description: Exemplo de Script CLI do Azure - Dimensionar um aplicativo Web manualmente usando a CLI do Azure 2.0
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 251d9074-8fff-4121-ad16-9eca9556ac96
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 64464c8a44522fdc2c8f3d0192388302a1d12667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="ba509-103">Dimensionar manualmente um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="ba509-103">Scale a web app manually</span></span>

<span data-ttu-id="ba509-104">Nesse cenário, você aprenderá toocreate um grupo de recursos, aplicativo de serviço web e o plano de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ba509-104">In this scenario you will learn toocreate a resource group, app service plan and web app.</span></span> <span data-ttu-id="ba509-105">Em seguida, você será dimensionado Olá plano do serviço de aplicativo de instâncias de toomultiple uma única instância.</span><span class="sxs-lookup"><span data-stu-id="ba509-105">You will then scale hello App Service Plan from a single instance toomultiple instances.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ba509-106">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="ba509-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ba509-107">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="ba509-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ba509-108">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ba509-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ba509-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="ba509-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Manual Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="ba509-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="ba509-110">Script explanation</span></span>

<span data-ttu-id="ba509-111">Esse script usa Olá comandos toocreate um grupo de recursos, aplicativo web e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="ba509-111">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="ba509-112">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="ba509-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ba509-113">Command</span><span class="sxs-lookup"><span data-stu-id="ba509-113">Command</span></span> | <span data-ttu-id="ba509-114">Observações</span><span class="sxs-lookup"><span data-stu-id="ba509-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ba509-115">az group create</span><span class="sxs-lookup"><span data-stu-id="ba509-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ba509-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="ba509-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ba509-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="ba509-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="ba509-118">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ba509-118">Creates an App Service plan.</span></span> <span data-ttu-id="ba509-119">Isso é como um farm de servidores para seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba509-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="ba509-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="ba509-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="ba509-121">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba509-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="ba509-122">az appservice plan update</span><span class="sxs-lookup"><span data-stu-id="ba509-122">az appservice plan update</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#update) | <span data-ttu-id="ba509-123">Atualiza as propriedades de saudação plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ba509-123">Updates properties of hello App Service plan.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ba509-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ba509-124">Next steps</span></span>

<span data-ttu-id="ba509-125">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ba509-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ba509-126">Exemplos de script CLI do serviço de aplicativo adicionais podem ser encontrados no hello [documentação do serviço de aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ba509-126">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
