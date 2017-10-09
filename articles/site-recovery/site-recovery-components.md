---
title: "aaaHow faz o trabalho de recuperação de Site? | Microsoft Docs"
description: "Este artigo fornece uma visão geral da arquitetura de Recuperação de Site"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-azure-to-azure-architecture
ms.openlocfilehash: ff1580d0fe294148dc0c621728491e6119c3048a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-site-recovery-work-for-on-premises-infrastructure"></a>Como funciona o Azure Site Recovery para a infraestrutura local?

> [!div class="op_single_selector"]
> * [Replicar as máquinas virtuais do Azure](site-recovery-azure-to-azure-architecture.md)
> * [Replicar as máquinas locais](site-recovery-components.md)

Este artigo descreve a arquitetura subjacentes do hello [do Azure Site Recovery](site-recovery-overview.md) serviço e Olá componentes funcionam para replicar as cargas de trabalho de tooAzure local.

Lançar os comentários na parte inferior deste artigo ou de saudação do hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="replicate-tooazure"></a>Replicar tooAzure

Você pode replicar e proteger os seguintes Olá tooAzure de infraestrutura local:

- **VMware**: VMS VMware locais em execução em um [host com suporte](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). Replique VMs VMware executando [sistemas operacionais com suporte](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)
- **Hyper-V**: VMs Hyper-V locais em execução em [hosts com suporte](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).
- **Máquinas físicas**: servidores físicos locais executando Windows ou Linux em [sistemas operacionais com suporte](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions). Replique VMs Hyper-V executando qualquer sistema operacional convidado [com suporte do Hyper-V e do Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).

## <a name="vmware-tooazure"></a>VMware tooAzure

Aqui está o que você precisa para replicar tooAzure VMs VMware.

Área | Componente | Detalhes
--- | --- | ---
**Servidor de configuração** | Um único servidor de gerenciamento (VM VMWare) executa todos os locais - servidor de configuração, servidor de processo, servidor de destino mestre | servidor de configuração de saudação coordena as comunicações entre o local e o Azure e gerencia a replicação de dados.
 **Servidor de processo**:  | Instalado por padrão no servidor de configuração de saudação. | Atua como um gateway de replicação. Recebe dados de replicação, otimizá-lo com o cache, a compactação e criptografia e envia tooAzure armazenamento.<br/><br/> servidor de processo Olá também lida com a instalação por push de máquinas de tooprotected de serviço de mobilidade hello e executa a descoberta automática de máquinas virtuais do VMware.<br/><br/> À medida que aumenta sua implantação, você pode adicionar mais processo dedicado separado servidores toohandle aumentar os volumes de tráfego de replicação.
 **Servidor de destino mestre** | Instalado por padrão no servidor de configuração local hello. | Lida com os dados de replicação durante o failback do Azure.<br/><br/> Se os volumes de tráfego de failback forem altos, você poderá implantar um servidor de destino mestre separado para failback.
**Servidores VMware** | Máquinas virtuais do VMware são hospedadas em servidores de ESXi do vSphere, e é recomendável um vCenter hosts de saudação do servidor toomanage. | Adicione o Cofre de serviços de recuperação de tooyour de servidores do VMware.<br/><br/>
**Computadores replicados** | Olá serviço de mobilidade será instalado em cada máquina virtual que você deseja tooreplicate VMware. Ele pode ser instalado manualmente em cada computador, ou com uma instalação por push saudação do servidor de processo.| -

**Figura 1: VMware tooAzure componentes**

![Componentes](./media/site-recovery-components/arch-enhanced.png)

### <a name="replication-process"></a>Processo de replicação

1. Configurar implantação hello, incluindo componentes do Azure e um cofre de serviços de recuperação. No cofre Olá você especificar origem da replicação hello e destino, configurar o servidor de configuração Olá, adicionar servidores VMware, crie uma política de replicação, implantar o serviço de mobilidade Olá, habilitar a replicação e executar um failover de teste.
2.  Máquinas iniciam a replicação de acordo com a política de replicação Olá, e uma cópia inicial dos dados de saudação é replicado tooAzure armazenamento.
4. A replicação de tooAzure de alterações delta começa após a conclusão da replicação inicial de saudação. As alterações acompanhadas para uma máquina são mantidas em um arquivo .hrl.
    - Replicadas máquinas se comunicar com servidor de configuração de saudação na porta HTTPS 443 entrada para o gerenciamento de replicação.
    - Replicadas máquinas enviam servidor de processo de toohello de dados de replicação na porta HTTPS 9443 entrada (pode ser configurado).
    - servidor de configuração de saudação orquestra o gerenciamento de replicação com o Azure através da porta HTTPS 443 de saída.
    - servidor de processo Olá recebe dados de máquinas de origem, otimiza criptografa e envia tooAzure armazenamento pela porta 443 saída.
    - Se você habilitar a consistência de várias VMs, em seguida, máquinas no grupo de replicação Olá comunicam entre si pela porta 20004. Várias VMS serão usadas se você agrupar vários computadores em grupos de replicação que compartilham pontos de recuperação consistentes com o aplicativo e com falhas ao realizar o failover. Isso é útil se estiver executando máquinas Olá a mesma carga de trabalho e precisam toobe consistente.
