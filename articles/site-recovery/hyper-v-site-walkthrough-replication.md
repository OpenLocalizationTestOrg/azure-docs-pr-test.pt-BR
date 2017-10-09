---
title: "aaaSet uma política de replicação para tooAzure de replicação (sem o System Center VMM) de VM do Hyper-V com o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas de saudação precisar tooset uma política de replicação durante a replicação de armazenamento de tooAzure de VMs Hyper-V"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 4bd7161f4a0f015da0ecf595fbc6861ede5d68b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-tooazure"></a>Etapa 9: Configurar uma política de replicação para tooAzure de replicação de VM do Hyper-V

Este artigo descreve como tooset uma política de replicação quando você estiver replicando tooAzure de VMs Hyper-V (sem o System Center VMM) usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.


Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="about-snapshots"></a>Sobre instantâneos

Hyper-V usa dois tipos de instantâneos — um instantâneo padrão que fornece um instantâneo incremental da saudação toda a máquina virtual e um instantâneo consistente com o aplicativo que usa um instantâneo point-in-time dos dados de aplicativo hello dentro da máquina virtual de saudação.
    - Instantâneos consistentes com o aplicativo usam tooensure Volume Shadow Copy Service (VSS) que os aplicativos estejam em um estado consistente quando Olá instantâneo é tirado.
    - Se você habilitar instantâneos consistentes com aplicativos, isso afetará o desempenho de saudação de aplicativos executados em máquinas virtuais de origem. Verifique se o valor de saudação definido é menor do que o número de saudação de pontos de recuperação adicionais que você configurar.

## <a name="set-up-a-replication-policy"></a>Configurar uma política de replicação

1. toocreate uma nova política de replicação, clique em **preparar infraestrutura** > **as configurações de replicação** > **+ criar e associar**.

    ![Rede](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. Em **Criar e associar política**, especifique um nome de política.
3. Em **frequência de cópia**, especifique com que frequência tooreplicate delta dados após a replicação inicial da saudação (a cada 30 segundos, 5 ou 15 minutos).

    > [!NOTE]
    > Uma frequência de segundo 30 não tem suporte durante a replicação de armazenamento toopremium. limitação de saudação é determinada pelo número de saudação de instantâneos por blob (100) com suporte pelo armazenamento premium. [Saiba mais](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).

4. Em **retenção de ponto de recuperação**, especifique em horas quanto tempo é uma janela de retenção Olá para cada ponto de recuperação. Máquinas virtuais podem ser recuperados tooany ponto dentro de uma janela.
5. Em **Frequência do instantâneo consistente com aplicativo**, especifique com que frequência (1 a 12 horas) são criados os pontos de recuperação que contêm instantâneos consistentes com o aplicativo.
6. Em **hora de início da replicação inicial**, especifique quando toostart Olá a replicação inicial. replicação Olá ocorre sobre a largura de banda de internet, portanto, talvez você queira tooschedule-lo fora do horário de ocupado. Em seguida, clique em **OK**.

    ![Política de replicação](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

Quando você cria uma nova política, ela está associada automaticamente com o site do Hyper-V hello. Você pode associar um site Hyper-V (e hello VMs nele) com várias políticas de replicação no **replicação** > nome da política > **associar o Site de Hyper-V**.



## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 10: habilitar a replicação](hyper-v-site-walkthrough-enable-replication.md)
