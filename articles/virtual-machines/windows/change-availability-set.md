---
title: Alterar um conjunto de disponibilidade de VM | Microsoft Docs
description: "Saiba como alterar o conjunto de disponibilidade de suas máquinas virtuais usando o Azure PowerShell e o modelo de implantação do Resource Manager."
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 44c90f90-bc9a-4260-a36f-5465e2a1ef94
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/15/2016
ms.author: drewm
ms.openlocfilehash: d1daa01191480eaeb81727416b2134b00c698dc3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="change-the-availability-set-for-a-windows-vm"></a><span data-ttu-id="0d1ea-103">Alterar a conjunto de disponibilidade para uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="0d1ea-103">Change the availability set for a Windows VM</span></span>
<span data-ttu-id="0d1ea-104">As etapas a seguir descrevem como alterar o conjunto de disponibilidade de uma VM usando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0d1ea-104">The following steps describe how to change the availability set of a VM using Azure PowerShell.</span></span> <span data-ttu-id="0d1ea-105">Uma VM só pode ser adicionada a um conjunto de disponibilidade quando ela é criada.</span><span class="sxs-lookup"><span data-stu-id="0d1ea-105">A VM can only be added to an availability set when it is created.</span></span> <span data-ttu-id="0d1ea-106">Para alterar o conjunto de disponibilidade, exclua e recrie a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0d1ea-106">In order to change the availability set, you need to delete and recreate the virtual machine.</span></span> 

## <a name="change-the-availability-set-using-powershell"></a><span data-ttu-id="0d1ea-107">Alterar a conjunto de disponibilidade usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d1ea-107">Change the availability set using PowerShell</span></span>
1. <span data-ttu-id="0d1ea-108">Capture os detalhes importantes a seguir da VM quer será modificada.</span><span class="sxs-lookup"><span data-stu-id="0d1ea-108">Capture the following key details from the VM to be modified.</span></span>
   
    <span data-ttu-id="0d1ea-109">Nome da VM</span><span class="sxs-lookup"><span data-stu-id="0d1ea-109">Name of the VM</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <Name-of-resource-group> -Name <name-of-VM>
    $vm.Name
    ```
   
    <span data-ttu-id="0d1ea-110">Tamanho da VM</span><span class="sxs-lookup"><span data-stu-id="0d1ea-110">VM Size</span></span>
   
    ```powershell
    $vm.HardwareProfile.VmSize
    ```
   
    <span data-ttu-id="0d1ea-111">Adaptador de rede primário da rede e adaptadores de rede opcionais, se existirem na VM</span><span class="sxs-lookup"><span data-stu-id="0d1ea-111">Network primary network interface and optional network interfaces if they exist on the VM</span></span>
   
    ```powershell
    $vm.NetworkProfile.NetworkInterfaces[0].Id
    ```
   
    <span data-ttu-id="0d1ea-112">Perfil de disco do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="0d1ea-112">OS Disk Profile</span></span>
   
    ```powershell
    $vm.StorageProfile.OsDisk.OsType
    $vm.StorageProfile.OsDisk.Name
    $vm.StorageProfile.OsDisk.Vhd.Uri
    ```
   
    <span data-ttu-id="0d1ea-113">Perfis de disco para cada disco de dados</span><span class="sxs-lookup"><span data-stu-id="0d1ea-113">Disk profiles for each data disk</span></span> 
   
    ```powershell
    $vm.StorageProfile.DataDisks[<index>].Lun
    $vm.StorageProfile.DataDisks[<index>].Vhd.Uri
    ```
   
    <span data-ttu-id="0d1ea-114">Extensões de VM instaladas</span><span class="sxs-lookup"><span data-stu-id="0d1ea-114">VM extensions installed</span></span> 
   
    ```powershell
    $vm.Extensions
    ```
2. <span data-ttu-id="0d1ea-115">Exclua a VM sem excluir qualquer um dos discos ou adaptadores de rede.</span><span class="sxs-lookup"><span data-stu-id="0d1ea-115">Delete the VM without deleting any of the disks or the network interfaces.</span></span>
   
    ```powershell
    Remove-AzureRmVM -ResourceGroupName <resourceGroupName> -Name <vmName> 
    ```
3. <span data-ttu-id="0d1ea-116">Criar o conjunto de disponibilidade se ele ainda não existir</span><span class="sxs-lookup"><span data-stu-id="0d1ea-116">Create the availability set if it does not already exist</span></span>
   
    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName <resourceGroupName> -Name <availabilitySetName> -Location "<location>" 
    ```
4. <span data-ttu-id="0d1ea-117">Recriar a VM usando o novo conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="0d1ea-117">Recreate the VM using the new availability set</span></span>
   
    ```powershell
    $vm2 = New-AzureRmVMConfig -VMName <VM-name> -VMSize <vm-size> -AvailabilitySetId <availability-set-id>
   
    Set-AzureRmVMOSDisk -CreateOption "Attach" -VM <vmConfig> -VhdUri <osDiskURI> -Name <osDiskName> [-Windows | -Linux]
   
    Add-AzureRmVMNetworkInterface -VM <vmConfig> -Id  <nicId> 
   
    New-AzureRmVM -ResourceGroupName <resourceGroupName> -Location <location> -VM <vmConfig>
    ``` 
