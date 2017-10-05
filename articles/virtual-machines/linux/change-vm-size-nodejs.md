---
title: Como redimensionar uma VM do Linux com a CLI 1.0 do Azure | Microsoft Docs
description: "Como escalar ou reduzir verticalmente uma máquina virtual Linux, alterando o tamanho da VM."
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
ms.openlocfilehash: 72f5a3cd6463befd5108040ed166984281bfc5f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a><span data-ttu-id="5c395-103">Redimensionar uma VM Linux com a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="5c395-103">Resize a Linux VM with Azure CLI 1.0</span></span>

## <a name="overview"></a><span data-ttu-id="5c395-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="5c395-104">Overview</span></span>

<span data-ttu-id="5c395-105">Depois de provisionar uma VM (máquina virtual), é possível escalar ou reduzir verticalmente a VM alterando o [tamanho da VM][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="5c395-105">After you provision a virtual machine (VM), you can scale the VM up or down by changing the [VM size][vm-sizes].</span></span> <span data-ttu-id="5c395-106">Em alguns casos, você deverá desalocar a VM primeiro.</span><span class="sxs-lookup"><span data-stu-id="5c395-106">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="5c395-107">Isso pode acontecer se o novo tamanho não estiver disponível no cluster de hardware que hospeda a VM.</span><span class="sxs-lookup"><span data-stu-id="5c395-107">This can happen if the new size is not available on the hardware cluster that is hosting the VM.</span></span>

<span data-ttu-id="5c395-108">Este artigo mostra como redimensionar uma VM Linux usando a [CLI do Azure][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="5c395-108">This article shows how to resize a Linux VM using the [Azure CLI][azure-cli].</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="5c395-109">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="5c395-109">CLI versions to complete the task</span></span>
<span data-ttu-id="5c395-110">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="5c395-110">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="5c395-111">[CLI 1.0 do Azure](#resize-a-linux-vm) – nossa CLI para os modelos de implantação clássico e de gerenciamento de recursos (este artigo)</span><span class="sxs-lookup"><span data-stu-id="5c395-111">[Azure CLI 1.0](#resize-a-linux-vm) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="5c395-112">[CLI 2.0 do Azure](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – nossa última geração de CLI para o modelo de implantação de gerenciamento de recursos</span><span class="sxs-lookup"><span data-stu-id="5c395-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="resize-a-linux-vm"></a><span data-ttu-id="5c395-113">Redimensionar uma VM Linux</span><span class="sxs-lookup"><span data-stu-id="5c395-113">Resize a Linux VM</span></span>
<span data-ttu-id="5c395-114">Para redimensionar uma VM, execute as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="5c395-114">To resize a VM, perform the following steps.</span></span>

1. <span data-ttu-id="5c395-115">Execute o comando da CLI a seguir.</span><span class="sxs-lookup"><span data-stu-id="5c395-115">Run the following CLI command.</span></span> <span data-ttu-id="5c395-116">Esse comando lista os tamanhos de VM que estão disponíveis no cluster do hardware onde a VM está hospedada.</span><span class="sxs-lookup"><span data-stu-id="5c395-116">This command lists the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span>
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. <span data-ttu-id="5c395-117">Se o tamanho desejado estiver listado, execute o comando a seguir para redimensionar a VM.</span><span class="sxs-lookup"><span data-stu-id="5c395-117">If the desired size is listed, run the following command to resize the VM.</span></span>
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    <span data-ttu-id="5c395-118">A VM será reiniciada durante esse processo.</span><span class="sxs-lookup"><span data-stu-id="5c395-118">The VM will restart during this process.</span></span> <span data-ttu-id="5c395-119">Após a reinicialização, os discos do sistema operacional e de dados serão remapeados.</span><span class="sxs-lookup"><span data-stu-id="5c395-119">After the restart, your existing OS and data disks will be remapped.</span></span> <span data-ttu-id="5c395-120">Qualquer coisa no disco temporário será perdida.</span><span class="sxs-lookup"><span data-stu-id="5c395-120">Anything on the temporary disk will be lost.</span></span>
   
    <span data-ttu-id="5c395-121">O uso da opção `--enable-boot-diagnostics` habilita o [diagnóstico de inicialização][boot-diagnostics], para registrar erros relacionados à inicialização.</span><span class="sxs-lookup"><span data-stu-id="5c395-121">Use the `--enable-boot-diagnostics` option enables [boot diagnostics][boot-diagnostics], to log any errors related to startup.</span></span>
3. <span data-ttu-id="5c395-122">Caso contrário, se o tamanho desejado não estiver listado, execute os comandos a seguir para desalocar a máquina virtual, redimensioná-la e, em seguida, reinicie a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5c395-122">Otherwise, if the desired size is not listed, run the following commands to deallocate the VM, resize it, and then restart the VM.</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="5c395-123">Desalocar a VM também libera os endereços IP dinâmicos atribuídos à VM.</span><span class="sxs-lookup"><span data-stu-id="5c395-123">Deallocating the VM also releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="5c395-124">Os discos do sistema operacional e de dados não são afetados.</span><span class="sxs-lookup"><span data-stu-id="5c395-124">The OS and data disks are not affected.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="5c395-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5c395-125">Next steps</span></span>
<span data-ttu-id="5c395-126">Para obter escalabilidade adicional, execute várias instâncias de VM e expanda.</span><span class="sxs-lookup"><span data-stu-id="5c395-126">For additional scalability, run multiple VM instances and scale out.</span></span> <span data-ttu-id="5c395-127">Para obter mais informações, consulte [Dimensionar automaticamente computadores Linux em um conjunto de dimensionamento de máquinas virtuais][scale-set].</span><span class="sxs-lookup"><span data-stu-id="5c395-127">For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
