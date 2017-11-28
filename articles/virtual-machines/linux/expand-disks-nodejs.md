---
title: disco aaaExpand SO na VM do Linux com hello 1.0 da CLI do Azure | Microsoft Docs
description: "Saiba como tooexpand Olá disco virtual do sistema operacional (SO) em uma VM do Linux usando hello Azure CLI 1.0 e o modelo de implantação do Gerenciador de recursos de saudação"
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
ms.openlocfilehash: 0db78c0b86b48b2c5358611e11bb0b7ad781a559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="expand-os-disk-on-a-linux-vm-using-hello-azure-cli-with-hello-azure-cli-10"></a><span data-ttu-id="9156b-103">Expanda o disco do sistema operacional em uma VM do Linux usando Olá CLI do Azure com hello 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9156b-103">Expand OS disk on a Linux VM using hello Azure CLI with hello Azure CLI 1.0</span></span>
<span data-ttu-id="9156b-104">tamanho de disco rígido virtual saudação padrão para o sistema operacional de saudação (SO) normalmente é 30 GB em uma máquina virtual do Linux (VM) no Azure.</span><span class="sxs-lookup"><span data-stu-id="9156b-104">hello default virtual hard disk size for hello operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="9156b-105">Você pode [adicionar discos de dados](add-disk.md) tooprovide para espaço de armazenamento adicional, mas você também poderá tooexpand disco de saudação sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="9156b-105">You can [add data disks](add-disk.md) tooprovide for additional storage space, but you may also wish tooexpand hello OS disk.</span></span> <span data-ttu-id="9156b-106">Este artigo fornece detalhes sobre como tooexpand Olá SO de disco para uma VM do Linux usando discos gerenciados por hello 1.0 da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="9156b-106">This article details how tooexpand hello OS disk for a Linux VM using unmanaged disks with hello Azure CLI 1.0.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="9156b-107">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="9156b-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="9156b-108">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="9156b-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="9156b-109">[1.0 de CLI do Azure](#prerequisites) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="9156b-109">[Azure CLI 1.0](#prerequisites) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="9156b-110">[2.0 do CLI do Azure](expand-disks.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="9156b-110">[Azure CLI 2.0](expand-disks.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9156b-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9156b-111">Prerequisites</span></span>
<span data-ttu-id="9156b-112">Você precisa Olá [1.0 mais recente de CLI do Azure](../../cli-install-nodejs.md) instalado e registrado no tooan [conta do Azure](https://azure.microsoft.com/pricing/free-trial/) usando o modo do Gerenciador de recursos de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9156b-112">You need hello [latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in tooan [Azure account](https://azure.microsoft.com/pricing/free-trial/) using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="9156b-113">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="9156b-113">In hello following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="9156b-114">Os nomes de parâmetro de exemplo incluem *myResourceGroup* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="9156b-114">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

## <a name="expand-os-disk"></a><span data-ttu-id="9156b-115">Expandir o disco do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="9156b-115">Expand OS disk</span></span>

1. <span data-ttu-id="9156b-116">Não é possível executar operações em discos rígidos virtuais com hello VM em execução.</span><span class="sxs-lookup"><span data-stu-id="9156b-116">Operations on virtual hard disks cannot be performed with hello VM running.</span></span> <span data-ttu-id="9156b-117">Olá exemplo a seguir interrompe e desaloca Olá VM denominada *myVM* no grupo de recursos de saudação denominado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="9156b-117">hello following example stops and deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="9156b-118">`azure vm stop`não liberar recursos de computação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9156b-118">`azure vm stop` does not release hello compute resources.</span></span> <span data-ttu-id="9156b-119">toorelease recursos de computação, use `azure vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="9156b-119">toorelease compute resources, use `azure vm deallocate`.</span></span> <span data-ttu-id="9156b-120">Olá VM deve ser desalocada tooexpand saudação do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="9156b-120">hello VM must be deallocated tooexpand hello virtual hard disk.</span></span>

2. <span data-ttu-id="9156b-121">Atualizar Olá tamanho do disco do sistema operacional Olá não gerenciado usando Olá `azure vm set` comando.</span><span class="sxs-lookup"><span data-stu-id="9156b-121">Update hello size of hello unmanaged OS disk using hello `azure vm set` command.</span></span> <span data-ttu-id="9156b-122">Olá atualizações de exemplo a seguir Olá VM denominada *myVM* no grupo de recursos de saudação denominado *myResourceGroup* toobe *50* GB:</span><span class="sxs-lookup"><span data-stu-id="9156b-122">hello following example updates hello VM named *myVM* in hello resource group named *myResourceGroup* toobe *50* GB:</span></span>

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. <span data-ttu-id="9156b-123">Inicie a VM da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9156b-123">Start your VM as follows:</span></span>

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="9156b-124">SSH tooyour VM com as credenciais apropriadas hello.</span><span class="sxs-lookup"><span data-stu-id="9156b-124">SSH tooyour VM with hello appropriate credentials.</span></span> <span data-ttu-id="9156b-125">disco de SO de saudação tooverify foi redimensionado, use `df -h`.</span><span class="sxs-lookup"><span data-stu-id="9156b-125">tooverify hello OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="9156b-126">Olá saída de exemplo a seguir mostra a partição primária hello (*/desenvolvimento/sda1*) agora é 50 GB:</span><span class="sxs-lookup"><span data-stu-id="9156b-126">hello following example output shows hello primary partition (*/dev/sda1*) is now 50 GB:</span></span>

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a><span data-ttu-id="9156b-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9156b-127">Next steps</span></span>
<span data-ttu-id="9156b-128">Se você precisar de armazenamento adicional, você também [adicionar discos de dados tooa VM Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="9156b-128">If you need additional storage, you also [add data disks tooa Linux VM](add-disk.md).</span></span> <span data-ttu-id="9156b-129">Para obter mais informações sobre criptografia de disco, consulte [Olá criptografar discos em uma VM do Linux usando a CLI do Azure](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="9156b-129">For more information about disk encryption, see [Encrypt disks on a Linux VM using hello Azure CLI](encrypt-disks.md).</span></span>
