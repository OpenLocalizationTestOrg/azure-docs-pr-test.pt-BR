---
title: "pré-requisitos do aaaReview Olá para replicação de tooAzure Hyper-V (com o System Center VMM) usando o Azure Site Recovery | Microsoft Docs"
description: "Descreve os pré-requisitos de saudação para configurar a replicação, failover e recuperação de máquinas virtuais de Hyper-V no local em tooAzure de nuvens do VMM, com o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a1c30fd5-c979-473c-af44-4f725ad3e3ba
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: raynew
ms.openlocfilehash: de13a2d80b1a9a5d968a180d559f661ab11e70c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-with-vmm-tooazure-replication"></a>Etapa 2: Examinar os pré-requisitos de saudação para replicação do Hyper-V (com o VMM) tooAzure

Depois que você está revisado Olá [arquitetura de cenário](vmm-to-azure-walkthrough-architecture.md), leia este toomake artigo se você compreender os pré-requisitos de implantação de saudação. 

## <a name="prerequisites-and-limitations"></a>Pré-requisitos e limitações

**Requisito** | **Detalhes**
--- | ---
**Conta do Azure** | Você precisa de uma conta do [Microsoft Azure](http://azure.microsoft.com/) .
**Armazenamento do Azure** | É necessário um toostore replicado dados da conta de armazenamento do Azure.<br/><br/> conta de armazenamento Olá deve estar no hello Cofre de serviços de recuperação do Azure com a mesma região hello.<br/><br/>Você pode usar [armazenamento com redundância geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) ou armazenamento com redundância local. Recomendamos usar armazenamento com redundância geográfica. Com o armazenamento com redundância geográfica, dados seja resilientes se ocorrer uma interrupção regional, ou se a região primária Olá não pode ser recuperado.<br/><br/> Você pode usar uma conta de armazenamento padrão do Azure, ou pode usar o [Armazenamento Premium](../storage/common/storage-premium-storage.md) do Azure. Armazenamento Premium pode hospedar cargas de trabalho intensivas de E/S e é normalmente usado em VMs que precisam de um desempenho de E/S consistentemente alto e baixa latência. Se você usar o Armazenamento Premium para os dados replicados, também precisará de uma conta de Armazenamento Standard. Uma conta de armazenamento standard armazena os logs de replicação que capturam dados de local tooon alterações contínuas.
**Rede do Azure** | É necessário um [rede Azure](../virtual-network/virtual-network-get-started-vnet-subnet.md), toowhich VMs do Azure se conectar após o failover. Olá rede do Azure deve estar no hello Cofre de serviços de recuperação com a mesma região hello.
**Servidores VMM locais** | Você precisa de um ou mais servidores VMM em execução no System Center 2012 R2 ou versão posterior.<br/><br/> Cada servidor VMM deve estar em uma ou mais nuvens privadas. Cada nuvem precisa de um ou mais grupos de hosts.<br/><br/> servidor do VMM Olá precisa de acesso à internet.
**Hyper-V local** | Servidores de host Hyper-V devem estar executando pelo menos Windows Server 2012 R2 com a função hello Hyper-V habilitada ou Microsoft Hyper-V Server 2012 R2. atualizações mais recentes do Hello devem ser instaladas.<br/><br/> host do Hyper-V Olá deve estar localizado em um grupo de hosts do VMM (localizado em uma nuvem do VMM).<br/><br/> Um host deve ter uma ou mais VMs que você deseja tooreplicated.<br/><br/> Hosts Hyper-V devem ser toohello conectado à internet para replicação tooAzure, diretamente ou com um proxy. Servidores Hyper-V devem ter descritas no artigo de correções de saudação [2961977](https://support.microsoft.com/kb/2961977).
**VMs do Hyper-V locais** | Máquinas virtuais que você deseja tooreplicate devem estar executando uma [sistema operacional com suporte](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)e em conformidade com [pré-requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). nome da VM Olá pode ser modificado depois que a replicação está habilitada. 




## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 3: planejar a capacidade](vmm-to-azure-walkthrough-capacity.md)
