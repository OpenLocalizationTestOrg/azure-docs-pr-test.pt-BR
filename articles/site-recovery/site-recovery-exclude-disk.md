---
title: "discos aaaExclude de proteção usando o Azure Site Recovery | Microsoft Docs"
description: "Descreve por que e como tooexclude VM discos de replicação para cenários de VMware tooAzure e tooAzure do Hyper-V."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: f47146bc57aeab3fce90123d0894fa86dde93417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="exclude-disks-from-replication"></a>Excluir discos da replicação
Este artigo descreve como tooexclude discos de replicação. Essa exclusão pode otimizar a largura de banda de replicação Olá consumido ou otimizar os recursos de destino Olá que utilizam esses discos. recurso de saudação tem suporte para cenários de VMware tooAzure e tooAzure do Hyper-V.

## <a name="prerequisites"></a>Pré-requisitos

Por padrão, todos os discos em um computador são replicados. tooexclude um disco de replicação, instale manualmente Olá serviço de mobilidade no computador de saudação antes de habilitar a replicação se você estiver replicando de tooAzure do VMware.


## <a name="why-exclude-disks-from-replication"></a>Por que excluir discos da replicação?
Excluir discos da replicação geralmente é necessário porque:

- dados de saudação é formados no disco Olá excluído não é importantes ou não necessário toobe replicada.

- Você deseja que os recursos de armazenamento e rede toosave não replicando essa variação.

## <a name="what-are-hello-typical-scenarios"></a>Quais são os cenários típicos Olá?
Você pode identificar exemplos específicos de variação de dados que são bons candidatos para exclusão. Os exemplos podem incluir grava o arquivo de paginação tooa (pagefile.sys) e grava arquivos de tempdb toohello do Microsoft SQL Server. Dependendo da carga de trabalho de saudação e o subsistema de armazenamento hello, arquivo de paginação Olá pode registrar uma quantidade significativa de variação. No entanto, replicando dados de saudação site primário tooAzure seria usar muitos recursos. Assim, você pode usar o hello a replicação de uma máquina virtual com um único disco virtual que tenha o sistema operacional de saudação e o arquivo de paginação Olá toooptimize as etapas a seguir:

1. Dividir o disco virtual Olá em dois discos virtuais. Um disco virtual tem o sistema operacional de saudação e Olá outros tem o arquivo de paginação de saudação.
2. Exclua o disco do arquivo de paginação de saudação da replicação.

Da mesma forma, você pode usar o hello seguindo as etapas toooptimize um disco que tem dois tempdb do Microsoft SQL Server Olá CAM e Olá o arquivo de banco de dados do sistema:

1. Manter o banco de dados de sistema hello e tempdb em discos diferentes dos dois.
2. Exclua o disco de tempdb Olá da replicação.

## <a name="how-tooexclude-disks-from-replication"></a>Como tooexclude discos de replicação?

### <a name="vmware-tooazure"></a>VMware tooAzure
Siga Olá [habilitar replicação](site-recovery-vmware-to-azure.md) tooprotect de fluxo de trabalho uma máquina virtual do portal do Azure Site Recovery hello. Na quarta etapa do fluxo de trabalho Olá Olá, use Olá **tooREPLICATE disco** discos de tooexclude de coluna da replicação. Por padrão, todos os discos são selecionados para replicação. Desmarque a caixa de seleção de saudação de discos que você deseja tooexclude de replicação e hello, em seguida, concluir etapas tooenable.

![Excluir discos de replicação e habilitar a replicação para VMware tooAzure failback](./media/site-recovery-exclude-disk/v2a-enable-replication-exclude-disk1.png)


