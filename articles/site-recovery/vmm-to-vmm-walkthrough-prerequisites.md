---
title: "pré-requisitos do aaaReview Olá para o Hyper-V replicação tooa VMM site secundário com o Azure Site Recovery | Microsoft Docs"
description: "Descreve os pré-requisitos de saudação para replicar máquinas virtuais do Hyper-V tooa site VMM secundário com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 21ff0545-8be5-4495-9804-78ab6e24add6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 1bd945fdda36c3cce5d159209abbd3c98a7e3682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-and-limitations-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a>Etapa 2: Examinar os pré-requisitos de hello e limitações para o site tooa VMM secundário replicação VM Hyper-V


Depois que você tiver examinado Olá [arquitetura de cenário](vmm-to-vmm-walkthrough-architecture.md), leia este toomake artigo se você compreender os pré-requisitos de implantação hello, ao replicar máquinas virtuais de Hyper-V no local (VMs) gerenciados no System Center Virtual Nuvens de Machine Manager (VMM), tooa secundário do site usando [Azure Site Recovery](site-recovery-overview.md) em Olá portal do Azure.

Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites-and-limitations"></a>Pré-requisitos e limitações

**Requisito** | **Detalhes**
--- | ---
**As tabelas** | Uma assinatura do [Microsoft Azure](http://azure.microsoft.com/).<br/><br/> Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).<br/><br/> [Saiba mais](https://azure.microsoft.com/pricing/details/site-recovery/) sobre os preços da Recuperação de Site.<br/><br/> Verificar regiões Olá com suporte para a recuperação de Site, em disponibilidade geográfica em [detalhes de preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
**Servidores do VMM** | Recomendamos que você tenha dois servidores do VMM, um site primário hello e um em Olá secundário.<br/><br/> Há suporte para a replicação entre nuvens em um único servidor VMM.<br/><br/> Servidores do VMM devem estar executando pelo menos System Center 2012 SP1 com atualizações mais recentes de saudação.<br/><br/> Servidores VMM precisam de acesso à Internet.
**Nuvens do VMM** | Cada servidor do VMM deve ter em uma ou mais nuvens, e todas as nuvens devem ter perfil de capacidade do Hyper-V Olá definida. <br/><br/>As nuvens devem conter um ou mais grupos de hosts do VMM.<br/><br/> Se você tiver apenas um servidor do VMM, ele precisa de pelo menos duas nuvens, tooact como primário e secundário.
**Hyper-V** | Servidores Hyper-V devem estar executando pelo menos o Windows Server 2012 com a função hello Hyper-V, e ter Olá as últimas atualizações instaladas.<br/><br/> Um servidor Hyper-V deve conter uma ou mais VMs.<br/><br/>  Servidores de host Hyper-V devem estar localizados em grupos de host em nuvens do VMM Olá primários e secundários.<br/><br/> Se você estiver executando o Hyper-V em um cluster no Windows Server 2012 R2, instale a [atualização 2961977](https://support.microsoft.com/kb/2961977)<br/><br/> Se estiver executando o Hyper-V em um cluster no Windows Server 2012, o agente de cluster não será criado automaticamente se você tiver um cluster baseado em endereço IP estático. Configure manualmente o agente do cluster hello. [Leia mais](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).<br/><br/> Os servidores do Hyper-V precisam de acesso à Internet.




## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 3: planejar a rede](vmm-to-vmm-walkthrough-network.md).
