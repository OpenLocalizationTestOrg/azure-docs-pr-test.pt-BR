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
# <a name="resize-a-windows-vm"></a>Redimensionar uma VM do Windows
Este artigo mostra como tooresize uma VM do Windows criada no modelo de implantação do Gerenciador de recursos do hello usando o Powershell do Azure.

Depois de criar uma máquina virtual (VM), você pode dimensionar Olá VM para cima ou para baixo, alterando o tamanho da VM hello. Em alguns casos, você deverá desalocar Olá VM pela primeira vez. Isso pode acontecer se o novo tamanho de saudação não está disponível no cluster de hardware de saudação que está hospedando Olá VM.

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a>Redimensionar uma VM do Windows que não está em um conjunto de disponibilidade
1. Lista os tamanhos de VM Olá que estão disponíveis no cluster de hardware Olá onde Olá VM está hospedado. 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. Se Olá desejado tamanho estiver listado, execute Olá comandos tooresize Olá VM a seguir. Se Olá desejado tamanho não estiver listado, vá toostep 3.
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. Se Olá desejado tamanho não estiver listado, execute Olá toodeallocate Olá VM, redimensioná-la e reiniciar Olá VM de comandos a seguir.
   
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
> Olá ao desalocar VM libera os endereços IP dinâmicos atribuídos toohello VM. Olá SO e discos de dados não são afetados. 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a>Redimensionar uma VM do Windows que está em um conjunto de disponibilidade
Se hello novo tamanho para uma VM em um conjunto de disponibilidade não está disponível no cluster de hardware Olá hospedando Olá VM, em seguida, todas as VMs no conjunto de disponibilidade Olá precisará toobe desalocada tooresize Olá VM. Talvez também seja necessário tooupdate tamanho de saudação de outras VMs no conjunto depois de uma máquina virtual foi redimensionada de disponibilidade de saudação. tooresize uma VM em um conjunto de disponibilidade, execute Olá etapas a seguir.

1. Lista os tamanhos de VM Olá que estão disponíveis no cluster de hardware Olá onde Olá VM está hospedado.
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. Se Olá desejado tamanho estiver listado, execute Olá comandos tooresize Olá VM a seguir. Se não estiver listado, vá toostep 3.
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. Se Olá desejado tamanho não estiver listado, continue com hello toodeallocate as etapas a seguir todas as VMs no conjunto de disponibilidade de saudação, redimensionar VMs e reiniciá-los.
4. Pare todas as VMs no conjunto de disponibilidade de saudação.
   
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
5. Redimensionar e reinicie Olá VMs no conjunto de disponibilidade de saudação.
   
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

## <a name="next-steps"></a>Próximas etapas
* Para obter escalabilidade adicional, execute várias instâncias de VM e expanda. Para saber mais, confira [Dimensionar automaticamente computadores Windows em um Conjunto de Dimensionamento de Máquinas Virtuais](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).

