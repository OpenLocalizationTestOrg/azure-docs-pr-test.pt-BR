---
title: aaaExpand um disco de dados anexado tooa VM do Windows no Azure | Microsoft Docs
description: "Expanda o tamanho de saudação de um disco de dados é anexado tooa máquina virtual do Windows usando o PowerShell."
services: virtual-machines-windows
documentationcenter: na
author: cynthn
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.openlocfilehash: b16ad0da9cff9dfffc9dc9ec7dd72891e7ddd745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="increase-hello-size-of-a-data-disk-attached-tooa-windows-vm"></a><span data-ttu-id="ab21a-103">Olá aumente o tamanho de um disco de dados anexado tooa VM do Windows</span><span class="sxs-lookup"><span data-stu-id="ab21a-103">Increase hello size of a data disk attached tooa Windows VM</span></span>

<span data-ttu-id="ab21a-104">Se você precisar tooincrease Olá tamanho da saudação dados disco anexado tooyour máquina virtual, você pode aumentar o tamanho de saudação usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ab21a-104">If you need tooincrease hello size of hello data disk attached tooyour virtual machine, you can increase hello size using PowerShell.</span></span> <span data-ttu-id="ab21a-105">Depois que você aumentar o tamanho de Olá Olá do disco de dados nas configurações de máquina virtual do Azure hello, você também precisa tooallocate Olá novo espaço em disco no hello VM.</span><span class="sxs-lookup"><span data-stu-id="ab21a-105">After you increase hello size of hello data disk in hello Azure VM settings, you also need tooallocate hello new disk space within hello VM.</span></span>


## <a name="use-powershell-tooincrease-hello-size-of-a-managed-data-disk"></a><span data-ttu-id="ab21a-106">Use Powershell tooincrease Olá tamanho de um disco de dados gerenciados</span><span class="sxs-lookup"><span data-stu-id="ab21a-106">Use Powershell tooincrease hello size of a managed data disk</span></span>

