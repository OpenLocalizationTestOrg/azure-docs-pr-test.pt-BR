---
title: "aaaPrerequisites para tooAzure de replicação usando o Azure Site Recovery | Microsoft Docs"
description: "Saiba mais sobre os pré-requisitos de saudação para replicar máquinas virtuais e máquinas físicas tooAzure usando o serviço do Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: jwhit
editor: tysonn
ms.assetid: e24eea6c-50a7-4cd5-aab4-2c5c4d72ee2d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: rajanaki
ms.openlocfilehash: 0e32ab7cd7c65a3f67ffa2f2c15af189c15b6f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
#  <a name="prerequisites-for-replication-from-on-premises-tooazure-by-using-site-recovery"></a>Pré-requisitos para a replicação do local tooAzure usando a recuperação de Site

> [!div class="op_single_selector"]
> * [Replicar do tooAzure do Azure](site-recovery-azure-to-azure-prereq.md)
> * [Replicar do local tooAzure](site-recovery-prereq.md)

O Azure Site Recovery pode ajudá-lo a dar suporte a sua estratégia de recuperação (BCDR) de desastre e continuidade de negócios ao orquestrar a replicação de uma máquina virtual do Azure (VM) de tooanother região do Azure. Recuperação de site também replica datacenter secundário tooa e VMs toohello nuvem (Azure) ou servidores físicos no local. Se ocorrer uma interrupção no local principal, você pode fazer failover tooa local secundário tookeep aplicativos e cargas de trabalho disponíveis. Você pode fazer localização primária tooyour back quando o local principal Olá retorna toonormal operações. Para obter mais informações sobre o Site Recovery, consulte [O que é o Site Recovery?](site-recovery-overview.md).

Neste artigo, vamos resumir os pré-requisitos de saudação para iniciar a replicação de recuperação de Site de um tooAzure de máquina local.

Você pode lançar os comentários na parte inferior de saudação do artigo hello. Você também pode fazer perguntas técnicas no hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="azure-requirements"></a>Requisitos do Azure

