---
title: "exemplo de script do PowerShell aaaAzure - rotear o tráfego por meio de um dispositivo de rede virtual | Microsoft Docs"
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
ms.openlocfilehash: 3b999f3289d654c00d5becb973e2883896457d52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="ea834-103">Rotear o tráfego por meio de uma solução de virtualização de rede</span><span class="sxs-lookup"><span data-stu-id="ea834-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="ea834-104">Este exemplo de script cria uma rede virtual com sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="ea834-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="ea834-105">Ele também cria uma VM com tráfego tooroute habilitado entre duas sub-redes de saudação de encaminhamento IP.</span><span class="sxs-lookup"><span data-stu-id="ea834-105">It also creates a VM with IP forwarding enabled tooroute traffic between hello two subnets.</span></span> <span data-ttu-id="ea834-106">Depois de executar o script hello, você pode implantar o software de rede, como um aplicativo de firewall, toohello VM.</span><span class="sxs-lookup"><span data-stu-id="ea834-106">After running hello script you can deploy network software, such as a firewall application, toohello VM.</span></span>

<span data-ttu-id="ea834-107">Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)e, em seguida, execute `Login-AzureRmAccount` toocreate uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="ea834-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ea834-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="ea834-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ea834-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="ea834-109">Clean up deployment</span></span> 

<span data-ttu-id="ea834-110">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="ea834-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a><span data-ttu-id="ea834-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="ea834-111">Script explanation</span></span>

<span data-ttu-id="ea834-112">Esse script usa Olá toocreate comandos a seguir, um grupo de recursos, a rede virtual e grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="ea834-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="ea834-113">Cada comando na tabela Olá vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="ea834-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="ea834-114">Command</span><span class="sxs-lookup"><span data-stu-id="ea834-114">Command</span></span> | <span data-ttu-id="ea834-115">Observações</span><span class="sxs-lookup"><span data-stu-id="ea834-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ea834-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ea834-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="ea834-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="ea834-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ea834-118">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="ea834-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="ea834-119">Cria uma rede virtual do Azure e uma sub-rede front-end.</span><span class="sxs-lookup"><span data-stu-id="ea834-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="ea834-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ea834-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="ea834-121">Cria as sub-redes back-end e DMZ.</span><span class="sxs-lookup"><span data-stu-id="ea834-121">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="ea834-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="ea834-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="ea834-123">Cria um tooaccess endereço IP público Olá VM de saudação à Internet.</span><span class="sxs-lookup"><span data-stu-id="ea834-123">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="ea834-124">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="ea834-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="ea834-125">Cria uma interface de rede virtual e habilita o encaminhamento IP nela.</span><span class="sxs-lookup"><span data-stu-id="ea834-125">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="ea834-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="ea834-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="ea834-127">Cria um grupo de segurança de rede (NSG).</span><span class="sxs-lookup"><span data-stu-id="ea834-127">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="ea834-128">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="ea834-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="ea834-129">Cria regras NSG que permitem que as portas HTTP e HTTPS de entrada toohello VM.</span><span class="sxs-lookup"><span data-stu-id="ea834-129">Creates NSG rules that allow HTTP and HTTPS ports inbound toohello VM.</span></span> |
| [<span data-ttu-id="ea834-130">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ea834-130">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| <span data-ttu-id="ea834-131">Associa Olá NSGs e toosubnets de tabelas de rota.</span><span class="sxs-lookup"><span data-stu-id="ea834-131">Associates hello NSGs and route tables toosubnets.</span></span> |
| [<span data-ttu-id="ea834-132">New-AzureRmRouteTable</span><span class="sxs-lookup"><span data-stu-id="ea834-132">New-AzureRmRouteTable</span></span>](/powershell/module/azurerm.network/new-azurermroutetable)| <span data-ttu-id="ea834-133">Cria uma tabela de rotas com todas as rotas.</span><span class="sxs-lookup"><span data-stu-id="ea834-133">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="ea834-134">New-AzureRMRouteConfig</span><span class="sxs-lookup"><span data-stu-id="ea834-134">New-AzureRMRouteConfig</span></span>](/powershell/module/azurerm.network/new-azurermrouteconfig)| <span data-ttu-id="ea834-135">Cria rotas tooroute tráfego entre as sub-redes e saudação da Internet por meio de saudação VM.</span><span class="sxs-lookup"><span data-stu-id="ea834-135">Creates routes tooroute traffic between subnets and hello Internet through hello VM.</span></span> |
| [<span data-ttu-id="ea834-136">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="ea834-136">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="ea834-137">Cria uma máquina virtual e anexa Olá NIC tooit.</span><span class="sxs-lookup"><span data-stu-id="ea834-137">Creates a virtual machine and attaches hello NIC tooit.</span></span> <span data-ttu-id="ea834-138">Esse comando também especifica Olá toouse de imagem de máquina virtual e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="ea834-138">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="ea834-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ea834-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | <span data-ttu-id="ea834-140">Exclui um grupo de recursos e todos os seus recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="ea834-140">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ea834-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ea834-141">Next steps</span></span>

<span data-ttu-id="ea834-142">Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ea834-142">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="ea834-143">Exemplos de script do PowerShell rede adicionais podem ser encontrados no hello [documentação de visão geral da rede do Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ea834-143">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
