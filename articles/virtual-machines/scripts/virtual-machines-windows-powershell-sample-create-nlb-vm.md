---
title: aaaAzure exemplo de Script do PowerShell - criar uma VM do Windows NLB | Microsoft Docs
description: "Amostra de script do Azure PowerShell – Criar uma VM NBL Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 60a48c5f243c8ff3ab886437ae45b21ce069ea4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="6e9be-103">Como balancear a carga de tráfego entre máquinas virtuais altamente disponíveis</span><span class="sxs-lookup"><span data-stu-id="6e9be-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="6e9be-104">Este exemplo de script cria todo o necessário toorun várias máquinas virtuais de Windows Server 2016 configurado em uma alta disponibilidade e de carga balanceada configuração.</span><span class="sxs-lookup"><span data-stu-id="6e9be-104">This script sample creates everything needed toorun several Windows Server 2016 virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="6e9be-105">Após o script hello em execução, você terá três máquinas virtuais, tooan ingressado no conjunto de disponibilidade do Azure e acessível por meio de um balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e9be-105">After running hello script, you will have three virtual machines, joined tooan Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6e9be-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="6e9be-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Create VM NLB")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6e9be-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="6e9be-107">Clean up deployment</span></span> 

<span data-ttu-id="6e9be-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="6e9be-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6e9be-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="6e9be-109">Script explanation</span></span>

<span data-ttu-id="6e9be-110">Esse script usa Olá implantação de saudação toocreate comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="6e9be-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="6e9be-111">Cada item na tabela de saudação vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="6e9be-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6e9be-112">Command</span><span class="sxs-lookup"><span data-stu-id="6e9be-112">Command</span></span> | <span data-ttu-id="6e9be-113">Observações</span><span class="sxs-lookup"><span data-stu-id="6e9be-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6e9be-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6e9be-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="6e9be-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="6e9be-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6e9be-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="6e9be-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="6e9be-117">Cria uma configuração de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="6e9be-117">Creates a subnet configuration.</span></span> <span data-ttu-id="6e9be-118">Essa configuração é usada com o processo de criação de rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="6e9be-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="6e9be-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="6e9be-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="6e9be-120">Cria uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="6e9be-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="6e9be-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="6e9be-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="6e9be-122">Cria um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="6e9be-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="6e9be-123">New-AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="6e9be-123">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="6e9be-124">Cria uma configuração de IP front-end para um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="6e9be-124">Creates a front-end IP configuration for a load balancer.</span></span> |
| [<span data-ttu-id="6e9be-125">New-AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="6e9be-125">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="6e9be-126">Cria uma configuração de pool de endereços de back-end para um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="6e9be-126">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="6e9be-127">New-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="6e9be-127">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="6e9be-128">Cria uma configuração de investigação para um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="6e9be-128">Creates a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="6e9be-129">New-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="6e9be-129">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="6e9be-130">Cria uma configuração de regra para um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="6e9be-130">Creates a rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="6e9be-131">New-AzureRmLoadBalancerInboundNatRuleConfig</span><span class="sxs-lookup"><span data-stu-id="6e9be-131">New-AzureRmLoadBalancerInboundNatRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | <span data-ttu-id="6e9be-132">Cria uma configuração de regra NAT de entrada para um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="6e9be-132">Creates an inbound NAT rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="6e9be-133">New-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="6e9be-133">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="6e9be-134">Cria um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="6e9be-134">Creates a load balancer.</span></span> |
| [<span data-ttu-id="6e9be-135">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="6e9be-135">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="6e9be-136">Cria uma configuração de regra de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="6e9be-136">Creates a network security group rule configuration.</span></span> <span data-ttu-id="6e9be-137">Essa configuração é usada toocreate uma regra NSG quando Olá NSG é criado.</span><span class="sxs-lookup"><span data-stu-id="6e9be-137">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="6e9be-138">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="6e9be-138">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="6e9be-139">Cria um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="6e9be-139">Creates a network security group.</span></span> |
| [<span data-ttu-id="6e9be-140">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="6e9be-140">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="6e9be-141">Obtém informações de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="6e9be-141">Gets subnet information.</span></span> <span data-ttu-id="6e9be-142">Essas informações são usadas ao criar um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="6e9be-142">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="6e9be-143">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="6e9be-143">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="6e9be-144">Cria um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="6e9be-144">Creates a network interface.</span></span> |
| [<span data-ttu-id="6e9be-145">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="6e9be-145">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="6e9be-146">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="6e9be-146">Creates a VM configuration.</span></span> <span data-ttu-id="6e9be-147">Essa configuração inclui informações como nome da VM, sistema operacional e credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="6e9be-147">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="6e9be-148">Olá configuração será usada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="6e9be-148">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="6e9be-149">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="6e9be-149">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="6e9be-150">Crie uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6e9be-150">Create a virtual machine.</span></span> |
|[<span data-ttu-id="6e9be-151">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6e9be-151">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="6e9be-152">Remove um grupo de recursos e todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="6e9be-152">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6e9be-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6e9be-153">Next steps</span></span>

<span data-ttu-id="6e9be-154">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6e9be-154">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="6e9be-155">Exemplos de script do PowerShell de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6e9be-155">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