**Requisito** | **Detalhes**
--- | ---
**Conta do Azure** | Uma [conta do Microsoft Azure](http://azure.microsoft.com/). Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
**Serviço do Site Recovery** | Para obter mais informações sobre preços para Olá serviço Azure Site Recovery, consulte [preços de recuperação de Site](https://azure.microsoft.com/pricing/details/site-recovery/). |
**Armazenamento do Azure** | É necessário um toostore replicado dados da conta de armazenamento do Azure. conta de armazenamento Olá deve estar no hello Cofre de serviços de recuperação do Azure com a mesma região hello. VMs do Azure são criadas quando ocorre um failover.<br/><br/> Dependendo do modelo de recurso Olá desejar toouse para failover de VM do Azure, você pode configurar uma conta usando Olá [modelo de implantação do Azure Resource Manager](../storage/common/storage-create-storage-account.md) ou hello [modelo de implantação clássico](../storage/common/storage-create-storage-account.md).<br/><br/>Você pode usar [armazenamento com redundância geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) ou armazenamento com redundância local. Recomendamos usar armazenamento com redundância geográfica. Com o armazenamento com redundância geográfica, dados seja resilientes se ocorrer uma interrupção regional, ou se a região primária Olá não pode ser recuperado.<br/><br/> Você pode usar uma conta de armazenamento padrão do Azure ou pode usar o Armazenamento Premium do Azure. O [Armazenamento Premium](https://docs.microsoft.com/azure/storage/storage-premium-storage) normalmente é usado para VMs que precisam de alto desempenho de E/S e baixa latência consistentemente. Com o Armazenamento Premium, uma VM pode hospedar cargas de trabalho com E/S intensivo. Se você usar o Armazenamento Premium para os dados replicados, também precisará de uma conta de Armazenamento Standard. Uma conta de armazenamento standard armazena os logs de replicação que capturam dados de local tooon alterações contínuas.<br/><br/>
**Limitações de armazenamento** | Você não pode mover contas de armazenamento que você usa no grupo de recursos diferente do Site Recovery tooa ou mover o uso de tooor com outra assinatura.<br/><br/> Atualmente, replicar toopremium contas de armazenamento na Índia Central e Sul da Índia não está disponível.
**Rede do Azure** | Você precisa de uma rede do Azure, conecte-se de VMs do Azure toowhich após o failover. Olá rede do Azure deve estar no hello Cofre de serviços de recuperação com a mesma região hello.<br/><br/> Em Olá portal do Azure, você pode criar uma rede do Azure usando Olá [modelo de implantação do Gerenciador de recursos](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) ou hello [modelo de implantação clássico](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).<br/><br/> Se você replicar do System Center Virtual Machine Manager (VMM) tooAzure, você deve definir o mapeamento de rede entre redes de VM do VMM e redes do Azure. Isso garante que as VMs do Azure se conectar a redes tooappropriate após o failover.
**Limitações de rede** | Você não pode mover contas de rede que você usa no grupo de recursos diferente do Site Recovery tooa ou mover o uso de tooor com outra assinatura.
**Mapeamento de rede** | Se você replicar VMs do Microsoft Hyper-V nas nuvens do VMM, será necessário definir o mapeamento de rede. Isso garante que as VMs do Azure conectar redes tooappropriate quando eles são criados após o failover.

> [!NOTE]
> Olá seções a seguir descrevem os pré-requisitos de saudação para vários componentes do ambiente de saudação do cliente. Para obter mais informações sobre o suporte para configurações específicas, consulte Olá [matriz de suporte](site-recovery-support-matrix.md).
>

## <a name="disaster-recovery-of-vmware-vms-or-physical-windows-or-linux-servers-tooazure"></a>Recuperação de desastres de máquinas virtuais do VMware ou tooAzure físico de servidores Windows ou Linux
Olá componentes a seguir é necessário para recuperação de desastres de máquinas virtuais do VMware ou servidores físicos do Windows ou Linux. Além disso, esses são toohello aqueles descrito em [requisitos do Azure](#azure-requirements).


### <a name="configuration-server-or-additional-process-server"></a>Servidor de configuração ou servidor em processo adicional

Configure um computador local como uma comunicação de tooorchestrate de servidor de configuração de saudação entre Olá no site local e o Azure. máquina local, Olá também gerencia a replicação de dados. <br/></br>

*   **Pré-requisitos de host do VMware vCenter ou vSphere**

    | **Componente** | **Requisitos** |
    | --- | --- |
    | **vSphere** | Você precisa de um ou mais hipervisores do VMware vSphere.<br/><br/>Hipervisores devem estar executando a versão do vSphere 5.1, 5.5 ou 6.0 com hello atualizações mais recentes.<br/><br/>É recomendável que vSphere hosts e servidores vCenter ser em Olá mesmo de rede como servidor de processo hello. A menos que você configurou um servidor de processo dedicado, essa é a rede de saudação onde se encontra o servidor de configuração hello. |
    | **vCenter** | É recomendável que você implante um toomanage do VMware vCenter server seus hosts vSphere. Ele deve estar executando o vCenter versão 6.0 ou 5.5, com atualizações mais recentes de saudação.<br/><br/>**Limitação**: o Site Recovery não dá suporte à replicação entre instâncias do vCenter vMotion. Também não há suporte para DRS e vMotion de Armazenamento em uma VM de destino mestre após uma operação de nova proteção.||

* **Pré-requisitos de computadores replicados**

    | **Componente** | **Requisitos** |
    | --- | --- |
    | **Computadores locais** (VMs VMware) | As VMs replicadas devem ter as ferramentas de VMware instaladas e em execução.<br/><br/> As VMs devem atender aos [Pré-requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) para a criação de uma VM do Azure.<br/><br/>A capacidade do disco em cada computador protegido não pode passar de 1.023 GB. <br/><br/>Um mínimo 2 GB de espaço disponível na unidade de instalação Olá é necessária para a instalação do componente.<br/><br/>Se você quiser tooenable consistência de várias VMs, porta 20004 deve ser aberta no firewall local da VM hello.<br/><br/>Os nomes dos computadores devem conter entre 1 e 63 caracteres (você pode usar letras, números e hifens). nome da saudação deve começar com uma letra ou número e terminar com uma letra ou número. <br/><br/>Depois de habilitar a replicação para uma máquina, você pode modificar Olá nomes do Azure.<br/><br/> |
    | **Computadores Windows** (físicos ou VMware) | Olá máquina deve estar executando um dos seguintes Olá suportados sistemas operacionais de 64 bits: <br/>– Windows Server 2012 R2<br/>– Windows Server 2012<br/>– Windows Server 2008 R2 com SP1 ou uma versão posterior<br/><br/> Olá sistema operacional instalado no disco de Olá sistema operacional da unidade C. deve ser um disco básico do Windows e não dinâmicos. disco de dados Olá pode ser dinâmico.<br/><br/>|
    | **Computadores com Linux** (físicos ou VMware) | Olá máquina deve estar executando um dos seguintes Olá suportados sistemas operacionais de 64 bits: <br/>– Red Hat Enterprise Linux 7.2, 7.1, 6.8 ou 6.7<br/>– Centos 7.2, 7.1, 7.0, 6.8, 6.7, 6.6 ou 6.5<br/>– Servidor Ubuntu 14.04 LTS (para ver uma lista das versões do kernel para Ubuntu com suporte, consulte [sistemas operacionais com suporte](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions))<br/>-Núcleo do oracle compatível com o Enterprise Linux 6.5 ou 6.4, executando o hello Red Hat ou inviolável Enterprise Kernel versão 3 (UEK3)<br/>– SUSE Linux Enterprise Server 11 SP4 ou SUSE Linux Enterprise Server 11 SP3<br/><br/>Seus arquivos de /etc/hosts em computadores protegidos devem ter entradas que mapeiam Olá host local nome tooIP endereços associados a todos os adaptadores de rede.<br/><br/>Após o failover, se você quiser tooconnect tooan VM do Azure que está executando o Linux usando um cliente do Secure Shell (SSH), verifique se serviço SSH Olá máquina Olá protegido está definido toostart automaticamente na inicialização do sistema. Certifique-se também que as regras de firewall permitem uma máquina de toohello protegido conexão SSH.<br/><br/>nome do host Hello, pontos de montagem, nomes de dispositivos e caminhos de sistema do Linux e nomes de arquivo (por exemplo, /etc/ e em /usr.) devem estar em inglês apenas.<br/><br/>Olá diretórios a seguir (se configurado como partições separadas ou sistemas de arquivos) devem estar no hello mesmo disco (disco Olá SO) no servidor de origem hello:<br/>- / (root)<br/>- /boot<br/>- /usr<br/>- /usr/local<br/>- /var<br/>- /etc<br/><br/>No momento, não há suporte para os recursos de XFS v5, como soma de verificação de metadados, pelo Site Recovery em sistemas de arquivos XFS. Verifique se seus sistemas de arquivos XFS não estão usando recursos da v5. Você pode usar super-bloco do hello xfs_info utilitário toocheck Olá XFS para partição hello. Se **ftype** está definido muito**1**, XFS v5 recursos estão sendo usados.<br/><br/>Nos servidores do Red Hat Enterprise Linux 7 e CentOS 7, o utilitário de lsof Olá deve estar instalado e disponível.<br/><br/>


## <a name="disaster-recovery-of-hyper-v-vms-tooazure-no-vmm"></a>Recuperação de desastres do tooAzure de VMs Hyper-V (sem VMM)

Olá componentes a seguir é necessário para recuperação de desastres de máquinas virtuais do Hyper-V nas nuvens do VMM. Além disso, esses são toohello aqueles descrito em [requisitos do Azure](#azure-requirements).

| **Pré-requisito** | **Detalhes** |
| --- | --- |
| **Host Hyper-V** |Um ou mais servidores de local devem estar executando o Windows Server 2012 R2 com atualizações mais recentes do hello e função do Hyper-V Olá habilitado ou Microsoft Hyper-V Server 2012 R2.<br/><br/>Servidores Hyper-V devem ter uma ou mais VMs.<br/><br/>Servidores Hyper-V devem ser toohello conectado à Internet, diretamente ou por meio de um proxy.<br/><br/>Servidores Hyper-V devem ter correções Olá descritas no artigo da Base de dados de Conhecimento Olá [2961977](https://support.microsoft.com/kb/2961977) instalado.
|**Provedor e agente**| Durante a implantação da recuperação de Site, você instalar o provedor do Azure Site Recovery hello. instalação do provedor Olá também instala o agente de serviços de recuperação do Azure de saudação em cada servidor Hyper-V que está executando máquinas virtuais que você deseja tooprotect. <br/><br/>Todos os servidores Hyper-V em uma recuperação de Site deve ter cofre Olá mesmas versões do provedor de saudação e agente de saudação.<br/><br/>provedor de saudação precisa tooconnect tooSite recuperação sobre Olá da Internet. O tráfego pode ser enviado diretamente ou por meio de um proxy. Não há suporte para o proxy com base em HTTPS. servidor de proxy Olá deve permitir o acesso toohello seguintes URLs:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/>Se você tiver regras de firewall baseado em endereço IP no servidor de saudação, certifique-se de regras de saudação permitem comunicação tooAzure.<br/><br/> Permitir Olá [intervalos IP do datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e HTTPS (porta 443).<br/><br/> Permitir que os intervalos de endereços IP para Olá região do Azure de sua assinatura e Olá Oeste dos EUA (usado para gerenciamento de identidades e controle de acesso).


## <a name="disaster-recovery-of-hyper-v-vms-in-vmm-clouds-tooazure"></a>Recuperação de desastres de máquinas virtuais do Hyper-V no VMM nuvens tooAzure

Olá componentes a seguir é necessário para recuperação de desastres de máquinas virtuais do Hyper-V nas nuvens do VMM. Além disso, esses são toohello aqueles descrito em [requisitos do Azure](#azure-requirements).

| **Pré-requisito** | **Detalhes** |
| --- | --- |
| **Virtual Machine Manager** |Você deverá ter um ou mais servidores VMM em execução no System Center 2012 R2 ou uma versão posterior. Cada servidor VMM deve ter uma ou mais nuvens configuradas. <br/><br/>Uma nuvem deve ter:<br/>- Um ou mais grupos de hosts do VMM.<br/>- Um ou mais servidores host Hyper-V ou clusters em cada grupo de hosts.<br/><br/>Para obter mais informações sobre como configurar nuvens do VMM, consulte [como toocreate uma nuvem no Virtual Machine Manager 2012](http://social.technet.microsoft.com/wiki/contents/articles/2729.how-to-create-a-cloud-in-vmm-2012.aspx). |
| **Hyper-V** |Servidores de host Hyper-V devem estar executando pelo menos Windows Server 2012 R2 com a função hello Hyper-V habilitada ou Microsoft Hyper-V Server 2012 R2. atualizações mais recentes do Hello devem ser instaladas.<br/><br/> Um servidor Hyper-V deve ter uma ou mais VMs.<br/><br/> Um servidor de host do Hyper-V ou cluster que inclui máquinas virtuais que você deseja tooreplicate deve ser gerenciado em uma nuvem do VMM.<br/><br/>Servidores Hyper-V devem ser toohello conectado à Internet, diretamente ou por meio de um proxy.<br/><br/>Servidores Hyper-V devem ter correções Olá descritas no artigo da Base de dados de Conhecimento Olá [2961977](https://support.microsoft.com/kb/2961977) instalado.<br/><br/>Servidores de host Hyper-V precisam de acesso à Internet para tooAzure de replicação de dados. |
| **Provedor e agente** |Durante a implantação do Azure Site Recovery, instale o provedor do Azure Site Recovery no servidor do VMM hello. Instale o Agente dos Serviços de Recuperação em hosts do Hyper-V. agente e provedor Olá necessário tooconnect tooAzure diretamente pela Olá da Internet ou por meio de um proxy. Não há suporte para um proxy com base em HTTPS. servidor de proxy Olá no servidor do VMM hello e hosts Hyper-V deve permitir acesso a: <br/><br/>[!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)] <br/><br/>Se você tiver regras de firewall baseado em endereço IP no servidor do VMM hello, certifique-se de regras de saudação permitem comunicação tooAzure.<br/><br/> Permitir Olá [intervalos IP do datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) e HTTPS (porta 443).<br/><br/>Permitir que os intervalos de endereços IP para Olá região do Azure para sua assinatura e Olá Oeste dos EUA (usado para gerenciamento de identidades e controle de acesso).<br/><br/> |

### <a name="replicated-machine-prerequisites"></a>Pré-requisitos de computadores replicados

| **Componente** | **Detalhes** |
| --- | --- |
| **VMs protegidas** | O Site Recovery é compatível com todos os sistemas operacionais que são aceitos pelo [Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx).<br/><br/>Máquinas virtuais devem atender aos Olá [pré-requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) para a criação de uma VM do Azure. Os nomes dos computadores devem conter entre 1 e 63 caracteres (você pode usar letras, números e hifens). nome da saudação deve começar com uma letra ou número e terminar com uma letra ou número. <br/><br/>Você pode modificar o nome da VM Olá depois de habilitar a replicação para Olá VM. <br/><br/> A capacidade do disco para cada computador protegido não pode passar de 1.023 GB. Uma VM pode ter os discos too16 (até too16 TB).<br/><br/>


## <a name="disaster-recovery-of-hyper-v-vms-in-vmm-clouds-tooa-customer-owned-site"></a>Site de propriedade tooa de nuvens de recuperação de desastres de máquinas virtuais do Hyper-V no VMM

Olá componentes a seguir é necessário para recuperação de desastres de máquinas virtuais do Hyper-V no site do VMM de nuvens tooa propriedade. Além disso, esses são toohello aqueles descrito em [requisitos do Azure](#azure-requirements).

| **Componente** | **Detalhes** |
| --- | --- |
| **Virtual Machine Manager** |  É recomendável que você implante um servidor do VMM no site primário hello e site secundário hello.<br/><br/> Você pode [replicar entre nuvens em um único servidor VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment). tooreplicate entre nuvens em um único servidor do VMM, você precisa de pelo menos duas nuvens configuradas no servidor do VMM hello.<br/><br/> Servidores do VMM devem estar executando pelo menos System Center 2012 SP1, as atualizações mais recentes de saudação.<br/><br/> Cada servidor VMM deve ter uma ou mais nuvens. Todas as nuvens devem ter Olá que conjunto de perfis de capacidade do Hyper-V. <br/><br/>As nuvens devem ter um ou mais grupos de hosts do VMM. Para obter mais informações sobre como configurar nuvens do VMM, consulte [Preparar para a implantação do Azure Site Recovery](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric). |
| **Hyper-V** | Servidores Hyper-V devem estar executando pelo menos o Windows Server 2012 com a função hello Hyper-V habilitada e ter Olá as últimas atualizações instaladas.<br/><br/> Um servidor Hyper-V deve ter uma ou mais VMs.<br/><br/>  Servidores de host Hyper-V devem estar localizados em grupos de host em nuvens do VMM Olá primários e secundários.<br/><br/> Se você executar o Hyper-V em um cluster no Windows Server 2012 R2, é recomendável que você instale a atualização Olá descrita no artigo da Base de dados de Conhecimento [2961977](https://support.microsoft.com/kb/2961977).<br/><br/> Se você executar o Hyper-V em um cluster no Windows Server 2012 e tiver um cluster baseado em endereço IP estático, o agente de cluster não será criado automaticamente. Você deve configurar manualmente o agente do cluster hello. Para obter mais informações sobre o agente de cluster hello, consulte [configurar função de agente de réplica Olá para replicação de cluster para cluster](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx). |
| **Provedor** | Durante a implantação da recuperação de Site, instale o provedor do Azure Site Recovery Olá nos servidores do VMM. provedor Olá se comunica com a recuperação de Site sobre a replicação de tooorchestrate HTTPS (porta 443). Replicação de dados ocorre entre Olá servidores primários e secundários Hyper-V pela Olá LAN ou através de uma conexão VPN.<br/><br/> provedor de saudação que está em execução no servidor do VMM Olá precisa acessar toohello seguintes URLs:<br/><br/>[!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)] <br/><br/>provedor de recuperação de Site Olá deve permitir a comunicação de firewall de saudação do VMM servidores toohello [intervalos IP do datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e permitir o protocolo HTTPS (porta 443) de saudação. |


## <a name="url-access"></a>Acesso à URL
Essas URLs devem estar disponíveis no VMware, no VMM e nos servidores host do Hyper-V:

|**URL** | **O VMM tooVMM** | **O VMM tooAzure** | **TooAzure Hyper-V** | **VMware tooAzure** |
|--- | --- | --- | --- | --- |
|``*.accesscontrol.windows.net`` | PERMITIR | Permitir | Permitir | Permitir |
|``*.backup.windowsazure.com`` | Não requerido | Permitir | Permitir | Permitir |
|``*.hypervrecoverymanager.windowsazure.com`` | Permitir | Permitir | Permitir | Permitir |
|``*.store.core.windows.net`` | Permitir | Permitir | Permitir | Permitir |
|``*.blob.core.windows.net`` | Não requerido | Permitir | Permitir | Permitir |
|``https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi`` | Não requerido | Não requerido | Não requerido | Permitir download do SQL |
|``time.windows.com`` | PERMITIR | Permitir | Permitir | Permitir|
|``time.nist.gov`` | Permitir | Permitir | Permitir | PERMITIR |
