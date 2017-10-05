---
title: "Exemplo de Script do Azure PowerShell – Abrir porta de aplicativo no balanceador de carga | Microsoft Docs"
description: "Exemplo de Script do Azure PowerShell – Abrir uma porta no Azure Load Balancer para um aplicativo do Service Fabric."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 2958bdef0889076249918608c04c66678fa80b97
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="open-an-application-port-in-the-azure-load-balancer"></a><span data-ttu-id="8a4b2-103">Abrir uma porta de aplicativo no Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="8a4b2-103">Open an application port in the Azure load balancer</span></span>

<span data-ttu-id="8a4b2-104">Um aplicativo do Service Fabric em execução no Azure fica por trás do Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="8a4b2-104">A Service Fabric application running in Azure sits behind the Azure load balancer.</span></span> <span data-ttu-id="8a4b2-105">Este exemplo de script abre uma porta em um Azure Load Balancer para que um aplicativo do Service Fabric possa se comunicar com clientes externos.</span><span class="sxs-lookup"><span data-stu-id="8a4b2-105">This sample script opens a port in an Azure load balancer so that a Service Fabric application can communicate with external clients.</span></span> <span data-ttu-id="8a4b2-106">Personalize os parâmetros conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="8a4b2-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="8a4b2-107">Se necessário, instale o módulo Service Fabric do PowerShell com o [SDK do Service Fabric](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8a4b2-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="8a4b2-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="8a4b2-108">Sample script</span></span>

<span data-ttu-id="8a4b2-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Abrir uma porta no balanceador de carga")]</span><span class="sxs-lookup"><span data-stu-id="8a4b2-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in the load balancer")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="8a4b2-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="8a4b2-110">Script explanation</span></span>

<span data-ttu-id="8a4b2-111">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="8a4b2-111">This script uses the following commands.</span></span> <span data-ttu-id="8a4b2-112">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="8a4b2-112">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="8a4b2-113">Command</span><span class="sxs-lookup"><span data-stu-id="8a4b2-113">Command</span></span> | <span data-ttu-id="8a4b2-114">Observações</span><span class="sxs-lookup"><span data-stu-id="8a4b2-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8a4b2-115">Get-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="8a4b2-115">Get-AzureRmResource</span></span>](/powershell/module/azurerm.resources/get-azurermresource) | <span data-ttu-id="8a4b2-116">Obtém um recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="8a4b2-116">Gets an Azure resource.</span></span>  |
| [<span data-ttu-id="8a4b2-117">Get-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="8a4b2-117">Get-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancer) | <span data-ttu-id="8a4b2-118">Obtém o Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="8a4b2-118">Gets the Azure load balancer.</span></span> |
| [<span data-ttu-id="8a4b2-119">Add-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="8a4b2-119">Add-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) | <span data-ttu-id="8a4b2-120">Adiciona uma configuração de investigação a um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="8a4b2-120">Adds a probe configuration to a load balancer.</span></span>|
| [<span data-ttu-id="8a4b2-121">Get-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="8a4b2-121">Get-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancerprobeconfig) | <span data-ttu-id="8a4b2-122">Obtém uma configuração de investigação para um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="8a4b2-122">Gets a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="8a4b2-123">Add-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="8a4b2-123">Add-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) | <span data-ttu-id="8a4b2-124">Adiciona uma configuração de regra a um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="8a4b2-124">Adds a rule configuration to a load balancer.</span></span> |
| [<span data-ttu-id="8a4b2-125">Set-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="8a4b2-125">Set-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/set-azurermloadbalancer) | <span data-ttu-id="8a4b2-126">Define a meta de estado para um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="8a4b2-126">Sets the goal state for a load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8a4b2-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8a4b2-127">Next steps</span></span>

<span data-ttu-id="8a4b2-128">Para obter mais informações sobre o módulo do Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8a4b2-128">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="8a4b2-129">Mais exemplos do PowerShell para o Azure Service Fabric podem ser encontrados nos [exemplos do Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8a4b2-129">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
