---
title: aaaReplicate tooAzure de VMs Hyper-V com o Azure Site Recovery | Microsoft Docs
description: "Descreve como tooorchestrate replicação, failover e recuperação de local Hyper-V VMs tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: efddd986-bc13-4a1d-932d-5484cdc7ad8d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: ab9cd14149ef32a416428d0f4327aa18b042e9c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure"></a>Replicar tooAzure de máquinas virtuais (sem VMM) do Hyper-V 

> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-hyper-v-site-to-azure.md)
> * [Azure clássico](site-recovery-hyper-v-site-to-azure-classic.md)
> * [PowerShell – Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

Este artigo fornece uma visão geral da saudação etapas necessárias tooreplicate local Hyper-V máquinas virtuais tooAzure, usando Olá [do Azure Site Recovery](site-recovery-overview.md) em Olá portal do Azure. Nessa implantação, VMs de Hyper-V não são gerenciadas pelo System Center Virtual Machine Manager (VMM).


Depois de ler este artigo, postar os comentários na parte inferior da saudação ou questões técnicas Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-architecture-and-prerequisites"></a>Etapa 1: Examinar a arquitetura e os pré-requisitos

Antes de iniciar a implantação, examine a arquitetura de cenário hello e certifique-se de que entender todos os componentes de saudação é necessário toodeploy

Vá muito[etapa 1: revisar arquitetura Olá](hyper-v-site-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Etapa 2: Examinar os pré-requisitos

Certifique-se de que ter Olá pré-requisitos em vigor para cada componente de implantação:

- **Pré-requisitos do Azure**: você precisa de uma conta do Microsoft Azure, redes do Azure e contas de armazenamento.
- **Pré-requisitos do Hyper-V local**: verifique se os hosts Hyper-V estão preparados para a implantação do Site Recovery.
- **Replicadas VMs**: máquinas virtuais que você deseja tooreplicate necessário toocomply com os requisitos do Azure.

Vá muito[etapa 2: verificar os pré-requisitos e limitações](hyper-v-site-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Etapa 3: Planejar a capacidade

Se você estiver fazendo uma implantação completa, que você precisa toofigure quais recursos de replicação é necessário. Há algumas toohelp disponíveis ferramentas você fazer isso. Vá tooStep 2. Se você estiver fazendo uma rápida de configurar o ambiente de saudação tootest, você pode ignorar esta etapa.

Vá muito[etapa 3: planejar a capacidade](hyper-v-site-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Etapa 4: Planejar a rede

É necessário toodo algum planejamento tooensure que máquinas virtuais do Azure são conectados toonetworks após o failover, e que se eles têm Olá direito de endereços IP da rede.

Vá muito[etapa 4: planejar a rede](hyper-v-site-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Etapa 5: Preparar os recursos do Azure

Configure as redes e o armazenamento do Azure antes de começar. Você pode fazer isso durante a implantação, mas recomendamos fazer isso antes de começar.

Vá muito[etapa 5: preparar o Azure](hyper-v-site-walkthrough-prepare-azure.md)


## <a name="step-6-prepare-hyper-v"></a>Etapa 6: Preparar o Hyper-V

Verifique se os Hyper-V Servers atendem aos requisitos de implantação do Site Recovery.

Vá muito[etapa 6: preparar Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)

## <a name="step-7-set-up-a-vault"></a>Etapa 7: Configurar um cofre

Você precisa tooset a um tooorchestrate de Cofre de serviços de recuperação e gerenciar a replicação. Quando você configura o cofre hello, especifique o que você deseja tooreplicate, e onde você deseja tooreplicate-o para.

Vá muito[etapa 7: criar um cofre](hyper-v-site-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>Etapa 8: Definir as configurações de origem e destino

Configure a origem de saudação e de destino que é usado para replicação. Definir configurações de origem inclui a adição de site do Hyper-V de tooa do Hyper-V hosts, instalando hello provedor de recuperação de Site e o agente de serviços de recuperação em cada host Hyper-V e registrando site Olá no hello que Cofre de serviços de recuperação.

Vá muito[etapa 8: configurar Olá origem e destino](hyper-v-site-walkthrough-source-target.md)

## <a name="step-9-set-up-a-replication-policy"></a>Etapa 9: Definir uma política de replicação

Defina as configurações de replicação de toospecify uma política para VMs Hyper-V no cofre hello.

Vá muito[etapa 9: configurar uma política de replicação](hyper-v-site-walkthrough-replication.md)


## <a name="step-10-enable-replication"></a>Etapa 10: Habilitar a replicação

Depois que você tiver uma política de replicação no local, depois de habilitar, ocorre a replicação inicial da saudação VM.

Vá muito[etapa 10: habilitar a replicação](hyper-v-site-walkthrough-enable-replication.md)

## <a name="step-11-run-a-test-failover"></a>Etapa 11: Executar um failover de teste

Após a conclusão da replicação inicial, e a replicação delta está em execução, você pode executar um toomake de failover de teste se que tudo está funcionando conforme o esperado.

Vá muito[etapa 11: executar um failover de teste](hyper-v-site-walkthrough-test-failover.md)
