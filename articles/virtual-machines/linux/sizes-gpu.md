---
title: tamanhos de VM do Linux do aaaAzure - GPU | Microsoft Docs
description: "Lista Olá GPU otimizada tamanhos diferentes disponíveis para máquinas virtuais Linux no Azure."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: e98f720499be37df4048aeb513aa4f6b187b7335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="gpu-linux-vm-sizes"></a><span data-ttu-id="905ee-103">Tamanhos de VM Linux para GPU</span><span class="sxs-lookup"><span data-stu-id="905ee-103">GPU Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-gpu](../../../includes/virtual-machines-common-sizes-gpu.md)]


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

<span data-ttu-id="905ee-104">Para etapas de verificação e instalação do driver, consulte [Instalação do driver na série N para Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="905ee-104">For driver installation and verification steps, see [N-series driver setup for Linux](n-series-driver-setup.md).</span></span>

[!INCLUDE [virtual-machines-n-series-considerations](../../../includes/virtual-machines-n-series-considerations.md)]

* <span data-ttu-id="905ee-105">Não é recomendável instalar o servidor ou outros sistemas que usam o driver de nouveau Olá no Ubuntu NC VMs.</span><span class="sxs-lookup"><span data-stu-id="905ee-105">We don't recommend installing X server or other systems that use hello nouveau driver on Ubuntu NC VMs.</span></span> <span data-ttu-id="905ee-106">Antes de instalar drivers de GPU NVIDIA, você precisa de driver do toodisable Olá nouveau.</span><span class="sxs-lookup"><span data-stu-id="905ee-106">Before installing NVIDIA GPU drivers, you need toodisable hello nouveau driver.</span></span>  

## <a name="other-sizes"></a><span data-ttu-id="905ee-107">Outros tamanhos</span><span class="sxs-lookup"><span data-stu-id="905ee-107">Other sizes</span></span>
- [<span data-ttu-id="905ee-108">Propósito geral</span><span class="sxs-lookup"><span data-stu-id="905ee-108">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="905ee-109">Computação otimizada</span><span class="sxs-lookup"><span data-stu-id="905ee-109">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="905ee-110">Memória otimizada</span><span class="sxs-lookup"><span data-stu-id="905ee-110">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="905ee-111">Armazenamento otimizado</span><span class="sxs-lookup"><span data-stu-id="905ee-111">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="905ee-112">Computação de alto desempenho</span><span class="sxs-lookup"><span data-stu-id="905ee-112">High performance compute</span></span>](sizes-hpc.md)

## <a name="next-steps"></a><span data-ttu-id="905ee-113">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="905ee-113">Next steps</span></span>
<span data-ttu-id="905ee-114">Saiba mais sobre como as [ACUs (unidade de computação do Azure)](acu.md) podem ajudar você a comparar o desempenho de computação entre SKUs do Azure.</span><span class="sxs-lookup"><span data-stu-id="905ee-114">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>