5. O tráfego é replicado tooAzure armazenamento pontos de extremidade públicos, mais Olá da internet. Como alternativa, você pode usar o [emparelhamento público](https://docs.microsoft.com/en-us/azure/expressroute/expressroute-circuit-peerings#public-peering) do Azure ExpressRoute. Replicação do tráfego por uma VPN site a site de um tooAzure de site local não tem suporte.

**Figura 2: VMware tooAzure replicação**

![Avançado](./media/site-recovery-components/v2a-architecture-henry.png)

### <a name="failover-and-failback"></a>Failover e failback

1. Depois de verificar que se o failover de teste está funcionando como esperado, você pode executar failovers não planejados tooAzure conforme necessário. Não há suporte para failover planejado.
2. Você pode fazer o failover de um único computador ou criar [planos de recuperação](site-recovery-create-recovery-plans.md), toofail entre várias VMs.
3. Ao executar um failover, VMs de réplica são criadas no Azure. Você pode confirmar uma failover toostart acessando Olá carga de trabalho da réplica Olá VM do Azure.
4. Quando o site primário local estiver disponível novamente, você poderá executar o failback. Configurar uma infra-estrutura de failback, iniciar a replicação de máquina de saudação do hello site secundário toohello primário e executar um failover não planejado do site secundário hello. Após você confirmar esse failover, dados serão back local e você precisa tooenable replicação tooAzure novamente. [Saiba mais](site-recovery-failback-azure-to-vmware.md)

**Figura 3: failback físico/de VMware**

![Failback](./media/site-recovery-components/enhanced-failback.png)

## <a name="physical-tooazure"></a>TooAzure físico

Quando você replica tooAzure de servidores locais físicos, a replicação usa também Olá mesmo componentes e processos como [tooAzure VMware](#vmware-replication-to-azure), mas observe essas diferenças:

- Você pode usar um servidor físico para o servidor de configuração hello, em vez de uma VM do VMware
- Você precisará de uma infraestrutura do VMware local para failback. Não é possível reprovar máquina física tooa voltar.

## <a name="hyper-v-tooazure"></a>TooAzure Hyper-V

### <a name="replication-process"></a>Processo de replicação

1. Você configurar Olá componentes do Azure. Recomendamos que você configure as contas de armazenamento e rede antes de começar a implantação da Recuperação de Site.
2. Crie um cofre de Serviços de Replicação para Recuperação de Site e defina configurações de cofre, incluindo:
    - Configurações de origem e destino. Se você não estiver gerenciando hosts Hyper-V em uma nuvem VMM, para o destino de saudação você cria um contêiner do Hyper-V site e adicionar tooit de hosts do Hyper-V. Se os hosts Hyper-V gerenciados no VMM, origem Olá é saudação do VMM. destino de saudação é o Azure.
    - Instalação do hello provedor Azure Site Recovery e o agente de serviços de recuperação do Microsoft Azure hello. Se você tiver Olá VMM provedor será instalado nele e Olá agente em cada host Hyper-V. Se você não tiver o VMM, Olá provedor e agente estão instalados em cada host.
    - Você criar uma política de replicação para o site do Hyper-V hello ou nuvem do VMM. política de saudação é tooall aplicada VMs localizadas em hosts na nuvem ou site hello.
    - Você habilita a replicação para VMs do Hyper-V. A replicação inicial ocorre de acordo com as configurações de política de replicação hello.
4. As alterações de dados são rastreadas e a replicação de tooAzure de alterações delta começa após a conclusão da replicação inicial de saudação. As alterações acompanhadas para um item são mantidas em um arquivo .hrl.
5. Executar um toomake de failover de teste se tudo está funcionando.

### <a name="failover-and-failback-process"></a>Processo de failover e failback

1. Você pode executar um planejado ou não planejado [failover](site-recovery-failover.md) de tooAzure de VMs Hyper-V local. Se você executar um failover planejado, máquinas virtuais de origem são encerrados tooensure sem perda de dados.
2. Você pode fazer o failover de um único computador ou criar [planos de recuperação](site-recovery-create-recovery-plans.md) tooorchestrate failover de várias máquinas.
4. Depois de executar failover hello, deve ser capaz de toosee Olá criado VMs de réplica no Azure. Você pode atribuir um toohello de endereço IP público VM se necessário.
5. Em seguida, confirmar Olá failover toostart acessando a carga de trabalho de saudação da réplica Olá VM do Azure.
6. Quando o site primário local estiver disponível novamente, você poderá executar o [failback](site-recovery-failback-from-azure-to-hyper-v.md). Disparar um failover planejado de um site primário toohello do Azure. Para um failover planejado, que você pode selecione toofailback toohello mesmo VM ou tooan um local alternativo e sincronizar alterações entre o Azure e no local, tooensure sem perda de dados. Quando as VMs são criadas no local, você confirmar failover de saudação.

**Figura 4: Replicação de tooAzure do site de Hyper-V**

![Componentes](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)

**Figura 5: TooAzure replicação de nuvem do Hyper-V no VMM**

![Componentes](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png)


## <a name="replicate-tooa-secondary-site"></a>Site secundário tooa replicar

Você pode replicar Olá site secundário tooyour a seguir:

- **VMware**: VMS VMware locais em execução em um [host com suporte](site-recovery-support-matrix-to-sec-site.md#on-premises-servers). Replique VMs VMware executando [sistemas operacionais com suporte](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions)
- **Máquinas físicas**: servidores físicos locais executando Windows ou Linux em [sistemas operacionais com suporte](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions).
- **Hyper-V**: VMs Hyper-V locais em execução em [hosts Hyper-V com suporte](site-recovery-support-matrix-to-sec-site.md#on-premises-servers) gerenciados em nuvens VMM. [hosts com suporte](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). Replique VMs Hyper-V executando qualquer sistema operacional convidado [com suporte do Hyper-V e do Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).


## <a name="vmwarephysical-tooa-secondary-site"></a>Site secundário tooa VMware/físicos

Replicar máquinas virtuais do VMware ou servidores físicos tooa secundário usando InMage Scout.

### <a name="components"></a>Componentes

**Área** | **Componente** | **Detalhes**
--- | --- | ---
**Servidor de processo** | Localizado no site primário | Implantar Olá processo servidor toohandle cache, a compactação e a otimização de dados.<br/><br/> Ele também lida com a instalação por push de hello toomachines Unified agente deseja tooprotect.
**Servidor de configuração** | Localizado no site secundário | gerencia o servidor de configuração de Hello, configurar e monitorar sua implantação, ou usando o site de gerenciamento de saudação ou console de vContinuum de saudação.
**Servidor vContinuum** | Opcional. Instalado em Olá mesmo local como servidor de configuração de saudação. | Ele fornece um console para o gerenciamento e monitoramento de seu ambiente protegido.
**Servidor de destino mestre** | Localizado no site secundário Olá | o servidor de destino mestre Olá mantém os dados replicados. Recebe dados de saudação do servidor de processo, cria uma máquina de réplica no site secundário hello e contém pontos de retenção de dados de saudação.<br/><br/> número de saudação de servidores de destino mestre que você precisa depende número Olá das máquinas que você está protegendo.<br/><br/> Se desejar que o site primário do toofail toohello back, é necessário um servidor de destino mestre há muito. Olá unificado agente está instalado neste servidor.
**Servidor VMware ESX/ESXi e vCenter** |  VMs são hospedadas em hosts ESX/ESXi. Hosts são gerenciados com um servidor do vCenter | Você precisa de uma infra-estrutura de VMware tooreplicate VMs VMware.
**VMs/servidores físicos** |  Unified agente instalado em máquinas virtuais do VMware e servidores físicos que você deseja tooreplicate. | Agente de saudação atua como um provedor de comunicação entre todos os componentes de saudação.


### <a name="replication-process"></a>Processo de replicação

1. Configurar servidores de componente de saudação em cada site (configuração, processo, destino mestre) e instalar Olá unificada agente em computadores que você deseja tooreplicate.
2. Após a replicação inicial, o agente de saudação em cada computador envia o servidor de processo do delta replicação alterações toohello.
3. servidor de processo Olá otimiza os dados de saudação e transfere-o servidor de destino mestre toohello no site secundário hello. servidor de configuração de saudação gerencia o processo de replicação de saudação.

**Figura 6: VMware tooVMware replicação**

![VMware tooVMware](./media/site-recovery-components/vmware-to-vmware.png)



## <a name="hyper-v-tooa-secondary-site"></a>Site secundário do Hyper-V tooa

Aqui está o que você precisa para a replicação de site secundário do tooa de VMs Hyper-V.


**Área** | **Componente** | **Detalhes**
--- | --- | ---
**Servidor VMM** | É recomendável um servidor do VMM no site primário hello e um no site secundário Olá | Cada servidor do VMM deve ser toohello conectado à internet.<br/><br/> Cada servidor deve ter pelo menos uma nuvem privada do VMM, com um conjunto de perfis de funcionalidade Olá Hyper-V.<br/><br/> Você pode instalar Olá provedor Azure Site Recovery no servidor do VMM hello. Olá provedor coordena e coordena a replicação com o serviço de recuperação de Site do hello sobre Olá internet. As comunicações entre hello provedor e do Azure são seguro e criptografado.
**Servidor Hyper-V** |  Um ou mais servidores Hyper-V host nas nuvens de saudação primários e secundários do VMM.<br/><br/> Os servidores devem estar toohello conectado à internet.<br/><br/> Dados são replicados entre Olá servidores primários e secundários Hyper-V host via LAN hello ou VPN, usando a autenticação Kerberos ou certificados.  
**VMs Hyper-V** | Localizado no servidor de host do Hyper-V de origem hello. | servidor de host de origem Olá deve ter pelo menos uma VM que você deseja tooreplicate.

### <a name="replication-process"></a>Processo de replicação

1. Configurar Olá conta do Azure.
2. Crie um cofre de Serviços de Replicação para Recuperação de Site e defina configurações de cofre, incluindo:

    - origem de replicação de saudação e de destino (sites primários e secundários).
    - Instalação do hello provedor Azure Site Recovery e o agente de serviços de recuperação do Microsoft Azure hello. Olá provedor é instalado em servidores do VMM e o agente de saudação em cada host Hyper-V.
    - Você cria uma política de replicação para a nuvem do VMM de origem. política de saudação é aplicado tooall as VMs localizadas nos hosts na nuvem de saudação.
    - Você habilita a replicação para VMs do Hyper-V. A replicação inicial ocorre de acordo com as configurações de política de replicação hello.
4. As alterações de dados são controladas, e a replicação delta altera toobegins após a conclusão da replicação inicial de saudação. As alterações acompanhadas para um item são mantidas em um arquivo .hrl.
5. Executar um toomake de failover de teste se tudo está funcionando.

**Figura 7: Replicação de tooVMM VMM**

![Tooon local no local](./media/site-recovery-components/arch-onprem-onprem.png)

### <a name="failover-and-failback"></a>Failover e failback

1. Você pode executar um [failover](site-recovery-failover.md) planejado ou não planejado entre sites locais. Se você executar um failover planejado, máquinas virtuais de origem são encerrados tooensure sem perda de dados.
2. Você pode fazer o failover de um único computador ou criar [planos de recuperação](site-recovery-create-recovery-plans.md) tooorchestrate failover de várias máquinas.
4. Se você executar um failover não planejado tooa site secundário, depois de executar failover em máquinas Olá no local secundário Olá não está habilitado para proteção ou replicação. Se você tiver executado um failover planejado, após o failover hello, as máquinas no local secundário Olá são protegidas.
5. Em seguida, você confirmar Olá failover toostart acessando Olá carga de trabalho da réplica Olá VM.
6. Quando seu site primário está disponível novamente, você pode iniciar tooreplicate replicação inversa da saudação site secundário toohello primário. Replicação inversa coloca máquinas virtuais de saudação em um estado protegido, mas o datacenter secundário Olá ainda é local ativo hello.
7. site primário do hello toomake em local ativo Olá novamente, você iniciar um failover planejado de tooprimary secundário, seguido de outra replicação inversa.


## <a name="next-steps"></a>Próximas etapas

- [Saiba mais](site-recovery-hyper-v-azure-architecture.md) sobre fluxo de trabalho de replicação Olá Hyper-V.
- [Verificar pré-requisitos](site-recovery-prereq.md)
