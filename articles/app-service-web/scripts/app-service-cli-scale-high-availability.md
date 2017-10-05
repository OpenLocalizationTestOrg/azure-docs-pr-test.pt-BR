---
title: Exemplo de Script CLI do Azure - dimensionar um aplicativo Web em todo o mundo com uma arquitetura de alta disponibilidade | Microsoft Docs
description: Exemplo de Script CLI do Azure - dimensionar um aplicativo Web em todo o mundo com uma arquitetura de alta disponibilidade
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4033a50-0e05-4505-8ce8-c876204b2acc
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: c368bdc48f197ff5b491d1796d85abfd339051a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="19bb0-103">Escalar um aplicativo Web em todo o mundo com uma arquitetura de alta disponibilidade</span><span class="sxs-lookup"><span data-stu-id="19bb0-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="19bb0-104">Nesse cenário, você criará um grupo de recursos, dois planos de serviço de aplicativo, dois aplicativos web, um perfil do Gerenciador de tráfego e dois pontos de extremidade de Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="19bb0-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="19bb0-105">Depois que o exercício for concluído, você terá uma alta disponibilidade a arquitetura que permite que fornece disponibilidade global do seu aplicativo Web com base na menor latência de rede.</span><span class="sxs-lookup"><span data-stu-id="19bb0-105">Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="19bb0-106">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="19bb0-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="19bb0-107">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="19bb0-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="19bb0-108">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="19bb0-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="19bb0-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="19bb0-109">Sample script</span></span>

<span data-ttu-id="19bb0-110">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "escala geográfica")]</span><span class="sxs-lookup"><span data-stu-id="19bb0-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="19bb0-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="19bb0-111">Script explanation</span></span>

<span data-ttu-id="19bb0-112">Esse script usa os seguintes comandos para criar um grupo de recursos, o aplicativo Web, o perfil do Gerenciador de tráfego e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="19bb0-112">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="19bb0-113">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="19bb0-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="19bb0-114">Command</span><span class="sxs-lookup"><span data-stu-id="19bb0-114">Command</span></span> | <span data-ttu-id="19bb0-115">Observações</span><span class="sxs-lookup"><span data-stu-id="19bb0-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="19bb0-116">az group create</span><span class="sxs-lookup"><span data-stu-id="19bb0-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="19bb0-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="19bb0-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="19bb0-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="19bb0-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="19bb0-119">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="19bb0-119">Creates an App Service plan.</span></span> <span data-ttu-id="19bb0-120">Isso é como um farm de servidores para seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="19bb0-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="19bb0-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="19bb0-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="19bb0-122">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="19bb0-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="19bb0-123">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="19bb0-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="19bb0-124">Cria um perfil de Gerenciador de Tráfego do Azure.</span><span class="sxs-lookup"><span data-stu-id="19bb0-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="19bb0-125">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="19bb0-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="19bb0-126">Adiciona um ponto de extremidade a um perfil do Gerenciador de tráfego do Azure.</span><span class="sxs-lookup"><span data-stu-id="19bb0-126">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="19bb0-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="19bb0-127">Next steps</span></span>

<span data-ttu-id="19bb0-128">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="19bb0-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="19bb0-129">Os exemplos de script da CLI do Serviço de Aplicativo adicionais podem ser encontrados na [documentação do Serviço de Aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="19bb0-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
