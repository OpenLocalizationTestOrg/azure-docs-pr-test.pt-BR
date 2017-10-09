---
title: "aaaHow funciona VMware replicação tooAzure no Azure Site Recovery? | Microsoft Docs"
description: "Este artigo fornece uma visão geral dos componentes e arquitetura usada quando replicar local VMs VMware e servidores físicos tooAzure com hello serviço Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: vmware-walkthrough-architecture
ms.openlocfilehash: f0fb834f8b251640f97e4d0163b2b9e54de691e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-vmware-replication-tooazure-work-in-site-recovery"></a>Como funciona a VMware replicação tooAzure na recuperação de Site?

Este artigo descreve os componentes de saudação e processos envolvidos ao replicar tooAzure máquinas virtuais e servidores físicos do Windows/Linux, VMware usando Olá local [do Azure Site Recovery](site-recovery-overview.md) serviço.

Quando você replica tooAzure de servidores locais físicos, a replicação usa também Olá mesmo componentes e processos como a replicação de VM do VMware, com essas diferenças:

- Você pode usar um servidor físico para o servidor de configuração hello, em vez de uma VM do VMware.
- Você precisará de uma infraestrutura do VMware local para failback. Não é possível reprovar máquina física tooa voltar.

Lançar os comentários na parte inferior da saudação deste artigo, ou fazer perguntas no hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="architectural-components"></a>Componentes de arquitetura

Há vários componentes envolvidos ao replicar máquinas virtuais do VMware e servidores físicos tooAzure.

**Componente** | **Localidade** | **Detalhes**
--- | --- | ---
**As tabelas** | No Azure, você precisa de uma conta do Azure, uma conta de armazenamento do Azure e uma rede do Azure. | Dados replicados são armazenados na conta de armazenamento hello e VMs do Azure são criadas com dados replicado de saudação quando ocorrer failover do seu site local. Olá VMs do Azure conectar toohello rede virtual do Azure quando eles são criados.
**Servidor de configuração** | Um único servidor de gerenciamento (VMWare VM) que executa todos os componentes de local de saudação que são necessárias para a implantação de hello, incluindo o servidor de configuração de saudação, o servidor de processo, o servidor de destino mestre local | componente de servidor de configuração de saudação coordena as comunicações entre o local e o Azure e gerencia a replicação de dados.
 **Servidor de processo**:  | Instalado por padrão no servidor de configuração de saudação. | Atua como um gateway de replicação. Recebe dados de replicação, otimizá-lo com o cache, a compactação e criptografia e envia tooAzure armazenamento.<br/><br/> servidor de processo Olá também lida com a instalação por push de máquinas de tooprotected de serviço de mobilidade hello e executa a descoberta automática de máquinas virtuais do VMware.<br/><br/> À medida que aumenta sua implantação, você pode adicionar mais processo dedicado separado servidores toohandle aumentar os volumes de tráfego de replicação.
 **Servidor de destino mestre** | Instalado por padrão no servidor de configuração local hello. | Lida com os dados de replicação durante o failback do Azure.<br/><br/> Se os volumes de tráfego de failback forem altos, você poderá implantar um servidor de destino mestre separado para failback.
**Servidores VMware** | Máquinas virtuais do VMware são hospedadas em servidores de ESXi do vSphere, e é recomendável um vCenter hosts de saudação do servidor toomanage. | Adicione o Cofre de serviços de recuperação de tooyour de servidores do VMware.
**Computadores replicados** | Olá serviço de mobilidade será instalado em cada máquina virtual que você deseja tooreplicate VMware. Ele pode ser instalado manualmente em cada computador, ou com uma instalação por push saudação do servidor de processo.

Saiba mais sobre os pré-requisitos de implantação de saudação e requisitos para cada um desses componentes de saudação [matriz de suporte](site-recovery-support-matrix-to-azure.md).

**Figura 1: VMware tooAzure componentes**

![Componentes](./media/site-recovery-components/arch-enhanced.png)

## <a name="replication-process"></a>Processo de replicação

