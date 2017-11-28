---
title: aaaAbout discos e VHDs para VMs do Windows do Microsoft Azure | Microsoft Docs
description: "Saiba mais sobre Olá Noções básicas sobre discos e máquinas virtuais de VHDs para Windows no Azure."
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
ms.openlocfilehash: 859e564dc74240bd7c70fec33255b8d071c4acf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a><span data-ttu-id="36058-103">Sobre discos e VHDs para VMs do Windows do Azure</span><span class="sxs-lookup"><span data-stu-id="36058-103">About disks and VHDs for Azure Windows VMs</span></span>
<span data-ttu-id="36058-104">Assim como qualquer outro computador, máquinas virtuais no Azure usam discos como toostore um local de um sistema operacional, aplicativos e dados.</span><span class="sxs-lookup"><span data-stu-id="36058-104">Just like any other computer, virtual machines in Azure use disks as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="36058-105">Todas as máquinas virtuais do Azure têm pelo menos dois discos – um disco do sistema operacional Windows e um disco temporário.</span><span class="sxs-lookup"><span data-stu-id="36058-105">All Azure virtual machines have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="36058-106">disco do sistema operacional Olá é criado a partir de uma imagem e disco do sistema operacional hello e imagem Olá são discos rígidos virtuais (VHDs) armazenados em uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="36058-106">hello operating system disk is created from an image, and both hello operating system disk and hello image are virtual hard disks (VHDs) stored in an Azure storage account.</span></span> <span data-ttu-id="36058-107">Máquinas virtuais também podem ter um ou mais discos de dados que também são armazenados em VHDs.</span><span class="sxs-lookup"><span data-stu-id="36058-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span> 

