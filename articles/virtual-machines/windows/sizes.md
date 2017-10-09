---
title: tamanhos de aaaWindows VM no Azure | Microsoft Docs
description: "Lista tamanhos diferentes de saudação disponíveis para máquinas virtuais do Windows no Azure."
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: aabf0d30-04eb-4d34-b44a-69f8bfb84f22
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 80bd8241b134031c41b56224e841c7557c4845cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a><span data-ttu-id="83ec4-103">Tamanhos das máquinas virtuais do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="83ec4-103">Sizes for Windows virtual machines in Azure</span></span>

<span data-ttu-id="83ec4-104">Este artigo descreve os tamanhos disponíveis hello e opções de saudação máquinas virtuais do Azure, você pode usar toorun seus aplicativos do Windows e cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="83ec4-104">This article describes hello available sizes and options for hello Azure virtual machines you can use toorun your Windows apps and workloads.</span></span> <span data-ttu-id="83ec4-105">Ele também fornece toobe de considerações de implantação ciente de quando você estiver planejando toouse esses recursos.</span><span class="sxs-lookup"><span data-stu-id="83ec4-105">It also provides deployment considerations toobe aware of when you're planning toouse these resources.</span></span>  <span data-ttu-id="83ec4-106">Este artigo também está disponível para [máquinas virtuais Linux](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="83ec4-106">This article is also available for [Linux virtual machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


