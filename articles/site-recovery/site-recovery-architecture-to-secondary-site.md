---
title: "aaaHow funciona local machine replicação tooa local secundário site no Azure Site Recovery? | Microsoft Docs"
description: "Este artigo fornece uma visão geral dos componentes e arquitetura usada quando replicar local VMs e servidores físicos tooa secundário com hello serviço Azure Site Recovery."
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
ms.openlocfilehash: 097a3f43446fec69ed7f9e0b7f11e8d11f41cc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-on-premises-machine-replication-tooa-secondary-site-work-in-site-recovery"></a>Como o local máquina replicação tooa site secundário trabalho na recuperação de Site?

Este artigo descreve os componentes de saudação e processos envolvidos ao replicar local máquinas virtuais e servidores físicos tooAzure, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço.

Você pode replicar Olá tooa secundária no local a seguir:
- VMs do Hyper-V em clusters Hyper-V e hosts autônomos gerenciadas em nuvens VMM (System Center Virtual Machine Manager).
- VMs VMware locais e servidores físicos do Windows/Linux. Neste cenário, a replicação é gerenciada pelo Scout.

Lançar os comentários na parte inferior deste artigo ou de saudação do hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="replicate-hyper-v-vms-tooa-secondary-on-premises-site"></a>Replicar máquinas virtuais do Hyper-V tooa secundário no site local


### <a name="architectural-components"></a>Componentes de arquitetura

Aqui está o que você precisa para a replicação de site secundário do tooa de VMs Hyper-V.

**Componente** | **Localidade** | **Detalhes**
--- | --- | ---
**As tabelas** | Você precisa de uma conta na Microsoft. |
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

**Figura 1: A replicação do VMM tooVMM**

![Tooon local no local](./media/site-recovery-components/arch-onprem-onprem.png)

### <a name="failover-and-failback-process"></a>Processo de failover e failback

1. Você pode executar um [failover](site-recovery-failover.md) planejado ou não planejado entre sites locais. Se você executar um failover planejado, máquinas virtuais de origem são encerrados tooensure sem perda de dados.
2. Você pode fazer o failover de um único computador ou criar [planos de recuperação](site-recovery-create-recovery-plans.md) tooorchestrate failover de várias máquinas.
4. Se você executar um failover não planejado tooa site secundário, depois de executar failover em máquinas Olá no local secundário Olá não está habilitado para proteção ou replicação. Se você tiver executado um failover planejado, após o failover hello, as máquinas no local secundário Olá são protegidas.
5. Em seguida, você confirmar Olá failover toostart acessando Olá carga de trabalho da réplica Olá VM.
6. Quando seu site primário está disponível novamente, você pode iniciar tooreplicate replicação inversa da saudação site secundário toohello primário. Replicação inversa coloca máquinas virtuais de saudação em um estado protegido, mas o datacenter secundário Olá ainda é local ativo hello.
7. site primário do hello toomake em local ativo Olá novamente, você iniciar um failover planejado de tooprimary secundário, seguido de outra replicação inversa.




## <a name="replicate-vmware-vmsphysical-servers-tooa-secondary-site"></a>Replicar máquinas virtuais VMware/físicos servidores tooa site secundário

Replicar máquinas virtuais do VMware ou servidores físicos tooa secundário usando InMage Scout, usando esses componentes de arquitetura:


### <a name="architectural-components"></a>Componentes de arquitetura

**Componente** | **Localidade** | **Detalhes**
--- | --- | ---
**As tabelas** | InMage Scout. | tooobtain InMage Scout, você precisa de uma assinatura do Azure.<br/><br/> Depois de criar um cofre de serviços de recuperação, você baixar InMage Scout e instalar Olá tooset mais recente de atualizações a implantação de saudação.
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

**Figura 2: VMware tooVMware replicação**

![VMware tooVMware](./media/site-recovery-components/vmware-to-vmware.png)


## <a name="next-steps"></a>Próximas etapas

Saudação de revisão [matriz de suporte](site-recovery-support-matrix-to-sec-site.md)
