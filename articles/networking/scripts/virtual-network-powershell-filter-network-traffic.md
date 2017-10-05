---
title: "Exemplo de script do Azure PowerShell – Filtrar o tráfego de rede da VM | Microsoft Docs"
description: "Exemplo de script do Azure PowerShell – Filtrar o tráfego de entrada e saída de rede da VM."
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
ms.openlocfilehash: e871ba2f370157936c2aaabc804dc9f5aea6d7ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="d2a57-103">Filtrar o tráfego de entrada e saída de rede da VM</span><span class="sxs-lookup"><span data-stu-id="d2a57-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="d2a57-104">Este exemplo de script cria uma rede virtual com sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="d2a57-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="d2a57-105">O tráfego de rede de entrada para a sub-rede de front-end é limitado a HTTP e HTTPS, enquanto o tráfego de rede de saída para a Internet da sub-rede de back-end não é permitido.</span><span class="sxs-lookup"><span data-stu-id="d2a57-105">Inbound network traffic to the front-end subnet is limited to HTTP, and HTTPS, while outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> <span data-ttu-id="d2a57-106">Depois de executar o script, você terá uma máquina virtual com dois NICs.</span><span class="sxs-lookup"><span data-stu-id="d2a57-106">After running the script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="d2a57-107">Cada NIC pode estar conectado a uma sub-rede diferente.</span><span class="sxs-lookup"><span data-stu-id="d2a57-107">Each NIC is connected to a different subnet.</span></span>

<span data-ttu-id="d2a57-108">Se necessário, instale o Azure PowerShell usando a instrução encontrada no [guia do Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) e, em seguida, execute `Login-AzureRmAccount` para criar uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="d2a57-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d2a57-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="d2a57-109">Sample script</span></span>


<span data-ttu-id="d2a57-110">[!code-powershell[main](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "Filtrar tráfego de rede da VM")]</span><span class="sxs-lookup"><span data-stu-id="d2a57-110">[!code-powershell[main](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "Filter VM network traffic")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d2a57-111">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="d2a57-111">Clean up deployment</span></span> 

<span data-ttu-id="d2a57-112">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="d2a57-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d2a57-113">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="d2a57-113">Script explanation</span></span>

<span data-ttu-id="d2a57-114">Este script usa os comandos a seguir para criar um grupo de recursos, uma rede virtual e grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="d2a57-114">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="d2a57-115">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="d2a57-115">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="d2a57-116">Command</span><span class="sxs-lookup"><span data-stu-id="d2a57-116">Command</span></span> | <span data-ttu-id="d2a57-117">Observações</span><span class="sxs-lookup"><span data-stu-id="d2a57-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d2a57-118">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d2a57-118">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d2a57-119">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="d2a57-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d2a57-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="d2a57-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="d2a57-121">Cria um objeto de configuração de sub-rede</span><span class="sxs-lookup"><span data-stu-id="d2a57-121">Creates a subnet configuration object</span></span> |
| [<span data-ttu-id="d2a57-122">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="d2a57-122">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="d2a57-123">Cria uma rede virtual do Azure e uma sub-rede front-end.</span><span class="sxs-lookup"><span data-stu-id="d2a57-123">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="d2a57-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="d2a57-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="d2a57-125">Cria regras de segurança a serem atribuídas a um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="d2a57-125">Creates security rules to be assigned to a network security group.</span></span> |
| [<span data-ttu-id="d2a57-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="d2a57-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) |<span data-ttu-id="d2a57-127">Cria regras NSG que permitem ou bloqueiam portas específicas para sub-redes específicas.</span><span class="sxs-lookup"><span data-stu-id="d2a57-127">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="d2a57-128">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="d2a57-128">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="d2a57-129">Associa os NSGs às sub-redes.</span><span class="sxs-lookup"><span data-stu-id="d2a57-129">Associates NSGs to subnets.</span></span> |
| [<span data-ttu-id="d2a57-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="d2a57-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="d2a57-131">Cria um endereço IP público para acessar a VM da Internet.</span><span class="sxs-lookup"><span data-stu-id="d2a57-131">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="d2a57-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="d2a57-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="d2a57-133">Cria as interfaces de rede virtual e as anexa às sub-redes de front-end e back-end da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="d2a57-133">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="d2a57-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="d2a57-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="d2a57-135">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="d2a57-135">Creates a VM configuration.</span></span> <span data-ttu-id="d2a57-136">Essa configuração inclui informações como nome da VM, sistema operacional e credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="d2a57-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="d2a57-137">A configuração é usada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="d2a57-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="d2a57-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="d2a57-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="d2a57-139">Crie uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d2a57-139">Create a virtual machine.</span></span> |
|[<span data-ttu-id="d2a57-140">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d2a57-140">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="d2a57-141">Remove um grupo de recursos e todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="d2a57-141">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d2a57-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d2a57-142">Next steps</span></span>

<span data-ttu-id="d2a57-143">Para obter mais informações sobre o Azure PowerShell, confira [Documentação do Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d2a57-143">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="d2a57-144">Exemplos adicionais de script de PowerShell de rede podem ser encontrados na [Documentação de visão geral da rede do Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d2a57-144">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>