>[!NOTE]
>
> * Você pode excluir somente os discos que já têm o serviço de mobilidade Olá instalado. Será necessário toomanually instalação do serviço de mobilidade hello, pois Olá serviço de mobilidade só é instalado usando o mecanismo de envio de saudação depois que a replicação está habilitada.
> * Apenas discos básicos podem ser excluídos da replicação. Você não pode excluir o sistema operacional ou discos dinâmicos.
> * Depois de habilitar a replicação, você não pode adicionar ou remover discos para replicação. Se você quiser tooadd ou excluir um disco, você precisa toodisable proteção da máquina de saudação e habilite-a novamente.
> * Se você excluir um disco que é necessário para um aplicativo toooperate, após o failover tooAzure, você precisará disco de saudação toocreate manualmente no Azure para que possa executar aplicativo hello replicada. Como alternativa, você pode integrar a automação do Azure em um disco de saudação de toocreate de plano de recuperação durante o failover da máquina de saudação.
> * Máquina virtual de janela: discos que você cria manualmente no Azure não são submetidos a failback. Por exemplo, se você executar failover de três discos e criar dois diretamente em VMs do Azure, apenas os três discos com failover serão enviados por failback. Você não pode incluir discos que você criou manualmente no failback ou em nova proteção de tooAzure local.
> * Máquina virtual Linux: discos que você cria manualmente no Azure são submetidos a failback. Por exemplo, se você executar o failover em três discos e criar dois discos diretamente em máquinas virtuais do Azure, todos os cinco serão submetidos a failback. Você não pode excluir do failback discos que foram criados manualmente.
>

### <a name="hyper-v-tooazure"></a>TooAzure Hyper-V
Siga Olá [habilitar replicação](site-recovery-hyper-v-site-to-azure.md) tooprotect de fluxo de trabalho uma máquina virtual do portal do Azure Site Recovery hello. Na quarta etapa do fluxo de trabalho Olá Olá, use Olá **tooREPLICATE disco** discos de tooexclude de coluna da replicação. Por padrão, todos os discos são selecionados para replicação. Desmarque a caixa de seleção de saudação de discos que você deseja tooexclude de replicação e hello, em seguida, concluir etapas tooenable.

![Excluir discos de replicação e habilitar a replicação para failback de tooAzure do Hyper-V](./media/site-recovery-vmm-to-azure/enable-replication6-with-exclude-disk.png)

>[!NOTE]
>
> * Você pode excluir somente os discos básicos da replicação. Você não pode excluir os discos do sistema operacional. É recomendável que você não exclua discos dinâmicos. O Azure Site Recovery não é possível identificar o disco rígido virtual (VHD) é básico ou dinâmico na máquina de virtual do convidado hello.  Se todos os discos de volume dinâmico dependentes não são excluídos, Olá protegido dinâmico disco torna-se um disco com falha em uma máquina virtual de failover e hello os dados no disco não estão acessíveis.
> * Depois de habilitar a replicação, você não pode adicionar ou remover discos para replicação. Se você quiser tooadd ou excluir um disco, você precisa toodisable proteção para a máquina virtual de saudação e habilite-a novamente.
> * Se você excluir um disco que é necessário para um aplicativo toooperate, após o failover tooAzure você precisará toocreate Olá disco manualmente no Azure para que possa executar aplicativo hello replicada. Como alternativa, você pode integrar a automação do Azure em um disco de saudação de toocreate de plano de recuperação durante o failover da máquina de saudação.
> * Não haverá failback de discos que você criar manualmente no Azure. Por exemplo, se você falha em três discos e cria dois discos diretamente em máquinas virtuais do Azure, somente três discos que foram failover realizarão da tooHyper-V do Azure. Você não pode incluir discos que foram criados manualmente no failback ou na replicação inversa do Hyper-V tooAzure.



## <a name="end-to-end-scenarios-of-exclude-disks"></a>Cenários de ponta a ponta para exclusão de discos
Vamos considerar o recurso de disco de dois cenários toounderstand Olá exclusão:

- Disco tempdb do SQL Server
- Disco (pagefile.sys) de arquivo de paginação

### <a name="exclude-hello-sql-server-tempdb-disk"></a>Excluir o disco de tempdb do SQL Server Olá
Vamos considerar uma máquina virtual do SQL Server que tenha um tempdb que possa ser excluído.

nome de saudação do disco virtual Olá é SalesDB.

Discos na máquina de virtual de origem Olá são da seguinte maneira:


