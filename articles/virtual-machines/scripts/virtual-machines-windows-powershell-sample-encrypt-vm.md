---
title: aaaAzure exemplo de Script do PowerShell - criptografar uma VM do Windows | Microsoft Docs
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
ms.openlocfilehash: 80c52a0b734a52a051ed30026b294840fd521143
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="dcd99-103">Criptografar uma máquina virtual Windows com o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcd99-103">Encrypt a Windows virtual machine with Azure PowerShell</span></span>

<span data-ttu-id="dcd99-104">Esse script cria um Azure Key Vault seguro, chaves de criptografia, uma entidade de serviço do Azure Active Directory e uma VM (máquina virtual) Windows.</span><span class="sxs-lookup"><span data-stu-id="dcd99-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="dcd99-105">Olá VM é criptografada usando a chave de criptografia de saudação do Cofre de chaves e credenciais de serviço principal.</span><span class="sxs-lookup"><span data-stu-id="dcd99-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="dcd99-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="dcd99-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="dcd99-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="dcd99-107">Clean up deployment</span></span> 

<span data-ttu-id="dcd99-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="dcd99-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="dcd99-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="dcd99-109">Script explanation</span></span>

<span data-ttu-id="dcd99-110">Esse script usa Olá implantação de saudação toocreate comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="dcd99-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="dcd99-111">Cada item na tabela de saudação vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="dcd99-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="dcd99-112">Command</span><span class="sxs-lookup"><span data-stu-id="dcd99-112">Command</span></span> | <span data-ttu-id="dcd99-113">Observações</span><span class="sxs-lookup"><span data-stu-id="dcd99-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dcd99-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="dcd99-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="dcd99-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="dcd99-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dcd99-116">New-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="dcd99-116">New-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/new-azurermkeyvault) | <span data-ttu-id="dcd99-117">Cria um cofre de chaves do Azure toostore proteger os dados, como chaves de criptografia.</span><span class="sxs-lookup"><span data-stu-id="dcd99-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="dcd99-118">Add-AzureKeyVaultKey</span><span class="sxs-lookup"><span data-stu-id="dcd99-118">Add-AzureKeyVaultKey</span></span>](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) | <span data-ttu-id="dcd99-119">Cria uma chave de criptografia no Key Vault.</span><span class="sxs-lookup"><span data-stu-id="dcd99-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="dcd99-120">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="dcd99-120">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="dcd99-121">Cria um serviço do Active Directory do Azure toosecurely principal autenticar e controlar o acesso tooencryption chaves.</span><span class="sxs-lookup"><span data-stu-id="dcd99-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="dcd99-122">Set-AzureRmKeyVaultAccessPolicy</span><span class="sxs-lookup"><span data-stu-id="dcd99-122">Set-AzureRmKeyVaultAccessPolicy</span></span>](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) | <span data-ttu-id="dcd99-123">Define permissões na Olá Cofre de chaves toogrant chaves de tooencryption Olá serviço principal de acesso.</span><span class="sxs-lookup"><span data-stu-id="dcd99-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="dcd99-124">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="dcd99-124">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="dcd99-125">Cria uma configuração de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="dcd99-125">Creates a subnet configuration.</span></span> <span data-ttu-id="dcd99-126">Essa configuração é usada com o processo de criação de rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="dcd99-126">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="dcd99-127">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="dcd99-127">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="dcd99-128">Cria uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="dcd99-128">Creates a virtual network.</span></span> |
| [<span data-ttu-id="dcd99-129">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="dcd99-129">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="dcd99-130">Cria um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="dcd99-130">Creates a public IP address.</span></span> |
| [<span data-ttu-id="dcd99-131">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="dcd99-131">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="dcd99-132">Cria uma configuração de regra de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="dcd99-132">Creates a network security group rule configuration.</span></span> <span data-ttu-id="dcd99-133">Essa configuração é usada toocreate uma regra NSG quando Olá NSG é criado.</span><span class="sxs-lookup"><span data-stu-id="dcd99-133">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="dcd99-134">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="dcd99-134">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="dcd99-135">Cria um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="dcd99-135">Creates a network security group.</span></span> |
| [<span data-ttu-id="dcd99-136">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="dcd99-136">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="dcd99-137">Obtém informações de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="dcd99-137">Gets subnet information.</span></span> <span data-ttu-id="dcd99-138">Essas informações são usadas ao criar um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="dcd99-138">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="dcd99-139">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="dcd99-139">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="dcd99-140">Cria um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="dcd99-140">Creates a network interface.</span></span> |
| [<span data-ttu-id="dcd99-141">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="dcd99-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="dcd99-142">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="dcd99-142">Creates a VM configuration.</span></span> <span data-ttu-id="dcd99-143">Essa configuração inclui informações como nome da VM, sistema operacional e credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="dcd99-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="dcd99-144">Olá configuração será usada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="dcd99-144">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="dcd99-145">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="dcd99-145">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="dcd99-146">Crie uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dcd99-146">Create a virtual machine.</span></span> |
| [<span data-ttu-id="dcd99-147">Get-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="dcd99-147">Get-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/get-azurermkeyvault) | <span data-ttu-id="dcd99-148">Obtém as informações necessárias sobre Olá Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="dcd99-148">Gets required information on hello Key Vault</span></span> |
| [<span data-ttu-id="dcd99-149">Set-AzureRmVMDiskEncryptionExtension</span><span class="sxs-lookup"><span data-stu-id="dcd99-149">Set-AzureRmVMDiskEncryptionExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) | <span data-ttu-id="dcd99-150">Habilita a criptografia em uma VM usando credenciais do serviço principal do hello e chave de criptografia.</span><span class="sxs-lookup"><span data-stu-id="dcd99-150">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="dcd99-151">Get-AzureRmVmDiskEncryptionStatus</span><span class="sxs-lookup"><span data-stu-id="dcd99-151">Get-AzureRmVmDiskEncryptionStatus</span></span>](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) | <span data-ttu-id="dcd99-152">Mostra o status de saudação do hello processo de criptografia de VM.</span><span class="sxs-lookup"><span data-stu-id="dcd99-152">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="dcd99-153">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="dcd99-153">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="dcd99-154">Remove um grupo de recursos e todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="dcd99-154">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dcd99-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dcd99-155">Next steps</span></span>

<span data-ttu-id="dcd99-156">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dcd99-156">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="dcd99-157">Exemplos de script do PowerShell de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dcd99-157">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
