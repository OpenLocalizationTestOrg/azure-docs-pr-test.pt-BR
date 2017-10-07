---
title: "matriz de suporte de recuperação de Site aaaAzure para replicar tooAzure | Microsoft Docs"
description: "Resume os componentes e sistemas operacionais de saudação com suporte do Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: rajanaki
ms.openlocfilehash: eae1db2ff1392d272f6b2eb0e3410da19d09da7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-support-matrix-for-replicating-from-on-premises-tooazure"></a>Matriz de suporte do Azure Site Recovery para replicação do local tooAzure


Este artigo resume os componentes e configurações com suporte para o Azure Site Recovery Quando a replicação e a recuperação tooAzure. Para obter mais informações sobre os requisitos de recuperação de Site do Azure, consulte Olá [pré-requisitos](site-recovery-prereq.md).


## <a name="support-for-deployment-options"></a>Suporte para opções de implantação

**Implantação** | **Servidor VMware/físico** | **Hyper-V (com/sem o Virtual Machine Manager)** |
--- | --- | ---
**Portal do Azure** | Local do armazenamento de tooAzure VMs VMware, com o Gerenciador de recursos do Azure ou armazenamento clássico e redes.<br/><br/> Failover tooResource clássicos ou com base no Gerenciador de máquinas virtuais. | Local do armazenamento de tooAzure de VMs Hyper-V, com o Gerenciador de recursos ou armazenamento clássico e redes.<br/><br/> Failover tooResource clássicos ou com base no Gerenciador de máquinas virtuais.
**Portal clássico** | Somente modo de manutenção. Não é possível criar novos cofres. | Somente modo de manutenção.
**PowerShell** | Não há suporte no momento. | Suportado


## <a name="support-for-datacenter-management-servers"></a>Suporte para servidores de gerenciamento do datacenter

### <a name="virtualization-management-entities"></a>Entidades de gerenciamento de virtualização

**Implantação** | **Suporte**
--- | ---
**Servidor da VM VMware/físico** | vCenter 6.5, 6.0 ou 5.5
**Hyper-V (com Virtual Machine Manager)** | System Center Virtual Machine Manager 2016 e System Center Virtual Machine Manager 2012 R2

  >[!Note]
  > No momento, não há suporte para uma nuvem do System Center Virtual Machine Manager 2016 com uma combinação de hosts do Windows Server 2016 e 2012 R2.

### <a name="host-servers"></a>Servidores de host

**Implantação** | **Suporte**
--- | ---
**Servidor da VM VMware/físico** | vSphere 6.5, 6.0, 5.5
**Hyper-V (com/sem o Virtual Machine Manager)** | Windows Server 2016, Windows Server 2012 R2 com as atualizações mais recentes.<br></br>Se for usado o SCVMM, os hosts do Windows Server 2016 deverão ser gerenciados pelo SCVMM 2016.


  >[!Note]
  >No momento, não há suporte para um site do Hyper-V que combine hosts que executam o Windows Server 2016 e 2012 R2. Atualmente não há suporte para recuperação tooan local alternativo para máquinas virtuais em um host do Windows Server 2016.

## <a name="support-for-replicated-machine-os-versions"></a>Suporte para versões do SO do computador replicado

