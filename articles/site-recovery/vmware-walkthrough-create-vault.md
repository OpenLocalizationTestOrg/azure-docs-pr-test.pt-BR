---
title: "aaaSet um cofre para VMware tooAzure de replicação usando o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas de saudação necessário tooset um cofre para VMware tooAzure de replicação usando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8bce940e-f19f-4418-8360-aee7b073519a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 8a7755a6c9a3f55f241c615e425285bc4b782493
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-vmware-replication-tooazure"></a>Etapa 7: Configurar um cofre para VMware tooAzure de replicação


Este artigo descreve como tooset até um cofre e especifique o que você deseja tooreplicate de sua localização no local, tooAzure usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.


Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a>Selecionar uma meta de proteção

Selecione o que você deseja tooreplicate, e onde você deseja tooreplicate para.

1. Clique em **Cofres dos Serviços de Recuperação** > cofre.
2. No hello recurso de Menu, clique em **recuperação de Site** > **preparar a infraestrutura** > **objetivo de proteção**.
3. Em **objetivo de proteção**, selecione **tooAzure** > **Sim, com VMware vSphere hipervisor**.



## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 8: configurar a origem e destino](vmware-walkthrough-source-target.md)
