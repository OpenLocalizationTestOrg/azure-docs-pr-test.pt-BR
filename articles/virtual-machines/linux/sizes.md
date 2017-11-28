---
title: Tamanhos da VM Linux no Azure | Microsoft Docs
description: "Lista os tamanhos diferentes disponíveis de máquinas virtuais do Linux no Azure."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: da681171-f045-4c80-a5a9-d8bd47964673
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: fe7a92901ae25aa99ef71f09c416e6c6ad30d39b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="sizes-for-linux-virtual-machines-in-azure"></a><span data-ttu-id="2a462-103">Tamanhos das máquinas virtuais do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="2a462-103">Sizes for Linux virtual machines in Azure</span></span>
<span data-ttu-id="2a462-104">Este artigo descreve os tamanhos e as opções disponíveis de máquinas virtuais do Azure que você pode usar para executar seus aplicativos Linux e cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2a462-104">This article describes the available sizes and options for the Azure virtual machines you can use to run your Linux apps and workloads.</span></span> <span data-ttu-id="2a462-105">Ele também fornece considerações de implantação a serem observadas ao planejar o uso desses recursos.</span><span class="sxs-lookup"><span data-stu-id="2a462-105">It also provides deployment considerations to be aware of when you're planning to use these resources.</span></span> <span data-ttu-id="2a462-106">Este artigo também está disponível para [máquinas virtuais do Windows](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2a462-106">This article is also available for [Windows virtual machines](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


| <span data-ttu-id="2a462-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="2a462-107">Type</span></span>                     | <span data-ttu-id="2a462-108">Tamanhos</span><span class="sxs-lookup"><span data-stu-id="2a462-108">Sizes</span></span>           |    <span data-ttu-id="2a462-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="2a462-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="2a462-110">Propósito geral</span><span class="sxs-lookup"><span data-stu-id="2a462-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="2a462-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7,</span><span class="sxs-lookup"><span data-stu-id="2a462-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7,</span></span>  | <span data-ttu-id="2a462-112">Relação equilibrada de CPU/memória.</span><span class="sxs-lookup"><span data-stu-id="2a462-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="2a462-113">Ideal para teste e desenvolvimento, bancos de dados pequenos a médios e servidores Web de tráfego baixo a médio.</span><span class="sxs-lookup"><span data-stu-id="2a462-113">Ideal for testing and development, small to medium databases, and low to medium traffic web servers.</span></span> |
| [<span data-ttu-id="2a462-114">Computação otimizada</span><span class="sxs-lookup"><span data-stu-id="2a462-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="2a462-115">Fs, F</span><span class="sxs-lookup"><span data-stu-id="2a462-115">Fs, F</span></span>             | <span data-ttu-id="2a462-116">Alta relação de CPU/memória.</span><span class="sxs-lookup"><span data-stu-id="2a462-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="2a462-117">Boa para servidores Web de tráfego médio, dispositivos de rede, processos de lote e servidores de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2a462-117">Good for medium traffic web servers, network appliances, bath processes, and application servers.</span></span>        |
| [<span data-ttu-id="2a462-118">Memória otimizada</span><span class="sxs-lookup"><span data-stu-id="2a462-118">Memory optimized</span></span>](sizes-memory.md)         | <span data-ttu-id="2a462-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="2a462-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="2a462-120">Alta relação de memória/CPU.</span><span class="sxs-lookup"><span data-stu-id="2a462-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="2a462-121">Ótima para servidores de banco de dados relacionais, caches médios a grandes e análises na memória.</span><span class="sxs-lookup"><span data-stu-id="2a462-121">Great for relational database servers, medium to large caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="2a462-122">Armazenamento otimizado</span><span class="sxs-lookup"><span data-stu-id="2a462-122">Storage optimized</span></span>](sizes-storage.md)        | <span data-ttu-id="2a462-123">Ls</span><span class="sxs-lookup"><span data-stu-id="2a462-123">Ls</span></span>                | <span data-ttu-id="2a462-124">Alta taxa de transferência de disco e de E/S.</span><span class="sxs-lookup"><span data-stu-id="2a462-124">High disk throughput and IO.</span></span> <span data-ttu-id="2a462-125">Ideal para Big Data, SQL e bancos de dados NoSQL.</span><span class="sxs-lookup"><span data-stu-id="2a462-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="2a462-126">GPU</span><span class="sxs-lookup"><span data-stu-id="2a462-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="2a462-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="2a462-127">NV, NC</span></span>            | <span data-ttu-id="2a462-128">Máquinas virtuais especializadas, destinadas para renderização gráfica e edição de vídeo pesadas.</span><span class="sxs-lookup"><span data-stu-id="2a462-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="2a462-129">Disponível com uma ou várias GPUs.</span><span class="sxs-lookup"><span data-stu-id="2a462-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="2a462-130">Computação de alto desempenho</span><span class="sxs-lookup"><span data-stu-id="2a462-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="2a462-131">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="2a462-131">H, A8-11</span></span>          | <span data-ttu-id="2a462-132">Nossas máquinas virtuais de CPU mais rápidas e potentes com adaptadores de rede de alta taxa de transferência (RDMA) opcionais.</span><span class="sxs-lookup"><span data-stu-id="2a462-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br>

- <span data-ttu-id="2a462-133">Para obter informações sobre os preços dos vários tamanhos, consulte [Preços de máquinas virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="2a462-133">For information about pricing of the various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span> 
- <span data-ttu-id="2a462-134">Para ver a disponibilidade de tamanhos de VM nas regiões do Azure, confira [Produtos disponíveis por região](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="2a462-134">For availability of VM sizes in Azure regions, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
- <span data-ttu-id="2a462-135">Para ver os limites gerais em VMs do Azure, consulte [Limites de assinatura e serviços do Azure, cotas e restrições](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="2a462-135">To see general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="2a462-136">Saiba mais sobre como as [ACUs (unidade de computação do Azure)](../windows/acu.md) podem ajudar você a comparar o desempenho de computação entre SKUs do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a462-136">Learn more about how [Azure compute units (ACU)](../windows/acu.md) can help you compare compute performance across Azure SKUs.</span></span>


## <a name="rest-api"></a><span data-ttu-id="2a462-137">API Rest</span><span class="sxs-lookup"><span data-stu-id="2a462-137">Rest API</span></span>

<span data-ttu-id="2a462-138">Para obter informações sobre como usar a API REST para consulta de tamanhos de VM, confira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="2a462-138">For information on using the REST API to query for VM sizes, see the following:</span></span>

- [<span data-ttu-id="2a462-139">Listar os tamanhos de máquina virtual disponíveis para redimensionamento</span><span class="sxs-lookup"><span data-stu-id="2a462-139">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [<span data-ttu-id="2a462-140">Listar os tamanhos de máquina virtual disponíveis para uma assinatura</span><span class="sxs-lookup"><span data-stu-id="2a462-140">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [<span data-ttu-id="2a462-141">Listar os tamanhos de máquina virtual disponíveis em um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="2a462-141">List available virtual machine sizes in an availability set</span></span>](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a><span data-ttu-id="2a462-142">ACU</span><span class="sxs-lookup"><span data-stu-id="2a462-142">ACU</span></span>

<span data-ttu-id="2a462-143">Saiba mais sobre como as [ACUs (unidade de computação do Azure)](acu.md) podem ajudar você a comparar o desempenho de computação entre SKUs do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a462-143">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a462-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2a462-144">Next steps</span></span>

<span data-ttu-id="2a462-145">Saiba mais sobre os diferentes tamanhos de VM que estão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="2a462-145">Learn more about the different VM sizes that are available:</span></span>
- [<span data-ttu-id="2a462-146">Propósito geral</span><span class="sxs-lookup"><span data-stu-id="2a462-146">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="2a462-147">Computação otimizada</span><span class="sxs-lookup"><span data-stu-id="2a462-147">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="2a462-148">Memória otimizada</span><span class="sxs-lookup"><span data-stu-id="2a462-148">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="2a462-149">Armazenamento otimizado</span><span class="sxs-lookup"><span data-stu-id="2a462-149">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="2a462-150">GPU</span><span class="sxs-lookup"><span data-stu-id="2a462-150">GPU</span></span>](sizes-gpu.md)
- [<span data-ttu-id="2a462-151">Computação de alto desempenho</span><span class="sxs-lookup"><span data-stu-id="2a462-151">High performance compute</span></span>](sizes-hpc.md)



