---
title: "aaaSet um cofre para o servidor físico tooAzure de replicação usando o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas de saudação necessário tooset a um tooAzure de servidores físicos do cofre tooreplicate usando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99f2605-f417-4995-be77-5323136b814f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 988928e3ece31116823f132cc39223fe44443468
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-tooazure"></a>Etapa 6: Configurar um cofre para tooAzure de replicação de servidor físico


Este artigo descreve como tooset um cofre. Criar cofre Olá e especifique o que você deseja tooreplicate do seu local local tooAzure, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.


Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a>Selecionar uma meta de proteção

Selecione o que você deseja tooreplicate, e onde você deseja tooreplicate para.

1. Clique em **Cofres dos Serviços de Recuperação** > cofre.
2. No hello recurso de Menu, clique em **recuperação de Site** > **preparar a infraestrutura** > **objetivo de proteção**.
3. Em **objetivo de proteção**, selecione **tooAzure** > **não virtualizados/outros**.


## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 7: configurar a origem e destino](physical-walkthrough-source-target.md)
