---
title: Sobre discos e VHDs para VMs do Windows do Microsoft Azure | Microsoft Docs
description: "Conheça o básico sobre discos e VHDs para máquinas virtuais do Windows no Azure."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0142c64d-5e8c-4d62-aa6f-06d6261f485a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: c194ca0f31d077ffa998764b9d63b12dd596ac32
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a><span data-ttu-id="28af3-103">Sobre discos e VHDs para VMs do Windows do Azure</span><span class="sxs-lookup"><span data-stu-id="28af3-103">About disks and VHDs for Azure Windows VMs</span></span>
<span data-ttu-id="28af3-104">Assim como qualquer outro computador, as máquinas virtuais do Azure usam os discos como locais onde armazenar um sistema operacional, aplicativos e dados.</span><span class="sxs-lookup"><span data-stu-id="28af3-104">Just like any other computer, virtual machines in Azure use disks as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="28af3-105">Todas as máquinas virtuais do Azure têm pelo menos dois discos – um disco do sistema operacional Windows e um disco temporário.</span><span class="sxs-lookup"><span data-stu-id="28af3-105">All Azure virtual machines have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="28af3-106">O disco do sistema operacional é criado por meio de uma imagem, e o disco do sistema operacional e a imagem são VHDs (discos rígidos virtuais) armazenados em uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="28af3-106">The operating system disk is created from an image, and both the operating system disk and the image are virtual hard disks (VHDs) stored in an Azure storage account.</span></span> <span data-ttu-id="28af3-107">Máquinas virtuais também podem ter um ou mais discos de dados que também são armazenados em VHDs.</span><span class="sxs-lookup"><span data-stu-id="28af3-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span> 