| <span data-ttu-id="83ec4-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="83ec4-107">Type</span></span>                     | <span data-ttu-id="83ec4-108">Tamanhos</span><span class="sxs-lookup"><span data-stu-id="83ec4-108">Sizes</span></span>           |    <span data-ttu-id="83ec4-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="83ec4-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="83ec4-110">Propósito geral</span><span class="sxs-lookup"><span data-stu-id="83ec4-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="83ec4-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="83ec4-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span> | <span data-ttu-id="83ec4-112">Relação equilibrada de CPU/memória.</span><span class="sxs-lookup"><span data-stu-id="83ec4-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="83ec4-113">Ideal para teste e desenvolvimento, toomedium pequeno de bancos de dados e servidores web com tráfego toomedium baixa.</span><span class="sxs-lookup"><span data-stu-id="83ec4-113">Ideal for testing and development, small toomedium databases, and low toomedium traffic web servers.</span></span> |
| [<span data-ttu-id="83ec4-114">Computação otimizada</span><span class="sxs-lookup"><span data-stu-id="83ec4-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="83ec4-115">Fs, F</span><span class="sxs-lookup"><span data-stu-id="83ec4-115">Fs, F</span></span>             | <span data-ttu-id="83ec4-116">Alta relação de CPU/memória.</span><span class="sxs-lookup"><span data-stu-id="83ec4-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="83ec4-117">Boa para servidores web de tráfego médio, dispositivos de rede, processos de lote e servidores de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="83ec4-117">Good for medium traffic web servers, network appliances, batch processes, and application servers.</span></span>        |
| [<span data-ttu-id="83ec4-118">Memória otimizada</span><span class="sxs-lookup"><span data-stu-id="83ec4-118">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)         | <span data-ttu-id="83ec4-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="83ec4-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="83ec4-120">Alta relação de memória/CPU.</span><span class="sxs-lookup"><span data-stu-id="83ec4-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="83ec4-121">Excelente para servidores de banco de dados relacional, caches toolarge médios e análise de memória.</span><span class="sxs-lookup"><span data-stu-id="83ec4-121">Great for relational database servers, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="83ec4-122">Armazenamento otimizado</span><span class="sxs-lookup"><span data-stu-id="83ec4-122">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)        | <span data-ttu-id="83ec4-123">Ls</span><span class="sxs-lookup"><span data-stu-id="83ec4-123">Ls</span></span>                | <span data-ttu-id="83ec4-124">Alta taxa de transferência de disco e de E/S.</span><span class="sxs-lookup"><span data-stu-id="83ec4-124">High disk throughput and IO.</span></span> <span data-ttu-id="83ec4-125">Ideal para Big Data, SQL e bancos de dados NoSQL.</span><span class="sxs-lookup"><span data-stu-id="83ec4-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="83ec4-126">GPU</span><span class="sxs-lookup"><span data-stu-id="83ec4-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="83ec4-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="83ec4-127">NV, NC</span></span>            | <span data-ttu-id="83ec4-128">Máquinas virtuais especializadas, destinadas para renderização gráfica e edição de vídeo pesadas.</span><span class="sxs-lookup"><span data-stu-id="83ec4-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="83ec4-129">Disponível com uma ou várias GPUs.</span><span class="sxs-lookup"><span data-stu-id="83ec4-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="83ec4-130">Computação de alto desempenho</span><span class="sxs-lookup"><span data-stu-id="83ec4-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="83ec4-131">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="83ec4-131">H, A8-11</span></span>          | <span data-ttu-id="83ec4-132">Nossas máquinas virtuais de CPU mais rápidas e potentes com adaptadores de rede de alta taxa de transferência (RDMA) opcionais.</span><span class="sxs-lookup"><span data-stu-id="83ec4-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br> 

- <span data-ttu-id="83ec4-133">Para obter informações sobre os preços de saudação vários tamanhos, consulte [preços das máquinas virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span><span class="sxs-lookup"><span data-stu-id="83ec4-133">For information about pricing of hello various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span></span> 
- <span data-ttu-id="83ec4-134">limites de toosee geral em VMs do Azure, consulte [assinatura do Azure e limites de serviço, cotas e restrições](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="83ec4-134">toosee general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="83ec4-135">Os custos de armazenamento são calculados separadamente com base nas páginas usadas na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="83ec4-135">Storage costs are calculated separately based on used pages in hello storage account.</span></span> <span data-ttu-id="83ec4-136">Para obter detalhes, [Preço de Armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="83ec4-136">For details, [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>
- <span data-ttu-id="83ec4-137">Saiba mais sobre como as [ACUs (unidade de computação do Azure)](acu.md) podem ajudar você a comparar o desempenho de computação entre SKUs do Azure.</span><span class="sxs-lookup"><span data-stu-id="83ec4-137">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>



## <a name="rest-api"></a><span data-ttu-id="83ec4-138">API Rest</span><span class="sxs-lookup"><span data-stu-id="83ec4-138">Rest API</span></span>

<span data-ttu-id="83ec4-139">Para obter informações sobre como usar tooquery da API REST de saudação de tamanhos de VM, consulte a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="83ec4-139">For information on using hello REST API tooquery for VM sizes, see hello following:</span></span>

- [<span data-ttu-id="83ec4-140">Listar os tamanhos de máquina virtual disponíveis para redimensionamento</span><span class="sxs-lookup"><span data-stu-id="83ec4-140">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [<span data-ttu-id="83ec4-141">Listar os tamanhos de máquina virtual disponíveis para uma assinatura</span><span class="sxs-lookup"><span data-stu-id="83ec4-141">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [<span data-ttu-id="83ec4-142">Listar os tamanhos de máquina virtual disponíveis em um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="83ec4-142">List available virtual machine sizes in an availability set</span></span>](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a><span data-ttu-id="83ec4-143">ACU</span><span class="sxs-lookup"><span data-stu-id="83ec4-143">ACU</span></span>

<span data-ttu-id="83ec4-144">Saiba mais sobre como as [ACUs (unidade de computação do Azure)](acu.md) podem ajudar você a comparar o desempenho de computação entre SKUs do Azure.</span><span class="sxs-lookup"><span data-stu-id="83ec4-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83ec4-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="83ec4-145">Next steps</span></span>

<span data-ttu-id="83ec4-146">Saiba mais sobre Olá diferentes tamanhos de VM que estão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="83ec4-146">Learn more about hello different VM sizes that are available:</span></span>
- [<span data-ttu-id="83ec4-147">Propósito geral</span><span class="sxs-lookup"><span data-stu-id="83ec4-147">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="83ec4-148">Computação otimizada</span><span class="sxs-lookup"><span data-stu-id="83ec4-148">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="83ec4-149">Memória otimizada</span><span class="sxs-lookup"><span data-stu-id="83ec4-149">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="83ec4-150">Armazenamento otimizado</span><span class="sxs-lookup"><span data-stu-id="83ec4-150">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="83ec4-151">GPU otimizada</span><span class="sxs-lookup"><span data-stu-id="83ec4-151">GPU optimized</span></span>](sizes-gpu.md)
- [<span data-ttu-id="83ec4-152">Computação de alto desempenho</span><span class="sxs-lookup"><span data-stu-id="83ec4-152">High performance compute</span></span>](sizes-hpc.md)



