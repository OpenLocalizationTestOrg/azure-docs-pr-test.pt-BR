---
title: "mapeamento de rede aaaPlan para replicação de VM do Hyper-V com o Site Recovery | Microsoft Docs"
description: "Configure o mapeamento de rede para replicação de máquina virtual do Hyper-V de um tooAzure de datacenter local ou site secundário tooa."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: tysonn
ms.assetid: fcaa2f52-489d-4c1c-865f-9e78e000b351
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/23/2017
ms.author: raynew
ms.openlocfilehash: 86199b5840ea10fd33630bcc75d14340a49e01bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-network-mapping-for-hyper-v-vm-replication-with-site-recovery"></a>Mapeamento de plano de rede para replicação de Hyper-V VM com recuperação de Site



Este artigo ajuda você a toounderstand e planejar de rede mapeando durante a replicação de máquinas virtuais do Hyper-V tooAzure ou site secundário tooa, usando Olá [serviço Azure Site Recovery](site-recovery-overview.md).

Depois de ler este artigo lançar os comentários na parte inferior da saudação deste artigo ou questões técnicas Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="network-mapping-for-replication-tooazure"></a>Mapeamento de rede para replicação tooAzure

Mapeamento de rede é usado ao replicar tooAzure de VMs Hyper-V (gerenciados no VMM). O mapeamento de rede mapeia entre as redes de VM em um servidor VMM de origem e as redes do Azure de destino. Mapeamento Olá a seguir:

- **Conexão de rede**— garante que VMs do Azure replicados são rede mapeada toohello conectado. Todos os computadores que o failover em Olá mesmo rede pode se conectar tooeach outra, mesmo se eles failover em planos de recuperação diferente.
- **Gateway de rede**— se um gateway de rede é configurado na rede Azure de destino hello, as VMs podem se conectar a tooother em máquinas virtuais.

Observe que:

- Você mapeia uma fonte de tooan de rede VM VMM rede virtual do Azure.
- Após o failover de máquinas virtuais do Azure no Olá a rede de origem será rede virtual de destino mapeada toohello conectado.
- Novas VMs adicionados estão conectados a rede VM de origem toohello toohello mapeadas de rede do Azure quando a replicação ocorre.
- Se a rede de destino Olá possui várias sub-redes e uma dessas sub-redes tem Olá mesmo nome da sub-rede na qual máquina de virtual de origem hello está localizado, Olá máquina de virtual de réplica se conecta a sub-rede de destino toothat após o failover.
- Se não houver nenhuma sub-rede de destino com um nome correspondente, Olá VM conecta toohello primeira sub-rede na rede de saudação.


## <a name="network-mapping-for-replication-tooa-secondary-datacenter"></a>Mapeamento de rede para o datacenter secundário de tooa de replicação

Mapeamento de rede é usado ao replicar o datacenter secundário de tooa de VMs Hyper-V (gerenciado no System Center Virtual Machine Manager (VMM)). O mapeamento de rede mapeia entre as redes de VM em um servidor VMM de origem e as redes do Azure de destino. Mapeamento Olá a seguir:

- **Conexão de rede**— conecta VMs tooappropriate redes após o failover. VM de réplica Olá será conectado toohello rede de destino que é a rede de origem mapeado toohello.
- **O posicionamento ideal**— ideal casas Olá máquinas virtuais de réplica nos servidores de host do Hyper-V. Máquinas virtuais de réplica são colocadas em hosts que podem Olá acesso redes VM mapeadas.
- **Nenhum mapeamento de rede**— se você não configurar o mapeamento de rede, máquinas virtuais de réplica não será conectada tooany redes VM após o failover.

Observe que:

- Mapeamento de rede pode ser configurado entre redes VM em dois servidores do VMM ou em um único servidor do VMM se dois sites forem gerenciados pelo Olá mesmo servidor.
- Quando o mapeamento for configurado corretamente e a replicação está habilitada, uma VM no local primário Olá será conectado tooa rede e sua réplica no local de destino hello será conectada tooits mapeado rede.
-
- Se redes tem sido instaladas corretamente no VMM, quando você seleciona uma rede de VM de destino durante o mapeamento de rede, nuvens de origem do VMM Olá que usam a rede VM de origem Olá serão exibidas, juntamente com redes VM de destino disponíveis Olá em nuvens de destino de saudação que são usadas para proteção.
- Se a rede de destino Olá tem várias sub-redes e uma dessas sub-redes Olá mesmo nome como Olá sub-rede na qual Olá máquina virtual de origem está localizada, em seguida, Olá máquina virtual de réplica será conectada toothat sub-rede de destino após o failover. Se não houver nenhuma sub-rede de destino com um nome correspondente, Olá máquina de virtual será conectado toohello primeira sub-rede na rede de saudação.



