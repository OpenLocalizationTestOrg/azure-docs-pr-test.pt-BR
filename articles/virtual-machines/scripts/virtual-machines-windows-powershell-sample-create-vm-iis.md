---
title: "Amostra de Script do Azure PowerShell – IIS | Microsoft Docs"
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
ms.openlocfilehash: 1f2f6301267c43919efc298573b6239cacf39239
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-iis-vm-with-powershell"></a><span data-ttu-id="5e794-103">Criar uma VM IIS com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e794-103">Create an IIS VM with PowerShell</span></span>

<span data-ttu-id="5e794-104">Esse script cria uma Máquina Virtual do Azure que executa o Windows Server 2016 e, em seguida, usa a Extensão de Script Personalizado da Máquina Virtual do Azure para instalar o IIS.</span><span class="sxs-lookup"><span data-stu-id="5e794-104">This script creates an Azure Virtual Machine running Windows Server 2016, and then uses the Azure Virtual Machine Custom Script Extension to install IIS.</span></span> <span data-ttu-id="5e794-105">Após a execução do script, é possível acessar o site do IIS padrão no endereço IP público da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5e794-105">After running the script, you can access the default IIS website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5e794-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="5e794-106">Sample script</span></span>

<span data-ttu-id="5e794-107">[!code-powershell[principal](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Criar VM IIS")]</span><span class="sxs-lookup"><span data-stu-id="5e794-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5e794-108">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="5e794-108">Clean up deployment</span></span> 

<span data-ttu-id="5e794-109">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="5e794-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5e794-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="5e794-110">Script explanation</span></span>

<span data-ttu-id="5e794-111">Esse script usa os seguintes comandos para criar a implantação.</span><span class="sxs-lookup"><span data-stu-id="5e794-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="5e794-112">Cada item em que a tabela contém links para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="5e794-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5e794-113">Command</span><span class="sxs-lookup"><span data-stu-id="5e794-113">Command</span></span> | <span data-ttu-id="5e794-114">Observações</span><span class="sxs-lookup"><span data-stu-id="5e794-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5e794-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5e794-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5e794-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="5e794-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5e794-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5e794-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5e794-118">Cria uma configuração de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="5e794-118">Creates a subnet configuration.</span></span> <span data-ttu-id="5e794-119">Essa configuração é usada com o processo de criação de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="5e794-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="5e794-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="5e794-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="5e794-121">Cria uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="5e794-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="5e794-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="5e794-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="5e794-123">Cria um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="5e794-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="5e794-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="5e794-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="5e794-125">Cria uma configuração de regra de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="5e794-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="5e794-126">Essa configuração é usada para criar uma regra NSG quando o NSG é criado.</span><span class="sxs-lookup"><span data-stu-id="5e794-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="5e794-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="5e794-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="5e794-128">Cria um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="5e794-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="5e794-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5e794-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5e794-130">Obtém informações de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="5e794-130">Gets subnet information.</span></span> <span data-ttu-id="5e794-131">Essas informações são usadas ao criar um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="5e794-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="5e794-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="5e794-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="5e794-133">Cria um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="5e794-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="5e794-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="5e794-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="5e794-135">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="5e794-135">Creates a VM configuration.</span></span> <span data-ttu-id="5e794-136">Essa configuração inclui informações como nome da VM, sistema operacional e credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="5e794-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="5e794-137">A configuração é usada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="5e794-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="5e794-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5e794-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="5e794-139">Crie uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5e794-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="5e794-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="5e794-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="5e794-141">Adicione uma extensão de VM à máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5e794-141">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="5e794-142">Neste exemplo, a extensão de script personalizado é usada para instalar o IIS.</span><span class="sxs-lookup"><span data-stu-id="5e794-142">In this sample, the custom script extension is used to install IIS.</span></span> |
|[<span data-ttu-id="5e794-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5e794-143">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5e794-144">Remove um grupo de recursos e todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="5e794-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5e794-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5e794-145">Next steps</span></span>

<span data-ttu-id="5e794-146">Para obter mais informações sobre o módulo do Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5e794-146">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5e794-147">Amostras de script do PowerShell da máquina virtual adicionais podem ser encontrados na [documentação da VM Windows do Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5e794-147">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
