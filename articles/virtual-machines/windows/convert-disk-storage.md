---
title: "aaaConvert Azure gerenciados armazenamento de discos de padrão toopremium e vice-versa | Microsoft Docs"
description: "Como tooconvert Azure discos gerenciado de toopremium padrão e vice-versa, usando o PowerShell do Azure."
services: virtual-machines-windows
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 11f35cde216e91c0599d3619682686e8eb162fad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a>Converter Azure discos de armazenamento gerenciada do toopremium padrão e vice-versa

Os Managed Disks oferecem duas opções de armazenamento: [Premium](../../storage/storage-premium-storage.md) (baseado em SSD) e [Padrão](../../storage/storage-standard-storage.md) (baseado em HDD). Ele permite que você tooeasily alternar entre as opções de saudação dois com tempo de inatividade mínimo com base em suas necessidades de desempenho. Ele não está disponível para discos não gerenciados. Mas você pode facilmente [converter discos toomanaged](convert-unmanaged-to-managed-disks.md) tooeasily alternar entre as opções de saudação dois.

Este artigo mostra como tooconvert gerenciada discos de toopremium padrão e vice-versa, usando o PowerShell do Azure. Se você precisa tooinstall ou atualizá-lo, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/install-azurerm-ps.md).

## <a name="before-you-begin"></a>Antes de começar

* conversão Olá exige uma reinicialização do hello VM, agende para migração de saudação do seu armazenamento de discos durante uma janela de manutenção já existente. 
* Se você estiver usando discos não gerenciados, primeiro [converter discos toomanaged](convert-unmanaged-to-managed-disks.md) toouse tooswitch este artigo entre as opções de armazenamento Olá dois. 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a>Converter todos os Olá gerenciados discos de uma VM do toopremium padrão e vice-versa

Saudação de exemplo a seguir, mostramos como tooswitch todos Olá discos de máquina virtual do armazenamento toopremium padrão. discos de premium toouse gerenciado, a VM deve usar um [tamanho da VM](sizes.md) que oferece suporte ao armazenamento premium. Este exemplo também alterna tamanho tooa que dá suporte ao armazenamento premium.

```powershell
# Name of hello resource group that contains hello VM
$rgName = 'yourResourceGroup'

# Name of hello your virtual machine
$vmName = 'yourVM'

# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'

# Premium capable size
# Required only if converting storage from standard toopremium
$size = 'Standard_DS2_v2'
$vm = Get-AzureRmVM -Name $vmName -resourceGroupName $rgName

# Stop and deallocate hello VM before changing hello size
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Get all disks in hello resource group of hello VM
$vmDisks = Get-AzureRmDisk -ResourceGroupName $rgName 

# For disks that belong toohello selected VM, convert toopremium storage
foreach ($disk in $vmDisks)
{
    if ($disk.OwnerId -eq $vm.Id)
    {
        $diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
        Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
        -DiskName $disk.Name
    }
}

Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a>Converter um disco gerenciado de toopremium padrão e vice-versa

Para sua carga de trabalho de desenvolvimento/teste, talvez você queira toohave mistura de discos standard e premium tooreduce seu custo. Para fazer isso por meio da atualização toopremium armazenamento, somente os discos de saudação que exigem um melhor desempenho. Saudação de exemplo a seguir, mostramos como tooswitch um único disco de máquina virtual do armazenamento toopremium padrão e vice-versa. discos de premium toouse gerenciado, a VM deve usar um [tamanho da VM](sizes.md) que oferece suporte ao armazenamento premium. Este exemplo também alterna tamanho tooa que dá suporte ao armazenamento premium.

```powershell

$diskName = 'yourDiskName'
# resource group that contains hello managed disk
$rgName = 'yourResourceGroupName'
# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'
# Premium capable size 
$size = 'Standard_DS2_v2'

$disk = Get-AzureRmDisk -DiskName $diskName -ResourceGroupName $rgName

# Get hello ARM resource tooget name and resource group of hello VM
$vmResource = Get-AzureRmResource -ResourceId $disk.OwnerId
$vm = Get-AzureRmVM $vmResource.ResourceGroupName -Name $vmResource.ResourceName 

# Stop and deallocate hello VM before changing hello storage type
Stop-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Update hello storage type
$diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
-DiskName $disk.Name

Start-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name
```

## <a name="next-steps"></a>Próximas etapas

Faça uma cópia somente leitura de uma VM usando [instantâneos](snapshot-copy-managed-disk.md).

