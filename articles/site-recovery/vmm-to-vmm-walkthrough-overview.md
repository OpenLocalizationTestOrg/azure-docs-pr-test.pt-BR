---
title: "aaaReplicate VMs Hyper-V tooa site VMM secundário com o Azure Site Recovery | Microsoft Docs"
description: "Fornece uma visão geral para replicar máquinas virtuais do Hyper-V tooa site VMM secundário usando Olá portal do Azure."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 476ca82a-8f5c-4498-9dcf-e1011d60ed59
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 90e44bfc2237dfa7646fb2b7b1e533a7f6d83c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a>Replicar máquinas virtuais Hyper-V no site tooa VMM secundário nuvens do VMM

> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-vmm-to-vmm.md)
> * [Portal clássico](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell – Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Este artigo fornece uma visão geral das etapas necessárias tooreplicate máquinas de virtuais de Hyper-V (VMs) gerenciadas em nuvens do System Center Virtual Machine Manager (VMM), local de VMM secundário tooa, locais de saudação usando [Azure Site Recovery](site-recovery-overview.md)em Olá portal do Azure.

Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-hello-scenario-architecture"></a>Etapa 1: Analisar a arquitetura de cenário Olá

Antes de iniciar a implantação, examine a arquitetura de cenário hello e certifique-se de que você compreenda todos os componentes de saudação precisar toodeploy.

Vá muito[etapa 1: revisar arquitetura Olá](vmm-to-vmm-walkthrough-architecture.md).

## <a name="step-2-review-prerequisites-and-limitations"></a>Etapa 2: Analisar os pré-requisitos e as limitações

Certifique-se de que você compreenda os pré-requisitos de implantação hello e limitações.

**Pré-requisitos do Azure**: você precisa de uma assinatura Microsoft Azure e serviços de recuperação do Azure cofre, tooorchestrate e gerenciar a replicação.
**Servidores do VMM no local e os hosts do Hyper-V**: verifique se os servidores VMM e os hosts do Hyper-V são compatíveis e se estão preparados para a implantação do Site Recovery.

Vá muito[etapa 2: verificar os pré-requisitos e limitações](vmm-to-vmm-walkthrough-prerequisites.md).

## <a name="step-3-plan-networking"></a>Etapa 3: Planejar a rede

É necessário toodo alguns tooensure que você pode configurar o mapeamento de rede entre redes de VM do VMM quando você implanta o cenário de saudação de planejamento da rede.

Vá muito[etapa 3: planejar a rede](vmm-to-vmm-walkthrough-network.md).


## <a name="step-4-prepare-vmm-and-hyper-v"></a>Etapa 4: Preparar o VMM e o Hyper-V

Prepare servidores VMM hello e hosts Hyper-V para implantação da recuperação de Site.

Vá muito[etapa 4: preparar servidores locais](vmm-to-vmm-walkthrough-vmm-hyper-v.md).

## <a name="step-5-set-up-a-vault"></a>Etapa 5: Configurar um cofre

Configurar um cofre dos Serviços de Recuperação. cofre Olá contém definições de configuração e coordena a replicação.

[Etapa 5: Configurar um cofre](vmm-to-vmm-walkthrough-create-vault.md).

## <a name="step-6-set-up-source-and-target-settings"></a>Etapa 6: Definir as configurações de origem e de destino

Configure locais de VMM de replicação de origem e destino de saudação. Adicionar o cofre do hello VMM servidores toohello e baixar arquivos de instalação Olá para componentes do Site Recovery. Execute a instalação do provedor Azure Site Recovery no servidor do VMM hello. A instalação instala Olá provedor no servidor do VMM hello e registra o servidor de saudação no cofre de saudação. Instale o agente de serviços de recuperação do Microsoft hello em cada host Hyper-V.

Vá muito[etapa 6: definir configurações de origem e destino Olá](vmm-to-vmm-walkthrough-source-target.md).

## <a name="step-7-configure-network-mapping"></a>Etapa 7: configurar o mapeamento de rede

Mapear redes de VM do VMM nos locais de origem e destino hello. Após o failover, máquinas virtuais são criadas na rede de destino Olá essa rede VM de origem do maps toohello em qual Olá VM do Hyper-V de origem está localizado.

Vá muito[etapa 7: Configurar mapeamento de rede](vmm-to-vmm-walkthrough-network-mapping.md).


## <a name="step-8-set-up-a-replication-policy"></a>Etapa 8: Configurar uma política de replicação

Especifica como as VMs serão replicadas entre os locais do VMM.

Vá muito[etapa 8: configurar uma política de replicação](vmm-to-vmm-walkthrough-replication.md).


## <a name="step-9-enable-replication-for-vms"></a>Etapa 9: Habilitar a replicação para VMs

Selecione VMs Olá deseja tooreplicate. Habilitar uma VM para o site secundário do toohello de replicação inicial de saudação do replicação gatilhos, seguido por replicação delta em andamento.

Vá muito[etapa 9: habilitar replicação](vmm-to-vmm-walkthrough-enable-replication.md).


## <a name="step-10-run-a-test-failover"></a>Etapa 10: Executar um failover de teste

Execute um toomake de failover de teste se que tudo está funcionando conforme o esperado.

Vá muito[etapa 10: executar um failover de teste](vmm-to-vmm-walkthrough-test-failover.md).
