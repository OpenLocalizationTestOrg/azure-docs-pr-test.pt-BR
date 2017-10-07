---
title: "aaaHigh disponibilidade e recuperação de desastres do SQL Server | Microsoft Docs"
description: "Uma discussão de hello vários tipos de estratégias HADR para SQL Server em execução em máquinas virtuais do Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 53981f7e-8370-4979-b26a-93a5988d905f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/27/2017
ms.author: mikeray
ms.openlocfilehash: 2b62d8b30520952ba6b7da7177a2c2de95bea8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-and-disaster-recovery-for-sql-server-in-azure-virtual-machines"></a>Alta disponibilidade e recuperação de desastre para SQL Server nas Máquinas Virtuais do Azure

Microsoft Azure máquinas virtuais () com o SQL Server pode ajudar a reduzir o custo de saudação de uma solução de banco de dados de recuperação (HADR) desastres e disponibilidade alta. A maioria das soluções HADR do SQL Server tem suporte em máquinas virtuais do Azure, tanto como somente Azure ou como soluções híbridas. Em uma solução somente no Azure, todo o sistema HADR Olá é executado no Azure. Em uma configuração híbrida, parte da solução de saudação é executado no Azure e Olá outros parte é executado localmente em sua organização. Olá flexibilidade da saudação ambiente Azure permite que você toomove parcialmente ou totalmente tooAzure toosatisfy Olá requisitos orçamento e HADR do SQL Server do banco de dados sistemas.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="understanding-hello-need-for-an-hadr-solution"></a>Noções básicas sobre Olá necessidade de uma solução HADR
É o tooyou tooensure seu sistema de banco de dados possui recursos HADR de Olá Olá contrato de nível de serviço (SLA) exige. Olá fato Azure fornecer mecanismos de alta disponibilidade, como recuperação de serviço para serviços de nuvem e a detecção de recuperação de falhas para máquinas virtuais, não é garantia que pode atender o SLA de saudação desejada. Esses mecanismos protegem a alta disponibilidade Olá Olá VMs, mas não Olá alta disponibilidade do SQL Server em execução dentro do hello VMs. É possível toofail de instância do SQL Server Olá enquanto Olá VM está online e íntegra. Além disso, mecanismos de alta disponibilidade mesmo Olá fornecidos pelo Azure permitem tempo de inatividade de saudação VMs devido tooevents como a recuperação de falhas de hardware ou software e atualizações do sistema operacional.