Máquinas virtuais que são protegidas deve atender aos [requisitos do Azure](#failed-over-azure-vm-requirements) ao replicar tooAzure.
Olá, a tabela a seguir resume o suporte de sistema operacional replicados em vários cenários de implantação durante o uso do Azure Site Recovery. Esse suporte é aplicável para qualquer carga de trabalho em execução no hello mencionado o sistema operacional.

 **Servidor VMware/físico** | **Hyper-V (com/sem o VMM)** |
--- | --- |
Windows Server 2012 R2 de 64 bits, Windows Server 2012, Windows Server 2008 R2 com pelo menos SP1<br/>*Windows Server 2016* – sem suporte no momento em máquinas virtuais VMware e servidores físicos. <br/><br/> Red Hat Enterprise Linux: 5.2 too5.11, too6.8 6.1, too7.3 7.0 <br/><br/>Sistema operacional centavos: too5.11 5.2, too6.8 6.1, too7.3 7.0 <br/><br/>Servidor do Ubuntu 14.04 LTS[ (suporte para versões de kernel)](#supported-ubuntu-kernel-versions-for-vmwarephysical-servers)<br/><br/>Servidor LTS do Ubuntu 16.04[ (versões de kernel com suporte)](#supported-ubuntu-kernel-versions-for-vmwarephysical-servers)<br/><br/>Oracle Enterprise Linux 6.4, 6.5 executando o kernel compatível do Red Hat hello ou inviolável Enterprise Kernel versão 3 (UEK3) <br/><br/> SUSE Linux Enterprise Server 11 SP3 <br/><br/> SUSE Linux Enterprise Server 11 SP4 <br/>(Não há suporte para atualização de replicação de máquinas do SLES 11 SP3 tooSLES 11 SP4. Se um computador replicado tiver sido atualizado do SLES 11SP3 tooSLES 11 SP4, você precisa de replicação toodisable e proteger máquina Olá novamente após atualização hello.) | Qualquer SO convidado [com suporte do Azure](https://technet.microsoft.com/library/cc794868.aspx)


>[!IMPORTANT]
>(Aplicável tooVMware/servidores físicos replicando tooAzure)
>
> No Red Hat Enterprise Linux Server 7 + e servidores CentOS 7 +, kernel versão 3.10.0-514 tem suporte a partir da versão 9,8 do hello serviço de mobilidade de recuperação de Site do Azure.<br/><br/>
> Os clientes do núcleo de 3.10.0-514 Olá com uma versão do hello inferior à versão 9,8 do serviço de mobilidade estão toodisable necessário replicação, versão de saudação de atualização do tooversion de serviço de mobilidade Olá 9,8 e, em seguida, habilitar novamente.


### <a name="supported-ubuntu-kernel-versions-for-vmwarephysical-servers"></a>Versões com suporte do kernel Ubuntu para servidores VMware/físicos

**Versão** | **Versão de serviço de mobilidade** | **Versão do kernel** |
--- | --- | --- |
14.04 LTS | 9.9 | 3.13.0-24-Generic too3.13.0-117-genérico<br/>3.16.0-25-Generic too3.16.0-77-genérico<br/>3.19.0-18-Generic too3.19.0-80-genérico<br/>4.2.0-18-Generic too4.2.0-42-genérico<br/>4.4.0-21-Generic too4.4.0 75 genérico |
14.04 LTS | 9.10 | 3.13.0-24-Generic too3.13.0 121-genérico,<br/>3.16.0-25-Generic too3.16.0-77-genérico<br/>3.19.0-18-Generic too3.19.0-80-genérico<br/>4.2.0-18-Generic too4.2.0-42-genérico<br/>4.4.0-21-Generic too4.4.0 81 genérico |
16.04 LTS | 9.10 | 4.4.0-21-Generic too4.4.0-81-genérico<br/>4.8.0-34-Generic too4.8.0-56-genérico<br/>4.10.0-14-Generic too4.10.0 24 genérico |


## <a name="supported-file-systems-and-guest-storage-configurations-on-linux-vmwarephysical-servers"></a>Sistemas de arquivos e configurações de armazenamento de convidado com suporte no Linux (servidores VMware/físicos)

a seguir Olá sistemas de arquivos e armazenamento há suporte para o software de configuração em servidores Linux em execução nos servidores VMware ou Physical:
* Sistemas de arquivos: ext3, ext4, ReiserFS (somente Suse Linux Enterprise Server), XFS
* Gerenciador de volumes: LVM2
* Software Multipath: Device Mapper

Não há suporte para dispositivos de armazenamento paravirtualizados (dispositivos exportados por drivers paravirtualizados).<br/>
Não há suporte para dispositivos de E/S de bloco de várias filas.<br/>
Não há suporte para servidores físicos com o controlador de armazenamento HP CCISS hello.<br/>

>[!Note]
> Na saudação de servidores Linux diretórios a seguir (se configurado como partições/arquivo-sistemas separados) devem estar no hello mesmo disco (disco Olá SO) no servidor de origem Olá: / (raiz), /boot em /usr., /usr/local, /var, /etc/hosts<br/><br/>
> Recursos de XFSv5 em sistemas de arquivos XFS como soma de verificação de metadados têm suporte a partir da versão 9.10 de saudação serviço de mobilidade. Se você estiver usando recursos XFSv5, execute o Serviço de Mobilidade versão 9.10 ou mais recente. Você pode usar super-bloco do hello xfs_info utilitário toocheck Olá XFS para partição hello. Se ftype for definido too1, XFSv5 recursos estão sendo usados.
>


## <a name="support-for-network-configuration"></a>Suporte para configuração da rede
Olá tabelas a seguir resume o suporte à configuração de rede em vários cenários de implantação que usam o Azure Site Recovery tooreplicate tooAzure.

### <a name="host-network-configuration"></a>Configuração de rede do host

**Configuração** | **Servidor VMware/físico** | **Hyper-V (com/sem o Virtual Machine Manager)**
--- | --- | ---
Agrupamento NIC | Sim<br/><br/>Não há suporte quando computadores físicos são replicados| Sim
VLAN | Sim | Sim
IPv4 | Sim | Sim
IPv6 | Não | Não

### <a name="guest-vm-network-configuration"></a>Configuração de rede da VM convidada

**Configuração** | **Servidor VMware/físico** | **Hyper-V (com/sem o Virtual Machine Manager)**
--- | --- | ---
Agrupamento NIC | Não | Não
IPv4 | Sim | Sim
IPv6 | Não | Não
IP estático (Windows) | Sim | Sim
IP estático (Linux) | Sim <br/><br/>Máquinas virtuais é configurado toouse DHCP em failback  | Não
NIC múltipla | Sim | Sim

### <a name="failed-over-azure-vm-network-configuration"></a>Configuração de rede da VM do Azure após failover

**Rede do Azure** | **Servidor VMware/físico** | **Hyper-V (com/sem o Virtual Machine Manager)**
--- | --- | ---
ExpressRoute | Sim | Sim
ILB | Sim | Sim
ELB | Sim | Sim
Gerenciador de Tráfego | Sim | Sim
NIC múltipla | Sim | Sim
IP Reservado | Sim | Sim
IPv4 | Sim | Sim
Reter o IP de origem | Sim | Sim


## <a name="support-for-storage"></a>Suporte para armazenamento
Olá tabelas a seguir resume o suporte à configuração de armazenamento em vários cenários de implantação que usam o Azure Site Recovery tooreplicate tooAzure.

### <a name="host-storage-configuration"></a>Configuração de armazenamento do host

**Configuração** | **Servidor VMware/físico** | **Hyper-V (com/sem o Virtual Machine Manager)**
--- | --- | --- | ---
NFS | Sim para VMware<br/><br/> Não para servidores físicos | N/D
SMB 3.0 | N/D | Sim
SAN (ISCSI) | Sim | Sim
Múltiplos caminhos (MPIO)<br></br>Testado com: Microsoft DSM, EMC PowerPath 5.7 SP4, EMC PowerPath DSM for CLARiiON | Sim | Sim

### <a name="guest-or-physical-server-storage-configuration"></a>Configuração de armazenamento do servidor físico ou convidado

**Configuração** | **Servidor VMware/físico** | **Hyper-V (com/sem o Virtual Machine Manager)**
--- | --- | ---
VMDK | Sim | N/D
VHD/VHDX | N/D | Sim
VM ger 2 | N/D | Sim
EFI/UEFI| Não | Sim
Disco de cluster compartilhado | Não | Não
Disco criptografado | Não | Não
NFS | Não | N/D
SMB 3.0 | Não | Não
RDM | Sim<br/><br/> N/D para servidores físicos | N/D
Disco > 1 TB | Sim<br/><br/>Até 4.095 GB | Sim<br/><br/>Até 4.095 GB
Disco com tamanho de setor de 4K | Sim | Sim, há suporte para VMs da geração 1<br/><br/>Não há suporte para VMs da geração 2.
Volume com discos distribuídos > 1 TB<br/><br/> Gerenciamento de Volume lógico LVM | Sim | Sim
Espaços de Armazenamento | Não | Sim
Adição/remoção de disco a quente | Não | Não
Exclusão de disco | Sim | Sim
Múltiplos caminhos (MPIO) | N/D | Sim

**Armazenamento do Azure** | **Servidor VMware/físico** | **Hyper-V (com/sem o Virtual Machine Manager)**
--- | --- | ---
LRS | Sim | Sim
GRS | Sim | Sim
RA-GRS | Sim | Sim
Armazenamento frio | Não | Não
Armazenamento quente| Não | Não
Criptografia em repouso (SSE)| Sim | Sim
Armazenamento Premium | Sim | Sim
Serviço de importação/exportação | Não | Não


## <a name="support-for-azure-compute-configuration"></a>Suporte para configuração de computação do Azure

**Recurso de computação** | **Servidor VMware/físico** | **Hyper-V (com/sem o Virtual Machine Manager)**
--- | --- | --- 
Conjuntos de disponibilidade | Sim | Sim
HUB | Sim | Sim  
Discos gerenciados | Sim | Sim<br/><br/>Failback tooon local da VM do Azure com discos gerenciados não é suportada atualmente.

## <a name="failed-over-azure-vm-requirements"></a>Requisitos de VM do Azure após failover

Você pode implantar a recuperação de Site tooreplicate VMs e servidores físicos executando qualquer sistema operacional com suporte pelo Azure. Isso inclui a maioria das versões do Windows e do Linux. Máquinas virtuais que você deseja tooreplicate devem estar em conformidade com hello seguindo os requisitos do Azure durante a replicação tooAzure ao local.

**Entidade** | **Requisitos** | **Detalhes**
--- | --- | ---
**Sistema operacional convidado** | Replicação do Hyper-V tooAzure: recuperação de Site oferece suporte a todos os sistemas operacionais que são [tem suporte pelo Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx). <br/><br/> Para replicação de servidor físico e VMware: verificar Olá Windows e Linux [pré-requisitos](site-recovery-vmware-to-azure-classic.md) | A verificação de pré-requisitos falhará se não houver suporte.
**Arquitetura do sistema operacional convidado** | 64 bits | A verificação de pré-requisitos falhará se não houver suporte
**Tamanho de disco do sistema operacional** | Até too2048 GB se você estiver replicando **VMs VMware ou servidores físicos tooAzure**.<br/><br/>Até 2.048 GB para VMs **Hyper-V Geração 1**.<br/><br/>Até 300 GB para VMs **Hyper-V Geração 2**.  | A verificação de pré-requisitos falhará se não houver suporte
**Contagem de discos do sistema operacional** | 1 | A verificação de pré-requisitos falhará se não houver suporte.
**Contagem de discos de dados** | 64 ou se você estiver replicando **VMs VMware tooAzure**; 16 ou menos se você estiver replicando **tooAzure de VMs Hyper-V** | A verificação de pré-requisitos falhará se não houver suporte
**Tamanho do VHD do disco de dados** | A too4095 GB | A verificação de pré-requisitos falhará se não houver suporte
**Adaptadores de rede** | Há suporte para vários adaptadores |
**VHD compartilhado** | Sem suporte | A verificação de pré-requisitos falhará se não houver suporte
**Disco FC** | Sem suporte | A verificação de pré-requisitos falhará se não houver suporte
**Formato de disco rígido** | VHD  <br/><br/> VHDX | Embora atualmente não há suporte para VHDX no Azure, recuperação de Site automaticamente VHDX tooVHD quando houver falha tooAzure. Quando você failback tooon Olá máquinas virtuais continuam no formato VHDX toouse hello.
**Bitlocker** | Sem suporte | O BitLocker deve ser desabilitado antes de proteger uma máquina virtual.
**Nome da VM** | Entre 1 e 63 caracteres. Tooletters restrito, números e hifens. nome da VM Olá deve começar e terminar com uma letra ou número. | Atualize o valor de saudação nas propriedades de máquina virtual de saudação na recuperação de Site.
**Tipo de VM** | Geração 1<br/><br/> Geração 2 - Windows | VMs da Geração 2 com um tipo de disco básico de SO (que inclui um ou dois volumes de dados formatados como VHDX) e suporte para menos de 300 GB de espaço em disco.<br></br>Não há suporte para VMs Linux da Geração 2. [Saiba mais](https://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/)|

## <a name="support-for-recovery-services-vault-actions"></a>Suporte para ações do cofre dos Serviços de Recuperação

**Ação** | **Servidor VMware/físico** | **Hyper-V (sem Virtual Machine Manager)** | **Hyper-V (com Virtual Machine Manager)**
--- | --- | --- | ---
Mover cofre entre grupos de recursos<br/><br/> Dentro e entre as assinaturas | Não | Não | Não
Mover armazenamento, rede, VMs do Azure entre grupos de recursos<br/><br/> Dentro e entre as assinaturas | Não | Não | Não


## <a name="support-for-provider-and-agent"></a>Suporte para o Provedor e o Agente

**Nome** | **Descrição** | **Última versão** | **Detalhes**
--- | --- | --- | --- | ---
**Provedor do Azure Site Recovery** | Coordena as comunicações entre servidores locais e o Azure <br/><br/> Instalado em servidores locais do Virtual Machine Manager ou em servidores Hyper-V, se não houver nenhum servidor do Virtual Machine Manager | 5.1.19 ([disponível no portal](http://aka.ms/downloaddra)) | [Recursos e correções mais recentes](https://support.microsoft.com/kb/3155002)
**Configuração do Azure Site Recovery unificado (tooAzure VMware)** | Coordena as comunicações entre servidores VMware locais e o Azure  <br/><br/> Instalado nos servidores VMware no locais | 9.3.4246.1 (disponível no portal) | [Recursos e correções mais recentes](https://support.microsoft.com/kb/3155002)
**Serviço de mobilidade** | Coordena a replicação entre servidores VMware/servidores físicos locais e o Azure/site secundário<br/><br/> Instalado na VM do VMware ou servidores físicos que você deseja tooreplicate  | N/D (disponível no portal) | N/D
**Agente de MARS (Serviços de Recuperação do Microsoft Azure)** | Coordena a replicação entre VMs Hyper-V e o Azure<br/><br/> Instalado em servidores Hyper-V locais (com ou sem um servidor do Virtual Machine Manager) | Agente mais recente ([disponível no portal](http://aka.ms/latestmarsagent)) |






## <a name="next-steps"></a>Próximas etapas
[Verificar pré-requisitos](site-recovery-prereq.md)
