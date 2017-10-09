---
title: aaaHow tooresize uma VM do Linux com hello 2.0 do CLI do Azure | Microsoft Docs
description: "Como a escala para baixo de uma máquina virtual Linux, alterando ou tooscale backup Olá tamanho da VM."
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
ms.openlocfilehash: e8fba485b5bcc7824f546de5cf3df77624a28008
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a><span data-ttu-id="81fca-103">Redimensionar uma máquina virtual do Linux usando a CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="81fca-103">Resize a Linux virtual machine using CLI 2.0</span></span>

<span data-ttu-id="81fca-104">Depois de provisionar uma máquina virtual (VM), você pode expandir ou reduzir Olá VM alterando Olá [tamanho da VM][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="81fca-104">After you provision a virtual machine (VM), you can scale hello VM up or down by changing hello [VM size][vm-sizes].</span></span> <span data-ttu-id="81fca-105">Em alguns casos, você deverá desalocar Olá VM pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="81fca-105">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="81fca-106">É necessário toodeallocate Olá VM se Olá desejado de tamanho não está disponível no cluster de hardware de saudação que está hospedando o hello VM.</span><span class="sxs-lookup"><span data-stu-id="81fca-106">You need toodeallocate hello VM if hello desired size is not available on hello hardware cluster that is hosting hello VM.</span></span> <span data-ttu-id="81fca-107">Este artigo fornece detalhes sobre como tooresize uma VM do Linux com hello 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="81fca-107">This article details how tooresize a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="81fca-108">Você também pode executar essas etapas com hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="81fca-108">You can also perform these steps with hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="resize-a-vm"></a><span data-ttu-id="81fca-109">Redimensionar uma VM</span><span class="sxs-lookup"><span data-stu-id="81fca-109">Resize a VM</span></span>
<span data-ttu-id="81fca-110">tooresize uma VM, você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="81fca-110">tooresize a VM, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

1. <span data-ttu-id="81fca-111">Tamanhos de exibir a lista de saudação de VM disponível no cluster de hardware Olá onde Olá VM for hospedado com [az vm lista-vm--opções de redimensionamento](/cli/azure/vm#list-vm-resize-options).</span><span class="sxs-lookup"><span data-stu-id="81fca-111">View hello list of available VM sizes on hello hardware cluster where hello VM is hosted with [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span></span> <span data-ttu-id="81fca-112">Olá, exemplo a seguir lista os tamanhos de VM para Olá VM denominada `myVM` no grupo de recursos de saudação `myResourceGroup` região:</span><span class="sxs-lookup"><span data-stu-id="81fca-112">hello following example lists VM sizes for hello VM named `myVM` in hello resource group `myResourceGroup` region:</span></span>
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. <span data-ttu-id="81fca-113">Se Olá desejado que o tamanho da VM está listado, redimensionar Olá VM com [az vm redimensionar](/cli/azure/vm#resize).</span><span class="sxs-lookup"><span data-stu-id="81fca-113">If hello desired VM size is listed, resize hello VM with [az vm resize](/cli/azure/vm#resize).</span></span> <span data-ttu-id="81fca-114">Olá redimensiona de exemplo a seguir Olá VM denominada `myVM` toohello `Standard_DS3_v2` tamanho:</span><span class="sxs-lookup"><span data-stu-id="81fca-114">hello following example resizes hello VM named `myVM` toohello `Standard_DS3_v2` size:</span></span>
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    <span data-ttu-id="81fca-115">Olá VM é reiniciado durante esse processo.</span><span class="sxs-lookup"><span data-stu-id="81fca-115">hello VM restarts during this process.</span></span> <span data-ttu-id="81fca-116">Após a reinicialização de saudação, seu sistema operacional existente e os discos de dados são remapeados.</span><span class="sxs-lookup"><span data-stu-id="81fca-116">After hello restart, your existing OS and data disks are remapped.</span></span> <span data-ttu-id="81fca-117">Tudo em disco temporário Olá será perdido.</span><span class="sxs-lookup"><span data-stu-id="81fca-117">Anything on hello temporary disk is lost.</span></span>

3. <span data-ttu-id="81fca-118">Se Olá desejado tamanho da VM não estiver listado, você precisa toofirst desalocar Olá VM com [az vm desalocar](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="81fca-118">If hello desired VM size is not listed, you need toofirst deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="81fca-119">Esse processo permite Olá VM toothen ser redimensionado tooany tamanho disponível Olá suporta de região e, em seguida, iniciado.</span><span class="sxs-lookup"><span data-stu-id="81fca-119">This process allows hello VM toothen be resized tooany size available that hello region supports and then started.</span></span> <span data-ttu-id="81fca-120">Olá etapas a seguir desalocar, redimensionar e, em seguida, iniciar Olá VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="81fca-120">hello following steps deallocate, resize, and then start hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="81fca-121">Olá ao desalocar VM também libera os endereços IP dinâmicos atribuídos toohello VM.</span><span class="sxs-lookup"><span data-stu-id="81fca-121">Deallocating hello VM also releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="81fca-122">Olá SO e discos de dados não são afetados.</span><span class="sxs-lookup"><span data-stu-id="81fca-122">hello OS and data disks are not affected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81fca-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="81fca-123">Next steps</span></span>
<span data-ttu-id="81fca-124">Para obter escalabilidade adicional, execute várias instâncias de VM e expanda. Para obter mais informações, consulte [Dimensionar automaticamente computadores Linux em um conjunto de dimensionamento de máquinas virtuais][scale-set].</span><span class="sxs-lookup"><span data-stu-id="81fca-124">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
