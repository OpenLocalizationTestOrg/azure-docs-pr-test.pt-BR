---
title: aaaAttach um disco de dados tooa VM do Windows no Azure usando o PowerShell | Microsoft Docs
description: "Como os dados de novo ou existente tooattach disco tooa VM do Windows usando o PowerShell com o modelo de implantação do Gerenciador de recursos de saudação."
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
ms.openlocfilehash: 12ffdd4ced791ba0948047d3af24ad73e36c7ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-vm-using-powershell"></a><span data-ttu-id="72bd1-103">Anexar um disco de dados tooa VM do Windows usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="72bd1-103">Attach a data disk tooa Windows VM using PowerShell</span></span>

<span data-ttu-id="72bd1-104">Este artigo mostra como tooattach novo e existente discos tooa máquina virtual do Windows usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72bd1-104">This article shows you how tooattach both new and existing disks tooa Windows virtual machine using PowerShell.</span></span> <span data-ttu-id="72bd1-105">Se sua VM usar discos gerenciados, anexe discos de dados gerenciados adicionais.</span><span class="sxs-lookup"><span data-stu-id="72bd1-105">If your VM uses managed disks, you can attach additional managed data disks.</span></span> <span data-ttu-id="72bd1-106">Você também pode anexar discos de dados não gerenciados tooa VM que utiliza discos não gerenciados em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="72bd1-106">You can also attach unmanaged data disks tooa VM that uses unmanaged disks in a storage account.</span></span>

<span data-ttu-id="72bd1-107">Antes de fazer isso, revise estas dicas:</span><span class="sxs-lookup"><span data-stu-id="72bd1-107">Before you do this, review these tips:</span></span>
* <span data-ttu-id="72bd1-108">tamanho de saudação da máquina virtual de saudação controla quantos discos de dados, você pode anexar.</span><span class="sxs-lookup"><span data-stu-id="72bd1-108">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="72bd1-109">Para obter detalhes, consulte [Tamanhos das máquinas virtuais](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="72bd1-109">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="72bd1-110">toouse armazenamento Premium, você precisará de um armazenamento Premium habilitado o tamanho da VM como Olá a máquina virtual da série DS ou série GS.</span><span class="sxs-lookup"><span data-stu-id="72bd1-110">toouse Premium storage, you'll need a Premium Storage enabled VM size like hello DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="72bd1-111">Você pode usar discos de contas de armazenamento Premium e Standard com essas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="72bd1-111">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="72bd1-112">O armazenamento Premium está disponível em determinadas regiões.</span><span class="sxs-lookup"><span data-stu-id="72bd1-112">Premium storage is available in certain regions.</span></span> <span data-ttu-id="72bd1-113">Para obter detalhes, confira [Armazenamento Premium: armazenamento de alto desempenho para as cargas de trabalho das máquinas virtuais do Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="72bd1-113">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="72bd1-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="72bd1-114">Before you begin</span></span>
<span data-ttu-id="72bd1-115">Se você usar o PowerShell, certifique-se de que você tem a versão mais recente Olá de saudação módulo AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72bd1-115">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="72bd1-116">Executar Olá tooinstall de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="72bd1-116">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="72bd1-117">Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="72bd1-117">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="add-an-empty-data-disk-tooa-virtual-machine"></a><span data-ttu-id="72bd1-118">Adicionar uma máquina virtual de tooa de disco de dados vazio</span><span class="sxs-lookup"><span data-stu-id="72bd1-118">Add an empty data disk tooa virtual machine</span></span>

<span data-ttu-id="72bd1-119">Este exemplo mostra como tooadd um dados vazios disco tooan máquina de virtual existente.</span><span class="sxs-lookup"><span data-stu-id="72bd1-119">This example shows how tooadd an empty data disk tooan existing virtual machine.</span></span>

### <a name="using-managed-disks"></a><span data-ttu-id="72bd1-120">Usar discos gerenciados</span><span class="sxs-lookup"><span data-stu-id="72bd1-120">Using managed disks</span></span>

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

### <a name="using-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="72bd1-121">Usar discos não gerenciados em uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="72bd1-121">Using unmanaged disks in a storage account</span></span>

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-hello-disk"></a><span data-ttu-id="72bd1-122">Inicializar disco Olá</span><span class="sxs-lookup"><span data-stu-id="72bd1-122">Initialize hello disk</span></span>

<span data-ttu-id="72bd1-123">Depois de adicionar um disco vazio, será necessário tooinitialize-lo.</span><span class="sxs-lookup"><span data-stu-id="72bd1-123">After you add an empty disk, you need tooinitialize it.</span></span> <span data-ttu-id="72bd1-124">disco de saudação tooinitialize, você pode registrar no gerenciamento de disco VM e o uso de tooa.</span><span class="sxs-lookup"><span data-stu-id="72bd1-124">tooinitialize hello disk, you can log in tooa VM and use disk management.</span></span> <span data-ttu-id="72bd1-125">Se você habilitou o WinRM e um certificado no hello VM ao criá-la, você pode usar o disco de saudação do tooinitialize PowerShell remoto.</span><span class="sxs-lookup"><span data-stu-id="72bd1-125">If you enabled WinRM and a certificate on hello VM when you created it, you can use remote PowerShell tooinitialize hello disk.</span></span> <span data-ttu-id="72bd1-126">Você também pode usar uma extensão de script personalizado:</span><span class="sxs-lookup"><span data-stu-id="72bd1-126">You can also use a custom script extension:</span></span> 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
<span data-ttu-id="72bd1-127">arquivo de script Hello pode conter algo como discos de saudação de tooinitialize este código:</span><span class="sxs-lookup"><span data-stu-id="72bd1-127">hello script file can contain something like this code tooinitialize hello disks:</span></span>

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


## <a name="attach-an-existing-data-disk-tooa-vm"></a><span data-ttu-id="72bd1-128">Anexar um tooa de disco de dados VM existente</span><span class="sxs-lookup"><span data-stu-id="72bd1-128">Attach an existing data disk tooa VM</span></span>

<span data-ttu-id="72bd1-129">Você também pode anexar um VHD existente como uma máquina virtual de tooa de disco de dados gerenciados.</span><span class="sxs-lookup"><span data-stu-id="72bd1-129">You can also attach an existing VHD as a managed data disk tooa virtual machine.</span></span> 

### <a name="using-managed-disks"></a><span data-ttu-id="72bd1-130">Usar discos gerenciados</span><span class="sxs-lookup"><span data-stu-id="72bd1-130">Using managed disks</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="72bd1-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="72bd1-131">Next steps</span></span>

<span data-ttu-id="72bd1-132">Criar um [instantâneo](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="72bd1-132">Create a [snapshot](snapshot-copy-managed-disk.md).</span></span>
