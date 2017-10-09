---
title: "práticas recomendadas de recuperação de Site aaaAzure | Microsoft Docs"
description: "Este artigo descreve as práticas recomendadas para a implantação do Azure Site Recovery"
services: site-recovery
documentationCenter: 
author: rayne-wiselman"
manager: cfreeman
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-support-matrix-to-azure
ms.openlocfilehash: 288df858a0e1c1f5ad96dbe8b9dd0dc69d8f56ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-ready-toodeploy-azure-site-recovery"></a>Obter toodeploy pronto do Azure Site Recovery

Este artigo descreve como tooprepare para implantação do Azure Site Recovery.

## <a name="protecting-hyper-v-virtual-machines"></a>Protegendo as máquinas virtuais Hyper-V

Você tem algumas opções de implantação para proteger máquinas virtuais Hyper-V. Você pode replicar tooAzure de VMs Hyper local ou datacenter secundário tooa. Há requisitos diferentes para cada implantação.

**Requisito** | **Replicar tooAzure (com o VMM)** | **Replicar máquinas virtuais do Hyper-V tooAzure (sem VMM)** | **Replicar máquinas virtuais do Hyper-V toosecondary site (com o VMM)** | **Detalhes**
---|---|---|---|---
**VMM** | VMM em execução no System Center 2012 R2 <br/><br/>Pelo menos uma nuvem do VMM que contém um ou mais grupos de hosts do VMM. | ND | Servidores do VMM em sites primários e secundários Olá executando pelo menos System Center 2012 SP1 com atualizações mais recentes. <br/><br/> Pelo menos uma nuvem em cada servidor VMM. Nuvens devem ter o perfil de capacidade do Hyper-V de saudação configurado.<br/><br/> nuvem de origem Olá deve ter pelo menos um grupo de hosts do VMM. | Opcional. Você não precisa toohave que System Center VMM implantado em ordem tooAzure de máquinas virtuais de Hyper-V de tooreplicate, mas se você fizer isso, você precisará toomake-se de que o servidor do VMM hello está configurado corretamente. Isso inclui fazer se que você está executando a versão correta de VMM hello e nuvens são configuradas.
**Hyper-V** | Pelo menos um servidor de host do Hyper-V no Olá no local executando o Windows Server 2012 R2 ou posterior | Pelo menos um servidor do Hyper-V em sites de origem e destino de saudação executando pelo menos o Windows Server 2012 com atualizações mais recentes do hello instalado e conectado toohello internet.<br/><br/> servidores do Hyper-V Olá devem ser em um grupo de host em uma nuvem do VMM. | Pelo menos um servidor do Hyper-V em sites de origem e destino de saudação executando pelo menos o Windows Server 2012 com atualizações mais recentes do hello instalado e conectado toohello internet.<br/><br/> servidores do Hyper-V Olá devem estar localizados em um grupo de host em uma nuvem do VMM. |
**Máquinas virtuais** | Pelo menos uma VM no servidor de host do Hyper-V de origem Olá | Pelo menos uma VM no servidor de host de saudação Hyper-V na nuvem do VMM de origem de saudação | Pelo menos uma VM no servidor de host de saudação Hyper-V na nuvem do VMM de origem de saudação. |  VMs replicando tooAzure devem estar de acordo com os pré-requisitos da máquina virtual do Azure
**Conta do Azure** | Você precisará de uma conta do Azure e um serviço de recuperação de Site do toohello de assinatura. | Você precisará de uma conta do Azure e um serviço de recuperação de Site do toohello de assinatura. | ND | Se você não tiver uma conta, comece com uma avaliação gratuita.
**Armazenamento do Azure** | Você precisará de uma assinatura para uma conta de Armazenamento do Azure com replicação geográfica habilitada. | Você precisará de uma assinatura para uma conta de Armazenamento do Azure com replicação geográfica habilitada. | ND | conta de saudação deve estar na Olá mesma região do cofre do Azure Site Recovery hello e estar associada a saudação mesma assinatura.
**Rede** | Configurar tooensure de mapeamento de rede que todos os computadores que o failover em Olá mesma rede do Azure pode se conectar a tooeach outro, independentemente do plano de recuperação que estão em. Além disso, se um gateway de rede é configurar no destino de saudação de rede do Azure, máquinas virtuais podem conectar o tooother em máquinas virtuais. Se você não configurar rede mapeamento somente as máquinas falharem em Olá mesmo plano de recuperação pode se conectar. | ND |  <br/><br/>Configure tooensure de mapeamento de rede que máquinas virtuais são conectadas tooappropriate redes após o failover, e máquinas virtuais de réplica são colocadas idealmente em servidores host Hyper-V. Se você não configurar rede máquinas replicadas de mapeamento não será conectada tooany rede VM após o failover. |  tooset o mapeamento de rede com o VMM, você precisará toomake-se de que a lógica do VMM e redes VM estão configuradas corretamente.
**Provedores e agentes** | Durante a implantação, você instalará Olá provedor Azure Site Recovery em servidores do VMM. Em servidores Hyper-V nas nuvens do VMM você instalará o agente de serviços de recuperação do Azure hello. | Durante a implantação você instalará Olá provedor Azure Site Recovery e o agente de serviços de recuperação do Azure Olá em cluster ou servidor de host do Hyper-V Olá| Durante a implantação, você instalará Olá provedor Azure Site Recovery em servidores do VMM. Em servidores Hyper-V nas nuvens do VMM você instalará o agente de serviços de recuperação do Azure hello. | Provedores e agentes tooSite recuperação sobre Olá conectar-se à internet usando uma conexão HTTPS criptografado. Você não precisa tooadd exceções de firewall ou criar um proxy específico para a conexão do provedor de saudação.
**Conectividade com a Internet** | Somente os servidores do VMM Olá precisam de uma conexão de internet | Somente Olá servidores de host de Hyper-V precisam de uma conexão de internet | Somente servidores do VMM precisam de uma conexão com a internet | Máquinas virtuais não precisa de nada instalado neles e não se conectar diretamente toohello internet.



