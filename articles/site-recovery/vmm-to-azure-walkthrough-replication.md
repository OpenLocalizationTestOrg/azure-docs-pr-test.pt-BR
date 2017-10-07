---
title: "aaaSet uma política de replicação para tooAzure de replicação de VM do Hyper-V (com o VMM) com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como tooset uma política de replicação para tooAzure de replicação de VM do Hyper-V (com o VMM) com o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ee808b20-324b-4198-b831-edb65b95e8b7
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: e1579fde559ca34eca19a01e740fec28a0df2f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-tooazure"></a>Etapa 10: Configurar uma política de replicação para tooAzure de replicação (com o VMM) de VM do Hyper-V


Depois de configurar o [mapeamento de rede](vmm-to-azure-walkthrough-network-mapping.md), use este artigo de tooconfigure uma política de replicação T\tooreplicate máquinas virtuais de Hyper-V gerenciados no System Center Virtual Machine Manager (VMM) nuvens tooAzure local, usando Olá [ O Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.

Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="create-a-policy"></a>Criar uma política

1. toocreate uma nova política de replicação, clique em **preparar infraestrutura** > **as configurações de replicação** > **+ criar e associar**.

    ![Rede](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. Em **Criar e associar política**, especifique um nome de política.
3. Em **frequência de cópia**, especifique com que frequência tooreplicate delta dados após a replicação inicial da saudação (a cada 30 segundos, 5 ou 15 minutos).

    > [!NOTE]
    >  Uma frequência de segundo 30 não tem suporte durante a replicação de armazenamento toopremium. limitação de saudação é determinada pelo número de saudação de instantâneos por blob (100) com suporte pelo armazenamento premium. [Saiba mais](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. Em **retenção de ponto de recuperação**, especifique, em horas, quanto tempo uma janela de retenção Olá será possível para cada ponto de recuperação. Computadores protegidos podem ser recuperados tooany ponto dentro de uma janela.
5. Em **Frequência do instantâneo consistente com aplicativo**, especifique com que frequência (1 a 12 horas) são criados os pontos de recuperação que incluam instantâneos consistentes com aplicativos. Hyper-V usa dois tipos de instantâneos — um instantâneo padrão que fornece um instantâneo incremental da saudação toda a máquina virtual e um instantâneo consistente com o aplicativo que usa um instantâneo point-in-time dos dados de aplicativo hello dentro da máquina virtual de saudação. Instantâneos consistentes com o aplicativo usam tooensure Volume Shadow Copy Service (VSS) que os aplicativos estejam em um estado consistente quando Olá instantâneo é tirado. Observe que, se você habilitar instantâneos consistentes com aplicativos, isso afetará Olá desempenho de aplicativos executados em máquinas virtuais de origem. Verifique se o valor de saudação definido é menor do que o número de saudação de pontos de recuperação adicionais que você configurar.
6. Em **hora de início da replicação inicial**, indicar quando toostart Olá a replicação inicial. replicação Olá ocorre sobre a largura de banda de internet, portanto, talvez você queira tooschedule-lo fora do horário de ocupado.
7. Em **criptografar dados armazenados no Azure**, especifique se tooencrypt dados rest no armazenamento do Azure. Em seguida, clique em **OK**.

    ![Política de replicação](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. Quando você cria uma nova política está associado automaticamente Olá nuvem do VMM. Clique em **OK**. Você pode associar nuvens do VMM adicionais (e Olá VMs neles) com esta política de replicação em **replicação** > nome da política > **associar VMM nuvem**.

    ![Política de replicação](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 11: habilitar a replicação](vmm-to-azure-walkthrough-enable-replication.md)
