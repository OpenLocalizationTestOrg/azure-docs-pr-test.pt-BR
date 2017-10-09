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
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="a190e-103">Converter Azure discos de armazenamento gerenciada do toopremium padrão e vice-versa</span><span class="sxs-lookup"><span data-stu-id="a190e-103">Convert Azure managed disks storage from standard toopremium, and vice versa</span></span>

<span data-ttu-id="a190e-104">Os Managed Disks oferecem duas opções de armazenamento: [Premium](../../storage/storage-premium-storage.md) (baseado em SSD) e [Padrão](../../storage/storage-standard-storage.md) (baseado em HDD).</span><span class="sxs-lookup"><span data-stu-id="a190e-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="a190e-105">Ele permite que você tooeasily alternar entre as opções de saudação dois com tempo de inatividade mínimo com base em suas necessidades de desempenho.</span><span class="sxs-lookup"><span data-stu-id="a190e-105">It allows you tooeasily switch between hello two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="a190e-106">Ele não está disponível para discos não gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a190e-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="a190e-107">Mas você pode facilmente [converter discos toomanaged](convert-unmanaged-to-managed-disks.md) tooeasily alternar entre as opções de saudação dois.</span><span class="sxs-lookup"><span data-stu-id="a190e-107">But you can easily [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) tooeasily switch between hello two options.</span></span>

<span data-ttu-id="a190e-108">Este artigo mostra como tooconvert gerenciada discos de toopremium padrão e vice-versa, usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="a190e-108">This article shows you how tooconvert managed disks from standard toopremium, and vice versa by using Azure PowerShell.</span></span> <span data-ttu-id="a190e-109">Se você precisa tooinstall ou atualizá-lo, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a190e-109">If you need tooinstall or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a190e-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="a190e-110">Before you begin</span></span>

* <span data-ttu-id="a190e-111">conversão Olá exige uma reinicialização do hello VM, agende para migração de saudação do seu armazenamento de discos durante uma janela de manutenção já existente.</span><span class="sxs-lookup"><span data-stu-id="a190e-111">hello conversion requires a restart of hello VM, so schedule hello migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="a190e-112">Se você estiver usando discos não gerenciados, primeiro [converter discos toomanaged](convert-unmanaged-to-managed-disks.md) toouse tooswitch este artigo entre as opções de armazenamento Olá dois.</span><span class="sxs-lookup"><span data-stu-id="a190e-112">If you are using unmanaged disks, first [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) toouse this article tooswitch between hello two storage options.</span></span> 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="a190e-113">Converter todos os Olá gerenciados discos de uma VM do toopremium padrão e vice-versa</span><span class="sxs-lookup"><span data-stu-id="a190e-113">Convert all hello managed disks of a VM from standard toopremium, and vice versa</span></span>

<span data-ttu-id="a190e-114">Saudação de exemplo a seguir, mostramos como tooswitch todos Olá discos de máquina virtual do armazenamento toopremium padrão.</span><span class="sxs-lookup"><span data-stu-id="a190e-114">In hello following example, we show how tooswitch all hello disks of a VM from standard toopremium storage.</span></span> <span data-ttu-id="a190e-115">discos de premium toouse gerenciado, a VM deve usar um [tamanho da VM](sizes.md) que oferece suporte ao armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="a190e-115">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="a190e-116">Este exemplo também alterna tamanho tooa que dá suporte ao armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="a190e-116">This example also switches tooa size that supports premium storage.</span></span>

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
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="a190e-117">Converter um disco gerenciado de toopremium padrão e vice-versa</span><span class="sxs-lookup"><span data-stu-id="a190e-117">Convert a managed disk from standard toopremium, and vice versa</span></span>

<span data-ttu-id="a190e-118">Para sua carga de trabalho de desenvolvimento/teste, talvez você queira toohave mistura de discos standard e premium tooreduce seu custo.</span><span class="sxs-lookup"><span data-stu-id="a190e-118">For your dev/test workload, you may want toohave mixture of standard and premium disks tooreduce your cost.</span></span> <span data-ttu-id="a190e-119">Para fazer isso por meio da atualização toopremium armazenamento, somente os discos de saudação que exigem um melhor desempenho.</span><span class="sxs-lookup"><span data-stu-id="a190e-119">You can accomplish it by upgrading toopremium storage, only hello disks that require better performance.</span></span> <span data-ttu-id="a190e-120">Saudação de exemplo a seguir, mostramos como tooswitch um único disco de máquina virtual do armazenamento toopremium padrão e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="a190e-120">In hello following example, we show how tooswitch a single disk of a VM from standard toopremium storage, and vice versa.</span></span> <span data-ttu-id="a190e-121">discos de premium toouse gerenciado, a VM deve usar um [tamanho da VM](sizes.md) que oferece suporte ao armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="a190e-121">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="a190e-122">Este exemplo também alterna tamanho tooa que dá suporte ao armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="a190e-122">This example also switches tooa size that supports premium storage.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a190e-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a190e-123">Next steps</span></span>

<span data-ttu-id="a190e-124">Faça uma cópia somente leitura de uma VM usando [instantâneos](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="a190e-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

