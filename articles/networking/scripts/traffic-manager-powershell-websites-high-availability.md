---
title: "Exemplo de script do Azure PowerShell – Rotear o tráfego para alta disponibilidade de aplicativos | Microsoft Docs"
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
ms.openlocfilehash: 2f0ac4fd1779661aab04bafb217e64af5d619a2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="4419c-103">Rotear o tráfego para alta disponibilidade de aplicativos</span><span class="sxs-lookup"><span data-stu-id="4419c-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="4419c-104">Este script cria um grupo de recursos, dois planos de serviço de aplicativo, dois aplicativos web, um perfil do Gerenciador de tráfego e dois pontos de extremidade de Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="4419c-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="4419c-105">O Gerenciador de Tráfego direciona o tráfego para o aplicativo em uma região como a região primária, e para a região secundária quando o aplicativo na região primária não estiver disponível.</span><span class="sxs-lookup"><span data-stu-id="4419c-105">Traffic Manager directs traffic to the application in one region as the primary region, and to the secondary region when the application in the primary region is unavailable.</span></span> <span data-ttu-id="4419c-106">Antes de executar o script, você deve alterar os valores MyWebApp, MyWebAppL1 e MyWebAppL2 para valores exclusivos no Azure.</span><span class="sxs-lookup"><span data-stu-id="4419c-106">Before executing the script, you must change the MyWebApp, MyWebAppL1 and MyWebAppL2 values to unique values across Azure.</span></span> <span data-ttu-id="4419c-107">Depois de executar o script, você pode acessar o aplicativo na região primária com a URL mywebapp.trafficmanager.net.</span><span class="sxs-lookup"><span data-stu-id="4419c-107">After running the script, you can access the app in the primary region with the URL mywebapp.trafficmanager.net.</span></span>

<span data-ttu-id="4419c-108">Se necessário, instale o Azure PowerShell usando a instrução encontrada no [guia do Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) e, em seguida, execute `Login-AzureRmAccount` para criar uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="4419c-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4419c-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="4419c-109">Sample script</span></span>

<span data-ttu-id="4419c-110">[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Rotear o tráfego para alta disponibilidade")]</span><span class="sxs-lookup"><span data-stu-id="4419c-110">[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]</span></span>


<span data-ttu-id="4419c-111">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="4419c-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a><span data-ttu-id="4419c-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="4419c-112">Script explanation</span></span>

<span data-ttu-id="4419c-113">Esse script usa os seguintes comandos para criar um grupo de recursos, o aplicativo Web, o perfil do Gerenciador de tráfego e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="4419c-113">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="4419c-114">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="4419c-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4419c-115">Command</span><span class="sxs-lookup"><span data-stu-id="4419c-115">Command</span></span> | <span data-ttu-id="4419c-116">Observações</span><span class="sxs-lookup"><span data-stu-id="4419c-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4419c-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4419c-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="4419c-118">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="4419c-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4419c-119">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="4419c-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="4419c-120">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4419c-120">Creates an App Service plan.</span></span> <span data-ttu-id="4419c-121">Isso é como um farm de servidores para seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="4419c-121">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="4419c-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="4419c-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="4419c-123">Cria um aplicativo web do Azure no plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4419c-123">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="4419c-124">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="4419c-124">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="4419c-125">Cria um aplicativo web do Azure no plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4419c-125">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="4419c-126">New-AzureRmTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="4419c-126">New-AzureRmTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="4419c-127">Cria um perfil de Gerenciador de Tráfego do Azure.</span><span class="sxs-lookup"><span data-stu-id="4419c-127">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="4419c-128">New-AzureRmTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="4419c-128">New-AzureRmTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="4419c-129">Adiciona um ponto de extremidade a um perfil do Gerenciador de tráfego do Azure.</span><span class="sxs-lookup"><span data-stu-id="4419c-129">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4419c-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4419c-130">Next steps</span></span>

<span data-ttu-id="4419c-131">Para obter mais informações sobre o Azure PowerShell, confira [Documentação do Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4419c-131">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="4419c-132">Exemplos adicionais de script de PowerShell de rede podem ser encontrados na [Documentação de visão geral da rede do Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4419c-132">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>