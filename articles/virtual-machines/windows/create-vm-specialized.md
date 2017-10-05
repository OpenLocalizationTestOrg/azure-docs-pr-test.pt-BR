---
title: Criar uma VM do Windows de um VHD especializado no Azure | Microsoft Docs
description: "Crie uma nova VM do Windows anexando um disco gerenciado especializado ao disco do sistema operacional no modelo de implantação do Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: fa952286a9ceca8b3b2c7efe2cc4867a2728c477
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a><span data-ttu-id="23fce-103">Criar uma VM do Windos a partir de um disco especializado</span><span class="sxs-lookup"><span data-stu-id="23fce-103">Create a Windows VM from a specialized disk</span></span>

<span data-ttu-id="23fce-104">Crie uma nova VM anexando um disco gerenciado especializado como o disco do sistema operacional usando o Powershell.</span><span class="sxs-lookup"><span data-stu-id="23fce-104">Create a new VM by attaching a specialized managed disk as the OS disk using Powershell.</span></span> <span data-ttu-id="23fce-105">Um disco especializado é uma cópia do disco rígido virtual (VHD) de uma VM existente que mantém as contas de usuário, aplicativos e outros dados de estado de sua VM original.</span><span class="sxs-lookup"><span data-stu-id="23fce-105">A specialized disk is a copy of virtual hard disk (VHD) from an existing VM that maintains the user accounts, applications, and other state data from your original VM.</span></span> 

<span data-ttu-id="23fce-106">Quando você usar um VHD especializado para criar uma nova VM, a nova VM retém o nome do computador da VM original.</span><span class="sxs-lookup"><span data-stu-id="23fce-106">When you use a specialized VHD to create a new VM, the new VM retains the computer name of the original VM.</span></span> <span data-ttu-id="23fce-107">Outras informações específicas do computador também são mantidas e, em alguns casos, essas informações duplicadas podem causar problemas.</span><span class="sxs-lookup"><span data-stu-id="23fce-107">Other computer-specific information is also be kept and, in some cases, this duplicate information could cause issues.</span></span> <span data-ttu-id="23fce-108">Lembre-se de que tipos de informações específicas do computador seus aplicativos dependem ao copiar uma VM.</span><span class="sxs-lookup"><span data-stu-id="23fce-108">Be aware of what types of computer-specific information your applications rely on when copying a VM.</span></span>

