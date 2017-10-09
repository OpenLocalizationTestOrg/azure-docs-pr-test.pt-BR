---
title: aaaAzure exemplo de Script do PowerShell - IIS | Microsoft Docs
description: "Amostra de Script do Azure PowerShell – IIS"
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
ms.custom: mvc
ms.openlocfilehash: 707563e3cce32e667c41ab9ec2392c8f12ef116c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iis-vm-with-powershell"></a><span data-ttu-id="01cc1-103">Criar uma VM IIS com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="01cc1-103">Create an IIS VM with PowerShell</span></span>

<span data-ttu-id="01cc1-104">Esse script cria uma máquina Virtual do Azure executando o Windows Server 2016 e, em seguida, usa tooinstall de extensão de Script de personalizado de máquina Virtual do Azure Olá IIS.</span><span class="sxs-lookup"><span data-stu-id="01cc1-104">This script creates an Azure Virtual Machine running Windows Server 2016, and then uses hello Azure Virtual Machine Custom Script Extension tooinstall IIS.</span></span> <span data-ttu-id="01cc1-105">Depois de executar o script hello, você pode acessar o site do IIS padrão Olá no endereço IP público de saudação da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="01cc1-105">After running hello script, you can access hello default IIS website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="01cc1-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="01cc1-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")]

## <a name="clean-up-deployment"></a><span data-ttu-id="01cc1-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="01cc1-107">Clean up deployment</span></span> 

<span data-ttu-id="01cc1-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="01cc1-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="01cc1-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="01cc1-109">Script explanation</span></span>

<span data-ttu-id="01cc1-110">Esse script usa Olá implantação de saudação toocreate comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="01cc1-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="01cc1-111">Cada item na tabela de saudação vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="01cc1-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="01cc1-112">Command</span><span class="sxs-lookup"><span data-stu-id="01cc1-112">Command</span></span> | <span data-ttu-id="01cc1-113">Observações</span><span class="sxs-lookup"><span data-stu-id="01cc1-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="01cc1-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="01cc1-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="01cc1-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="01cc1-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="01cc1-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="01cc1-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="01cc1-117">Cria uma configuração de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="01cc1-117">Creates a subnet configuration.</span></span> <span data-ttu-id="01cc1-118">Essa configuração é usada com o processo de criação de rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="01cc1-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="01cc1-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="01cc1-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="01cc1-120">Cria uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="01cc1-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="01cc1-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="01cc1-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="01cc1-122">Cria um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="01cc1-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="01cc1-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="01cc1-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="01cc1-124">Cria uma configuração de regra de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="01cc1-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="01cc1-125">Essa configuração é usada toocreate uma regra NSG quando Olá NSG é criado.</span><span class="sxs-lookup"><span data-stu-id="01cc1-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="01cc1-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="01cc1-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="01cc1-127">Cria um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="01cc1-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="01cc1-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="01cc1-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="01cc1-129">Obtém informações de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="01cc1-129">Gets subnet information.</span></span> <span data-ttu-id="01cc1-130">Essas informações são usadas ao criar um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="01cc1-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="01cc1-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="01cc1-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="01cc1-132">Cria um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="01cc1-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="01cc1-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="01cc1-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="01cc1-134">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="01cc1-134">Creates a VM configuration.</span></span> <span data-ttu-id="01cc1-135">Essa configuração inclui informações como nome da VM, sistema operacional e credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="01cc1-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="01cc1-136">Olá configuração será usada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="01cc1-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="01cc1-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="01cc1-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="01cc1-138">Crie uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="01cc1-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="01cc1-139">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="01cc1-139">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="01cc1-140">Adicione uma máquina virtual de toohello de extensão VM.</span><span class="sxs-lookup"><span data-stu-id="01cc1-140">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="01cc1-141">Neste exemplo, extensão do script personalizado Olá é usado tooinstall IIS.</span><span class="sxs-lookup"><span data-stu-id="01cc1-141">In this sample, hello custom script extension is used tooinstall IIS.</span></span> |
|[<span data-ttu-id="01cc1-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="01cc1-142">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="01cc1-143">Remove um grupo de recursos e todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="01cc1-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="01cc1-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="01cc1-144">Next steps</span></span>

<span data-ttu-id="01cc1-145">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="01cc1-145">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="01cc1-146">Exemplos de script do PowerShell de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="01cc1-146">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
