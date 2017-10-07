---
title: tooAzure aaaMigrate com o Site Recovery | Microsoft Docs
description: "Este artigo fornece uma visão geral de migração de VMs e servidores físicos tooAzure com o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/05/2017
ms.author: raynew
ms.openlocfilehash: 6e65deee337c5371d441812ddb820dc8bc233684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-tooazure-with-site-recovery"></a>Migrar tooAzure com a recuperação de Site

Leia este artigo para uma visão geral do uso do serviço hello Azure Site Recovery para a migração de máquinas virtuais e servidores físicos.

Recuperação de site é um serviço do Azure que contribui com a estratégia BCDR tooyour, pela replicação de orquestração de servidores de locais físicos e máquinas virtuais toohello nuvem (Azure) ou datacenter secundário tooa. Quando ocorrem paralisações do local primário, você failover toohello local secundário tookeep aplicativos e cargas de trabalho disponíveis. Você não local primário tooyour voltar ao retornar toonormal operações. Saiba mais em [O que é Recuperação de Site?](site-recovery-overview.md) Você também pode usar a recuperação de Site toomigrate existente local cargas de trabalho tooAzure tooexpedite sua jornada de nuvem e disp Olá matriz de recursos que o Azure oferece.

Para uma visão geral de como tooperform de migração, consulte o vídeo toothis.
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/ASRHowTo-Video2-Migrate-Virtual-Machines-to-Azure/player]

Este artigo descreve a implantação no hello [portal do Azure](https://portal.azure.com). Olá [portal clássico do Azure](https://manage.windowsazure.com/) pode ser usado toomaintain existentes cofres da recuperação de Site, mas você não pode criar novos cofres.

Lança os comentários na parte inferior da saudação deste artigo. Perguntas técnicas Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="what-do-we-mean-by-migration"></a>O que queremos dizer por migração?

Você pode implantar a recuperação de Site para replicação de VMs locais e servidores físicos, tooAzure ou tooa site secundário. Replicar máquinas, o failover do site primário hello quando ocorrem paralisações e falharem-los site primário toohello voltar quando ele recuperará. Em adição toothis, você pode usar o Site Recovery toomigrate VMs e servidores físicos tooAzure, para que os usuários podem acessá-los como VMs do Azure. Migração envolve a replicação e o failover de saudação tooAzure de site primário e um gesto de concluir a migração.

## <a name="what-can-site-recovery-migrate"></a>O que o Site Recovery pode migrar?

Você pode:

- Migre cargas de trabalho em execução no local toorun de VMs Hyper-V, máquinas virtuais do VMware e servidores físicos, em VMs do Azure. Você também pode fazer a replicação completa e o failback nesse cenário.
- Migre [VMs IaaS do Azure](site-recovery-migrate-azure-to-azure.md) entre regiões do Azure. Atualmente, apenas a migração tem suporte nesse cenário, o que significa que não há suporte para failback.
- Migrar [instâncias do Windows AWS](site-recovery-migrate-aws-to-azure.md) tooAzure VMs de IaaS. Atualmente, apenas a migração tem suporte nesse cenário, o que significa que não há suporte para failback.

## <a name="migrate-on-premises-vms-and-physical-servers"></a>Migrar servidores físicos e VMs locais

toomigrate local VMs Hyper-V, máquinas virtuais do VMware e servidores físicos, siga quase Olá mesmo etapas usadas para a replicação normal.

1. Configurar um cofre dos Serviços de Recuperação
2. Configurar servidores de gerenciamento Olá necessário (VMware, o VMM, Hyper-V - dependendo do que você deseja toomigrate), adicioná-los toohello cofre e especifique as configurações de replicação.
3. Habilitar a replicação para Olá máquinas que você deseja toomigrate
4. Após a migração inicial do hello, execute um tooensure de failover de teste rápido que tudo está funcionando como deveria.
5. Após verificar se o ambiente de replicação está funcionando, você usa um failover planejado ou não, dependendo do [que tem suporte](site-recovery-failover.md) para seu cenário. Recomendamos que você use um failover planejado, quando possível.
6. Para a migração, você não precisa toocommit um failover ou excluí-lo. Em vez disso, você pode selecionar Olá **concluir a migração** opção para cada máquina que você deseja toomigrate.
     - Em **itens replicados**, clique com botão direito Olá VM e clique em **concluir a migração**. Clique em **Okey** toocomplete. Você pode acompanhar o progresso nas propriedades VM hello, no monitorando o trabalho de migração completa Olá no **trabalhos de recuperação de Site**.
     - Olá **concluir a migração** ação terminar o processo de migração hello, remove a replicação para máquina hello e interrompe a cobrança de recuperação de Site para a máquina de saudação.

![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

## <a name="migrate-between-azure-regions"></a>Migrar entre regiões do Azure

Você pode migrar VMs do Azure entre regiões usando o Site Recovery. Nesse cenário, apenas a migração tem suporte. Em outras palavras, você pode replicar máquinas virtuais do Azure de saudação e o failover tooanother região, mas você não pode realizar failback. Neste cenário que você configurar um cofre de serviços de recuperação, implantar uma replicação de toomanage do servidor de configuração local, adicioná-lo toohello cofre e especifique as configurações de replicação. Habilitar a replicação para failover de teste de máquinas de saudação desejado toomigrate e executar uma rápida. Em seguida, execute um failover não planejado com hello **concluir a migração** opção.

## <a name="migrate-aws-tooazure"></a>Migrar AWS tooAzure

Você pode migrar AWS instâncias tooAzure VMs. Nesse cenário, apenas a migração tem suporte. Em outras palavras, você pode replicar instâncias AWS hello e o failover tooAzure, mas você não pode realizar failback. Instâncias AWS são tratadas no hello mesma maneira que os servidores físicos para fins de migração. Configurar um cofre de serviços de recuperação, implantar uma replicação de toomanage do servidor de configuração local, adicioná-lo toohello cofre e especifique as configurações de replicação. Habilitar a replicação para failover de teste de máquinas de saudação desejado toomigrate e executar uma rápida. Em seguida, execute um failover não planejado com hello **concluir a migração** opção.




## <a name="next-steps"></a>Próximas etapas

- [Migrar máquinas virtuais do VMware tooAzure](site-recovery-vmware-to-azure.md)
- [Migrar máquinas virtuais do Hyper-V no VMM nuvens tooAzure](site-recovery-vmm-to-azure.md)
- [Migrar máquinas virtuais do Hyper-V sem tooAzure do VMM](site-recovery-hyper-v-site-to-azure.md)
- [Migrar VMs do Azure entre regiões do Azure](site-recovery-migrate-azure-to-azure.md)
- [Migrar AWS instâncias tooAzure](site-recovery-migrate-aws-to-azure.md)
- [Preparar máquinas migradas tooenable replicação](site-recovery-azure-to-azure-after-migration.md) tooanother região para necessidades de recuperação de desastres.
- Inicie a proteção de suas cargas de trabalho ao [replicar máquinas virtuais do Azure.](site-recovery-azure-to-azure.md)
