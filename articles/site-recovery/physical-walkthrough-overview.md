---
title: "aaaReplicate físico tooAzure de servidores com o Azure Site Recovery local | Microsoft Docs"
description: "Fornece uma visão geral das etapas de saudação para replicar as cargas de trabalho em execução no local Windows/Linux servidores físicos tooAzure com hello serviço Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a>Replicar tooAzure servidores físicos com a recuperação de Site

Este artigo fornece uma visão geral da saudação etapas necessárias tooreplicate local Windows/Linux servidores físicos tooAzure, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.


## <a name="step-1-review-architecture-and-prerequisites"></a>Etapa 1: Examinar a arquitetura e os pré-requisitos

Antes de iniciar a implantação, examine a arquitetura de cenário de saudação e certifique-se de que entender todos os componentes de saudação é necessário tooset a implantação de saudação.

Vá muito[etapa 1: revisar arquitetura Olá](physical-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Etapa 2: Examinar os pré-requisitos

Certifique-se de que ter Olá pré-requisitos em vigor para cada componente de implantação:

- **Pré-requisitos do Azure**: você precisa de uma conta do Microsoft Azure, redes do Azure e contas de armazenamento.
- **Componentes locais do Site Recovery**: Você precisa de uma máquina que execute os componentes locais do Site Recovery.
- **As máquinas replicadas**: precisam de servidores que você deseja tooreplicate toocomply com locais e os requisitos do Azure.

Vá muito[etapa 2: analisar os pré-requisitos e limitações](physical-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Etapa 3: Planejar a capacidade

Se você estiver fazendo uma implantação completa, que você precisa toofigure quais recursos de replicação é necessário. Se você estiver fazendo uma rápida de configurar o ambiente de saudação tootest, você pode ignorar esta etapa.

Vá muito[etapa 3: planejar a capacidade](physical-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Etapa 4: Planejar a rede

É necessário toodo algum planejamento tooensure que máquinas virtuais do Azure são conectados toonetworks após o failover, e que se eles têm Olá direito de endereços IP da rede.

Vá muito[etapa 4: planejar a rede](physical-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Etapa 5: Preparar os recursos do Azure

Configure as redes e o armazenamento do Azure antes de começar. 

Vá muito[etapa 5: preparar o Azure](physical-walkthrough-prepare-azure.md)


## <a name="step-6-set-up-a-vault"></a>Etapa 6: Configurar um cofre

Configurar um tooorchestrate de Cofre de serviços de recuperação e gerenciar a replicação. Quando você configura o cofre hello, especifique o que você deseja tooreplicate, e onde você deseja tooreplicate-o para.

Vá muito[etapa 6: configurar um cofre](physical-walkthrough-create-vault.md)

## <a name="step-7-configure-source-and-target-settings"></a>Etapa 7: Definir as configurações de origem e destino

Definir configurações para Olá fonte e de destino site (Azure). Configurações de origem inclui a execução tooinstall de instalação do Unified componentes de recuperação de Site local hello.

Vá muito[etapa 7: configurar Olá origem e destino](physical-walkthrough-source-target.md)

## <a name="step-8-set-up-a-replication-policy"></a>Etapa 8: Configurar uma política de replicação

Configurar uma política toospecify físicos como servidores devem replicar.

Vá muito[etapa 8: configurar uma política de replicação](physical-walkthrough-replication.md)

## <a name="step-9-install-hello-mobility-service"></a>Etapa 9: Instale o serviço de mobilidade Olá

Olá serviço de mobilidade deve ser instalado em cada servidor que você deseja tooreplicate. Há alguns tooset maneiras serviço hello, com a instalação por push ou pull.

Vá muito[etapa 9: Instale o serviço de mobilidade Olá](physical-walkthrough-install-mobility.md)

## <a name="step-10-enable-replication"></a>Etapa 10: Habilitar a replicação

Olá serviço de mobilidade em execução em um servidor, você pode habilitar a replicação para ele. Depois de habilitar, ocorre a replicação inicial dos Olá VM.

Vá muito[etapa 10: habilitar a replicação](physical-walkthrough-enable-replication.md)

## <a name="step-11-run-a-test-failover"></a>Etapa 11: Executar um failover de teste

Após a conclusão da replicação inicial e a replicação delta está em execução, você pode executar um toomake de failover de teste se que tudo está funcionando conforme o esperado.

Vá muito[etapa 11: executar um failover de teste](physical-walkthrough-test-failover.md)

