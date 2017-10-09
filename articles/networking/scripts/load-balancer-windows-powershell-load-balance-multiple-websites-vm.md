---
title: "balanceamento de carga de aaaAzure exemplo de Script do PowerShell - vários sites com o Azure PowerShell | Microsoft Docs"
description: "Exemplo de Script do PowerShell do Azure - toohello de vários sites o balanceamento de carga mesma máquina virtual"
services: load-balancer
documentationcenter: load-balancer
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 316818964eb6928fe4163ef69eb7f05da2dc9636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="b3f9f-103">Balanceamento de carga de vários sites</span><span class="sxs-lookup"><span data-stu-id="b3f9f-103">Load balance multiple websites</span></span>

<span data-ttu-id="b3f9f-104">Este exemplo de script cria uma rede virtual com duas VMs (máquinas virtuais) que são membros de um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="b3f9f-105">Um balanceador de carga direcione o tráfego para separar duas toohello duas VMs de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-105">A load balancer directs traffic for two separate IP addresses toohello two VMs.</span></span> <span data-ttu-id="b3f9f-106">Após o script hello em execução, você pode implantar web server software toohello VMs e hospedar vários sites, cada qual com seu próprio endereço IP.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-106">After running hello script, you could deploy web server software toohello VMs and host multiple web sites, each with its own IP address.</span></span>

<span data-ttu-id="b3f9f-107">Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)e, em seguida, execute `Login-AzureRmAccount` toocreate uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b3f9f-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="b3f9f-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.ps1  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b3f9f-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="b3f9f-109">Clean up deployment</span></span> 

<span data-ttu-id="b3f9f-110">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b3f9f-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="b3f9f-111">Script explanation</span></span>

<span data-ttu-id="b3f9f-112">Esse script usa Olá comandos toocreate um grupo de recursos de rede virtual, o balanceador de carga e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-112">This script uses hello following commands toocreate a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="b3f9f-113">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b3f9f-114">Command</span><span class="sxs-lookup"><span data-stu-id="b3f9f-114">Command</span></span> | <span data-ttu-id="b3f9f-115">Observações</span><span class="sxs-lookup"><span data-stu-id="b3f9f-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b3f9f-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b3f9f-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="b3f9f-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b3f9f-118">New-AzureRmAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="b3f9f-118">New-AzureRmAvailabilitySet</span></span>](/powershell/module/azurerm.compute/new-azurermavailabilityset) | <span data-ttu-id="b3f9f-119">Cria um conjunto de disponibilidade do Azure tooprovide disponibilidade de alta.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-119">Creates an Azure availability set tooprovide high availability.</span></span> |
| [<span data-ttu-id="b3f9f-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="b3f9f-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="b3f9f-121">Cria uma configuração de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-121">Creates a subnet configuration.</span></span> <span data-ttu-id="b3f9f-122">Essa configuração é usada com o processo de criação de rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-122">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="b3f9f-123">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="b3f9f-123">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="b3f9f-124">Cria uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-124">Creates a virtual network.</span></span> |
| [<span data-ttu-id="b3f9f-125">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="b3f9f-125">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="b3f9f-126">Cria um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-126">Creates a public IP address.</span></span> |
| [<span data-ttu-id="b3f9f-127">New-AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="b3f9f-127">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="b3f9f-128">Cria uma configuração de IP front-end para um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-128">Creates a front end IP config for a load balancer.</span></span> |
| [<span data-ttu-id="b3f9f-129">New-AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="b3f9f-129">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="b3f9f-130">Cria uma configuração de pool de endereços de back-end para um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-130">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="b3f9f-131">New-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="b3f9f-131">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="b3f9f-132">Cria uma investigação NLB.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-132">Creates an NLB probe.</span></span> <span data-ttu-id="b3f9f-133">Uma investigação NLB é usado toomonitor cada VM no conjunto NLB hello.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-133">An NLB probe is used toomonitor each VM in hello NLB set.</span></span> <span data-ttu-id="b3f9f-134">Se qualquer VM ficar inacessível, o tráfego não é roteado toohello VM.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-134">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="b3f9f-135">New-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="b3f9f-135">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="b3f9f-136">Cria uma regra NLB.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-136">Creates an NLB rule.</span></span> <span data-ttu-id="b3f9f-137">Neste exemplo, uma regra é criada para a porta 80.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-137">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="b3f9f-138">Como o tráfego HTTP chega ao Olá NLB, é roteado tooport 80 uma das VMs Olá Olá NLB conjunto.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-138">As HTTP traffic arrives at hello NLB, it is routed tooport 80 one of hello VMs in hello NLB set.</span></span> |
| [<span data-ttu-id="b3f9f-139">New-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="b3f9f-139">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="b3f9f-140">Cria um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-140">Creates a load balancer.</span></span> |
| [<span data-ttu-id="b3f9f-141">New-AzureRmNetworkInterfaceIpConfig</span><span class="sxs-lookup"><span data-stu-id="b3f9f-141">New-AzureRmNetworkInterfaceIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterfaceipconfig) | <span data-ttu-id="b3f9f-142">Define os recursos avançados para uma interface de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-142">Defines advanced features for a virtual network interface.</span></span> |
| [<span data-ttu-id="b3f9f-143">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="b3f9f-143">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="b3f9f-144">Cria um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-144">Creates a network interface.</span></span> |
| [<span data-ttu-id="b3f9f-145">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="b3f9f-145">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="b3f9f-146">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-146">Creates a VM configuration.</span></span> <span data-ttu-id="b3f9f-147">Essa configuração inclui informações como nome da VM, sistema operacional e credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-147">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="b3f9f-148">Olá configuração será usada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-148">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="b3f9f-149">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="b3f9f-149">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="b3f9f-150">Crie uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-150">Create a virtual machine.</span></span> |
|[<span data-ttu-id="b3f9f-151">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b3f9f-151">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="b3f9f-152">Remove um grupo de recursos e todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-152">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b3f9f-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b3f9f-153">Next steps</span></span>

<span data-ttu-id="b3f9f-154">Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b3f9f-154">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="b3f9f-155">Exemplos de script do PowerShell rede adicionais podem ser encontrados no hello [documentação de visão geral da rede do Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b3f9f-155">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
