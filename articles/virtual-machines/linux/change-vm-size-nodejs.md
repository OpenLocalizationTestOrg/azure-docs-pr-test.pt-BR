---
title: aaaHow tooresize uma VM do Linux com hello 1.0 da CLI do Azure | Microsoft Docs
description: "Como a escala para baixo de uma máquina virtual Linux, alterando ou tooscale backup Olá tamanho da VM."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2016
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 43dd955dc2f2dd9d1b2da07ecbfbf2459bcaa4d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a><span data-ttu-id="efcd2-103">Redimensionar uma VM Linux com a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="efcd2-103">Resize a Linux VM with Azure CLI 1.0</span></span>

## <a name="overview"></a><span data-ttu-id="efcd2-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="efcd2-104">Overview</span></span>

<span data-ttu-id="efcd2-105">Depois de provisionar uma máquina virtual (VM), você pode expandir ou reduzir Olá VM alterando Olá [tamanho da VM][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="efcd2-105">After you provision a virtual machine (VM), you can scale hello VM up or down by changing hello [VM size][vm-sizes].</span></span> <span data-ttu-id="efcd2-106">Em alguns casos, você deverá desalocar Olá VM pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="efcd2-106">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="efcd2-107">Isso pode acontecer se o novo tamanho de saudação não está disponível no cluster de hardware de saudação que está hospedando o hello VM.</span><span class="sxs-lookup"><span data-stu-id="efcd2-107">This can happen if hello new size is not available on hello hardware cluster that is hosting hello VM.</span></span>

<span data-ttu-id="efcd2-108">Este artigo mostra como tooresize uma VM do Linux usando Olá [CLI do Azure][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="efcd2-108">This article shows how tooresize a Linux VM using hello [Azure CLI][azure-cli].</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="efcd2-109">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="efcd2-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="efcd2-110">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="efcd2-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="efcd2-111">[1.0 de CLI do Azure](#resize-a-linux-vm) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="efcd2-111">[Azure CLI 1.0](#resize-a-linux-vm) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="efcd2-112">[2.0 do CLI do Azure](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="efcd2-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="resize-a-linux-vm"></a><span data-ttu-id="efcd2-113">Redimensionar uma VM Linux</span><span class="sxs-lookup"><span data-stu-id="efcd2-113">Resize a Linux VM</span></span>
<span data-ttu-id="efcd2-114">tooresize uma VM, execute Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="efcd2-114">tooresize a VM, perform hello following steps.</span></span>

1. <span data-ttu-id="efcd2-115">Execute Olá CLI comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="efcd2-115">Run hello following CLI command.</span></span> <span data-ttu-id="efcd2-116">Esse comando lista os tamanhos de VM Olá que estão disponíveis no cluster de hardware Olá onde hello VM está hospedada.</span><span class="sxs-lookup"><span data-stu-id="efcd2-116">This command lists hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span>
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. <span data-ttu-id="efcd2-117">Se Olá desejado tamanho estiver listado, execute Olá Olá tooresize de comando VM a seguir.</span><span class="sxs-lookup"><span data-stu-id="efcd2-117">If hello desired size is listed, run hello following command tooresize hello VM.</span></span>
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    <span data-ttu-id="efcd2-118">Olá VM será reiniciado durante esse processo.</span><span class="sxs-lookup"><span data-stu-id="efcd2-118">hello VM will restart during this process.</span></span> <span data-ttu-id="efcd2-119">Após a reinicialização de saudação, seu sistema operacional existente e os discos de dados serão remapeados.</span><span class="sxs-lookup"><span data-stu-id="efcd2-119">After hello restart, your existing OS and data disks will be remapped.</span></span> <span data-ttu-id="efcd2-120">Tudo em disco temporário hello serão perdido.</span><span class="sxs-lookup"><span data-stu-id="efcd2-120">Anything on hello temporary disk will be lost.</span></span>
   
    <span data-ttu-id="efcd2-121">Saudação de uso `--enable-boot-diagnostics` opção habilita [diagnósticos de inicialização][boot-diagnostics], toolog qualquer toostartup de erros relacionados.</span><span class="sxs-lookup"><span data-stu-id="efcd2-121">Use hello `--enable-boot-diagnostics` option enables [boot diagnostics][boot-diagnostics], toolog any errors related toostartup.</span></span>
3. <span data-ttu-id="efcd2-122">Caso contrário, se Olá desejado tamanho não estiver listado, execute Olá toodeallocate Olá VM, redimensioná-la e, em seguida, reiniciar Olá VM de comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="efcd2-122">Otherwise, if hello desired size is not listed, run hello following commands toodeallocate hello VM, resize it, and then restart hello VM.</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="efcd2-123">Olá ao desalocar VM também libera os endereços IP dinâmicos atribuídos toohello VM.</span><span class="sxs-lookup"><span data-stu-id="efcd2-123">Deallocating hello VM also releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="efcd2-124">Olá SO e discos de dados não são afetados.</span><span class="sxs-lookup"><span data-stu-id="efcd2-124">hello OS and data disks are not affected.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="efcd2-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="efcd2-125">Next steps</span></span>
<span data-ttu-id="efcd2-126">Para obter escalabilidade adicional, execute várias instâncias de VM e expanda. Para obter mais informações, consulte [Dimensionar automaticamente computadores Linux em um conjunto de dimensionamento de máquinas virtuais][scale-set].</span><span class="sxs-lookup"><span data-stu-id="efcd2-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
