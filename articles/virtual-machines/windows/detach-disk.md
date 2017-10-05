---
title: "Desanexar um disco de dados de uma VM Windows – Azure | Microsoft Docs"
description: "Saiba como desanexar um disco de dados de uma máquina virtual no Azure usando o modelo de implantação do Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 13180343-ac49-4a3a-85d8-0ead95e2028c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 97aa69745d200ee76f9f859eb3a8b0ad2f202bad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-detach-a-data-disk-from-a-windows-virtual-machine"></a><span data-ttu-id="1b23c-103">Como desanexar um disco de dados de uma máquina virtual Windows</span><span class="sxs-lookup"><span data-stu-id="1b23c-103">How to detach a data disk from a Windows virtual machine</span></span>
<span data-ttu-id="1b23c-104">Quando não precisar mais de um disco de dados conectado a uma máquina virtual, você poderá desanexá-lo facilmente.</span><span class="sxs-lookup"><span data-stu-id="1b23c-104">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span></span> <span data-ttu-id="1b23c-105">Essa ação remove o disco da máquina virtual, mas não o remove do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1b23c-105">This removes the disk from the virtual machine, but doesn't remove it from storage.</span></span>

> [!WARNING]
> <span data-ttu-id="1b23c-106">Se você desanexar um disco, ele não será excluído automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1b23c-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="1b23c-107">Se você se inscreveu para o armazenamento Premium, você continuará incorrendo em encargos de armazenamento para o disco.</span><span class="sxs-lookup"><span data-stu-id="1b23c-107">If you have subscribed to Premium storage, you will continue to incur storage charges for the disk.</span></span> <span data-ttu-id="1b23c-108">Para obter mais informações, consulte [Preços e cobrança ao usar o Armazenamento Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="1b23c-108">For more information refer to [Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span>
>
>

<span data-ttu-id="1b23c-109">Se desejar usar os dados existentes no disco novamente, você pode reanexá-lo à mesma máquina virtual ou anexá-lo a uma outra máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1b23c-109">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span></span>

## <a name="detach-a-data-disk-using-the-portal"></a><span data-ttu-id="1b23c-110">Desanexar um disco de dados usando o portal</span><span class="sxs-lookup"><span data-stu-id="1b23c-110">Detach a data disk using the portal</span></span>
1. <span data-ttu-id="1b23c-111">No hub do portal, selecione **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="1b23c-111">In the portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="1b23c-112">Selecione a máquina virtual que tem o disco de dados que você deseja desanexar e clique em **Parar** para desalocar a VM.</span><span class="sxs-lookup"><span data-stu-id="1b23c-112">Select the virtual machine that has the data disk you want to detach and click **Stop** to deallocate the VM.</span></span>
3. <span data-ttu-id="1b23c-113">Na folha da máquina virtual, selecione **Discos**.</span><span class="sxs-lookup"><span data-stu-id="1b23c-113">In the virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="1b23c-114">Na parte superior da folha **Discos**, selecione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="1b23c-114">At the top of the **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="1b23c-115">Na folha **Discos**, mais à direita do disco de dados que você deseja desanexar, clique no botão Desanexar ![Imagem do botão Desanexar](./media/detach-disk/detach.png).</span><span class="sxs-lookup"><span data-stu-id="1b23c-115">In the **Disks** blade, to the far right of the data disk that you would like to detach, click the ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="1b23c-116">Depois que o disco for removido, clique em Salvar na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="1b23c-116">After the disk has been removed, click Save on the top of the blade.</span></span>
6. <span data-ttu-id="1b23c-117">Na folha da máquina virtual, clique em **Visão Geral** e, em seguida, clique no botão **Iniciar** na parte superior da folha para reiniciar a VM.</span><span class="sxs-lookup"><span data-stu-id="1b23c-117">In the virtual machine blade, click **Overview** and then click the **Start** button at the top of the blade to restart the VM.</span></span>



<span data-ttu-id="1b23c-118">O disco permanece no armazenamento mas não esteja conectado a uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1b23c-118">The disk remains in storage but is no longer attached to a virtual machine.</span></span>

## <a name="detach-a-data-disk-using-powershell"></a><span data-ttu-id="1b23c-119">Desanexar um disco de dados usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b23c-119">Detach a data disk using PowerShell</span></span>
<span data-ttu-id="1b23c-120">Neste exemplo, o primeiro comando obtém a máquina virtual chamada **MyVM07** no grupo de recursos **RG11** usando o cmdlet Get-AzureRmVM.</span><span class="sxs-lookup"><span data-stu-id="1b23c-120">In this example, the first command gets the virtual machine named **MyVM07** in the **RG11** resource group using the Get-AzureRmVM cmdlet.</span></span> <span data-ttu-id="1b23c-121">O comando armazena a máquina virtual na variável **$VirtualMachine** .</span><span class="sxs-lookup"><span data-stu-id="1b23c-121">The command stores the virtual machine in the **$VirtualMachine** variable.</span></span>

<span data-ttu-id="1b23c-122">O segundo comando remove da máquina virtual o disco de dados denominado DataDisk3.</span><span class="sxs-lookup"><span data-stu-id="1b23c-122">The second command removes the data disk named DataDisk3 from the virtual machine.</span></span>

<span data-ttu-id="1b23c-123">O comando final atualiza o estado da máquina virtual para concluir o processo de remoção do disco de dados.</span><span class="sxs-lookup"><span data-stu-id="1b23c-123">The final command updates the state of the virtual machine to complete the process of removing the data disk.</span></span>

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

<span data-ttu-id="1b23c-124">Para obter mais informações, consulte [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="1b23c-124">For more information, see [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b23c-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1b23c-125">Next steps</span></span>
<span data-ttu-id="1b23c-126">Se você quiser reutilizar o disco de dados, você poderá simplesmente [anexá-lo a outra VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="1b23c-126">If you want to reuse the data disk, you can just [attach it to another VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

