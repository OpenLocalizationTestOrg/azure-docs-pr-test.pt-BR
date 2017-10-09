---
title: "site secundário do aaaEnable Hyper-V replicação tooa com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como a replicação para máquinas virtuais do Hyper-V replicando tooa tooenable System Center VMM secundário do site com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a>Etapa 9: Habilitar o site secundário do tooa de replicação para máquinas virtuais do Hyper-V


Depois de configurar uma política de replicação, use o artigo tooenable replicação tooa System Center Virtual Machine Manager (VMM) site secundário para local Hyper-V máquinas virtuais (VM), usando [do Azure Site Recovery](site-recovery-overview.md).

Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="select-vms-tooreplicate"></a>Selecione tooreplicate de VMs

1. Clique em **Etapa 2: replicar aplicativo** > **Origem**. 

    ![Habilitar a replicação](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. Em **fonte**, selecione o servidor do VMM hello e Olá nuvem na qual Olá hosts Hyper-V que você deseja tooreplicate estão localizados. Em seguida, clique em **OK**.

    ![Habilitar a replicação](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. Em **destino**, verifique se Olá servidor secundário do VMM e a nuvem.
4. Em **máquinas virtuais**, selecione VMs Olá deseja tooprotect da lista de saudação.

    ![Habilitar Proteção da Máquina Virtual](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

Você pode acompanhar o progresso da saudação **Habilitar proteção** ação **trabalhos** > **trabalhos de recuperação de Site**. Depois de saudação **finalizar proteção** trabalho for concluído, Olá a replicação inicial está concluída e máquina virtual de saudação está pronta para failover.

Observe que:

- Você também pode habilitar a proteção para máquinas virtuais no console do VMM hello. Clique em **Habilitar proteção** na barra de ferramentas Olá nas propriedades de máquina virtual hello > **do Azure Site Recovery** guia.
- Depois de habilitar a replicação, você pode exibir propriedades para Olá VM em **itens duplicados**. Em Olá **Essentials** painel, você pode ver informações sobre a política de replicação Olá Olá VM e seu status. Clique em **Propriedades** para obter mais detalhes.

## <a name="onboard-existing-vms"></a>Integrar VMs existentes

Se você tiver máquinas virtuais existentes no VMM replicadas com a Réplica do Hyper-V, poderá carregá-las na replicação do Azure Site Recovery da seguinte maneira:

1. Verifique se o servidor Olá Hyper-V hospeda Olá que VM existente está localizado na nuvem primária hello e servidor Hyper-V Olá Olá máquina de virtual de réplica de hospedagem está localizado na nuvem secundária hello.
2. Certifique-se de que uma política de replicação é configurada para nuvem VMM primária de saudação.
3. Habilite a replicação para máquina virtual primária de saudação. Do Azure Site Recovery e o VMM Certifique-se de que hello mesmo host de réplica e máquina virtual for detectado e reutilizar o Azure Site Recovery e restabelecer a replicação usando Olá especificar configurações.


## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 10: executar um failover de teste](vmm-to-vmm-walkthrough-test-failover.md).
