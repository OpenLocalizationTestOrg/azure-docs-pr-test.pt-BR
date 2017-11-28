---
title: "Amostra de script do Azure PowerShell – Criptografar uma VM Windows | Microsoft Docs"
description: "Amostra de script do Azure PowerShell – Criptografar uma VM Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 9279fea482fcd8716bcd996985e10f500a4775ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="4de60-103">Criptografar uma máquina virtual Windows com o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4de60-103">Encrypt a Windows virtual machine with Azure PowerShell</span></span>

<span data-ttu-id="4de60-104">Esse script cria um Azure Key Vault seguro, chaves de criptografia, uma entidade de serviço do Azure Active Directory e uma VM (máquina virtual) Windows.</span><span class="sxs-lookup"><span data-stu-id="4de60-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="4de60-105">A VM é então criptografada usando a chave de criptografia do Key Vault e as credenciais da entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="4de60-105">The VM is then encrypted using the encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4de60-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="4de60-106">Sample script</span></span>

<span data-ttu-id="4de60-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Criptografar discos de VM")]</span><span class="sxs-lookup"><span data-stu-id="4de60-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Encrypt VM disks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="4de60-108">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="4de60-108">Clean up deployment</span></span> 

<span data-ttu-id="4de60-109">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="4de60-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="4de60-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="4de60-110">Script explanation</span></span>

<span data-ttu-id="4de60-111">Esse script usa os seguintes comandos para criar a implantação.</span><span class="sxs-lookup"><span data-stu-id="4de60-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="4de60-112">Cada item em que a tabela contém links para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="4de60-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4de60-113">Command</span><span class="sxs-lookup"><span data-stu-id="4de60-113">Command</span></span> | <span data-ttu-id="4de60-114">Observações</span><span class="sxs-lookup"><span data-stu-id="4de60-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4de60-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4de60-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="4de60-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="4de60-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4de60-117">New-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="4de60-117">New-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/new-azurermkeyvault) | <span data-ttu-id="4de60-118">Cria um Azure Key Vault para armazenar dados seguros, como chaves de criptografia.</span><span class="sxs-lookup"><span data-stu-id="4de60-118">Creates an Azure Key Vault to store secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="4de60-119">Add-AzureKeyVaultKey</span><span class="sxs-lookup"><span data-stu-id="4de60-119">Add-AzureKeyVaultKey</span></span>](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) | <span data-ttu-id="4de60-120">Cria uma chave de criptografia no Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4de60-120">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="4de60-121">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="4de60-121">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="4de60-122">Cria uma entidade de serviço do Azure Active Directory para autenticar com segurança e controlar o acesso às chaves de criptografia.</span><span class="sxs-lookup"><span data-stu-id="4de60-122">Creates an Azure Active Directory service principal to securely authenticate and control access to encryption keys.</span></span> |
| [<span data-ttu-id="4de60-123">Set-AzureRmKeyVaultAccessPolicy</span><span class="sxs-lookup"><span data-stu-id="4de60-123">Set-AzureRmKeyVaultAccessPolicy</span></span>](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) | <span data-ttu-id="4de60-124">Define as permissões no Key Vault para conceder à entidade de serviço o acesso às chaves de criptografia.</span><span class="sxs-lookup"><span data-stu-id="4de60-124">Sets permissions on the Key Vault to grant the service principal access to encryption keys.</span></span> |
| [<span data-ttu-id="4de60-125">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="4de60-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="4de60-126">Cria uma configuração de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="4de60-126">Creates a subnet configuration.</span></span> <span data-ttu-id="4de60-127">Essa configuração é usada com o processo de criação de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="4de60-127">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="4de60-128">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="4de60-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="4de60-129">Cria uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="4de60-129">Creates a virtual network.</span></span> |
| [<span data-ttu-id="4de60-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="4de60-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="4de60-131">Cria um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="4de60-131">Creates a public IP address.</span></span> |
| [<span data-ttu-id="4de60-132">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="4de60-132">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="4de60-133">Cria uma configuração de regra de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="4de60-133">Creates a network security group rule configuration.</span></span> <span data-ttu-id="4de60-134">Essa configuração é usada para criar uma regra NSG quando o NSG é criado.</span><span class="sxs-lookup"><span data-stu-id="4de60-134">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="4de60-135">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="4de60-135">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="4de60-136">Cria um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="4de60-136">Creates a network security group.</span></span> |
| [<span data-ttu-id="4de60-137">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="4de60-137">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="4de60-138">Obtém informações de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="4de60-138">Gets subnet information.</span></span> <span data-ttu-id="4de60-139">Essas informações são usadas ao criar um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="4de60-139">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="4de60-140">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="4de60-140">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="4de60-141">Cria um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="4de60-141">Creates a network interface.</span></span> |
| [<span data-ttu-id="4de60-142">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="4de60-142">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="4de60-143">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="4de60-143">Creates a VM configuration.</span></span> <span data-ttu-id="4de60-144">Essa configuração inclui informações como nome da VM, sistema operacional e credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="4de60-144">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="4de60-145">A configuração é usada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="4de60-145">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="4de60-146">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="4de60-146">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="4de60-147">Crie uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4de60-147">Create a virtual machine.</span></span> |
| [<span data-ttu-id="4de60-148">Get-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="4de60-148">Get-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/get-azurermkeyvault) | <span data-ttu-id="4de60-149">Obtém as informações necessárias sobre o Key Vault</span><span class="sxs-lookup"><span data-stu-id="4de60-149">Gets required information on the Key Vault</span></span> |
| [<span data-ttu-id="4de60-150">Set-AzureRmVMDiskEncryptionExtension</span><span class="sxs-lookup"><span data-stu-id="4de60-150">Set-AzureRmVMDiskEncryptionExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) | <span data-ttu-id="4de60-151">Habilita a criptografia em uma VM usando as credenciais da entidade de serviço e a chave de criptografia.</span><span class="sxs-lookup"><span data-stu-id="4de60-151">Enables encryption on a VM using the service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="4de60-152">Get-AzureRmVmDiskEncryptionStatus</span><span class="sxs-lookup"><span data-stu-id="4de60-152">Get-AzureRmVmDiskEncryptionStatus</span></span>](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) | <span data-ttu-id="4de60-153">Mostra o status do processo de criptografia da VM.</span><span class="sxs-lookup"><span data-stu-id="4de60-153">Shows the status of the VM encryption process.</span></span> |
| [<span data-ttu-id="4de60-154">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4de60-154">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="4de60-155">Remove um grupo de recursos e todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="4de60-155">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4de60-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4de60-156">Next steps</span></span>

<span data-ttu-id="4de60-157">Para obter mais informações sobre o módulo do Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4de60-157">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4de60-158">Amostras de script do PowerShell da máquina virtual adicionais podem ser encontrados na [documentação da VM Windows do Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4de60-158">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
