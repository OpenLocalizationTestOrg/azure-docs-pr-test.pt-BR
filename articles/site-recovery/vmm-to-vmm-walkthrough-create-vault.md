---
title: "aaaCreate um cofre para o site secundário do Hyper-V replicação tooa com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como toocreate um cofre ao replicar máquinas virtuais do Hyper-V tooa System Center VMM secundário do site com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ff65dbfb-cb26-410e-ab48-76971625db08
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 96ee09cbf2376a5089b9efa09dc7ab3fb7d472cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-create-a-vault-for-hyper-v-replication-tooa-secondary-site"></a>Etapa 5: Criar um cofre do site secundário do Hyper-V replicação tooa

Depois de preparar local [/clusters de hosts Hyper-V e de servidores do System Center Virtual Machine Manager (VMM)](vmm-to-vmm-walkthrough-vmm-hyper-v.md) para o site secundário usando o Hyper-V replicação tooa [do Azure Site Recovery](site-recovery-overview.md), você pode criar um Cofre de serviços de recuperação e selecione Olá replicação cenário.

Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a>Escolher um objetivo de proteção

Selecione o que você deseja tooreplicate e onde você deseja tooreplicate para.

1. Clique em **Site Recovery** > **Etapa 1: Preparar a Infraestrutura** > **Meta de proteção**.
2. Selecione **toorecovery site**e selecione **Sim, com o Hyper-V**.
3. Selecione **Sim** tooindicate você estiver usando os hosts do VMM toomanage Olá Hyper-V.
4. Selecione **Sim** se você tiver um servidor VMM secundário. Se você estiver implantando a replicação entre nuvens em um único servidor VMM, clique em **Não**. Em seguida, clique em **OK**.

    ![Escolher metas](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 6: configurar a origem de replicação hello e de destino](vmm-to-vmm-walkthrough-source-target.md).
