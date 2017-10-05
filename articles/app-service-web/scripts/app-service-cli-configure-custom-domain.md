---
title: "Exemplo de Script CLI do Azure - mapeie um domínio personalizado para um aplicativo Web | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - mapeie um domínio personalizado para um aplicativo Web"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5ac4a680-cc73-4578-bcd6-8668c08802c2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6712be8a551731fbafd92ef19564e89399e23e76
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="map-a-custom-domain-to-a-web-app"></a><span data-ttu-id="e6069-103">Mapear um domínio para um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="e6069-103">Map a custom domain to a web app</span></span>

<span data-ttu-id="e6069-104">Este script de exemplo cria um aplicativo Web no serviço de aplicativo com seus recursos relacionados e, em seguida, mapeia `www.<yourdomain>` a ele.</span><span class="sxs-lookup"><span data-stu-id="e6069-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` to it.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e6069-105">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e6069-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e6069-106">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="e6069-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="e6069-107">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e6069-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="e6069-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="e6069-108">Sample script</span></span>

<span data-ttu-id="e6069-109">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Mapear um domínio personalizado para um aplicativo Web")]</span><span class="sxs-lookup"><span data-stu-id="e6069-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e6069-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="e6069-110">Script explanation</span></span>

<span data-ttu-id="e6069-111">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="e6069-111">This script uses the following commands.</span></span> <span data-ttu-id="e6069-112">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="e6069-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e6069-113">Command</span><span class="sxs-lookup"><span data-stu-id="e6069-113">Command</span></span> | <span data-ttu-id="e6069-114">Observações</span><span class="sxs-lookup"><span data-stu-id="e6069-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e6069-115">az group create</span><span class="sxs-lookup"><span data-stu-id="e6069-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e6069-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="e6069-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e6069-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="e6069-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="e6069-118">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e6069-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="e6069-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="e6069-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="e6069-120">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6069-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="e6069-121">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="e6069-121">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="e6069-122">Mapeia um domínio personalizado para um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="e6069-122">Maps a custom domain to a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e6069-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e6069-123">Next steps</span></span>

<span data-ttu-id="e6069-124">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e6069-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e6069-125">Os exemplos de script da CLI do Serviço de Aplicativo adicionais podem ser encontrados na [documentação do Serviço de Aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e6069-125">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
