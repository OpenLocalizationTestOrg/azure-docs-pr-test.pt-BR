---
title: "Exemplo de Script CLI do Azure - mapeie um domínio personalizado para um aplicativo de funções | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - mapeie um domínio personalizado para um aplicativo de funções no Azure."
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
ms.openlocfilehash: 6fcea6d32f9dd25b0fafb4f895f60d8320ac9df8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="map-a-custom-domain-to-a-function-app"></a><span data-ttu-id="bb570-103">Mapear um domínio personalizado para um aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="bb570-103">Map a custom domain to a function app</span></span>

<span data-ttu-id="bb570-104">Este exemplo de script cria um aplicativo de funções com seus recursos relacionados e depois mapeia `www.<yourdomain>` para ele.</span><span class="sxs-lookup"><span data-stu-id="bb570-104">This sample script creates a function app with related resources, and then maps `www.<yourdomain>` to it.</span></span> <span data-ttu-id="bb570-105">Para mapear um domínio personalizado, seu aplicativo de funções deve ser criado em um Plano do Serviço de Aplicativo, e não em um plano de consumo.</span><span class="sxs-lookup"><span data-stu-id="bb570-105">To map to a custom domain, your function app must be created in an App Service plan and not in a consumption plan.</span></span> <span data-ttu-id="bb570-106">O Azure Functions oferece suporte ao mapeamento apenas um domínio personalizado usando um registro A.</span><span class="sxs-lookup"><span data-stu-id="bb570-106">Azure Functions only supports mapping a custom domain using an A record.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bb570-107">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="bb570-107">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="bb570-108">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="bb570-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="bb570-109">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bb570-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="bb570-110">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="bb570-110">Sample script</span></span>

<span data-ttu-id="bb570-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Mapear um domínio personalizado para um aplicativo de funções")]</span><span class="sxs-lookup"><span data-stu-id="bb570-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain to a function app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="bb570-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="bb570-112">Script explanation</span></span>

<span data-ttu-id="bb570-113">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="bb570-113">This script uses the following commands.</span></span> <span data-ttu-id="bb570-114">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="bb570-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="bb570-115">Command</span><span class="sxs-lookup"><span data-stu-id="bb570-115">Command</span></span> | <span data-ttu-id="bb570-116">Observações</span><span class="sxs-lookup"><span data-stu-id="bb570-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bb570-117">az group create</span><span class="sxs-lookup"><span data-stu-id="bb570-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="bb570-118">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="bb570-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bb570-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="bb570-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="bb570-120">Cria uma conta de armazenamento necessária para o aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="bb570-120">Creates a storage account required by the function app.</span></span> |
| [<span data-ttu-id="bb570-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="bb570-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="bb570-122">Cria um Plano do Serviço de Aplicativo necessário para mapear um domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="bb570-122">Creates an App Service plan required to map a custom domain.</span></span> |
| [<span data-ttu-id="bb570-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="bb570-123">az functionapp create</span></span>]() | <span data-ttu-id="bb570-124">Cria um aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="bb570-124">Creates a function app.</span></span> |
| [<span data-ttu-id="bb570-125">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="bb570-125">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="bb570-126">Mapear um domínio personalizado para um aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="bb570-126">Maps a custom domain to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bb570-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bb570-127">Next steps</span></span>

<span data-ttu-id="bb570-128">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bb570-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="bb570-129">Exemplos adicionais de scripts da CLI do Functions podem ser encontrados na [Documentação do Azure Functions]().</span><span class="sxs-lookup"><span data-stu-id="bb570-129">Additional Functions CLI script samples can be found in the [Azure Functions documentation]().</span></span>