## <a name="protect-vmware-virtual-machines-or-physical-servers"></a>Proteger máquinas virtuais VMware ou servidores físicos

Há algumas opções de implantação para a proteção de máquinas virtuais VMware ou de servidores físicos com Windows/Linux. Você pode replicá-los tooAzure ou datacenter secundário tooa. Há requisitos diferentes para cada implantação.

**Requisito** | **Replicar máquinas virtuais/físicas VMware servidores tooAzure)** | * **Replicar máquinas virtuais VMware/físicos servidores toosecondary site**  
---|---|---
**Site primário** | **Servidor de processo**: um servidor dedicado com Windows (físico ou virtual) | **Servidor de processo**: um servidor dedicado com Windows (físico ou máquina virtual VMware)<br/><br/>  
**Site local secundário** | ND | **Servidor de configuração**: um servidor dedicado com Windows (físico ou virtual) <br/><br/> **Servidor de destino mestre**: um servidor dedicado (físico ou virtual). Configure com máquinas do Windows tooprotect Windows ou Linux tooprotect Linux.
**As tabelas** | **Assinatura**: você precisará de uma assinatura para Olá serviço de recuperação de Site. <br/><br/> **Conta de armazenamento**: você precisará de uma conta de armazenamento com replicação geográfica habilitada. conta de saudação deve estar na Olá mesma região do Cofre de recuperação de Site hello e estar associada a saudação mesma assinatura. <br/><br/> **Servidor de configuração**: você precisará tooset o servidor de configuração de saudação como uma VM do Azure <br/><br/> **Servidor de destino mestre**: você precisará tooset o servidor de destino mestre hello como uma VM do Azure <br/><br/> Configure com máquinas do Windows tooprotect Windows ou Linux tooprotect Linux.<br/><br/> **Rede virtual do Azure**: você precisará de uma rede virtual do Azure no qual Olá servidor de configuração e o servidor de destino mestre serão implantados. Ele deve estar no hello mesma assinatura e região do cofre Azure Site Recovery Olá | ND  
**Máquinas virtuais/servidores físicos** | Pelo menos uma máquina virtual de VMware ou servidor físico do Windows/Linux.<br/><br/>Durante a implantação Olá serviço de mobilidade será instalado em cada máquina| Pelo menos uma VM VMware ou servidor físico com Windows/Linux.<br/><br/> Durante a implantação do agente de unificada de saudação está instalado em cada computador.




