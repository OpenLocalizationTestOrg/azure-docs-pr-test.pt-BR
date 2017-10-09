---
title: "aaaSet um cofre para tooAzure de replicação (sem o System Center VMM) do Hyper-V usando o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas de saudação necessário tooset um cofre para tooAzure de replicação do Hyper-V usando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a936b3e2-0dbe-47ac-a98e-5285d96dc786
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: e3ef8758faab36d19d0968d98a23105bed7830f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a>Etapa 7: configurar um cofre para replicação do Hyper-V

Este artigo descreve como tooset até um cofre e especifique o que você deseja tooreplicate de sua localização no local, tooAzure usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.


Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a>Selecionar uma meta de proteção

Selecione o que você deseja tooreplicate, e onde você deseja tooreplicate para.

1. Clique em **Cofres dos Serviços de Recuperação** > cofre.
2. No hello recurso de Menu, clique em **recuperação de Site** > **preparar a infraestrutura** > **objetivo de proteção**.
3. Em **objetivo de proteção**, selecione **tooAzure** > **Sim, com o Hyper-V**. Selecione **não** tooconfirm não estiver usando o VMM. 

    ![Escolher metas](./media/hyper-v-site-walkthrough-create-vault/choose-goals2.png)



## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 8: configurar a origem e destino](hyper-v-site-walkthrough-source-target.md)
