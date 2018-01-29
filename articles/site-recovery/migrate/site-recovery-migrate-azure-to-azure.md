---
title: "Migrar VMs IaaS do Azure entre regiões do Azure | Microsoft Docs"
description: "Use o Azure Site Recovery para migrar máquinas virtuais IaaS do Azure de uma região do Azure para outra."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8a29e0d9-0010-4739-972f-02b8bdf360f6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/27/2017
ms.author: raynew
ms.openlocfilehash: f645150aa7b93ebbd98899cc8fdd495dfeaf3076
ms.sourcegitcommit: 29bac59f1d62f38740b60274cb4912816ee775ea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/29/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a>Migrar máquinas virtuais IaaS do Azure entre regiões do Azure com o Azure Site Recovery

Bem-vindo ao Azure Site Recovery! Use este artigo se você deseja migrar VMs do Azure entre regiões do Azure.
>[!NOTE]
>
> Para replicar VMs do Azure para outra região para necessidades de migração e de recuperação de desastre, consulte [este documento](../site-recovery-azure-to-azure.md). Atualmente, a replicação do Site Recovery para máquinas virtuais do Azure está em versão prévia.


## <a name="prerequisites"></a>Pré-requisitos
Aqui está o que você precisa para essa implantação:

* **Máquinas virtuais IaaS**: as VMs que você deseja migrar. Você pode migrar essas VMs tratando-as como computadores físicos.

## <a name="deployment-steps"></a>Etapas de implantação.
Esta seção descreve as etapas de implantação no novo Portal do Azure.

1. [Crie um cofre](../site-recovery-azure-to-azure.md#create-a-recovery-services-vault).
2. [Habilite a replicação]../(site-recovery-azure-to-azure.md) para as VMs que você deseja migrar e escolha o Azure como a origem.
  >[!NOTE]
  >
  > No momento, não há suporte para replicação nativa de VMs do Azure usando Managed Disks. Você pode usar a opção "Físico para o Azure" [neste documento](../site-recovery-vmware-to-azure.md) para migrar VMs com Managed Disks.
3. [Executar um failover](../site-recovery-failover.md). Depois que a replicação inicial for concluída, você poderá executar um failover de uma região do Azure para outra. Se preferir, você pode criar um plano de recuperação e executar um failover para migrar várias máquinas virtuais entre regiões. [Saiba mais](../site-recovery-create-recovery-plans.md) sobre planos de recuperação.

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre outros cenários de replicação em [O que é o Azure Site Recovery?](../site-recovery-overview.md)
