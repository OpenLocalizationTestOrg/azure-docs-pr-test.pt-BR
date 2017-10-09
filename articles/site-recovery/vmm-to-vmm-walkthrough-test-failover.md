---
title: "aaaRun um failover de teste para o site secundário do Hyper-V VM replicação tooa com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como toorun um failover de teste para a VM do Hyper-V replicação tooa System Center VMM secundário do site com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a3fd11ce-65a1-4308-8435-45cf954353ef
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: a60411541c2db001c573735bcb0d651f6618f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-tooa-secondary-site"></a>Etapa 10: Executar um failover de teste para o site secundário do Hyper-V replicação tooa


Após habilitar a replicação para máquinas virtuais de Hyper-V (VMs) [do Azure Site Recovery](site-recovery-overview.md), use toorun este artigo um failover de teste. Um failover de teste verifica se a replicação está funcionando, sem afetar o ambiente de produção. 


Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Antes de começar

- Quando você estiver ativando um failover de teste, você pode especificar a réplica de teste de saudação do hello rede toowhich que VMs se conectará. [Saiba mais](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) sobre opções de rede de saudação.
- É recomendável não escolher uma rede que foi selecionada durante o mapeamento de rede.
- Olá instruções neste artigo descrevem como toofail em uma única VM. Leia sobre [Criando planos de recuperação](site-recovery-create-recovery-plans.md) se você quiser toofail entre várias VMs juntos.
- Leia sobre [limitações para failovers de teste](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).
- Olá, endereço IP fornecido tooa VM durante o failover de teste é Olá deve receber o mesmo endereço IP que Olá VM para um failover planejado ou não planejado (presumindo que o endereço IP de saudação está disponível na rede de failover de teste de saudação). Se o endereço IP de saudação não está disponível na rede de failover de teste hello, Olá VM recebe outro endereço IP que está disponível na rede de failover de teste de saudação.
- Se você quiser toodo um failover de teste em sua rede de produção, para validação completa da máquina de conectividade de rede de ponta a ponta, observe que:
    - Olá que VM primária deve ser desligado quando você está fazendo o failover de teste de saudação. Caso contrário, duas VMs com hello mesma identidade estará sendo executada em hello mesma rede em hello simultaneamente. 
    - Se você fizer alterações tootest VMs, essas alterações serão perdidas quando você limpar Olá failover de teste. Essas alterações não são replicada toohello back VM primária.
    - Testando um uma rede de produção leva toodowntime para suas cargas de trabalho de produção. Peça aos usuários que não toouse aplicativo hello quando a análise de recuperação de desastres hello está em andamento.  


## <a name="run-a-test-failover-for-a-vm"></a>Executar um failover de teste para uma VM

1. toofail em uma única VM, em **itens replicados**, clique em Olá VM > **Failover de teste**.
2. Em **Failover de teste**, especificar como máquinas virtuais de teste será conectado toonetworks após o failover de teste de saudação. 
3. Clique em **Okey** toobegin Olá failover. Controlar o andamento da saudação **trabalhos** guia.
5. Após o failover estiver concluído, verifique se esse teste saudação inicial de VMs com êxito.
6. Quando terminar, clique em **failover de teste de limpeza** no plano de recuperação de saudação.
7. Em **notas**, gravar e salvar todas as observações associadas Olá failover de teste. Esta etapa exclui Olá virtual máquinas e redes que foram criadas durante o failover de teste.


## <a name="next-steps"></a>Próximas etapas

Depois que você testou implantação hello, saiba mais sobre outros tipos de [failover](site-recovery-failover.md).