<span data-ttu-id="28af3-108">Neste artigo, vamos falar sobre os diferentes usos dos discos e discutir os diferentes tipos de discos que você pode criar e usar.</span><span class="sxs-lookup"><span data-stu-id="28af3-108">In this article, we will talk about the different uses for the disks, and then discuss the different types of disks you can create and use.</span></span> <span data-ttu-id="28af3-109">Este artigo também está disponível para [máquinas virtuais Linux](about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="28af3-109">This article is also available for [Linux virtual machines](about-disks-and-vhds.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a><span data-ttu-id="28af3-110">Discos usados por VMs</span><span class="sxs-lookup"><span data-stu-id="28af3-110">Disks used by VMs</span></span>

<span data-ttu-id="28af3-111">Vamos dar uma olhada em como os discos são usados pelas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="28af3-111">Let's take a look at how the disks are used by the VMs.</span></span>

### <a name="operating-system-disk"></a><span data-ttu-id="28af3-112">Disco do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="28af3-112">Operating system disk</span></span>
<span data-ttu-id="28af3-113">Cada máquina virtual tem um disco de sistema operacional anexado.</span><span class="sxs-lookup"><span data-stu-id="28af3-113">Every virtual machine has one attached operating system disk.</span></span> <span data-ttu-id="28af3-114">Ele é registrado como uma unidade SATA e rotulado como a unidade C: por padrão.</span><span class="sxs-lookup"><span data-stu-id="28af3-114">It's registered as a SATA drive and labeled as the C: drive by default.</span></span> <span data-ttu-id="28af3-115">Este disco tem uma capacidade máxima de 2048 gigabytes (GB).</span><span class="sxs-lookup"><span data-stu-id="28af3-115">This disk has a maximum capacity of 2048 gigabytes (GB).</span></span> 

### <a name="temporary-disk"></a><span data-ttu-id="28af3-116">Disco temporário</span><span class="sxs-lookup"><span data-stu-id="28af3-116">Temporary disk</span></span>
<span data-ttu-id="28af3-117">Cada VM contém um disco temporário.</span><span class="sxs-lookup"><span data-stu-id="28af3-117">Each VM contains a temporary disk.</span></span> <span data-ttu-id="28af3-118">O disco temporário fornece armazenamento de curto prazo para aplicativos e processos e destina-se apenas a armazenar dados, como arquivos de paginação ou de permuta.</span><span class="sxs-lookup"><span data-stu-id="28af3-118">The temporary disk provides short-term storage for applications and processes and is intended to only store data such as page or swap files.</span></span> <span data-ttu-id="28af3-119">Os dados no disco temporário podem ser perdidos durante um [evento de manutenção](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) ou durante a [reimplantação de uma VM](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="28af3-119">Data on the temporary disk may be lost during a [maintenance event](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) or when you [redeploy a VM](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="28af3-120">Durante a reinicialização padrão da VM, os dados na unidade temporária devem persistir.</span><span class="sxs-lookup"><span data-stu-id="28af3-120">During a standard reboot of the VM, the data on the temporary drive should persist.</span></span>

<span data-ttu-id="28af3-121">O disco temporário é rotulado como a unidade D: por padrão e é usado para armazenar o arquivo pagefile.sys.</span><span class="sxs-lookup"><span data-stu-id="28af3-121">The temporary disk is labeled as the D: drive by default and it used for storing pagefile.sys.</span></span> <span data-ttu-id="28af3-122">Para remapear este disco para uma letra de unidade diferente, consulte [Alterar a letra da unidade de disco temporário do Windows](change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="28af3-122">To remap this disk to a different drive letter, see [Change the drive letter of the Windows temporary disk](change-drive-letter.md).</span></span> <span data-ttu-id="28af3-123">O tamanho do disco temporário varia com base no tamanho da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="28af3-123">The size of the temporary disk varies, based on the size of the virtual machine.</span></span> <span data-ttu-id="28af3-124">Para obter mais informações, consulte [Tamanhos de máquinas virtuais do Windows](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="28af3-124">For more information, see [Sizes for Windows virtual machines](sizes.md).</span></span>

<span data-ttu-id="28af3-125">Para obter mais informações sobre como o Azure usa o disco temporário, consulte [Noções básicas sobre a unidade temporária nas Máquinas Virtuais do Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="28af3-125">For more information on how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>


### <a name="data-disk"></a><span data-ttu-id="28af3-126">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="28af3-126">Data disk</span></span>
<span data-ttu-id="28af3-127">Um disco de dados é um VHD anexado a uma máquina virtual para armazenar dados de aplicativos ou outros dados que precisam ser mantidos.</span><span class="sxs-lookup"><span data-stu-id="28af3-127">A data disk is a VHD that's attached to a virtual machine to store application data, or other data you need to keep.</span></span> <span data-ttu-id="28af3-128">Discos de dados são registrados como unidades SCSI e rotulados com a letra que você escolher.</span><span class="sxs-lookup"><span data-stu-id="28af3-128">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span></span> <span data-ttu-id="28af3-129">Cada disco de dados tem uma capacidade máxima de 4095 GB.</span><span class="sxs-lookup"><span data-stu-id="28af3-129">Each data disk has a maximum capacity of 4095 GB.</span></span> <span data-ttu-id="28af3-130">O tamanho da máquina virtual determina quantos discos de dados você pode anexar a ele e o tipo de armazenamento que pode usar para hospedar os discos.</span><span class="sxs-lookup"><span data-stu-id="28af3-130">The size of the virtual machine determines how many data disks you can attach to it and the type of storage you can use to host the disks.</span></span>

> [!NOTE]
> <span data-ttu-id="28af3-131">Para obter mais informações sobre as capacidades de máquinas virtuais, veja [Tamanhos das máquinas virtuais do Windows](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="28af3-131">For more information about virtual machines capacities, see [Sizes for Windows virtual machines](sizes.md).</span></span>
> 

<span data-ttu-id="28af3-132">Quando você cria uma máquina virtual por meio de uma imagem, o Azure cria um disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="28af3-132">Azure creates an operating system disk when you create a virtual machine from an image.</span></span> <span data-ttu-id="28af3-133">Se você usar uma imagem que inclui discos de dados, o Azure também cria os discos de dados quando cria a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="28af3-133">If you use an image that includes data disks, Azure also creates the data disks when it creates the virtual machine.</span></span> <span data-ttu-id="28af3-134">Caso contrário, adicione discos de dados após criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="28af3-134">Otherwise, you add data disks after you create the virtual machine.</span></span>

<span data-ttu-id="28af3-135">Você pode adicionar discos de dados a uma máquina virtual a qualquer momento **anexando** o disco à máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="28af3-135">You can add data disks to a virtual machine at any time, by **attaching** the disk to the virtual machine.</span></span> <span data-ttu-id="28af3-136">Você pode usar um VHD carregado ou copiado para sua conta de armazenamento ou um criado pelo Azure para você.</span><span class="sxs-lookup"><span data-stu-id="28af3-136">You can use a VHD that you've uploaded or copied to your storage account, or one that Azure creates for you.</span></span> <span data-ttu-id="28af3-137">A anexação de um disco de dados associa o arquivo VHD à VM fazendo uma “concessão” ao VHD, de forma que ele não possa ser excluído do armazenamento enquanto estiver anexado.</span><span class="sxs-lookup"><span data-stu-id="28af3-137">Attaching a data disk associates the VHD file with the VM by placing a 'lease' on the VHD so it can't be deleted from storage while it's still attached.</span></span>


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a><span data-ttu-id="28af3-138">Uma última recomendação: use o TRIM com discos padrão não gerenciados</span><span class="sxs-lookup"><span data-stu-id="28af3-138">One last recommendation: Use TRIM with unmanaged standard disks</span></span> 

<span data-ttu-id="28af3-139">Se você usar discos padrão não gerenciados (HDD), será necessário habilitar o TRIM.</span><span class="sxs-lookup"><span data-stu-id="28af3-139">If you use unmanaged standard disks (HDD), you should enable TRIM.</span></span> <span data-ttu-id="28af3-140">O TRIM descarta os blocos não usados do disco para que você seja cobrado apenas pelo armazenamento que está efetivamente sendo usado.</span><span class="sxs-lookup"><span data-stu-id="28af3-140">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="28af3-141">Isso poderá representar uma economia dos custos se você criar arquivos grandes e, em seguida, excluí-los.</span><span class="sxs-lookup"><span data-stu-id="28af3-141">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="28af3-142">Você pode executar esse comando para verificar a configuração de TRIM.</span><span class="sxs-lookup"><span data-stu-id="28af3-142">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="28af3-143">Abra um prompt de comando na sua VM do Windows e digite:</span><span class="sxs-lookup"><span data-stu-id="28af3-143">Open a command prompt on your Windows VM and type:</span></span>


```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="28af3-144">Se o comando retornar 0, o TRIM estará habilitado corretamente.</span><span class="sxs-lookup"><span data-stu-id="28af3-144">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="28af3-145">Se ele retornar 1, execute o seguinte comando para habilitar o TRIM:</span><span class="sxs-lookup"><span data-stu-id="28af3-145">If it returns 1, run the following command to enable TRIM:</span></span>

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> <span data-ttu-id="28af3-146">Observação: O suporte de corte começa com o Windows Server 2012 / Windows 8 e posterior, consulte [Nova API permite que aplicativos enviem "CORTE e desmapeamento" dicas para mídia de armazenamento](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span><span class="sxs-lookup"><span data-stu-id="28af3-146">Note: Trim support starts with Windows Server 2012 / Windows 8 and above, see see [New API allows apps to send "TRIM and Unmap" hints to storage media](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span></span>
> 

<!-- Might want to match next-steps from overview of managed disks -->
## <a name="next-steps"></a><span data-ttu-id="28af3-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="28af3-147">Next steps</span></span>
* <span data-ttu-id="28af3-148">[Anexar um disco](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para adicionar mais armazenamento à sua VM.</span><span class="sxs-lookup"><span data-stu-id="28af3-148">[Attach a disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to add additional storage for your VM.</span></span>
* <span data-ttu-id="28af3-149">[Altere a letra da unidade do disco temporário do Windows](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) para que seu aplicativo possa usar a unidade D: para dados.</span><span class="sxs-lookup"><span data-stu-id="28af3-149">[Change the drive letter of the Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) so your application can use the D: drive for data.</span></span>

