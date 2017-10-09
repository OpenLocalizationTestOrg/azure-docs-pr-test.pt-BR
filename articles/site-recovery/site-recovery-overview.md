---
title: "aaaWhat é o Azure Site Recovery? | Microsoft Docs"
description: "Fornece uma visão geral da saudação serviço Azure Site Recovery e resume os cenários de implantação."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: e9b97b00-0c92-4970-ae92-5166a4d43b68
ms.service: site-recovery
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: da6755654b8036a03314ec836f014b64428d5518
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-site-recovery"></a>O que é a Recuperação de Site?

Bem-vindo serviço do Azure Site Recovery toohello! Este artigo fornece uma visão geral do serviço de saudação.

## <a name="business-continuity-and-disaster-recovery-bcdr-with-azure-recovery-services"></a>Continuidade de negócios e recuperação de desastre (BCDR) com os Serviços de Recuperação do Azure

Como uma organização, você precisa toofigure-out como você vai tookeep seus dados seguros e aplicativos/cargas de trabalho em execução quando planejados e não planejados ocorrem.

Serviços de recuperação do Azure contribuir estratégia BCDR tooyour:

- **O serviço Site Recovery**: o Site Recovery ajuda a garantir a continuidade dos negócios, mantendo seus aplicativos em execução em VMs e servidores físicos disponíveis se um site fica inoperante. Recuperação de site replica as cargas de trabalho em execução em máquinas virtuais e servidores físicos para que eles permanecem disponíveis em um local secundário se o site primário Olá não está disponível. Recupera as cargas de trabalho toohello site primário quando ele está ativo e em execução novamente.
- **Serviço de backup**: Além disso, Olá [Backup do Azure](https://docs.microsoft.com/azure/backup/) serviço mantém seus dados seguros e recuperáveis fazendo backup tooAzure.

O Site Recovery pode gerenciar a replicação para:

- VMs do Azure que replicam entre regiões do Azure.
- Local máquinas virtuais e servidores físicos replicando tooAzure ou site secundário tooa.


## <a name="what-does-site-recovery-provide"></a>O que o Site Recovery fornece?

**Recurso** | **Detalhes**
--- | ---
**Implantar uma solução simples de BCDR** | Com a recuperação de Site, você pode configurar e gerenciar replicação, failover e failback em um único local em Olá portal do Azure.
**Replicar máquinas virtuais do Azure** | Você pode configurar sua estratégia de BCDR para que as VMs do Azure sejam replicadas entre regiões do Azure.
**Replicar VMs locais fora do site** | Você pode replicar VMs locais e servidores físicos tooAzure ou tooa secundária no local. Replicação tooAzure elimina Olá custo e a complexidade de manter um datacenter secundário.
**Replicar carga de trabalho** | Replicar qualquer carga de trabalho em execução em VMs do Azure, VMs locais do Hyper-V e VMs do VMware com suporte, bem como em servidores físicos Windows/Linux.
**Manter dados flexíveis e seguros** | A recuperação de site gerencia a replicação e o failover, sem interceptar dados de aplicativo. Dados replicados são armazenados no armazenamento do Azure, com resiliência de saudação que fornece. Quando ocorre o failover, máquinas virtuais do Azure são criadas com base em dados replicado de saudação.
**Atender aos RTOs e RPOs** | Manter os RTO (objetivos de tempo de recuperação) e os RPO (objetivos de ponto de recuperação) dentro dos limites da organização. O Site Recovery fornece uma frequência da replicação tão baixa quanto 30 segundos para o Hyper-V, assim como a replicação contínua para o as VMs do Azure e VMs do VMware. Você pode reduzir os RTO (objetivos de tempo de recuperação) ainda mais integrando o [Gerenciador de Tráfego do Azure](https://azure.microsoft.com/blog/reduce-rto-by-using-azure-traffic-manager-with-azure-site-recovery/).
**Manter os aplicativos consistentes durante um failover** | Você pode configurar pontos de recuperação com instantâneos consistentes no aplicativo. Os instantâneos consistentes com os aplicativos capturam dados de disco, todos os dados na memória e todas as transações em andamento.
**Testar sem interrupção** | Você pode executar com facilidade os failovers de teste toosupport recuperação de desastre, sem afetar a replicação em andamento.
**Executar failovers flexíveis** | Você pode executar failovers planejados para interrupções esperadas com perda de dados zero ou failovers não planejados com perda mínima de dados (dependendo da frequência de replicação) para desastres inesperados. Facilmente você pode fazer o site primário tooyour back quando ele estiver disponível novamente.
**Criar planos de recuperação** | Você pode personalizar e sequenciar o failover e a recuperação de aplicativos de várias camadas em várias VMs com planos de recuperação. Agrupe computadores em planos e adicione scripts e ações manuais. Os planos de recuperação podem ser integrados com runbooks de automação do Azure.
**Integrar com tecnologias BCDR existentes** | O Site Recovery se integra a outras tecnologias BCDR. Por exemplo, você pode usar a recuperação de Site tooprotect saudação do SQL Server back-end de cargas de trabalho corporativas, incluindo o suporte nativo para o SQL Server AlwaysOn, toomanage Olá failover de grupos de disponibilidade.
**Integrar a biblioteca de automação da saudação** | Uma biblioteca de Automação do Azure avançada fornece scripts prontos para a produção e específicos do aplicativo que podem ser baixados e integrados na Recuperação de Site.
**Definir configurações de rede** | O Site Recovery se integra com o Azure para gerenciamento de rede de aplicativo simples, incluindo a reserva de endereços IP, a configuração de balanceadores de carga e a integração do Gerenciador de Tráfego do Azure para ter uma troca de rede eficiente.


## <a name="what-can-i-replicate"></a>O que posso replicar?

**Com suporte** | **Detalhes**
--- | ---
**O que posso replicar?** | VMs do Azure entre regiões do Azure (em versão prévia)<br/><br/>  Máquinas virtuais VMware, máquinas virtuais do Hyper-V, tooAzure de servidores físicos (Windows e Linux) no local < br /<br/> Máquinas virtuais VMware, máquinas virtuais do Hyper-V, site secundário do tooa servidores físicos ao local. Para máquinas virtuais do Hyper-V, o site secundário do tooa de replicação só é suportado se hosts Hyper-V são gerenciados pelo System Center VMM.
**Quais são as regiões têm suporte para o Site Recovery?** | [Regiões com suporte](https://azure.microsoft.com/regions/services/) |
**De quais sistemas operacionais os computadores replicados precisam?** | [Requisitos de VM do Azure](site-recovery-support-matrix-azure-to-azure.md#support-for-replicated-machine-os-versions)s<br></br>[Requisitos de VM do VMware](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)<br/><br/> Para VMs do Hyper-V, há suporte para qualquer [SO convidado](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows) com suporte do Azure e do Hyper-V.<br/><br/> [Requisitos de servidor físico](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)
**Quais servidores/hosts VMware são necessários?** | As VMs VMware pode estar localizadas em [servidores vCenter/hosts vSphere com suporte](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers)
**Quais cargas de trabalho posso replicar?** | Você pode replicar qualquer carga de trabalho em execução em um computador de replicação com suporte. Além disso, equipe de recuperação de Site Olá executou específico do aplicativo de teste para um [número de aplicativos](site-recovery-workload.md#workload-summary).


## <a name="azure-portal-considerations"></a>Considerações sobre o portal do Azure

* Recuperação de site pode ser implantada em Olá [portal do Azure](https://portal.azure.com).
* Olá portal clássico do Azure, é possível gerenciar Site Recovery com modelo de gerenciamento de serviços clássico hello.
- portal clássico Olá só deve ser usado toomaintain implantações de recuperação de Site existentes. Você não pode criar novos cofres no portal clássico do hello.

## <a name="next-steps"></a>Próximas etapas
* Leia mais sobre [Suporte a carga de trabalho](site-recovery-workload.md)
* Introdução ao [replicação de VM do Azure entre regiões](site-recovery-azure-to-azure.md), [VMware replicação tooAzure](vmware-walkthrough-overview.md), ou [tooAzure de replicação do Hyper-V](hyper-v-site-walkthrough-overview.md).
