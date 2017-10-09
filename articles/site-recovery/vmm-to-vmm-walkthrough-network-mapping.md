---
title: "redes aaaMap para o site secundário do Hyper-V VM replicação tooa com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como toomap redes ao replicar máquinas virtuais do Hyper-V tooa site VMM secundário com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 461b7c1c-ef61-4005-aeec-2324e727a3d0
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: d4f621df4ce08ae055bc6809daea0b71b76754ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-tooa-secondary-site"></a>Etapa 7: Mapear redes para o site secundário de tooa de replicação de VM do Hyper-V


Depois de configurar o [configurações de origem e destino](vmm-to-vmm-walkthrough-source-target.md) para a replicação de site tooa System Center Virtual Machine Manager (VMM) secundário (VMs) de máquinas virtuais Hyper-V, use esse mapeamento de rede do artigo tooconfigure virtual Hyper-v tooa de replicação de VM (máquina) secundário do site, usando [do Azure Site Recovery](site-recovery-overview.md).

Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Antes de começar

- Saiba mais sobre [mapeamento de rede](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) antes de iniciar.
- Verifique se máquinas virtuais nos servidores VMM estão conectados tooa rede VM.

## <a name="configure-network-mapping"></a>Configurar o mapeamento de rede

1. Em **Mapeamento de Rede** > **Mapeamentos de rede**, clique em **+Mapeamento de Rede**.
2. Em **Adicionar mapeamento de rede** , selecione a fonte de saudação e servidores do VMM de destino. redes VM Olá associados aos servidores do VMM Olá são recuperados.
3. Em **rede de origem**, selecione rede hello serão toouse de lista de saudação de redes VM associadas Olá servidor primário do VMM.
4. Em **rede de destino**, selecione rede hello serão toouse no servidor VMM secundário de saudação. Em seguida, clique em **OK**.

    ![Mapeamento de rede](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

Veja o que acontece quando começa o mapeamento de rede:

* Qualquer máquinas de virtuais de réplica existente que correspondem a rede VM de origem toohello será conectado toohello rede VM de destino.
* Novas máquinas virtuais que estão conectados toohello rede VM de origem será conectado toohello destino mapeadas rede após a replicação.
* Se você modificar um mapeamento existente com uma nova rede, máquinas virtuais de réplica serão conectadas usando Olá novas configurações.
* Se a rede de destino Olá tem várias sub-redes e uma dessas sub-redes tem Olá mesmo nome da sub-rede na qual máquina de virtual de origem hello está localizado, Olá máquina de virtual de réplica será conectada toothat sub-rede de destino após o failover. Se não houver nenhuma sub-rede de destino com um nome correspondente, Olá máquina de virtual será conectado toohello primeira sub-rede na rede de saudação.



## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 8: configurar uma política de replicação](vmm-to-vmm-walkthrough-replication.md).
