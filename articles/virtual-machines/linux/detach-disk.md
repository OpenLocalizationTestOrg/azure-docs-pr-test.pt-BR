---
title: aaaDetach um disco de dados de uma VM do Linux - Azure | Microsoft Docs
description: "Saiba toodetach um disco de dados de uma máquina virtual no Azure usando a CLI 2.0 ou hello portal do Azure."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: azurecli
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 1c6145fc97f13179457225e93e0fb7adc261a65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-linux-virtual-machine"></a><span data-ttu-id="10490-103">Como toodetach dados de um disco de uma máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="10490-103">How toodetach a data disk from a Linux virtual machine</span></span>

<span data-ttu-id="10490-104">Quando você não precisa mais um disco de dados é anexado tooa VM, você pode facilmente desanexá-lo.</span><span class="sxs-lookup"><span data-stu-id="10490-104">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="10490-105">Isso remove o disco de saudação da máquina virtual de hello, mas não o remove do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="10490-105">This removes hello disk from hello virtual machine, but doesn't remove it from storage.</span></span> 

> [!WARNING]
> <span data-ttu-id="10490-106">Se você desanexar um disco, ele não será excluído automaticamente.</span><span class="sxs-lookup"><span data-stu-id="10490-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="10490-107">Se você se inscreveu tooPremium armazenamento, você continuará tooincur encargos de armazenamento de disco de saudação.</span><span class="sxs-lookup"><span data-stu-id="10490-107">If you have subscribed tooPremium storage, you will continue tooincur storage charges for hello disk.</span></span> <span data-ttu-id="10490-108">Para obter mais informações, consulte muito[preços e faturamento ao usar o armazenamento Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="10490-108">For more information refer too[Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span> 
> 
> 

<span data-ttu-id="10490-109">Se você quiser toouse Olá dados existentes ao disco Olá novamente, você poderá reanexar-toohello mesma máquina virtual ou outro.</span><span class="sxs-lookup"><span data-stu-id="10490-109">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>  

## <a name="detach-a-data-disk-using-cli-20"></a><span data-ttu-id="10490-110">Desanexar um disco de dados usando a CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="10490-110">Detach a data disk using CLI 2.0</span></span>

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

<span data-ttu-id="10490-111">disco Olá permanece no armazenamento, mas não está mais anexado tooa virtual machine.</span><span class="sxs-lookup"><span data-stu-id="10490-111">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>


## <a name="detach-a-data-disk-using-hello-portal"></a><span data-ttu-id="10490-112">Desanexar um disco de dados usando o portal de saudação</span><span class="sxs-lookup"><span data-stu-id="10490-112">Detach a data disk using hello portal</span></span>
1. <span data-ttu-id="10490-113">No hub de portal hello, selecione **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="10490-113">In hello portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="10490-114">Selecionar máquina virtual Olá que tenha Olá disco de dados que deseja toodetach e clique **parar** toodeallocate Olá VM.</span><span class="sxs-lookup"><span data-stu-id="10490-114">Select hello virtual machine that has hello data disk you want toodetach and click **Stop** toodeallocate hello VM.</span></span>
3. <span data-ttu-id="10490-115">Na folha de máquina virtual hello, selecione **discos**.</span><span class="sxs-lookup"><span data-stu-id="10490-115">In hello virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="10490-116">Na parte superior de saudação do hello **discos** folha, selecione **editar**.</span><span class="sxs-lookup"><span data-stu-id="10490-116">At hello top of hello **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="10490-117">Em Olá **discos** folha, toohello à direita saudação do disco de dados que deseja toodetach, clique em Olá ![imagem do botão desanexar](./media/detach-disk/detach.png) desanexar botão.</span><span class="sxs-lookup"><span data-stu-id="10490-117">In hello **Disks** blade, toohello far right of hello data disk that you would like toodetach, click hello ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="10490-118">Depois que o disco Olá foi removido, clique em Salvar na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="10490-118">After hello disk has been removed, click Save on hello top of hello blade.</span></span>
6. <span data-ttu-id="10490-119">Na folha de máquina virtual de saudação, clique em **visão geral** e, em seguida, clique em Olá **iniciar** botão na parte superior de saudação do hello toorestart da folha Olá VM.</span><span class="sxs-lookup"><span data-stu-id="10490-119">In hello virtual machine blade, click **Overview** and then click hello **Start** button at hello top of hello blade toorestart hello VM.</span></span>

<span data-ttu-id="10490-120">disco Olá permanece no armazenamento, mas não está mais anexado tooa virtual machine.</span><span class="sxs-lookup"><span data-stu-id="10490-120">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>








## <a name="next-steps"></a><span data-ttu-id="10490-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="10490-121">Next steps</span></span>
<span data-ttu-id="10490-122">Se desejar que o disco de dados tooreuse hello, você pode simplesmente [anexá-lo tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="10490-122">If you want tooreuse hello data disk, you can just [attach it tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

