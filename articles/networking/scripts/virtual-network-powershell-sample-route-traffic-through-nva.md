---
title: "Exemplo de script do Azure PowerShell – Rotear o tráfego por meio de uma solução de virtualização de rede | Microsoft Docs"
description: "Exemplo de script do Azure PowerShell – Rotear o tráfego por meio de uma solução de virtualização de rede de firewall.solução de virtualização."
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 883d28dac72a66c2186d222f72b04d68e532cead
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="0a09a-103">Rotear o tráfego por meio de uma solução de virtualização de rede</span><span class="sxs-lookup"><span data-stu-id="0a09a-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="0a09a-104">Este exemplo de script cria uma rede virtual com sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="0a09a-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="0a09a-105">Ele também cria uma VM com o encaminhamento de IP habilitado para rotear o tráfego entre as duas sub-redes.</span><span class="sxs-lookup"><span data-stu-id="0a09a-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span></span> <span data-ttu-id="0a09a-106">Depois de executar o script, você pode implantar o software de rede, como um aplicativo de firewall, à VM.</span><span class="sxs-lookup"><span data-stu-id="0a09a-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span></span>

<span data-ttu-id="0a09a-107">Se necessário, instale o Azure PowerShell usando a instrução encontrada no [guia do Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) e, em seguida, execute `Login-AzureRmAccount` para criar uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="0a09a-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="0a09a-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="0a09a-108">Sample script</span></span>


<span data-ttu-id="0a09a-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Rotear o tráfego por meio de uma solução de virtualização de rede")]</span><span class="sxs-lookup"><span data-stu-id="0a09a-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="0a09a-110">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="0a09a-110">Clean up deployment</span></span> 

<span data-ttu-id="0a09a-111">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="0a09a-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a><span data-ttu-id="0a09a-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="0a09a-112">Script explanation</span></span>

<span data-ttu-id="0a09a-113">Este script usa os comandos a seguir para criar um grupo de recursos, uma rede virtual e grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="0a09a-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="0a09a-114">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="0a09a-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="0a09a-115">Command</span><span class="sxs-lookup"><span data-stu-id="0a09a-115">Command</span></span> | <span data-ttu-id="0a09a-116">Observações</span><span class="sxs-lookup"><span data-stu-id="0a09a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0a09a-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0a09a-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="0a09a-118">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="0a09a-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0a09a-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="0a09a-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="0a09a-120">Cria uma rede virtual do Azure e uma sub-rede front-end.</span><span class="sxs-lookup"><span data-stu-id="0a09a-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="0a09a-121">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="0a09a-121">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="0a09a-122">Cria as sub-redes back-end e DMZ.</span><span class="sxs-lookup"><span data-stu-id="0a09a-122">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="0a09a-123">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="0a09a-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="0a09a-124">Cria um endereço IP público para acessar a VM da Internet.</span><span class="sxs-lookup"><span data-stu-id="0a09a-124">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="0a09a-125">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="0a09a-125">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="0a09a-126">Cria uma interface de rede virtual e habilita o encaminhamento IP nela.</span><span class="sxs-lookup"><span data-stu-id="0a09a-126">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="0a09a-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="0a09a-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="0a09a-128">Cria um grupo de segurança de rede (NSG).</span><span class="sxs-lookup"><span data-stu-id="0a09a-128">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="0a09a-129">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="0a09a-129">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="0a09a-130">Cria regras de NSG que permitem as portas HTTP e HTTPS de entrada para a VM.</span><span class="sxs-lookup"><span data-stu-id="0a09a-130">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span></span> |
| [<span data-ttu-id="0a09a-131">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="0a09a-131">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| <span data-ttu-id="0a09a-132">Associa os NSGs e tabelas de rotas às sub-redes.</span><span class="sxs-lookup"><span data-stu-id="0a09a-132">Associates the NSGs and route tables to subnets.</span></span> |
| [<span data-ttu-id="0a09a-133">New-AzureRmRouteTable</span><span class="sxs-lookup"><span data-stu-id="0a09a-133">New-AzureRmRouteTable</span></span>](/powershell/module/azurerm.network/new-azurermroutetable)| <span data-ttu-id="0a09a-134">Cria uma tabela de rotas com todas as rotas.</span><span class="sxs-lookup"><span data-stu-id="0a09a-134">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="0a09a-135">New-AzureRMRouteConfig</span><span class="sxs-lookup"><span data-stu-id="0a09a-135">New-AzureRMRouteConfig</span></span>](/powershell/module/azurerm.network/new-azurermrouteconfig)| <span data-ttu-id="0a09a-136">Cria as rotas para rotear o tráfego entre sub-redes e a Internet por meio da VM.</span><span class="sxs-lookup"><span data-stu-id="0a09a-136">Creates routes to route traffic between subnets and the Internet through the VM.</span></span> |
| [<span data-ttu-id="0a09a-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="0a09a-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="0a09a-138">Cria uma máquina virtual e anexa o NIC a ela.</span><span class="sxs-lookup"><span data-stu-id="0a09a-138">Creates a virtual machine and attaches the NIC to it.</span></span> <span data-ttu-id="0a09a-139">Este comando também especifica a imagem de máquina virtual a ser usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="0a09a-139">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="0a09a-140">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0a09a-140">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | <span data-ttu-id="0a09a-141">Exclui um grupo de recursos e todos os seus recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="0a09a-141">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0a09a-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0a09a-142">Next steps</span></span>

<span data-ttu-id="0a09a-143">Para obter mais informações sobre o Azure PowerShell, confira [Documentação do Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0a09a-143">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="0a09a-144">Exemplos adicionais de script de PowerShell de rede podem ser encontrados na [Documentação de visão geral da rede do Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0a09a-144">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>