5. <span data-ttu-id="0d1ea-118">Adicione extensões e discos de dados.</span><span class="sxs-lookup"><span data-stu-id="0d1ea-118">Add data disks and extensions.</span></span> <span data-ttu-id="0d1ea-119">Para saber mais, confira [Anexar um disco de dados à VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [Extensões nos modelos do Resource Manager](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span><span class="sxs-lookup"><span data-stu-id="0d1ea-119">For more information, see [Attach Data Disk to VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Extensions in Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span> <span data-ttu-id="0d1ea-120">É possível adicionar extensões e discos de dados à VM usando o PowerShell ou a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d1ea-120">Data disks and extensions can be added to the VM using PowerShell or Azure CLI.</span></span>

## <a name="example-script"></a><span data-ttu-id="0d1ea-121">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="0d1ea-121">Example Script</span></span>
<span data-ttu-id="0d1ea-122">O script a seguir fornece um exemplo de como coletar as informações necessárias, como excluir a VM original e como recriá-la em um novo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="0d1ea-122">The following script provides an example of gathering the required information, deleting the original VM and then recreating it in a new availability set.</span></span>

```powershell
    #set variables
    $rg = "demo-resource-group"
    $vmName = "demo-vm"
    $newAvailSetName = "demo-as"
    $outFile = "C:\temp\outfile.txt"

    #Get VM Details
    $OriginalVM = get-azurermvm -ResourceGroupName $rg -Name $vmName

    #Output VM details to file
    "VM Name: " | Out-File -FilePath $outFile 
    $OriginalVM.Name | Out-File -FilePath $outFile -Append

    "Extensions: " | Out-File -FilePath $outFile -Append
    $OriginalVM.Extensions | Out-File -FilePath $outFile -Append

    "VMSize: " | Out-File -FilePath $outFile -Append
    $OriginalVM.HardwareProfile.VmSize | Out-File -FilePath $outFile -Append

    "NIC: " | Out-File -FilePath $outFile -Append
    $OriginalVM.NetworkProfile.NetworkInterfaces[0].Id | Out-File -FilePath $outFile -Append

    "OSType: " | Out-File -FilePath $outFile -Append
    $OriginalVM.StorageProfile.OsDisk.OsType | Out-File -FilePath $outFile -Append

    "OS Disk: " | Out-File -FilePath $outFile -Append
    $OriginalVM.StorageProfile.OsDisk.Vhd.Uri | Out-File -FilePath $outFile -Append

    if ($OriginalVM.StorageProfile.DataDisks) {
    "Data Disk(s): " | Out-File -FilePath $outFile -Append
    $OriginalVM.StorageProfile.DataDisks | Out-File -FilePath $outFile -Append
    }

    #Remove the original VM
    Remove-AzureRmVM -ResourceGroupName $rg -Name $vmName

    #Create new availability set if it does not exist
    $availSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rg -Name $newAvailSetName -ErrorAction Ignore
    if (-Not $availSet) {
    $availset = New-AzureRmAvailabilitySet -ResourceGroupName $rg -Name $newAvailSetName -Location $OriginalVM.Location
    }

    #Create the basic configuration for the replacement VM
    $newVM = New-AzureRmVMConfig -VMName $OriginalVM.Name -VMSize $OriginalVM.HardwareProfile.VmSize -AvailabilitySetId $availSet.Id
    Set-AzureRmVMOSDisk -VM $NewVM -VhdUri $OriginalVM.StorageProfile.OsDisk.Vhd.Uri  -Name $OriginalVM.Name -CreateOption Attach -Windows

    #Add Data Disks
    foreach ($disk in $OriginalVM.StorageProfile.DataDisks ) { 
    Add-AzureRmVMDataDisk -VM $newVM -Name $disk.Name -VhdUri $disk.Vhd.Uri -Caching $disk.Caching -Lun $disk.Lun -CreateOption Attach -DiskSizeInGB $disk.DiskSizeGB
    }

    #Add NIC(s)
    foreach ($nic in $OriginalVM.NetworkInterfaceIDs) {
        Add-AzureRmVMNetworkInterface -VM $NewVM -Id $nic
    }

    #Create the VM
    New-AzureRmVM -ResourceGroupName $rg -Location $OriginalVM.Location -VM $NewVM -DisableBginfoExtension
```

## <a name="next-steps"></a><span data-ttu-id="0d1ea-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0d1ea-123">Next steps</span></span>
<span data-ttu-id="0d1ea-124">Adicione armazenamento adicional à sua VM incluindo um [disco de dados](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)adicional.</span><span class="sxs-lookup"><span data-stu-id="0d1ea-124">Add additional storage to your VM by adding an additional [data disk](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

