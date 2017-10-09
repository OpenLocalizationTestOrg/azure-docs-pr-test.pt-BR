---
title: "aaaPrerequisites para tooAzure de replicação usando o Azure Site Recovery | Microsoft Docs"
description: "Este artigo resume os pré-requisitos para replicar máquinas virtuais e máquinas físicas tooAzure usando o serviço do Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: jwhit
editor: tysonn
ms.assetid: e24eea6c-50a7-4cd5-aab4-2c5c4d72ee2d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/01/2017
ms.author: rajanaki
ms.openlocfilehash: c66cea8b097a872bae57e7b42e659e58c4b0b1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
#  <a name="prerequisites-for-replicating-azure-virtual-machines-tooanother-region-by-using-azure-site-recovery"></a>Pré-requisitos para replicar máquinas virtuais do Azure tooanother região usando o Azure Site Recovery

> [!div class="op_single_selector"]
> * [Replicar do tooAzure do Azure](site-recovery-azure-to-azure-prereq.md)
> * [Replicar do local tooAzure](site-recovery-prereq.md)

Olá serviço Azure Site Recovery contribui com a estratégia de recuperação (BCDR) de desastre e continuidade de negócios tooyour ao orquestrar a:
* Replicação de máquinas virtuais do Azure tooanother região do Azure.
* Replicação do local físico máquinas virtuais e servidores tooAzure ou tooa datacenter secundário. 

Quando ocorrem paralisações do local primário, você pode fazer failover tooa local secundário tookeep aplicativos e cargas de trabalho disponíveis. Você pode fazer o local primário tooyour back quando ele retorna toonormal operações. Para mais informações sobre o Site Recovery, consulte [O que é Site Recovery?](site-recovery-overview.md).

Este artigo resume Olá de pré-requisitos necessários toobegin replicação de recuperação de Site de tooAzure local.

Lançar os comentários na parte inferior de saudação do artigo hello ou questões técnicas Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="azure-requirements"></a>Requisitos do Azure

**Requisito** | **Detalhes**
--- | ---
**Conta do Azure** | Uma conta do [Microsoft Azure](http://azure.microsoft.com/) .<br/><br/> Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
**Serviço do Site Recovery** | Para obter mais informações sobre os preços do Site Recovery, consulte [Preços do Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/). É recomendável que você crie um cofre de serviços de recuperação no destino Olá região do Azure que você deseja toouse como um local de recuperação de desastres. Por exemplo, se sua fonte de VMs estão sendo executados no Leste dos EUA, e deseja tooreplicate tooCentral, recomendamos que você crie Olá cofre no centro dos EUA.|
**Capacidade do Azure** | Para o destino Olá região do Azure que você deseja toouse como seu local de recuperação de desastres, você precisa toohave uma assinatura com capacidade suficiente para máquinas virtuais, contas de armazenamento e componentes de rede. Você pode contatar o suporte tooadd mais capacidade.
**Diretrizes de armazenamento** | Certifique-se de que você siga Olá [diretrizes de armazenamento](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) para sua fonte de virtual do Azure máquinas tooavoid eventuais problemas de desempenho. Se você seguir as configurações padrão de saudação, recuperação de Site cria contas de armazenamento Olá necessárias com base na configuração de fonte de saudação. Se você personalizar e selecione suas próprias configurações, certifique-se de que você siga Olá [alvos de escalabilidade para discos de máquina virtual](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
**Diretrizes de rede** | É necessário ter conectividade de saída de hello toowhitelist da sua VM do Azure para intervalos de IP ou URLs específicas. Para obter mais detalhes, consulte toohello [diretrizes para replicar máquinas virtuais do Azure de rede](site-recovery-azure-to-azure-networking-guidance.md) artigo.
**VM do Azure** | Certifique-se de que todos os certificados raiz hello mais recentes estão presentes no hello Windows ou a VM do Linux. Se os certificados raiz mais recentes de saudação não estiverem presentes, Olá VM não pode ser registrado tooSite recuperação devido a restrições de toosecurity.

>[!NOTE]
>Para obter mais detalhes sobre o suporte para configurações específicas, leia Olá [matriz de suporte](site-recovery-support-matrix-azure-to-azure.md).

## <a name="next-steps"></a>Próximas etapas
- Saiba mais sobre as [Diretrizes de rede para replicar máquinas virtuais do Azure](site-recovery-azure-to-azure-networking-guidance.md).
- Inicie a proteção de suas cargas de trabalho ao [replicar máquinas virtuais do Azure](site-recovery-azure-to-azure.md).