<span data-ttu-id="36058-108">Neste artigo, nós falar sobre os diferentes usos Olá discos hello e, em seguida, aborde tipos diferentes de saudação de discos, você pode criar e usar.</span><span class="sxs-lookup"><span data-stu-id="36058-108">In this article, we will talk about hello different uses for hello disks, and then discuss hello different types of disks you can create and use.</span></span> <span data-ttu-id="36058-109">Este artigo também está disponível para [máquinas virtuais Linux](storage-about-disks-and-vhds-linux.md).</span><span class="sxs-lookup"><span data-stu-id="36058-109">This article is also available for [Linux virtual machines](storage-about-disks-and-vhds-linux.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a><span data-ttu-id="36058-110">Discos usados por VMs</span><span class="sxs-lookup"><span data-stu-id="36058-110">Disks used by VMs</span></span>

<span data-ttu-id="36058-111">Vamos dar uma olhada em como discos de saudação são usados pelo Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="36058-111">Let's take a look at how hello disks are used by hello VMs.</span></span>

### <a name="operating-system-disk"></a><span data-ttu-id="36058-112">Disco do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="36058-112">Operating system disk</span></span>
<span data-ttu-id="36058-113">Cada máquina virtual tem um disco de sistema operacional anexado.</span><span class="sxs-lookup"><span data-stu-id="36058-113">Every virtual machine has one attached operating system disk.</span></span> <span data-ttu-id="36058-114">Ele foi registrado como uma unidade SATA e rotulado como unidade c: de saudação por padrão.</span><span class="sxs-lookup"><span data-stu-id="36058-114">It's registered as a SATA drive and labeled as hello C: drive by default.</span></span> <span data-ttu-id="36058-115">Este disco tem uma capacidade máxima de 2048 gigabytes (GB).</span><span class="sxs-lookup"><span data-stu-id="36058-115">This disk has a maximum capacity of 2048 gigabytes (GB).</span></span> 

### <a name="temporary-disk"></a><span data-ttu-id="36058-116">Disco temporário</span><span class="sxs-lookup"><span data-stu-id="36058-116">Temporary disk</span></span>
<span data-ttu-id="36058-117">Cada VM contém um disco temporário.</span><span class="sxs-lookup"><span data-stu-id="36058-117">Each VM contains a temporary disk.</span></span> <span data-ttu-id="36058-118">disco temporário Olá fornece armazenamento de curto prazo para aplicativos e processos e dados de repositório tooonly desejado, como arquivos de paginação ou de permuta.</span><span class="sxs-lookup"><span data-stu-id="36058-118">hello temporary disk provides short-term storage for applications and processes and is intended tooonly store data such as page or swap files.</span></span> <span data-ttu-id="36058-119">Dados em disco temporário Olá podem ser perdidos durante uma [evento de manutenção](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) ou quando você [reimplantar uma VM](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="36058-119">Data on hello temporary disk may be lost during a [maintenance event](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) or when you [redeploy a VM](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="36058-120">Durante uma reinicialização padrão do hello VM, devem persistir os dados de saudação na unidade temporária hello.</span><span class="sxs-lookup"><span data-stu-id="36058-120">During a standard reboot of hello VM, hello data on hello temporary drive should persist.</span></span>

<span data-ttu-id="36058-121">disco temporário Olá é rotulado como Olá unidade d: por padrão e ele é usado para armazenar pagefile.sys.</span><span class="sxs-lookup"><span data-stu-id="36058-121">hello temporary disk is labeled as hello D: drive by default and it used for storing pagefile.sys.</span></span> <span data-ttu-id="36058-122">tooremap essa letra de unidade diferente de tooa de disco, consulte [alterar a letra da unidade saudação do disco temporário do Windows hello](../virtual-machines/windows/change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="36058-122">tooremap this disk tooa different drive letter, see [Change hello drive letter of hello Windows temporary disk](../virtual-machines/windows/change-drive-letter.md).</span></span> <span data-ttu-id="36058-123">tamanho de saudação do disco temporário Olá varia de acordo com base no tamanho de saudação da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="36058-123">hello size of hello temporary disk varies, based on hello size of hello virtual machine.</span></span> <span data-ttu-id="36058-124">Para obter mais informações, consulte [Tamanhos de máquinas virtuais do Windows](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="36058-124">For more information, see [Sizes for Windows virtual machines](../virtual-machines/windows/sizes.md).</span></span>

<span data-ttu-id="36058-125">Para obter mais informações sobre como o Azure usa o disco temporário hello, consulte [Noções básicas sobre unidades temporárias de saudação em máquinas virtuais do Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="36058-125">For more information on how Azure uses hello temporary disk, see [Understanding hello temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>


### <a name="data-disk"></a><span data-ttu-id="36058-126">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="36058-126">Data disk</span></span>
<span data-ttu-id="36058-127">Um disco de dados é um VHD anexado tooa máquina virtual toostore aplicativo dados ou outros dados que você precisa tookeep.</span><span class="sxs-lookup"><span data-stu-id="36058-127">A data disk is a VHD that's attached tooa virtual machine toostore application data, or other data you need tookeep.</span></span> <span data-ttu-id="36058-128">Discos de dados são registrados como unidades SCSI e rotulados com a letra que você escolher.</span><span class="sxs-lookup"><span data-stu-id="36058-128">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span></span> <span data-ttu-id="36058-129">Cada disco de dados tem uma capacidade máxima de 4095 GB.</span><span class="sxs-lookup"><span data-stu-id="36058-129">Each data disk has a maximum capacity of 4095 GB.</span></span> <span data-ttu-id="36058-130">tamanho da máquina virtual de saudação Hello determina quantos discos de dados, você pode anexar tooit e hello tipo de armazenamento que você pode usar discos de saudação toohost.</span><span class="sxs-lookup"><span data-stu-id="36058-130">hello size of hello virtual machine determines how many data disks you can attach tooit and hello type of storage you can use toohost hello disks.</span></span>

> [!NOTE]
> <span data-ttu-id="36058-131">Para obter mais informações sobre as capacidades de máquinas virtuais, veja [Tamanhos das máquinas virtuais do Windows](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="36058-131">For more information about virtual machines capacities, see [Sizes for Windows virtual machines](../virtual-machines/windows/sizes.md).</span></span>
> 

<span data-ttu-id="36058-132">Quando você cria uma máquina virtual por meio de uma imagem, o Azure cria um disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="36058-132">Azure creates an operating system disk when you create a virtual machine from an image.</span></span> <span data-ttu-id="36058-133">Se você usar uma imagem que inclui discos de dados, Azure também cria Olá discos de dados quando ele cria a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="36058-133">If you use an image that includes data disks, Azure also creates hello data disks when it creates hello virtual machine.</span></span> <span data-ttu-id="36058-134">Caso contrário, adicione discos de dados depois de criar a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="36058-134">Otherwise, you add data disks after you create hello virtual machine.</span></span>

<span data-ttu-id="36058-135">Você pode adicionar dados discos tooa virtuais máquina a qualquer momento, por **anexando** Olá disco toohello VM.</span><span class="sxs-lookup"><span data-stu-id="36058-135">You can add data disks tooa virtual machine at any time, by **attaching** hello disk toohello virtual machine.</span></span> <span data-ttu-id="36058-136">Você pode usar um VHD que você carregou ou copiou tooyour conta de armazenamento ou um que o Azure cria para você.</span><span class="sxs-lookup"><span data-stu-id="36058-136">You can use a VHD that you've uploaded or copied tooyour storage account, or one that Azure creates for you.</span></span> <span data-ttu-id="36058-137">Anexar um disco de dados associa arquivo VHD Olá Olá VM colocando uma concessão em Olá VHD não pode ser excluído do armazenamento enquanto ele ainda está conectado.</span><span class="sxs-lookup"><span data-stu-id="36058-137">Attaching a data disk associates hello VHD file with hello VM by placing a 'lease' on hello VHD so it can't be deleted from storage while it's still attached.</span></span>


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a><span data-ttu-id="36058-138">Uma última recomendação: use o TRIM com discos padrão não gerenciados</span><span class="sxs-lookup"><span data-stu-id="36058-138">One last recommendation: Use TRIM with unmanaged standard disks</span></span> 

<span data-ttu-id="36058-139">Se você usar discos padrão não gerenciados (HDD), será necessário habilitar o TRIM.</span><span class="sxs-lookup"><span data-stu-id="36058-139">If you use unmanaged standard disks (HDD), you should enable TRIM.</span></span> <span data-ttu-id="36058-140">TRIM descarta blocos não usados no disco Olá para que você é cobrado somente para o armazenamento que você está usando.</span><span class="sxs-lookup"><span data-stu-id="36058-140">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="36058-141">Isso poderá representar uma economia dos custos se você criar arquivos grandes e, em seguida, excluí-los.</span><span class="sxs-lookup"><span data-stu-id="36058-141">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="36058-142">Você pode executar essa configuração de CORTE de saudação do comando toocheck.</span><span class="sxs-lookup"><span data-stu-id="36058-142">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="36058-143">Abra um prompt de comando na sua VM do Windows e digite:</span><span class="sxs-lookup"><span data-stu-id="36058-143">Open a command prompt on your Windows VM and type:</span></span>


```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="36058-144">Se o comando Olá retorna 0, TRIM está habilitada corretamente.</span><span class="sxs-lookup"><span data-stu-id="36058-144">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="36058-145">Se ele retorna 1, execute Olá comando tooenable TRIM a seguir:</span><span class="sxs-lookup"><span data-stu-id="36058-145">If it returns 1, run hello following command tooenable TRIM:</span></span>

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> <span data-ttu-id="36058-146">Observação: O suporte de corte começa com o Windows Server 2012 / Windows 8 e posterior, consulte consulte [nova API permite que aplicativos da mídia de toostorage dicas toosend "CORTE e desmapeamento"](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span><span class="sxs-lookup"><span data-stu-id="36058-146">Note: Trim support starts with Windows Server 2012 / Windows 8 and above, see see [New API allows apps toosend "TRIM and Unmap" hints toostorage media](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span></span>
> 

<!-- Might want toomatch next-steps from overview of managed disks -->
## <a name="next-steps"></a><span data-ttu-id="36058-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="36058-147">Next steps</span></span>
* <span data-ttu-id="36058-148">[Anexar um disco](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd de armazenamento adicional para sua VM.</span><span class="sxs-lookup"><span data-stu-id="36058-148">[Attach a disk](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd additional storage for your VM.</span></span>
* <span data-ttu-id="36058-149">[Alterar a letra da unidade saudação do disco temporário do Windows hello](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) para seu aplicativo pode usar a unidade d: de saudação para dados.</span><span class="sxs-lookup"><span data-stu-id="36058-149">[Change hello drive letter of hello Windows temporary disk](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) so your application can use hello D: drive for data.</span></span>

