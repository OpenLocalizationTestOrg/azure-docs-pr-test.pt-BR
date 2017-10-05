---
title: Expandir o disco do sistema operacional em uma VM Linux com a CLI do Azure 1.0 | Microsoft Docs
description: "Saiba como expandir o disco virtual do sistema operacional em uma VM Linux usando a CLI do Azure 1.0 e o modelo de implantação do Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0aedcd70b54c2ed47ec327ccf0529a48351353c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="expand-os-disk-on-a-linux-vm-using-the-azure-cli-with-the-azure-cli-10"></a><span data-ttu-id="42502-103">Expandir o disco do sistema operacional em uma VM Linux usando a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="42502-103">Expand OS disk on a Linux VM using the Azure CLI with the Azure CLI 1.0</span></span>
<span data-ttu-id="42502-104">Normalmente, o tamanho do disco rígido virtual padrão do sistema operacional é de 30 GB em uma VM (máquina virtual) do Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="42502-104">The default virtual hard disk size for the operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="42502-105">É possível [adicionar discos de dados](add-disk.md) para fornecer espaço de armazenamento adicional, mas você também pode desejar expandir o disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="42502-105">You can [add data disks](add-disk.md) to provide for additional storage space, but you may also wish to expand the OS disk.</span></span> <span data-ttu-id="42502-106">Este artigo fornece detalhes sobre como expandir o disco do sistema operacional de uma VM Linux usando discos não gerenciados com a CLI do Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="42502-106">This article details how to expand the OS disk for a Linux VM using unmanaged disks with the Azure CLI 1.0.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="42502-107">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="42502-107">CLI versions to complete the task</span></span>
<span data-ttu-id="42502-108">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="42502-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="42502-109">[CLI 1.0 do Azure](#prerequisites) – nossa CLI para os modelos de implantação clássico e de gerenciamento de recursos (este artigo)</span><span class="sxs-lookup"><span data-stu-id="42502-109">[Azure CLI 1.0](#prerequisites) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="42502-110">[CLI 2.0 do Azure](expand-disks.md) – nossa última geração de CLI para o modelo de implantação de gerenciamento de recursos</span><span class="sxs-lookup"><span data-stu-id="42502-110">[Azure CLI 2.0](expand-disks.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42502-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="42502-111">Prerequisites</span></span>
<span data-ttu-id="42502-112">Você precisa da [última CLI do Azure 1.0](../../cli-install-nodejs.md) instalada e conectada a uma [conta do Azure](https://azure.microsoft.com/pricing/free-trial/) usando o modo do Resource Manager, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="42502-112">You need the [latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in to an [Azure account](https://azure.microsoft.com/pricing/free-trial/) using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="42502-113">Nas amostras a seguir, substitua os nomes de parâmetro de exemplo por seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="42502-113">In the following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="42502-114">Os nomes de parâmetro de exemplo incluem *myResourceGroup* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="42502-114">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

## <a name="expand-os-disk"></a><span data-ttu-id="42502-115">Expandir o disco do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="42502-115">Expand OS disk</span></span>

1. <span data-ttu-id="42502-116">As operações em discos rígidos virtuais não podem ser executadas com a VM em execução.</span><span class="sxs-lookup"><span data-stu-id="42502-116">Operations on virtual hard disks cannot be performed with the VM running.</span></span> <span data-ttu-id="42502-117">O exemplo a seguir interrompe e desaloca a VM chamada *myVM* no grupo de recursos chamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="42502-117">The following example stops and deallocates the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="42502-118">`azure vm stop` não libera os recursos de computação.</span><span class="sxs-lookup"><span data-stu-id="42502-118">`azure vm stop` does not release the compute resources.</span></span> <span data-ttu-id="42502-119">Para liberar os recursos de computação, use `azure vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="42502-119">To release compute resources, use `azure vm deallocate`.</span></span> <span data-ttu-id="42502-120">A VM deve ser desalocada para que o disco rígido virtual seja expandido.</span><span class="sxs-lookup"><span data-stu-id="42502-120">The VM must be deallocated to expand the virtual hard disk.</span></span>

2. <span data-ttu-id="42502-121">Atualize o tamanho do disco não gerenciado do sistema operacional usando o comando `azure vm set`.</span><span class="sxs-lookup"><span data-stu-id="42502-121">Update the size of the unmanaged OS disk using the `azure vm set` command.</span></span> <span data-ttu-id="42502-122">O exemplo a seguir atualiza a VM chamada *myVM* no grupo de recursos chamado *myResourceGroup* para ser *50* GB:</span><span class="sxs-lookup"><span data-stu-id="42502-122">The following example updates the VM named *myVM* in the resource group named *myResourceGroup* to be *50* GB:</span></span>

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. <span data-ttu-id="42502-123">Inicie a VM da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="42502-123">Start your VM as follows:</span></span>

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="42502-124">SSH da VM com as credenciais apropriadas.</span><span class="sxs-lookup"><span data-stu-id="42502-124">SSH to your VM with the appropriate credentials.</span></span> <span data-ttu-id="42502-125">Para verificar se o disco do sistema operacional foi redimensionado, use `df -h`.</span><span class="sxs-lookup"><span data-stu-id="42502-125">To verify the OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="42502-126">A saída de exemplo a seguir mostra que a partição primária (*/dev/sda1*) agora tem 50 GB:</span><span class="sxs-lookup"><span data-stu-id="42502-126">The following example output shows the primary partition (*/dev/sda1*) is now 50 GB:</span></span>

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a><span data-ttu-id="42502-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="42502-127">Next steps</span></span>
<span data-ttu-id="42502-128">Se precisar de armazenamento adicional, também [adicione discos de dados a uma VM do Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="42502-128">If you need additional storage, you also [add data disks to a Linux VM](add-disk.md).</span></span> <span data-ttu-id="42502-129">Para obter mais informações sobre a criptografia de disco, consulte [Criptografar discos em uma VM do Linux usando a CLI do Azure](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="42502-129">For more information about disk encryption, see [Encrypt disks on a Linux VM using the Azure CLI](encrypt-disks.md).</span></span>
