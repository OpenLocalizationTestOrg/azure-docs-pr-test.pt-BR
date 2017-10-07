---
title: "aaaSet um cofre para VM do Azure repliction entre regiões com o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas de saudação necessário tooset um cofre para a replicação entre regiões do Azure usando o Azure Site Recovery do Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 40472189-3d80-4963-b175-8bddcbc2f61f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 9959c59c7ea57114763f13bf060404ddd267ba80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-a-vault-for-azure-tooazure-replication"></a>Etapa 4: Configurar um cofre para replicação tooAzure do Azure

Depois de [Planejando redes](azure-to-azure-walkthrough-network.md), use este tooset artigo um cofre, para máquinas virtuais (VMs) do Azure replicando tooanother região do Azure, usando Olá [Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.

- Quando você terminar de artigo hello, você deve ter um cofre de serviços de recuperação configurado.
- Lançar os comentários na parte inferior da saudação deste artigo, ou fazer perguntas no hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



>[!NOTE]
>
> Atualmente, a replicação de VM do Azure está em versão prévia.




## <a name="create-a-vault"></a>Criar um cofre

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> É recomendável que você crie Olá Cofre de serviços de recuperação no local de saudação onde você deseja que seu tooreplicate VMs. Por exemplo, se o local de destino é hello central nos, criar hello cofre no **centro dos EUA**.


## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 5: habilitar a replicação](azure-to-azure-walkthrough-enable-replication.md)
