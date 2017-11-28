---
title: aaaAzure exemplo de Script CLI - dimensionar um aplicativo web em todo o mundo com uma arquitetura de alta disponibilidade | Microsoft Docs
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
ms.openlocfilehash: b72fbccd7f2aaab58e4b4721e14dca14146c7c72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="eb0f2-103">Escalar um aplicativo Web em todo o mundo com uma arquitetura de alta disponibilidade</span><span class="sxs-lookup"><span data-stu-id="eb0f2-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="eb0f2-104">Nesse cenário, você criará um grupo de recursos, dois planos de serviço de aplicativo, dois aplicativos web, um perfil do Gerenciador de tráfego e dois pontos de extremidade de Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="eb0f2-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="eb0f2-105">Depois que o exercício de saudação for concluído, você terá uma alta disponibilidade arquitetura que permite que fornece disponibilidade global do seu aplicativo web com base na menor latência de rede hello.</span><span class="sxs-lookup"><span data-stu-id="eb0f2-105">Once hello exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on hello lowest network latency.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="eb0f2-106">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="eb0f2-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="eb0f2-107">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb0f2-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="eb0f2-108">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eb0f2-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="eb0f2-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="eb0f2-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="eb0f2-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="eb0f2-110">Script explanation</span></span>

<span data-ttu-id="eb0f2-111">Esse script usa Olá comandos toocreate um grupo de recursos, o aplicativo web, o perfil do Gerenciador de tráfego a seguir, e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="eb0f2-111">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="eb0f2-112">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="eb0f2-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="eb0f2-113">Command</span><span class="sxs-lookup"><span data-stu-id="eb0f2-113">Command</span></span> | <span data-ttu-id="eb0f2-114">Observações</span><span class="sxs-lookup"><span data-stu-id="eb0f2-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="eb0f2-115">az group create</span><span class="sxs-lookup"><span data-stu-id="eb0f2-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="eb0f2-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="eb0f2-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="eb0f2-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="eb0f2-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="eb0f2-118">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eb0f2-118">Creates an App Service plan.</span></span> <span data-ttu-id="eb0f2-119">Isso é como um farm de servidores para seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb0f2-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="eb0f2-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="eb0f2-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="eb0f2-121">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb0f2-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="eb0f2-122">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="eb0f2-122">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="eb0f2-123">Cria um perfil de Gerenciador de Tráfego do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb0f2-123">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="eb0f2-124">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="eb0f2-124">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="eb0f2-125">Adiciona um ponto de extremidade tooan perfil do Gerenciador de tráfego do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb0f2-125">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="eb0f2-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eb0f2-126">Next steps</span></span>

<span data-ttu-id="eb0f2-127">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="eb0f2-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="eb0f2-128">Exemplos de script CLI do serviço de aplicativo adicionais podem ser encontrados no hello [documentação do serviço de aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="eb0f2-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
