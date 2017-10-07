---
title: 'Azure Site Recovery: perguntas frequentes | Microsoft Docs'
description: "Este artigo aborda dúvidas comuns sobre o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5cdc4bcd-b4fe-48c7-8be1-1db39bd9c078
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/22/2017
ms.author: raynew
ms.openlocfilehash: 6d0bd2475466e5745e1f084bd2267d954d624ebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-frequently-asked-questions-faq"></a>Azure Site Recovery: perguntas frequentes
Este artigo contém perguntas frequentes sobre o Azure Site Recovery. Se você tiver dúvidas depois de ler este artigo, poste-as no hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).

## <a name="general"></a>Geral
### <a name="what-does-site-recovery-do"></a>O que faz o Site Recovery?
Recuperação de site contribuição de continuidade de negócios tooyour e estratégia de recuperação (BCDR) de desastres, orquestrar e automatizar a replicação de máquinas virtuais do Azure entre regiões, máquinas virtuais em locais e servidores físicos tooAzure e tooa máquinas locais datacenter secundário. [Saiba mais](site-recovery-overview.md).

### <a name="what-can-site-recovery-protect"></a>O que o Site Recovery pode proteger?
* **VMs do Azure**: o Site Recovery pode replicar qualquer carga de trabalho em execução em uma VM do Azure com suporte
* **Máquinas virtuais do Hyper-V**: o Site Recovery pode proteger qualquer carga de trabalho em execução em uma VM Hyper-V.
* **Servidores físicos**: o Site Recovery pode proteger servidores físicos com o Windows ou o Linux em execução.
* **Máquinas virtuais VMware**: o Site Recovery pode proteger qualquer carga de trabalho em execução em uma VM VMware.

### <a name="does-site-recovery-support-hello-azure-resource-manager-model"></a>Recuperação de Site dá suporte ao modelo do Azure Resource Manager Olá?
Recuperação de site está disponível no portal do Azure com suporte para o Gerenciador de recursos de saudação. Recuperação de site oferece suporte a implantações herdadas Olá portal clássico do Azure. Não é possível criar novos cofres no portal clássico do hello, e não há suporte para novos recursos.

### <a name="can-i-replicate-azure-vms"></a>Posso replicar VMs do Azure?
Sim, você pode replicar VMs do Azure com suporte entre regiões do Azure. [Saiba mais](site-recovery-azure-to-azure.md).

### <a name="what-do-i-need-in-hyper-v-tooorchestrate-replication-with-site-recovery"></a>O que é necessário na replicação do Hyper-V tooorchestrate com a recuperação de Site?
Para o servidor de host do Hyper-V Olá o que você precisa depende de cenário de implantação de saudação. Check-out Olá pré-requisitos do Hyper-V em:

