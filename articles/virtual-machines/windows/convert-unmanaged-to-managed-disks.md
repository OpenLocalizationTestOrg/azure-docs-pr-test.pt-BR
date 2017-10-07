---
title: "aaaConvert uma máquina virtual do Windows de não discos toomanaged discos - Azure gerenciados | Microsoft Docs"
description: "Como tooconvert uma VM do Windows de discos não gerenciado toomanaged discos usando o PowerShell no modelo de implantação do Gerenciador de recursos de saudação"
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
ms.date: 06/23/2017
ms.author: cynthn
ms.openlocfilehash: e8ed8694b0e776d22df26261e2fc8340bfe5cafa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>Converter uma máquina virtual do Windows de discos de toomanaged de discos não gerenciado

Se você tiver existente Windows (máquinas virtuais) que usa discos não gerenciados, você pode converter Olá VMs toouse gerenciado discos por meio de saudação [discos gerenciado do Azure](managed-disks-overview.md) serviço. Esse processo converte disco Olá SO e discos de dados anexado.

Este artigo mostra como tooconvert VMs usando o PowerShell do Azure. Se você precisa tooinstall ou atualizá-lo, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/install-azurerm-ps.md).

## <a name="before-you-begin"></a>Antes de começar


* Revisão [planejar a migração de saudação do tooManaged discos](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a>Converter VMs de instância única
Esta seção aborda como VMs do Azure de não gerenciado de instância única de tooconvert discos toomanaged discos. (Se suas VMs estiverem em um conjunto de disponibilidade, consulte Olá próxima seção.) 

1. Desalocar Olá VM usando Olá [AzureRmVM Stop](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet. exemplo a seguir Hello desaloca Olá VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`: 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. Converter os discos de toomanaged VM hello usando Olá [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet. Olá seguindo o processo converte Olá VM anterior, incluindo disco Olá SO e discos de dados:

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. Iniciar Olá VM depois de discos do hello conversão toomanaged usando [AzureRmVM início](/powershell/module/azurerm.compute/start-azurermvm). Olá reinicializações de exemplo a seguir Olá VM anterior:

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a>Converter VMs em um conjunto de disponibilidade

Se Olá VMs que você deseja tooconvert toomanaged discos estão em um conjunto de disponibilidade, é necessário primeiro conjunto de disponibilidade do tooconvert Olá tooa gerenciado conjunto de disponibilidade.

1. Converter a disponibilidade de saudação definida por meio de saudação [AzureRmAvailabilitySet atualização](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet. Olá atualizações Olá conjunto nomeada de disponibilidade de exemplo a seguir `myAvailabilitySet` no grupo de recursos de saudação chamado `myResourceGroup`:

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  Se região Olá onde se encontra o conjunto de disponibilidade tiver apenas 2 domínios de falha gerenciado mas número Olá de domínios de falha não gerenciado é 3, este comando mostra um erro semelhante muito "hello especificado contagem de domínios de falha 3 deve estar no hello too2 de intervalo de 1." tooresolve Olá erro, too2 de domínio de falha de saudação de atualização e update `Sku` muito`Aligned` da seguinte maneira:

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. Desalocar e converter Olá VMs no conjunto de disponibilidade de saudação. Olá script a seguir desaloca cada VM usando Olá [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, converte-o usando [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk)e reiniciá-lo usando [AzureRmVM de início ](/powershell/module/azurerm.compute/start-azurermvm):

  ```powershell
  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName

  foreach($vmInfo in $avSet.VirtualMachinesReferences)
  {
     $vm = Get-AzureRmVM -ResourceGroupName $rgName | Where-Object {$_.Id -eq $vmInfo.id}
     Stop-AzureRmVM -ResourceGroupName $rgName -Name $vm.Name -Force
     ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vm.Name
     Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  }
  ```


## <a name="troubleshooting"></a>Solucionar problemas

Se houver um erro durante a conversão, ou se uma VM está em um estado de falha devido a problemas na conversão anterior, execute Olá `ConvertTo-AzureRmVMManagedDisk` cmdlet novamente. Uma repetição simple geralmente desbloqueia situação hello.


## <a name="next-steps"></a>Próximas etapas

[Converter discos gerenciados padrão toopremium](convert-disk-storage.md)

Faça uma cópia somente leitura de uma VM usando [instantâneos](snapshot-copy-managed-disk.md).