<span data-ttu-id="ab21a-107">tamanho de saudação tooincrease de um disco de dados gerenciados, Olá use cmdlets do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab21a-107">tooincrease hello size of a managed data disk, use hello following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="ab21a-108">Get-AzureRMReseourceGroup</span><span class="sxs-lookup"><span data-stu-id="ab21a-108">Get-AzureRMReseourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | [<span data-ttu-id="ab21a-109">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="ab21a-109">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="ab21a-110">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="ab21a-110">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                        | [<span data-ttu-id="ab21a-111">Update-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="ab21a-111">Update-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Update-AzureRmDisk) |
 | [<span data-ttu-id="ab21a-112">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="ab21a-112">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |
<br>

<span data-ttu-id="ab21a-113">Olá script a seguir irá orientá-lo por meio de Obtendo informações de VM hello, seleção de disco de dados hello e especificando o novo tamanho de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab21a-113">hello following script will walk you through getting hello VM information, selecting hello data disk and specifying hello new size.</span></span>

```powershell
# Select resource group

    $rg = Get-AzureRMResourceGroup | Out-GridView `
        -Title "Select hello resource group" `
        -PassThru

    $rgName = $rg.ResourceGroupName

# Select hello VM

    $vm = Get-AzureRMVM -ResourceGroupName $rgName `
        | Out-GridView `
            -Title "Select a VM" `
             -PassThru

# Select data disk

    $disk = $vm.StorageProfile.DataDisks | Out-GridView `
        -Title "Select a data disk" `
        -PassThru

# Specify a larger size for hello data disk

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior tooresizing data disk

    $vm | Stop-AzureRMVM -Force

# Set hello new disk size

    $diskUpdateConfig = New-AzureRmDiskUpdateConfig -DiskSizeGB $size

# Update hello configuration in Azure

    $managedDisk = Get-AzureRmResource -ResourceId $disk.ManagedDisk.Id
    Update-AzureRmDisk -DiskName $managedDisk.ResourceName -ResourceGroupName $managedDisk.ResourceGroupName -DiskUpdate $diskUpdateConfig

# Start hello VM

    Start-AzureRmVM -ResourceGroupName $rgName -VMName $vm.name
```

## <a name="use-powershell-tooincrease-hello-size-of-an-unmanaged-data-disk"></a><span data-ttu-id="ab21a-114">Use PowerShell tooincrease Olá tamanho de um disco de dados não gerenciados</span><span class="sxs-lookup"><span data-stu-id="ab21a-114">Use PowerShell tooincrease hello size of an unmanaged data disk</span></span>

<span data-ttu-id="ab21a-115">tamanho de saudação tooincrease de discos de dados não gerenciados em uma conta de armazenamento, Olá use cmdlets do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab21a-115">tooincrease hello size of unmanaged data disks in a storage account, use hello following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="ab21a-116">Get-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="ab21a-116">Get-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccount) | [<span data-ttu-id="ab21a-117">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="ab21a-117">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="ab21a-118">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="ab21a-118">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                       | [<span data-ttu-id="ab21a-119">Set-AzureRmVMDataDisk</span><span class="sxs-lookup"><span data-stu-id="ab21a-119">Set-AzureRmVMDataDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmdatadisk) |
| [<span data-ttu-id="ab21a-120">Update-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="ab21a-120">Update-AzureRmVM</span></span>](/powershell/module/azurerm.compute/update-azurermvm)                   | [<span data-ttu-id="ab21a-121">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="ab21a-121">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |

<br>

<span data-ttu-id="ab21a-122">Olá script a seguir irá orientá-lo por meio de obtendo Olá VM e o armazenamento de informações de conta, seleção de disco de dados hello e especificando o novo tamanho de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab21a-122">hello following script will walk you through getting hello VM and storage account information, selecting hello data disk and specifying hello new size.</span></span>

```powershell

# Select Azure Storage Account

    $storageAccount =
        Get-AzureRMStorageAccount | Out-GridView `
            -Title "Select Azure Storage Account" `
            -PassThru

    $rgName = $storageAccount.ResourceGroupName

# Select hello VM

    $vm = Get-AzureRMVM `
    -ResourceGroupName $rgName | Out-GridView `
            -Title "Select a VM …" `
            -PassThru

# Select Data Disk tooresize

    $disk =
        $vm.DataDiskNames | Out-GridView `
            -Title "Select a data disk tooresize" `
            -PassThru


# Specify a larger data disk size

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior tooresizing data disk

    $vm | Stop-AzureRMVM -Force

# Set hello new disk size

    Set-AzureRmVMDataDisk -VM $vm -Name "$disk" `
        -DiskSizeInGB $size

# Update hello configuration in Azure

    Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Start hello VM
    Start-AzureRmVM -ResourceGroupName $rgName `
    -VMName $vm.name

```

## <a name="allocate-hello-unallocated-disk-space"></a><span data-ttu-id="ab21a-123">Alocar espaço em disco não alocado de saudação</span><span class="sxs-lookup"><span data-stu-id="ab21a-123">Allocate hello unallocated disk space</span></span>

<span data-ttu-id="ab21a-124">Depois que você fez unidade Olá maior, você precisa tooallocate Olá novo espaço não alocado de dentro de saudação VM.</span><span class="sxs-lookup"><span data-stu-id="ab21a-124">Once you have made hello drive larger, you need tooallocate hello new unallocated space from within hello VM.</span></span> <span data-ttu-id="ab21a-125">espaço de saudação tooallocate, você pode conectar o uso VM toohello gerenciamento de disco (diskmgmt.msc).</span><span class="sxs-lookup"><span data-stu-id="ab21a-125">tooallocate hello space, you can connect toohello VM use Disk Management (diskmgmt.msc).</span></span> <span data-ttu-id="ab21a-126">Ou, se você habilitou o WinRM e um certificado no hello VM ao criá-la, você pode usar o disco de saudação do tooinitialize PowerShell remoto.</span><span class="sxs-lookup"><span data-stu-id="ab21a-126">Or, if you enabled WinRM and a certificate on hello VM when you created it, you can use remote PowerShell tooinitialize hello disk.</span></span> <span data-ttu-id="ab21a-127">Você também pode usar uma extensão de script personalizado:</span><span class="sxs-lookup"><span data-stu-id="ab21a-127">You can also use a custom script extension:</span></span>

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```

<span data-ttu-id="ab21a-128">arquivo de script Hello pode conter algo parecido com este código tooincrease Olá unidade alocação toohello tamanho máximo Olá discos:</span><span class="sxs-lookup"><span data-stu-id="ab21a-128">hello script file can contain something like this code tooincrease hello drive allocation toohello maximum size hello disks:</span></span>

```powershell
$driveLetter= "F"

$MaxSize = (Get-PartitionSupportedSize -DriveLetter $driveLetter).sizeMax

Resize-Partition -DriveLetter $driveLetter -Size $MaxSize
```

## <a name="next-steps"></a><span data-ttu-id="ab21a-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ab21a-129">Next Steps</span></span>
- [<span data-ttu-id="ab21a-130">Saiba mais sobre discos e VHDs</span><span class="sxs-lookup"><span data-stu-id="ab21a-130">Learn more about disks and VHDs</span></span>](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