**Nome do disco** | **Sistema operacional convidado - disco nº** | **Letra da unidade** | **Tipo de dados em disco Olá**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Disco do sistema operacional
DB-Disk1| Disk1 | D:\ | Banco de dados do sistema SQL e User Database1
Disco com o banco de dados 2 (disco de saudação excluídas da proteção) | Disk2 | E:\ | Arquivos temporários
Banco de dados-Disk3 (disco de saudação excluídas da proteção) | Disk3 | F:\ | Banco de dados tempdb do SQL (caminho de pasta (F:\MSSQL\Data\) </br/>< / br/> Anote o caminho da pasta Olá antes do failover.
DB-Disk4 | Disk4 |G:\ |User Database2

Como a rotatividade de dados em dois discos da máquina virtual de saudação é temporária, enquanto você protege Olá SalesDB virtual machine, exclua o disco 2 e Disk3 da replicação. O Azure Site Recovery não replicará esses discos. Durante um failover, os discos não estarão presentes na máquina de virtual Olá failover no Azure.

Discos na máquina virtual do Azure após o failover de saudação são da seguinte maneira:

**Sistema operacional convidado - disco nº** | **Letra da unidade** | **Tipo de dados em disco Olá**
--- | --- | ---
DISK0 | C:\ | Disco do sistema operacional
Disk1 | E:\ | Armazenamento temporário </br / >< / br / > Azure adiciona esse disco e atribui a primeira letra de unidade disponível hello.
Disk2 | D:\ | Banco de dados do sistema SQL e User Database1
Disk3 | G:\ | User Database2

Porque o disco 2 e Disk3 foram excluídos da máquina de virtual SalesDB Olá, e é primeira letra de unidade Olá da lista disponível hello. Azure atribui o volume de armazenamento temporário de toohello e:. Para todos os discos de saudação replicado, permanecem letras de unidade de Olá Olá mesmo.

Disk3, que era o disco de tempdb do SQL hello (caminho de pasta de tempdb F:\MSSQL\Data\), foi excluído da replicação. Olá disco não está disponível na máquina de virtual Olá failover. Como resultado, Olá serviço do SQL está em um estado parado e é necessário que o caminho de F:\MSSQL\Data hello.

Há dois toocreate de maneiras esse caminho:

- Adicione um novo disco e atribua o caminho da pasta tempdb.
- Use um disco de armazenamento temporário existente para o caminho da pasta Olá tempdb.

#### <a name="add-a-new-disk"></a>Adicione um novo disco:

1. Anote os caminhos de saudação do SQL tempdb.mdf e tempdb.ldf antes do failover.
2. De Olá portal do Azure, adicione uma novo disco toohello failover máquina virtual com hello mais tamanho igual ou do disco de tempdb Olá origem SQL (Disk3).
3. Entrar toohello máquina virtual do Azure. No console de gerenciamento (diskmgmt.msc) de disco hello, inicializar e formatar Olá recém-adicionado disco.
4. Olá atribuir mesma unidade que foi usado por disco de tempdb Olá SQL (f).
5. Crie uma pasta de tempdb no hello volume f: (F:\MSSQL\Data).
6. Inicie serviço SQL de saudação do console de serviço Olá.

#### <a name="use-an-existing-temporary-storage-disk-for-hello-sql-tempdb-folder-path"></a>Use um disco de armazenamento temporário existente para o caminho da pasta Olá SQL tempdb:

1. Abra um prompt de comando.
2. Execute o SQL Server no modo de recuperação do prompt de comando de saudação.

        Net start MSSQLSERVER /f / T3608

3. Execute Olá sqlcmd toochange Olá tempdb toohello novo caminho a seguir.

        sqlcmd -A -S SalesDB        **Use your SQL DBname**
        USE master;     
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = tempdev, FILENAME = 'E:\MSSQL\tempdata\tempdb.mdf');
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = templog, FILENAME = 'E:\MSSQL\tempdata\templog.ldf');       
        GO


4. Pare o serviço do Microsoft SQL Server hello.

        Net stop MSSQLSERVER
