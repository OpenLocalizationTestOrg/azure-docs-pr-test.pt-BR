---
title: "aaaExpand de discos rígidos virtuais em uma VM do Linux no Azure | Microsoft Docs"
description: "Saiba como tooexpand de discos rígidos virtuais em uma VM do Linux com hello 2.0 do CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 7c09a682cb4322c027e57667640e8f1f8e6612f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a><span data-ttu-id="8e050-103">Como tooexpand de discos rígidos virtuais em uma VM do Linux com hello CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8e050-103">How tooexpand virtual hard disks on a Linux VM with hello Azure CLI</span></span>
<span data-ttu-id="8e050-104">tamanho de disco rígido virtual saudação padrão para o sistema operacional de saudação (SO) normalmente é 30 GB em uma máquina virtual do Linux (VM) no Azure.</span><span class="sxs-lookup"><span data-stu-id="8e050-104">hello default virtual hard disk size for hello operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="8e050-105">Você pode [adicionar discos de dados](add-disk.md) tooprovide para espaço de armazenamento adicional, mas você também poderá tooexpand um disco de dados existente.</span><span class="sxs-lookup"><span data-stu-id="8e050-105">You can [add data disks](add-disk.md) tooprovide for additional storage space, but you may also wish tooexpand an existing data disk.</span></span> <span data-ttu-id="8e050-106">Este artigo fornece detalhes sobre como tooexpand discos gerenciado para uma VM do Linux com hello 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e050-106">This article details how tooexpand managed disks for a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="8e050-107">Você também pode expandir o disco do sistema operacional não gerenciado de saudação com hello [Azure CLI 1.0](expand-disks-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8e050-107">You can also expand hello unmanaged OS disk with hello [Azure CLI 1.0](expand-disks-nodejs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="8e050-108">Certifique-se sempre de fazer backup dos dados antes de realizar operações de redimensionamento do disco.</span><span class="sxs-lookup"><span data-stu-id="8e050-108">Always make sure that you back up your data before you perform disk resize operations.</span></span> <span data-ttu-id="8e050-109">Para saber mais, confira [Fazer backup de máquinas virtuais do Linux no Azure](tutorial-backup-vms.md).</span><span class="sxs-lookup"><span data-stu-id="8e050-109">For more information, see [Back up Linux VMs in Azure](tutorial-backup-vms.md).</span></span>

## <a name="expand-disk"></a><span data-ttu-id="8e050-110">Expandir disco</span><span class="sxs-lookup"><span data-stu-id="8e050-110">Expand disk</span></span>
<span data-ttu-id="8e050-111">Certifique-se de que você tenha mais recente Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="8e050-111">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="8e050-112">Este artigo requer uma VM existente no Azure com, pelo menos, um disco de dados anexado e preparado.</span><span class="sxs-lookup"><span data-stu-id="8e050-112">This article requires an existing VM in Azure with at least one data disk attached and prepared.</span></span> <span data-ttu-id="8e050-113">Caso ainda não tenha uma VM que possa ser usada, confira [Criar e preparar uma VM com discos de dados](tutorial-manage-disks.md#create-and-attach-disks).</span><span class="sxs-lookup"><span data-stu-id="8e050-113">If you do not already have a VM that you can use, see [Create and prepare a VM with data disks](tutorial-manage-disks.md#create-and-attach-disks).</span></span>

<span data-ttu-id="8e050-114">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="8e050-114">In hello following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8e050-115">Os nomes de parâmetro de exemplo incluem *myResourceGroup* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="8e050-115">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

1. <span data-ttu-id="8e050-116">Não é possível executar operações em discos rígidos virtuais com hello VM em execução.</span><span class="sxs-lookup"><span data-stu-id="8e050-116">Operations on virtual hard disks cannot be performed with hello VM running.</span></span> <span data-ttu-id="8e050-117">Desaloque a VM com [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="8e050-117">Deallocate your VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="8e050-118">exemplo a seguir Hello desaloca Olá VM denominada *myVM* no grupo de recursos de saudação denominado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="8e050-118">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="8e050-119">`az vm stop`não liberar recursos de computação de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e050-119">`az vm stop` does not release hello compute resources.</span></span> <span data-ttu-id="8e050-120">toorelease recursos de computação, use `az vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="8e050-120">toorelease compute resources, use `az vm deallocate`.</span></span> <span data-ttu-id="8e050-121">Olá VM deve ser desalocada tooexpand saudação do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="8e050-121">hello VM must be deallocated tooexpand hello virtual hard disk.</span></span>

2. <span data-ttu-id="8e050-122">Veja uma lista de discos gerenciados em um grupo de recursos com [az disk list](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="8e050-122">View a list of managed disks in a resource group with [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="8e050-123">Olá exemplo a seguir exibe uma lista de discos gerenciados no grupo de recursos de saudação denominado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="8e050-123">hello following example displays a list of managed disks in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    <span data-ttu-id="8e050-124">Expandir disco necessária de saudação com [atualização de disco az](/cli/azure/disk#update).</span><span class="sxs-lookup"><span data-stu-id="8e050-124">Expand hello required disk with [az disk update](/cli/azure/disk#update).</span></span> <span data-ttu-id="8e050-125">exemplo a seguir Hello expande chamado de disco gerenciado do hello *myDataDisk* toobe *200*Gb de tamanho:</span><span class="sxs-lookup"><span data-stu-id="8e050-125">hello following example expands hello managed disk named *myDataDisk* toobe *200*Gb in size:</span></span>

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > <span data-ttu-id="8e050-126">Quando você expande um disco gerenciado, o tamanho de Olá atualizado é mapeada toohello mais próximo do tamanho de disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="8e050-126">When you expand a managed disk, hello updated size is mapped toohello nearest managed disk size.</span></span> <span data-ttu-id="8e050-127">Para uma tabela de tamanhos de disco gerenciado disponível hello e camadas, consulte [gerenciados discos visão geral do Azure - preços e faturamento](../windows/managed-disks-overview.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="8e050-127">For a table of hello available managed disk sizes and tiers, see [Azure Managed Disks Overview - Pricing and Billing](../windows/managed-disks-overview.md#pricing-and-billing).</span></span>

3. <span data-ttu-id="8e050-128">Inicie a VM com [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="8e050-128">Start your VM with [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="8e050-129">Olá inicia de exemplo a seguir Olá VM denominada *myVM* no grupo de recursos de saudação denominado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="8e050-129">hello following example starts hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="8e050-130">SSH tooyour VM com as credenciais apropriadas hello.</span><span class="sxs-lookup"><span data-stu-id="8e050-130">SSH tooyour VM with hello appropriate credentials.</span></span> <span data-ttu-id="8e050-131">Você pode obter o endereço IP público de saudação da VM com [Mostrar de vm az](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="8e050-131">You can obtain hello public IP address of your VM with [az vm show](/cli/azure/vm#show):</span></span>

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. <span data-ttu-id="8e050-132">Olá toouse expandido em disco, é necessário filesystem e partição do tooexpand Olá subjacente.</span><span class="sxs-lookup"><span data-stu-id="8e050-132">toouse hello expanded disk, you need tooexpand hello underlying partition and filesystem.</span></span>

    <span data-ttu-id="8e050-133">a.</span><span class="sxs-lookup"><span data-stu-id="8e050-133">a.</span></span> <span data-ttu-id="8e050-134">Se já estiver montado, desmonte disco hello:</span><span class="sxs-lookup"><span data-stu-id="8e050-134">If already mounted, unmount hello disk:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

    <span data-ttu-id="8e050-135">b.</span><span class="sxs-lookup"><span data-stu-id="8e050-135">b.</span></span> <span data-ttu-id="8e050-136">Use `parted` tooview informações do disco e redimensionar a partição hello:</span><span class="sxs-lookup"><span data-stu-id="8e050-136">Use `parted` tooview disk information and resize hello partition:</span></span>

    ```bash
    sudo parted /dev/sdc
    ```

    <span data-ttu-id="8e050-137">Exibir informações sobre o layout de partição existente Olá com `print`.</span><span class="sxs-lookup"><span data-stu-id="8e050-137">View information about hello existing partition layout with `print`.</span></span> <span data-ttu-id="8e050-138">saudação de saída é semelhante toohello exemplo, que mostra o disco subjacente Olá tem 215Gb a seguir:</span><span class="sxs-lookup"><span data-stu-id="8e050-138">hello output is similar toohello following example, which shows hello underlying disk is 215Gb in size:</span></span>

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome tooGNU Parted! Type 'help' tooview a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    <span data-ttu-id="8e050-139">c.</span><span class="sxs-lookup"><span data-stu-id="8e050-139">c.</span></span> <span data-ttu-id="8e050-140">Expanda a partição de saudação com `resizepart`.</span><span class="sxs-lookup"><span data-stu-id="8e050-140">Expand hello partition with `resizepart`.</span></span> <span data-ttu-id="8e050-141">Insira o número de partição Olá *1*e um tamanho para a nova partição de saudação:</span><span class="sxs-lookup"><span data-stu-id="8e050-141">Enter hello partition number, *1*, and a size for hello new partition:</span></span>

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    <span data-ttu-id="8e050-142">d.</span><span class="sxs-lookup"><span data-stu-id="8e050-142">d.</span></span> <span data-ttu-id="8e050-143">tooexit, digite`quit`</span><span class="sxs-lookup"><span data-stu-id="8e050-143">tooexit, enter `quit`</span></span>

5. <span data-ttu-id="8e050-144">Partição Olá redimensionado, verificar a consistência de partição de saudação com `e2fsck`:</span><span class="sxs-lookup"><span data-stu-id="8e050-144">With hello partition resized, verify hello partition consistency with `e2fsck`:</span></span>

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. <span data-ttu-id="8e050-145">Redimensionar agora Olá filesystem com `resize2fs`:</span><span class="sxs-lookup"><span data-stu-id="8e050-145">Now resize hello filesystem with `resize2fs`:</span></span>

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. <span data-ttu-id="8e050-146">Montagem Olá partição toohello desejado local, como `/datadrive`:</span><span class="sxs-lookup"><span data-stu-id="8e050-146">Mount hello partition toohello desired location, such as `/datadrive`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. <span data-ttu-id="8e050-147">disco de SO de saudação tooverify foi redimensionado, use `df -h`.</span><span class="sxs-lookup"><span data-stu-id="8e050-147">tooverify hello OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="8e050-148">Olá saída de exemplo a seguir mostra a unidade de dados hello, */desenvolvimento/sdc1*, agora é de 200 GB:</span><span class="sxs-lookup"><span data-stu-id="8e050-148">hello following example output shows hello data drive, */dev/sdc1*, is now 200 GB:</span></span>

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a><span data-ttu-id="8e050-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8e050-149">Next steps</span></span>
<span data-ttu-id="8e050-150">Se você precisar de armazenamento adicional, você também [adicionar discos de dados tooa VM Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="8e050-150">If you need additional storage, you also [add data disks tooa Linux VM](add-disk.md).</span></span> <span data-ttu-id="8e050-151">Para obter mais informações sobre criptografia de disco, consulte [Olá criptografar discos em uma VM do Linux usando a CLI do Azure](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="8e050-151">For more information about disk encryption, see [Encrypt disks on a Linux VM using hello Azure CLI](encrypt-disks.md).</span></span>
