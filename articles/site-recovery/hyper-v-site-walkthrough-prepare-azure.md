---
title: aaaPrepare recursos do Azure tooreplicate VMs Hyper-V (sem o System Center VMM) tooAzure usando o Azure Site Recovery | Microsoft Docs
description: "Descreve o que você precisa em vigor no Azure antes de iniciar a replicação tooAzure de VMs Hyper-V (sem VMM) usando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 28fa722c-675e-4637-98eb-7ccbf3806d69
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: f659e300c39253b0eaf7218bee9d39b11682edb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-tooazure"></a>Etapa 5: Preparar recursos do Azure para tooAzure de replicação do Hyper-V

Use as instruções de saudação em tooprepare este artigo Azure recursos para que você possa replicar locais VMs Hyper-V (sem o System Center VMM) tooAzure usando Olá [Azure Site Recovery](site-recovery-overview.md) serviço.

Depois de ler este artigo, postar os comentários na parte inferior da saudação ou questões técnicas Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Antes de começar

Verifique se você leu Olá [pré-requisitos](hyper-v-site-walkthrough-prerequisites.md)

## <a name="set-up-an-azure-account"></a>Configurar uma conta do Azure

- Obter uma [conta do Microsoft Azure](http://azure.microsoft.com/).
- Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
- Verificar regiões Olá com suporte para a recuperação de Site, em disponibilidade geográfica em [detalhes de preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
- Saiba mais sobre [preços de recuperação de Site](site-recovery-faq.md#pricing)e obter Olá [detalhes de preços](https://azure.microsoft.com/pricing/details/site-recovery/).


## <a name="set-up-an-azure-network"></a>Configurar uma rede do Azure

- Configure uma rede do Azure. As VMs do Azure são colocadas nessa rede quando são criadas após o failover.
- rede Olá deve estar no hello Cofre de serviços de recuperação com a mesma região Olá
- Recuperação de site no portal do Azure de saudação pode usar redes configuradas no [Gerenciador de recursos](../resource-manager-deployment-model.md), ou no modo clássico.
- É recomendável configurar uma rede antes de começar. Se você não fizer isso, você precisa toodo-lo durante a implantação da recuperação de Site.
- Saiba mais sobre os [preços de rede virtual](https://azure.microsoft.com/pricing/details/virtual-network/).


## <a name="set-up-an-azure-storage-account"></a>Configure uma conta de armazenamento do Azure

- Recuperação de site replica o armazenamento de tooAzure máquinas locais. Máquinas virtuais do Azure são criados a partir do armazenamento Olá após o failover.
- Configurar um padrão/premium [conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold dados replicados tooAzure.
- [Armazenamento Premium](../storage/common/storage-premium-storage.md) é normalmente usado para máquinas virtuais que precisam de um desempenho de e/s consistentemente alto e baixa latência toohost e/s intensivas cargas de trabalho.
- Se você quiser toouse dados replicados de um toostore de conta premium, você também precisa de um armazenamento padrão toostore replicação logs de conta de captura contínua altera dados tooon locais.
- Dependendo do modelo de recurso Olá desejar toouse para o failover de máquinas virtuais do Azure, você configurar uma conta no [Gerenciador de recursos de modo](../storage/common/storage-create-storage-account.md), ou [modo clássico](../storage/common/storage-create-storage-account.md).
- É recomendável que você configure uma conta de armazenamento antes de começar. Se você não é necessário toodo-lo durante a implantação da recuperação de Site. Olá devem estar no hello Cofre de serviços de recuperação com a mesma região hello.
- Não é possível mover contas de armazenamento usada pela recuperação de Site em grupos de recursos dentro de saudação mesma assinatura, ou em assinaturas diferentes.


## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 6: recursos do Hyper-V preparar](hyper-v-site-walkthrough-prepare-hyper-v.md)