5. Inicie o serviço do Microsoft SQL Server hello.

        Net start MSSQLSERVER

Consulte toohello seguindo a orientação do Azure para o disco de armazenamento temporário:

* [Usando SSDs em VMs do Azure toostore TempDB do SQL Server e extensões do Pool de Buffer](https://blogs.technet.microsoft.com/dataplatforminsider/2014/09/25/using-ssds-in-azure-vms-to-store-sql-server-tempdb-and-buffer-pool-extensions/)
* [Práticas recomendadas para o SQL Server em Máquinas Virtuais do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance)

### <a name="failback-from-azure-tooan-on-premises-host"></a>Failback (a partir do host do Azure tooan local)
Agora vamos entender discos Olá duplicados quando houver falha do host de Hyper-V ou VMware local tooyour do Azure. Os discos criados manualmente no Azure não serão replicados. Por exemplo, se você executar failover de três discos e criar dois diretamente na VM do Azure, apenas os três discos com failover serão enviados por failback. Você não pode incluir discos que foram criados manualmente no failback ou em nova proteção de tooAzure local. Ele também não replicará os hosts de tooon local Olá armazenamento temporário em disco.

#### <a name="failback-toooriginal-location-recovery"></a>Recuperação em local toooriginal failback

No exemplo anterior de saudação, configuração de disco de máquina virtual do Azure Olá é o seguinte:

**Sistema operacional convidado - disco nº** | **Letra da unidade** | **Tipo de dados em disco Olá**
--- | --- | ---
DISK0 | C:\ | Disco do sistema operacional
Disk1 | E:\ | Armazenamento temporário </br / >< / br / > Azure adiciona esse disco e atribui a primeira letra de unidade disponível hello.
Disk2 | D:\ | Banco de dados do sistema SQL e User Database1
Disk3 | G:\ | User Database2


#### <a name="vmware-tooazure"></a>VMware tooAzure
Quando o failback é feito o local original toohello, configuração de disco de máquina virtual de failback Olá não tem discos excluídos. Os discos que foram excluídos do VMware tooAzure não estará disponíveis na máquina de virtual Olá failback.

Após o failover planejado do Azure local tooon VMware, discos na máquina virtual da VMWare hello (local original) são:

**Sistema operacional convidado - disco nº** | **Letra da unidade** | **Tipo de dados em disco Olá**
--- | --- | ---
DISK0 | C:\ | Disco do sistema operacional
Disk1 | D:\ | Banco de dados do sistema SQL e User Database1
Disk2 | G:\ | User Database2

#### <a name="hyper-v-tooazure"></a>TooAzure Hyper-V
Quando o failback local original toohello, Olá failback máquina virtual em disco configuração permanece Olá mesmo que da configuração original de disco de máquina virtual do Hyper-V. Discos que foram excluídos do Hyper-V site tooAzure estão disponíveis na máquina de virtual Olá failback.

Após o failover planejado do Azure local tooon Hyper-V, discos na máquina virtual de Hyper-V hello (local original) são:

**Nome do Disco** | **Sistema operacional convidado - disco nº** | **Letra da unidade** | **Tipo de dados em disco Olá**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 |   C:\ | Disco do sistema operacional
DB-Disk1 | Disk1 | D:\ | Banco de dados do sistema SQL e User Database1
DB-disco 2 (disco excluídos) | Disk2 | E:\ | Arquivos temporários
DB-Disk3 (disco excluídos) | Disk3 | F:\ | Banco de dados do tempdb do SQL (caminho da pasta (F:\MSSQL\Data\)
DB-Disk4 | Disk4 | G:\ | User Database2


#### <a name="exclude-hello-paging-file-pagefilesys-disk"></a>Excluir o disco de arquivo (pagefile.sys) de paginação Olá

Vamos considerar uma máquina virtual que tem um disco de arquivo de paginação que pode ser excluído.
Existem dois casos.

#### <a name="case-1-hello-paging-file-is-configured-on-hello-d-drive"></a>Caso 1: o arquivo de paginação hello está configurado no hello unidade d:
Aqui está a configuração de disco hello:


**Nome do disco** | **Sistema operacional convidado - disco nº** | **Letra da unidade** | **Tipo de dados em disco Olá**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Disco do sistema operacional
Banco de dados-Disco1 (disco de saudação excluídas da proteção de saudação) | Disk1 | D:\ | pagefile.sys
DB-Disk2 | Disk2 | E:\ | User data 1
DB-Disk3 | Disk3 | F:\ | User data 2

Aqui estão configurações de arquivo paginação Olá na máquina de virtual de origem hello:

![Configurações do arquivo de paginação na máquina virtual de origem](./media/site-recovery-exclude-disk/pagefile-on-d-drive-sourceVM.png)


Após o failover da máquina virtual de saudação do VMware tooAzure ou tooAzure do Hyper-V, discos em Olá máquina virtual do Azure são:

**Nome do disco** | **Sistema operacional convidado - disco nº** | **Letra da unidade** | **Tipo de dados em disco Olá**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Disco do sistema operacional
DB-Disk1 | Disk1 | D:\ | Armazenamento temporário</br /> </br />pagefile.sys
DB-Disk2 | Disk2 | E:\ | User data 1
DB-Disk3 | Disk3 | F:\ | User data 2

Disco1 (d) foi excluído, d: é a primeira letra de unidade Olá da lista disponível hello. Azure atribui d: volume de armazenamento temporário de toohello. Como unidade d: estão disponíveis na máquina virtual do Azure de saudação, configuração arquivo de paginação saudação do hello máquina virtual permanece Olá mesmo.

Aqui estão configurações de arquivo paginação Olá em Olá máquina virtual do Azure:

![Configurações do arquivo de paginação na máquina virtual do Azure](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover.png)

#### <a name="case-2-hello-paging-file-is-configured-on-another-drive-other-than-d-drive"></a>Caso 2: arquivo de paginação de saudação é configurado em outra unidade (que não seja a unidade d:)

Aqui está a configuração de disco de máquina virtual de origem hello:

**Nome do disco** | **Sistema operacional convidado - disco nº** | **Letra da unidade** | **Tipo de dados em disco Olá**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Disco do sistema operacional
Banco de dados-Disco1 (disco de saudação excluídas da proteção) | Disk1 | G:\ | pagefile.sys
DB-Disk2 | Disk2 | E:\ | User data 1
DB-Disk3 | Disk3 | F:\ | User data 2

Aqui estão configurações de arquivo paginação Olá na máquina virtual local, hello:

![Configurações de arquivo na máquina virtual local, Olá de paginação](./media/site-recovery-exclude-disk/pagefile-on-g-drive-sourceVM.png)

Após o failover da máquina virtual de saudação do VMware/Hyper-V tooAzure, discos em Olá máquina virtual do Azure são:

**Nome do disco**| **Sistema operacional convidado - disco nº**| **Letra da unidade** | **Tipo de dados em disco Olá**
--- | --- | --- | ---
DB-Disk0-OS | DISK0  |C:\ |Disco do sistema operacional
DB-Disk1 | Disk1 | D:\ | Armazenamento temporário</br /> </br />pagefile.sys
DB-Disk2 | Disk2 | E:\ | User data 1
DB-Disk3 | Disk3 | F:\ | User data 2

Como d: é a primeira letra de unidade hello, na lista de saudação disponíveis, o Azure atribui d: volume de armazenamento temporário de toohello. Para todos os discos de saudação replicado, permanece de letra de unidade Olá Olá mesmo. Porque Olá g disco não estiver disponível, o sistema de saudação usará unidade c: de saudação para Olá arquivo de paginação.

Aqui estão configurações de arquivo paginação Olá em Olá máquina virtual do Azure:

![Configurações do arquivo de paginação na máquina virtual do Azure](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover-2.png)

## <a name="next-steps"></a>Próximas etapas
Depois que a implantação estiver configurada e em funcionamento, [saiba mais](site-recovery-failover.md) sobre o os diferentes tipos de failover.
