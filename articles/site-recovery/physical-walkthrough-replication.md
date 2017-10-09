---
title: "aaaSet uma política de replicação para o servidor físico tooAzure de replicação com o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas de hello, você precisará tooset uma política de replicação ao replicar o armazenamento de tooAzure de servidores físicos usando o serviço do Azure Site Recovery Olá no local"
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
ms.openlocfilehash: d6bdeeffc24ffc8eaba24311f7c76452edb65648
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy-for-physical-server-replication-tooazure"></a>Etapa 8: Configurar uma política de replicação para o servidor físico tooAzure de replicação


Este artigo descreve como tooset uma política de replicação quando você estiver replicando tooAzure de servidores físicos do Windows/Linux usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.


Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="configure-a-policy"></a>Configurar uma política

1. Clique em **Infraestrutura do Site Recovery** > **Políticas de Replicação** > **+Política de Replicação**.
2. Em **Criar política de replicação**, especifique um nome de política.
3. Em **limite de RPO**, especifique o limite RPO hello. Esse valor indica com que frequência os pontos de recuperação de dados são criados. Um alerta será gerado se a replicação contínua exceder esse limite.
4. Em **retenção de ponto de recuperação**, especifique quanto tempo (em horas) é uma janela de retenção Olá para cada ponto de recuperação. Máquinas virtuais replicadas podem ser recuperados tooany ponto em uma janela. A retenção horas tem suporte para máquinas de too24 replicado toopremium armazenamento e 72 horas para o armazenamento padrão.
5. Em **Frequência do instantâneo consistente com o aplicativo**, especifique com que frequência (em minutos) os pontos de recuperação contendo instantâneos consistentes com aplicativos serão criados. Clique em **Okey** toocreate política de saudação.

    ![Política de replicação](./media/physical-walkthrough-replication/gs-replication2.png)
8. Quando você cria uma nova política automaticamente associado com o servidor de configuração de saudação. Por padrão, uma política de correspondência é criada automaticamente para failback. Por exemplo, se hello política de replicação é **política rep** diretiva de failback hello serão **representante de diretiva de failback**. Essa política não é usada até você iniciar um failback do Azure.

## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 9: Instale o serviço de mobilidade Olá](physical-walkthrough-install-mobility.md)