Além disso, o GRS (Armazenamento com Redundância Geográfica) no Azure, que é implementado com um recurso chamado replicação geográfica, pode não ser uma solução de recuperação de desastres adequada para seus bancos de dados. Porque a replicação geográfica envia dados de forma assíncrona, as atualizações recentes podem ser perdidas em caso de saudação de desastre. Para obter mais informações sobre limitações de replicação geográfica são abordadas em Olá [não tem suportada para arquivos de dados e de log em discos separados de replicação geográfica](#geo-replication-support) seção.

## <a name="hadr-deployment-architectures"></a>Arquiteturas de implantação de HADR
As tecnologias HADR do SQL Server que têm suporte no Azure incluem:

* [Grupos de disponibilidade AlwaysOn](https://technet.microsoft.com/library/hh510230.aspx)
* [Instâncias do cluster de failover AlwaysOn](https://technet.microsoft.com/library/ms189134.aspx)
* [Envio de logs](https://technet.microsoft.com/library/ms187103.aspx)
* [Backup e restauração do SQL Server com o Serviço de armazenamento de blobs do Azure](https://msdn.microsoft.com/library/jj919148.aspx)
* [Espelhamento de banco de dados](https://technet.microsoft.com/library/ms189852.aspx) - preterido no SQL Server 2016

É possível toocombine Olá tecnologias juntos tooimplement uma solução de SQL Server que tenha alta disponibilidade e recursos de recuperação de desastres. Dependendo da tecnologia de saudação usada, uma implantação híbrida pode exigir um túnel VPN com hello rede virtual do Azure. Olá seções a seguir mostram algumas das arquiteturas de implantação de exemplo hello.

## <a name="azure-only-high-availability-solutions"></a>Somente Azure: soluções de alta disponibilidade

É possível ter uma solução de alta disponibilidade para o SQL Server em um nível de banco de dados com Grupos de Disponibilidade AlwaysOn - chamados de grupos de disponibilidade. Você também pode criar uma solução de alta disponibilidade no nível da instância com Instâncias de Cluster de Failover do Always On - instâncias de cluster de failover. Para adicionar redundância, crie a redundância nos dois níveis, criando grupos de disponibilidade em instâncias de cluster de failover. 

| Tecnologia | Arquiteturas de exemplo |
| --- | --- |
| **Grupos de disponibilidade** |Réplicas de disponibilidade executadas em VMs do Azure no hello mesmo região fornecer alta disponibilidade. É necessário tooconfigure um controlador de domínio VM, como clustering de failover do Windows requer um domínio do Active Directory.<br/> ![Grupos de Disponibilidade](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_ha_always_on.gif)<br/>Para saber mais, consulte [Configurar Grupos de Disponibilidade no Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups.md). |
| **Instâncias do cluster de failover** |FCI (Instâncias de Cluster de Failover), que exigem armazenamento compartilhado, podem ser criadas de três maneiras diferentes.<br/><br/>1. Um cluster de failover de dois nós em execução em VMs do Azure com o uso do armazenamento anexado [Windows Server 2016 espaços de armazenamento diretos \(S2D\) ](virtual-machines-windows-portal-sql-create-failover-cluster.md) tooprovide uma SAN virtual com base em software.<br/><br/>2. Um cluster de failover de dois nós em execução nas VMs do Azure com armazenamento com suporte em uma solução de clustering de terceiros. Para obter um exemplo específico que usa o SIOS DataKeeper, consulte [Alta disponibilidade para um compartilhamento de arquivos usando o clustering de failover e o software de terceiros SIOS Datakeeper](https://azure.microsoft.com/blog/high-availability-for-a-file-share-using-wsfc-ilb-and-3rd-party-software-sios-datakeeper/).<br/><br/>3. Um cluster de failover de dois nós em execução nas VMs do Azure com armazenamento em bloco compartilhado do Destino iSCSI remoto por meio do ExpressRoute. Por exemplo, armazenamento privado em NetApp (NPS) expõe um destino de iSCSI por meio do ExpressRoute com Equinix tooAzure VMs.<br/><br/>Para armazenamento compartilhado de terceiros e soluções de replicação de dados, você deverá contatar o fornecedor de saudação todos os problemas relacionados tooaccessing dados durante o failover.<br/><br/>Observe que ainda não há suporte para o uso do FCI no [Armazenamento de arquivos do Azure](https://azure.microsoft.com/services/storage/files/) , pois esta solução não utiliza o Armazenamento Premium. Estamos trabalhando toosupport em breve. |

## <a name="azure-only-disaster-recovery-solutions"></a>Somente Azure: soluções de recuperação de desastre
Você pode ter uma solução de recuperação de desastres para seus bancos de dados do SQL Server no Azure usando Grupos de Disponibilidade, espelhamento de banco de dados ou backup e restauração com blobs de armazenamento.

| Tecnologia | Arquiteturas de exemplo |
| --- | --- |
| **Grupos de Disponibilidade** |Réplicas de disponibilidade executadas em vários datacenters em VMs do Azure para recuperação de desastres. Essa solução de regiões cruzadas protege contra interrupção completa de site. <br/> ![Grupos de Disponibilidade](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_alwayson.png)<br/>Dentro de uma região, todas as réplicas devem estar dentro Olá mesmo serviço de nuvem e Olá mesma rede virtual. Como cada região terá uma VNet separada, essas soluções exigem conectividade de tooVNet de rede virtual. Para obter mais informações, consulte [configurar uma rede virtual a rede conexão usando Olá portal do Azure](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md). Para obter instruções detalhadas, confira [Configurar um grupo de disponibilidade do SQL Server em máquinas virtuais do Azure em diferentes regiões](virtual-machines-windows-portal-sql-availability-group-dr.md).|
| **Espelhamento de banco de dados** |Servidores principal e de espelho em execução em diferentes datacenters para recuperação de desastres. Você deve implantar usando certificados de servidor, pois um domínio do Active Directory não pode abranger vários datacenters.<br/>![Espelhamento de banco de dados](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_dbmirroring.gif) |
| **Backup e restauração com o Serviço de armazenamento de blob do Azure** |Backup de bancos de dados de produção diretamente tooblob armazenamento em um datacenter diferente para a recuperação de desastres.<br/>![Backup e restauração](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_backup_restore.gif)<br/>Para obter mais informações, consulte [Backup e Restauração para SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-backup-recovery.md). |

## <a name="hybrid-it-disaster-recovery-solutions"></a>TI híbrida: soluções de recuperação de desastre
Você pode ter uma solução de recuperação de desastres para seus bancos de dados do SQL Server em um ambiente de TI híbrida, usando Grupos de disponibilidade, espelhamento de banco de dados, envio de log e backup e restauração com o armazenamento de blog do Azure.

| Tecnologia | Arquiteturas de exemplo |
| --- | --- |
| **Grupos de Disponibilidade** |Algumas réplicas de disponibilidade executadas em VMs do Azure e outras réplicas executadas localmente para recuperação de desastres intersite. Olá site de produção pode ser local ou em um datacenter do Azure.<br/>![Grupos de Disponibilidade](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_alwayson.gif)<br/>Como todas as réplicas de disponibilidade devem estar no hello mesmo cluster de failover, hello cluster deve abranger as duas redes (um cluster de failover de várias sub-redes). Essa configuração requer uma conexão VPN entre a rede de local do Azure e hello.<br/><br/>Para a recuperação de desastres com êxito de seus bancos de dados, você também deve instalar um controlador de domínio de réplica no local de recuperação de desastres hello.<br/><br/>É possível toouse Olá assistente Adicionar réplica no SSMS tooadd um tooan de réplica do Azure sempre no grupo de disponibilidade existente. Para obter mais informações, consulte o Tutorial: estender tooAzure seu grupo de disponibilidade AlwaysOn. |
| **Espelhamento de banco de dados** |Um parceiro executado em uma máquina virtual do Azure e hello outros em execução no local para recuperação de desastres entre sites usando certificados de servidor. Os parceiros não precisarem toobe em Olá mesmo domínio do Active Directory, e nenhuma conexão de VPN é necessária.<br/>![Espelhamento de banco de dados](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_dbmirroring.gif)<br/>Outro cenário de espelhamento de banco de dados envolve um parceiro executado em uma VM do Azure e hello outra executada localmente em Olá mesmo domínio do Active Directory para a recuperação de desastres entre sites. Um [conexão VPN entre a rede de saudação do Azure virtual network e hello local](../../../vpn-gateway/vpn-gateway-site-to-site-create.md) é necessária.<br/><br/>Para a recuperação de desastres com êxito de seus bancos de dados, você também deve instalar um controlador de domínio de réplica no local de recuperação de desastres hello. |
| **Envio de logs** |Um servidor executado em uma máquina virtual do Azure e hello outros em execução no local para recuperação de desastres entre sites. Envio de logs depende de compartilhamento de arquivos do Windows, para que uma conexão VPN entre Olá rede virtual do Azure e hello a rede é necessária no local.<br/>![Envio de logs](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_log_shipping.gif)<br/>Para a recuperação de desastres com êxito de seus bancos de dados, você também deve instalar um controlador de domínio de réplica no local de recuperação de desastres hello. |
| **Backup e restauração com o Serviço de armazenamento de blob do Azure** |Bancos de dados de produção feitos diretamente o armazenamento de blob tooAzure para recuperação de desastres ao local.<br/>![Backup e restauração](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_backup_restore.gif)<br/>Para obter mais informações, consulte [Backup e Restauração para SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-backup-recovery.md). |

## <a name="important-considerations-for-sql-server-hadr-in-azure"></a>Considerações importantes para HADR do SQL Server no Azure
VMs do Azure, armazenamento e rede têm características operacionais diferentes da infraestrutura de TI local, não virtualizada. Uma implementação bem-sucedida de uma solução HADR do SQL Server no Azure requer que você compreenda essas diferenças e crie sua solução tooaccommodate-los.

### <a name="high-availability-nodes-in-an-availability-set"></a>Nós de alta disponibilidade em um conjunto de disponibilidade
Conjuntos de disponibilidade no Azure permitem que você tooplace nós de alta disponibilidade de saudação em domínios de falha (FDs) e domínios de atualização (UDs) separados. Para máquinas virtuais do Azure toobe colocado em Olá mesmo conjunto de disponibilidade, você deve implantá-los em Olá mesmo serviço de nuvem. Apenas nós no mesmo serviço de nuvem pode participar de Olá Olá mesmo conjunto de disponibilidade. Para obter mais informações, consulte [gerenciar Olá disponibilidade das máquinas virtuais](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="failover-cluster-behavior-in-azure-networking"></a>Comportamento do cluster de failover na rede do Azure
serviço DHCP não compatível com RFC Olá no Azure pode causar a criação de saudação de determinados toofail de configurações de cluster de failover, devido a nome de rede de cluster toohello sendo atribuído um endereço IP duplicado, como saudação de endereços IP mesmo como um de nós de cluster de saudação. Este é um problema quando você implementa grupos de disponibilidade, que depende do recurso de cluster de failover do Windows hello.

Considere o cenário de saudação quando um cluster de dois nós é criado e colocado online:

1. Olá cluster fica online e, em seguida, NODE1 solicita um endereço IP atribuído dinamicamente para o nome de rede de cluster hello.
2. Nenhum endereço IP que não seja o endereço IP de NODE1 é determinado pelo Olá serviço DHCP, como Olá serviço DHCP reconhece essa solicitação hello proveniente NODE1 em si.
3. O Windows detecta que um endereço duplicado é atribuído tooNODE1 e toohello nome de rede do cluster de failover e grupo de clusters padrão Olá falha toocome on-line.
4. grupo de clusters padrão Olá move tooNODE2, que trata o endereço IP de NODE1 como o endereço IP de cluster hello e coloca o grupo de clusters de padrão de saudação online.
5. Quando NODE2 tenta tooestablish conectividade com NODE1, pacotes direcionados a NODE1 nunca deixam NODE2 pois ele resolve tooitself de endereço IP de NODE1. NODE2 não pode estabelecer conectividade com NODE1, perde quorum e fecha o cluster de saudação.
6. Em Olá enquanto isso, NODE1 pode enviar pacotes tooNODE2, mas NODE2 não pode responder. Node1 perde quorum e fecha o cluster de saudação.

Esse cenário pode ser evitado atribuindo um estático endereço IP não usado, como um endereço IP de link local como 169.254.1.1, o nome de rede de cluster toohello na ordem toobring Olá rede nome do cluster online. toosimplify esse processo, consulte [Configurando o Windows cluster de failover do Azure para grupos de disponibilidade](http://social.technet.microsoft.com/wiki/contents/articles/14776.configuring-windows-failover-cluster-in-windows-azure-for-alwayson-availability-groups.aspx).

Para saber mais, consulte [Configurar grupos de disponibilidade no Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups.md).

### <a name="availability-group-listener-support"></a>Suporte do ouvinte do grupo de disponibilidade
Ouvintes do grupo de disponibilidade têm suporte em VMs do Azure que executam o Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 e Windows Server 2016. Esse suporte é possibilitado pelo uso de saudação dos pontos de extremidade com balanceamento de carga habilitado em VMs do Azure Olá que são nós de grupo de disponibilidade. Você deve seguir as etapas de configuração especial para Olá ouvintes toowork para aplicativos cliente que estão em execução no Azure, bem como aqueles em execução no local.

Há duas opções principais para configurar o ouvinte: externo (público) ou interno. usos de ouvinte (público) externo Olá voltado para a internet um balanceador de carga e está associado com um público IP Virtual (VIP) que é acessível pela Olá da internet. Um ouvinte interno usa um balanceador de carga interno e Olá de somente oferece suporte a clientes na mesma rede Virtual. Para qualquer desses dois tipos de balanceador de carga, você deve habilitar o retorno de servidor direto. 

Se Olá grupo de disponibilidade abranger diversas sub-redes do Azure (como uma implantação que cruza regiões do Azure), cadeia de caracteres de conexão de cliente Olá deve incluir "**MultisubnetFailover = True**". Isso resulta em réplicas de toohello tentativas de conexão paralelas em sub-redes diferentes hello. Para obter instruções sobre como configurar um ouvinte, consulte

* [Configurar um ouvinte de ILB para grupos de disponibilidade no Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md).
* [Configurar um ouvinte externo para grupos de disponibilidade no Azure](../classic/ps-sql-ext-listener.md).

Você ainda pode conectar tooeach réplica de disponibilidade separadamente conectando-se diretamente a instância do serviço toohello. Além disso, como grupos de disponibilidade são compatíveis com versões anteriores com clientes de espelhamento de banco de dados, você pode se conectar toohello réplicas de disponibilidade como parceiros de espelhamento como Olá réplicas são configuradas de banco de dados de espelhamento toodatabase semelhante:

* Uma réplica primária e uma réplica secundária
* Olá réplica secundária está configurada como ilegível (**secundária legível** opção definida muito**não**)

Uma cadeia de conexão de cliente de exemplo que corresponde a toothis configuração de espelhamento de banco de dados usando ADO.NET ou o SQL Server Native Client está abaixo:

    Data Source=ReplicaServer1;Failover Partner=ReplicaServer2;Initial Catalog=AvailabilityDatabase;

Para obter mais informações sobre conectividade de cliente, consulte:

* [Usando palavras-chave da cadeia de conexão com o SQL Server Native Client](https://msdn.microsoft.com/library/ms130822.aspx)
* [Conectar clientes tooa sessão de espelhamento de banco de dados (SQL Server)](https://technet.microsoft.com/library/ms175484.aspx)
* [Conectando tooAvailability ouvinte de grupo em TI híbrida](http://blogs.msdn.com/b/sqlalwayson/archive/2013/02/14/connecting-to-availability-group-listener-in-hybrid-it.aspx)
* [Ouvintes de grupo de disponibilidade, conectividade de cliente e failover de aplicativo (SQL Server)](https://technet.microsoft.com/library/hh213417.aspx)
* [Usando cadeias de conexão de espelhamento de banco de dados com grupos de disponibilidade](https://technet.microsoft.com/library/hh213417.aspx)

### <a name="network-latency-in-hybrid-it"></a>Latência de rede em TI híbrida
Você deve implantar sua solução HADR com a suposição de saudação que pode haver períodos de tempo com alta latência da rede entre sua rede local e o Azure. Ao implantar réplicas tooAzure, você deve usar a confirmação assíncrona, em vez de confirmação síncrona para o modo de sincronização de saudação. Ao implantar servidores de espelhamento de banco de dados local tanto no Azure, use o modo de alto desempenho Olá em vez do modo de alta segurança hello.

### <a name="geo-replication-support"></a>Suporte para replicação geográfica
A replicação geográfica em discos do Azure não oferece suporte a arquivo de dados de saudação e o arquivo de log da saudação toobe do mesmo banco de dados armazenado em discos separados. GRS replica as alterações em cada disco, de forma independente e assíncrona. Esse mecanismo garante a ordem de gravação da saudação dentro de um único disco na cópia replicada geograficamente de hello, mas não em cópias replicadas geograficamente de vários discos. Se você configurar um banco de dados toostore seu arquivo de dados e o arquivo de log em discos separados, Olá recuperado discos após um desastre poderão conter uma cópia mais recente saudação do arquivo de dados que o arquivo de log hello, quais quebras Olá log write-ahead no SQL Server e Olá ACID Propriedades de transações. Se você não tiver Olá opção toodisable a replicação geográfica na conta de armazenamento hello, você deve manter todos os dados e arquivos de log para um determinado banco de dados Olá mesmo disco. Se você precisar usar mais de um disco devido toohello o tamanho do banco de dados de hello, é necessário toodeploy uma das soluções de recuperação de desastres Olá listadas acima tooensure a redundância de dados.

## <a name="next-steps"></a>Próximas etapas
Se você precisar toocreate uma máquina virtual do Azure com o SQL Server, consulte [provisionar uma máquina Virtual do SQL Server no Azure](virtual-machines-windows-portal-sql-server-provision.md).

tooget Olá melhor desempenho do SQL Server em execução em uma VM do Azure, consulte as diretrizes de saudação em [práticas recomendadas de desempenho para o SQL Server em máquinas virtuais Azure](virtual-machines-windows-sql-performance.md).

Para outros tópicos relacionados toorunning do SQL Server em VMs do Azure, consulte [do SQL Server em máquinas virtuais Azure](virtual-machines-windows-sql-server-iaas-overview.md).

### <a name="other-resources"></a>Outros recursos
* [Instalar uma nova floresta do Active Directory no Azure](../../../active-directory/active-directory-new-forest-virtual-machine.md)
* [Criar um cluster de failover para grupos de disponibilidade em uma VM do Azure](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a)

