---
title: Upload de um VHD generalizado para Script de Exemplo do Azure PowerShell | Microsoft Docs
description: "Script de exemplo do PowerShell para carregar um VHD generalizado para o Azure e criar uma nova VM utilizando o modelo de implantação do gerenciador de recursos e Managed Disks."
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
ms.openlocfilehash: cd3d87bb4384971e28d3330cd5c1a3d351129036
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="sample-script-to-upload-a-vhd-to-azure-and-create-a-new-vm"></a><span data-ttu-id="e1298-103">Script de exemplo para carregar um VHD para o Azure e criar uma nova VM</span><span class="sxs-lookup"><span data-stu-id="e1298-103">Sample script to upload a VHD to Azure and create a new VM</span></span>

<span data-ttu-id="e1298-104">Esse script leva um arquivo .vhd local de uma VM generalizada e carrega-o para o Azure, cria uma imagem de Managed Disk e utiliza para criar uma nova VM.</span><span class="sxs-lookup"><span data-stu-id="e1298-104">This script takes a local .vhd file from a generalized VM and uploads it to Azure, creates a Managed Disk image and uses the to create a new VM.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e1298-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="e1298-105">Sample script</span></span>

```powershell
# Provide values for the variables
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

# Get the username and password to be used for the administrators account on the VM. 
# This is used when connecting to the VM using RDP.

$cred = Get-Credential

# Upload the VHD
New-AzureRmResourceGroup -Name $resourceGroup -Location $location
New-AzureRmStorageAccount -ResourceGroupName $resourceGroup -Name $storageAccount -Location $location `
    -SkuName $storageType -Kind "Storage"
$urlOfUploadedImageVhd = ('https://' + $storageaccount + '.blob.core.windows.net/' + $containername + '/' + $vhdName)
Add-AzureRmVhd -ResourceGroupName $resourceGroup -Destination $urlOfUploadedImageVhd `
    -LocalFilePath $localPath

# Note: Uploading the VHD may take awhile!

# Create a managed image from the uploaded VHD 
$imageConfig = New-AzureRmImageConfig -Location $location
$imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized `
    -BlobUri $urlOfUploadedImageVhd
$image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $resourceGroup -Image $imageConfig
 
# Create the networking resources
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

# Start building the VM configuration
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

# Set the VM image as source image for the new VM
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id

# Finish the VM configuration and add the NIC.
$vm = Set-AzureRmVMOSDisk -VM $vm  -DiskSizeInGB $diskSizeGB -CreateOption FromImage -Caching ReadWrite
$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

# Create the VM
New-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup -Location $location

# Verify that the VM was created
$vmList = Get-AzureRmVM -ResourceGroupName $resourceGroup
$vmList.Name


