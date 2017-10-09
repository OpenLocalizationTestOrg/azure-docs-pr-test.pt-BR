---
title: "aaaBackup e recuperação de desastres para os discos do Azure IaaS | Microsoft Docs"
description: "Neste artigo, explicaremos como tooplan para Backup e recuperação de desastres (DR) de máquinas virtuais (VMs) e discos no Azure. Este documento aborda Discos Gerenciados e Discos Não Gerenciados"
services: storage
cloud: Azure
documentationcenter: na
author: luywang
manager: kavithag
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: luywang
ms.openlocfilehash: 49b0e7732d6df9407e1e44d9af2500c99a85b37e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-disaster-recovery-for-azure-iaas-disks"></a>Backup e recuperação de desastre de discos de IaaS do Azure

Neste artigo, explicaremos como tooplan para Backup e recuperação de desastres (DR) de máquinas virtuais (VMs) e discos no Azure. Este documento aborda Discos Gerenciados e Discos Não Gerenciados.

Primeiro, falaremos sobre Olá falhas incorporada tolerância recursos em Olá plataforma Windows Azure que ajudam a proteger contra falhas locais. Em seguida, discutiremos os cenários de desastre Olá não totalmente cobertos pelo recursos internos de saudação, que é o tópico principal Olá, resolvido por este documento. Também mostraremos vários exemplos de cenários de carga de trabalho nos quais diferentes considerações de Backup e DR podem se aplicar. Depois, examinaremos possíveis soluções para DR de discos de IaaS. 

## <a name="introduction"></a>Introdução

Olá plataforma Windows Azure usa vários métodos para redundância e toohelp de tolerância a falhas proteger os clientes contra falhas de hardware localizadas que podem ocorrer. Falhas locais podem incluir problemas com um computador de servidor de armazenamento do Azure que armazena a parte dos dados de saudação para um disco virtual ou falhas de um SSD ou HDD nesse servidor. Essas falhas de componente de hardware isoladas podem ocorrer durante as operações normais e plataforma de saudação é projetado toobe toothese resiliente falhas. Desastres graves podem resultar em falhas ou na incapacidade de acesso de um grande número de servidores de armazenamento ou de um datacenter inteiro. Enquanto a suas máquinas virtuais e discos normalmente são protegidos contra falhas localizadas, etapas adicionais são necessária tooprotect sua carga de trabalho de toda a região de falhas catastróficas (por exemplo, um grande desastre) que pode afetar sua VM e discos.

Além disso toohello a possibilidade de falhas de plataforma, com dados ou aplicativo de cliente hello podem ocorrer problemas. Por exemplo, uma nova versão do seu aplicativo pode inadvertidamente tornar uma separação toohello dados de alteração. Nesse caso, convém aplicativo hello de toorevert e Olá dados tooa versão anterior contendo Olá último estado bom conhecido. Isso exige a manutenção de backups regulares.

Para a recuperação de desastre regional, você deve fazer o backup de sua região do IaaS VM discos tooa diferente. 

Antes de examinarmos as opções de Backup e DR, vamos recapitular alguns métodos disponíveis para o tratamento de falhas localizadas.

### <a name="azure-iaas-resiliency"></a>Resiliência de IaaS do Azure

*Resiliência* refere-se a toohello tolerância a falhas normais que ocorrem nos componentes de hardware. Resiliência é Olá toorecover de capacidade de falhas e continuar toofunction. Não é sobre como evitar falhas, mas respondendo toofailures de uma maneira que evita o tempo de inatividade ou perda de dados. meta de saudação de resiliência é tooreturn Olá tooa funcionando completamente o estado do aplicativo após uma falha. Máquinas virtuais do Azure e os discos são falhas de hardware projetado toobe toocommon resiliente. Vamos dar uma olhada em como plataforma de IaaS do Azure Olá fornece essa capacidade de recuperação.

Uma máquina virtual consiste principalmente em duas partes: (1) um servidor e discos persistentes hello (2) de computação. Ambos afetam a tolerância a falhas de saudação de uma máquina virtual.

Se o servidor de host de computação do Azure Olá que hospeda a VM passa por uma falha de hardware (que é rara), o Azure é projetado tooautomatically restauração Olá VM em outro servidor. Se isso acontecer, você terá uma reinicialização e Olá VM será feito backup após algum tempo. Azure automaticamente detecta essas falhas de hardware e executa recuperações toohelp garantir cliente Olá VM estarão disponível assim que possível.

