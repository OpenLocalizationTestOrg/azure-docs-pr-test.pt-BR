---
title: Anexar um disco de dados a uma VM do Windows no Azure usando o PowerShell | Microsoft Docs
description: "Como anexar novos discos de dados, ou existente, a uma VM do Windows usando o PowerShell com o modelo de implantação do Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: cynthn
ms.openlocfilehash: 486e6a27fa28ec63001d824fe9f59c03a7aea5a7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="attach-a-data-disk-to-a-windows-vm-using-powershell"></a><span data-ttu-id="7f081-103">Anexar um disco de dados a uma VM do Windows usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f081-103">Attach a data disk to a Windows VM using PowerShell</span></span>

<span data-ttu-id="7f081-104">Este artigo mostra como anexar discos novos e existentes a uma máquina virtual Windows usando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f081-104">This article shows you how to attach both new and existing disks to a Windows virtual machine using PowerShell.</span></span> <span data-ttu-id="7f081-105">Se sua VM usar discos gerenciados, anexe discos de dados gerenciados adicionais.</span><span class="sxs-lookup"><span data-stu-id="7f081-105">If your VM uses managed disks, you can attach additional managed data disks.</span></span> <span data-ttu-id="7f081-106">Você também pode anexar discos de dados não gerenciados a uma VM que utiliza discos não gerenciados em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7f081-106">You can also attach unmanaged data disks to a VM that uses unmanaged disks in a storage account.</span></span>

<span data-ttu-id="7f081-107">Antes de fazer isso, revise estas dicas:</span><span class="sxs-lookup"><span data-stu-id="7f081-107">Before you do this, review these tips:</span></span>
* <span data-ttu-id="7f081-108">O tamanho da máquina virtual controla quantos discos de dados você pode anexar a ela.</span><span class="sxs-lookup"><span data-stu-id="7f081-108">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="7f081-109">Para obter detalhes, consulte [Tamanhos das máquinas virtuais](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7f081-109">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="7f081-110">Para usar o Armazenamento Premium, você precisará de uma VM habilitada para Armazenamento Premium, como a série DS ou GS.</span><span class="sxs-lookup"><span data-stu-id="7f081-110">To use Premium storage, you'll need a Premium Storage enabled VM size like the DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="7f081-111">Você pode usar discos de contas de armazenamento Premium e Standard com essas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="7f081-111">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="7f081-112">O armazenamento Premium está disponível em determinadas regiões.</span><span class="sxs-lookup"><span data-stu-id="7f081-112">Premium storage is available in certain regions.</span></span> <span data-ttu-id="7f081-113">Para obter detalhes, confira [Armazenamento Premium: armazenamento de alto desempenho para as cargas de trabalho das máquinas virtuais do Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7f081-113">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7f081-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="7f081-114">Before you begin</span></span>
<span data-ttu-id="7f081-115">Caso use o PowerShell, verifique se você tem a versão mais recente do módulo AzureRM.Compute do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f081-115">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="7f081-116">Execute o comando a seguir para instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="7f081-116">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="7f081-117">Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="7f081-117">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="add-an-empty-data-disk-to-a-virtual-machine"></a><span data-ttu-id="7f081-118">Adicionar um disco de dados vazio a uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7f081-118">Add an empty data disk to a virtual machine</span></span>

<span data-ttu-id="7f081-119">Este exemplo mostra como adicionar um disco de dados vazio a uma máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="7f081-119">This example shows how to add an empty data disk to an existing virtual machine.</span></span>

### <a name="using-managed-disks"></a><span data-ttu-id="7f081-120">Usar discos gerenciados</span><span class="sxs-lookup"><span data-stu-id="7f081-120">Using managed disks</span></span>

```powershell
$rgName = 'myResourceGroup'
$vmName = 'myVM'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk1'

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Empty -DiskSizeGB 128

$dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

### <a name="using-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="7f081-121">Usar discos não gerenciados em uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="7f081-121">Using unmanaged disks in a storage account</span></span>

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-the-disk"></a><span data-ttu-id="7f081-122">Inicializar o disco</span><span class="sxs-lookup"><span data-stu-id="7f081-122">Initialize the disk</span></span>

<span data-ttu-id="7f081-123">Depois de adicionar um disco vazio, é necessário inicializá-lo.</span><span class="sxs-lookup"><span data-stu-id="7f081-123">After you add an empty disk, you need to initialize it.</span></span> <span data-ttu-id="7f081-124">Para inicializar o disco, você pode fazer logon em uma VM e usar o gerenciamento de disco.</span><span class="sxs-lookup"><span data-stu-id="7f081-124">To initialize the disk, you can log in to a VM and use disk management.</span></span> <span data-ttu-id="7f081-125">Se você habilitou o WinRM e um certificado na VM durante a criação, você pode usar o PowerShell remoto para inicializar o disco.</span><span class="sxs-lookup"><span data-stu-id="7f081-125">If you enabled WinRM and a certificate on the VM when you created it, you can use remote PowerShell to initialize the disk.</span></span> <span data-ttu-id="7f081-126">Você também pode usar uma extensão de script personalizado:</span><span class="sxs-lookup"><span data-stu-id="7f081-126">You can also use a custom script extension:</span></span> 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
<span data-ttu-id="7f081-127">O arquivo de script pode conter algo parecido com este código para inicialização dos discos:</span><span class="sxs-lookup"><span data-stu-id="7f081-127">The script file can contain something like this code to initialize the disks:</span></span>

```powershell
    $disks = Get-Disk | Where partitionstyle -eq 'raw' | sort number

    $letters = 70..89 | ForEach-Object { [char]$_ }
    $count = 0
    $labels = "data1","data2"

    foreach ($disk in $disks) {
        $driveLetter = $letters[$count].ToString()
        $disk | 
        Initialize-Disk -PartitionStyle MBR -PassThru |
        New-Partition -UseMaximumSize -DriveLetter $driveLetter |
        Format-Volume -FileSystem NTFS -NewFileSystemLabel $labels[$count] -Confirm:$false -Force
    $count++
    }
```


## <a name="attach-an-existing-data-disk-to-a-vm"></a><span data-ttu-id="7f081-128">Anexar um disco de dados existente a uma VM</span><span class="sxs-lookup"><span data-stu-id="7f081-128">Attach an existing data disk to a VM</span></span>

<span data-ttu-id="7f081-129">Você também pode anexar um VHD existente como um disco de dados gerenciados para uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7f081-129">You can also attach an existing VHD as a managed data disk to a virtual machine.</span></span> 

### <a name="using-managed-disks"></a><span data-ttu-id="7f081-130">Usar discos gerenciados</span><span class="sxs-lookup"><span data-stu-id="7f081-130">Using managed disks</span></span>

```powershell
$rgName = 'myRG'
$vmName = 'ContosoMdPir3'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk2'
$dataVhdUri = 'https://mystorageaccount.blob.core.windows.net/vhds/managed_data_disk.vhd' 

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Import -SourceUri $dataVhdUri -DiskSizeGB 128

$dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk2.Id -Lun 2

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

## <a name="next-steps"></a><span data-ttu-id="7f081-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7f081-131">Next steps</span></span>

<span data-ttu-id="7f081-132">Criar um [instantâneo](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="7f081-132">Create a [snapshot](snapshot-copy-managed-disk.md).</span></span>
