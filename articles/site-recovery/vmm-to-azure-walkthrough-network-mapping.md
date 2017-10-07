---
title: "mapeamento de rede aaaConfigure para replicar máquinas virtuais do Hyper-V no VMM nuvens tooAzure com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como o mapeamento de rede tooconfigure ao replicar máquinas virtuais do Hyper-V no VMM nuvens tooAzure com o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 081a9fdb0ffa4114099e9bcb9c1b1e43ad26ecbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-tooazure"></a>Etapa 9: Configurar o mapeamento de rede para tooAzure de replicação (com o VMM) do Hyper-V

Depois de configurar Olá [as configurações de replicação de origem e destino](vmm-to-azure-walkthrough-source-target.md), use toomap de mapeamento de rede Este artigo tooconfigure entre redes VM do VMM local e redes do Azure.

Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Antes de começar

- Saiba mais sobre [mapeamento de rede](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).
- [Preparar VMM para mapeamento de rede](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping). 
- Verifique se que máquinas virtuais no servidor do VMM Olá são conectados tooa rede VM e que você criou pelo menos uma rede virtual do Azure. Várias redes VM podem ser mapeado tooa única rede do Azure.

## <a name="configure-mapping"></a>Configurar o mapeamento

Configure o mapeamento da seguinte maneira:

1. Em **infra-estrutura de recuperação de Site** > **mapeamentos de rede** > **mapeamento de rede**, clique em Olá **+ de mapeamento de rede**  ícone.

    ![Mapeamento de rede](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. Em **Adicionar mapeamento de rede**, selecione servidor VMM de origem Olá, e **Azure** como destino de saudação.
3. Verifique se a assinatura hello e modelo de implantação de saudação após o failover.
4. Em **rede de origem**, selecione rede VM do local de origem de saudação desejado toomap da lista de saudação associada ao servidor do VMM hello.
5. Em **rede de destino**, selecione Olá rede do Azure no qual réplica VMs do Azure serão localizadas quando eles são criados. Em seguida, clique em **OK**.

    ![Mapeamento de rede](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

Veja o que acontece quando começa o mapeamento de rede:

* Máquinas virtuais existentes na rede VM de origem de saudação são conectados toohello rede de destino quando iniciar o mapeamento. Nova rede VM de origem para toohello conectado VMs estão conectados toohello mapeadas de rede do Azure quando a replicação ocorre.
* Se você modificar um mapeamento de rede existente, máquinas virtuais de réplica se conectar usando Olá novas configurações.
* Se a rede de destino Olá possui várias sub-redes e uma dessas sub-redes tem Olá mesmo nome da sub-rede na qual máquina de virtual de origem hello está localizado, Olá máquina de virtual de réplica se conecta a sub-rede de destino toothat após o failover.
* Se não houver nenhuma sub-rede de destino com um nome correspondente, Olá VM conecta toohello primeira sub-rede na rede de saudação.



## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 10: criar uma política de replicação](vmm-to-azure-walkthrough-replication.md)
