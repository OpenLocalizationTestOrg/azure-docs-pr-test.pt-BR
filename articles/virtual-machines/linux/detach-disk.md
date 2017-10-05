---
title: "Desanexar um disco de dados de uma VM Linux – Azure | Microsoft Docs"
description: "Saiba como desanexar um disco de dados de uma máquina virtual no Azure usando a CLI 2.0 ou o portal do Azure."
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
ms.openlocfilehash: 3f29547e1da6028b1e4b91d9e29fd3bcdfe08d50
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-detach-a-data-disk-from-a-linux-virtual-machine"></a><span data-ttu-id="673ee-103">Como desanexar um disco de dados de uma máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="673ee-103">How to detach a data disk from a Linux virtual machine</span></span>

<span data-ttu-id="673ee-104">Quando não precisar mais de um disco de dados conectado a uma máquina virtual, você poderá desanexá-lo facilmente.</span><span class="sxs-lookup"><span data-stu-id="673ee-104">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span></span> <span data-ttu-id="673ee-105">Essa ação remove o disco da máquina virtual, mas não o remove do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="673ee-105">This removes the disk from the virtual machine, but doesn't remove it from storage.</span></span> 

> [!WARNING]
> <span data-ttu-id="673ee-106">Se você desanexar um disco, ele não será excluído automaticamente.</span><span class="sxs-lookup"><span data-stu-id="673ee-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="673ee-107">Se você se inscreveu para o armazenamento Premium, você continuará incorrendo em encargos de armazenamento para o disco.</span><span class="sxs-lookup"><span data-stu-id="673ee-107">If you have subscribed to Premium storage, you will continue to incur storage charges for the disk.</span></span> <span data-ttu-id="673ee-108">Para obter mais informações, consulte [Preços e cobrança ao usar o Armazenamento Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="673ee-108">For more information refer to [Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span> 
> 
> 

<span data-ttu-id="673ee-109">Se desejar usar os dados existentes no disco novamente, você pode reanexá-lo à mesma máquina virtual ou anexá-lo a uma outra máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="673ee-109">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span></span>  

## <a name="detach-a-data-disk-using-cli-20"></a><span data-ttu-id="673ee-110">Desanexar um disco de dados usando a CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="673ee-110">Detach a data disk using CLI 2.0</span></span>

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

<span data-ttu-id="673ee-111">O disco permanece no armazenamento mas não esteja conectado a uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="673ee-111">The disk remains in storage but is no longer attached to a virtual machine.</span></span>


## <a name="detach-a-data-disk-using-the-portal"></a><span data-ttu-id="673ee-112">Desanexar um disco de dados usando o portal</span><span class="sxs-lookup"><span data-stu-id="673ee-112">Detach a data disk using the portal</span></span>
1. <span data-ttu-id="673ee-113">No hub do portal, selecione **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="673ee-113">In the portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="673ee-114">Selecione a máquina virtual que tem o disco de dados que você deseja desanexar e clique em **Parar** para desalocar a VM.</span><span class="sxs-lookup"><span data-stu-id="673ee-114">Select the virtual machine that has the data disk you want to detach and click **Stop** to deallocate the VM.</span></span>
3. <span data-ttu-id="673ee-115">Na folha da máquina virtual, selecione **Discos**.</span><span class="sxs-lookup"><span data-stu-id="673ee-115">In the virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="673ee-116">Na parte superior da folha **Discos**, selecione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="673ee-116">At the top of the **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="673ee-117">Na folha **Discos**, mais à direita do disco de dados que você deseja desanexar, clique no botão Desanexar ![Imagem do botão Desanexar](./media/detach-disk/detach.png).</span><span class="sxs-lookup"><span data-stu-id="673ee-117">In the **Disks** blade, to the far right of the data disk that you would like to detach, click the ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="673ee-118">Depois que o disco for removido, clique em Salvar na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="673ee-118">After the disk has been removed, click Save on the top of the blade.</span></span>
6. <span data-ttu-id="673ee-119">Na folha da máquina virtual, clique em **Visão Geral** e, em seguida, clique no botão **Iniciar** na parte superior da folha para reiniciar a VM.</span><span class="sxs-lookup"><span data-stu-id="673ee-119">In the virtual machine blade, click **Overview** and then click the **Start** button at the top of the blade to restart the VM.</span></span>

<span data-ttu-id="673ee-120">O disco permanece no armazenamento mas não esteja conectado a uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="673ee-120">The disk remains in storage but is no longer attached to a virtual machine.</span></span>








## <a name="next-steps"></a><span data-ttu-id="673ee-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="673ee-121">Next steps</span></span>
<span data-ttu-id="673ee-122">Se deseja reutilizar o disco de dados, basta [anexá-lo a outra VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="673ee-122">If you want to reuse the data disk, you can just [attach it to another VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

