---
title: "arquitetura de saudação aaaReview para tooAzure de replicação de servidor físico, usando o Azure Site Recovery | Microsoft Docs"
description: "Este artigo fornece uma visão geral dos componentes e arquitetura usada ao replicar local tooAzure de servidores físicos com hello serviço Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 09c9b136-35f5-465e-8d0f-f4c5d5d9f880
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 4f334c181fa6f0821adf978ebe9dbd7d36a3c753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-physical-server-replication-tooazure"></a>Etapa 1: Revisar arquitetura Olá para tooAzure de replicação de servidor físico

Este artigo descreve os componentes de saudação e processos usados quando você replica tooAzure de servidores físicos do Windows/Linux local, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço.

Lançar os comentários na parte inferior da saudação deste artigo, ou fazer perguntas no hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="architectural-components"></a>Componentes de arquitetura

tabela de saudação Resume componentes Olá que necessários.

**Componente** | **Requisito** | **Detalhes**
--- | --- | ---
**As tabelas** | Você precisa de uma conta do Azure, uma conta de armazenamento do Azure e uma rede do Azure. | Dados replicados são armazenados na conta de armazenamento hello e VMs do Azure são criadas com dados replicado de saudação quando ocorre um failover. Máquinas virtuais do Azure conectam toohello rede virtual do Azure quando eles são criados.
**Servidor de configuração** | Um único servidor de gerenciamento (servidor físico ou VM VMware) que executa todos os Olá local componentes de recuperação de Site no local. Isso inclui um servidor de configuração, um servidor em processo e um servidor de destino mestre. | componente de servidor de configuração de saudação coordena as comunicações entre o local e o Azure e gerencia a replicação de dados.
 **Servidor de processo**  | Instalado por padrão no servidor de configuração de saudação. | Atua como um gateway de replicação. Recebe dados de replicação, otimizá-lo com o cache, a compactação e criptografia e envia tooAzure armazenamento.<br/><br/> servidor de processo Olá também lida com a instalação por push de máquinas de tooprotected de serviço de mobilidade hello.<br/><br/> Você pode adicionar servidores adicionais processo dedicado separado, toohandle aumentar os volumes de tráfego de replicação.
 **Servidor de destino mestre** | Instalado por padrão no servidor de configuração local hello. | Lida com os dados de replicação durante o failback do Azure.<br/><br/> Se os volumes de tráfego de failback forem altos, você poderá implantar um servidor de destino mestre separado para failback.
**Servidores replicados** | Olá componente de serviço de mobilidade está instalado em cada servidor do Windows/Linux que você deseja tooreplicate. Ele pode ser instalado manualmente em cada computador, ou com uma instalação por push saudação do servidor de processo.
**Failback** | Para o failback, uma infraestrutura do VMware é necessária. Não é possível reprovar servidor físico tooa voltar.


**Figura 1: TooAzure físico componentes**

![Componentes](./media/physical-walkthrough-architecture/arch-enhanced.png)

## <a name="replication-process"></a>Processo de replicação

1. Configurar implantação hello, incluindo o local e os componentes do Azure. No cofre de serviços de recuperação hello, você pode especificar origem da replicação hello e destino, configurar o servidor de configuração de hello, criar uma política de replicação, implantar o serviço de mobilidade hello, habilitar a replicação e executar um failover de teste.
2.  Replicar máquinas acordo com a política de replicação hello e uma cópia inicial dos dados de saudação é replicado tooAzure de armazenamento.
4. Após a conclusão da replicação inicial, a replicação delta alterações tooAzure começa. As alterações acompanhadas para uma máquina são mantidas em um arquivo .hrl.
    - Replicadas máquinas se comunicar com servidor de configuração de saudação na porta HTTPS 443 entrada para o gerenciamento de replicação.
    - Replicadas máquinas enviam servidor de processo de toohello de dados de replicação na porta HTTPS 9443 entrada (pode ser modificada).
    - servidor de configuração de saudação orquestra o gerenciamento de replicação com o Azure através da porta HTTPS 443 de saída.
    - servidor de processo Olá recebe dados de máquinas de origem, otimiza criptografa e envia tooAzure armazenamento pela porta 443 saída.
    - Se você habilitar a consistência de várias VMs, em seguida, máquinas no grupo de replicação Olá comunicam entre si pela porta 20004. Várias VMS serão usadas se você agrupar vários computadores em grupos de replicação que compartilham pontos de recuperação consistentes com o aplicativo e com falhas ao realizar o failover. Isso é útil se estiver executando máquinas Olá a mesma carga de trabalho e precisam toobe consistente.
5. O tráfego é replicado tooAzure armazenamento pontos de extremidade públicos, mais Olá da internet. Como alternativa, você pode usar o [emparelhamento público](../expressroute/expressroute-circuit-peerings.md#public-peering) do Azure ExpressRoute. Replicação do tráfego por uma VPN site a site de um tooAzure de site local não tem suporte.

**Figura 2: TooAzure físico replicação**

![Avançado](./media/physical-walkthrough-architecture/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>Processo de failover e failback

Depois de verificar que se o failover de teste está funcionando como esperado, você pode executar failovers não planejados tooAzure conforme necessário. Ao executar um failover, as VMs do Azure são criadas com base nos dados replicados. Depois, quando o site primário local estiver disponível novamente, você poderá fazer failback. Observe que:

- Não há suporte para failover planejado.
- Você pode fazer o failover de um único computador ou criar [planos de recuperação](site-recovery-create-recovery-plans.md), toofail em vários computadores juntos.
- Você pode confirmar uma failover toostart acessando Olá carga de trabalho da réplica Olá VM do Azure.
- Quando o site primário hello está disponível novamente, você replicar máquina de saudação do site primário do hello toohello secundário. Em seguida, execute um failover não planejado do site secundário hello. Após você confirmar esse failover, dados serão back local e você precisa tooenable replicação tooAzure novamente.

Os componentes do failback incluem:

- **Servidor de processo temporário no Azure**: É necessário tooset um tooact de VM do Azure como um servidor de processo, a replicação toohandle do Azure. Você pode excluir a VM após a conclusão do failback.
- **Conexão VPN**: É necessário uma conexão VPN (ou rota expressa do Azure) de saudação do Azure rede toohello no site local.
- **O servidor de destino mestre local separado**: servidor de destino mestre local hello (instalado por padrão no servidor de configuração de saudação) trata o failback. Se você fizer failback de grandes volumes de tráfego, deverá configurar um servidor de destino mestre local separado para essa finalidade.
- **Política de failback**: você precisa de uma política de failback. Isso é criado automaticamente quando você cria sua política de replicação.
- **O VMware infrastructure**: você deve realizar failback tooan de VM do VMware no local. Isso significa que você precisa de uma infra-estrutura de VMware no local, mesmo se você estiver replicando tooAzure de servidores físicos no local.

**Figura 3: Failback de servidor físico**

![Failback](./media/physical-walkthrough-architecture/enhanced-failback.png)


## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 2: verificar os pré-requisitos e limitações](physical-walkthrough-prerequisites.md)
