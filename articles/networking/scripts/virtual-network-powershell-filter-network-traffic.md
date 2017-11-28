---
title: "exemplo de script do PowerShell aaaAzure - o tráfego de rede VM de filtro | Microsoft Docs"
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
ms.openlocfilehash: 39eae6a43a8dc7f9fc616ef3ec50f95443fd3547
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="cc292-103">Filtrar o tráfego de entrada e saída de rede da VM</span><span class="sxs-lookup"><span data-stu-id="cc292-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="cc292-104">Este exemplo de script cria uma rede virtual com sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="cc292-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="cc292-105">O tráfego de rede de entrada toohello front-end subrede é limitada tooHTTP e toohello Internet de sub-rede de back-end de saudação não é permitida o tráfego HTTPS, enquanto a saída.</span><span class="sxs-lookup"><span data-stu-id="cc292-105">Inbound network traffic toohello front-end subnet is limited tooHTTP, and HTTPS, while outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> <span data-ttu-id="cc292-106">Depois de executar o script hello, você terá uma máquina virtual com dois NICs.</span><span class="sxs-lookup"><span data-stu-id="cc292-106">After running hello script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="cc292-107">Cada NIC é conectado tooa outra sub-rede.</span><span class="sxs-lookup"><span data-stu-id="cc292-107">Each NIC is connected tooa different subnet.</span></span>

<span data-ttu-id="cc292-108">Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)e, em seguida, execute `Login-AzureRmAccount` toocreate uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="cc292-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="cc292-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="cc292-109">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a><span data-ttu-id="cc292-110">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="cc292-110">Clean up deployment</span></span> 

<span data-ttu-id="cc292-111">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="cc292-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="cc292-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="cc292-112">Script explanation</span></span>

<span data-ttu-id="cc292-113">Esse script usa Olá toocreate comandos a seguir, um grupo de recursos, a rede virtual e grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="cc292-113">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="cc292-114">Cada comando na tabela Olá vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="cc292-114">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="cc292-115">Command</span><span class="sxs-lookup"><span data-stu-id="cc292-115">Command</span></span> | <span data-ttu-id="cc292-116">Observações</span><span class="sxs-lookup"><span data-stu-id="cc292-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cc292-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cc292-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="cc292-118">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="cc292-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="cc292-119">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="cc292-119">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="cc292-120">Cria um objeto de configuração de sub-rede</span><span class="sxs-lookup"><span data-stu-id="cc292-120">Creates a subnet configuration object</span></span> |
| [<span data-ttu-id="cc292-121">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="cc292-121">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="cc292-122">Cria uma rede virtual do Azure e uma sub-rede front-end.</span><span class="sxs-lookup"><span data-stu-id="cc292-122">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="cc292-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="cc292-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="cc292-124">Cria toobe de regras de segurança atribuído a grupos de segurança de rede tooa.</span><span class="sxs-lookup"><span data-stu-id="cc292-124">Creates security rules toobe assigned tooa network security group.</span></span> |
| [<span data-ttu-id="cc292-125">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="cc292-125">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) |<span data-ttu-id="cc292-126">Cria regras NSG que permitam ou bloqueiem as sub-redes de toospecific portas específicas.</span><span class="sxs-lookup"><span data-stu-id="cc292-126">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="cc292-127">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="cc292-127">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="cc292-128">Associa os NSGs toosubnets.</span><span class="sxs-lookup"><span data-stu-id="cc292-128">Associates NSGs toosubnets.</span></span> |
| [<span data-ttu-id="cc292-129">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="cc292-129">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="cc292-130">Cria um tooaccess endereço IP público Olá VM de saudação à Internet.</span><span class="sxs-lookup"><span data-stu-id="cc292-130">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="cc292-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="cc292-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="cc292-132">Cria as interfaces de rede virtual e os conecta sub-redes da rede virtual toohello de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="cc292-132">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="cc292-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="cc292-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="cc292-134">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="cc292-134">Creates a VM configuration.</span></span> <span data-ttu-id="cc292-135">Essa configuração inclui informações como nome da VM, sistema operacional e credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="cc292-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="cc292-136">Olá configuração será usada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="cc292-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="cc292-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="cc292-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="cc292-138">Crie uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cc292-138">Create a virtual machine.</span></span> |
|[<span data-ttu-id="cc292-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cc292-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="cc292-140">Remove um grupo de recursos e todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="cc292-140">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cc292-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cc292-141">Next steps</span></span>

<span data-ttu-id="cc292-142">Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cc292-142">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="cc292-143">Exemplos de script do PowerShell rede adicionais podem ser encontrados no hello [documentação de visão geral da rede do Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc292-143">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
