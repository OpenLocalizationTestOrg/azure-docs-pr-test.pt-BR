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
# <a name="sizes-for-windows-virtual-machines-in-azure"></a>Tamanhos das máquinas virtuais do Windows no Azure

Este artigo descreve os tamanhos disponíveis hello e opções de saudação máquinas virtuais do Azure, você pode usar toorun seus aplicativos do Windows e cargas de trabalho. Ele também fornece toobe de considerações de implantação ciente de quando você estiver planejando toouse esses recursos.  Este artigo também está disponível para [máquinas virtuais Linux](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


| Tipo                     | Tamanhos           |    Descrição       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [Propósito geral](sizes-general.md)          | Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7 | Relação equilibrada de CPU/memória. Ideal para teste e desenvolvimento, toomedium pequeno de bancos de dados e servidores web com tráfego toomedium baixa. |
| [Computação otimizada](sizes-compute.md)        | Fs, F             | Alta relação de CPU/memória. Boa para servidores web de tráfego médio, dispositivos de rede, processos de lote e servidores de aplicativo.        |
| [Memória otimizada](../virtual-machines-windows-sizes-memory.md)         | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Alta relação de memória/CPU. Excelente para servidores de banco de dados relacional, caches toolarge médios e análise de memória.                 |
| [Armazenamento otimizado](../virtual-machines-windows-sizes-storage.md)        | Ls                | Alta taxa de transferência de disco e de E/S. Ideal para Big Data, SQL e bancos de dados NoSQL.                                                         |
| [GPU](sizes-gpu.md)            | NV, NC            | Máquinas virtuais especializadas, destinadas para renderização gráfica e edição de vídeo pesadas. Disponível com uma ou várias GPUs.       |
| [Computação de alto desempenho](sizes-hpc.md) | H, A8-11          | Nossas máquinas virtuais de CPU mais rápidas e potentes com adaptadores de rede de alta taxa de transferência (RDMA) opcionais. 

<br> 

- Para obter informações sobre os preços de saudação vários tamanhos, consulte [preços das máquinas virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows). 
- limites de toosee geral em VMs do Azure, consulte [assinatura do Azure e limites de serviço, cotas e restrições](../../azure-subscription-service-limits.md).
- Os custos de armazenamento são calculados separadamente com base nas páginas usadas na conta de armazenamento hello. Para obter detalhes, [Preço de Armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/).
- Saiba mais sobre como as [ACUs (unidade de computação do Azure)](acu.md) podem ajudar você a comparar o desempenho de computação entre SKUs do Azure.



## <a name="rest-api"></a>API Rest

Para obter informações sobre como usar tooquery da API REST de saudação de tamanhos de VM, consulte a seguir hello:

- [Listar os tamanhos de máquina virtual disponíveis para redimensionamento](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [Listar os tamanhos de máquina virtual disponíveis para uma assinatura](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [Listar os tamanhos de máquina virtual disponíveis em um conjunto de disponibilidade](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a>ACU

Saiba mais sobre como as [ACUs (unidade de computação do Azure)](acu.md) podem ajudar você a comparar o desempenho de computação entre SKUs do Azure.

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre Olá diferentes tamanhos de VM que estão disponíveis:
- [Propósito geral](sizes-general.md)
- [Computação otimizada](sizes-compute.md)
- [Memória otimizada](../virtual-machines-windows-sizes-memory.md)
- [Armazenamento otimizado](../virtual-machines-windows-sizes-storage.md)
- [GPU otimizada](sizes-gpu.md)
- [Computação de alto desempenho](sizes-hpc.md)



