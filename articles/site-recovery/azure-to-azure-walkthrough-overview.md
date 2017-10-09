---
title: "aaaReplicate VMs do Azure entre regiões do Azure | Microsoft Docs"
description: "Resume Olá etapas necessárias tooreplicate VMs do Azure entre regiões do Azure com o serviço do Azure Site Recovery Olá no hello portal do Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 6dd36239-4363-4538-bf80-a18e71b8ec67
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: f4ac386f040945131f8a10f02143437f4441e298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a>Você pode replicar VMs do Azure entre regiões usando o Site Recovery

>Este artigo fornece uma visão geral da saudação etapas necessárias tooreplicate máquinas virtuais (VMs) do Azure em uma região do Azure tooAzure VMs em uma região diferente. 

>[!NOTE]
>
> Atualmente, a replicação de VM do Azure está em versão prévia.

Postar perguntas e comentários na parte inferior da saudação deste artigo ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="step-1-review-architecture"></a>Etapa 1: revisar a arquitetura

Antes de iniciar a implantação, revise Olá cenário arquitetura e componentes Olá necessários toodeploy.

Vá muito[etapa 1: revisar arquitetura Olá](azure-to-azure-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Etapa 2: Examinar os pré-requisitos

Verifique que você tenha Olá pré-requisitos do Azure em locais, incluindo uma assinatura, redes virtuais, contas de armazenamento e os requisitos de VM.

Vá muito[etapa 2: verificar os pré-requisitos e limitações](azure-to-azure-walkthrough-prerequisites.md)


## <a name="step-3-plan-networking"></a>Etapa 3: Planejar a rede

Verifique se a conectividade de saída está configurada em VMs do Azure que você deseja tooreplicate e conexões locais são configurados.

Vá muito[etapa 4: planejar a rede](azure-to-azure-walkthrough-network.md)



## <a name="step-4-create-a-vault"></a>Etapa 4: criar um cofre 

Necessário tooset a um tooorchestrate de Cofre de serviços de recuperação e gerenciar a replicação e especificar a região de origem de saudação.

Vá muito[etapa 4: criar um cofre](azure-to-azure-walkthrough-vault.md)


## <a name="step-5-enable-replication"></a>Etapa 5: habilitar a replicação


replicação tooenable, definir configurações de local de destino, configurar uma política de replicação e selecione Olá VMs do Azure que você deseja tooreplicate. Depois de habilitar, ocorre a replicação inicial dos Olá VM.

Vá muito[etapa 5: habilitar a replicação](azure-to-azure-walkthrough-enable-replication.md)


## <a name="step-6-run-a-test-failover"></a>Etapa 6: executar um failover de teste

Após a conclusão da replicação inicial, e a replicação delta está em execução, você pode executar um toomake de failover de teste se que tudo está funcionando conforme o esperado.

Vá muito[etapa 6: executar um failover de teste](azure-to-azure-walkthrough-test-failover.md)


