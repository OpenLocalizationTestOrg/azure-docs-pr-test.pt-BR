---
title: "aaaAzure exemplo de Script CLI - mapear um aplicativo de função do domínio personalizado tooa | Microsoft Docs"
description: "Exemplo de Script do Azure CLI - mapa de um aplicativo de função tooa domínio personalizado no Azure."
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d127e347-7581-47d7-b289-e0f51f2fbfbc
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c7cb0a3e132b491250623b945aecf6aea4f57c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-function-app"></a><span data-ttu-id="4002c-103">Mapa de um aplicativo de função tooa domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="4002c-103">Map a custom domain tooa function app</span></span>

<span data-ttu-id="4002c-104">Esse script de exemplo cria um aplicativo de função com os recursos relacionados e, em seguida, mapeia `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="4002c-104">This sample script creates a function app with related resources, and then maps `www.<yourdomain>` tooit.</span></span> <span data-ttu-id="4002c-105">toomap tooa o domínio personalizado, seu aplicativo de função deve ser criado em um plano de serviço de aplicativo e não em um plano de consumo.</span><span class="sxs-lookup"><span data-stu-id="4002c-105">toomap tooa custom domain, your function app must be created in an App Service plan and not in a consumption plan.</span></span> <span data-ttu-id="4002c-106">O Azure Functions oferece suporte ao mapeamento apenas um domínio personalizado usando um registro A.</span><span class="sxs-lookup"><span data-stu-id="4002c-106">Azure Functions only supports mapping a custom domain using an A record.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4002c-107">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="4002c-107">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4002c-108">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="4002c-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4002c-109">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4002c-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="4002c-110">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="4002c-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa function app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="4002c-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="4002c-111">Script explanation</span></span>

<span data-ttu-id="4002c-112">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="4002c-112">This script uses hello following commands.</span></span> <span data-ttu-id="4002c-113">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="4002c-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4002c-114">Command</span><span class="sxs-lookup"><span data-stu-id="4002c-114">Command</span></span> | <span data-ttu-id="4002c-115">Observações</span><span class="sxs-lookup"><span data-stu-id="4002c-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4002c-116">az group create</span><span class="sxs-lookup"><span data-stu-id="4002c-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="4002c-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="4002c-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4002c-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="4002c-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="4002c-119">Cria uma conta de armazenamento exigida pelo aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="4002c-119">Creates a storage account required by hello function app.</span></span> |
| [<span data-ttu-id="4002c-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="4002c-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="4002c-121">Cria um toomap é necessário um plano de serviço de aplicativo em um domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="4002c-121">Creates an App Service plan required toomap a custom domain.</span></span> |
| [<span data-ttu-id="4002c-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="4002c-122">az functionapp create</span></span>]() | <span data-ttu-id="4002c-123">Cria um aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="4002c-123">Creates a function app.</span></span> |
| [<span data-ttu-id="4002c-124">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="4002c-124">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="4002c-125">Mapeia um aplicativo de função tooa domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="4002c-125">Maps a custom domain tooa function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4002c-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4002c-126">Next steps</span></span>

<span data-ttu-id="4002c-127">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4002c-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4002c-128">Exemplos de script CLI de funções adicionais podem ser encontrados no hello [documentação de funções do Azure]().</span><span class="sxs-lookup"><span data-stu-id="4002c-128">Additional Functions CLI script samples can be found in hello [Azure Functions documentation]().</span></span>
