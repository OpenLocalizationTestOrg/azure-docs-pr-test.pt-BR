---
title: "aaaAzure exemplo de Script CLI - rotear o tráfego para alta disponibilidade de aplicativos | Microsoft Docs"
description: "Exemplo de script da CLI do Azure - Rotear o tráfego para alta disponibilidade de aplicativos"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: tysonn
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 2142c8bbec1dffc2f12b5500df142a429393a145
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="527ac-103">Rotear o tráfego para alta disponibilidade de aplicativos</span><span class="sxs-lookup"><span data-stu-id="527ac-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="527ac-104">Este script cria um grupo de recursos, dois planos de serviço de aplicativo, dois aplicativos web, um perfil do Gerenciador de tráfego e dois pontos de extremidade de Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="527ac-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="527ac-105">Traffic Manager direciona o aplicativo de toohello de tráfego em uma região, como região primária hello e região secundária toohello quando o aplicativo hello na região primária Olá não está disponível.</span><span class="sxs-lookup"><span data-stu-id="527ac-105">Traffic Manager directs traffic toohello application in one region as hello primary region, and toohello secondary region when hello application in hello primary region is unavailable.</span></span> <span data-ttu-id="527ac-106">Antes de executar o script hello, você deve alterar Olá MyWebApp, MyWebAppL1 e MyWebAppL2 valores toounique valores no Azure.</span><span class="sxs-lookup"><span data-stu-id="527ac-106">Before executing hello script, you must change hello MyWebApp, MyWebAppL1 and MyWebAppL2 values toounique values across Azure.</span></span> <span data-ttu-id="527ac-107">Depois de executar o script hello, você pode acessar o aplicativo de saudação em região primária Olá Olá URL mywebapp.trafficmanager.net.</span><span class="sxs-lookup"><span data-stu-id="527ac-107">After running hello script, you can access hello app in hello primary region with hello URL mywebapp.trafficmanager.net.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="527ac-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="527ac-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]


## <a name="clean-up-deployment"></a><span data-ttu-id="527ac-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="527ac-109">Clean up deployment</span></span> 

<span data-ttu-id="527ac-110">Após a execução do exemplo de script hello, Olá siga comando pode ser usado tooremove grupo de recursos de saudação, aplicativo de serviço de aplicativo e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="527ac-110">After hello script sample has been run, hello follow command can be used tooremove hello resource group, App Service app, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a><span data-ttu-id="527ac-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="527ac-111">Script explanation</span></span>

<span data-ttu-id="527ac-112">Esse script usa Olá comandos toocreate um grupo de recursos, o aplicativo web, o perfil do Gerenciador de tráfego a seguir, e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="527ac-112">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="527ac-113">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="527ac-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="527ac-114">Command</span><span class="sxs-lookup"><span data-stu-id="527ac-114">Command</span></span> | <span data-ttu-id="527ac-115">Observações</span><span class="sxs-lookup"><span data-stu-id="527ac-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="527ac-116">az group create</span><span class="sxs-lookup"><span data-stu-id="527ac-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="527ac-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="527ac-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="527ac-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="527ac-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="527ac-119">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="527ac-119">Creates an App Service plan.</span></span> <span data-ttu-id="527ac-120">Isso é como um farm de servidores para seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="527ac-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="527ac-121">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="527ac-121">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="527ac-122">Cria um aplicativo web do Azure em Olá plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="527ac-122">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="527ac-123">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="527ac-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="527ac-124">Cria um perfil de Gerenciador de Tráfego do Azure.</span><span class="sxs-lookup"><span data-stu-id="527ac-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="527ac-125">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="527ac-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="527ac-126">Adiciona um ponto de extremidade tooan perfil do Gerenciador de tráfego do Azure.</span><span class="sxs-lookup"><span data-stu-id="527ac-126">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="527ac-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="527ac-127">Next steps</span></span>

<span data-ttu-id="527ac-128">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="527ac-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="527ac-129">Exemplos de script CLI do serviço de aplicativo adicionais podem ser encontrados no hello [documentação de rede do Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="527ac-129">Additional App Service CLI script samples can be found in hello [Azure Networking documentation](../cli-samples.md).</span></span>