<span data-ttu-id="23fce-109">Você tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="23fce-109">You have two options:</span></span>
* [<span data-ttu-id="23fce-110">Carregar um VHD</span><span class="sxs-lookup"><span data-stu-id="23fce-110">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="23fce-111">Copiar uma VM existente do Azure</span><span class="sxs-lookup"><span data-stu-id="23fce-111">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

<span data-ttu-id="23fce-112">Este tópico mostra como usar discos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="23fce-112">This topic shows you how to use managed disks.</span></span> <span data-ttu-id="23fce-113">Se você tiver uma implantação herdada que requer o uso de uma conta de armazenamento, consulte [Criar uma VM em um VHD especializado em uma conta de armazenamento](sa-create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="23fce-113">If you have a legacy deployment that requires using a storage account, see [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="23fce-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="23fce-114">Before you begin</span></span>
<span data-ttu-id="23fce-115">Caso use o PowerShell, verifique se você tem a versão mais recente do módulo AzureRM.Compute do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23fce-115">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="23fce-116">Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="23fce-116">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="23fce-117">Opção 1: Carregar um VHD especializado</span><span class="sxs-lookup"><span data-stu-id="23fce-117">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="23fce-118">Você pode carregar o VHD de uma VM especializada criado com uma ferramenta de virtualização local, como o Hyper-V, ou em uma VM exportada de outra nuvem.</span><span class="sxs-lookup"><span data-stu-id="23fce-118">You can upload the VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-the-vm"></a><span data-ttu-id="23fce-119">Preparar a VM</span><span class="sxs-lookup"><span data-stu-id="23fce-119">Prepare the VM</span></span>
<span data-ttu-id="23fce-120">Se você pretende usar o VHD no estado em que se encontra para criar uma nova VM, certifique-se de que as seguintes etapas sejam concluídas.</span><span class="sxs-lookup"><span data-stu-id="23fce-120">If you intend to use the VHD as-is to create a new VM, ensure the following steps are completed.</span></span> 
  
  * <span data-ttu-id="23fce-121">[Preparar um VHD do Windows para carregar no Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="23fce-121">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="23fce-122">**Não** generalizar a VM usando o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="23fce-122">**Do not** generalize the VM using Sysprep.</span></span>
  * <span data-ttu-id="23fce-123">Remover quaisquer ferramentas e agentes de virtualização de convidado que estejam instalados na VM (ou seja, ferramentas do VMware).</span><span class="sxs-lookup"><span data-stu-id="23fce-123">Remove any guest virtualization tools and agents that are installed on the VM (like VMware tools).</span></span>
  * <span data-ttu-id="23fce-124">Verifique se a VM está configurada para obter o endereço IP e as configurações de DNS por meio de DHCP.</span><span class="sxs-lookup"><span data-stu-id="23fce-124">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="23fce-125">Isso garante que o servidor obtém um endereço IP na VNet quando ele é iniciado.</span><span class="sxs-lookup"><span data-stu-id="23fce-125">This ensures that the server obtains an IP address within the VNet when it starts up.</span></span> 


### <a name="get-the-storage-account"></a><span data-ttu-id="23fce-126">Obter a conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="23fce-126">Get the storage account</span></span>
<span data-ttu-id="23fce-127">Você precisa de uma conta de armazenamento no Azure para armazenar o VHD carregado.</span><span class="sxs-lookup"><span data-stu-id="23fce-127">You need a storage account in Azure to store the uploaded VHD.</span></span> <span data-ttu-id="23fce-128">Você pode usar uma conta de armazenamento existente ou criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="23fce-128">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="23fce-129">Para exibir as contas de armazenamento disponíveis, digite:</span><span class="sxs-lookup"><span data-stu-id="23fce-129">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="23fce-130">Se você quiser usar uma conta de armazenamento existente, vá para a seção [Carregar o VHD](#upload-the-vhd-to-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="23fce-130">If you want to use an existing storage account, proceed to the [Upload the VHD](#upload-the-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="23fce-131">Se você precisa criar uma conta de armazenamento, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="23fce-131">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="23fce-132">Você precisa do nome do grupo de recursos no qual a conta de armazenamento deve ser criada.</span><span class="sxs-lookup"><span data-stu-id="23fce-132">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="23fce-133">Para saber quais são todos os grupos de recursos que estão em sua assinatura, digite:</span><span class="sxs-lookup"><span data-stu-id="23fce-133">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="23fce-134">Para criar um grupo de recursos denominado *myResourceGroup* na região *Oeste dos EUA*, digite:</span><span class="sxs-lookup"><span data-stu-id="23fce-134">To create a resource group named *myResourceGroup* in the *West US* region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="23fce-135">Crie uma conta de armazenamento com o nome *mystorageaccount* neste grupo de recursos usando o cmdlet [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount):</span><span class="sxs-lookup"><span data-stu-id="23fce-135">Create a storage account named *mystorageaccount* in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="23fce-136">Carregar o VHD na sua conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="23fce-136">Upload the VHD to your storage account</span></span> 
<span data-ttu-id="23fce-137">Use o cmdlet [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) para carregar o VHD em um contêiner na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="23fce-137">Use the [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet to upload the VHD to a container in your storage account.</span></span> <span data-ttu-id="23fce-138">Este exemplo carrega o arquivo *myVHD.vhd* de `"C:\Users\Public\Documents\Virtual hard disks\"` em uma conta de armazenamento denominada *mystorageaccount* no grupo de recursos *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="23fce-138">This example uploads the file *myVHD.vhd* from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named *mystorageaccount* in the *myResourceGroup* resource group.</span></span> <span data-ttu-id="23fce-139">O arquivo será armazenado em um contêiner chamado *mycontainer* e o novo nome do arquivo será *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="23fce-139">The file is stored in the container named *mycontainer* and the new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="23fce-140">Se o comando tiver êxito, você receberá uma resposta semelhante a esta:</span><span class="sxs-lookup"><span data-stu-id="23fce-140">If successful, you get a response that looks similar to this:</span></span>

```powershell
MD5 hash is being calculated for the file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for the operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="23fce-141">Dependendo da conexão de rede e do tamanho do arquivo VHD, esse comando pode demorar um pouco para ser concluído</span><span class="sxs-lookup"><span data-stu-id="23fce-141">Depending on your network connection and the size of your VHD file, this command may take a while to complete</span></span>

### <a name="create-a-managed-disk-from-the-vhd"></a><span data-ttu-id="23fce-142">Criar um disco gerenciado do VHD</span><span class="sxs-lookup"><span data-stu-id="23fce-142">Create a managed disk from the VHD</span></span>

<span data-ttu-id="23fce-143">Crie um disco gerenciado do VHD especializado na sua conta de armazenamento usando [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="23fce-143">Create a managed disk from the specialized VHD in your storage account using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="23fce-144">Este exemplo usa **myOSDisk1** para o nome do disco, coloca o disco no armazenamento *StandardLRS* e usa *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* como o URI para o VHD de origem.</span><span class="sxs-lookup"><span data-stu-id="23fce-144">This example uses **myOSDisk1** for the disk name, puts the disk in *StandardLRS* storage, and uses *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* as the URI for the source VHD.</span></span>

<span data-ttu-id="23fce-145">Criar um novo grupo de recursos para a nova VM.</span><span class="sxs-lookup"><span data-stu-id="23fce-145">Create a new resource group for the new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="23fce-146">Crie o novo disco de sistema operacional no VHD carregado.</span><span class="sxs-lookup"><span data-stu-id="23fce-146">Create the new OS disk from the uploaded VHD.</span></span> 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a><span data-ttu-id="23fce-147">Opção 2: Copiar uma VM existente do Azure</span><span class="sxs-lookup"><span data-stu-id="23fce-147">Option 2: Copy an existing Azure VM</span></span>

<span data-ttu-id="23fce-148">Você pode criar uma cópia de uma VM que usa discos gerenciado por tirar um instantâneo da VM, em seguida, usando esse instantâneo para criar um novo gerenciado em disco e uma nova VM.</span><span class="sxs-lookup"><span data-stu-id="23fce-148">You can create a copy of a VM that uses managed disks by taking a snapshot of the VM, then using that snapshot to create a new managed disk and a new VM.</span></span>


### <a name="take-a-snapshot-of-the-os-disk"></a><span data-ttu-id="23fce-149">Tirar um instantâneo do disco do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="23fce-149">Take a snapshot of the OS disk</span></span>

<span data-ttu-id="23fce-150">Você pode tirar um instantâneo de toda a VM (incluindo todos os discos) ou apenas um único disco.</span><span class="sxs-lookup"><span data-stu-id="23fce-150">You can take a snapshot of and entire VM (including all disks) or of just a single disk.</span></span> <span data-ttu-id="23fce-151">As etapas a seguir mostram como criar um instantâneo apenas do disco do sistema operacional de sua VM usando o cmdlet [AzureRmSnapshot novo](/powershell/module/azurerm.compute/new-azurermsnapshot).</span><span class="sxs-lookup"><span data-stu-id="23fce-151">The following steps show you how to take a snapshot of just the OS disk of your VM using the [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span></span> 

<span data-ttu-id="23fce-152">Defina alguns parâmetros.</span><span class="sxs-lookup"><span data-stu-id="23fce-152">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

<span data-ttu-id="23fce-153">Obtenha o objeto da VM.</span><span class="sxs-lookup"><span data-stu-id="23fce-153">Get the VM object.</span></span>

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="23fce-154">Obtenha o nome de disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="23fce-154">Get the OS disk name.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

<span data-ttu-id="23fce-155">Crie a configuração do instantâneo.</span><span class="sxs-lookup"><span data-stu-id="23fce-155">Create the snapshot configuration.</span></span> 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

<span data-ttu-id="23fce-156">Crie o instantâneo.</span><span class="sxs-lookup"><span data-stu-id="23fce-156">Take the snapshot.</span></span>

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


<span data-ttu-id="23fce-157">Se você planeja usar o instantâneo para criar uma VM que precisa ser de alto desempenho, use o parâmetro `-AccountType Premium_LRS` com o comando New-AzureRmSnapshot.</span><span class="sxs-lookup"><span data-stu-id="23fce-157">If you plan to use the snapshot to create a VM that needs to be high performing, use the parameter `-AccountType Premium_LRS` with the New-AzureRmSnapshot command.</span></span> <span data-ttu-id="23fce-158">O parâmetro cria o instantâneo para que ele seja armazenado como um Disco Gerenciado Premium.</span><span class="sxs-lookup"><span data-stu-id="23fce-158">The parameter creates the snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="23fce-159">Os Discos Gerenciados Premium são mais caros que os Standard.</span><span class="sxs-lookup"><span data-stu-id="23fce-159">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="23fce-160">Portanto certifique-se de que você realmente precisa Premium antes de usar o parâmetro.</span><span class="sxs-lookup"><span data-stu-id="23fce-160">So be sure you really need Premium before using the parameter.</span></span>

### <a name="create-a-new-disk-from-the-snapshot"></a><span data-ttu-id="23fce-161">Criar um novo disco a partir do instantâneo</span><span class="sxs-lookup"><span data-stu-id="23fce-161">Create a new disk from the snapshot</span></span>

<span data-ttu-id="23fce-162">Criar um disco gerenciado de instantâneo usando [AzureRMDisk novo](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="23fce-162">Create a managed disk from the snapshot using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="23fce-163">Este exemplo usa *myOSDisk* para o nome do disco.</span><span class="sxs-lookup"><span data-stu-id="23fce-163">This example uses *myOSDisk* for the disk name.</span></span>

<span data-ttu-id="23fce-164">Criar um novo grupo de recursos para a nova VM.</span><span class="sxs-lookup"><span data-stu-id="23fce-164">Create a new resource group for the new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="23fce-165">Defina o nome de disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="23fce-165">Set the OS disk name.</span></span> 

```powershell
$osDiskName = 'myOsDisk'
```

<span data-ttu-id="23fce-166">Criar o disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="23fce-166">Create the managed disk.</span></span>

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-the-new-vm"></a><span data-ttu-id="23fce-167">Crie a nova VM</span><span class="sxs-lookup"><span data-stu-id="23fce-167">Create the new VM</span></span> 

<span data-ttu-id="23fce-168">Crie rede e outros recursos de máquina virtual a ser usado pela nova VM.</span><span class="sxs-lookup"><span data-stu-id="23fce-168">Create networking and other VM resources to be used by the new VM.</span></span>

### <a name="create-the-subnet-and-vnet"></a><span data-ttu-id="23fce-169">Criar a VNet e a sub-rede</span><span class="sxs-lookup"><span data-stu-id="23fce-169">Create the subNet and vNet</span></span>

<span data-ttu-id="23fce-170">Crie a rede virtual e a sub-rede da [rede virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="23fce-170">Create the vNet and subNet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="23fce-171">Crie a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="23fce-171">Create the subNet.</span></span> <span data-ttu-id="23fce-172">Este exemplo cria uma sub-rede chamada **mySubNet** no grupo de recursos **myDestinationResourceGroup** e defina o prefixo de endereço como **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="23fce-172">This example creates a subnet named **mySubNet**, in the resource group **myDestinationResourceGroup**, and sets the subnet address prefix to **10.0.0.0/24**.</span></span>
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="23fce-173">Crie a VNet.</span><span class="sxs-lookup"><span data-stu-id="23fce-173">Create the vNet.</span></span> <span data-ttu-id="23fce-174">Este exemplo define o nome de rede virtual para **myVnetName**, o local para **Oeste dos EUA** e o prefixo de endereço da rede virtual para **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="23fce-174">This example sets the virtual network name to be **myVnetName**, the location to **West US**, and the address prefix for the virtual network to **10.0.0.0/16**.</span></span> 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="23fce-175">Criar o grupo de segurança de rede e uma regra RDP</span><span class="sxs-lookup"><span data-stu-id="23fce-175">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="23fce-176">Para fazer logon em sua VM usando RDP, é preciso ter uma regra de segurança que permita acesso RDP na porta 3389.</span><span class="sxs-lookup"><span data-stu-id="23fce-176">To be able to log in to your VM using RDP, you need to have a security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="23fce-177">Como o VHD para a nova VM foi criado com base em uma VM especializada existente, você pode usar uma conta na máquina virtual de origem para o RDP.</span><span class="sxs-lookup"><span data-stu-id="23fce-177">Because the VHD for the new VM was created from an existing specialized VM, you can use an account from the source virtual machine for RDP.</span></span>

<span data-ttu-id="23fce-178">Este exemplo define o nome NSG para **myNsg** e o nome da regra RDP para **myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="23fce-178">This example sets the NSG name to **myNsg** and the RDP rule name to **myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="23fce-179">Para obter mais informações sobre regras de NSGs e pontos de extremidade, veja [Abrir portas para uma VM no Azure usando PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="23fce-179">For more information about endpoints and NSG rules, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="23fce-180">Criar um endereço IP público e uma NIC</span><span class="sxs-lookup"><span data-stu-id="23fce-180">Create a public IP address and NIC</span></span>
<span data-ttu-id="23fce-181">Para habilitar a comunicação com a máquina virtual na rede virtual, são necessários um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="23fce-181">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

<span data-ttu-id="23fce-182">Crie o endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="23fce-182">Create the public IP.</span></span> <span data-ttu-id="23fce-183">Neste exemplo, o nome do endereço IP público é definido como **myIP**.</span><span class="sxs-lookup"><span data-stu-id="23fce-183">In this example, the public IP address name is set to **myIP**.</span></span>
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

<span data-ttu-id="23fce-184">Crie a NIC.</span><span class="sxs-lookup"><span data-stu-id="23fce-184">Create the NIC.</span></span> <span data-ttu-id="23fce-185">Neste exemplo, o nome da NIC é definido como **myNicName**.</span><span class="sxs-lookup"><span data-stu-id="23fce-185">In this example, the NIC name is set to **myNicName**.</span></span>
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-the-vm-name-and-size"></a><span data-ttu-id="23fce-186">Como definir o nome e tamanho da VM</span><span class="sxs-lookup"><span data-stu-id="23fce-186">Set the VM name and size</span></span>

<span data-ttu-id="23fce-187">Este exemplo define o nome da VM para *myVM* e o tamanho da VM para *Standard_A2*.</span><span class="sxs-lookup"><span data-stu-id="23fce-187">This example sets the VM name to *myVM* and the VM size to *Standard_A2*.</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-the-nic"></a><span data-ttu-id="23fce-188">Como adicionar o NIC</span><span class="sxs-lookup"><span data-stu-id="23fce-188">Add the NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-the-os-disk"></a><span data-ttu-id="23fce-189">Adicionar o disco do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="23fce-189">Add the OS disk</span></span> 

<span data-ttu-id="23fce-190">Adicionar o disco do sistema operacional para a configuração usando [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="23fce-190">Add the OS disk to the configuration using [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span> <span data-ttu-id="23fce-191">Este exemplo define o tamanho do disco para *128 GB* e anexa o disco gerenciado como um disco do sistema operacional do *Windows*.</span><span class="sxs-lookup"><span data-stu-id="23fce-191">This example sets the size of the disk to *128 GB* and attaches the managed disk as a *Windows* OS disk.</span></span>
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-the-vm"></a><span data-ttu-id="23fce-192">Concluir a VM</span><span class="sxs-lookup"><span data-stu-id="23fce-192">Complete the VM</span></span> 

<span data-ttu-id="23fce-193">Crie a VM usando as configurações [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm) que acabamos de criar.</span><span class="sxs-lookup"><span data-stu-id="23fce-193">Create the VM using [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)the configurations that we just created.</span></span>

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

<span data-ttu-id="23fce-194">Se o comando for bem-sucedido, você verá uma saída como esta:</span><span class="sxs-lookup"><span data-stu-id="23fce-194">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="23fce-195">Verificar se a VM foi criada</span><span class="sxs-lookup"><span data-stu-id="23fce-195">Verify that the VM was created</span></span>
<span data-ttu-id="23fce-196">Você deverá ver a VM recém-criada no [Portal do Azure](https://portal.azure.com) em **Procurar** > **Máquinas virtuais** ou usando os seguintes comandos do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="23fce-196">You should see the newly created VM either in the [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="23fce-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="23fce-197">Next steps</span></span>
<span data-ttu-id="23fce-198">Para entrar em sua nova máquina virtual, navegue até a VM no [portal](https://portal.azure.com), clique em **Conectar**e abra o arquivo RDP da Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="23fce-198">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="23fce-199">Use as credenciais da conta da máquina virtual original para entrar na nova máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="23fce-199">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="23fce-200">Para obter mais informações, veja [Como se conectar e fazer logon em uma máquina virtual do Azure executando o Windows](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="23fce-200">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md).</span></span>

