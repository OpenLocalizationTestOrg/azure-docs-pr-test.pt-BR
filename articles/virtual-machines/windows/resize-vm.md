---
title: Use o PowerShell para redimensionar uma VM Windows no Azure | Microsoft Docs
description: "Redimensione uma máquina virtual do Windows criada no modelo de implantação do Resource Manager usando o Azure Powershell."
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 057ff274-6dad-415e-891c-58f8eea9ed78
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 742efd1496de9ce76b1e5636297ef30f546bd108
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-windows-vm"></a><span data-ttu-id="24298-103">Redimensionar uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="24298-103">Resize a Windows VM</span></span>
<span data-ttu-id="24298-104">Este artigo mostra como redimensionar uma VM do Windows criada no modelo de implantação do Resource Manager usando o Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="24298-104">This article shows you how to resize a Windows VM, created in the Resource Manager deployment model using Azure Powershell.</span></span>

<span data-ttu-id="24298-105">Depois de criar uma VM (máquina virtual), você pode expandir ou reduzir a VM, alterando o tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="24298-105">After you create a virtual machine (VM), you can scale the VM up or down by changing the VM size.</span></span> <span data-ttu-id="24298-106">Em alguns casos, você deverá desalocar a VM primeiro.</span><span class="sxs-lookup"><span data-stu-id="24298-106">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="24298-107">Isso pode acontecer se o novo tamanho não estiver disponível no cluster de hardware que hospeda atualmente a VM.</span><span class="sxs-lookup"><span data-stu-id="24298-107">This can happen if the new size is not available on the hardware cluster that is currently hosting the VM.</span></span>

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a><span data-ttu-id="24298-108">Redimensionar uma VM do Windows que não está em um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="24298-108">Resize a Windows VM not in an availability set</span></span>
1. <span data-ttu-id="24298-109">Liste os tamanhos de VM que estão disponíveis no cluster do hardware onde a VM está hospedada.</span><span class="sxs-lookup"><span data-stu-id="24298-109">List the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span> 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. <span data-ttu-id="24298-110">Se o tamanho desejado estiver listado, execute o comando a seguir para redimensionar a VM.</span><span class="sxs-lookup"><span data-stu-id="24298-110">If the desired size is listed, run the following commands to resize the VM.</span></span> <span data-ttu-id="24298-111">Se o tamanho desejado não estiver listado, vá para a etapa 3.</span><span class="sxs-lookup"><span data-stu-id="24298-111">If the desired size is not listed, go on to step 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="24298-112">Se o tamanho desejado não estiver listado, execute os comandos a seguir para desalocar a máquina virtual, redimensioná-la e reinicie a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="24298-112">If the desired size is not listed, run the following commands to deallocate the VM, resize it, and restart the VM.</span></span>
   
    ```powershell
    $rgname = "<resourceGroupName>"
    $vmname = "<vmName>"
    Stop-AzureRmVM -ResourceGroupName $rgname -VMName $vmname -Force
    $vm = Get-AzureRmVM -ResourceGroupName $rgname -VMName $vmname
    $vm.HardwareProfile.VmSize = "<newVMSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName $rgname
    Start-AzureRmVM -ResourceGroupName $rgname -Name $vmname
    ```

> [!WARNING]
> <span data-ttu-id="24298-113">Desalocar a VM libera os endereços IP dinâmicos atribuídos à VM.</span><span class="sxs-lookup"><span data-stu-id="24298-113">Deallocating the VM releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="24298-114">Os discos do sistema operacional e de dados não são afetados.</span><span class="sxs-lookup"><span data-stu-id="24298-114">The OS and data disks are not affected.</span></span> 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a><span data-ttu-id="24298-115">Redimensionar uma VM do Windows que está em um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="24298-115">Resize a Windows VM in an availability set</span></span>
<span data-ttu-id="24298-116">Se o novo tamanho de uma VM em um conjunto de disponibilidade não estiver disponível no cluster de hardware que está hospedando atualmente a VM, todas as VMs no conjunto de disponibilidade precisarão ser desalocadas para redimensionar a VM.</span><span class="sxs-lookup"><span data-stu-id="24298-116">If the new size for a VM in an availability set is not available on the hardware cluster currently hosting the VM, then all VMs in the availability set will need to be deallocated to resize the VM.</span></span> <span data-ttu-id="24298-117">Talvez também seja necessário atualizar o tamanho de outras VMs no conjunto de disponibilidade depois que uma máquina virtual for redimensionada.</span><span class="sxs-lookup"><span data-stu-id="24298-117">You also might need to update the size of other VMs in the availability set after one VM has been resized.</span></span> <span data-ttu-id="24298-118">Para redimensionar uma VM em um conjunto de disponibilidade, execute as seguintes etapas.</span><span class="sxs-lookup"><span data-stu-id="24298-118">To resize a VM in an availability set, perform the following steps.</span></span>

1. <span data-ttu-id="24298-119">Liste os tamanhos de VM que estão disponíveis no cluster do hardware onde a VM está hospedada.</span><span class="sxs-lookup"><span data-stu-id="24298-119">List the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span>
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. <span data-ttu-id="24298-120">Se o tamanho desejado estiver listado, execute o comando a seguir para redimensionar a VM.</span><span class="sxs-lookup"><span data-stu-id="24298-120">If the desired size is listed, run the following commands to resize the VM.</span></span> <span data-ttu-id="24298-121">Se ela não estiver listada, vá para a etapa 3.</span><span class="sxs-lookup"><span data-stu-id="24298-121">If it is not listed, go to step 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="24298-122">Se o tamanho desejado não estiver listado, continue com as etapas a seguir para desalocar todas as VMs no conjunto de disponibilidade, redimensionar as VMs e reiniciá-las.</span><span class="sxs-lookup"><span data-stu-id="24298-122">If the desired size is not listed, continue with the following steps to deallocate all VMs in the availability set, resize VMs, and restart them.</span></span>
4. <span data-ttu-id="24298-123">Pare todas as VMs no conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="24298-123">Stop all VMs in the availability set.</span></span>
   
   ```powershell
   $rg = "<resourceGroupName>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     Stop-AzureRmVM -ResourceGroupName $rg -Name $vmName -Force
   } 
   ```
5. <span data-ttu-id="24298-124">Redimensione e reinicie todas as VMs no conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="24298-124">Resize and restart the VMs in the availability set.</span></span>
   
   ```powershell
   $rg = "<resourceGroupName>"
   $newSize = "<newVmSize>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     $vm = Get-AzureRmVM -ResourceGroupName $rg -Name $vmName
     $vm.HardwareProfile.VmSize = $newSize
     Update-AzureRmVM -ResourceGroupName $rg -VM $vm
     Start-AzureRmVM -ResourceGroupName $rg -Name $vmName
   }
   ```

## <a name="next-steps"></a><span data-ttu-id="24298-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="24298-125">Next steps</span></span>
* <span data-ttu-id="24298-126">Para obter escalabilidade adicional, execute várias instâncias de VM e expanda.</span><span class="sxs-lookup"><span data-stu-id="24298-126">For additional scalability, run multiple VM instances and scale out.</span></span> <span data-ttu-id="24298-127">Para saber mais, confira [Dimensionar automaticamente computadores Windows em um Conjunto de Dimensionamento de Máquinas Virtuais](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="24298-127">For more information, see [Automatically scale Windows machines in a Virtual Machine Scale Set](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span></span>

