---
title: "arquitetura de saudação aaaReview para o site secundário do Hyper-V replicação tooa com o Azure Site Recovery | Microsoft Docs"
description: "Este artigo fornece uma visão geral da arquitetura de saudação para replicar máquinas virtuais do Hyper-V tooa secundário System Center VMM site local com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 07099161-4cc7-4f32-8eb9-2a71bbf0750b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 0de4b4e8601116c73e6fd710597ce4e561884368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooa-secondary-site"></a>Etapa 1: Revisar arquitetura Olá para o site secundário do Hyper-V replicação tooa

Este artigo descreve os componentes de saudação e processos envolvidos ao replicar máquinas de virtuais (VMs) Hyper-V nas nuvens do System Center Virtual Machine Manager (VMM), site VMM secundário tooa usando Olá local [Azure Site Recovery](site-recovery-overview.md)serviço Olá portal do Azure.

Lançar os comentários na parte inferior deste artigo ou de saudação do hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="architectural-components"></a>Componentes de arquitetura

Aqui está o que você precisa para a replicação de site VMM secundário de tooa VMs Hyper-V.

**Componente** | **Localidade** | **Detalhes**
--- | --- | ---
**As tabelas** | Assinatura no Azure. | Crie um cofre de serviços de recuperação no hello assinatura do Azure, tooorchestrate e gerenciar a replicação entre os locais do VMM.
**Servidor VMM** | Você precisa de locais primário e secundário para o VMM. | É recomendável um servidor do VMM no site primário hello e um no site secundário Olá 
**Servidor Hyper-V** |  Um ou mais servidores Hyper-V host nas nuvens de saudação primários e secundários do VMM. | Dados são replicados entre Olá servidores primários e secundários Hyper-V host via LAN hello ou VPN, usando a autenticação Kerberos ou certificados.  
**VMs Hyper-V** | No servidor de host do Hyper-V. | servidor de host de origem Olá deve ter pelo menos uma VM que você deseja tooreplicate.

## <a name="replication-process"></a>Processo de replicação

1. Configurar Olá conta do Azure, crie um cofre de serviços de recuperação e especificar o que você deseja tooreplicate.
2. Configurar o hello origem e destino as configurações de replicação, que inclui a instalação Olá provedor Azure Site Recovery em servidores do VMM e o agente de serviços de recuperação do Microsoft Azure Olá em cada host Hyper-V.
3. Você criar uma política de replicação para a fonte de saudação nuvem do VMM. política de saudação é aplicado tooall as VMs localizadas nos hosts na nuvem de saudação.
4. Habilitar replicação para cada VMM e ocorre a replicação inicial de uma VM acordo com as configurações de saudação que você escolher.
5. Após a replicação inicial, a replicação de alterações delta começa. As alterações acompanhadas para um item são mantidas em um arquivo .hrl.


![Tooon local no local](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a>Processo de failover e failback

1. Você pode executar um [failover](site-recovery-failover.md) planejado ou não planejado entre sites locais. Se você executar um failover planejado, máquinas virtuais de origem são encerrados tooensure sem perda de dados.
2. Você pode fazer o failover de um único computador ou criar [planos de recuperação](site-recovery-create-recovery-plans.md) tooorchestrate failover de várias máquinas.
4. Se você executar um failover não planejado tooa site secundário, depois de executar failover em máquinas Olá no local secundário Olá não está habilitado para proteção ou replicação. Se você tiver executado um failover planejado, após o failover hello, as máquinas no local secundário Olá são protegidas.
5. Em seguida, você confirmar Olá failover toostart acessando Olá carga de trabalho da réplica Olá VM.
6. Quando seu site primário está disponível novamente, você pode iniciar tooreplicate replicação inversa da saudação site secundário toohello primário. Replicação inversa coloca máquinas virtuais de saudação em um estado protegido, mas o datacenter secundário Olá ainda é local ativo hello.
7. site primário do hello toomake em local ativo Olá novamente, você iniciar um failover planejado de tooprimary secundário, seguido de outra replicação inversa.



## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 2: Examinar Olá pré-requisitos e limitações](vmm-to-vmm-walkthrough-prerequisites.md).
