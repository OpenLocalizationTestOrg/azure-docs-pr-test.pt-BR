---
title: "máquinas virtuais do VMware aaaReplicate e tooAzure de servidores físicos no portal clássico de hello | Microsoft Docs"
description: "Este artigo descreve como a replicação toodeploy Azure Site Recovery tooorchestrate, failover e recuperação de local máquinas virtuais VMware e tooAzure de servidores físicos do Windows/Linux."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: a9022c1f-43c1-4d38-841f-52540025fb46
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-vmware-to-azure
ms.openlocfilehash: f85e4139ad45552ce963072e14d71d279bb7dac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-tooazure-with-azure-site-recovery"></a>Replicar máquinas virtuais VMware e servidores físicos tooAzure com o Azure Site Recovery
> [!div class="op_single_selector"]
> * [Olá portal do Azure](site-recovery-vmware-to-azure.md)
> * [portal clássico Olá](site-recovery-vmware-to-azure-classic.md)
> * [portal clássico do Hello (legados)](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

Olá serviço Azure Site Recovery contribui com a estratégia de recuperação (BCDR) de desastre e continuidade de negócios tooyour ao orquestrar a replicação, failover e recuperação de máquinas virtuais e servidores físicos. Computadores podem ser replicado tooAzure ou data center do tooa no local secundário. Para ter uma breve visão geral, consulte [O que é Azure Site Recovery?](site-recovery-overview.md)

## <a name="overview"></a>Visão geral
Este artigo descreve como:

* **Replicar tooAzure de máquinas virtuais VMware**: replicação de toocoordinate implantar recuperação de Site, failover e recuperação de armazenamento de tooAzure de máquinas virtuais de VMware no local.
* **Replicar os servidores físicos tooAzure**: replicação de toocoordinate de implantar o Azure Site Recovery, failover e recuperação de físicos locais do Windows e Linux tooAzure servidores.

> [!NOTE]
> Este artigo descreve como tooreplicate tooAzure. Se você quiser tooreplicate VMs VMware ou Windows/Linux servidores físicos tooa datacenter secundário, consulte [tooVMware VMware de recuperação de Site](site-recovery-vmware-to-vmware.md).
>
>

Postar comentários e perguntas na parte inferior da saudação deste artigo ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="enhanced-deployment"></a>Implantação avançada
Este artigo inclui instruções para uma implantação avançada em Olá portal clássico do Azure. Recomendamos que você use esta versão para todas as novas implantações. Se você já implantou por usando Olá versão herdado anterior, é recomendável que você migre toohello nova versão. Para obter mais informações sobre migração, consulte [VMware de recuperação de Site tooAzure clássico herdado](site-recovery-vmware-to-azure-classic-legacy.md#migrate-to-the-enhanced-deployment).

implantação de saudação avançada é uma atualização importante. Aqui está um resumo das melhorias de saudação fizemos:

* **Nenhuma infraestrutura de máquinas virtuais no Azure**: replicam os dados diretamente tooan conta de armazenamento do Azure. Além disso, há tooset sem necessidade de qualquer infra-estrutura de VMs (como o servidor de configuração ou o servidor de destino mestre) para replicação e failover como era necessário na implantação herdado hello.  
* **Instalação unificada**: uma única instalação permite uma configuração simples e escalabilidade para os componentes locais.
* **Implantação segura**: todo o tráfego é criptografado, e as comunicações de gerenciamento da replicação são enviadas por HTTPS 443.
* **Pontos de recuperação**: suporte para falhas e pontos de recuperação consistentes com aplicativos para ambientes do Windows e Linux, e suporte para configurações consistentes com VM única ou várias VMs.
* **Failover de teste**: suporte para tooAzure de failover de teste sem interrupção sem afetar a produção ou pausa a replicação.
* **Failover não planejado**: suporte para failover não planejado tooAzure com uma opção avançada tooautomatically desligar VMs antes do failover.
* **Failback**: failback integrado que replica somente as alterações delta fazer toohello site local.
* **vSphere 6.0**: suporte limitado para as implantações do VMware Vsphere 6.0.

## <a name="how-does-site-recovery-help-protect-virtual-machines-and-physical-servers"></a>Como a Recuperação de Site ajuda a proteger servidores físicos e máquinas virtuais?
* Os administradores de VMware podem configurar tooprotect garantias fora do site do Azure de cargas de trabalho de negócios e aplicativos executados em máquinas virtuais VMware. Os gerentes do servidor podem replicar tooAzure de servidores Windows e Linux no local físico.
* console do Azure Site Recovery Olá fornece um único local para instalação simple e gerenciamento de replicação, failover e processos de recuperação.
* Se você replicar máquinas virtuais VMware que são gerenciadas por um servidor vCenter, a Recuperação de Site poderá descobrir essas VMs automaticamente. Se os computadores estiverem em um host de ESXi, recuperação de Site descobre máquinas virtuais no host de saudação.
* Se você executar failovers fácil de seu tooAzure de infraestrutura local, você pode não fazer (Restaurar) dos servidores VM do Azure tooVMware no Olá no site local.
* Você pode configurar planos de recuperação que agrupem cargas de trabalho de aplicativos que estão organizadas em camadas em vários computadores. Se você fizer failover esses planos, recuperação de Site fornece consistência de várias VMs para que as máquinas em execução Olá às cargas de trabalho podem ser recuperados juntos tooa ponto de dados consistente.

## <a name="supported-operating-systems"></a>Sistemas operacionais com suporte
### <a name="windows-64-bit-only"></a>Windows (somente 64 bits)
* Windows Server 2008 R2 SP1+
* Windows Server 2012
* Windows Server 2012 R2

### <a name="linux-64-bit-only"></a>Linux (somente 64 bits)
* Red Hat Enterprise Linux 6.7, 7.1, e 7.2
* CentOS 6.5, 6.6, 6.7, 7.0, 7.1 e 7.2
* Kernel compatível do Oracle Enterprise Linux 6.4 e 6.5 executando qualquer Olá Red Hat ou inviolável Enterprise Kernel versão 3 (UEK3)
* SUSE Linux Enterprise Server 11 SP3

## <a name="scenario-architecture"></a>Arquitetura de cenário
Componentes do cenário:

* **Um servidor de gerenciamento local**: servidor de gerenciamento de saudação executar componentes do Site Recovery:
  * **Servidor de configuração**: coordena a comunicação e gerencia os processos de replicação e recuperação de dados.
  * **Servidor de processo**: atua como um gateway de replicação. Ele recebe dados de máquinas de origem protegido; otimiza o cache, compactação e criptografia; e o armazenamento de tooAzure de dados de replicação envia. Ele também lida com a instalação por push de máquinas de tooprotected do serviço de mobilidade e executa a descoberta automática de máquinas virtuais do VMware.
  * **Servidor de destino mestre**: lida com os dados de replicação durante o failback do Azure.
    Você também pode implantar um servidor de gerenciamento que atua como um tooscale de servidor de processo em sua implantação.
* **Olá serviço de mobilidade**: esse componente é implantado em cada computador (VM VMware ou servidor físico) que você deseja tooreplicate tooAzure. Ele captura gravações de dados na máquina de saudação e encaminha-servidor de processo toohello.
* **Azure**: não é necessário toocreate quaisquer máquinas virtuais do Azure toohandle replicação e failover. Olá serviço de recuperação de Site lida com gerenciamento de dados e replicam os dados diretamente tooAzure armazenamento. Replicado VMs do Azure são giradas automaticamente backup somente quando ocorre failover tooAzure. No entanto, se você quiser toofail do toohello do Azure no site local, você precisará tooset backup tooact uma VM do Azure como um servidor de processo.

saudação (criado pelo Henry Robalino) do gráfico a seguir mostra como esses componentes interagem:

![Arquitetura de componente](./media/site-recovery-vmware-to-azure/v2a-architecture-henry.png)

## <a name="capacity-planning"></a>Planejamento da capacidade
Quando você estiver planejando a capacidade, aqui está o que você precisa toothink sobre:

* **ambiente de origem Olá**: planejamento ou hello VMware infraestrutura e origem máquina requisitos de capacidade.
* **servidor de gerenciamento Olá**: planejar a saudação de servidores de gerenciamento que executar componentes do Site Recovery no local.
* **Largura de banda de rede de origem tootarget**: planejamento de largura de banda de rede necessária para a replicação entre origem hello e o Azure.

### <a name="source-environment-considerations"></a>Considerações sobre o ambiente de origem
* **Taxa de alteração diária máxima**: um computador protegido pode usar apenas um servidor de processo. Um servidor de processo único pode lidar com backup too2 TB de dados de alteração por dia. Assim, a 2 TB é máxima de dados diário Olá alterar taxa em que há suporte para um computador protegido.
* **Taxa de transferência máxima**: um computador replicado pode pertencer tooone conta de armazenamento do Azure. Uma conta de armazenamento padrão pode lidar com um máximo de 20.000 solicitações por segundo, e é recomendável que você mantenha o número de saudação de IOPS em uma too20 da máquina de origem, 000. Por exemplo, se você tiver uma máquina de origem com 5 discos, e cada disco gera 120 IOPS (tamanho de 8 KB) na fonte de hello, ele será em hello Azure por limite de IOPS de disco de 500. Olá número de contas de armazenamento necessário = total fonte IOPs/20, 000.

### <a name="management-server-considerations"></a>Considerações sobre o servidor de gerenciamento
servidor de gerenciamento Olá executa os componentes de recuperação de Site que lidam com otimização de dados, replicação e gerenciamento. Ele deve ser capacidade taxa de alteração diária toohandle capaz de saudação em todas as cargas de trabalho em execução em computadores protegidos e tem toocontinuously de largura de banda suficiente replicar armazenamento tooAzure de dados. Especificamente:

* servidor de processo Olá recebe dados de replicação de computadores protegidos e otimiza-lo com o cache, a compactação e criptografia antes de enviá-la tooAzure. servidor de gerenciamento de saudação deve ter tooperform de recursos suficientes, essas tarefas.
* servidor de processo Olá usa cache baseadas em disco. Recomendamos que um disco de cache separado de 600 GB ou mais alterações de dados de toohandle armazenadas no evento de saudação do afunilamento de rede ou interrupção. Durante a implantação, você pode configurar o cache de saudação em qualquer unidade que tenha pelo menos 5 GB de armazenamento disponível, mas 600 GB é recomendação mínimo hello.
* Como uma prática recomendada, é recomendável que esse servidor de gerenciamento hello está localizado em Olá mesma rede e o segmento de LAN Olá máquinas que você deseja tooprotect. Ela pode estar localizada em uma rede diferente, mas as máquinas que você deseja tooprotect devem ter L3 tooit de visibilidade de rede.

Recomendações de tamanho para o servidor de gerenciamento Olá estão resumidas na Olá a tabela a seguir:

| **CPU do servidor de gerenciamento** | **Memória** | **Tamanho do disco de cache** | **Taxa de alteração de dados** | **Computadores protegidos** |
| --- | --- | --- | --- | --- |
| 8 vCPUs (2 soquetes * 4 núcleos @ 2,5 GHz) |16 GB |300 GB |500 GB ou menos |Implante um servidor de gerenciamento com essas configurações tooreplicate menos de 100 máquinas. |
| 12 vCPUs (2 soquetes * 6 núcleos @ 2,5 GHz) |18 GB |600 GB |500 GB too1 TB |Implante um servidor de gerenciamento com essas máquinas de 100-150 tooreplicate configurações. |
| 16 vCPUs (2 soquetes * 8 núcleos @ 2,5 GHz) |32 GB |1 TB |1 TB too2 TB |Implante um servidor de gerenciamento com essas máquinas de 150 e 200 tooreplicate configurações. |
| Implantar outro servidor de processo | | |> 2 TB |Implante servidores de processo adicional se você estiver replicando mais de 200 máquinas, ou se alterar dados diários Olá taxa excede 2 TB. |

Em que:

* Cada computador de origem é configurado com 3 discos de 100 GB.
* Usamos armazenamento de benchmark de 8 unidades SAS de 10K RPM com RAID 10.000 para as medidas do disco de cache.

### <a name="network-bandwidth-from-source-tootarget"></a>Largura de banda de rede de origem tootarget
Verifique se você calcular a largura de banda de saudação que seria necessária para a replicação inicial e a replicação delta usando Olá [ferramenta Planejador de capacidade](site-recovery-capacity-planner.md).

#### <a name="throttling-bandwidth-used-for-replication"></a>Limitação de largura de banda usada para replicação
VMware tráfego replicado tooAzure passa por um servidor de processo específico. Você pode acelerar Olá largura de banda disponível para replicação de recuperação de Site no servidor da seguinte maneira:

1. Abra Olá snap-in de MMC de Backup do Microsoft Azure no servidor de gerenciamento principal hello ou em um servidor de gerenciamento executando adicionais provisionado servidores de processo. Por padrão, um atalho para o Microsoft Azure Backup é criado na área de trabalho de saudação. Ou você pode encontrá-lo em C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Olá snap-in, clique em **alterar propriedades**.

    ![Limitar propriedades de largura de banda](./media/site-recovery-vmware-to-azure-classic/throttle1.png)
3. Em Olá **limitação** guia, especifique a largura de banda de saudação que pode ser usada para replicação de recuperação de Site e Olá agendamento aplicável.

    ![Limitar replicação de largura de banda](./media/site-recovery-vmware-to-azure-classic/throttle2.png)

Você também pode definir a limitação usando o PowerShell. Aqui está um exemplo:

    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth (512*1024) -NonWorkHourBandwidth (2048*1024)

#### <a name="maximizing-bandwidth-usage"></a>Maximizar o uso da largura de banda
tooincrease Olá largura de banda utilizada para replicação pelo Azure Site Recovery, você precisa toochange uma chave do registro.

Olá seguintes controles de tecla Olá número de threads por replicação de disco que são usados durante a replicação:

    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication\UploadThreadsPerVM

 Em uma rede sobreprovisionada, essa chave do registro precisa toobe alterado de seus valores padrão. Damos suporte ao máximo de 32.  

Para obter mais informações sobre o planejamento de capacidade detalhada, confira [Planejador de capacidade do Site Recovery](site-recovery-capacity-planner.md).

### <a name="additional-process-servers"></a>Servidores de processo adicionais
Se você precisa de mais de 200 máquinas tooprotect ou sua taxa de alteração diária é maior que 2 TB, você pode adicionar servidores adicionais toohandle Olá carga. tooscale-out, você pode:

* Aumente o número de saudação de servidores de gerenciamento. Por exemplo, você pode proteger as máquinas too400 com dois servidores de gerenciamento.
* Adicionar servidores de processo adicional e usar essas toohandle tráfego em vez de (ou além) Olá management server.

Esta tabela descreve um cenário em que:

* Você pode configurar Olá original toouse de servidor de gerenciamento como um servidor de configuração.
* Você configura um servidor de processo adicional.
* Configurar o servidor em processo adicionais de máquinas virtuais protegidas toouse hello.
* Cada computador de origem protegido é configurado com três discos de 100 GB cada.

| **Servidor de gerenciamento original**<br/><br/>(servidor de configuração) | **Servidor de processo adicional** | **Tamanho do disco de cache** | **Taxa de alteração de dados** | **Computadores protegidos** |
| --- | --- | --- | --- | --- |
| 8 vCPUs (2 soquetes * 4 núcleos @ 2,5 GHz), 16 GB de RAM |4 vCPUs (2 soquetes * 2 núcleos @ 2,5 GHz), 8 GB de RAM |300 GB |250 GB ou menos |Você pode replicar 85 computadores ou menos. |
| 8 vCPUs (2 soquetes * 4 núcleos @ 2,5 GHz), 16 GB de RAM |8 vCPUs (2 soquetes * 4 núcleos @ 2,5 GHz), 12 GB de RAM |600 GB |250 GB too1 TB |Você pode replicar de 85 a 150 computadores. |
| 12 vCPUs (2 soquetes * 6 núcleos @ 2,5 GHz), 18 GB de RAM |12 vCPUs (2 soquetes * 6 núcleos @ 2,5 GHz), 24 GB de RAM |1 TB |1 TB too2 TB |Você pode replicar de 150 a 225 computadores. |

A maneira como você escala seus servidores depende de sua preferência por um modelo que escale vertical ou horizontalmente. Você pode escalar verticalmente implantando alguns servidores de processo e de gerenciamento de alto nível ou escalar horizontalmente implantando mais servidores com menos recursos. Por exemplo: se você precisar 220 máquinas tooprotect, você pode fazer Olá seguinte:

* Configure o servidor de gerenciamento original Olá com 12 vCPUs e 18 GB de RAM. Configure o servidor de gerenciamento original com 12 vCPUs e 24 GB de RAM. Configure computadores protegidos toouse somente Olá processo adicional servidor.
* Configure dois servidores de gerenciamento (vCPUs 2 x 8 e 16 GB de RAM) e dois servidores de processo adicional (vCPUs 1x8 e 4vCPUs x 1 máquinas (220) de toohandle 135 + 85). Configure computadores protegidos toouse somente Olá processo adicional servidores.

Siga as instruções de saudação em [implantar servidores de processo adicional](#deploy-additional-process-servers) tooset um servidor de processo adicional.

## <a name="before-you-start-deployment"></a>Antes de começar a implantação
Olá, tabelas a seguir resumem os pré-requisitos de saudação para implantar este cenário.

### <a name="azure-prerequisites"></a>Pré-requisitos do Azure
| **Pré-requisito** | **Detalhes** |
| --- | --- |
| **Conta do Azure** |Você precisa de uma conta do [Microsoft Azure](https://azure.microsoft.com/) . Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/). Para obter mais informações sobre os preços do Site Recovery, consulte [Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/). |
| **Armazenamento do Azure** |É necessário um toostore replicado dados da conta de armazenamento do Azure. Os dados replicados são armazenados no armazenamento do Azure e as VMs do Azure se adaptam quando ocorre failover. <br/><br/>Você precisa de uma [conta de armazenamento com redundância geográfica standard](../storage/storage-redundancy.md#geo-redundant-storage). conta de saudação deve estar no hello mesma região Olá serviço Site Recovery e estar associada a saudação mesma assinatura. Contas de armazenamento de toopremium de replicação não tem suporte no momento e não deve ser usado.<br/><br/>Não há suporte para mover contas de armazenamento criadas usando Olá [portal do Azure](../storage/storage-create-storage-account.md) entre grupos de recursos. Para obter mais informações, consulte [tooMicrosoft Introdução armazenamento do Azure](../storage/storage-introduction.md).<br/><br/> |
| **Rede do Azure** |Você precisa de uma rede virtual do Azure que irá se conectar a máquinas virtuais do Azure toowhen failover ocorre. Olá rede virtual do Azure deve estar no hello mesma região Olá Cofre de recuperação de Site.<br/><br/>toofail após tooAzure de failover, você precisa de uma VPN conexão (ou rota expressa do Azure) configurar de saudação do Azure rede toohello no site local. |

### <a name="on-premises-prerequisites"></a>Pré-requisitos do local
| **Pré-requisito** | **Detalhes** |
| --- | --- |
| **Servidor de gerenciamento** |Você precisa de um servidor Windows 2012 R2 local em execução em uma máquina virtual ou em um servidor físico. Todos os componentes de Site Recovery Olá locais estão instalados neste servidor de gerenciamento.<br/><br/> É recomendável que implantar o servidor de saudação como uma VM altamente disponível do VMware. Failback toohello no site local do Azure é sempre tooVMware VMs, independentemente de se você fez failover VMs ou servidores físicos. Se você não configurar o servidor de gerenciamento hello como uma VM do VMware, você precisa tooset um servidor de destino mestre separada como um tráfego de failback tooreceive VM do VMware.<br/><br/>servidor de saudação não deve ser um controlador de domínio.<br/><br/>servidor de saudação deve ter um endereço IP estático.<br/><br/>nome de host de saudação do servidor de saudação deve ser de 15 caracteres ou menos.<br/><br/>localidade do sistema operacional Olá deve estar em inglês apenas.<br/><br/>servidor de gerenciamento de saudação requer acesso à Internet.<br/><br/>Você precisa ter acesso de saída do servidor de saudação da seguinte maneira: acesso temporário em 80 de HTTP durante a instalação dos componentes de recuperação de Site hello (toodownload MySQL); acesso de saída em andamento em HTTPS 443 para o gerenciamento de replicação. em andamento acesso de saída na 9443 HTTPS para o tráfego de replicação (essa porta pode ser modificada).<br/><br/> Verifique se que as URLs são acessíveis no servidor de gerenciamento de saudação: <br/>- \*.hypervrecoverymanager.windowsazure.com<br/>- \*.accesscontrol.windows.net<br/>- \*.backup.windowsazure.com<br/>- \*.blob.core.windows.net<br/>- \*.store.core.windows.net<br/>- https://www.msftncsi.com/ncsi.txt<br/>- [https://dev.MySQL.com/Get/archives/MySQL-5.5/MySQL-5.5.37-Win32.msi] (https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi")<br/><br/>Se você tiver regras de firewall baseado em endereço IP no servidor de saudação, verifique que regras de saudação permitem tooAzure de comunicação. Você precisa Olá tooallow [intervalos de IP de Datacenter do Azure](https://www.microsoft.com/download/details.aspx?id=41653) e hello porta HTTPS (443). Também é necessário toowhitelist os intervalos de endereços IP para Olá região do Azure de sua assinatura e Oeste dos EUA. Olá URL [https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi] (https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi") download MySQL. |
| **vCenter VMware/host ESXi** |Você precisa de um ou mais VMware vSphere ESX/ESXi hipervisores gerenciar suas máquinas virtuais VMware, executando ESX/ESXi versão 5.1, 5.5 ou 6.0 com atualizações mais recentes de saudação.<br/><br/> É recomendável que você implante um toomanage do VMware vCenter server seus hosts ESXi. Ele deve ser executado vCenter versão 6.0 ou 5.5 com atualizações mais recentes de saudação.<br/><br/>Observe que a Recuperação de Site não dá suporte aos novos recursos do vCenter e vSphere 6.0, como o vCenter vMotion cruzado, os volumes virtuais e o DRS de armazenamento. Suporte à recuperação de site é limitado toofeatures que também estavam disponíveis na versão 5.5. |
| **Computadores protegidos** |**As tabelas**<br/><br/>Máquinas que você deseja tooprotect devem estar em conformidade com [pré-requisitos do Azure](site-recovery-prereq.md) para a criação de máquinas virtuais do Azure.<br><br/>Se você quiser tooconnect toohello VMs do Azure após o failover, você precisa tooenable conexões de área de trabalho remota no firewall local hello.<br/><br/>A capacidade do disco individual nos computadores protegidos não deve ser maior que 1023 GB. Uma VM pode ter os discos too64 (e, portanto, o too64 TB). Se você tiver discos com mais de 1 TB, considere o uso da replicação de banco de dados, como o AlwaysOn do SQL Server ou Oracle Data Guard.<br/><br/>Mínimo 2 GB de espaço disponível na unidade de instalação Olá para instalação de componentes.<br/><br/>Não há suporte para clusters convidados de disco compartilhado. Se você tiver uma implantação clusterizada, considere o uso da replicação de banco de dados, como o AlwaysOn do SQL Server ou Oracle Data Guard.<br/><br/>Não há suporte para inicialização EFI (Extensible Firmware Interface)/UEFI (Unified Extensible Firmware Interface).<br/><br/>Os nomes dos computadores devem conter entre 1 e 63 caracteres (letras, números e hifens). nome da saudação deve começar com uma letra ou número e terminar com uma letra ou número. Depois que um computador estiver protegido, você pode modificar Olá nomes do Azure.<br/><br/>**VMs VMware**<br/><br>É necessário tooinstall VMware vSphere PowerCLI 6.0. no servidor de gerenciamento de saudação (servidor de configuração).<br/><br/>Você deseja tooprotect devem ter as ferramentas do VMware instalado e em execução de máquinas virtuais VMware.<br/><br/>Se a VM de origem Olá tem agrupamento NIC, ele será convertido tooa única NIC após tooAzure de failover.<br/><br/>Se as VMs protegidas tem um disco iSCSI, recuperação de Site converte Olá protegido disco iSCSI a VM em um arquivo VHD quando ocorrer failover tooAzure do hello VM. Se o destino iSCSI pode ser alcançado por Olá VM do Azure, ele se conectará destino tooiSCSI e basicamente ver dois discos: disco VHD Olá Olá VM do Azure e hello fonte iSCSI em disco. Nesse caso, você precisa toodisconnect do destino iSCSI Olá que aparece no hello failover VM do Azure.<br/><br/>Para obter mais informações sobre permissões de usuário do VMware Olá esse Site necessidades de recuperação, consulte [VMware permissões para acesso do vCenter](#vmware-permissions-for-vcenter-access).<br/><br/> **Computadores com Windows Server (na VM VMware ou no servidor físico)**<br/><br/>servidor de saudação deve estar executando um sistema operacional de 64 bits com suporte: Windows Server 2012 R2, Windows Server 2012 ou Windows Server 2008 R2 com no mínimo SP1.<br/><br/>sistema de operacional Olá deve ser instalado na unidade C e o disco de SO Olá deve ser um disco básico do Windows. (Olá sistema operacional não deve ser instalado em um disco dinâmico do Windows).<br/><br/>Para máquinas do Windows Server 2008 R2, você precisa toohave do .NET Framework 3.5.1 instalado.<br/><br/>Você precisa tooprovide uma conta de administrador (deve ser um administrador local no computador do Windows hello) para Olá instalação por push Olá serviço de mobilidade em servidores Windows. Se Olá fornecido é uma conta de domínio não, será necessário toodisable controle de acesso de usuário remoto na máquina local hello. Para obter mais informações, consulte [instalar serviço de mobilidade Olá com a instalação por push](#install-the-mobility-service-with-push-installation).<br/><br/>A Recuperação de Site dá suporte a VMs com um disco RDM. Durante o failback, recuperação de Site reutilizará o disco RDM Olá se Olá original de VM de origem e o disco RDM estão disponíveis. Se eles não estiverem disponíveis, o Site Recovery vai criar um novo arquivo VMDK para cada disco durante o failback.<br/><br/>**Computadores Linux**<br/><br/>Você precisa de um sistema operacional de 64 bits com suporte: Red Hat Enterprise Linux 6.7; CentOS 6.5, 6.6 ou 6.7; Oracle Enterprise Linux 6.4 ou 6.5 executando o kernel compatível do Red Hat hello ou inviolável Enterprise Kernel versão 3 (UEK3); SUSE Linux Enterprise Server 11 SP3.<br/><br/>arquivos de /etc/hosts em computadores protegidos devem conter entradas que mapeiam Olá host local nome tooIP endereços associados a todos os adaptadores de rede. <br/><br/>Se você quiser tooconnect tooan máquina virtual do Azure executando o Linux após o failover com um Secure Shell cliente (ssh), verifique se o serviço de Secure Shell Olá na máquina Olá protegido é definido toostart automaticamente na inicialização do sistema, e que regras de firewall permitem um ssh tooit de conexão.<br/><br/>Proteção só pode ser habilitada para máquinas Linux com hello armazenamento a seguir: arquivo de sistema (EXT3, ETX4, ReiserFS, XFS); Multipath dispositivo software mapeador (vários caminhos); Gerenciador de volumes (LVM2). Não há suporte a servidores físicos com o armazenamento de controlador HP CCISS. sistema de arquivos do Hello ReiserFS só tem suporte em SUSE Linux Enterprise Server 11 SP3.<br/><br/>A Recuperação de Site dá suporte a VMs com um disco RDM. Durante o failback para o Linux, a recuperação de Site não reutilizar o disco RDM hello. Em vez disso, ele cria um novo arquivo VMDK para cada disco RDM correspondente. |

Somente para uma VM do Linux: Certifique-se de que você definir Olá disk.enableUUID=true em Olá parâmetros de configuração de saudação VM no VMware. Se essa linha não existir, adicione-a. Isso é necessário tooprovide um toohello UUID VMDK consistente para que ele monta corretamente. Sem essa configuração, failback causará um download completo, mesmo se Olá VM está disponível no local. Adicionar essa configuração garante que apenas as alterações delta sejam transferidas durante o failback.

## <a name="step-1-create-a-vault"></a>Etapa 1: criar um cofre
1. Entrar toohello [portal do Azure](https://manage.windowsazure.com/).
2. Expanda **Serviços de Dados** > **Serviços de Recuperação** e clique em **Cofre do Site Recovery**.
3. Clique em **Criar Novo** > **Criação Rápida**.
4. Em **nome**, insira um cofre de saudação tooidentify nome amigável.
5. Em **região**, selecione Olá região geográfica para Olá cofre. regiões de toocheck com suporte, consulte [detalhes de preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Clique em **Criar cofre**.
    ![Criar cofre](./media/site-recovery-vmware-to-azure-classic/quick-start-create-vault.png)

Verifique a saudação tooconfirm de barra de status que Olá cofre foi criado com êxito. Olá cofre será listado como **Active** em Olá principal **dos serviços de recuperação** página.

## <a name="step-2-set-up-an-azure-network"></a>Etapa 2: configurar uma rede do Azure
Configure uma rede do Azure para que as VMs do Azure será conectado tooa rede após o failover e para que o local do failback toohello site pode funcionar como esperado.

1. No portal do Azure de Olá, selecione **criar rede virtual** e especifique o nome de rede de saudação, o intervalo de endereços IP e o nome da sub-rede.
2. Se você precisar de failback toodo, adicione a rede de toohello VPN/rota expressa. VPN/rota expressa pode ser adicionada toohello rede mesmo após o failover.

Para obter mais informações sobre redes do Azure, consulte [Visão geral de redes virtuais](../virtual-network/virtual-networks-overview.md).

> [!NOTE]
> [Migração de redes](../azure-resource-manager/resource-group-move-resources.md) em recursos grupos dentro Olá a mesma assinatura ou em assinaturas não é há suporte para redes usados para implantar a recuperação de Site.
>
>

## <a name="step-3-install-hello-vmware-components"></a>Etapa 3: Instalar os componentes do VMware Olá
Se você quiser que máquinas virtuais VMware a tooreplicate, siga estas etapas no servidor de gerenciamento de saudação:

1. [Baixe](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1) e instale o VMware vSphere Power CLI 6.0.
2. Reinicie o servidor de saudação.

## <a name="step-4-download-a-vault-registration-key"></a>Etapa 4: baixar uma chave de registro do cofre
1. No servidor de gerenciamento hello, abra o console de recuperação de Site de Olá no Azure. Em Olá **dos serviços de recuperação** , clique em saudação do hello cofre tooopen **início rápido** página. Você também pode abrir Olá **início rápido** página a qualquer momento clicando Olá ícone.

    ![Ícone Início Rápido](./media/site-recovery-vmware-to-azure-classic/quick-start-icon.png)
2. Em Olá **início rápido** , clique em **preparar recursos de destino** > **baixar uma chave de registro**. arquivo de registro de saudação é gerado automaticamente. Ele é válido por cinco dias após ter sido gerado.

## <a name="step-5-install-hello-management-server"></a>Etapa 5: Instalar o servidor de gerenciamento de saudação
> [!TIP]
> Verifique se que as URLs são acessíveis no servidor de gerenciamento de saudação:
>
> * *.hypervrecoverymanager.windowsazure.com
> * *.accesscontrol.windows.net
> * *.backup.windowsazure.com
> * *.blob.core.windows.net
> * *.store.core.windows.net
> * https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi
> * https://www.msftncsi.com/ncsi.txt
>
>



>[!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Setup-Registration/player]



1. Em Olá **início rápido** página, baixe o servidor de toohello de arquivos de instalação unificada hello.
2. Execute a instalação de toostart de arquivo de instalação Olá Olá **unificada de configuração do Site Recovery** assistente.
3. Em **antes de começar a**, selecione **instalar o servidor de configuração de saudação e servidor de processo**.

   ![Antes de começar](./media/site-recovery-vmware-to-azure-classic/combined-wiz1.png)
4. Em **licença de Software de terceiros**, clique em **aceito** toodownload e instalar o MySQL.

    ![Software de terceiros](./media/site-recovery-vmware-to-azure-classic/combined-wiz105.PNG)
5. Em **registro**, navegue e selecione a chave de registro de saudação que você baixou do cofre hello.

    ![Registro](./media/site-recovery-vmware-to-azure-classic/combined-wiz3.png)
6. Em **configurações de Internet**, especifique como o provedor de saudação em execução no servidor de configuração de saudação conectarão tooAzure Site Recovery pela Internet da saudação.

   * Se você desejar tooconnect com o proxy de saudação que está configurado na máquina hello, selecione **conectar-se com as configurações de proxy existentes**.
   * Se você desejar Olá provedor tooconnect diretamente, selecione **conectar-se diretamente sem um proxy**.
   * Se o proxy existente Olá requer autenticação, ou se você quiser toouse um proxy personalizado para a conexão do provedor de saudação, selecione **conectar-se com as configurações de proxy personalizadas**.
     * Se você usar um proxy personalizado, você precisará de credenciais, porta e endereço de saudação toospecify.
     * Se você estiver usando um proxy, você deve já ter permissão Olá seguintes URLs:
       * *.hypervrecoverymanager.windowsazure.com    
       * *.accesscontrol.windows.net
       * *.backup.windowsazure.com
       * *.blob.core.windows.net
       * *.store.core.windows.net

    ![Firewall](./media/site-recovery-vmware-to-azure-classic/combined-wiz4.png)

1. Em **verificação de pré-requisitos**, um toomake seleção-se de que a instalação de saudação pode executar a instalação é executada.

    ![Pré-requisitos](./media/site-recovery-vmware-to-azure-classic/combined-wiz5.png)

     Se aparecer um aviso sobre Olá **verificação da sincronização de horário Global**, verifique se esse tempo de saudação no relógio do sistema de saudação (**data e hora** configurações) Olá mesmo como o fuso horário hello.

     ![Problema de sincronização de tempo](./media/site-recovery-vmware-to-azure-classic/time-sync-issue.png)

1. Em **configuração MySQL**, criar credenciais para a assinatura na instância do servidor MySQL toohello que será instalada.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz6.png)
2. Em **detalhes do ambiente**, selecione se você vai tooreplicate VMware VMs. Se a resposta for positiva, a instalação verificará se o PowerCLI 6.0 está instalado.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz7.png)
3. Em **local de instalação**, selecione onde você deseja tooinstall binários de saudação e armazena o cache de saudação. Você pode selecionar uma unidade que tem ao menos 5 GB de espaço em disco disponível, mas é recomendável uma unidade de cache com ao menos 600 GB de espaço em disco disponível.

   ![Local de instalação](./media/site-recovery-vmware-to-azure-classic/combined-wiz8.png)
4. Em **seleção de rede**, especifique o ouvinte de saudação (adaptador de rede e porta SSL) no qual Olá servidor de configuração enviar e receber dados de replicação. Você pode modificar saudação padrão da porta (9443). Porta de toothis de adição, a porta 443 será usada por um servidor web que orquestra as operações de replicação. Não use a 443 para receber tráfego de replicação.

    ![Seleção da Rede](./media/site-recovery-vmware-to-azure-classic/combined-wiz9.png)



1. Em **resumo**, revise as informações de saudação e clique em **instalar**. Após a conclusão da instalação, uma frase secreta é gerada. Você precisará dela quando habilitar a replicação, portanto copie-a e guarde-a em um local seguro.

   ![Resumo](./media/site-recovery-vmware-to-azure-classic/combined-wiz10.png)


> [!WARNING]
> Olá proxy de agente de serviço de recuperação do Microsoft Azure deve ser configurado.
> Após a instalação de hello, inicie Olá Shell do Microsoft Azure Recovery Services no menu Iniciar do Windows do hello. Na janela de comando de saudação que é aberta, execute Olá conjunto de comandos tooset as configurações de servidor proxy Olá a seguir.
>
>
    $pwd = ConvertTo-SecureString -String ProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumb – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
>


### <a name="run-setup-from-hello-command-line"></a>Execute a instalação da linha de comando Olá
Você também pode executar Assistente unificada Olá Olá linha de comando, da seguinte maneira:

    UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]

Em que:

* /ServerMode: obrigatório. Especifica se a instalação de saudação deve instalar servidores de configuração e o processo de saudação ou Olá processo apenas servidor (servidores de processo adicional tooinstall usado). Valores de entrada: CS, PS.
* InstallDrive: obrigatório. Especifica a pasta de saudação onde Olá componentes estão instalados.
* /MySQLCredFilePath. Obrigatório. Especifica o arquivo de tooa de caminho Olá onde as credenciais do servidor MySQL Olá são armazenadas. Obter arquivo de Olá Olá modelo toocreate.
* /VaultCredFilePath. Obrigatório. Local do arquivo de credenciais de cofre hello.
* /EnvType. Obrigatório. Tipo de instalação. Valores: VMware, NonVMware.
* /PSIP e /CSIP. Obrigatório. Endereço IP do servidor de processo hello e o servidor de configuração.
* /PassphraseFilePath. Obrigatório. Local do arquivo de senha hello.
* /ByPassProxy. Opcional. Especifica o servidor de gerenciamento de saudação que se conecta tooAzure sem um proxy.
* /ProxySettingsFilePath. Opcional. Especifica configurações para um proxy personalizado (proxy padrão no servidor de saudação que requer autenticação) ou proxy personalizado.

## <a name="step-6-set-up-credentials-for-hello-vcenter-server"></a>Etapa 6: Configurar as credenciais do servidor do vCenter Olá
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Discovery/player]
>
>

servidor de processo Olá pode descobrir automaticamente máquinas virtuais do VMware que são gerenciados por um servidor do vCenter. Para a descoberta automática, recuperação de Site precisa de uma conta e credenciais que podem acessar o servidor do vCenter hello. Isso não é relevante se você estiver replicando apenas servidores físicos.

conta de saudação do tooset e as credenciais:

1. No servidor do vCenter hello, crie uma função (**Azure_Site_Recovery**) no nível do vCenter Olá com hello [as permissões necessárias](#vmware-permissions-for-vcenter-access).
2. Atribuir Olá **Azure_Site_Recovery** usuário do função tooa vCenter.

   > [!NOTE]
   > Uma conta de usuário do vCenter que tem a função hello de somente leitura pode executar failover sem desligar as máquinas de origem protegida. Se você quiser tooshut essas máquinas, você precisará Olá Azure_Site_Recovery função. Se você só estiver migrando máquinas virtuais do VMware tooAzure e não precisa toofail novamente, a função hello de somente leitura é suficiente.
   >
   >
3. conta de saudação tooadd, abra **cspsconfigtool**. Ele está disponível como um atalho na área de trabalho hello e está localizado na pasta de \home\svsystems\bin de Olá [local de instalação].
4. Em Olá **gerenciar contas** , clique em **adicionar conta**.

    ![Adicionar Conta](./media/site-recovery-vmware-to-azure-classic/credentials1.png)
5. Em **detalhes da conta**, adicionar as credenciais que podem ser usados tooaccess Olá servidor vCenter. Pode levar mais de 15 minutos para Olá tooappear de nome de conta no portal de saudação. tooupdate imediatamente, clique em **atualizar** em Olá **servidores de configuração** guia.

    ![Detalhes](./media/site-recovery-vmware-to-azure-classic/credentials2.png)

## <a name="step-7-add-vcenter-servers-and-esxi-hosts"></a>Etapa 7: adicionar servidores vCenter e hosts ESXi
Se você estiver replicando máquinas virtuais do VMware, você precisará tooadd um servidor do vCenter (ou host ESXi).

1. Em Olá **servidores** > **servidores de configuração** guia, selecione **adicionar vCenter server**.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter1.png)
2. Adicione servidor do vCenter hello ou detalhes de host de ESXi, nome de saudação da conta de saudação especificado tooaccess Olá servidor vCenter na etapa anterior Olá e o servidor de processo de saudação que será usado toodiscover VMware VMs que são gerenciados pelo servidor do vCenter Olá. servidor do vCenter Hello ou host ESXi deve estar localizado em Olá mesma rede como servidor de saudação em qual saudação do servidor em processo está instalado.

   > [!NOTE]
   > Se você está adicionando o host de ESXi com uma conta que não tem privilégios de administrador no servidor de saudação vCenter ou host ou servidor do vCenter Olá, certifique-se de Olá vCenter ou contas de ESXi tem esses privilégios habilitados: Datacenter, armazenamento de dados, pasta, Jost, rede, Recurso, a máquina Virtual e vSphere distribuído do comutador. servidor do vCenter Olá precisa de exibições de armazenamento de saudação privilégio habilitado.
   >
   >

    ![Adicionar servidor vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter2.png)
3. Após a descoberta, servidor do vCenter Olá será listado na Olá **servidores de configuração** guia.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter3.png)

## <a name="step-8-create-a-protection-group"></a>Etapa 8: criar um grupo de proteção
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Protection/player]
>
>

Grupos de proteção são agrupamentos lógicos de máquinas virtuais ou servidores físicos que você deseja tooprotect usando Olá mesmas configurações de proteção. Aplicar o grupo de proteção de tooa de configurações de proteção e essas configurações são aplicadas tooall máquinas (virtuais ou físicas) que você adicionar grupo toohello.

1. Vá muito**itens protegidos** > **grupo de proteção** e clique em Olá ícone tooadd um grupo de proteção.

    ![Criar grupo de proteção](./media/site-recovery-vmware-to-azure-classic/protection-groups1.png)
2. Em Olá **especificar configurações do grupo de proteção** página, especifique um nome para o grupo de saudação. Em Olá **de** lista suspensa, o servidor de configuração de select Olá no qual você deseja que o grupo de saudação toocreate. O **Destino** é Microsoft Azure.

    ![Configurações do grupo de proteção](./media/site-recovery-vmware-to-azure-classic/protection-groups2.png)
3. Em Olá **especificar configurações de replicação** página, defina as configurações de replicação de saudação que serão usadas para todas as máquinas Olá no grupo de saudação.

    ![Replicação do grupo de proteção](./media/site-recovery-vmware-to-azure-classic/protection-groups3.png)

   * **Consistência de múltiplas VMs**: se você ativar isso, ele cria pontos de recuperação consistentes com o aplicativo compartilhado entre máquinas Olá Olá grupo de proteção. Essa configuração é mais relevante quando estiver executando todas as máquinas no grupo de proteção Olá Olá a mesma carga de trabalho. Todos os computadores serão recuperado toohello mesmo ponto de dados. Esse recurso estará disponível se você estiver replicando VMs VMware ou servidores físicos (Windows ou Linux).
   * **O limite de RPO**: conjuntos Olá RPO. Alertas são gerados quando a replicação de proteção de dados contínua Olá excede o valor de limite RPO Olá configurado.
   * **Retenção de ponto de recuperação**: especifica uma janela de retenção hello. Computadores protegidos podem ser recuperados tooany ponto nessa janela.
   * **Frequência do instantâneo consistente com aplicativo**: especifica com que frequência são criados os pontos de recuperação que contêm instantâneos consistentes com aplicativos.

Quando você seleciona a marca de seleção hello, um grupo de proteção é criado com o nome hello especificado. Além disso, um segundo grupo de proteção é criado com o nome da saudação *nome do grupo de proteção*- Failback. Esse grupo de proteção é usado se você não toohello back local após tooAzure de failover. Você pode monitorar os grupos de proteção Olá conforme eles são criados em Olá **itens protegidos** página.

## <a name="step-9-install-hello-mobility-service"></a>Etapa 9: Instale o serviço de mobilidade Olá
Olá primeira etapa para habilitar a proteção para máquinas virtuais e servidores físicos é serviço de mobilidade tooinstall hello. É possível fazer isso de duas formas:

* Enviar por push e instalar serviço de saudação em cada computador saudação do servidor de processo automaticamente. Quando você adicionar o grupo de proteção tooa máquinas e eles já estiver executando uma versão apropriada do hello serviço de mobilidade, a instalação por push não ocorrerá. Você pode instalar o serviço Olá também automaticamente usando o método de push enterprise, como o WSUS ou o System Center Configuration Manager. Certifique-se de que configurar o servidor de gerenciamento de saudação antes de fazer isso.
* Instale serviço de saudação manualmente em cada computador que você deseja tooprotect. Certifique-se de que configurar o servidor de gerenciamento de saudação antes de fazer isso.

### <a name="install-hello-mobility-service-with-push-installation"></a>Instalar serviço de mobilidade Olá com a instalação por push
Quando você adiciona o grupo de proteção tooa máquinas, Olá serviço de mobilidade é automaticamente enviada por push e instalado em cada computador pelo servidor de processo hello.

#### <a name="prepare-for-automatic-push-on-windows-machines"></a>Preparar para o envio por push automático em computadores com Windows
tooprepare máquinas do Windows para que esse serviço de mobilidade Olá pode ser instalado automaticamente pelo servidor de processo hello:

1. Crie uma conta que nesse servidor de processo Olá pode usar a máquina de saudação do tooaccess. conta de saudação deve ter privilégios de administrador (local ou domínio). Essas credenciais são usadas apenas para a instalação por push do serviço de mobilidade de saudação.

   > [!NOTE]
   > Se você não estiver usando uma conta de domínio, você precisará toodisable controle de acesso de usuário remoto na máquina local hello. toodo isso, no registro de saudação sob HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System, adicione Olá entrada DWORD LocalAccountTokenFilterPolicy com um valor de 1 em. entrada de registro de saudação tooadd de uma CLI comando Abrir ou usando o PowerShell, digite  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** .
   >
   >
2. Firewall do Windows na máquina de saudação que você deseja tooprotect, selecione **permitem que um aplicativo ou recurso pelo Firewall**e habilitar **compartilhamento de arquivos e impressora** e **gerenciamento do Windows Instrumentação**. Para máquinas que pertencem a tooa domínio, você pode configurar a política de firewall de saudação com um GPO.

   ![Configurações de firewall](./media/site-recovery-vmware-to-azure-classic/mobility1.png)
3. Adicione conta Olá que você criou:

   * Abra **cspsconfigtool**. Ele está disponível como um atalho na área de trabalho hello e está localizado na pasta de \home\svsystems\bin de Olá [local de instalação].
   * Em Olá **gerenciar contas** , clique em **adicionar conta**.
   * Adicione conta Olá que você criou. Depois de adicionar a conta de saudação, você precisará tooprovide credenciais de hello quando você adiciona um grupo de proteção do computador tooa.

#### <a name="prepare-for-automatic-push-on-linux-servers"></a>Preparar para o envio por push automático em servidores Linux
1. Verifique se o computador Linux Olá desejado tooprotect tenha suporte, conforme descrito em [pré-requisitos locais](#on-premises-prerequisites). Verifique se há conectividade de rede entre a máquina Olá você deseja que o servidor de gerenciamento tooprotect e hello que executa o servidor de processo hello.
2. Crie uma conta que nesse servidor de processo Olá pode usar a máquina de saudação do tooaccess. conta de saudação deve ser um usuário raiz no servidor do hello origem Linux. Essas credenciais são usadas apenas para a instalação por push do serviço de mobilidade de saudação.

   * Abra **cspsconfigtool**. Ele está disponível como um atalho na área de trabalho hello e está localizado na pasta de \home\svsystems\bin de Olá [local de instalação].
   * Em Olá **gerenciar contas** , clique em **adicionar conta**.
   * Adicione conta Olá que você criou. Depois de adicionar a conta de saudação, você precisará tooprovide credenciais de hello quando você adiciona um grupo de proteção do computador tooa.
3. Verifique o arquivo /etc/hosts Olá na fonte Olá Linux server contém entradas que mapeiam Olá nome do host local tooIP endereços associados a todos os adaptadores de rede.
4. Instale pacotes de openssh, servidor openssh e openssl da mais recentes Olá na máquina de saudação que você deseja tooprotect.
5. Verifique se SSH está habilitado e em execução na porta 22.
6. Habilite a autenticação de subsistema e a senha SFTP no arquivo de sshd_config de saudação da seguinte maneira:

   * Entre como raiz.
   * No arquivo de /etc/ssh/sshd_config hello, localize a linha de saudação que começa com PasswordAuthentication.
   * Descomente a linha hello e altere o valor de saudação de **sem** muito**Sim**.
   * Linha de saudação de localização que começa com **subsistema** e remova os comentários de linha de saudação.

     ![Padrão de substituição de nenhum subsistema do Linux](./media/site-recovery-vmware-to-azure-classic/mobility2.png)

### <a name="install-hello-mobility-service-manually"></a>Instalar serviço de mobilidade Olá manualmente
instaladores de saudação estão disponíveis em C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository.

| Sistema operacional de origem | Arquivo de instalação do Serviço de mobilidade |
| --- | --- |
| Windows Server (somente 64 bits) |Microsoft-ASR_UA_9.*.0.0_Windows_* release.exe |
| CentOS 6.4, 6.5, 6.6 (somente 64 bits) |Microsoft-ASR_UA_9.*.0.0_RHEL6-64_*release.tar.gz |
| SUSE Linux Enterprise Server 11 SP3 (somente 64 bits) |Microsoft-ASR_UA_9.*.0.0_SLES11-SP3-64_*release.tar.gz |
| Oracle Enterprise Linux 6.4, 6.5 (somente 64 bits) |Microsoft-ASR_UA_9.*.0.0_OL6-64_*release.tar.gz |

#### <a name="install-hello-mobility-service-manually-on-a-windows-server"></a>Instalar serviço de mobilidade Olá manualmente em um servidor do Windows
1. Baixe e execute o instalador relevantes hello.
2. Em **Antes de começar**, selecione **Serviço de mobilidade**.

    ![Instalação do Serviço de mobilidade](./media/site-recovery-vmware-to-azure-classic/mobility3.png)
3. Em **detalhes do servidor de configuração**, especifique o endereço IP de saudação do servidor de gerenciamento hello e Olá frase secreta que foi gerada quando você instalou os componentes de servidor de gerenciamento de saudação. Você pode recuperar a frase secreta de saudação executando  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** no servidor de gerenciamento de saudação.

    ![Serviço de mobilidade](./media/site-recovery-vmware-to-azure-classic/mobility6.png)
4. Em **local de instalação**, manter saudação padrão local e clique em **próximo** toobegin instalação.
5. Em **progresso da instalação**, verifique a instalação e se solicitado, reinicie o computador de saudação.

Você também pode instalar inserindo Olá linha de comando de saudação do texto a seguir:

    UnifiedAgent.exe [/Role <Agent/MasterTarget>] [/InstallLocation <Installation Directory>] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>] [/LogFilePath <Log File Path>]

Em Olá precede o comando:

* /Role: obrigatório. Especifica se o serviço de mobilidade da saudação deve ser instalada.
* /InstallLocation: obrigatório. Especifica onde tooinstall Olá serviço.
* /PassphraseFilePath: obrigatório. Especifica a senha de servidor de configuração de saudação.
* /LogFilePath: obrigatório. Especifica o local de arquivo de configuração de log de saudação.

#### <a name="uninstall-hello-mobility-service-manually"></a>Desinstalar manualmente o serviço de mobilidade Olá
Você pode desinstalar o serviço de mobilidade hello usando **desinstalar ou alterar um programa** no painel de controle ou usando a linha de comando hello.

Olá comando toouninstall serviço de mobilidade usando a linha de comando Olá é:

    MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1}

#### <a name="change-hello-ip-address-of-hello-management-server"></a>Alterar o endereço IP hello saudação do servidor de gerenciamento
Depois de executar o Assistente de saudação, você pode alterar o endereço IP de saudação do servidor de gerenciamento de saudação da seguinte maneira:

1. Abra Olá arquivo hostconfig.exe (localizado na área de trabalho de saudação).
2. Em Olá **Global** , altere o endereço IP hello saudação do servidor de gerenciamento.

   > [!NOTE]
   > Altere somente o endereço IP hello saudação do servidor de gerenciamento. número da porta Olá para comunicações de servidor de gerenciamento deverá ser 443, e **Use HTTPS** deve ser esquerda habilitada. Não altere a senha hello.
   >
   >

    ![Endereço IP do servidor de gerenciamento](./media/site-recovery-vmware-to-azure-classic/host-config.png)

#### <a name="install-hello-mobility-service-manually-on-a-linux-server"></a>Instalar serviço de mobilidade Olá manualmente em um servidor Linux
1. Copie a máquina Olá tar apropriado arquivamento toohello Linux que você deseja tooprotect. Consulte a tabela de saudação em [instalar manualmente o serviço de mobilidade Olá](#install-the-mobility-service-manually) toodetermine quais tar arquivar deve usar.
2. Abrir um programa de shell e extraia o caminho do arquivo tar compactado arquivamento tooa local Olá executando:`tar -xvzf Microsoft-ASR_UA_8.5.0.0*`
3. Crie um arquivo chamado passphrase.txt em toowhich de diretório local Olá você extraiu o conteúdo de saudação do arquivo morto tar de saudação. toodo, cópia Olá senha de C:\ProgramData\Microsoft do Azure Site Recovery\private\connection.passphrase no servidor de gerenciamento hello e salve-o em passphrase.txt executando  *`echo <passphrase> >passphrase.txt`*  no shell de saudação.
4. Instale serviço de mobilidade Olá inserindo Olá comando a seguir:*`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`*
5. Especifique o endereço IP interno de saudação do servidor de gerenciamento hello e verifique se a porta 443 está selecionada.

#### <a name="install-hello-mobility-service-from-hello-command-line"></a>Instalar serviço de mobilidade de saudação da linha de comando Olá

Copiar senha Olá de C:\Program Files (x86) \InMage Systems\private\connection no servidor de gerenciamento hello e salvá-lo como "passphrase.txt" no servidor de gerenciamento de saudação. Em seguida, execute Olá comandos a seguir. Em nosso exemplo, endereço IP do servidor de gerenciamento de saudação é 104.40.75.37 e Olá porta HTTPS é 443:

tooinstall em um servidor de produção:

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt

tooinstall no servidor de destino mestre hello:

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt


## <a name="step-10-enable-protection-for-a-machine"></a>Etapa 10: habilitar a proteção para um computador
proteção de tooenable, adicionar máquinas virtuais e o grupo de proteção tooa servidores físicos. Antes de começar, observe o seguinte Olá se você estiver protegendo as máquinas virtuais VMware:

* Máquinas virtuais do VMware são descobertos a cada 15 minutos, e pode levar mais de 15 minutos para que eles tooappear no portal de recuperação de Site Olá após a descoberta.
* Alterações de ambiente na máquina virtual de saudação (como instalação de ferramentas do VMware) também podem levar mais de 15 minutos toobe atualizado na recuperação de Site.
* Você pode verificar o último Olá descoberto tempo para VMs VMware em hello **último contato em** campo servidor/ESXi host vCenter Olá Olá **servidores de configuração** guia.
* Se você adicionar um servidor vCenter ou host ESXi depois de criar um grupo de proteção, pode levar mais de 15 minutos para hello Azure Site Recovery portal toorefresh em máquinas virtuais toobe listados no hello **do grupo de proteção em tooa adicionar máquinas**caixa de diálogo.
* Se você quiser tooproceed imediatamente e adicionar o grupo de proteção tooa máquinas sem aguardar a descoberta agendada hello, realce o servidor de configuração de saudação (não clique nele) e clique em **atualizar**.

Além disso:

* Recomendamos que você arquitete seus grupos de proteção para que reflitam suas cargas de trabalho. Por exemplo, adicionar máquinas que executam um aplicativo específico toohello mesmo grupo.
* Quando você adiciona o grupo de proteção tooa máquinas, o servidor de processo Olá envia automaticamente e instala o serviço de mobilidade Olá se ele já não estiver instalado. Você precisará toohave mecanismo de envio de saudação preparado conforme descrito na etapa anterior hello.

### <a name="add-machines-tooa-protection-group"></a>Adicionar grupo de proteção tooa máquinas

1. Vá muito**itens protegidos** > **grupo de proteção** > **máquinas** > **adicionar máquinas** .
2. Se você estiver protegendo máquinas virtuais VMware, em **selecionar máquinas virtuais**, selecione um servidor do vCenter que gerencia suas máquinas virtuais (Olá EXSi host ou em que estejam em execução) e, em seguida, selecione as máquinas de saudação.

    ![Habilitar a proteção para máquinas virtuais](./media/site-recovery-vmware-to-azure-classic/enable-protection2.png)
3. Se você estiver protegendo servidores físicos, em **selecionar máquinas virtuais**, abra Olá **adicionar máquinas físicas** assistente e forneça o endereço IP de saudação e o nome amigável. Em seguida, selecione família de sistemas operacionais de saudação.

   ![Habilitar a proteção para servidores físicos](./media/site-recovery-vmware-to-azure-classic/enable-protection1.png)
4. Em **especificar recursos de destino**, selecione a conta de armazenamento Olá que você está usando para a replicação e selecione se Olá configurações devem ser usadas para todas as cargas de trabalho. Observe que as contas de armazenamento Premium não têm suporte no momento.

   > [!NOTE]
   > Não há suporte para mover contas de armazenamento criadas usando Olá [portal do Azure](../storage/storage-create-storage-account.md) entre grupos de recursos.                           
   > [Migração de contas de armazenamento](../azure-resource-manager/resource-group-move-resources.md) em recursos grupos dentro Olá a mesma assinatura ou em assinaturas não é há suporte para contas de armazenamento usadas para implantar a recuperação de Site.
   >
   >

    ![Definir as configurações de destino](./media/site-recovery-vmware-to-azure-classic/enable-protection3.png)
5. Em **especificar contas**, selecione Olá conta [configurar](#install-the-mobility-service-with-push-installation) toouse para instalação automática do serviço de mobilidade de saudação.

    ![Especificar as contas](./media/site-recovery-vmware-to-azure-classic/enable-protection4.png)
6. Clique em toofinish de marca de seleção Olá adicionando máquinas toohello proteção toostart e grupo de replicação inicial para cada máquina.

   > [!NOTE]
   > Se a instalação por push foi preparada, Olá serviço de mobilidade é instalado automaticamente nos computadores que não têm como elas são adicionadas toohello grupo de proteção. Depois Olá serviço é instalado, um trabalho de proteção é iniciado e falha. Depois de falha de hello, você precisará toomanually reiniciar cada máquina que tenha sido Olá serviço de mobilidade instalado. Após a reinicialização do hello, o trabalho de proteção Olá começa novamente e ocorre a replicação inicial.
   >
   >

Você pode monitorar o status de saudação **trabalhos** página.

![Monitorar o status na página de trabalhos Olá](./media/site-recovery-vmware-to-azure-classic/enable-protection5.png)

O status da proteção também pode ser monitorado em **Itens Protegidos** > *nome do grupo de proteção* > **Máquinas Virtuais**. Após a conclusão da replicação inicial e os dados são sincronizados, máquina alterações de status muito**protegidos**.

![Monitorar o status em Itens Protegidos](./media/site-recovery-vmware-to-azure-classic/enable-protection6.png)

## <a name="step-11-set-protected-machine-properties"></a>Etapa 11: definir propriedades de computador protegido
1. Quando um computador tem o status **Protegido**, você pode configurar as respectivas propriedades de failover. Em detalhes do grupo de proteção hello, selecione Olá Olá máquina e abra **configurar** guia.
2. Recuperação de site automaticamente sugere propriedades Olá VM do Azure e detecta Olá as configurações de rede local.

    ![Definir propriedades da máquina virtual](./media/site-recovery-vmware-to-azure-classic/vm-properties1.png)
3. Você pode alterar essas configurações:

   * **Nome da VM do Azure**: esse é nome hello terá toohello máquina do Azure após o failover. nome de saudação deve atender aos requisitos do Azure.
   * **Tamanho da VM do Azure**: número de saudação de adaptadores de rede é determinado pelo tamanho da saudação que você especificar para a máquina de virtual de destino hello. Para obter mais informações sobre tamanhos e adaptadores, consulte Olá [tamanho tabelas](../virtual-machines/linux/sizes.md). Observe que:

     * Quando você modificar o tamanho de saudação de uma máquina virtual e salva as configurações de Olá, o número de saudação de adaptadores de rede mudará quando você abrir Olá **configurar** Olá guia próxima vez. número mínimo de saudação de adaptadores de rede em máquinas virtuais de destino é igual toohello o número mínimo de adaptadores de rede em uma máquina virtual de origem. número máximo de saudação de adaptadores de rede é determinado pelo tamanho da saudação da máquina virtual de saudação.
       * Se Olá número de adaptadores de rede no computador de origem de saudação é menor ou igual toohello número de adaptadores permitido para tamanho de máquina de destino Olá, destino Olá terá Olá o mesmo número de adaptadores de fonte de saudação.
       * Se número Olá dos adaptadores de saudação da máquina virtual de origem exceder o número de saudação permitido para o tamanho de destino hello, tamanho máximo da saudação destino será usado.
        Por exemplo, se um computador de origem tem dois adaptadores de rede e o tamanho de máquina de destino Olá oferece suporte a quatro, computador de destino Olá terá dois adaptadores. Se máquina de origem Olá tem dois adaptadores de mas tamanho de destino Olá suporte oferece suporte a apenas um, computador de destino Olá terá apenas um adaptador.
     * Se a máquina virtual de saudação tem vários adaptadores de rede, todos os adaptadores devem ser conectado toohello mesma rede do Azure.
   * **Rede do Azure**: você deve especificar uma rede do Azure que máquinas virtuais do Azure será conectado tooafter failover. Se você não especificar um, Olá VMs do Azure não será conectada tooany rede. Além disso, você precisa toospecify uma rede do Azure se você quiser toofailback de toohello do Azure no site local. O failback requer uma conexão VPN entre uma rede do Azure e uma rede local.
   * **Endereço IP do Azure/sub-rede**: para cada adaptador de rede, selecione Olá Olá de toowhich de subrede VM do Azure deve se conectar. Observe que, se o adaptador de rede Olá Olá computador de origem é toouse configurado um endereço IP estático, você pode especificar um endereço IP estático para Olá VM do Azure. Se você não fornecer um endereço IP estático, um endereço IP disponível será alocado. Se o endereço IP de destino Olá for especificado, mas ele já está em uso por outra VM no Azure, failover falhará. Se o adaptador de rede Olá Olá computador de origem é configurado toouse DHCP, você terá de DHCP como configuração de saudação do Azure.      

## <a name="step-12-create-a-recovery-plan-and-run-a-failover"></a>Etapa 12: criar um plano de recuperação e executar um failover
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failover/player]
>
>

Você pode executar um failover para um único computador, ou você pode fazer failover de várias máquinas virtuais que executam Olá mesma tarefa ou execute Olá mesma carga de trabalho. toofail em vários computadores em Olá mesmo tempo, você adiciona o plano de recuperação tooa.

toocreate um plano de recuperação:

1. Em Olá **planos de recuperação** , clique em **Adicionar plano de recuperação** e adicionar um plano de recuperação. Especificar detalhes do plano de saudação e selecione **Azure** como destino de saudação.

 ![Configurar plano de recuperação](./media/site-recovery-vmware-to-azure-classic/recovery-plan1.png)
2. Em **Selecionar Máquina Virtual**, selecione um grupo de proteção e, em seguida, selecione máquinas no plano de recuperação Olá grupo tooadd toohello.

 ![Adicionar máquinas virtuais](./media/site-recovery-vmware-to-azure-classic/recovery-plan2.png)

Você pode personalizar a ordem de saudação sequência na qual máquinas no plano de recuperação de saudação são submetidas a failover e grupos de toocreate do plano de saudação. Você também pode adicionar scripts e prompts para ações manuais. Os scripts podem ser criados manualmente ou usando os [Runbooks de Automação do Azure](site-recovery-runbook-automation.md). Para obter mais informações sobre como personalizar os planos de recuperação, confira [Criar planos de recuperação](site-recovery-create-recovery-plans.md).

## <a name="run-a-failover"></a>Executar um failover
Antes de executar um failover:

* Verifique se que esse servidor de gerenciamento hello está em execução e disponível. Se não estiver, o failover falhará.
* Se executar um failover não planejado:

  * Se possível, você deve desligar os computadores primários antes de fazer um failover não planejado. Isso garante que você não tem dois computadores de origem e a réplica Olá em execução no hello simultaneamente. Se você estiver replicando máquinas virtuais do VMware, quando você executa um failover não planejado, você pode especificar que a recuperação de Site deve tentar tooshut máquinas de origem hello. Dependendo do estado de saudação do site primário hello, isso pode ou não funcione. Se você estiver replicando servidores físicos, o Site Recovery não oferecerá essa opção.
  * Um failover não planejado interrompe a replicação de dados de computadores primários para que qualquer delta de dados não seja transferido após o início desse failover não planejado.
  * Se você quiser a máquina virtual de réplica de toohello tooconnect no Azure após o failover, habilite Conexão de área de trabalho remota no computador de origem de saudação antes de executar failover de saudação. Permitir que a conexão RDP através do firewall do hello. Você também precisará tooallow RDP no ponto de extremidade públicos de máquina virtual do Azure de saudação Olá após o failover. Execute [práticas recomendadas](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) tooensure RDP funciona após um failover.

> [!NOTE]
> tooget Olá melhor desempenho quando você fizer uma tooAzure de failover, certifique-se de que você tenha instalado o hello Azure agente na máquina Olá protegido. Isso ajuda a inicialização da máquina hello mais rápido e ajuda a diagnosticar problemas. Hello Azure agente está disponível para [Linux](https://github.com/Azure/WALinuxAgent) e [Windows](http://go.microsoft.com/fwlink/?LinkID=394789).
>
>

### <a name="run-a-test-failover"></a>Execute um teste de failover
Executar o failover de um toosimulate de failover de teste e processos de recuperação em uma rede isolada que não afeta seu ambiente de produção e permite que a replicação normal continuarem normalmente. Failover de teste é initiatd na fonte Olá, e você pode executá-lo de duas maneiras:

* **Não especifique uma rede do Azure**: se você executar um failover de teste sem uma rede, o teste Olá verificará que máquinas virtuais iniciar e aparecer corretamente no Azure. Máquinas virtuais não será conectada tooan rede Azure após o failover.
* **Especifique uma rede do Azure**: esse tipo de failover verifica se o ambiente de replicação inteira Olá aparece conforme o esperado e máquinas virtuais do Azure são conectado toohello rede especificada.

toorun um failover de teste:

1. Em Olá **planos de recuperação** , selecione o plano de saudação e clique em **Failover de teste**.

 ![Selecione o plano de saudação](./media/site-recovery-vmware-to-azure-classic/test-failover1.png)
2. Em **confirmar Failover de teste**, selecione **nenhum** tooindicate que você não quiser toouse uma rede do Azure para failover de teste hello, ou teste de Olá Olá selecione rede toowhich máquinas virtuais será conectada após o failover. Clique em Olá marca de seleção toostart Olá failover.

 ![Faça uma seleção](./media/site-recovery-vmware-to-azure-classic/test-failover2.png)
3. Monitorar o progresso de failover no hello **trabalhos** guia.

 ![Monitorar o progresso](./media/site-recovery-vmware-to-azure-classic/test-failover3.png)
4. Após a conclusão do failover hello, você também deve ser capaz de toosee Olá réplica máquina do Azure aparecerá na **máquinas virtuais** no hello portal do Azure. Se você quiser tooinitiate uma conexão de RDP toohello VM do Azure, você precisará tooopen porta 3389 no ponto de extremidade VM hello.
5. Depois que você estiver concluído, quando failover atinge Olá **concluir** teste fase, clique em **teste completo** toofinish. Em **notas**, gravar e salvar todas as observações associadas Olá failover de teste.
6. Clique em **Olá failover de teste for concluído** tooautomatically limpar o ambiente de teste de saudação. Após ter feito isso, o failover de teste Olá mostrará uma **concluir** status. Os elementos ou máquinas virtuais criadas automaticamente durante o failover de teste de saudação são excluídos. Se um failover de teste continua mais de duas semanas, ele será forçado toofinish.

### <a name="run-an-unplanned-failover"></a>Executar um failover não planejado
Failover não planejado é iniciado do Azure e pode ser executado, mesmo se o site primário Olá não está disponível.

1. Em Olá **planos de recuperação** , selecione o plano de saudação e clique em **Failover** > **Failover não planejado**.

 ![Selecione o plano de saudação](./media/site-recovery-vmware-to-azure-classic/unplanned-failover1.png)
2. Se você estiver replicando máquinas virtuais VMware, você pode tentar tooshut para VMs locais. Esta é uma ação de melhor esforço e failover continua se esforço Olá for bem-sucedida ou não. Se não for bem-sucedida, os detalhes do erro serão exibida no hello **trabalhos** guia **trabalhos de Failover não planejado**.

 ![Opção para desligar as VMs locais](./media/site-recovery-vmware-to-azure-classic/unplanned-failover2.png)

 > [!NOTE]
 > Essa opção não estará disponível se você estiver replicando servidores físicos. Você precisará tootry tooshut aqueles para baixo manualmente se possível.
 >
 >

3. Em **confirmar Failover**, verifique se a direção do failover hello (tooAzure) e selecione o ponto de recuperação de saudação que você deseja toouse para failover de saudação. Se você tiver habilitado várias VMs ao configurar propriedades de replicação, você pode recuperar o ponto de recuperação mais recente consistente ou aplicativo toohello. Você também pode selecionar **ponto de recuperação personalizado** toorecover tooan ponto anterior no tempo. Clique em Olá marca de seleção toostart Olá failover.

 ![Confirmar direção do failover](./media/site-recovery-vmware-to-azure-classic/unplanned-failover3.png)
4. Aguarde a saudação toofinish de trabalho de failover não planejado. Você pode monitorar o progresso de failover em Olá **trabalhos** guia. Mesmo se ocorrerem erros durante o failover não planejado, o plano de recuperação de saudação executa até que ela seja concluída. Você também deve ser capaz de toosee Olá réplica máquina do Azure aparecerá na **máquinas virtuais** no hello portal do Azure.

### <a name="connect-tooreplicated-azure-virtual-machines-after-failover"></a>Conecte-se tooreplicated Azure máquinas virtuais depois do failover
tooconnect tooreplicated máquinas virtuais no Azure após o failover, você precisa:

- Uma conexão de área de trabalho remota habilitada na máquina principal hello.
- Firewall do Windows no computador primário Olá definido tooallow RDP.
- RDP adicionado toohello o ponto de extremidade público para Olá máquina virtual do Azure.

Para obter mais informações sobre a configuração, confira [Solucionando problemas de conexão de área de trabalho remota após failover usando ASR](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

## <a name="deploy-additional-process-servers"></a>Implantar servidores de processo adicionais
Se você deve expandir sua implantação, além de 200 máquinas de origem, ou se a taxa de rotatividade diária total exceder 2 TB, você precisará de volume de tráfego de saudação do processo adicional servidores toohandle. tooset um servidor de processo adicional, verificação de saudação requisitos no [servidores adicionais do processo](#additional-process-servers), e em seguida, configure o servidor de processo Olá toohello de acordo com as instruções a seguir. Depois de configurar o servidor de saudação, você pode configurar a origem máquinas toouse-lo.

### <a name="set-up-an-additional-process-server"></a>Configurar um servidor de processo adicional
Defina um servidor de processo adicional da seguinte maneira:

* Execute Olá unificado Assistente tooconfigure um servidor de gerenciamento como um servidor de processo.
* Se você quiser a replicação de dados toomanage usando apenas Olá novo servidor de processo, você precisa toomigrate seus computadores protegidos.

### <a name="install-hello-process-server"></a>Instalar o servidor de processo Olá
1. Em Olá **início rápido** página, baixe o arquivo de instalação unificada de saudação do hello instalação de componentes do Site Recovery. Execute a instalação.
2. Em **antes de começar a**, selecione **adicionar tooscale de servidores de processo adicional implantação**.

 ![Adicionar servidor de processo](./media/site-recovery-vmware-to-azure-classic/add-ps1.png)
3. Conclua o Assistente de saudação como você fez quando você [configurar](#step-5-install-the-management-server) primeiro servidor de gerenciamento hello.
4. Em **detalhes do servidor de configuração**, insira o endereço IP Olá Olá original do servidor de gerenciamento em que você instalou o servidor de configuração de saudação e, em seguida, insira a senha de saudação. Se você não tem senha hello, execute  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** em tooretrieve de servidor de gerenciamento original Olá-lo.

 ![Detalhes do servidor de configuração](./media/site-recovery-vmware-to-azure-classic/add-ps2.png)

### <a name="migrate-machines-toouse-hello-new-process-server"></a>Migrar máquinas toouse Olá novo servidor de processo
1. Abra **servidores de configuração** > **servidor** > *nome do servidor de gerenciamento original Olá*  >   **Detalhes do servidor**.

 ![Detalhes do servidor](./media/site-recovery-vmware-to-azure-classic/update-process-server1.png)
2. Em Olá **servidores de processo** lista, selecione **alterar servidor de processo** próximo servidor toohello que você deseja toochange.

 ![Atualizar o servidor de processo Olá](./media/site-recovery-vmware-to-azure-classic/update-process-server2.png)
3. Selecione **alterar servidor de processo**, selecione **servidor de processo de destino**, e, em seguida, selecione Olá novo servidor de gerenciamento. Máquinas virtuais selecione Olá Olá novo servidor de processo tratará. Clique em Olá ícone tooget informações sobre o servidor de saudação. Olá médio espaço necessário tooreplicate cada máquina virtual selecionada toohello novo servidor de processo é exibida toohelp que você fizer as decisões de carga. Clique em toostart de marca de seleção Olá replicando toohello novo servidor de processo.

 ![Alterar servidor de processo Olá](./media/site-recovery-vmware-to-azure-classic/update-process-server3.png)

## <a name="vmware-permissions-for-vcenter-access"></a>Permissões de VMware para acesso do vCenter
servidor de processo Olá pode descobrir automaticamente as VMs em um servidor do vCenter. descoberta automática de tooperform, você precisa toodefine uma função (Azure_Site_Recovery) no servidor de saudação vCenter nível tooallow recuperação de Site tooaccess Olá vCenter. Se você só precisa toomigrate VMware máquinas tooAzure e não é necessário toofailback do Azure, você pode definir uma função somente leitura que é suficiente. Configurar as permissões de saudação conforme descrito em [etapa 6: configurar as credenciais do servidor do vCenter Olá](#step-6-set-up-credentials-for-the-vcenter-server). permissões de função Hello estão resumidas na Olá a tabela a seguir:

| **Função** | **Detalhes** | **Permissões** |
| --- | --- | --- |
| Função Azure_Site_Recovery |Descoberta de máquina virtual VMware |Atribua esses privilégios para o servidor de v-Center hello:<br/><br/>Datastore: Alocar espaço, Pesquisar datastore, Operações de arquivo de nível baixo, Remover arquivo, Atualizar arquivos de máquina virtual<br/><br/>Rede: Atribuição de rede<br/><br/>Recurso: Atribua pool tooresource de máquinas virtuais, migração desligado máquina virtual, migrar alimentado na máquina virtual<br/><br/>Tarefas: Criar tarefa, Atualizar tarefa<br/><br/>Máquina virtual: Configuração<br/><br/>Máquina virtual: Interagir -> Responder pergunta, Conexão de dispositivo, Configurar mídia de CD, Configurar mídia de disquete, Desligar, Ligar, Instalação de ferramentas VMware<br/><br/>Máquina virtual > Inventário > Criar, Registrar, Cancelar registro<br/><br/>Máquina virtual > Provisionamento -> Permitir download de máquina virtual, Permitir upload de arquivos de máquina virtual<br/><br/>Máquina virtual > Instantâneos > Remover instantâneos |
| Função de usuário do vCenter |Descoberta de máquina virtual VMware/Failover sem o desligamento da VM de origem |Atribua esses privilégios para o servidor de v-Center hello:<br/><br/>Objeto de Data Center > propagar tooChild objeto, a função = somente leitura <br/><br/>usuário Olá é atribuído ao nível de datacenter hello e, portanto, tem acesso tooall Olá objetos no datacenter hello. Se você quiser toorestrict Olá acesso, atribuir Olá **nenhum acesso** função com hello **propagar toochild** toohello os objetos filho (hosts ESX, armazenamentos de dados, máquinas virtuais e redes) do objeto. |
| Função de usuário do vCenter |Failover e failback |Atribua esses privilégios para o servidor de v-Center hello:<br/><br/>Objeto de data center – Propagate toochild objeto, a função = Azure_Site_Recovery<br/><br/>usuário de saudação é atribuído ao nível do datacenter e, portanto, tem acesso tooall Olá objetos no datacenter hello.  Se você quiser toorestrict Olá acesso, atribuir hello * * sem acesso * * função com hello **Propagate toochild objeto** objeto filho de toohello (hosts ESX, armazenamentos de dados, máquinas virtuais e redes). |

## <a name="third-party-software-notices-and-information"></a>Avisos e informações de software de terceiros
<!--Do Not Translate or Localize-->

software Hello e firmware em execução no hello produto da Microsoft ou o serviço se baseia em ou incorpora material dos Olá projetos listados abaixo (coletivamente, "código de terceiros").  A Microsoft está Olá autor original não Olá código de terceiros.  Olá original de direitos autorais e licença, sob a qual a Microsoft recebeu esse código de terceiros, estão definidos abaixo.

informações de saudação na seção A é em relação ao código de terceiros, componentes de projetos de saudação listados abaixo. Such licenses and information are provided for informational purposes only.  Esse código de terceiros está sendo tooyou relicensed pela Microsoft em termos de produto da Microsoft hello ou o serviço de licenciamento de software da Microsoft.  

informações de saudação na seção B for referente a componentes de código de terceiros que estão sendo feitas tooyou disponível pela Microsoft em termos de licenciamento original hello.

arquivo completo Olá pode ser encontrado em Olá [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel or otherwise.

## <a name="next-steps"></a>Próximas etapas
[Saiba mais sobre failback](site-recovery-failback-azure-to-vmware-classic.md) toobring tooyour ambiente de local de volta a suas máquinas de failover em execução no Azure.
