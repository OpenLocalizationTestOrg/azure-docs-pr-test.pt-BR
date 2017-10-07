---
title: "arquitetura de saudação aaaReview para VMware replicação tooAzure | Microsoft Docs"
description: "Este artigo fornece uma visão geral dos componentes e arquitetura usada ao replicar tooAzure de VMs VMware locais com hello serviço Azure Site Recovery"
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
ms.topic: article
ms.date: 06/27.017
ms.author: raynew
ms.openlocfilehash: 7acb1d8e83a846dca79e175fd1af9324f2c31e65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-vmware-replication-tooazure"></a>Etapa 1: Revisar arquitetura Olá para VMware tooAzure de replicação

Este artigo descreve os componentes de saudação e processos usados quando a replicação local tooAzure de máquinas virtuais VMware usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço.

Lançar os comentários na parte inferior da saudação deste artigo, ou fazer perguntas no hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="architectural-components"></a>Componentes de arquitetura

tabela de saudação Resume componentes Olá que necessários.

**Componente** | **Requisito** | **Detalhes**
--- | --- | ---
**As tabelas** | Você precisa de uma assinatura do Azure, uma conta de armazenamento do Azure e uma rede do Azure. | Dados replicados são armazenados na conta de armazenamento hello. Máquinas virtuais do Azure são criados com dados replicado de saudação quando ocorrer failover do seu site local. Olá VMs do Azure conectar toohello rede virtual do Azure quando eles são criados.
**Servidor de configuração** | Um único servidor de gerenciamento (VMware VM) que executa todos os Olá local componentes do Site Recovery para a implantação de saudação no local. Isso inclui um servidor de configuração, um servidor em processo e um servidor de destino mestre. | componente de servidor de configuração de saudação coordena as comunicações entre o local e o Azure e gerencia a replicação de dados.
 **Servidor de processo**:  | Instalado por padrão no servidor de configuração de saudação. | Atua como um gateway de replicação. Recebe dados de replicação, otimizá-lo com o cache, a compactação e criptografia e envia tooAzure armazenamento.<br/><br/> servidor de processo Olá também lida com a instalação por push de máquinas de tooprotected de serviço de mobilidade hello e executa a descoberta automática de máquinas virtuais do VMware.<br/><br/> À medida que aumenta sua implantação, você pode adicionar mais processo dedicado separado servidores toohandle aumentar os volumes de tráfego de replicação.
 **Servidor de destino mestre** | Instalado por padrão no servidor de configuração local hello. | Lida com os dados de replicação durante o failback do Azure.<br/><br/> Se os volumes de tráfego de failback forem altos, você poderá implantar um servidor de destino mestre separado para failback.
**Servidores VMware** | Máquinas virtuais do VMware são hospedadas em servidores de ESXi do vSphere, e é recomendável um vCenter hosts de saudação do servidor toomanage. | Adicione o Cofre de serviços de recuperação de tooyour de servidores do VMware.
**Computadores replicados** | Olá serviço de mobilidade será instalado em cada VM VMware replicar. Ele pode ser instalado manualmente em cada computador, ou com uma instalação por push saudação do servidor de processo.

**Figura 1: VMware tooAzure componentes**

![Componentes](./media/vmware-walkthrough-architecture/arch-enhanced.png)

## <a name="replication-process"></a>Processo de replicação

1. Configurar implantação hello, incluindo o local e os componentes do Azure. No cofre de serviços de recuperação hello, você pode especificar origem da replicação hello e destino, configurar o servidor de configuração de hello, criar uma política de replicação, implantar o serviço de mobilidade hello, habilitar a replicação e executar um failover de teste.
2. Replicar máquinas acordo com a política de replicação hello e uma cópia inicial dos dados de saudação é replicado tooAzure de armazenamento.
3. Após a conclusão da replicação inicial, a replicação delta alterações tooAzure começa. As alterações acompanhadas para uma máquina são mantidas em um arquivo .hrl.
    - Replicadas máquinas se comunicar com servidor de configuração de saudação na porta HTTPS 443 entrada para o gerenciamento de replicação.
    - Replicadas máquinas enviam servidor de processo de toohello de dados de replicação na porta HTTPS 9443 entrada (pode ser modificada).
    - servidor de configuração de saudação orquestra o gerenciamento de replicação com o Azure através da porta HTTPS 443 de saída.
    - servidor de processo Olá recebe dados de máquinas de origem, otimiza criptografa e envia tooAzure armazenamento pela porta 443 saída.
    - Se você habilitar a consistência de várias VMs, em seguida, máquinas no grupo de replicação Olá comunicam entre si pela porta 20004. Várias VMS serão usadas se você agrupar vários computadores em grupos de replicação que compartilham pontos de recuperação consistentes com o aplicativo e com falhas ao realizar o failover. Isso é útil se estiver executando máquinas Olá a mesma carga de trabalho e precisam toobe consistente.
4. O tráfego é replicado tooAzure armazenamento pontos de extremidade públicos, mais Olá da internet. Como alternativa, você pode usar o [emparelhamento público](../expressroute/expressroute-circuit-peerings.md#public-peering) do Azure ExpressRoute. Replicação do tráfego por uma VPN site a site de um tooAzure de site local não tem suporte.


**Figura 2: VMware tooAzure replicação**

![Avançado](./media/vmware-walkthrough-architecture/v2a-architecture-henry.png)

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

![Failback](./media/vmware-walkthrough-architecture/enhanced-failback.png)


## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 2: verificar os pré-requisitos e limitações](vmware-walkthrough-prerequisites.md)
