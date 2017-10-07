---
title: aaaPrepare recursos do Azure tooreplicate tooAzure VMs VMware usando o Azure Site Recovery local | Microsoft Docs
description: "Descreve o que você precisa em vigor no Azure antes de você inicia a replicação local VMs VMware tooAzure usando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 4e320d9b-8bb8-46bb-ba21-77c5d16748ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ac72fff0593783add789408ecfeb1812d70108b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-vmware-replication-tooazure"></a>Etapa 5: Preparar recursos do Azure para VMWare tooAzure de replicação


Use instruções Olá tooprepare este artigo Azure recursos para que você pode replicar tooAzure de máquinas locais usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço.

Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Antes de começar

Verifique se você leu Olá [pré-requisitos](vmware-walkthrough-prerequisites.md)

## <a name="set-up-an-azure-account"></a>Configurar uma conta do Azure

- Obter uma [conta do Microsoft Azure](http://azure.microsoft.com/).
- Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
- Verificar regiões Olá com suporte para a recuperação de Site, em disponibilidade geográfica em [detalhes de preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
- Saiba mais sobre [preços de recuperação de Site](site-recovery-faq.md#pricing)e obter Olá [detalhes de preços](https://azure.microsoft.com/pricing/details/site-recovery/).



## <a name="set-up-an-azure-network"></a>Configurar uma rede do Azure

- Configure uma rede do Azure. As VMs do Azure são colocadas nessa rede quando são criadas após o failover.
- Recuperação de site no portal do Azure de saudação pode usar redes configuradas no [Gerenciador de recursos](../resource-manager-deployment-model.md), ou no modo clássico.
- rede Olá deve estar no hello Cofre de serviços de recuperação com a mesma região Olá
- Saiba mais sobre os [preços de rede virtual](https://azure.microsoft.com/pricing/details/virtual-network/).
- Saiba mais sobre a [Conectividade de VM do Azure](site-recovery-network-design.md) após o failover.


## <a name="set-up-an-azure-storage-account"></a>Configure uma conta de armazenamento do Azure

- Recuperação de site replica o armazenamento de tooAzure máquinas locais. Máquinas virtuais do Azure são criados a partir do armazenamento Olá após o failover.
- [Configure uma conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) para os dados replicados.
- Recuperação de site no portal do Azure de saudação pode usar contas de armazenamento configuradas no Gerenciador de recursos ou em modo clássico.
- conta de armazenamento Olá pode ser padrão ou [premium](../storage/common/storage-premium-storage.md).
- Se você configurar uma conta premium, também precisará de uma conta padrão adicional para dados de log.


## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 6: recursos do VMware preparar](vmware-walkthrough-prepare-vmware.md)
