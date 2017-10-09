---
title: "aaaAzure exemplo de script do PowerShell - criar uma rede para aplicativos de várias camadas | Microsoft Docs"
description: "Exemplo de script do Azure PowerShell – Criar uma rede virtual para aplicativos de várias camadas."
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
ms.openlocfilehash: 46d6d16dc5dbc8be467359f31346f017727b1abe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="ce6b1-103">Criar uma rede para aplicativos de várias camadas</span><span class="sxs-lookup"><span data-stu-id="ce6b1-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="ce6b1-104">Este exemplo de script cria uma rede virtual com sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="ce6b1-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="ce6b1-105">Sub-rede front-end do tráfego toohello é tooHTTP limitada e SSH, enquanto o tráfego toohello sub-rede back-end é tooMySQL limitado, porta 3306.</span><span class="sxs-lookup"><span data-stu-id="ce6b1-105">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> <span data-ttu-id="ce6b1-106">Após o script hello em execução, você terá duas máquinas virtuais em cada sub-rede que você pode implantar o servidor web e o software MySQL.</span><span class="sxs-lookup"><span data-stu-id="ce6b1-106">After running hello script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

<span data-ttu-id="ce6b1-107">Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)e, em seguida, execute `Login-AzureRmAccount` toocreate uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="ce6b1-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ce6b1-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="ce6b1-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ce6b1-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="ce6b1-109">Clean up deployment</span></span> 

<span data-ttu-id="ce6b1-110">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="ce6b1-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ce6b1-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="ce6b1-111">Script explanation</span></span>

<span data-ttu-id="ce6b1-112">Esse script usa Olá toocreate comandos a seguir, um grupo de recursos, a rede virtual e grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="ce6b1-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="ce6b1-113">Cada comando na tabela Olá vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="ce6b1-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="ce6b1-114">Command</span><span class="sxs-lookup"><span data-stu-id="ce6b1-114">Command</span></span> | <span data-ttu-id="ce6b1-115">Observações</span><span class="sxs-lookup"><span data-stu-id="ce6b1-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ce6b1-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ce6b1-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="ce6b1-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="ce6b1-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ce6b1-118">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="ce6b1-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="ce6b1-119">Cria uma rede virtual do Azure e uma sub-rede front-end.</span><span class="sxs-lookup"><span data-stu-id="ce6b1-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="ce6b1-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ce6b1-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="ce6b1-121">Cria uma sub-rede back-end.</span><span class="sxs-lookup"><span data-stu-id="ce6b1-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="ce6b1-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="ce6b1-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="ce6b1-123">Cria um tooaccess endereço IP público Olá VM de saudação à Internet.</span><span class="sxs-lookup"><span data-stu-id="ce6b1-123">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="ce6b1-124">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="ce6b1-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="ce6b1-125">Cria as interfaces de rede virtual e os conecta sub-redes da rede virtual toohello de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="ce6b1-125">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="ce6b1-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="ce6b1-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="ce6b1-127">Cria grupos de segurança de rede (NSG) que estão associados toohello sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="ce6b1-127">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="ce6b1-128">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="ce6b1-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |<span data-ttu-id="ce6b1-129">Cria regras NSG que permitam ou bloqueiem as sub-redes de toospecific portas específicas.</span><span class="sxs-lookup"><span data-stu-id="ce6b1-129">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="ce6b1-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="ce6b1-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="ce6b1-131">Cria máquinas virtuais e anexa um tooeach NIC VM.</span><span class="sxs-lookup"><span data-stu-id="ce6b1-131">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="ce6b1-132">Esse comando também especifica Olá toouse de imagem de máquina virtual e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="ce6b1-132">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="ce6b1-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ce6b1-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="ce6b1-134">Exclui um grupo de recursos e todos os seus recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="ce6b1-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ce6b1-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ce6b1-135">Next steps</span></span>

<span data-ttu-id="ce6b1-136">Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ce6b1-136">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="ce6b1-137">Exemplos de script do PowerShell rede adicionais podem ser encontrados no hello [documentação de visão geral da rede do Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ce6b1-137">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