### <a name="example"></a>Exemplo

Aqui está um exemplo tooillustrate esse mecanismo. Vamos usar uma organização com dois locais, Nova Iorque e Chicago.

**Localidade** | **Servidor VMM** | **Redes VM** | **Mapeado para**
---|---|---|---
Nova Iorque | VMM-NewYork| VMNetwork1-NewYork | TooVMNetwork1 mapeada-Chicago
 |  | VMNetwork2-NewYork | Não mapeado
Chicago | VMM-Chicago| VMNetwork1-Chicago | TooVMNetwork1-NewYork mapeada
 | | VMNetwork1-Chicago | Não mapeado

Neste exemplo:

- Quando uma máquina virtual de réplica é criada para qualquer máquina virtual que está conectada tooVMNetwork1-NewYork, ela será conectado tooVMNetwork1-Chicago.
- Quando uma máquina virtual de réplica é criada para VMNetwork2-NewYork ou VMNetwork2-Chicago, ele não será conectado tooany rede.

Aqui está como nuvens do VMM são configurados em nossa organização de exemplo e redes lógicas de saudação associados Olá nuvens.

#### <a name="cloud-protection-settings"></a>Configurações de proteção de nuvem

**Nuvem protegida** | **Protegendo a nuvem** | **Rede lógica (Nova Iorque)**  
---|---|---
GoldCloud1 | GoldCloud2 |
SilverCloud1| SilverCloud2 |
GoldCloud2 | <p>ND</p><p></p> | <p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p>
SilverCloud2 | <p>ND</p><p></p> | <p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p>

#### <a name="logical-and-vm-network-settings"></a>Configurações de rede lógica e de VM

**Localidade** | **Rede lógica** | **Rede VM associada**
---|---|---
Nova Iorque | LogicalNetwork1-NewYork | VMNetwork1-NewYork
Chicago | LogicalNetwork1-Chicago | VMNetwork1-Chicago
 | LogicalNetwork2Chicago | VMNetwork2-Chicago

#### <a name="target-network-settings"></a>Configurações de rede de destino

Com base nessas configurações, quando você seleciona a rede VM de destino hello, Olá a tabela a seguir mostra opções Olá que estarão disponíveis.

**Seleção** | **Nuvem protegida** | **Protegendo a nuvem** | **Rede de destino disponível**
---|---|---|---
VMNetwork1-Chicago | SilverCloud1 | SilverCloud2 | Disponível
 | GoldCloud1 | GoldCloud2 | Disponível
VMNetwork2-Chicago | SilverCloud1 | SilverCloud2 | Não disponível
 | GoldCloud1 | GoldCloud2 | Disponível


Se a rede de destino Olá tem várias sub-redes e uma dessas sub-redes Olá mesmo nome como Olá sub-rede na qual Olá máquina virtual de origem está localizada, em seguida, Olá máquina virtual de réplica será conectada toothat sub-rede de destino após o failover. Se não houver nenhuma sub-rede de destino com um nome correspondente, Olá máquina de virtual será conectado toohello primeira sub-rede na rede de saudação.


#### <a name="failback-behavior"></a>Comportamento de failback

toosee o que acontece no caso de saudação de failback (replicação inversa), vamos supor que a VMNetwork1-NewYork é mapeado tooVMNetwork1-Chicago, com hello configurações a seguir.


**Máquina virtual** | **Rede tooVM conectado**
---|---
VM1 | VMNetwork1-Rede
VM2 (réplica de VM1) | VMNetwork1-Chicago

Com essas configurações, vamos analisar o que acontece em alguns cenários possíveis.

**Cenário** | **Resultado**
---|---
Nenhuma alteração nas propriedades de rede Olá de VM-2 após o failover. | VM-1 permanece conectado toohello rede de origem.
As propriedades de rede de VM-2 são alteradas após o failover e ela é desconectada. | A VM-1 é desconectada.
Propriedades de rede de VM-2 são alteradas depois do failover e é conectado tooVMNetwork2-Chicago. | Se a VMNetwork2-Chicago não estiver mapeada, a VM-1 será desconectada.
O mapeamento de rede da VMNetwork1-Chicago é alterado. | VM-1 será conectado toohello de rede mapeada agora tooVMNetwork1-Chicago.



## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre [planejar a infraestrutura de rede Olá](site-recovery-network-design.md).
