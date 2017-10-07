---
title: "aaaSet uma política de replicação para tooAzure de replicação de VM do VMware com o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas de saudação tooset uma política de replicação é necessário ao replicar máquinas virtuais do VMware tooAzure armazenamento"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 12870f3f98a4dd412221b817581403cd4bf7a76d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-vmware-vm-replication-tooazure"></a>Etapa 9: Configurar uma política de replicação para tooAzure de replicação de VM do VMware


Este artigo descreve como tooset uma política de replicação quando você estiver replicando máquinas virtuais do VMware tooAzure usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.


Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="configure-a-policy"></a>Configurar uma política

Obtenha uma rápida visão geral em vídeo antes de começar:
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. toocreate uma nova política de replicação, clique em **infra-estrutura de recuperação de Site** > **políticas de replicação** > **+ política de replicação**.
2. Em **Criar política de replicação**, especifique um nome de política.
3. Em **limite de RPO**, especifique o limite RPO hello. Esse valor especifica com que frequência os pontos de recuperação de dados são criados. Um alerta será gerado se a replicação contínua exceder esse limite.
4. Em **retenção de ponto de recuperação**, especifique quanto tempo (em horas) é uma janela de retenção Olá para cada ponto de recuperação. Máquinas virtuais replicadas podem ser recuperados tooany ponto em uma janela. A retenção horas tem suporte para máquinas de too24 replicado toopremium armazenamento e 72 horas para o armazenamento padrão.
5. Em **Frequência do instantâneo consistente com o aplicativo**, especifique com que frequência (em minutos) os pontos de recuperação contendo instantâneos consistentes com aplicativos serão criados. Clique em **Okey** toocreate política de saudação.

    ![Política de replicação](./media/vmware-walkthrough-replication/gs-replication2.png)
8. Quando você cria uma nova política automaticamente associado com o servidor de configuração de saudação. Por padrão, uma política de correspondência é criada automaticamente para failback. Por exemplo, se hello política de replicação é **política rep** diretiva de failback hello serão **representante de diretiva de failback**. Essa política não é usada até você iniciar um failback do Azure.

## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 10: instalar o serviço de mobilidade Olá](vmware-walkthrough-install-mobility.md)
