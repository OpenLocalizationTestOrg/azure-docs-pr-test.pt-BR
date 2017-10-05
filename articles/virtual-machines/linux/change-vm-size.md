---
title: Como redimensionar uma VM Linux com a CLI 2.0 do Azure | Microsoft Docs
description: "Como escalar ou reduzir verticalmente uma máquina virtual Linux, alterando o tamanho da VM."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: e163f878-b919-45c5-9f5a-75a64f3b14a0
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2017
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23fc9f7f34732079682857d4ee685fe811751698
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a><span data-ttu-id="604af-103">Redimensionar uma máquina virtual do Linux usando a CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="604af-103">Resize a Linux virtual machine using CLI 2.0</span></span>

<span data-ttu-id="604af-104">Depois de provisionar uma VM (máquina virtual), é possível escalar ou reduzir verticalmente a VM alterando o [tamanho da VM][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="604af-104">After you provision a virtual machine (VM), you can scale the VM up or down by changing the [VM size][vm-sizes].</span></span> <span data-ttu-id="604af-105">Em alguns casos, você deverá desalocar a VM primeiro.</span><span class="sxs-lookup"><span data-stu-id="604af-105">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="604af-106">Você precisará desalocar a VM se o tamanho desejado não estiver disponível no cluster de hardware que está hospedando a VM.</span><span class="sxs-lookup"><span data-stu-id="604af-106">You need to deallocate the VM if the desired size is not available on the hardware cluster that is hosting the VM.</span></span> <span data-ttu-id="604af-107">Este artigo detalha como redimensionar uma VM Linux com a CLI do Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="604af-107">This article details how to resize a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="604af-108">Você também pode executar essas etapas com a [CLI do Azure 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="604af-108">You can also perform these steps with the [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="resize-a-vm"></a><span data-ttu-id="604af-109">Redimensionar uma VM</span><span class="sxs-lookup"><span data-stu-id="604af-109">Resize a VM</span></span>
<span data-ttu-id="604af-110">Para redimensionar uma VM, é preciso ter a [CLI 2.0 do Azure](/cli/azure/install-az-cli2) mais recente instalada e conectada a uma conta do Azure usando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="604af-110">To resize a VM, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

1. <span data-ttu-id="604af-111">Veja a lista de tamanhos de VM disponíveis no cluster de hardware onde a VM está hospedada com [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span><span class="sxs-lookup"><span data-stu-id="604af-111">View the list of available VM sizes on the hardware cluster where the VM is hosted with [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span></span> <span data-ttu-id="604af-112">O exemplo a seguir lista tamanhos de VM para a VM chamada `myVM` na região `myResourceGroup` do grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="604af-112">The following example lists VM sizes for the VM named `myVM` in the resource group `myResourceGroup` region:</span></span>
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. <span data-ttu-id="604af-113">Se o tamanho desejado da VM estiver listado, redimensione a VM com [az vm resize](/cli/azure/vm#resize).</span><span class="sxs-lookup"><span data-stu-id="604af-113">If the desired VM size is listed, resize the VM with [az vm resize](/cli/azure/vm#resize).</span></span> <span data-ttu-id="604af-114">O exemplo a seguir redimensiona a VM chamada `myVM` para o tamanho `Standard_DS3_v2`:</span><span class="sxs-lookup"><span data-stu-id="604af-114">The following example resizes the VM named `myVM` to the `Standard_DS3_v2` size:</span></span>
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    <span data-ttu-id="604af-115">A VM é reiniciada durante esse processo.</span><span class="sxs-lookup"><span data-stu-id="604af-115">The VM restarts during this process.</span></span> <span data-ttu-id="604af-116">Após a reinicialização, os discos existentes do sistema operacional e de dados são remapeados.</span><span class="sxs-lookup"><span data-stu-id="604af-116">After the restart, your existing OS and data disks are remapped.</span></span> <span data-ttu-id="604af-117">Tudo o que está no disco temporário é perdido.</span><span class="sxs-lookup"><span data-stu-id="604af-117">Anything on the temporary disk is lost.</span></span>

3. <span data-ttu-id="604af-118">Se o tamanho desejado da VM não estiver listado, você precisará primeiro desalocar a VM com [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="604af-118">If the desired VM size is not listed, you need to first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="604af-119">Esse processo permite que a VM seja redimensionada para qualquer tamanho disponível ao qual a região dê suporte e então reiniciada.</span><span class="sxs-lookup"><span data-stu-id="604af-119">This process allows the VM to then be resized to any size available that the region supports and then started.</span></span> <span data-ttu-id="604af-120">As etapas a seguir desalocam, redimensionam e iniciam a VM denominada `myVM` no grupo de recursos chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="604af-120">The following steps deallocate, resize, and then start the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="604af-121">Desalocar a VM também libera os endereços IP dinâmicos atribuídos à VM.</span><span class="sxs-lookup"><span data-stu-id="604af-121">Deallocating the VM also releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="604af-122">Os discos do sistema operacional e de dados não são afetados.</span><span class="sxs-lookup"><span data-stu-id="604af-122">The OS and data disks are not affected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="604af-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="604af-123">Next steps</span></span>
<span data-ttu-id="604af-124">Para obter escalabilidade adicional, execute várias instâncias de VM e expanda.</span><span class="sxs-lookup"><span data-stu-id="604af-124">For additional scalability, run multiple VM instances and scale out.</span></span> <span data-ttu-id="604af-125">Para obter mais informações, consulte [Dimensionar automaticamente computadores Linux em um conjunto de dimensionamento de máquinas virtuais][scale-set].</span><span class="sxs-lookup"><span data-stu-id="604af-125">For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
