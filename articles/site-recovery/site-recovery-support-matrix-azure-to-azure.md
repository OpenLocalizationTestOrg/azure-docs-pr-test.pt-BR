---
title: "matriz de suporte a recuperação de Site para replicação do Azure tooAzure aaaAzure | Microsoft Docs"
description: "Resume os sistemas operacionais de saudação com suporte e configurações de replicação do Azure Site Recovery de máquinas virtuais (VMs) do Azure de uma região tooanother para necessidades de recuperação de desastres."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/10/2017
ms.author: sujayt
ms.openlocfilehash: 75b2451b4c2069ca4b11deb0efe1329d43879eb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-support-matrix-for-replicating-from-azure-tooazure"></a>Matriz de suporte do Azure Site Recovery para replicação do tooAzure do Azure


>[!NOTE]
>
> Atualmente, a replicação do Site Recovery para máquinas virtuais do Azure está em versão prévia.

Este artigo resume os componentes e configurações com suporte para o Azure Site Recovery Quando a replicação e a recuperação de máquinas virtuais do Azure da região de tooanother de uma região.

## <a name="user-interface-options"></a>Opções de interface do usuário

**Interface do usuário** |  **Com suporte/Sem suporte**
--- | ---
**Portal do Azure** | Suportado
**Portal clássico** | Sem suporte
**PowerShell** | Sem suporte no momento
**API REST** | Sem suporte no momento
**CLI** | Sem suporte no momento


## <a name="resource-move-support"></a>Suporte de movimentação de recursos

**Tipo de movimentação de recursos** | **Com suporte/Sem suporte** | **Comentários**  
--- | --- | ---
**Mover cofre entre grupos de recursos** | Sem suporte |Você não pode mover o Cofre de serviços de recuperação de saudação entre grupos de recursos.
**Mover Computação, Armazenamento e Rede entre grupos de recursos** | Sem suporte |Se você mover uma máquina virtual (ou seus componentes associados, como armazenamento e rede) depois de habilitar a replicação, você precisa de replicação toodisable e habilitar a replicação da máquina virtual de saudação novamente.


## <a name="support-for-deployment-models"></a>Suporte para modelos de implantação

**Modelo de implantação** | **Com suporte/Sem suporte** | **Comentários**  
--- | --- | ---
**Clássico** | Suportado | É possível replicar apenas uma máquina virtual clássica e recuperá-la como uma máquina virtual clássica. Não é possível recuperá-la como uma máquina de virtual do Resource Manager. Se você implantar uma VM clássica sem uma rede virtual e diretamente tooan região do Azure, não há suporte.
**Gerenciador de Recursos** | Suportado |

## <a name="support-for-replicated-machine-os-versions"></a>Suporte para versões do SO do computador replicado

Olá abaixo suporte é aplicável para qualquer carga de trabalho em execução no hello mencionado o sistema operacional.

#### <a name="windows"></a>Windows

- Windows Server 2016 (Server Core e Servidor com Experiência Desktop)*
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 com, no mínimo, SP1

>[!NOTE]
>
> \* Não há suporte para o Windows Server 2016 Nano Server.

#### <a name="linux"></a>Linux

