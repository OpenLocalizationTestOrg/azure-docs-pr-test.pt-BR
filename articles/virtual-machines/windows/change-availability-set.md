---
title: "aaaChange um conjunto de disponibilidade de máquinas virtuais | Microsoft Docs"
description: "Saiba como a disponibilidade de saudação toochange definida para suas máquinas virtuais usando o PowerShell do Azure e o modelo de implantação do Gerenciador de recursos de saudação."
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
ms.openlocfilehash: 3b1cc010a6d4c4883f2e34da9cfca4372aec92cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-availability-set-for-a-windows-vm"></a><span data-ttu-id="09790-103">Alterar a disponibilidade de saudação definido para uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="09790-103">Change hello availability set for a Windows VM</span></span>
<span data-ttu-id="09790-104">Olá, as etapas a seguir descreve como toochange Olá conjunto de disponibilidade de uma VM usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="09790-104">hello following steps describe how toochange hello availability set of a VM using Azure PowerShell.</span></span> <span data-ttu-id="09790-105">Uma VM só pode ser adicionada tooan disponibilidade definida quando ele é criado.</span><span class="sxs-lookup"><span data-stu-id="09790-105">A VM can only be added tooan availability set when it is created.</span></span> <span data-ttu-id="09790-106">No conjunto de disponibilidade do pedido toochange hello, você precisa toodelete e recria a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="09790-106">In order toochange hello availability set, you need toodelete and recreate hello virtual machine.</span></span> 

## <a name="change-hello-availability-set-using-powershell"></a><span data-ttu-id="09790-107">Alterar a disponibilidade de saudação definida usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="09790-107">Change hello availability set using PowerShell</span></span>
1. <span data-ttu-id="09790-108">Capture Olá seguir detalhes da chave de saudação VM toobe modificado.</span><span class="sxs-lookup"><span data-stu-id="09790-108">Capture hello following key details from hello VM toobe modified.</span></span>
   
    <span data-ttu-id="09790-109">Nome da saudação VM</span><span class="sxs-lookup"><span data-stu-id="09790-109">Name of hello VM</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <Name-of-resource-group> -Name <name-of-VM>
    $vm.Name
    ```
   
    <span data-ttu-id="09790-110">Tamanho da VM</span><span class="sxs-lookup"><span data-stu-id="09790-110">VM Size</span></span>
   
    ```powershell
    $vm.HardwareProfile.VmSize
    ```
   
    <span data-ttu-id="09790-111">Interface de rede principal e interfaces de rede opcional se eles existirem no hello VM</span><span class="sxs-lookup"><span data-stu-id="09790-111">Network primary network interface and optional network interfaces if they exist on hello VM</span></span>
   
    ```powershell
    $vm.NetworkProfile.NetworkInterfaces[0].Id
    ```
   
    <span data-ttu-id="09790-112">Perfil de disco do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="09790-112">OS Disk Profile</span></span>
   
    ```powershell
    $vm.StorageProfile.OsDisk.OsType
    $vm.StorageProfile.OsDisk.Name
    $vm.StorageProfile.OsDisk.Vhd.Uri
    ```
   
    <span data-ttu-id="09790-113">Perfis de disco para cada disco de dados</span><span class="sxs-lookup"><span data-stu-id="09790-113">Disk profiles for each data disk</span></span> 
   
    ```powershell
    $vm.StorageProfile.DataDisks[<index>].Lun
    $vm.StorageProfile.DataDisks[<index>].Vhd.Uri
    ```
   
    <span data-ttu-id="09790-114">Extensões de VM instaladas</span><span class="sxs-lookup"><span data-stu-id="09790-114">VM extensions installed</span></span> 
   
    ```powershell
    $vm.Extensions
    ```
2. <span data-ttu-id="09790-115">Exclua Olá VM sem excluir nenhum dos discos de saudação ou interfaces de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="09790-115">Delete hello VM without deleting any of hello disks or hello network interfaces.</span></span>
   
    ```powershell
    Remove-AzureRmVM -ResourceGroupName <resourceGroupName> -Name <vmName> 
    ```
3. <span data-ttu-id="09790-116">Criar hello disponibilidade definida se ele ainda não existir</span><span class="sxs-lookup"><span data-stu-id="09790-116">Create hello availability set if it does not already exist</span></span>
   
    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName <resourceGroupName> -Name <availabilitySetName> -Location "<location>" 
    ```
4. <span data-ttu-id="09790-117">Recriar Olá VM usando o novo conjunto de disponibilidade Olá</span><span class="sxs-lookup"><span data-stu-id="09790-117">Recreate hello VM using hello new availability set</span></span>
   
    ```powershell
    $vm2 = New-AzureRmVMConfig -VMName <VM-name> -VMSize <vm-size> -AvailabilitySetId <availability-set-id>
   
    Set-AzureRmVMOSDisk -CreateOption "Attach" -VM <vmConfig> -VhdUri <osDiskURI> -Name <osDiskName> [-Windows | -Linux]
   
    Add-AzureRmVMNetworkInterface -VM <vmConfig> -Id  <nicId> 
   
    New-AzureRmVM -ResourceGroupName <resourceGroupName> -Location <location> -VM <vmConfig>
    ``` 
5. <span data-ttu-id="09790-118">Adicione extensões e discos de dados.</span><span class="sxs-lookup"><span data-stu-id="09790-118">Add data disks and extensions.</span></span> <span data-ttu-id="09790-119">Para obter mais informações, consulte [anexar disco de dados tooVM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [extensões em modelos do Gerenciador de recursos](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span><span class="sxs-lookup"><span data-stu-id="09790-119">For more information, see [Attach Data Disk tooVM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Extensions in Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span> <span data-ttu-id="09790-120">Discos de dados e as extensões podem ser adicionadas toohello VM usando o PowerShell ou CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="09790-120">Data disks and extensions can be added toohello VM using PowerShell or Azure CLI.</span></span>

## <a name="example-script"></a><span data-ttu-id="09790-121">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="09790-121">Example Script</span></span>
<span data-ttu-id="09790-122">Olá, script a seguir fornece um exemplo de coleta de informações de saudação necessária, excluindo Olá VM original e, em seguida, recriá-la em um novo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="09790-122">hello following script provides an example of gathering hello required information, deleting hello original VM and then recreating it in a new availability set.</span></span>

```powershell
    #set variables
    $rg = "demo-resource-group"
    $vmName = "demo-vm"
    $newAvailSetName = "demo-as"
    $outFile = "C:\temp\outfile.txt"

    #Get VM Details
    $OriginalVM = get-azurermvm -ResourceGroupName $rg -Name $vmName

    #Output VM details toofile
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

    #Remove hello original VM
    Remove-AzureRmVM -ResourceGroupName $rg -Name $vmName

    #Create new availability set if it does not exist
    $availSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rg -Name $newAvailSetName -ErrorAction Ignore
    if (-Not $availSet) {
    $availset = New-AzureRmAvailabilitySet -ResourceGroupName $rg -Name $newAvailSetName -Location $OriginalVM.Location
    }

    #Create hello basic configuration for hello replacement VM
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

    #Create hello VM
    New-AzureRmVM -ResourceGroupName $rg -Location $OriginalVM.Location -VM $NewVM -DisableBginfoExtension
```

## <a name="next-steps"></a><span data-ttu-id="09790-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="09790-123">Next steps</span></span>
<span data-ttu-id="09790-124">Adicionar armazenamento adicional tooyour VM adicionando mais [disco de dados](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="09790-124">Add additional storage tooyour VM by adding an additional [data disk](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