1. Configurar implantação hello, incluindo componentes do Azure e um cofre de serviços de recuperação. No cofre Olá você especificar origem da replicação hello e destino, configurar o servidor de configuração Olá, adicionar servidores VMware, crie uma política de replicação, implantar o serviço de mobilidade Olá, habilitar a replicação e executar um failover de teste.
2.  Máquinas iniciam a replicação de acordo com a política de replicação Olá, e uma cópia inicial dos dados de saudação é replicado tooAzure armazenamento.
4. A replicação de tooAzure de alterações delta começa após a conclusão da replicação inicial de saudação. As alterações acompanhadas para uma máquina são mantidas em um arquivo .hrl.
    - Replicadas máquinas se comunicar com servidor de configuração de saudação na porta HTTPS 443 entrada para o gerenciamento de replicação.
    - Replicadas máquinas enviam servidor de processo de toohello de dados de replicação na porta HTTPS 9443 entrada (pode ser configurado).
    - servidor de configuração de saudação orquestra o gerenciamento de replicação com o Azure através da porta HTTPS 443 de saída.
    - servidor de processo Olá recebe dados de máquinas de origem, otimiza criptografa e envia tooAzure armazenamento pela porta 443 saída.
    - Se você habilitar a consistência de várias VMs, em seguida, máquinas no grupo de replicação Olá comunicam entre si pela porta 20004. Várias VMS serão usadas se você agrupar vários computadores em grupos de replicação que compartilham pontos de recuperação consistentes com o aplicativo e com falhas ao realizar o failover. Isso é útil se estiver executando máquinas Olá a mesma carga de trabalho e precisam toobe consistente.
5. O tráfego é replicado tooAzure armazenamento pontos de extremidade públicos, mais Olá da internet. Como alternativa, você pode usar o [emparelhamento público](../expressroute/expressroute-circuit-peerings.md#public-peering) do Azure ExpressRoute. Replicação do tráfego por uma VPN site a site de um tooAzure de site local não tem suporte.

**Figura 2: VMware tooAzure replicação**

![Avançado](./media/site-recovery-components/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>Processo de failover e failback

1. Depois de verificar que se o failover de teste está funcionando como esperado, você pode executar failovers não planejados tooAzure conforme necessário. Não há suporte para failover planejado.
2. Você pode fazer o failover de um único computador ou criar [planos de recuperação](site-recovery-create-recovery-plans.md), toofail entre várias VMs.
3. Ao executar um failover, VMs de réplica são criadas no Azure. Você pode confirmar uma failover toostart acessando Olá carga de trabalho da réplica Olá VM do Azure.
4. Quando o site primário local estiver disponível novamente, você poderá executar o failback. Configurar uma infra-estrutura de failback, iniciar a replicação de máquina de saudação do hello site secundário toohello primário e executar um failover não planejado do site secundário hello. Após você confirmar esse failover, dados serão back local e você precisa tooenable replicação tooAzure novamente. [Saiba mais](site-recovery-failback-azure-to-vmware.md)

Há alguns requisitos de failback:


- **Servidor de processo temporário no Azure**: se você quiser toofail do Azure após o failover, você precisará tooset a uma VM do Azure configurado como um servidor de processo, a replicação toohandle do Azure. Você pode excluir a VM após a conclusão do failback.
- **Conexão VPN**: para failback, você precisará de uma conexão VPN (ou rota expressa do Azure) configurar de saudação do Azure rede toohello no site local.
- **O servidor de destino mestre local separado**: servidor de destino mestre local Olá manipula failback. o servidor de destino mestre Olá é instalado por padrão no servidor de gerenciamento hello, mas se você estiver falhando volta maiores volumes de tráfego de você deve configurar um servidor de destino mestre local separado para essa finalidade.
- **Diretiva de failback**: tooyour back tooreplicate site local, você precisará de uma política de failback. Isso é criado automaticamente quando você cria sua política de replicação.
- **O VMware infrastructure**: você deve realizar failback tooan de VM do VMware no local. Isso significa que você precisa de uma infra-estrutura de VMware no local, mesmo se você estiver replicando tooAzure de servidores físicos no local.

**Figura 3: failback físico/de VMware**

![Failback](./media/site-recovery-components/enhanced-failback.png)


## <a name="next-steps"></a>Próximas etapas

Saudação de revisão [matriz de suporte](site-recovery-support-matrix-to-azure.md)
