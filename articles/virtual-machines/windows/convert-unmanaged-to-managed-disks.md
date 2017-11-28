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
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a><span data-ttu-id="9247b-103">Converter uma máquina virtual do Windows de discos de toomanaged de discos não gerenciado</span><span class="sxs-lookup"><span data-stu-id="9247b-103">Convert a Windows virtual machine from unmanaged disks toomanaged disks</span></span>

<span data-ttu-id="9247b-104">Se você tiver existente Windows (máquinas virtuais) que usa discos não gerenciados, você pode converter Olá VMs toouse gerenciado discos por meio de saudação [discos gerenciado do Azure](managed-disks-overview.md) serviço.</span><span class="sxs-lookup"><span data-stu-id="9247b-104">If you have existing Windows virtual machines (VMs) that use unmanaged disks, you can convert hello VMs toouse managed disks through hello [Azure Managed Disks](managed-disks-overview.md) service.</span></span> <span data-ttu-id="9247b-105">Esse processo converte disco Olá SO e discos de dados anexado.</span><span class="sxs-lookup"><span data-stu-id="9247b-105">This process converts both hello OS disk and any attached data disks.</span></span>

<span data-ttu-id="9247b-106">Este artigo mostra como tooconvert VMs usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="9247b-106">This article shows you how tooconvert VMs by using Azure PowerShell.</span></span> <span data-ttu-id="9247b-107">Se você precisa tooinstall ou atualizá-lo, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9247b-107">If you need tooinstall or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9247b-108">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="9247b-108">Before you begin</span></span>


* <span data-ttu-id="9247b-109">Revisão [planejar a migração de saudação do tooManaged discos](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span><span class="sxs-lookup"><span data-stu-id="9247b-109">Review [Plan for hello migration tooManaged Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a><span data-ttu-id="9247b-110">Converter VMs de instância única</span><span class="sxs-lookup"><span data-stu-id="9247b-110">Convert single-instance VMs</span></span>
<span data-ttu-id="9247b-111">Esta seção aborda como VMs do Azure de não gerenciado de instância única de tooconvert discos toomanaged discos.</span><span class="sxs-lookup"><span data-stu-id="9247b-111">This section covers how tooconvert single-instance Azure VMs from unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="9247b-112">(Se suas VMs estiverem em um conjunto de disponibilidade, consulte Olá próxima seção.)</span><span class="sxs-lookup"><span data-stu-id="9247b-112">(If your VMs are in an availability set, see hello next section.)</span></span> 

1. <span data-ttu-id="9247b-113">Desalocar Olá VM usando Olá [AzureRmVM Stop](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9247b-113">Deallocate hello VM by using hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet.</span></span> <span data-ttu-id="9247b-114">exemplo a seguir Hello desaloca Olá VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9247b-114">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span> 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. <span data-ttu-id="9247b-115">Converter os discos de toomanaged VM hello usando Olá [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9247b-115">Convert hello VM toomanaged disks by using hello [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet.</span></span> <span data-ttu-id="9247b-116">Olá seguindo o processo converte Olá VM anterior, incluindo disco Olá SO e discos de dados:</span><span class="sxs-lookup"><span data-stu-id="9247b-116">hello following process converts hello previous VM, including hello OS disk and any data disks:</span></span>

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. <span data-ttu-id="9247b-117">Iniciar Olá VM depois de discos do hello conversão toomanaged usando [AzureRmVM início](/powershell/module/azurerm.compute/start-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="9247b-117">Start hello VM after hello conversion toomanaged disks by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span></span> <span data-ttu-id="9247b-118">Olá reinicializações de exemplo a seguir Olá VM anterior:</span><span class="sxs-lookup"><span data-stu-id="9247b-118">hello following example restarts hello previous VM:</span></span>

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="9247b-119">Converter VMs em um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="9247b-119">Convert VMs in an availability set</span></span>

<span data-ttu-id="9247b-120">Se Olá VMs que você deseja tooconvert toomanaged discos estão em um conjunto de disponibilidade, é necessário primeiro conjunto de disponibilidade do tooconvert Olá tooa gerenciado conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="9247b-120">If hello VMs that you want tooconvert toomanaged disks are in an availability set, you first need tooconvert hello availability set tooa managed availability set.</span></span>

1. <span data-ttu-id="9247b-121">Converter a disponibilidade de saudação definida por meio de saudação [AzureRmAvailabilitySet atualização](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9247b-121">Convert hello availability set by using hello [Update-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet.</span></span> <span data-ttu-id="9247b-122">Olá atualizações Olá conjunto nomeada de disponibilidade de exemplo a seguir `myAvailabilitySet` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9247b-122">hello following example updates hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  <span data-ttu-id="9247b-123">Se região Olá onde se encontra o conjunto de disponibilidade tiver apenas 2 domínios de falha gerenciado mas número Olá de domínios de falha não gerenciado é 3, este comando mostra um erro semelhante muito "hello especificado contagem de domínios de falha 3 deve estar no hello too2 de intervalo de 1."</span><span class="sxs-lookup"><span data-stu-id="9247b-123">If hello region where your availability set is located has only 2 managed fault domains but hello number of unmanaged fault domains is 3, this command shows an error similar too"hello specified fault domain count 3 must fall in hello range 1 too2."</span></span> <span data-ttu-id="9247b-124">tooresolve Olá erro, too2 de domínio de falha de saudação de atualização e update `Sku` muito`Aligned` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9247b-124">tooresolve hello error, update hello fault domain too2 and update `Sku` too`Aligned` as follows:</span></span>

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. <span data-ttu-id="9247b-125">Desalocar e converter Olá VMs no conjunto de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="9247b-125">Deallocate and convert hello VMs in hello availability set.</span></span> <span data-ttu-id="9247b-126">Olá script a seguir desaloca cada VM usando Olá [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, converte-o usando [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk)e reiniciá-lo usando [AzureRmVM de início ](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="9247b-126">hello following script deallocates each VM by using hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, converts it by using [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk), and restarts it by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

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


## <a name="troubleshooting"></a><span data-ttu-id="9247b-127">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="9247b-127">Troubleshooting</span></span>

<span data-ttu-id="9247b-128">Se houver um erro durante a conversão, ou se uma VM está em um estado de falha devido a problemas na conversão anterior, execute Olá `ConvertTo-AzureRmVMManagedDisk` cmdlet novamente.</span><span class="sxs-lookup"><span data-stu-id="9247b-128">If there is an error during conversion, or if a VM is in a failed state because of issues in a previous conversion, run hello `ConvertTo-AzureRmVMManagedDisk` cmdlet again.</span></span> <span data-ttu-id="9247b-129">Uma repetição simple geralmente desbloqueia situação hello.</span><span class="sxs-lookup"><span data-stu-id="9247b-129">A simple retry usually unblocks hello situation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9247b-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9247b-130">Next steps</span></span>

[<span data-ttu-id="9247b-131">Converter discos gerenciados padrão toopremium</span><span class="sxs-lookup"><span data-stu-id="9247b-131">Convert standard managed disks toopremium</span></span>](convert-disk-storage.md)

<span data-ttu-id="9247b-132">Faça uma cópia somente leitura de uma VM usando [instantâneos](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="9247b-132">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

