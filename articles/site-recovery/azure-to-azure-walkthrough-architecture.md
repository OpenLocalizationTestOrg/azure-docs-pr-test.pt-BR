---
title: "arquitetura de saudação aaaReview para replicação de máquinas virtuais do Azure entre regiões do Azure | Microsoft Docs"
description: "Este artigo fornece uma visão geral dos componentes e arquitetura usada ao replicar máquinas virtuais do Azure entre regiões do Azure usando o serviço do Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/12/2017
ms.author: raynew
ms.openlocfilehash: 4caab4e7a764040f317201d1345c40c73f836d81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-azure-vm-replication-between-azure-regions"></a>Etapa 1: Revisar arquitetura Olá para replicação de VM do Azure entre regiões do Azure


Depois de revisar Olá [etapas de visão geral](azure-to-azure-walkthrough-overview.md) para essa implantação, leia este componentes de saudação do artigo toounderstand e processos usados quando a replicação e a recuperação de máquinas virtuais (VMs) do Azure de tooanother de uma região do Azure, usando [Azure Site Recovery](site-recovery-overview.md).

- Quando você terminar de artigo hello, você deve ter uma compreensão clara de como funciona a região de tooanother de replicação de VM do Azure.
- Lançar os comentários na parte inferior da saudação deste artigo, ou fazer perguntas no hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
>Replicação de VM do Azure com o serviço de recuperação de Site do hello está atualmente em visualização.



## <a name="architectural-components"></a>Componentes de arquitetura

Olá diagrama a seguir fornece uma visão geral de um ambiente de VM do Azure em uma região específica (no exemplo, Olá local do Leste dos EUA). Em um ambiente de VM do Azure:
- Os aplicativos podem ser executados em VMs com discos distribuídos em contas de armazenamento.
- Olá VMs pode ser incluído em uma ou mais sub-redes em uma rede virtual.

![ambiente do cliente](./media/azure-to-azure-walkthrough-architecture/source-environment.png)

## <a name="replication-process"></a>Processo de replicação

### <a name="step-1"></a>Etapa 1

Quando você habilitar a replicação de VM do Azure no portal do Azure de saudação, Olá recursos mostrados em Olá seguinte diagrama e tabela são criados automaticamente na região de destino hello. Por padrão, os recursos são criados com base nas configurações da região de origem. Você pode personalizar as configurações de destino de saudação conforme necessário. [Saiba mais](site-recovery-replicate-azure-to-azure.md).

![Habilitar o processo de replicação, etapa 1](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-1.png)

**Recurso** | **Detalhes**
--- | ---
**Grupo de recursos de destino** | Olá toowhich do grupo de recursos pertencem VMs replicadas após o failover.
**Rede virtual de destino** | rede virtual de saudação em que VMs replicadas estão localizadas após o failover. Um mapeamento de rede é criado entre redes virtuais de origem e de destino e vice-versa.
**Contas de armazenamento de cache** | Antes das alterações na fonte que VMs são replicadas toohello conta de armazenamento de destino, eles são controlados e enviados toohello conta de armazenamento de cache no local de destino hello. Isso garante um impacto mínimo sobre aplicativos de produção em execução em Olá VM.
**Contas de armazenamento de destino**  | Contas de armazenamento em dados de Olá Olá destino local toowhich é replicada.
**Conjuntos de disponibilidade de destino**  | Conjuntos de disponibilidade no qual Olá replicada VMs estão localizadas após o failover.

### <a name="step-2"></a>Etapa 2

Como a replicação estiver habilitada, Olá serviço de mobilidade de extensão de recuperação de Site é instalado automaticamente nos Olá VM. a seguir Olá ocorre:

1. Olá VM está registrado com o Site Recovery.

2. A replicação contínua está configurada para Olá VM. Grava dados em Olá VM discos estão continuamente transferidos toohello conta de armazenamento de cache no local de origem hello.

   ![Habilitar o processo de replicação, etapa 2](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-2.png)

  
  Observe que a recuperação de Site nunca precisa de conectividade toohello VM de entrada. Saída somente endereços do serviço de recuperação de tooSite conectividade URLs/IP, endereços de IP/URLs de autenticação do Office 365 e endereços IP de conta de armazenamento de cache é necessária. 

## <a name="continuous-replication-process"></a>Processo de replicação contínua

Depois que a replicação contínua está funcionando, o disco gravações são imediatamente transferidos toohello conta de armazenamento de cache. Recuperação de site processa dados saudação e envia toohello conta de armazenamento de destino. Após o processamento de dados de saudação, pontos de recuperação são gerados na conta de armazenamento de destino Olá intervalos de alguns minutos.

## <a name="failover-process"></a>Processo de failover

Quando você iniciar um failover, Olá que máquinas virtuais são criadas no grupo de recursos de destino hello, a rede virtual de destino, a sub-rede de destino e hello destino conjunto de disponibilidade. Durante um failover, você pode usar qualquer ponto de recuperação.

![Processo de failover](./media/azure-to-azure-walkthrough-architecture/failover.png)

## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 2: verificar os pré-requisitos e limitações](azure-to-azure-walkthrough-prerequisites.md)
