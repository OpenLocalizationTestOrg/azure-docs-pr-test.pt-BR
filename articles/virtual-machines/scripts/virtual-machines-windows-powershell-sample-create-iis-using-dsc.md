---
title: aaaAzure exemplo de Script do PowerShell - IIS com DSC | Microsoft Docs
description: "Amostra de script do Azure PowerShell – IIS com DSC"
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
ms.date: 03/01/2017
ms.author: nepeters
ms.openlocfilehash: ef855bf92ef7b0fd07466527bc5f71f688e150fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iis-vm-with-powershell"></a><span data-ttu-id="ac907-103">Criar uma VM IIS com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac907-103">Create an IIS VM with PowerShell</span></span>

<span data-ttu-id="ac907-104">Esse script cria uma máquina Virtual do Azure executando o Windows Server 2016 e, em seguida, usa tooinstall de extensão de DSC de máquina Virtual do Azure Olá IIS.</span><span class="sxs-lookup"><span data-stu-id="ac907-104">This script creates an Azure Virtual Machine running Windows Server 2016, and then uses hello Azure Virtual Machine DSC Extension tooinstall IIS.</span></span> <span data-ttu-id="ac907-105">Depois de executar o script hello, você pode acessar o site do IIS padrão Olá no endereço IP público de saudação da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac907-105">After running hello script, you can access hello default IIS website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ac907-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="ac907-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-dsc/create-windows-vm-iis-dsc.ps1 "Create VM IIS DSC")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ac907-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="ac907-107">Clean up deployment</span></span> 

<span data-ttu-id="ac907-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="ac907-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ac907-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="ac907-109">Script explanation</span></span>

<span data-ttu-id="ac907-110">Esse script usa Olá implantação de saudação toocreate comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="ac907-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="ac907-111">Cada item na tabela de saudação vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="ac907-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ac907-112">Command</span><span class="sxs-lookup"><span data-stu-id="ac907-112">Command</span></span> | <span data-ttu-id="ac907-113">Observações</span><span class="sxs-lookup"><span data-stu-id="ac907-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ac907-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ac907-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="ac907-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="ac907-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ac907-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ac907-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="ac907-117">Cria uma configuração de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="ac907-117">Creates a subnet configuration.</span></span> <span data-ttu-id="ac907-118">Essa configuração é usada com o processo de criação de rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="ac907-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="ac907-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="ac907-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="ac907-120">Cria uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="ac907-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="ac907-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="ac907-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="ac907-122">Cria um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="ac907-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="ac907-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="ac907-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="ac907-124">Cria uma configuração de regra de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="ac907-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="ac907-125">Essa configuração é usada toocreate uma regra NSG quando Olá NSG é criado.</span><span class="sxs-lookup"><span data-stu-id="ac907-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="ac907-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="ac907-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="ac907-127">Cria um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="ac907-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="ac907-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ac907-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="ac907-129">Obtém informações de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="ac907-129">Gets subnet information.</span></span> <span data-ttu-id="ac907-130">Essas informações são usadas ao criar um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="ac907-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="ac907-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="ac907-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="ac907-132">Cria um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="ac907-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="ac907-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="ac907-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="ac907-134">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="ac907-134">Creates a VM configuration.</span></span> <span data-ttu-id="ac907-135">Essa configuração inclui informações como nome da VM, sistema operacional e credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="ac907-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="ac907-136">Olá configuração será usada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="ac907-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="ac907-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="ac907-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="ac907-138">Crie uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ac907-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="ac907-139">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="ac907-139">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="ac907-140">Adicione uma máquina virtual de toohello de extensão VM.</span><span class="sxs-lookup"><span data-stu-id="ac907-140">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="ac907-141">Neste exemplo, extensão do script personalizado Olá é usado tooinstall IIS.</span><span class="sxs-lookup"><span data-stu-id="ac907-141">In this sample, hello custom script extension is used tooinstall IIS.</span></span> |
|[<span data-ttu-id="ac907-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ac907-142">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="ac907-143">Remove um grupo de recursos e todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="ac907-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ac907-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ac907-144">Next steps</span></span>

<span data-ttu-id="ac907-145">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ac907-145">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ac907-146">Exemplos de script do PowerShell de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ac907-146">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
