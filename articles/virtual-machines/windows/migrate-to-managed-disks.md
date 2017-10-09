---
title: aaaMigrate VMs do Azure tooManaged discos | Microsoft Docs
description: "Migre máquinas virtuais do Azure criadas usando discos não gerenciados em contas de armazenamento toouse discos gerenciado."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 29420f13c4ffd5b25726e0ef1aafe89347286a89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-vms-toomanaged-disks-in-azure"></a>Migrar máquinas virtuais do Azure tooManaged discos no Azure

Discos gerenciado do Azure simplifica o gerenciamento de armazenamento, removendo a necessidade de saudação tooseparately gerenciar contas de armazenamento.  Também é possível migrar sua toobenefit de discos de tooManaged VMs do Azure existente de confiabilidade de VMs em um conjunto de disponibilidade. Garante que os discos Olá das diferentes VMs em um conjunto de disponibilidade será suficientemente isolados de cada outro tooavoid ponto único de falhas. Coloca automaticamente discos de diferentes VMs em um conjunto de disponibilidade em diferentes unidades de escala de armazenamento (carimbos) que limita o impacto de saudação de falhas de unidade de escala de armazenamento único causado devido a falhas de software e toohardware.
Com base em suas necessidades, você pode escolher entre dois tipos de opções de armazenamento:

- Os [Managed Disks Premium](../../storage/common/storage-premium-storage.md) são uma mídia de armazenamento com base em unidade de estado sólido (SSD), que fornece alto desempenho, suporte a disco de baixa latência para máquinas virtuais com cargas de trabalho de E/S intensas. Você pode tirar proveito de velocidade de saudação e o desempenho desses discos por discos Migrando do tooPremium gerenciados.

- [Discos padrão gerenciado](../../storage/common/storage-standard-storage.md) usar a mídia de armazenamento de disco rígido (HDD) com base e são mais adequados para desenvolvimento/teste e outras cargas de trabalho de acesso incomum que são menos confidencial variabilidade de tooperformance.

Você pode migrar discos tooManaged nos seguintes cenários:

| Migrar...                                            | Link da documentação                                                                                                                                                                                                                                                                  |
|----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Converter VMs autônomas e máquinas virtuais em um discos de toomanaged do conjunto de disponibilidade   | [Converter os discos toouse gerenciado VMs](convert-unmanaged-to-managed-disks.md) |
| Uma única VM de clássico tooResource Manager em discos gerenciados     | [Migrar uma única VM](migrate-single-classic-to-resource-manager.md)  | 
| Todas as VMs de saudação em uma rede virtual do clássico tooResource Manager em discos gerenciados     | [Migrar recursos de IaaS de tooResource clássico Manager](migration-classic-resource-manager-ps.md) e, em seguida, [converter uma VM de discos de toomanaged de discos não gerenciado](convert-unmanaged-to-managed-disks.md) | 






## <a name="plan-for-hello-conversion-toomanaged-disks"></a>Planejar para conversão de saudação tooManaged discos

Esta seção Ajuda toomake Olá melhor decisão sobre tipos de VM e disco.


## <a name="location"></a>Local

Escolha um local onde o Azure Managed Disks estão disponíveis. Se você estiver movendo tooPremium gerenciados discos, também Verifique se o armazenamento Premium está disponível na região Olá onde você está planejando toomove para. Confira [Serviços do Azure por região](https://azure.microsoft.com/regions/#services) para obter informações atualizadas sobre as localizações disponíveis.

## <a name="vm-sizes"></a>Tamanhos de VM

Se você estiver migrando tooPremium gerenciados discos, você tem tooupdate tamanho de saudação do hello VM tooPremium tamanho com capacidade de armazenamento disponível na região Olá onde a VM está localizada. Examine os tamanhos de VM Olá que são compatíveis com um armazenamento Premium. especificações de tamanho de VM do Azure Olá são listadas na [tamanhos das máquinas virtuais](sizes.md).
Examine as características de desempenho de saudação de máquinas virtuais que funcionam com o armazenamento Premium e escolha o tamanho VM mais apropriado hello mais adequada para sua carga de trabalho. Certifique-se de que há largura de banda suficiente disponível no seu tráfego de disco VM toodrive hello.

## <a name="disk-sizes"></a>Tamanhos do disco

**Managed Disks Premium**

Há sete tipos de discos gerenciados premium que podem ser usados com sua VM e cada um tem IOPs e limites de taxa de transferência específicos. Leve em consideração esses limites ao escolher Olá tipo de disco Premium para sua VM com base nas necessidades de saudação do seu aplicativo em termos de capacidade, escalabilidade e desempenho e cargas de pico.

| Tipo de discos premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Tamanho do disco           | 128 GB| 512 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| IOPS por disco       | 120   | 240   | 500   | 2.300              | 5.000              | 7500              | 7500              | 
| Taxa de transferência por disco | 25 MB por segundo  | 50 MB por segundo  | 100 MB por segundo | 150 MB por segundo | 200 MB por segundo | 250 MB por segundo | 250 MB por segundo |

**Managed Disks Standard**

Há sete tipos de discos gerenciados standard que podem ser usados com sua VM. Cada um deles tem uma capacidade diferente, mas com os mesmos limites de taxa de transferência e IOPS. Escolha o tipo de saudação de discos gerenciados padrão com base nas necessidades de capacidade de saudação do seu aplicativo.

| Tipo de disco Standard  | S4               | S6               | S10              | S20              | S30              | S40              | S50              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| Tamanho do disco           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1024 GB (1 TB)   | 2048 GB (2TB)    | 4095 GB (4 TB)   | 
| IOPS por disco       | 500              | 500              | 500              | 500              | 500              | 500             | 500              | 
| Taxa de transferência por disco | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 

## <a name="disk-caching-policy"></a>Política de cache de disco

**Managed Disks Premium**

Por padrão, a política de cache de disco é *somente leitura* para todos os discos de dados Premium, de hello e *leitura-gravação* para o disco do sistema operacional Premium Olá anexado toohello VM. Esta configuração é recomendável tooachieve Olá o desempenho ideal para IOs seu aplicativo. Para discos de dados de gravação intensa ou somente gravação (como arquivos de log do SQL Server), desabilite o cache de disco para que possa obter o melhor desempenho do aplicativo.

## <a name="pricing"></a>Preços

Saudação de revisão [preços para discos gerenciados](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Preços de discos gerenciados do Premium são igual a saudação discos de Premium não gerenciado. No entanto, os preços do Standard Managed Disks são diferentes dos preços do Standard Unmanaged Disks.



## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre [Managed Disks](managed-disks-overview.md)