Em relação aos discos de IaaS, é fundamental para a plataforma de armazenamento persistente Olá durabilidade dos dados. Clientes do Azure têm aplicativos de negócios importantes em execução em IaaS e eles dependem de persistência de saudação de dados de saudação. O Azure projeta a proteção para esses discos de IaaS com três cópias redundantes dos dados armazenados localmente, fornecendo alta durabilidade contra falhas locais. Se um dos componentes de hardware de saudação que contém o disco falhar, a VM não é afetada porque há duas cópias adicionais toosupport disco solicitações. Ele funciona corretamente mesmo se dois componentes de hardware diferente, dando suporte a um disco falharem em Olá mesmo tempo (o que seria muito raro). Verifique se toohelp sempre mantemos três réplicas, o serviço de armazenamento do Azure hello gera automaticamente uma nova cópia dos dados no plano de fundo de saudação se um dos três cópias de saudação ficar indisponível. Portanto, não deve ser necessário toouse RAID com discos do Azure para tolerância a falhas. Um simples de RAID 0 configuração deve ser suficiente para distribuição discos Olá se volumes maiores toocreate necessário.

Devido a essa arquitetura, o **Azure proporcionou durabilidade de nível empresarial de modo consistente para discos de IaaS, com uma [Taxa de Falha Anualizada](https://en.wikipedia.org/wiki/Annualized_failure_rate) líder do setor de 0%.**

Falhas de hardware localizadas na saudação de computação de host ou no armazenamento de saudação plataforma às vezes pode resultar na indisponibilidade temporária para Olá VM que é coberto por Olá [SLA do Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) para disponibilidade de VM. O Azure também fornece um SLA líder do setor para instâncias de VM individuais que usam discos do Armazenamento Premium.

toosafeguard cargas de trabalho de aplicativo de tempo de inatividade devido a indisponibilidade temporária de um disco ou a VM toohello, os clientes podem aproveitar [conjuntos de disponibilidade](../../virtual-machines/windows/manage-availability.md). Dois ou mais máquinas virtuais em um conjunto de disponibilidade fornece redundância para o aplicativo hello. Em seguida, o Azure cria essas VMs e esses discos em domínios de falha separados com diferentes componentes de energia, rede e servidor. Assim, falhas de hardware localizadas geralmente não afetam várias VMs em Olá definido no hello simultaneamente, fornecendo alta disponibilidade para seu aplicativo. Ele é considerado que uma disponibilidade de uma boa prática toouse define quando a alta disponibilidade é necessária. Para obter mais informações, consulte aspectos de recuperação de desastres Olá detalhados abaixo.

### <a name="backup-and-disaster-recovery"></a>Backup e recuperação de desastre

Recuperação de desastres (DR) é Olá toorecover de capacidade de incidentes raras mas principais: falhas não transitório, de larga escala, como interrupções de serviço que afeta toda a região. A recuperação de desastre inclui backup e arquivamento de dados e pode incluir a intervenção manual, como a restauração um banco de dados com base em um backup.

Hello a proteção interna da plataforma Azure contra falhas localizadas pode não proteger totalmente Olá VMs/discos no caso de saudação de grandes desastres que pode causar interrupções em larga escala. Isso inclui eventos catastróficos, como um data center atingido por um furacão, terremoto, incêndio ou falhas de unidade de hardware em grande escala. Além disso, você pode encontrar falhas devido a problemas de tooapplication ou dados.

toohelp proteger suas cargas de trabalho de IaaS de interrupções, você deve planejar a recuperação de tooenable redundância e backups. Recuperação de desastres, você deve planejar backup em um local geográfico diferente para fora do site primário hello e redundância. Isso ajuda a garantir que o backup não é afetado por Olá mesmo evento que originalmente afetados Olá VM ou os discos. Para obter mais informações, consulte [Recuperação de desastre para aplicativos criados no Azure](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications).

Suas considerações de recuperação de desastres podem incluir Olá aspectos a seguir:

1. Alta disponibilidade (HA) é a capacidade Olá Olá toocontinue de aplicativo em execução em um estado íntegro, sem tempo de inatividade significativo. Por "estado de integridade", queremos dizer aplicativo hello está respondendo, e os usuários podem conectar-se o aplicativo toohello e interagir com ele. Determinados aplicativos de missão crítica e bancos de dados podem ser necessário toobe disponível sempre, mesmo quando há falhas na plataforma de saudação. Para essas cargas de trabalho, talvez seja necessário tooplan redundância para o aplicativo hello, bem como dados de saudação.

2. Durabilidade de dados: Em alguns casos, consideração principal de saudação é garantir que dados saudação são preservados no caso de saudação de um desastre. Portanto, talvez seja necessário fazer um backup dos dados em outro site. Para essas cargas de trabalho, talvez não seja necessário redundância total para o aplicativo hello, mas um backup regular de discos de saudação.

## <a name="backup-and-dr-scenarios"></a>Cenários de backup e DR

Vamos examinar alguns exemplos comuns de cenários de carga de trabalho do aplicativo e considerações de saudação para o planejamento de recuperação de desastres.

### <a name="scenario-1-major-database-solutions"></a>Cenário 1: principais soluções de banco de dados

Considere um servidor de banco de dados de produção como o SQL Server ou o Oracle que pode dar suporte à Alta Disponibilidade. Usuários e aplicativos de produção críticos dependem desse banco de dados. plano de recuperação de desastres Olá para este sistema talvez seja necessário Olá toosupport requisitos a seguir:

1. Os dados devem ser protegidos e recuperáveis.
2.  O servidor deve estar disponível para uso.

Isso pode exigir a manutenção de uma réplica de banco de dados de saudação em uma região diferente, como um backup. Dependendo dos requisitos de saudação para recuperação de dados e a disponibilidade do servidor, a solução Olá poderia variar de um ativo ou ativo-passivo réplica site tooperiodic backups offline de dados de saudação. Bancos de dados relacionais, como o SQL Server e o Oracle, fornecem várias opções de replicação. Para o SQL Server, [Grupos de Disponibilidade AlwaysOn do SQL Server](https://msdn.microsoft.com/library/hh510230.aspx) podem ser usados para alta disponibilidade.

Bancos de dados NoSQL como o MongoDB também dão suporte a [réplicas](https://docs.mongodb.com/manual/replication/) para redundância. réplicas Olá para alta disponibilidade podem ser usadas.

### <a name="scenario-2-a-cluster-of-redundant-vms"></a>Cenário 2: um cluster de VMs redundantes

Considere uma carga de trabalho manipulada por um cluster de VMs que fornece redundância e balanceamento de carga. Um exemplo seria um cluster do Cassandra implantado em uma região. Esse tipo de arquitetura já fornece um alto nível de redundância nessa região. No entanto, tooprotect carga de trabalho de saudação de uma falha de nível regional, você deve considerar se espalhando cluster Olá em duas regiões ou tornar backups periódicos tooanother região.

### <a name="scenario-3-iaas-application-workload"></a>Cenário 3: carga de trabalho de aplicativos IaaS

Isso pode ser uma carga de trabalho de produção típica em execução em uma VM do Azure. Por exemplo, poderia ser um servidor web ou servidor de arquivo contém conteúdo hello e outros recursos de um site. Ele também pode ser um aplicativo de negócios personalizados executados em uma VM que armazenados seus dados, recursos e o estado do aplicativo em discos VM hello. Nesse caso, é importante toomake-se de que você faça backups regularmente. Frequência de backup deve ser baseada na natureza de saudação de carga de trabalho VM hello. Por exemplo, se o aplicativo hello é executada diariamente e modifica dados, em seguida, backup Olá cuidado a cada hora.

Outro exemplo é um servidor de relatórios que efetua pull de dados de outras fontes e gera relatórios agregados. Perda dessa VM ou discos levará toohello perda de saudação relatórios. No entanto, pode ser toorerun possíveis Olá relatórios de processo e a saída de hello regenerar. Nesse caso, você realmente não tem uma perda de dados, mesmo se o servidor de relatórios de saudação é atingido com um desastre, portanto você pode ter um nível mais alto de tolerância da perda de parte de dados Olá Olá reporting server. Nesse caso, menos frequentes backups é um custo de saudação tooreduce opção.

### <a name="scenario-4-iaas-application-data-issues"></a>Cenário 4: problemas de dados de aplicativos IaaS

Você tem um aplicativo que calcula, mantém e fornece dados comerciais críticos, como informações sobre preços. Uma nova versão do seu aplicativo tinha um bug do software que incorretamente computada Olá preços e Olá existente commerce dados servidos por plataforma Olá corrompidos. Aqui, melhor o curso de ação Olá seria toorevert toohello versão anterior do aplicativo hello e dados saudação primeiro. tooenable, backups periódicos de tirar do seu sistema.

## <a name="disaster-recovery-solution-azure-backup-service"></a>Solução de Recuperação de Desastre: Serviço de Backup do Azure

O [Serviço de Backup do Azure](https://azure.microsoft.com/services/backup/) pode ser usado para Backup e DR e funciona com [Managed Disks](../../virtual-machines/windows/managed-disks-overview.md), bem como com [Discos Não Gerenciados](../../virtual-machines/windows/about-disks-and-vhds.md#unmanaged-disks). Crie um trabalho de backup com backups baseados em tempo, fácil restauração de VM e políticas de retenção de backup. 

Se você usar [discos de armazenamento Premium](storage-premium-storage.md), [discos gerenciados](../../virtual-machines/windows/managed-disks-overview.md), ou outros tipos de disco com hello [armazenamento localmente redundante (LRS)](storage-redundancy.md#locally-redundant-storage) opção é especialmente importante tooleverage backups periódicos de recuperação de desastres. Backup do Azure armazena dados saudação em seu Cofre de serviços de recuperação para retenção de longo prazo. Escolha Olá [armazenamento com redundância geográfica (GRS)](storage-redundancy.md#geo-redundant-storage) opção Olá serviços de recuperação de Backup do cofre. Isso vai garantir que os backups são replicados tooa outra região do Azure para proteger contra desastres regionais.

Para [discos não gerenciado](../../virtual-machines/windows/about-disks-and-vhds.md#unmanaged-disks), você pode usar o tipo de armazenamento LRS Olá para discos de IaaS, mas certifique-se de que o Backup do Azure está habilitado com hello opção GRS Olá Cofre de serviços de recuperação.

**Se você usar o hello [GRS](storage-redundancy.md#geo-redundant-storage)/[RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage) opção para os discos não gerenciado, você ainda precisa de instantâneos consistentes para Backup e recuperação de desastres.** Use o [Serviço de Backup do Azure](https://azure.microsoft.com/services/backup/) ou [instantâneos consistentes](#alternative-solution-consistent-snapshots).

a seguir Olá é um resumo das soluções para recuperação de desastres.

| Cenário | Replicação automática | Solução de DR |
| --- | --- | --- |
| *Discos do Armazenamento Premium* | Local ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Serviço de Backup do Azure](https://azure.microsoft.com/services/backup/) |
| *Managed Disks* | Local ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Serviço de Backup do Azure](https://azure.microsoft.com/services/backup/) |
| *Discos LRS Não Gerenciados* | Local ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Serviço de Backup do Azure](https://azure.microsoft.com/services/backup/) |
| *Discos GRS Não Gerenciados* | Várias regiões ([GRS](storage-redundancy.md#geo-redundant-storage)) | [Serviço de Backup do Azure](https://azure.microsoft.com/services/backup/)<br/>[Instantâneos consistentes](#alternative-solution-consistent-snapshots) |
| *Discos RA-GRS Não Gerenciados* | Várias regiões ([RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage)) | [Serviço de Backup do Azure](https://azure.microsoft.com/services/backup/)<br/>[Instantâneos consistentes](#alternative-solution-consistent-snapshots) |

Alta disponibilidade por melhor pode atendido por meio do uso de saudação de discos gerenciado em um conjunto de disponibilidade junto com o Backup do Azure. Se você estiver usando Discos Não Gerenciados, ainda poderá usar o Backup do Azure para DR. Se você não é possível toouse Backup do Azure, tirar [instantâneos consistentes](#alternative-solution-consistent-snapshots) conforme descrito em uma seção posterior é uma solução alternativa para Backup e recuperação de desastres.

Suas escolhas de alta disponibilidade, backup e DR nos níveis do Aplicativo ou da Infraestrutura podem ser representadas conforme mostrado abaixo:

| *Level* | Alta disponibilidade   | Backup/DR |
| --- | --- | --- |
| *Aplicativo* | SQL AlwaysOn | Serviço de Backup do Azure |
| *Infraestrutura*  | Conjunto de disponibilidade  | GRS com instantâneos consistentes |

### <a name="using-hello-azure-backup-service"></a>Usando hello Azure Backup Service

[O Backup do Azure](../../backup/backup-azure-vms-introduction.md) pode fazer backup de suas VMs executando o Windows ou Linux toohello Cofre de serviços de recuperação do Azure. Fazendo backup e restaurando dados críticos de negócios é complicada pelo fato de saudação dados críticos de negócios devem ser feitos enquanto os aplicativos de saudação que produzem Olá dados estão em execução. tooaddress, Backup do Azure fornece backups consistentes com o aplicativo para cargas de trabalho da Microsoft usando tooensure de serviço de sombra de Volume (VSS) do hello que dados sejam gravados corretamente toostorage. Para VMs do Linux, apenas os backups consistentes de arquivos são possíveis, como Linux não tem tooVSS de funcionalidade equivalente.

![](./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-1.png)   

Quando o Backup do Azure inicia um trabalho de backup no tempo de saudação agendado, ela aciona extensão de backup Olá instalado na VM tootake um instantâneo point-in-time de saudação. Um instantâneo é tirado em coordenação com VSS tooget um instantâneo consistente de discos Olá na máquina virtual de saudação sem ter que tooshut-para baixo. extensão de backup Olá no hello VM libera todas as gravações antes de tirar um instantâneo consistente de saudação de todos os discos de saudação. Depois de saudação instantâneo é tirado, dados de saudação são transferidos por Cofre de backup do Azure Backup toohello. toomake Olá processo de backup mais eficiente, serviço Olá identifica e transfere apenas os blocos de dados que foram alterados desde o último backup de Olá Olá.


toorestore, você pode exibir os backups disponíveis por meio do Backup do Azure hello e, em seguida, inicie uma restauração. Você pode criar e restaurar backups do Azure por meio de saudação [portal do Azure](https://portal.azure.com/), [usando o PowerShell](../../backup/backup-azure-vms-automation.md ), ou usando Olá [CLI do Azure](https://docs.microsoft.com/azure/xplat-cli-install). Para obter mais informações, consulte Backup do Azure.

### <a name="steps-tooenable-backup"></a>Etapas tooEnable Backup

Olá, etapas a seguir são tooenable geralmente usados backups de suas VMs usando Olá [Portal do Azure](https://portal.azure.com/). Haverá algumas variações dependendo do cenário exato. Consulte toohello [Backup do Azure](../../backup/backup-azure-vms-introduction.md) documentação para obter detalhes completos. O Backup do Azure também [dá suporte a VMs com o Managed Disks](https://azure.microsoft.com/blog/azure-managed-disk-backup/).

1.  Crie um cofre de serviços de recuperação para uma VM usando Olá etapas a seguir:

    a.  Usando Olá [portal do Azure](https://portal.azure.com/), procurar todos os recursos e localizar "Cofres de serviços de recuperação".

    b.  Em Olá menu os cofres de serviços de recuperação, clique em Adicionar e siga Olá etapas toocreate um novo cofre em Olá Olá VM mesma região. Por exemplo, se a VM estiver na região Oeste dos EUA, escolha Oeste dos EUA para o cofre hello.

2.  Verifique se a replicação de armazenamento Olá para Olá recém-criado cofre. toodo, acesso Olá Cofre de saudação dos serviços de recuperação cofres folha e ir toohello configurações/Backup configuração. Certifique-se de saudação opção GRS é selecionada por padrão. Isso irá garantir que seu cofre é automaticamente replicados tooa data center secundário. Por exemplo, o cofre no Oeste dos EUA será replicada automaticamente tooEast dos EUA.

3.  Configurar a política de backup hello e selecione Olá VM da saudação mesma interface do usuário.

4.  Verifique se Olá que backup Agent está instalado na VM de saudação. Se a VM é criada usando uma imagem da Galeria do Azure, o agente de Backup Olá já está instalado. Caso contrário (ou seja, se você estiver usando uma imagem personalizada), use instruções muito[Olá instalar agente de VM na máquina virtual de saudação](../../backup/backup-azure-arm-vms-prepare.md#install-the-vm-agent-on-the-virtual-machine).

5.  Certifique-se de que Olá VM permite que a conectividade de rede para Olá toofunction de serviço de backup. Siga estas instruções para a [Conectividade de rede](../../backup/backup-azure-arm-vms-prepare.md#network-connectivity).

6.  Depois que Olá acima etapas forem concluídas, o backup de Olá será executado em intervalos regulares, conforme especificado na política de backup hello. Se necessário, você pode disparar o primeiro backup Olá manualmente do painel do cofre Olá em Olá portal do Azure.

Para automatizar o Backup do Azure usando scripts, consulte muito[cmdlets do PowerShell para backup de VM](../../backup/backup-azure-vms-automation.md).

### <a name="steps-for-recovery"></a>Etapas de recuperação

Se você precisa toorepair ou recriar uma VM, você pode restaurar Olá VM de qualquer um dos pontos de recuperação de backup Olá no cofre hello. Há duas opções diferentes para executar recuperação hello:

1.  Você pode criar uma nova VM como uma representação pontual da VM copiada em backup.

2.  Você pode restaurar Olá discos e, em seguida, use o modelo de saudação para Olá VM toocustomize e Olá de reconstrução restaurado VM. 

Consulte as instruções muito[máquinas de virtuais do Azure Use toorestore portal](../../backup/backup-azure-arm-restore-vms.md#restoring-a-vm-during-azure-datacenter-disaster). documento Hello também explica as etapas específicas de Olá para restaurar o backup VMs toohello emparelhados data center usando o Cofre de backup com redundância geográfica no caso de saudação de um desastre no Centro de dados primário hello. Nesse caso, o Backup do Azure usa o serviço de computação de saudação da máquina virtual do hello região secundária toocreate Olá restaurado.

Use também o PowerShell para [restaurar uma VM](../../backup/backup-azure-vms-automation.md#restore-an-azure-vm) ou [criar uma nova VM com base em discos restaurados](../../backup/backup-azure-vms-automation.md#create-a-vm-from-restored-disks).

## <a name="alternative-solution-consistent-snapshots"></a>Solução alternativa: instantâneos consistentes

Se você não é possível toouse Olá serviço Backup do Azure, você pode implementar seu próprio mecanismo de backup usando os instantâneos. É complicado toocreate instantâneos consistentes para todos os discos usados por uma máquina virtual e, em seguida, replicar esses região tooanother de instantâneos. Por esse motivo, o Azure considera Olá aproveitando o serviço de Backup uma opção melhor do que a criação de uma solução personalizada. Se você usar o armazenamento de RA-GRS/GRS para discos, os instantâneos são replicados automaticamente tooa data center secundário. Se você usar o armazenamento LRS para discos, você precisará tooreplicate Olá dados por conta própria. Para obter mais informações, consulte [Fazer backup de discos não gerenciados de VM do Azure com instantâneos incrementais](../../virtual-machines/windows/incremental-snapshots.md).

Um instantâneo é uma representação de um objeto em um ponto específico no tempo. Um instantâneo incorrerá em cobrança para tamanho de Olá incremental de dados Olá ele mantém. Para obter mais informações, consulte [Criar um instantâneo de blob](../blobs/storage-blob-snapshots.md).

### <a name="creating-snapshots-while-hello-vm-is-running"></a>Criação de instantâneos durante a saudação VM está em execução

Enquanto você pode fazer um instantâneo a qualquer momento, se hello VM estiver em execução, ainda está sendo transmitidos toohello discos de dados e instantâneos Olá podem conter operações parciais que estavam em trânsito. Além disso, se houver vários discos envolvidos, instantâneos de saudação de discos diferentes podem ter ocorrido em momentos diferentes, que significa que esses instantâneos podem não ser coordenados. Isso é especialmente problemático para volumes distribuídos cujos arquivos podem ser corrompidos se alterações estavam sendo feitas durante o backup.

tooavoid nessa situação, o processo de backup Olá deve implementar Olá etapas a seguir:

1.  Congelar todos os discos de saudação

2.  Liberar Olá todas as gravações pendentes

3.  Em seguida, [criar um instantâneo de blob](../blobs/storage-blob-snapshots.md) para todos os discos de Olá

Alguns aplicativos do Windows como o SQL Server fornecem um mecanismo de backup coordenado por meio de backups consistentes com aplicativos do VSS toocreate. No Linux, você pode usar uma ferramenta como fsfreeze para coordenar discos hello, que fornecerão backups consistentes de arquivos, mas não consistentes com aplicativos instantâneos. Esse processo é complicado; portanto, considere o uso de [Backup do Azure](../../backup/backup-azure-vms-introduction.md) ou de uma solução de backup de terceiros que já implementa isso.

Olá acima processo resulta em uma coleção de instantâneos coordenados para todos os discos VM hello, representando uma exibição point-in-time específica de saudação VM. Isso é um ponto de restauração de backup para Olá VM. Você pode repetir o processo de saudação em backups periódicos do toocreate intervalos agendados. Consulte abaixo para obter as etapas Olá muito[região do cópia Olá backups tooanother](#copy-the-snapshots-to-another-region) para recuperação de desastres.

### <a name="creating-snapshots-while-hello-vm-is-offline"></a>Criação de instantâneos durante a saudação a VM está offline

Backups consistentes do outra opção toocreate está sendo desligado hello VM e obter blob instantâneos de cada disco. Isso é mais fácil do que coordenar instantâneos de uma VM em execução, mas exige alguns minutos de inatividade. Para esse processo, siga estas etapas:

1. Desligar Olá VM.

2. Crie um instantâneo de cada blob do VHD, o que leva apenas alguns segundos.

    toocreate um instantâneo, você pode usar [PowerShell](storage-powershell-guide-full.md#how-to-manage-azure-blob-snapshots), Olá [API de Rest do armazenamento do Azure](https://msdn.microsoft.com/library/azure/ee691971.aspx), [CLI do Azure](https://docs.microsoft.com/azure/xplat-cli-install), ou uma saudação bibliotecas de cliente de armazenamento do Azure, como [ biblioteca de cliente de armazenamento Olá para .NET](https://msdn.microsoft.com/library/azure/hh488361.aspx).

3. Olá iniciar VM, que termina o tempo de inatividade de saudação. Normalmente, todo o processo de saudação é concluída em alguns minutos.

Esse processo resulta em uma coleção de instantâneos consistentes para todos os discos hello, fornecendo um ponto de restauração de backup para Olá VM. Consulte abaixo para região tooanother instantâneos de saudação do hello etapas toocopy para recuperação de desastres.

### <a name="copy-hello-snapshots-tooanother-region"></a>Região de tooanother cópia Olá instantâneos

Criação de instantâneos de saudação somente pode não ser suficiente para recuperação de desastres. Região de tooanother de backups de instantâneo Olá também devem ser replicados.

Se você estiver usando o GRS ou RA-GRS para os discos, instantâneos de saudação são região secundária toohello replicados automaticamente. Pode haver alguns minutos de retardo antes da replicação hello e se Olá data center primário ficar inativo antes de instantâneos Olá concluir a replicação, você não poderá ser tooaccess capaz de instantâneos de saudação do hello data center secundário. probabilidade de saudação deste é pequena.

> [!Note] 
> Tendo apenas discos de saudação em uma conta GRS ou RA-GRS não protege Olá VM de desastres. Também é necessário criar instantâneos coordenados ou usar o Backup do Azure. Isso é necessário toorecover um estado consistente de tooa VM.

Se você estiver usando LRS, você deve copiar Olá instantâneos tooa outra conta de armazenamento imediatamente após a criação do instantâneo de saudação. o destino de cópia Olá pode ser uma conta de armazenamento LRS em uma região diferente, resultando na cópia de saudação em uma região remota. Você também pode copiar a conta de armazenamento Olá instantâneo tooan RA-GRS em Olá mesma região. Nesse caso, instantâneo Olá será região secundária do remoto toohello lentamente replicado. O backup é protegido após um desastre no site primário hello quando Olá cópia e replicação for concluída.

toocopy seus instantâneos incrementais para recuperação de desastres com eficiência, examine instruções Olá [backup de discos VM não gerenciados do Azure com instantâneos incrementais](../../virtual-machines/windows/incremental-snapshots.md).

![](./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-2.png)   

### <a name="recovery-from-snapshots"></a>Recuperação com base em instantâneos

tooretrieve um instantâneo, copie-o toomake um novo blob. Se você estiver copiando instantâneo Olá da conta primária hello, você pode copiar Olá instantâneo sobre toohello blob de base de instantâneo hello, assim, revertendo Olá disco toohello instantâneo; Isso é conhecido como promover um instantâneo de saudação. Se você estiver copiando o backup de instantâneo de saudação de uma conta secundária (no caso de saudação de RA-GRS), ele deve ser copiado tooa primário da conta. Você pode copiar um instantâneo [usando o PowerShell](storage-powershell-guide-full.md#how-to-copy-a-snapshot-of-a-blob) ou usando o utilitário AzCopy de saudação. Para obter mais informações, consulte [transferir dados com o utilitário de linha de comando AzCopy de hello](storage-use-azcopy.md).

No caso de saudação de VMs com vários discos, você deve copiar todos os instantâneos Olá que fazem parte da saudação mesmas coordenadas de ponto de restauração. Quando você copia Olá instantâneos toowritable VHD blobs, você pode usar Olá blobs toorecreate sua VM usando o modelo de saudação para Olá VM.

## <a name="other-options"></a>Outras opções

### <a name="sql-server"></a>SQL Server

SQL Server em execução em uma VM tem seu próprio toobackup recursos internos seu tooAzure de banco de dados do SQL Server o armazenamento de Blob ou em um compartilhamento de arquivo. Se a conta de armazenamento de saudação é GRS ou RA-GRS, você pode acessar esses backups no Centro de dados secundários da conta de armazenamento Olá no evento de saudação de um desastre, com hello mesmas restrições, como discutido anteriormente. Para obter mais informações, consulte [Backup e Restauração para SQL Server em Máquinas Virtuais do Azure](../../virtual-machines/windows/sql/virtual-machines-windows-sql-backup-recovery.md). Em adição toobackup e restauração, [SQL Server AlwaysOn em grupos de disponibilidade](../../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md) pode manter réplicas secundárias de bancos de dados toogreatly reduzem o tempo de recuperação de desastres de saudação.

## <a name="other-considerations"></a>Outras considerações

Este artigo discutiu como toobackup ou tirar instantâneos de suas VMs e recuperação de desastres do toosupport seus discos e como toouse esses toorecover. Com o modelo do Azure Resource Manager hello, muitas pessoas usam modelos toocreate suas VMs e outra infraestrutura no Azure. Você pode usar um modelo toocreate uma VM que tenha Olá mesma configuração de cada vez. Se você usar imagens personalizadas para criar suas VMs, você também deve verificar se as imagens são protegidas usando um toostore de conta de RA-GRS-los.

Consequentemente, o processo de backup pode ser uma combinação de duas coisas:

1. Dados de backup de saudação (discos)
2. Configuração de backup hello (modelos, imagens personalizadas)

Dependendo da opção de backup Olá que você escolher, você pode ter backup Olá toohandle dados saudação e configuração de saudação ou serviço de backup Olá pode lidar com tudo isso para você.

## <a name="appendix---understanding-hello-impact-of-lrs-grs-and-ra-grs"></a>Apêndice a-Noções básicas sobre o impacto de saudação do LRS, GRS e RA-GRS

Para contas de armazenamento no Azure, há três tipos de redundância de dados que devem ser considerados em relação à recuperação de desastre – LRS (redundância local), GRS (redundância geográfica) ou RA-GRS (redundância geográfica com acesso de leitura). 

Localmente o armazenamento redundante (LRS) mantém três cópias de dados Olá Olá mesmo data center. Ao gravar dados hello, todos os três cópias são atualizadas antes do sucesso será retornado toohello chamador, para que você saiba que eles são idênticos. O disco está protegido contra falhas locais, pois é muito improvável que todos os três cópias seriam afetadas em Olá simultaneamente. No caso de saudação de LRS, não há nenhuma redundância geográfica e disco Olá não está protegido contra falhas catastróficas que podem afetar uma unidade de todo o data center ou armazenamento.

Com o GRS e RA-GRS, três cópias de seus dados são mantidas na região primária do hello (selecionado por você) e três cópias mais de seus dados são mantidas em uma região secundária correspondente (definida pelo Azure). Por exemplo, se você armazenar dados no Oeste dos EUA, dados de saudação serão replicada tooEast dos EUA. Isso é feito de forma assíncrona, e há um pequeno atraso entre as atualizações toohello primário e secundário. Réplicas de discos Olá no site secundário Olá estão consistentes em uma base por disco (com atraso Olá), mas réplicas de vários discos ativos podem não estar sincronizadas **uns com os outros**. réplicas consistente em vários discos, instantâneos consistentes de toohave são necessários.

Olá principal diferença entre GRS e RA-GRS é que, com RA-GRS, você pode ler cópia secundária Olá a qualquer momento. Se houver um problema que processa os dados de saudação na região primária Olá inacessível, Olá, equipe do Azure tornará cada acesso toorestore de esforço. Enquanto Olá primário estiver inativo, se você tiver RA-GRS habilitado, você pode acessar dados Olá Olá data center secundário. Portanto, se você planejar tooread da réplica Olá enquanto Olá primário estiver inacessível, em seguida, RA-GRS deve ser considerada.

Se acontece toobe uma interrupção significativa Olá, equipe do Azure pode disparar um failover geográfico e altere o armazenamento Olá primário DNS entradas toopoint toosecondary. Neste ponto, se você tiver o GRS ou RA-GRS habilitado, você pode acessar dados de saudação na região Olá usados toobe Olá secundário. Em outras palavras, se sua conta de armazenamento é GRS e há um problema, você pode acessar o armazenamento secundário Olá somente se houver um failover geográfico.

Para obter mais informações, consulte [que toodo se ocorrer uma interrupção de armazenamento do Azure](storage-disaster-recovery-guidance.md). 

Observe que a Microsoft controla a ocorrência de um failover. O failover não é controlado por conta de armazenamento e, portanto, isso não é decidido por clientes individuais. tooimplement a recuperação de desastres para contas de armazenamento específico ou discos de máquina virtual, você deve usar técnicas de saudação descritas anteriormente neste artigo.