* [Replicando tooAzure de VMs Hyper-V (sem VMM)](site-recovery-hyper-v-site-to-azure.md)
* [Replicando tooAzure de VMs Hyper-V (com o VMM)](site-recovery-vmm-to-azure.md)
* [Replicando o datacenter secundário de tooa de VMs Hyper-V](site-recovery-vmm-to-vmm.md)
* Se você estiver replicando tooa secundário datacenter leia sobre [sistemas operacionais convidados suportados para máquinas virtuais do Hyper-V](https://technet.microsoft.com/library/mt126277.aspx).
* Se você estiver replicando tooAzure, recuperação de Site oferece suporte a todos os sistemas de operacionais de convidados de saudação que são [tem suporte pelo Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx).

### <a name="can-i-protect-vms-when-hyper-v-is-running-on-a-client-operating-system"></a>Posso proteger VMs quando o Hyper-V está em execução em um sistema operacional cliente?
Não, as VMs devem estar localizadas em um servidor de host do Hyper-V sendo executado em uma máquina do servidor Windows com suporte. Se você precisar tooprotect um computador cliente você pode replicá-lo como uma máquina física muito[Azure](site-recovery-vmware-to-azure.md) ou um [datacenter secundário](site-recovery-vmware-to-vmware.md).

### <a name="what-workloads-can-i-protect-with-site-recovery"></a>Quais cargas de trabalho posso proteger com o Site Recovery?
Você pode usar a recuperação de Site tooprotect a maioria das cargas de trabalho em execução em uma VM com suporte ou o servidor físico. Recuperação de site fornece suporte para replicação com reconhecimento de aplicativos, para que os aplicativos podem ser recuperados do estado de tooan inteligente. Ele se integra aos aplicativos da Microsoft, incluindo o SharePoint, Exchange, Dynamics, SQL Server e Active Directory, e trabalha em conjunto com os principais fornecedores, incluindo Oracle, SAP, IBM e Red Hat. [Saiba mais](site-recovery-workload.md) sobre a proteção de carga de trabalho.

### <a name="do-hyper-v-hosts-need-toobe-in-vmm-clouds"></a>Hosts Hyper-V são necessário toobe nas nuvens do VMM?
Se você quiser tooreplicate tooa o datacenter secundário, e máquinas virtuais do Hyper-V deve estar em Hyper-V hospeda os servidores localizados em uma nuvem do VMM. Se você quiser tooreplicate tooAzure, você pode replicar máquinas virtuais nos servidores de host do Hyper-V com ou sem nuvens do VMM. [Leia mais](site-recovery-hyper-v-site-to-azure.md).

### <a name="can-i-deploy-site-recovery-with-vmm-if-i-only-have-one-vmm-server"></a>Posso implantar o Site Recovery com VMM se eu tiver apenas um servidor VMM?

Sim. Ou você pode replicar máquinas virtuais em servidores Hyper-V no tooAzure de nuvem do VMM hello, ou pode replicar entre nuvens do VMM no hello mesmo servidor. Para replicação de local tooon local, é recomendável que você tenha um servidor do VMM em ambos os sites primários e secundários de saudação.  

### <a name="what-physical-servers-can-i-protect"></a>Quais servidores físicos posso proteger?
Você pode replicar os servidores físicos executando o Windows e Linux tooAzure ou tooa site secundário. [Saiba mais](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) sobre os requisitos do sistema operacional.  Olá mesmos requisitos se aplicam se você estiver replicando tooAzure de servidores físicos ou site secundário tooa.


Observe que servidores físicos serão executados como VMs no Azure se seu servidor local ficar inativo. Failback tooan local atualmente não há suporte para servidor físico. Para um computador protegido como físico, você pode apenas failback tooa máquina virtual VMware.

### <a name="what-vmware-vms-can-i-protect"></a>Quais VMs VMware posso proteger?

tooprotect VMs VMware você precisará de um hipervisor vSphere e máquinas virtuais executando as ferramentas do VMware. Também recomendamos que você tenha um toomanage Olá hipervisores do VMware vCenter server. [Saiba mais](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) sobre os requisitos exatos para replicação de servidores VMware e VMs tooAzure ou site secundário tooa.


### <a name="can-i-manage-disaster-recovery-for-my-branch-offices-with-site-recovery"></a>Posso gerenciar a recuperação de desastre nas minhas filiais com o Site Recovery?
Sim. Quando você usa o Site Recovery tooorchestrate replicação e failover em suas filiais, você terá uma orquestração unificada e o modo de exibição de todas as suas cargas de trabalho da office de ramificação em um local central. Você pode facilmente executar failovers e administrar a recuperação de desastres de todas as ramificações de seu escritório principal, sem visitar ramificações hello.

## <a name="pricing"></a>Preços

### <a name="what-charges-do-i-incur-while-using-azure-site-recovery"></a>Quais encargos serão cobrados quando eu usar o Azure Site Recovery?
Quando você usa a recuperação de Site, incorre em encargos para licenças de recuperação de Site hello, armazenamento do Azure, transações de armazenamento e transferência de dados de saída. [Saiba mais](https://azure.microsoft.com/pricing/details/site-recovery).

Olá a licença de recuperação de Site é por instância protegida, onde uma instância é uma VM ou um servidor físico.

- Se um disco VM replica tooa conta de armazenamento padrão, Olá custos de armazenamento do Azure é para consumo de armazenamento de saudação. Por exemplo, se o tamanho do disco de origem Olá é 1 TB e 400 GB é usado, recuperação de Site cria um VHD de 1 TB no Azure, mas armazenamento Olá cobrado é 400 GB (mais a quantidade de saudação do espaço de armazenamento usado para logs de replicação).
- Se um disco VM replica a conta de armazenamento premium tooa, Olá custos de armazenamento do Azure é para tamanho de armazenamento Olá provisionado, cercado para hello mais próximo da opção de disco de armazenamento premium. Por exemplo, se o tamanho do disco de origem Olá for 50 GB, recuperação de Site cria um disco de 50 GB no Azure e o Azure mapeia esse toohello mais próximo do disco de armazenamento premium (P10).  Os custos são calculados em P10 e não no tamanho do disco de 50 GB hello.  [Saiba mais](https://aka.ms/premium-storage-pricing).  Se você estiver usando o armazenamento premium, uma conta de armazenamento padrão para o log de replicação também é necessária e quantidade de saudação do espaço de armazenamento padrão usado para esses logs também é cobrada.
- Nenhum disco é criado até a realização de um failover de teste ou de um failover. No estado de replicação hello, armazenamento de encargos na categoria de saudação de "blob de páginas e de disco" de acordo com a saudação [Calculadora de preços de armazenamento](https://azure.microsoft.com/en-in/pricing/calculator/) incorridas. Esses encargos baseiam-se no tipo de armazenamento de saudação de redundância de dados premium/standard e Olá digite - LRS, GRS, RA-GRS etc.
- Se Olá opção toouse discos gerenciado em um failover estiver selecionado, [encargos para discos gerenciados](https://azure.microsoft.com/en-in/pricing/details/managed-disks/) aplicar após um failover de teste/failover. Os encargos de discos gerenciados não se aplicam durante a replicação.
- Se Olá opção toouse gerenciado discos em um failover não estiver selecionada, armazenamento de encargos na categoria de saudação de "blob de páginas e de disco" de acordo com a saudação [Calculadora de preços de armazenamento](https://azure.microsoft.com/en-in/pricing/calculator/) incorridas após o failover. Esses encargos baseiam-se no tipo de armazenamento de saudação de redundância de dados premium/standard e Olá digite - LRS, GRS, RA-GRS etc.
- As transações de armazenamento são cobradas durante a replicação de estado estacionário e para operações regulares de VM após um failover/failover de teste. Mas essas cobranças são insignificantes.

Também os custos são durante o failover de teste, onde os custos de transações de VM, armazenamento, saída e armazenamento Olá serão aplicados.



## <a name="security"></a>Segurança
### <a name="is-replication-data-sent-toohello-site-recovery-service"></a>Dados de replicação enviados toohello serviço de recuperação de Site?
Não, o Site Recovery não intercepta dados replicados e não tem informações sobre o que está em execução nas máquinas virtuais ou nos servidores físicos.
Os dados de replicação são trocados entre hosts locais do Hyper-V, hipervisores VMware ou servidores físicos e o armazenamento do Azure ou seu site secundário. Recuperação de site não tem toointercept nenhuma capacidade esses dados. Apenas os metadados de saudação necessário tooorchestrate replicação e failover é enviado toohello serviço de recuperação de Site.  

Recuperação de site é ISO 27001: 2013, 27018, HIPAA, DPA certificados e está no processo de saudação do SOC2 e FedRAMP JAB avaliações.

### <a name="for-compliance-reasons-even-our-on-premises-metadata-must-remain-within-hello-same-geographic-region-can-site-recovery-help-us"></a>Por motivos de conformidade, até mesmo nossos metadados local devem permanecer no hello mesma região geográfica. O Site Recovery pode nos ajudar?
Sim. Quando você criar um cofre de recuperação de Site em uma região, garantimos que todos os metadados que precisamos tooenable e orquestrar a replicação e failover permanece dentro dessa região 's geográfica limite.

### <a name="does-site-recovery-encrypt-replication"></a>O Site Recovery criptografa a replicação?
Para máquinas virtuais e servidores físicos que estão sendo replicados entre sites locais, há suporte para a criptografia em trânsito. Para máquinas virtuais e servidores físicos replicando tooAzure, ambos os criptografia em trânsito e [criptografia em repouso (no Azure)](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) têm suporte.

## <a name="replication"></a>Replicação

### <a name="can-i-replicate-over-a-site-to-site-vpn-tooazure"></a>Pode replicar em um tooAzure VPN site a site?
O Azure Site Recovery replica dados tooan conta de armazenamento Azure, em um ponto de extremidade público. A replicação não ocorre através de uma VPN site a site. Você pode criar uma VPN site a site, com uma rede virtual do Azure. Isso não interfere na replicação do Site Recovery.

### <a name="can-i-use-expressroute-tooreplicate-virtual-machines-tooazure"></a>É possível usar ExpressRoute tooreplicate máquinas virtuais tooAzure?
Sim, a rota expressa pode ser usado tooreplicate tooAzure de máquinas virtuais. Recuperação de Site do Azure replica dados tooan conta de armazenamento do Azure em um ponto de extremidade público. Você precisa tooset backup [emparelhamento público](../expressroute/expressroute-circuit-peerings.md#public-peering) toouse rota expressa para replicação de recuperação de Site. Após Olá failover máquinas virtuais têm sido tooan rede virtual do Azure você pode acessá-los usando Olá [emparelhamento privado](../expressroute/expressroute-circuit-peerings.md#private-peering) instalação com hello rede virtual do Azure.

### <a name="are-there-any-prerequisites-for-replicating-virtual-machines-tooazure"></a>Há todos os pré-requisitos para replicar máquinas virtuais tooAzure?
Máquinas virtuais que você deseja tooreplicate tooAzure devem ser compatíveis com [requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

Sua conta de usuário do Azure precisa toohave determinados [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable de replicação de um novo tooAzure de máquina virtual.

### <a name="can-i-replicate-hyper-v-generation-2-virtual-machines-tooazure"></a>Posso replicar tooAzure de máquinas virtuais de 2ª geração Hyper-V?
Sim. Recuperação de site converte de geração 2 toogeneration 1 durante o failover. Em failback Olá é convertido toogeneration back 2. [Leia mais](http://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/).

### <a name="if-i-replicate-tooazure-how-do-i-pay-for-azure-vms"></a>Se posso replicar tooAzure como pagar o para máquinas virtuais do Azure?
Durante a replicação normal, dados são replicados de armazenamento do Azure com redundância toogeo e não é necessário toopay quaisquer encargos de máquina virtual IaaS do Azure, fornecendo uma vantagem significativa. Quando você executa um tooAzure de failover, recuperação de Site automaticamente cria máquinas virtuais IaaS do Azure e, depois que você será cobrado por recursos de computação de saudação que consomem no Azure.

### <a name="can-i-automate-site-recovery-scenarios-with-an-sdk"></a>Posso automatizar os cenários do Site Recovery com um SDK?
Sim. Você pode automatizar fluxos de trabalho de recuperação de Site usando Olá API Rest, o PowerShell ou saudação do SDK do Azure. Cenários com suporte no momento para implantar a Recuperação de Site usando o PowerShell:

* [Replicar máquinas virtuais do Hyper-V em nuvens de VMMs tooAzure Gerenciador de recursos do PowerShell](site-recovery-vmm-to-azure-powershell-resource-manager.md)
* [Replicar máquinas virtuais do Hyper-V sem VMM tooAzure Gerenciador de recursos do PowerShell](site-recovery-deploy-with-powershell-resource-manager.md)

### <a name="if-i-replicate-tooazure-what-kind-of-storage-account-do-i-need"></a>Se eu replicar tooAzure que tipo de conta de armazenamento é necessário?
* **Portal clássico do Azure**: se você estiver implantando a recuperação de Site em Olá portal clássico do Azure, será necessário um [conta de armazenamento com redundância geográfica standard](../storage/common/storage-redundancy.md#geo-redundant-storage). Atualmente não há suporte para o armazenamento Premium. Olá conta deve ser no hello mesma região Olá Cofre de recuperação de Site.
* **Portal do Azure**: se você estiver implantando a recuperação de Site em Olá portal do Azure, você precisará de uma conta de armazenamento LRS ou GRS. É recomendável GRS para que dados sejam resilientes, se ocorrer uma interrupção regional, ou se a região primária Olá não pode ser recuperado. Olá conta deve ser no hello Cofre de serviços de recuperação com a mesma região hello. Agora há suporte para armazenamento Premium para VM do VMware, VM Hyper-V e replicação de servidor físico, quando você implanta a recuperação de Site no hello portal do Azure.

### <a name="how-often-can-i-replicate-data"></a>Com que frequência posso replicar dados?
* **Hyper-V:** as VMs Hyper-V podem ser replicadas a cada 30 segundos (exceto para armazenamento Premium), cinco minutos ou 15 minutos. Se você tiver definido a replicação da rede SAN, ela será simultânea.
* **VMware e servidores físicos:** não é relevante estabelecer uma frequência de replicação para eles. A replicação é contínua.

### <a name="can-i-extend-replication-from-existing-recovery-site-tooanother-tertiary-site"></a>Posso estender a replicação do site tooanother terciário local de recuperação existente?
Esse tipo de replicação estendida ou encadeada não tem suporte. Solicite esse recurso no [fórum de comentários](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6097959-support-for-exisiting-extended-replication).

### <a name="can-i-do-an-offline-replication-hello-first-time-i-replicate-tooazure"></a>É possível fazer uma saudação replicação offline primeira vez que posso replicar tooAzure?
Não há suporte para isso. Solicitar esse recurso no hello [Fórum de comentários](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6227386-support-for-offline-replication-data-transfer-from).

### <a name="can-i-exclude-specific-disks-from-replication"></a>Posso excluir discos específicos da replicação?
Há suporte para isso quando você estiver [replicando máquinas virtuais do VMware e VMs Hyper-V](site-recovery-exclude-disk.md) tooAzure, usando Olá portal do Azure.

### <a name="can-i-replicate-virtual-machines-with-dynamic-disks"></a>Posso replicar máquinas virtuais com discos dinâmicos?
Os discos dinâmicos têm suporte na replicação de máquinas virtuais Hyper-V. Eles também têm suporte quando a replicação de máquinas virtuais do VMware e tooAzure máquinas físicas. disco do sistema operacional Olá deve ser um disco básico.

### <a name="can-i-add-a-new-machine-tooan-existing-replication-group"></a>Adicionar um nova máquina tooan grupo de replicação existente?
Há suporte para a adição de novos grupos de replicação tooexisting máquinas. toodo, então, selecione o grupo de replicação de saudação (de 'Itens replicadas' folha) e o menu de contexto/selecionar clique com botão direito no grupo de replicação de saudação e selecione opção apropriada da saudação.

![Adicionar grupo tooreplication](./media/site-recovery-faq/add-server-replication-group.png)

### <a name="can-i-throttle-bandwidth-allotted-for-hyper-v-replication-traffic"></a>Posso restringir a largura de banda alocada para o tráfego de replicação do Hyper-V?
Sim. Você pode ler mais sobre a limitação de largura de banda em artigos sobre implantação hello:

* [Planejamento de capacidade para a replicação de VMs VMware e servidores físicos](site-recovery-plan-capacity-vmware.md)
* [Planejamento de capacidade para a replicação de VMs Hyper-V em nuvens VMM](site-recovery-vmm-to-azure.md#capacity-planning)
* [Planejamento de capacidade para a replicação de VMs Hyper-V sem VMM](site-recovery-hyper-v-site-to-azure.md)

## <a name="failover"></a>Failover
### <a name="if-im-failing-over-tooazure-how-do-i-access-hello-azure-virtual-machines-after-failover"></a>Se eu estou failover tooAzure, como acesso hello Azure máquinas virtuais após o failover?
Você pode acessar Olá VMs do Azure em uma conexão segura de Internet, através de uma VPN site a site ou em rota expressa do Azure. Você precisará tooprepare um número de itens na ordem tooconnect. [Saiba mais](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)


### <a name="if-i-fail-over-tooazure-how-does-azure-make-sure-my-data-is-resilient"></a>Se eu fizer failover tooAzure como Azure Certifique-se meus dados seja resilientes?
O Azure foi desenvolvido para resiliência. Recuperação de site já foi criada para failover tooa datacenter secundário do Azure, conforme Olá surge de SLA do Azure se precisar de saudação. Se isso acontecer, verificamos se seus metadados e cofres permaneçam em hello mesma região geográfica que você escolheu para o cofre.  

### <a name="if-im-replicating-between-two-datacenters-what-happens-if-my-primary-datacenter-experiences-an-unexpected-outage"></a>Ao replicar entre dois datacenters, o que acontece se meu datacenter primário sofrer uma interrupção inesperada?
Você pode disparar um failover não planejado do site secundário hello. Recuperação de site não precisa de conectividade de site primário de saudação tooperform Olá failover.

### <a name="is-failover-automatic"></a>O failover é automático?
O failover não é automático. Iniciar failovers com um único clique no portal de hello, ou você pode usar [PowerShell de recuperação de Site](/powershell/module/azurerm.siterecovery) tootrigger um failover. Failback é uma ação simple no portal de recuperação de Site hello.

tooautomate que você pode usar toodetect Orchestrator ou no Operations Manager uma falha de máquina virtual local e, em seguida, gatilho Olá failover usando Olá SDK.

* [Leia mais](site-recovery-create-recovery-plans.md) sobre planos de recuperação.
* [Saiba mais](site-recovery-failover.md) sobre failover.
* [Saiba mais](site-recovery-failback-azure-to-vmware.md) como realizar failback das VMs VMware e servidores físicos

### <a name="if-my-on-premises-host-is-not-responding-or-crashed-can-i-failover-back-tooa-different-host"></a>Se o host local não está respondendo ou falha, é possível realizar failover de host diferentes tooa back?
Sim, você pode usar o hello local alternativo recuperação toofailback tooa host diferente do Azure. Leia mais sobre as opções de saudação da saudação links a seguir para máquinas virtuais VMware e Hyper-v.

* [Para máquinas virtuais VMware](site-recovery-how-to-failback-azure-to-vmware.md#fail-back-to-the-original-or-alternate-location)
* [Para máquinas virtuais Hyper-V](site-recovery-failback-from-azure-to-hyper-v.md#failback-to-an-alternate-location)

## <a name="service-providers"></a>Provedores de serviço
### <a name="im-a-service-provider-does-site-recovery-work-for-dedicated-and-shared-infrastructure-models"></a>Sou um provedor de serviço. O Site Recovery funciona com modelos de infraestrutura compartilhados e dedicados?
Sim, o Site Recovery dá suporte aos modelos de infraestrutura dedicados e compartilhados.

### <a name="for-a-service-provider-is-hello-identity-of-my-tenant-shared-with-hello-site-recovery-service"></a>Para um provedor de serviço, é a identidade de saudação do meu locatário compartilhado com o serviço de recuperação de Site Olá?
Não. A identidade do locatário permanece anônima. Portal de recuperação de Site do acesso toohello não precisam de seus locatários. Somente Olá serviço provedor administrador interage com o portal hello.

### <a name="will-tenant-application-data-ever-go-tooazure"></a>Dados de aplicativo de locatário nunca ir tooAzure?
Ao replicar entre sites de propriedade do provedor de serviços, dados de aplicativo nunca vai tooAzure. Dados são criptografados em trânsito e replicados diretamente entre os sites de provedor de serviço de saudação.

Se você estiver replicando tooAzure, dados de aplicativo são enviados tooAzure armazenamento mas toohello serviço de recuperação de Site. Os dados são criptografados em trânsito e permanecem criptografados no Azure.

### <a name="will-my-tenants-receive-a-bill-for-any-azure-services"></a>Meus locatários receberão alguma fatura relativa a serviços do Azure?
Não. Relação de cobrança do Azure está diretamente com o provedor de serviços de saudação. Os provedores de serviços são responsáveis por gerar faturas específicas para seus locatários.

### <a name="if-im-replicating-tooazure-do-we-need-toorun-virtual-machines-in-azure-at-all-times"></a>Se eu estou replicando tooAzure, precisamos toorun as máquinas virtuais no Azure sempre?
Não, os dados são replicado tooan conta de armazenamento do Azure em sua assinatura. Quando você executa um failover de teste (análise de DR) ou um failover real, o Site Recovery cria automaticamente máquinas virtuais em sua assinatura.

### <a name="do-you-ensure-tenant-level-isolation-when-i-replicate-tooazure"></a>Garantir o isolamento de nível de locatário quando posso replicar tooAzure?
Sim.

### <a name="what-platforms-do-you-currently-support"></a>A quais plataformas vocês oferecem suporte atualmente?
Damos suporte ao Azure Pack, ao Sistema de Plataforma de Nuvem e a implantações baseadas no System Center (2012 e posterior). [Saiba mais](https://technet.microsoft.com/library/dn850370.aspx) sobre a integração do Azure Pack e da Recuperação de Site.

### <a name="do-you-support-single-azure-pack-and-single-vmm-server-deployments"></a>Você também dá suporte implantações únicas de Azure Pack e servidor VMM?
Sim, você pode replicar tooAzure de máquinas virtuais do Hyper-V, ou entre os sites do provedor de serviço.  Observe que, se você replicar entre sites do provedor de serviços, a integração de runbook do Azure não estará disponível.

## <a name="next-steps"></a>Próximas etapas
* Saudação de leitura [visão geral da recuperação de Site](site-recovery-overview.md)
* Saiba mais sobre a [arquitetura do Site Recovery](site-recovery-components.md)  
