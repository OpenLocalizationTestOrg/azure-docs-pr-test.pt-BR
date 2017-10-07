---
title: aaaUpload um tooAzure VHD generalizado exemplo de Script do PowerShell | Microsoft Docs
description: "PowerShell tooupload script um tooAzure VHD generalizada de exemplo e criar uma nova VM usando o modelo de implantação do Gerenciador de recursos de hello e discos gerenciados."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/18/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 72b4ff09eb7a6ba1604b9d5cbac51e60eded7545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-script-tooupload-a-vhd-tooazure-and-create-a-new-vm"></a><span data-ttu-id="a3fcf-103">Exemplo de script tooupload tooAzure um VHD e criar uma nova VM</span><span class="sxs-lookup"><span data-stu-id="a3fcf-103">Sample script tooupload a VHD tooAzure and create a new VM</span></span>

<span data-ttu-id="a3fcf-104">Esse script usa um arquivo. vhd local de uma VM generalizada e carrega-tooAzure, cria uma imagem de disco gerenciado e usa Olá toocreate uma nova VM.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-104">This script takes a local .vhd file from a generalized VM and uploads it tooAzure, creates a Managed Disk image and uses hello toocreate a new VM.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a3fcf-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="a3fcf-105">Sample script</span></span>

```powershell
# Provide values for hello variables
$resourceGroup = 'myResourceGroup'
$location = 'EastUS'
$storageaccount = 'mystorageaccount'
$storageType = 'Standard_LRS'
$containername = 'mycontainer'
$localPath = 'C:\Users\Public\Documents\Hyper-V\VHDs\generalized.vhd'
$vmName = 'myVM'
$imageName = 'myImage'
$vhdName = 'myUploadedVhd.vhd'
$diskSizeGB = '128'
$subnetName = 'mySubnet'
$vnetName = 'myVnet'
$ipName = 'myPip'
$nicName = 'myNic'
$nsgName = 'myNsg'
$ruleName = 'myRdpRule'
$vmName = 'myVM'
$computerName = 'myComputerName'
$vmSize = 'Standard_DS1_v2'

# Get hello username and password toobe used for hello administrators account on hello VM. 
# This is used when connecting toohello VM using RDP.

$cred = Get-Credential

# Upload hello VHD
New-AzureRmResourceGroup -Name $resourceGroup -Location $location
New-AzureRmStorageAccount -ResourceGroupName $resourceGroup -Name $storageAccount -Location $location `
    -SkuName $storageType -Kind "Storage"
$urlOfUploadedImageVhd = ('https://' + $storageaccount + '.blob.core.windows.net/' + $containername + '/' + $vhdName)
Add-AzureRmVhd -ResourceGroupName $resourceGroup -Destination $urlOfUploadedImageVhd `
    -LocalFilePath $localPath

# Note: Uploading hello VHD may take awhile!

# Create a managed image from hello uploaded VHD 
$imageConfig = New-AzureRmImageConfig -Location $location
$imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized `
    -BlobUri $urlOfUploadedImageVhd
$image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $resourceGroup -Image $imageConfig
 
# Create hello networking resources
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $resourceGroup -Location $location `
    -AllocationMethod Dynamic
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroup -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description 'Allow RDP' -Access Allow `
    -Protocol Tcp -Direction Inbound -Priority 110 -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $resourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $resourceGroup -Name $vnetName

# Start building hello VM configuration
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

# Set hello VM image as source image for hello new VM
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id

# Finish hello VM configuration and add hello NIC.
$vm = Set-AzureRmVMOSDisk -VM $vm  -DiskSizeInGB $diskSizeGB -CreateOption FromImage -Caching ReadWrite
$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

# Create hello VM
New-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup -Location $location

# Verify that hello VM was created
$vmList = Get-AzureRmVM -ResourceGroupName $resourceGroup
$vmList.Name


