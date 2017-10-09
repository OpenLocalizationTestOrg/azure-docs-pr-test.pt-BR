---
title: "aaaMigrate VMs Azure IaaS entre regiões do Azure | Microsoft Docs"
description: "Use o Azure Site Recovery toomigrate Azure máquinas virtuais de um tooanother de região do Azure."
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
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: c84dc77716b8d19969eab60707ed1332ca39b893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a>Migrar máquinas virtuais IaaS do Azure entre regiões do Azure com o Azure Site Recovery
## <a name="overview"></a>Visão geral
Bem-vindo tooAzure recuperação de Site! Use este artigo se você deseja toomigrate Azure VMs entre regiões do Azure. Antes de começar, observe que:

* O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: Azure Resource Manager e Clássico. Azure também tem dois portais – Olá portal clássico do Azure que dá suporte ao modelo de implantação clássico hello e Olá portal do Azure com suporte para ambos os modelos de implantação. etapas básicas Olá para migração são Olá mesmo se você estiver configurando a recuperação de Site no Gerenciador de recursos ou em clássico. No entanto Olá instruções de interface do usuário e capturas de tela neste artigo são relevantes para Olá portal do Azure.
* **Atualmente só é possível migrar de uma região tooanother. Você pode fazer failover de máquinas virtuais de tooanother de uma região do Azure, mas você não pode failback-los novamente.**

Postar comentários e perguntas na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Pré-requisitos
Aqui está o que você precisa para essa implantação:

* **Máquinas virtuais IaaS**: Olá VMs que você deseja toomigrate. Você pode migrar essas VMs tratando-as como computadores físicos.

## <a name="deployment-steps"></a>Etapas de implantação.
Esta seção descreve as etapas de implantação Olá no novo portal do Azure de saudação.

1. [Crie um cofre](site-recovery-vmware-to-azure.md).
2. [Habilite a replicação](site-recovery-vmware-to-azure.md). Habilite a replicação para Olá VMs que você deseja toomigrate e escolha o Azure como origem. 
3. [ Execute um failover não planejado](site-recovery-failover.md). Depois que a replicação inicial for concluída, você pode executar um failover não planejado de um tooanother de região do Azure. Opcionalmente, você pode criar um plano de recuperação e executar um failover não planejado, toomigrate várias máquinas virtuais entre regiões. [Saiba mais](site-recovery-create-recovery-plans.md) sobre planos de recuperação.

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre outros cenários de replicação em [O que é o Azure Site Recovery?](site-recovery-overview.md)