## <a name="azure-virtual-machine-requirements"></a>Requisitos de máquina virtual do Azure

Você pode implantar a recuperação de Site tooreplicate VMs e servidores físicos executando qualquer sistema operacional com suporte pelo Azure. Isso inclui a maioria das versões do Windows e do Linux. Você precisará toomake-se que máquinas virtuais que você deseja tooprotect estão em conformidade com os requisitos do Azure no local.


## <a name="optimizing-your-deployment"></a>Otimizando sua implantação

Use Olá dicas toohelp otimizar e dimensionar sua implantação a seguir.

- **Tamanho de volume do sistema operacional**: quando você replicar uma saudação tooAzure de máquina virtual operacional volume do sistema deve ser menor que 1 TB. Se você tiver mais volumes que isso você pode movê-las manualmente tooa outro disco antes de iniciar a implantação.
- **Tamanho de disco de dados**: se você estiver replicando tooAzure, você pode ter até too32 discos de dados em uma máquina virtual, cada um com um máximo de 1 TB. Você pode replicar e realizar de forma efetiva o failover de uma máquina virtual de aproximadamente 32 TB.
- **Limites de plano de recuperação**: recuperação de Site pode ser dimensionado toothousands de máquinas virtuais. Planos de recuperação são projetados como um modelo para aplicativos que devem executar failover em conjunto para limitamos Olá número de máquinas em um too50 do plano de recuperação.
- **Limites de serviço do Azure**: toda assinatura do Azure vem com um conjunto de limites padrão de núcleos, serviços de nuvem etc. É recomendável que você execute uma disponibilidade de saudação do teste failover toovalidate dos recursos em sua assinatura. Você pode modificar esses limites por meio do suporte do Azure.
- **Planejamento de capacidade**: planeje o desempenho e o dimensionamento.
- **Largura de banda de replicação**: se você tiver pouca largura de banda de replicação, observe o seguinte:
    - **ExpressRoute**: a Recuperação de Site funciona com o Azure ExpressRoute e com otimizadores de WAN, por exemplo, Riverbed.
    - **Tráfego de replicação**: recuperação de Site usa executa a replicação inicial inteligente usando apenas os blocos de dados e não Olá VHD inteiro. Somente as alterações são replicadas durante a replicação contínua.
    - **O tráfego de rede**: você pode controlar o tráfego de rede usado para replicação, configurando a QoS do Windows com uma política com base no endereço IP de destino hello e porta.  Além disso, se você estiver replicando tooAzure recuperação de Site usando hello Azure Backup agent. Você pode configurar a limitação para esse agente.
- **RTO**: se você quiser toomeasure Olá tempo objetivo de recuperação (RTO) você pode esperar com o Site Recovery sugerimos que você executar um failover de teste e exibição tooanalyze de trabalhos de recuperação de Site Olá quanto tempo leva toocomplete operações hello. Se você estiver realizando o failover tooAzure, para Olá RTO melhor, é recomendável que você automatizar todas as ações manuais integrando a recuperação da automação do Azure planos.
- **RPO**: recuperação de Site oferece suporte a um objetivo de ponto de recuperação próximo síncrono (RPO) quando você replica tooAzure. Isso pressupõe uma largura de banda suficiente entre seu armazenamento de dados e o Azure.