```


<!-- 
[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")] -->

## <a name="clean-up-deployment"></a><span data-ttu-id="a3fcf-106">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="a3fcf-106">Clean up deployment</span></span> 

<span data-ttu-id="a3fcf-107">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="a3fcf-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="a3fcf-108">Script explanation</span></span>

<span data-ttu-id="a3fcf-109">Esse script usa Olá implantação de saudação toocreate comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-109">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="a3fcf-110">Cada item na tabela de saudação vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a3fcf-111">Command</span><span class="sxs-lookup"><span data-stu-id="a3fcf-111">Command</span></span>                                                                                                             | <span data-ttu-id="a3fcf-112">Observações</span><span class="sxs-lookup"><span data-stu-id="a3fcf-112">Notes</span></span>                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="a3fcf-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a3fcf-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)                           | <span data-ttu-id="a3fcf-114">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-114">Creates a resource group in which all resources are stored.</span></span>                                                                                                                          |
| [<span data-ttu-id="a3fcf-115">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="a3fcf-115">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.resources/new-azurermstorageaccount)                         | <span data-ttu-id="a3fcf-116">Cria uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-116">Creates a storage account.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="a3fcf-117">Add-AzureRmVhd</span><span class="sxs-lookup"><span data-stu-id="a3fcf-117">Add-AzureRmVhd</span></span>](/powershell/module/azurerm.resources/add-azurermvhd)                                               | <span data-ttu-id="a3fcf-118">Carrega um disco rígido virtual de um blob de tooa de máquina virtual local em uma conta de armazenamento de nuvem no Azure.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-118">Uploads a virtual hard disk from an on-premises virtual machine tooa blob in a cloud storage account in Azure.</span></span>                                                                       |
| [<span data-ttu-id="a3fcf-119">New-AzureRmImageConfig</span><span class="sxs-lookup"><span data-stu-id="a3fcf-119">New-AzureRmImageConfig</span></span>](/powershell/module/azurerm.resources/new-azurermimageconfig)                               | <span data-ttu-id="a3fcf-120">Cria um objeto de imagem configurável.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-120">Creates a configurable image object.</span></span>                                                                                                                                                 |
| [<span data-ttu-id="a3fcf-121">Set-AzureRmImageOsDisk</span><span class="sxs-lookup"><span data-stu-id="a3fcf-121">Set-AzureRmImageOsDisk</span></span>](/powershell/module/azurerm.resources/set-azurermimageosdisk)                               | <span data-ttu-id="a3fcf-122">Define propriedades de disco de sistema operacional de saudação em um objeto de imagem.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-122">Sets hello operating system disk properties on an image object.</span></span>                                                                                                                        |
| [<span data-ttu-id="a3fcf-123">New-AzureRmImage</span><span class="sxs-lookup"><span data-stu-id="a3fcf-123">New-AzureRmImage</span></span>](/powershell/module/azurerm.resources/new-azurermimage)                                           | <span data-ttu-id="a3fcf-124">Cria uma nova imagem.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-124">Creates a new image.</span></span>                                                                                                                                                                 |
| [<span data-ttu-id="a3fcf-125">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="a3fcf-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="a3fcf-126">Cria uma configuração de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-126">Creates a subnet configuration.</span></span> <span data-ttu-id="a3fcf-127">Essa configuração é usada com o processo de criação de rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-127">This configuration is used with hello virtual network creation process.</span></span>                                                                                |
| [<span data-ttu-id="a3fcf-128">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="a3fcf-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetwork)                         | <span data-ttu-id="a3fcf-129">Cria uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-129">Creates a virtual network.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="a3fcf-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="a3fcf-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.resources/new-azurermpublicipaddress)                       | <span data-ttu-id="a3fcf-131">Cria um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-131">Creates a public IP address.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="a3fcf-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="a3fcf-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.resources/new-azurermnetworkinterface)                     | <span data-ttu-id="a3fcf-133">Cria um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-133">Creates a network interface.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="a3fcf-134">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="a3fcf-134">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecurityruleconfig)   | <span data-ttu-id="a3fcf-135">Cria uma configuração de regra de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-135">Creates a network security group rule configuration.</span></span> <span data-ttu-id="a3fcf-136">Essa configuração é usada toocreate uma regra NSG quando Olá NSG é criado.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-136">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span>                                                       |
| [<span data-ttu-id="a3fcf-137">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="a3fcf-137">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecuritygroup)             | <span data-ttu-id="a3fcf-138">Cria um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-138">Creates a network security group.</span></span>                                                                                                                                                    |
| [<span data-ttu-id="a3fcf-139">Get-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="a3fcf-139">Get-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/get-azurermvirtualnetwork)                         | <span data-ttu-id="a3fcf-140">Obtém uma rede virtual em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-140">Gets a virtual network in a resource group.</span></span>                                                                                                                                          |
| [<span data-ttu-id="a3fcf-141">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="a3fcf-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvmconfig)                                     | <span data-ttu-id="a3fcf-142">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-142">Creates a VM configuration.</span></span> <span data-ttu-id="a3fcf-143">Essa configuração inclui informações como nome da VM, sistema operacional e credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="a3fcf-144">Olá configuração será usada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-144">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="a3fcf-145">Set-AzureRmVMSourceImage</span><span class="sxs-lookup"><span data-stu-id="a3fcf-145">Set-AzureRmVMSourceImage</span></span>](/powershell/module/azurerm.resources/set-azurermvmsourceimage)                           | <span data-ttu-id="a3fcf-146">Especifica uma imagem para uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-146">Specifies an image for a virtual machine.</span></span>                                                                                                                                            |
| [<span data-ttu-id="a3fcf-147">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="a3fcf-147">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.resources/set-azurermvmosdisk)                                     | <span data-ttu-id="a3fcf-148">Define as propriedades do disco do sistema de operacional de Olá em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-148">Sets hello operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="a3fcf-149">Set-AzureRmVMOperatingSystem</span><span class="sxs-lookup"><span data-stu-id="a3fcf-149">Set-AzureRmVMOperatingSystem</span></span>](/powershell/module/azurerm.resources/set-azurermvmoperatingsystem)                   | <span data-ttu-id="a3fcf-150">Define as propriedades do disco do sistema de operacional de Olá em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-150">Sets hello operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="a3fcf-151">Add-AzureRmVMNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="a3fcf-151">Add-AzureRmVMNetworkInterface</span></span>](/powershell/module/azurerm.resources/add-azurermvmnetworkinterface)                 | <span data-ttu-id="a3fcf-152">Adiciona uma máquina virtual de tooa de interface de rede.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-152">Adds a network interface tooa virtual machine.</span></span>                                                                                                                                       |
| [<span data-ttu-id="a3fcf-153">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="a3fcf-153">New-AzureRmVM</span></span>](/powershell/module/azurerm.resources/new-azurermvm)                                                 | <span data-ttu-id="a3fcf-154">Crie uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-154">Create a virtual machine.</span></span>                                                                                                                                                            |
| [<span data-ttu-id="a3fcf-155">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a3fcf-155">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)                     | <span data-ttu-id="a3fcf-156">Remove um grupo de recursos e todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="a3fcf-156">Removes a resource group and all resources contained within.</span></span>                                                                                                                         |

## <a name="next-steps"></a><span data-ttu-id="a3fcf-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a3fcf-157">Next steps</span></span>

<span data-ttu-id="a3fcf-158">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a3fcf-158">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a3fcf-159">Exemplos de script do PowerShell de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a3fcf-159">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
