---
title: aaaDetach um disco de dados de uma VM do Windows - Azure | Microsoft Docs
description: "Saiba toodetach um disco de dados de uma máquina virtual no Azure usando o modelo de implantação do Gerenciador de recursos de saudação."
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
ms.openlocfilehash: f3f581d3f33329db2ecb7d25a68bc59af7361aad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-windows-virtual-machine"></a><span data-ttu-id="f7b5b-103">Como toodetach dados de um disco de máquina virtual do Windows</span><span class="sxs-lookup"><span data-stu-id="f7b5b-103">How toodetach a data disk from a Windows virtual machine</span></span>
<span data-ttu-id="f7b5b-104">Quando você não precisa mais um disco de dados é anexado tooa VM, você pode facilmente desanexá-lo.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-104">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="f7b5b-105">Isso remove o disco de saudação da máquina virtual de hello, mas não o remove do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-105">This removes hello disk from hello virtual machine, but doesn't remove it from storage.</span></span>

> [!WARNING]
> <span data-ttu-id="f7b5b-106">Se você desanexar um disco, ele não será excluído automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="f7b5b-107">Se você se inscreveu tooPremium armazenamento, você continuará tooincur encargos de armazenamento de disco de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-107">If you have subscribed tooPremium storage, you will continue tooincur storage charges for hello disk.</span></span> <span data-ttu-id="f7b5b-108">Para obter mais informações, consulte muito[preços e faturamento ao usar o armazenamento Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="f7b5b-108">For more information refer too[Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span>
>
>

<span data-ttu-id="f7b5b-109">Se você quiser toouse Olá dados existentes ao disco Olá novamente, você poderá reanexar-toohello mesma máquina virtual ou outro.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-109">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>

## <a name="detach-a-data-disk-using-hello-portal"></a><span data-ttu-id="f7b5b-110">Desanexar um disco de dados usando o portal de saudação</span><span class="sxs-lookup"><span data-stu-id="f7b5b-110">Detach a data disk using hello portal</span></span>
1. <span data-ttu-id="f7b5b-111">No hub de portal hello, selecione **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-111">In hello portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="f7b5b-112">Selecionar máquina virtual Olá que tenha Olá disco de dados que deseja toodetach e clique **parar** toodeallocate Olá VM.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-112">Select hello virtual machine that has hello data disk you want toodetach and click **Stop** toodeallocate hello VM.</span></span>
3. <span data-ttu-id="f7b5b-113">Na folha de máquina virtual hello, selecione **discos**.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-113">In hello virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="f7b5b-114">Na parte superior de saudação do hello **discos** folha, selecione **editar**.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-114">At hello top of hello **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="f7b5b-115">Em Olá **discos** folha, toohello à direita saudação do disco de dados que deseja toodetach, clique em Olá ![imagem do botão desanexar](./media/detach-disk/detach.png) desanexar botão.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-115">In hello **Disks** blade, toohello far right of hello data disk that you would like toodetach, click hello ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="f7b5b-116">Depois que o disco Olá foi removido, clique em Salvar na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-116">After hello disk has been removed, click Save on hello top of hello blade.</span></span>
6. <span data-ttu-id="f7b5b-117">Na folha de máquina virtual de saudação, clique em **visão geral** e, em seguida, clique em Olá **iniciar** botão na parte superior de saudação do hello toorestart da folha Olá VM.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-117">In hello virtual machine blade, click **Overview** and then click hello **Start** button at hello top of hello blade toorestart hello VM.</span></span>



<span data-ttu-id="f7b5b-118">disco Olá permanece no armazenamento, mas não está mais anexado tooa virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-118">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>

## <a name="detach-a-data-disk-using-powershell"></a><span data-ttu-id="f7b5b-119">Desanexar um disco de dados usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7b5b-119">Detach a data disk using PowerShell</span></span>
<span data-ttu-id="f7b5b-120">Neste exemplo, Olá primeiro comando obtém Olá máquina virtual denominada **MyVM07** em Olá **RG11** usando o cmdlet Get-AzureRmVM de saudação do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-120">In this example, hello first command gets hello virtual machine named **MyVM07** in hello **RG11** resource group using hello Get-AzureRmVM cmdlet.</span></span> <span data-ttu-id="f7b5b-121">Olá comando repositórios Olá máquina virtual no hello **$VirtualMachine** variável.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-121">hello command stores hello virtual machine in hello **$VirtualMachine** variable.</span></span>

<span data-ttu-id="f7b5b-122">comando segundo Olá remove o disco de dados de saudação chamado DataDisk3 da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-122">hello second command removes hello data disk named DataDisk3 from hello virtual machine.</span></span>

<span data-ttu-id="f7b5b-123">comando final Olá atualizará o estado de saudação do processo de saudação do hello máquina virtual toocomplete de remover o disco de dados hello.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-123">hello final command updates hello state of hello virtual machine toocomplete hello process of removing hello data disk.</span></span>

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

<span data-ttu-id="f7b5b-124">Para obter mais informações, consulte [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="f7b5b-124">For more information, see [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7b5b-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f7b5b-125">Next steps</span></span>
<span data-ttu-id="f7b5b-126">Se desejar que o disco de dados tooreuse hello, você pode simplesmente [anexá-lo tooanother VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="f7b5b-126">If you want tooreuse hello data disk, you can just [attach it tooanother VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

