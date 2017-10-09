---
title: "pré-requisitos do aaaReview Olá para replicação de tooAzure Hyper-V (sem o System Center VMM) usando o Azure Site Recovery | Microsoft Docs"
description: "Descreve os pré-requisitos de saudação para configurar a replicação, failover e recuperação de local tooAzure de VMs Hyper-V com o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 3eefc3b7e3982ec6c413c1db7f7784863f9c701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-without-vmm-tooazure-replication"></a>Etapa 2: Examinar os pré-requisitos de saudação para replicação do Hyper-V (sem VMM) tooAzure

pré-requisitos de saudação são resumidos na tabela de saudação.


**Pré-requisito** | **Detalhes** 
--- | --- 
**As tabelas** | Saiba mais sobre os [requisitos do Azure](site-recovery-prereq.md#azure-requirements).
**Servidores locais** | [Saiba mais](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) sobre os requisitos para hosts de Hyper-V local hello.
**VMs do Hyper-V locais** | Máquinas virtuais que você deseja tooreplicate devem estar executando uma [sistema operacional com suporte](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)e em conformidade com [pré-requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URLs do Azure** | Hosts Hyper-V precisará de acesso toothese URLs:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Se você tiver regras de firewall baseado em endereço IP, certifique-se de que permitem comunicação tooAzure.<br/></br> Permitir Olá [intervalos de IP de Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).<br/></br> Permitir que os intervalos de endereços IP para Olá região do Azure de sua assinatura e Oeste dos EUA (usado para gerenciamento de identidade e controle de acesso).



## <a name="next-steps"></a>Próximas etapas

- Se você estiver fazendo uma implantação completa, vá muito[etapa 3: planejar a capacidade](hyper-v-site-walkthrough-capacity.md)
- Se você estiver fazendo uma implantação de teste simples, vá muito[etapa 4: planejar a rede](hyper-v-site-walkthrough-network.md).
