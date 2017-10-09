---
title: aaaUse PowerShell tooresize uma VM do Windows Azure | Microsoft Docs
description: "Redimensione uma máquina virtual do Windows criada no modelo de implantação do Gerenciador de recursos de hello, usando o Powershell do Azure."
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
ms.openlocfilehash: a4a80f3bc99911e4f1a095f0ce63aca00fa50694
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm"></a><span data-ttu-id="eb714-103">Redimensionar uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="eb714-103">Resize a Windows VM</span></span>
<span data-ttu-id="eb714-104">Este artigo mostra como tooresize uma VM do Windows criada no modelo de implantação do Gerenciador de recursos do hello usando o Powershell do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb714-104">This article shows you how tooresize a Windows VM, created in hello Resource Manager deployment model using Azure Powershell.</span></span>

<span data-ttu-id="eb714-105">Depois de criar uma máquina virtual (VM), você pode dimensionar Olá VM para cima ou para baixo, alterando o tamanho da VM hello.</span><span class="sxs-lookup"><span data-stu-id="eb714-105">After you create a virtual machine (VM), you can scale hello VM up or down by changing hello VM size.</span></span> <span data-ttu-id="eb714-106">Em alguns casos, você deverá desalocar Olá VM pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="eb714-106">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="eb714-107">Isso pode acontecer se o novo tamanho de saudação não está disponível no cluster de hardware de saudação que está hospedando Olá VM.</span><span class="sxs-lookup"><span data-stu-id="eb714-107">This can happen if hello new size is not available on hello hardware cluster that is currently hosting hello VM.</span></span>

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a><span data-ttu-id="eb714-108">Redimensionar uma VM do Windows que não está em um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="eb714-108">Resize a Windows VM not in an availability set</span></span>
1. <span data-ttu-id="eb714-109">Lista os tamanhos de VM Olá que estão disponíveis no cluster de hardware Olá onde Olá VM está hospedado.</span><span class="sxs-lookup"><span data-stu-id="eb714-109">List hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span> 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. <span data-ttu-id="eb714-110">Se Olá desejado tamanho estiver listado, execute Olá comandos tooresize Olá VM a seguir.</span><span class="sxs-lookup"><span data-stu-id="eb714-110">If hello desired size is listed, run hello following commands tooresize hello VM.</span></span> <span data-ttu-id="eb714-111">Se Olá desejado tamanho não estiver listado, vá toostep 3.</span><span class="sxs-lookup"><span data-stu-id="eb714-111">If hello desired size is not listed, go on toostep 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="eb714-112">Se Olá desejado tamanho não estiver listado, execute Olá toodeallocate Olá VM, redimensioná-la e reiniciar Olá VM de comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="eb714-112">If hello desired size is not listed, run hello following commands toodeallocate hello VM, resize it, and restart hello VM.</span></span>
   
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
> <span data-ttu-id="eb714-113">Olá ao desalocar VM libera os endereços IP dinâmicos atribuídos toohello VM.</span><span class="sxs-lookup"><span data-stu-id="eb714-113">Deallocating hello VM releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="eb714-114">Olá SO e discos de dados não são afetados.</span><span class="sxs-lookup"><span data-stu-id="eb714-114">hello OS and data disks are not affected.</span></span> 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a><span data-ttu-id="eb714-115">Redimensionar uma VM do Windows que está em um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="eb714-115">Resize a Windows VM in an availability set</span></span>
<span data-ttu-id="eb714-116">Se hello novo tamanho para uma VM em um conjunto de disponibilidade não está disponível no cluster de hardware Olá hospedando Olá VM, em seguida, todas as VMs no conjunto de disponibilidade Olá precisará toobe desalocada tooresize Olá VM.</span><span class="sxs-lookup"><span data-stu-id="eb714-116">If hello new size for a VM in an availability set is not available on hello hardware cluster currently hosting hello VM, then all VMs in hello availability set will need toobe deallocated tooresize hello VM.</span></span> <span data-ttu-id="eb714-117">Talvez também seja necessário tooupdate tamanho de saudação de outras VMs no conjunto depois de uma máquina virtual foi redimensionada de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb714-117">You also might need tooupdate hello size of other VMs in hello availability set after one VM has been resized.</span></span> <span data-ttu-id="eb714-118">tooresize uma VM em um conjunto de disponibilidade, execute Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="eb714-118">tooresize a VM in an availability set, perform hello following steps.</span></span>

1. <span data-ttu-id="eb714-119">Lista os tamanhos de VM Olá que estão disponíveis no cluster de hardware Olá onde Olá VM está hospedado.</span><span class="sxs-lookup"><span data-stu-id="eb714-119">List hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span>
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. <span data-ttu-id="eb714-120">Se Olá desejado tamanho estiver listado, execute Olá comandos tooresize Olá VM a seguir.</span><span class="sxs-lookup"><span data-stu-id="eb714-120">If hello desired size is listed, run hello following commands tooresize hello VM.</span></span> <span data-ttu-id="eb714-121">Se não estiver listado, vá toostep 3.</span><span class="sxs-lookup"><span data-stu-id="eb714-121">If it is not listed, go toostep 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="eb714-122">Se Olá desejado tamanho não estiver listado, continue com hello toodeallocate as etapas a seguir todas as VMs no conjunto de disponibilidade de saudação, redimensionar VMs e reiniciá-los.</span><span class="sxs-lookup"><span data-stu-id="eb714-122">If hello desired size is not listed, continue with hello following steps toodeallocate all VMs in hello availability set, resize VMs, and restart them.</span></span>
4. <span data-ttu-id="eb714-123">Pare todas as VMs no conjunto de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb714-123">Stop all VMs in hello availability set.</span></span>
   
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
5. <span data-ttu-id="eb714-124">Redimensionar e reinicie Olá VMs no conjunto de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb714-124">Resize and restart hello VMs in hello availability set.</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="eb714-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eb714-125">Next steps</span></span>
* <span data-ttu-id="eb714-126">Para obter escalabilidade adicional, execute várias instâncias de VM e expanda. Para saber mais, confira [Dimensionar automaticamente computadores Windows em um Conjunto de Dimensionamento de Máquinas Virtuais](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="eb714-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Windows machines in a Virtual Machine Scale Set](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span></span>

