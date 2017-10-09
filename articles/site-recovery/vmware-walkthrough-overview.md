---
title: aaaReplicate VMs VMware tooAzure com o Azure Site Recovery | Microsoft Docs
description: "Fornece uma visão geral das etapas de saudação para replicar as cargas de trabalho em execução em máquinas virtuais do VMware tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 7104f67a3635b916048dcb61bca770c89f0c77fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-vms-tooazure-with-site-recovery"></a>Replicar máquinas virtuais do VMware tooAzure com a recuperação de Site

Este artigo fornece uma visão geral da saudação etapas necessárias tooreplicate local VMware máquinas virtuais tooAzure, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.


![Processo de implantação](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

**Figura 1: Resumo do processo de implantação**

## <a name="step-1-review-architecture-and-prerequisites"></a>Etapa 1: Examinar a arquitetura e os pré-requisitos

Antes de iniciar a implantação, examine a arquitetura de cenário hello e certifique-se de que entender todos os componentes de saudação é necessário toodeploy

Vá muito[etapa 1: revisar arquitetura Olá](vmware-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Etapa 2: Examinar os pré-requisitos

Certifique-se de que ter Olá pré-requisitos em vigor para cada componente de implantação:

- **Pré-requisitos do Azure**: você precisa de uma conta do Microsoft Azure, redes do Azure e contas de armazenamento.
- **Componentes locais do Site Recovery**: Você precisa de uma máquina que execute os componentes locais do Site Recovery.
- **Pré-requisitos do VMware no local**: tooset contas é necessário para que a recuperação de Site pode acessar servidores VMware e máquinas virtuais.
- **Replicadas VMs**: VMs que você deseja tooreplicate necessidade toocomply com os requisitos do Azure e ter o componente de serviço de mobilidade Olá instalado.

Vá muito[etapa 2: analisar os pré-requisitos e limitações](vmware-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Etapa 3: Planejar a capacidade

Se você estiver fazendo uma implantação completa, que você precisa toofigure quais recursos de replicação é necessário. Há algumas toohelp disponíveis ferramentas você fazer isso. Vá tooStep 2. Se você estiver fazendo uma rápida de configurar o ambiente de saudação tootest, você pode ignorar esta etapa.

Vá muito[etapa 3: planejar a capacidade](vmware-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Etapa 4: Planejar a rede

É necessário toodo algum planejamento tooensure que máquinas virtuais do Azure são conectados toonetworks após o failover, e que se eles têm Olá direito de endereços IP da rede.

Vá muito[etapa 4: planejar a rede](vmware-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Etapa 5: Preparar os recursos do Azure

Configure as redes e o armazenamento do Azure antes de começar. Você pode fazer isso durante a implantação, mas recomendamos fazer isso antes de começar.

Vá muito[etapa 5: preparar o Azure](vmware-walkthrough-prepare-azure.md)


## <a name="step-6-prepare-vmware"></a>Etapa 6: Preparar o VMware

É necessário tooset as contas de recuperação de Site será usado para:

- Acesso tooautomatically de servidores de virtualização de VMware detectar VMs.
- Acesse o serviço de mobilidade VMs tooinstall hello. Cada máquina virtual que você deseja tooreplicate devem ter o agente de serviço de mobilidade de Olá instalado antes de você pode habilitar a replicação para ele.

Vá muito[etapa 6: preparar VMware](vmware-walkthrough-prepare-vmware.md)

## <a name="step-7-set-up-a-vault"></a>Etapa 7: Configurar um cofre

Você precisa tooset a um tooorchestrate de Cofre de serviços de recuperação e gerenciar a replicação. Quando você configura o cofre hello, especifique o que você deseja tooreplicate, e onde você deseja tooreplicate-o para.

Vá muito[etapa 7: configurar um cofre](vmware-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>Etapa 8: Definir as configurações de origem e destino

Configure a origem de saudação e de destino que é usado para replicação. Definir configurações de origem inclui a execução tooinstall de instalação do Unified componentes de recuperação de Site Olá locais.

Vá muito[etapa 8: configurar Olá origem e destino](vmware-walkthrough-source-target.md)

## <a name="step-9-set-up-a-replication-policy"></a>Etapa 9: Definir uma política de replicação

Defina as configurações de replicação de toospecify uma política para VMs VMware no cofre hello.

Vá muito[etapa 9: configurar uma política de replicação](vmware-walkthrough-replication.md)

## <a name="step-10-install-hello-mobility-service"></a>Etapa 10: Instalar o serviço de mobilidade Olá

Olá serviço de mobilidade deve ser instalado em cada máquina virtual que você deseja tooreplicate. Há alguns tooset maneiras serviço Olá com instalação de push ou pull.

Vá muito[etapa 10: instalar o serviço de mobilidade Olá](vmware-walkthrough-install-mobility.md)

## <a name="step-11-enable-replication"></a>Etapa 11: Habilitar a replicação

Depois de saudação serviço de mobilidade está em execução em uma máquina virtual, você pode habilitar replicação para ele. Depois de habilitar, ocorre a replicação inicial dos Olá VM.

Vá muito[etapa 11: habilitar a replicação](vmware-walkthrough-enable-replication.md)

## <a name="step-12-run-a-test-failover"></a>Etapa 12: Executar um failover de teste

Após a conclusão da replicação inicial, e a replicação delta está em execução, você pode executar um toomake de failover de teste se que tudo está funcionando conforme o esperado.

Vá muito[etapa 12: executar um failover de teste](vmware-walkthrough-test-failover.md)
