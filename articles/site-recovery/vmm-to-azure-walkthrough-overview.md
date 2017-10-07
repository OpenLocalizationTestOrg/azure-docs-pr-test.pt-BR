---
title: aaaReplicate VMs Hyper-V no VMM nuvens tooAzure com o Azure Site Recovery | Microsoft Docs
description: "Fornece uma visão geral para replicar máquinas virtuais do Hyper-V no VMM tooAzure de nuvens usando o serviço do Azure Site Recovery Olá"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: d6f729a49cc86ea07bebc4d7266fd7b58b3998f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a>Replicar máquinas virtuais Hyper-V no tooAzure de nuvens do VMM usando o Site Recovery no portal do Azure de saudação
> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-vmm-to-azure.md)
> * [Azure clássico](site-recovery-vmm-to-azure-classic.md)
> * [Implantação do Resource Manager do PowerShell](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [Implantação clássica do PowerShell](site-recovery-deploy-with-powershell.md)


Este artigo fornece uma visão geral da saudação etapas necessárias tooreplicate máquinas de virtuais de Hyper-V (VMs) gerenciadas no tooAzure de nuvens do System Center Virtual Machine Manager (VMM), usando Olá local [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.

Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-hello-scenario-architecture"></a>Etapa 1: Analisar a arquitetura de cenário Olá

Antes de iniciar a implantação, examine a arquitetura de cenário hello e certifique-se de que você compreenda todos os componentes de saudação precisar toodeploy.

Vá muito[etapa 1: revisar arquitetura Olá](vmm-to-azure-walkthrough-architecture.md)

## <a name="step-2-review-prerequisites-and-limitations"></a>Etapa 2: Analisar os pré-requisitos e as limitações

Certifique-se de que você compreenda os pré-requisitos de implantação hello e limitações.

**Pré-requisitos do Azure**: você precisa de uma conta do Microsoft Azure, redes do Azure e contas de armazenamento.
**Servidores do VMM no local e os hosts do Hyper-V**: verifique se os servidores VMM e os hosts do Hyper-V são compatíveis e se estão preparados para a implantação do Site Recovery.
**Replicadas VMs**: Verifique se as VMs que você deseja tooreplicate atender aos requisitos do Azure.

Vá muito[etapa 2: verificar os pré-requisitos e limitações](vmm-to-azure-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Etapa 3: Planejar a capacidade

Se você estiver fazendo uma implantação completa, você precisa toofigure quais recursos de replicação é necessário. Há algumas toohelp disponíveis ferramentas você fazer isso. Se você estiver fazendo uma rápida de configurar o ambiente de saudação tootest, você pode ignorar esta etapa.

Vá muito[etapa 3: planejar a capacidade](vmm-to-azure-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Etapa 4: Planejar a rede

É necessário toodo alguma rede planejamento tooensure que você pode configurar o mapeamento de rede quando você implanta o cenário de hello, máquinas virtuais do Azure será redes virtuais conectadas tooAzure após failover ocorrer e que quais estão atribuídas IP apropriada de endereços.

Vá muito[etapa 4: planejar a rede](vmm-to-azure-walkthrough-network.md)


## <a name="step-5-prepare-azure-resources"></a>Etapa 5: Preparar os recursos do Azure

Configure uma conta, redes e armazenamento do Azure. Você pode fazer isso durante a implantação, mas recomendamos fazer isso antes de começar.

Vá muito[etapa 5: preparar o Azure](vmm-to-azure-walkthrough-prepare-azure.md)

## <a name="step-6-prepare-vmm-and-hyper-v"></a>Etapa 6: Preparar o VMM e o Hyper-V

Prepare servidores do VMM local hello e hosts Hyper-V para implantação da recuperação de Site.

Vá muito[etapa 6: preparar servidores locais](vmm-to-azure-walkthrough-vmm-hyper-v.md)

## <a name="step-7-set-up-a-vault"></a>Etapa 7: Configurar um cofre

Configurar um cofre dos Serviços de Recuperação. cofre Olá contém definições de configuração e coordena a replicação.

[Etapa 7: Configurar um cofre](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>Etapa 8: Definir as configurações de origem e destino

Configure locais de replicação de origem e destino hello. Adicionar o cofre do hello VMM server toohello e baixar arquivos de instalação Olá para componentes do Site Recovery. Execute a instalação do provedor Azure Site Recovery no servidor do VMM hello. A instalação instala Olá provedor no servidor do VMM hello e registra o servidor de saudação no cofre de saudação. Instale o agente de serviços de recuperação do Microsoft hello em cada host Hyper-V.

Vá muito[etapa 8: definir configurações de origem e destino](vmm-to-azure-walkthrough-source-target.md)

## <a name="step-9-configure-network-mapping"></a>Etapa 9: Configurar o mapeamento de rede

Mapa de redes virtuais de tooAzure de redes de VM do VMM no local. Após o failover, máquinas virtuais do Azure são criados no hello rede do Azure que mapeia a rede VM do toohello local no qual Olá Hyper-V de origem está localizado.

Vá muito[etapa 9: Configurar mapeamento de rede](vmm-to-azure-walkthrough-network-mapping.md)


## <a name="step-10-set-up-a-replication-policy"></a>Etapa 10: Configurar uma política de replicação

Especifique como VMs locais serão replicada tooAzure.

Vá muito[etapa 10: configurar uma política de replicação](vmm-to-azure-walkthrough-replication.md)


## <a name="step-11-enable-replication-for-vms"></a>Etapa 11: Habilitar a replicação para VMs

Selecione VMs Olá deseja tooreplicate. Habilitar uma máquina virtual para replicação gatilhos Olá a replicação inicial tooAzure, seguido por replicação delta em andamento.

Vá muito[etapa 11: habilitar a replicação](vmm-to-azure-walkthrough-enable-replication.md)


## <a name="step-12-run-a-test-failover"></a>Etapa 12: Executar um failover de teste

Execute um toomake de failover de teste se que tudo está funcionando conforme o esperado.

Vá muito[etapa 12: executar um failover de teste](vmm-to-azure-walkthrough-test-failover.md)


