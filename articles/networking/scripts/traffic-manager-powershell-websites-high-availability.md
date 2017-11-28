---
title: "Exemplo de Script do PowerShell - rotear o tráfego para alta disponibilidade de aplicativos de aaaAzure | Microsoft Docs"
description: "Exemplo de script do Azure PowerShell – Rotear o tráfego para alta disponibilidade de aplicativos"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: georgewallace
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 11d15780403b4ed79e85d7b3495bc5d674bfdaee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="9dc55-103">Rotear o tráfego para alta disponibilidade de aplicativos</span><span class="sxs-lookup"><span data-stu-id="9dc55-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="9dc55-104">Este script cria um grupo de recursos, dois planos de serviço de aplicativo, dois aplicativos web, um perfil do Gerenciador de tráfego e dois pontos de extremidade de Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="9dc55-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="9dc55-105">Traffic Manager direciona o aplicativo de toohello de tráfego em uma região, como região primária hello e região secundária toohello quando o aplicativo hello na região primária Olá não está disponível.</span><span class="sxs-lookup"><span data-stu-id="9dc55-105">Traffic Manager directs traffic toohello application in one region as hello primary region, and toohello secondary region when hello application in hello primary region is unavailable.</span></span> <span data-ttu-id="9dc55-106">Antes de executar o script hello, você deve alterar Olá MyWebApp, MyWebAppL1 e MyWebAppL2 valores toounique valores no Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc55-106">Before executing hello script, you must change hello MyWebApp, MyWebAppL1 and MyWebAppL2 values toounique values across Azure.</span></span> <span data-ttu-id="9dc55-107">Depois de executar o script hello, você pode acessar o aplicativo de saudação em região primária Olá Olá URL mywebapp.trafficmanager.net.</span><span class="sxs-lookup"><span data-stu-id="9dc55-107">After running hello script, you can access hello app in hello primary region with hello URL mywebapp.trafficmanager.net.</span></span>

<span data-ttu-id="9dc55-108">Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)e, em seguida, execute `Login-AzureRmAccount` toocreate uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc55-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9dc55-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="9dc55-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]


<span data-ttu-id="9dc55-110">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="9dc55-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a><span data-ttu-id="9dc55-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="9dc55-111">Script explanation</span></span>

<span data-ttu-id="9dc55-112">Esse script usa Olá comandos toocreate um grupo de recursos, o aplicativo web, o perfil do Gerenciador de tráfego a seguir, e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="9dc55-112">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="9dc55-113">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="9dc55-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9dc55-114">Command</span><span class="sxs-lookup"><span data-stu-id="9dc55-114">Command</span></span> | <span data-ttu-id="9dc55-115">Observações</span><span class="sxs-lookup"><span data-stu-id="9dc55-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9dc55-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9dc55-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="9dc55-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="9dc55-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9dc55-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="9dc55-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="9dc55-119">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9dc55-119">Creates an App Service plan.</span></span> <span data-ttu-id="9dc55-120">Isso é como um farm de servidores para seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc55-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="9dc55-121">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="9dc55-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="9dc55-122">Cria um aplicativo web do Azure em Olá plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9dc55-122">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="9dc55-123">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="9dc55-123">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="9dc55-124">Cria um aplicativo web do Azure em Olá plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9dc55-124">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="9dc55-125">New-AzureRmTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="9dc55-125">New-AzureRmTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="9dc55-126">Cria um perfil de Gerenciador de Tráfego do Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc55-126">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="9dc55-127">New-AzureRmTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="9dc55-127">New-AzureRmTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="9dc55-128">Adiciona um ponto de extremidade tooan perfil do Gerenciador de tráfego do Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc55-128">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9dc55-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9dc55-129">Next steps</span></span>

<span data-ttu-id="9dc55-130">Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9dc55-130">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="9dc55-131">Exemplos de script do PowerShell rede adicionais podem ser encontrados no hello [documentação de visão geral da rede do Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9dc55-131">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
