---
title: aaaAzure exemplo de Script do PowerShell - criar uma VM do Linux | Microsoft Docs
description: "Amostra de script do Azure PowerShell – Criar uma VM Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 8ee2ee42aa68ee135a859b7eaead25811cf54095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-configured-virtual-machine-with-powershell"></a><span data-ttu-id="f1d29-103">Criar uma máquina virtual totalmente configurada com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1d29-103">Create a fully configured virtual machine with PowerShell</span></span>

<span data-ttu-id="f1d29-104">Este script cria uma Máquina Virtual do Azure com um sistema operacional Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="f1d29-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="f1d29-105">Depois de executar o script hello, você pode acessar a máquina virtual de saudação via SSH.</span><span class="sxs-lookup"><span data-stu-id="f1d29-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f1d29-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="f1d29-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.ps1 "Create VM detailed")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f1d29-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="f1d29-107">Clean up deployment</span></span> 

<span data-ttu-id="f1d29-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="f1d29-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f1d29-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="f1d29-109">Script explanation</span></span>

<span data-ttu-id="f1d29-110">Esse script usa Olá implantação de saudação toocreate comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="f1d29-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="f1d29-111">Cada item na tabela de saudação vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="f1d29-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f1d29-112">Command</span><span class="sxs-lookup"><span data-stu-id="f1d29-112">Command</span></span> | <span data-ttu-id="f1d29-113">Observações</span><span class="sxs-lookup"><span data-stu-id="f1d29-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f1d29-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f1d29-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f1d29-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="f1d29-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f1d29-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="f1d29-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="f1d29-117">Cria uma configuração de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="f1d29-117">Creates a subnet configuration.</span></span> <span data-ttu-id="f1d29-118">Essa configuração é usada com o processo de criação de rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="f1d29-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="f1d29-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="f1d29-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="f1d29-120">Cria uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="f1d29-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="f1d29-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="f1d29-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="f1d29-122">Cria um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="f1d29-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="f1d29-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="f1d29-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="f1d29-124">Cria uma configuração de regra de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="f1d29-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="f1d29-125">Essa configuração é usada toocreate uma regra NSG quando Olá NSG é criado.</span><span class="sxs-lookup"><span data-stu-id="f1d29-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="f1d29-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="f1d29-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="f1d29-127">Cria um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="f1d29-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="f1d29-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="f1d29-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="f1d29-129">Obtém informações de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="f1d29-129">Gets subnet information.</span></span> <span data-ttu-id="f1d29-130">Essas informações são usadas ao criar um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="f1d29-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="f1d29-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="f1d29-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="f1d29-132">Cria um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="f1d29-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="f1d29-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="f1d29-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="f1d29-134">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="f1d29-134">Creates a VM configuration.</span></span> <span data-ttu-id="f1d29-135">Essa configuração inclui informações como nome da VM, sistema operacional e credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="f1d29-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="f1d29-136">Olá configuração será usada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="f1d29-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="f1d29-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="f1d29-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="f1d29-138">Crie uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f1d29-138">Create a virtual machine.</span></span> |
|[<span data-ttu-id="f1d29-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f1d29-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="f1d29-140">Remove um grupo de recursos e todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="f1d29-140">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f1d29-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f1d29-141">Next steps</span></span>

<span data-ttu-id="f1d29-142">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f1d29-142">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f1d29-143">Exemplos de script do PowerShell de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f1d29-143">Additional virtual machine PowerShell script samples can be found in hello [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
