---
title: "aaaConvert uma máquina virtual do Linux no Azure de não discos toomanaged discos - Azure gerenciados | Microsoft Docs"
description: "Como tooconvert uma VM do Linux de discos não gerenciado toomanaged discos usando 2.0 do CLI do Azure no modelo de implantação do Gerenciador de recursos de saudação"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 1b94da11deab46f344e28ab4491cf220506b6347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a><span data-ttu-id="be26b-103">Converter uma máquina virtual Linux de discos de toomanaged de discos não gerenciado</span><span class="sxs-lookup"><span data-stu-id="be26b-103">Convert a Linux virtual machine from unmanaged disks toomanaged disks</span></span>

<span data-ttu-id="be26b-104">Se você tiver existente Linux (máquinas virtuais) que usa discos não gerenciados, você pode converter Olá VMs toouse gerenciado discos por meio de saudação [discos gerenciado do Azure](../windows/managed-disks-overview.md) serviço.</span><span class="sxs-lookup"><span data-stu-id="be26b-104">If you have existing Linux virtual machines (VMs) that use unmanaged disks, you can convert hello VMs toouse managed disks through hello [Azure Managed Disks](../windows/managed-disks-overview.md) service.</span></span> <span data-ttu-id="be26b-105">Esse processo converte disco Olá SO e discos de dados anexado.</span><span class="sxs-lookup"><span data-stu-id="be26b-105">This process converts both hello OS disk and any attached data disks.</span></span>

<span data-ttu-id="be26b-106">Este artigo mostra como tooconvert VMs usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="be26b-106">This article shows you how tooconvert VMs by using hello Azure CLI.</span></span> <span data-ttu-id="be26b-107">Se você precisa tooinstall ou atualizá-lo, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="be26b-107">If you need tooinstall or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="be26b-108">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="be26b-108">Before you begin</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a><span data-ttu-id="be26b-109">Converter VMs de instância única</span><span class="sxs-lookup"><span data-stu-id="be26b-109">Convert single-instance VMs</span></span>
<span data-ttu-id="be26b-110">Esta seção aborda como VMs do Azure de não gerenciado de instância única de tooconvert discos toomanaged discos.</span><span class="sxs-lookup"><span data-stu-id="be26b-110">This section covers how tooconvert single-instance Azure VMs from unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="be26b-111">(Se suas VMs estiverem em um conjunto de disponibilidade, consulte Olá próxima seção.) Você pode usar esse processo tooconvert Olá VMs a partir de discos de toopremium gerenciado discos premium (SSD) não gerenciado ou padrão (HDD) não gerenciados discos toostandard gerenciado discos.</span><span class="sxs-lookup"><span data-stu-id="be26b-111">(If your VMs are in an availability set, see hello next section.) You can use this process tooconvert hello VMs from premium (SSD) unmanaged disks toopremium managed disks, or from standard (HDD) unmanaged disks toostandard managed disks.</span></span>

1. <span data-ttu-id="be26b-112">Desalocar Olá VM usando [az vm desalocar](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="be26b-112">Deallocate hello VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="be26b-113">exemplo a seguir Hello desaloca Olá VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="be26b-113">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. <span data-ttu-id="be26b-114">Converter os discos de toomanaged VM hello usando [az vm converter](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="be26b-114">Convert hello VM toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="be26b-115">Olá seguindo o processo converte Olá VM denominada `myVM`, incluindo disco Olá SO e discos de dados:</span><span class="sxs-lookup"><span data-stu-id="be26b-115">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="be26b-116">Iniciar Olá VM depois de discos do hello conversão toomanaged usando [início de vm az](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="be26b-116">Start hello VM after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="be26b-117">Olá inicia de exemplo a seguir Olá VM denominada `myVM` no grupo de recursos de saudação denominado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="be26b-117">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="be26b-118">Converter VMs em um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="be26b-118">Convert VMs in an availability set</span></span>

<span data-ttu-id="be26b-119">Se Olá VMs que você deseja tooconvert toomanaged discos estão em um conjunto de disponibilidade, é necessário primeiro conjunto de disponibilidade do tooconvert Olá tooa gerenciado conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="be26b-119">If hello VMs that you want tooconvert toomanaged disks are in an availability set, you first need tooconvert hello availability set tooa managed availability set.</span></span>

<span data-ttu-id="be26b-120">Todas as VMs no conjunto de disponibilidade Olá devem ser desalocadas antes de converter o conjunto de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="be26b-120">All VMs in hello availability set must be deallocated before you convert hello availability set.</span></span> <span data-ttu-id="be26b-121">Plano tooconvert todos os discos de toomanaged VMs após a disponibilidade de saudação definido foi convertido tooa gerenciado conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="be26b-121">Plan tooconvert all VMs toomanaged disks after hello availability set itself has been converted tooa managed availability set.</span></span> <span data-ttu-id="be26b-122">Em seguida, inicie todas as VMs hello e continuar a operar normalmente.</span><span class="sxs-lookup"><span data-stu-id="be26b-122">Then, start all hello VMs and continue operating as normal.</span></span>

1. <span data-ttu-id="be26b-123">Liste todas as VMs em um conjunto de disponibilidade usando [az vm availability-set list](/cli/azure/vm/availability-set#list).</span><span class="sxs-lookup"><span data-stu-id="be26b-123">List all VMs in an availability set by using [az vm availability-set list](/cli/azure/vm/availability-set#list).</span></span> <span data-ttu-id="be26b-124">Olá exemplo a seguir lista todas as VMs no conjunto nomeada de disponibilidade de saudação `myAvailabilitySet` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="be26b-124">hello following example lists all VMs in hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. <span data-ttu-id="be26b-125">Desalocar todas as VMs hello usando [az vm desalocar](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="be26b-125">Deallocate all hello VMs by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="be26b-126">exemplo a seguir Hello desaloca Olá VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="be26b-126">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="be26b-127">Converter a disponibilidade de saudação definida por meio de [converter de conjunto de disponibilidade de vm az](/cli/azure/vm/availability-set#convert).</span><span class="sxs-lookup"><span data-stu-id="be26b-127">Convert hello availability set by using [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span></span> <span data-ttu-id="be26b-128">Olá, exemplo a seguir converte conjunto nomeada de disponibilidade de saudação `myAvailabilitySet` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="be26b-128">hello following example converts hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. <span data-ttu-id="be26b-129">Converter todos os discos do hello VMs toomanaged usando [az vm converter](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="be26b-129">Convert all hello VMs toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="be26b-130">Olá seguindo o processo converte Olá VM denominada `myVM`, incluindo disco Olá SO e discos de dados:</span><span class="sxs-lookup"><span data-stu-id="be26b-130">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. <span data-ttu-id="be26b-131">Iniciar todas as VMs Olá após discos de toomanaged conversão hello usando [início de vm az](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="be26b-131">Start all hello VMs after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="be26b-132">Olá inicia de exemplo a seguir Olá VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="be26b-132">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="be26b-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="be26b-133">Next steps</span></span>
<span data-ttu-id="be26b-134">Para saber mais sobre as opções de armazenamento, confira a [Visão geral dos Azure Managed Disks](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="be26b-134">For more information about storage options, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>