```


<!-- 
[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")] -->

## <a name="clean-up-deployment"></a><span data-ttu-id="e1298-106">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="e1298-106">Clean up deployment</span></span> 

<span data-ttu-id="e1298-107">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="e1298-107">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e1298-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="e1298-108">Script explanation</span></span>

<span data-ttu-id="e1298-109">Esse script usa os seguintes comandos para criar a implantação.</span><span class="sxs-lookup"><span data-stu-id="e1298-109">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="e1298-110">Cada item em que a tabela contém links para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="e1298-110">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e1298-111">Command</span><span class="sxs-lookup"><span data-stu-id="e1298-111">Command</span></span>                                                                                                             | <span data-ttu-id="e1298-112">Observações</span><span class="sxs-lookup"><span data-stu-id="e1298-112">Notes</span></span>                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="e1298-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e1298-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)                           | <span data-ttu-id="e1298-114">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="e1298-114">Creates a resource group in which all resources are stored.</span></span>                                                                                                                          |
| [<span data-ttu-id="e1298-115">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="e1298-115">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.resources/new-azurermstorageaccount)                         | <span data-ttu-id="e1298-116">Cria uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e1298-116">Creates a storage account.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="e1298-117">Add-AzureRmVhd</span><span class="sxs-lookup"><span data-stu-id="e1298-117">Add-AzureRmVhd</span></span>](/powershell/module/azurerm.resources/add-azurermvhd)                                               | <span data-ttu-id="e1298-118">Carrega um disco rígido virtual de uma máquina virtual no local para um blob em uma conta de armazenamento em nuvem no Azure.</span><span class="sxs-lookup"><span data-stu-id="e1298-118">Uploads a virtual hard disk from an on-premises virtual machine to a blob in a cloud storage account in Azure.</span></span>                                                                       |
| [<span data-ttu-id="e1298-119">New-AzureRmImageConfig</span><span class="sxs-lookup"><span data-stu-id="e1298-119">New-AzureRmImageConfig</span></span>](/powershell/module/azurerm.resources/new-azurermimageconfig)                               | <span data-ttu-id="e1298-120">Cria um objeto de imagem configurável.</span><span class="sxs-lookup"><span data-stu-id="e1298-120">Creates a configurable image object.</span></span>                                                                                                                                                 |
| [<span data-ttu-id="e1298-121">Set-AzureRmImageOsDisk</span><span class="sxs-lookup"><span data-stu-id="e1298-121">Set-AzureRmImageOsDisk</span></span>](/powershell/module/azurerm.resources/set-azurermimageosdisk)                               | <span data-ttu-id="e1298-122">Define as propriedades do disco do sistema operacional em um objeto de imagem.</span><span class="sxs-lookup"><span data-stu-id="e1298-122">Sets the operating system disk properties on an image object.</span></span>                                                                                                                        |
| [<span data-ttu-id="e1298-123">New-AzureRmImage</span><span class="sxs-lookup"><span data-stu-id="e1298-123">New-AzureRmImage</span></span>](/powershell/module/azurerm.resources/new-azurermimage)                                           | <span data-ttu-id="e1298-124">Cria uma nova imagem.</span><span class="sxs-lookup"><span data-stu-id="e1298-124">Creates a new image.</span></span>                                                                                                                                                                 |
| [<span data-ttu-id="e1298-125">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="e1298-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="e1298-126">Cria uma configuração de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="e1298-126">Creates a subnet configuration.</span></span> <span data-ttu-id="e1298-127">Essa configuração é usada com o processo de criação de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="e1298-127">This configuration is used with the virtual network creation process.</span></span>                                                                                |
| [<span data-ttu-id="e1298-128">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="e1298-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetwork)                         | <span data-ttu-id="e1298-129">Cria uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="e1298-129">Creates a virtual network.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="e1298-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="e1298-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.resources/new-azurermpublicipaddress)                       | <span data-ttu-id="e1298-131">Cria um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="e1298-131">Creates a public IP address.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="e1298-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="e1298-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.resources/new-azurermnetworkinterface)                     | <span data-ttu-id="e1298-133">Cria um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="e1298-133">Creates a network interface.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="e1298-134">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="e1298-134">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecurityruleconfig)   | <span data-ttu-id="e1298-135">Cria uma configuração de regra de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="e1298-135">Creates a network security group rule configuration.</span></span> <span data-ttu-id="e1298-136">Essa configuração é usada para criar uma regra NSG quando o NSG é criado.</span><span class="sxs-lookup"><span data-stu-id="e1298-136">This configuration is used to create an NSG rule when the NSG is created.</span></span>                                                       |
| [<span data-ttu-id="e1298-137">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="e1298-137">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecuritygroup)             | <span data-ttu-id="e1298-138">Cria um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="e1298-138">Creates a network security group.</span></span>                                                                                                                                                    |
| [<span data-ttu-id="e1298-139">Get-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="e1298-139">Get-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/get-azurermvirtualnetwork)                         | <span data-ttu-id="e1298-140">Obtém uma rede virtual em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e1298-140">Gets a virtual network in a resource group.</span></span>                                                                                                                                          |
| [<span data-ttu-id="e1298-141">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="e1298-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvmconfig)                                     | <span data-ttu-id="e1298-142">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="e1298-142">Creates a VM configuration.</span></span> <span data-ttu-id="e1298-143">Essa configuração inclui informações como nome da VM, sistema operacional e credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="e1298-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="e1298-144">A configuração é usada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="e1298-144">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="e1298-145">Set-AzureRmVMSourceImage</span><span class="sxs-lookup"><span data-stu-id="e1298-145">Set-AzureRmVMSourceImage</span></span>](/powershell/module/azurerm.resources/set-azurermvmsourceimage)                           | <span data-ttu-id="e1298-146">Especifica uma imagem para uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e1298-146">Specifies an image for a virtual machine.</span></span>                                                                                                                                            |
| [<span data-ttu-id="e1298-147">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="e1298-147">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.resources/set-azurermvmosdisk)                                     | <span data-ttu-id="e1298-148">Define as propriedades do disco do sistema operacional em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e1298-148">Sets the operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="e1298-149">Set-AzureRmVMOperatingSystem</span><span class="sxs-lookup"><span data-stu-id="e1298-149">Set-AzureRmVMOperatingSystem</span></span>](/powershell/module/azurerm.resources/set-azurermvmoperatingsystem)                   | <span data-ttu-id="e1298-150">Define as propriedades do disco do sistema operacional em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e1298-150">Sets the operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="e1298-151">Add-AzureRmVMNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="e1298-151">Add-AzureRmVMNetworkInterface</span></span>](/powershell/module/azurerm.resources/add-azurermvmnetworkinterface)                 | <span data-ttu-id="e1298-152">Adiciona uma interface de rede a uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e1298-152">Adds a network interface to a virtual machine.</span></span>                                                                                                                                       |
| [<span data-ttu-id="e1298-153">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="e1298-153">New-AzureRmVM</span></span>](/powershell/module/azurerm.resources/new-azurermvm)                                                 | <span data-ttu-id="e1298-154">Crie uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e1298-154">Create a virtual machine.</span></span>                                                                                                                                                            |
| [<span data-ttu-id="e1298-155">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e1298-155">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)                     | <span data-ttu-id="e1298-156">Remove um grupo de recursos e todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="e1298-156">Removes a resource group and all resources contained within.</span></span>                                                                                                                         |

## <a name="next-steps"></a><span data-ttu-id="e1298-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e1298-157">Next steps</span></span>

<span data-ttu-id="e1298-158">Para obter mais informações sobre o módulo do Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e1298-158">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e1298-159">Amostras de script do PowerShell da máquina virtual adicionais podem ser encontrados na [documentação da VM Windows do Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e1298-159">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