- Red Hat Enterprise Linux 6.7, 6.8, 7.0, 7.1, 7.2 e 7.3
- CentOS 6.5, 6.6, 6.7, 6.8, 7.0, 7.1, 7.2, 7.3
- Ubuntu 14.04 LTS Server [ (versões de kernel com suporte)](#supported-ubuntu-kernel-versions-for-azure-virtual-machines)
- Ubuntu 16.04 LTS Server [ (versões de kernel com suporte)](#supported-ubuntu-kernel-versions-for-azure-virtual-machines)
- Oracle Enterprise Linux 6.4, 6.5 executando o kernel compatível do Red Hat hello ou inviolável Enterprise Kernel versão 3 (UEK3)
- SUSE Linux Enterprise Server 11 SP3

>[!NOTE]
>
> Ubuntu servidores usando a senha com base em autenticação e logon, e usar máquinas de virtuais de nuvem Olá nuvem init pacote tooconfigure, pode ter senha logon desabilitada após o failover (dependendo da configuração de cloudinit hello.) Logon baseada em senha pode ser habilitada novamente na máquina virtual de saudação redefinindo a senha de saudação no menu de configurações de saudação (em Olá suporte + seção solução de problemas) do hello failover da máquina virtual no portal do Azure de saudação.

### <a name="supported-ubuntu-kernel-versions-for-azure-virtual-machines"></a>Versões com suporte do kernel Ubuntu para máquinas virtuais do Azure

**Versão** | **Versão de serviço de mobilidade** | **Versão do kernel** |
--- | --- | --- |
14.04 LTS | 9.9 | 3.13.0-24-Generic too3.13.0-117-genérico<br/>3.16.0-25-Generic too3.16.0-77-genérico<br/>3.19.0-18-Generic too3.19.0-80-genérico<br/>4.2.0-18-Generic too4.2.0-42-genérico<br/>4.4.0-21-Generic too4.4.0 75 genérico |
14.04 LTS | 9.10 | 3.13.0-24-Generic too3.13.0 121-genérico,<br/>3.16.0-25-Generic too3.16.0-77-genérico<br/>3.19.0-18-Generic too3.19.0-80-genérico<br/>4.2.0-18-Generic too4.2.0-42-genérico<br/>4.4.0-21-Generic too4.4.0 81 genérico |
16.04 LTS | 9.10 | 4.4.0-21-Generic too4.4.0-81-genérico<br/>4.8.0-34-Generic too4.8.0-56-genérico<br/>4.10.0-14-Generic too4.10.0 24 genérico |

## <a name="supported-file-systems-and-guest-storage-configurations-on-azure-virtual-machines-running-linux-os"></a>Sistemas de arquivos com suporte e configurações de armazenamento de convidado em máquinas virtuais do Azure que executam o sistema operacional Linux

* Sistemas de arquivos: ext3, ext4, ReiserFS (somente Suse Linux Enterprise Server), XFS
* Gerenciador de volumes: LVM2
* Software Multipath: Device Mapper

## <a name="region-support"></a>Suporte de regiões

Você pode replicar e recuperar VMs entre quaisquer duas regiões dentro de saudação mesmo cluster geográfico.

**Cluster geográfico** | **Regiões do Azure**
-- | --
América | Leste do Canadá, Canadá Central, Centro-Sul dos EUA, Centro-Oeste dos EUA, Leste dos EUA, Leste dos EUA 2, Oeste dos EUA, Oeste dos EUA 2, EUA Central, Centro-Norte dos EUA
Europa | Oeste do Reino Unido, Sul do Reino Unido, Europa Setentrional, Europa Ocidental
Ásia | Sul da Índia, Índia Central, Sudeste Asiático, Ásia Oriental, Leste do Japão, Oeste do Japão, Coreia Central, Sul da Coreia
Austrália   | Leste da Austrália, Sudeste da Austrália

>[!NOTE]
>
> Para região Sul do Brasil, você só pode replicar e fazer failover tooone do Centro Sul dos EUA, oeste centro dos EUA, Leste dos EUA, Leste dos EUA 2, oeste dos EUA, oeste dos EUA 2 e regiões Centro Norte dos EUA e falha.


## <a name="support-for-compute-configuration"></a>Suporte para configuração de Computação

**Configuração** | **Com suporte/Sem suporte** | **Comentários**
--- | --- | ---
Tamanho | Qualquer tamanho de VM do Azure com, no mínimo, 2 núcleos de CPU e 1 GB de RAM | Consulte também[tamanhos de máquina virtual do Azure](../virtual-machines/windows/sizes.md)
Conjuntos de disponibilidade | Suportado | Se você usar a opção padrão de saudação durante a etapa 'Habilitar replicação' no portal, o conjunto de disponibilidade de saudação é automaticamente criado com base na configuração de região de origem. Você pode alterar a disponibilidade de destino Olá definida ' item replicadas > Configurações > computação e rede > conjunto de disponibilidade ' qualquer momento.
VMs do HUB (Benefício de Uso Híbrido) | Suportado | Se a VM de origem Olá tem licença HUB habilitada, Olá failover de teste ou Failover de VM também usa licenças HUB hello.
conjuntos de escala de máquina virtual | Sem suporte |
Imagens da Galeria do Azure – publicadas pela Microsoft | Suportado | Suporte contanto que Olá VM é executado em um sistema operacional suportado pela recuperação de Site
Imagens da Galeria do Azure – publicadas por terceiros | Suportado | Suporte como Olá VM é executado em um sistema operacional suportado pela recuperação de Site.
Imagens personalizadas – publicadas por terceiros | Suportado | Suporte como Olá VM é executado em um sistema operacional suportado pela recuperação de Site.
VMs migradas com o Site Recovery | Suportado | Se ele é migrado de uma máquina VMware/físicos tooAzure com a recuperação de Site, você precisa toouninstall hello mais antiga versão do serviço de mobilidade e reiniciar a máquina de saudação antes de replicar o tooanother região do Azure.

## <a name="support-for-storage-configuration"></a>Suporte para configuração de Armazenamento

**Configuração** | **Com suporte/Sem suporte** | **Comentários**
--- | --- | ---
Tamanho máximo do disco do sistema operacional | 1023 GB | Consulte também[discos usados por máquinas virtuais.](../virtual-machines/windows/about-disks-and-vhds.md#disks-used-by-vms)
Tamanho máximo do disco de dados | 1023 GB | Consulte também[discos usados por máquinas virtuais.](../virtual-machines/windows/about-disks-and-vhds.md#disks-used-by-vms)
Número de discos de dados | Até 64, com suporte em um tamanho específico de VM do Azure | Consulte também[tamanhos de máquina virtual do Azure](../virtual-machines/windows/sizes.md)
Disco temporário | Sempre excluído da replicação | O disco temporário sempre é excluído da replicação. Você não deve colocar nenhum dado persistente no disco temporário, de acordo com as diretrizes do Azure. Consulte também[em disco temporário em VMs do Azure](../virtual-machines/windows/about-disks-and-vhds.md#temporary-disk) para obter mais detalhes.
Taxa de disco de saudação de alteração de dados | Máximo de 6 MBps por disco | Se a taxa de alteração de dados de média de saudação em disco hello está além 6 MBps continuamente, a replicação não será atualizado. No entanto, se for uma intermitência de dados ocasionais e Olá taxa de alteração de dados é maior que 6 MBps por algum tempo e resume, a replicação será atualizado. Nesse caso, talvez você veja os pontos de recuperação um pouco atrasados.
Discos em contas de armazenamento Standard | Suportado |
Discos em contas de armazenamento Premium | Suportado | Se uma VM tem discos distribuídos em contas de armazenamento standard e premium, você pode selecionar uma conta de armazenamento de destino diferente para cada disco tooensure tiver Olá a mesma configuração de armazenamento na região de destino
Managed Disks Standard | Sem suporte |  
Managed Disks Premium | Sem suporte |
Espaços de armazenamento | Suportado |         
Criptografia em repouso (SSE) | Suportado | Para contas de armazenamento de cache e de destino, você pode selecionar uma conta de armazenamento habilitada para SSE.     
ADE (Azure Disk Encryption) | Sem suporte |
Adição/remoção de disco a quente | Sem suporte | Se você adicionar ou remove discos de dados em Olá VM, você precisa de replicação toodisable e habilitar a replicação novamente para Olá VM.
Exclusão de disco | Sem suporte|   O disco temporário é excluído por padrão.
LRS | Suportado |
GRS | Suportado |
RA-GRS | Suportado |
ZRS | Sem suporte |  
Armazenamento Frio e Quente | Sem suporte | Não há suporte para discos de máquina virtual no armazenamento frio e quente

>[!IMPORTANT]
> Certifique-se de que você siga Olá [diretrizes de armazenamento](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) para sua fonte de virtual do Azure máquinas tooavoid eventuais problemas de desempenho. Se você seguir as configurações padrão de saudação, recuperação de Site criará contas de armazenamento Olá necessárias com base na configuração de fonte de saudação. Se você personalizar e selecione suas próprias configurações, certifique-se de seguir hello (... / storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) como a fonte de VMs.

## <a name="support-for-network-configuration"></a>Suporte para configuração de Rede
**Configuração** | **Com suporte/Sem suporte** | **Comentários**
--- | --- | ---
NIC (adaptador de rede) | Até o número máximo de NICs com suporte em um tamanho específico de VM do Azure | NICs são criados quando Olá VM é criado como parte da operação de Failover ou failover de teste. Olá número de NICs em failover Olá que VM depende do número Olá da fonte de saudação NICs de que VM tem no tempo de saudação de habilitação da replicação. Se você adicionar ou remover NIC depois de habilitar a replicação, ele não afeta contagem NIC Olá failover da VM.
Balanceador de Carga de Internet | Suportado | Você precisa tooassociate Olá pré-configurado balanceador de carga usando um script de automação do azure em um plano de recuperação.
Balanceador de carga interno | Suportado | Você precisa tooassociate Olá pré-configurado balanceador de carga usando um script de automação do azure em um plano de recuperação.
IP público| Suportado | Necessário tooassociate um toohello IP público NIC já existente ou crie um e associar toohello NIC usando um script de automação do azure em um plano de recuperação.
NSG na NIC (Resource Manager)| Suportado | É necessário tooassociate Olá NSG toohello NIC usando um script de automação do azure em um plano de recuperação.  
NSG na sub-rede (Resource Manager e Clássico)| Suportado | É necessário tooassociate Olá NSG toohello NIC usando um script de automação do azure em um plano de recuperação.
NSG na VM (Clássico)| Suportado | É necessário tooassociate Olá NSG toohello NIC usando um script de automação do azure em um plano de recuperação.
IP Reservado (IP Estático)/Reter o IP de origem | Suportado | Se Olá NIC na VM de origem Olá configuração de IP estático e a sub-rede de destino Olá tem Olá mesmo IP disponível, ele está atribuído toohello failover VM. Se a sub-rede de destino Olá não tem Olá mesmo IP disponível, um dos Olá IPs disponíveis na sub-rede Olá será reservada para essa VM. Você pode especificar um IP fixo de sua escolha em “Item replicado > Configurações > Computação e Rede > Adaptadores de rede”. Você pode selecionar Olá NIC e especificar sub-rede hello e IP de sua escolha.
IP Dinâmico| Suportado | Se Olá NIC na VM de origem Olá configuração de IP dinâmico Olá NIC Olá failover VM também é dinâmico por padrão. Você pode especificar um IP fixo de sua escolha em “Item replicado > Configurações > Computação e Rede > Adaptadores de rede”. Você pode selecionar Olá NIC e especificar sub-rede hello e IP de sua escolha.
Integração do Gerenciador de Tráfego | Suportado | Você pode pré-configurar o Gerenciador de tráfego de forma que o tráfego de Olá é o ponto de extremidade roteados toohello na região de origem em um ponto de extremidade regular base e toohello na região de destino no caso de failover.
DNS gerenciado do Azure | Suportado |
DNS Personalizado  | Suportado |    
Proxy não autenticado | Suportado | Consulte também[documento de diretrizes de rede.](site-recovery-azure-to-azure-networking-guidance.md)    
Proxy autenticado | Sem suporte | Se Olá VM estiver usando um proxy autenticado para conectividade de saída, ela não pode ser replicada usando o Azure Site Recovery.  
Site tooSite VPN com o local (com ou sem ExpressRoute)| Suportado | Certifique-se de que UDRs hello e NSGs estão configurados de forma tráfego Olá de recuperação de Site não é roteado tooon local. Consulte também[documento de diretrizes de rede.](site-recovery-azure-to-azure-networking-guidance.md)  
Conexão de tooVNET de rede virtual | Suportado | Consulte também[documento de diretrizes de rede.](site-recovery-azure-to-azure-networking-guidance.md)  


## <a name="next-steps"></a>Próximas etapas
- Saiba mais sobre as [diretrizes de rede para replicação de VMs do Azure](site-recovery-azure-to-azure-networking-guidance.md)
- Inicie a proteção de suas cargas de trabalho [replicando VMs do Azure](site-recovery-azure-to-azure.md)
