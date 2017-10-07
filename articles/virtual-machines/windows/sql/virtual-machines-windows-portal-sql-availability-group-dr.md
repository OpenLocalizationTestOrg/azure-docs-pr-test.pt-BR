---
title: "Grupos de disponibilidade de servidor - máquinas virtuais do Azure - recuperação de desastres do aaaSQL | Microsoft Docs"
description: "Este artigo explica como grupo de tooconfigure uma disponibilidade de SQL Server em máquinas virtuais do Azure com uma réplica em uma região diferente."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 388c464e-a16e-4c9d-a0d5-bb7cf5974689
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: df6238dc61c5a56879c75c9bf7314c618f43c0ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a>Configurar um Grupo de Disponibilidade Always On em máquinas virtuais do Azure em diferentes regiões

Este artigo explica como tooconfigure uma disponibilidade de SQL Server Always On agrupar réplica em máquinas virtuais do Azure em um local remoto do Azure. Use a recuperação de desastres de toosupport de configuração.

Este artigo se aplica a tooAzure máquinas virtuais no modo do Gerenciador de recursos.

Olá imagem a seguir mostra uma implementação comum de um grupo de disponibilidade em máquinas virtuais do Azure:

   ![Grupo de Disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

Nessa implantação, todas as máquinas virtuais estão em uma região do Azure. réplicas de grupo de disponibilidade Olá podem ter de confirmação síncrona com failover automático no SQL-1 e 2 do SQL. toobuild essa arquitetura, consulte [modelo do grupo de disponibilidade ou tutorial](virtual-machines-windows-portal-sql-availability-group-overview.md).

Essa arquitetura é vulnerável toodowntime se Olá região do Azure torna-se inacessível. tooovercome essa vulnerabilidade, adicionar uma réplica em uma região do Azure diferente. Olá diagrama a seguir mostra como seria a nova arquitetura de saudação:

   ![Recuperação de desastre de grupo de disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

Olá diagrama anterior mostra uma nova máquina virtual chamada SQL-3. SQL-3 está em outra região do Azure. SQL-3 é adicionado toohello Cluster de Failover do Windows Server. SQL-3 pode hospedar uma réplica do grupo de disponibilidade. Finalmente, observe que a região do Azure para o SQL-3 Olá tem um novo balanceador de carga do Azure.

>[!NOTE]
> Um conjunto de disponibilidade do Azure é necessário quando mais de uma máquina virtual está em Olá mesma região. Se houver apenas uma máquina virtual na região hello, Olá conjunto de disponibilidade não é necessário. Você só pode colocar uma máquina virtual em um momento da criação do conjunto de disponibilidade. Se a máquina virtual de saudação já está em um conjunto de disponibilidade, você pode adicionar uma máquina virtual para uma réplica adicional mais tarde.

Nessa arquitetura, réplica Olá na região remota Olá normalmente é configurada com o modo de disponibilidade de confirmação assíncrona e modo de failover manual.

Quando as réplicas de grupo de disponibilidade em máquinas virtuais do Azure em diferentes regiões do Azure, requer que cada região:

* Um gateway de rede virtual
* Uma conexão de gateway de rede virtual

Olá diagrama a seguir mostra como redes de saudação se comunicam entre data centers.

   ![Grupo de Disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
>Essa arquitetura incorre em encargos de dados de saída para os dados replicados entre regiões do Azure. Veja [Preços de Largura de Banda](http://azure.microsoft.com/pricing/details/bandwidth/).  

## <a name="create-remote-replica"></a>Criar réplica remota

Olá toocreate uma réplica em um data center remoto, as etapas a seguir:

1. [Criar uma rede virtual na nova região de saudação](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

1. [Configurar uma conexão de rede virtual a rede usando o portal do Azure de saudação](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).

   >[!NOTE]
   >Em alguns casos, você pode ter a conexão de rede virtual a rede toouse PowerShell toocreate hello. Por exemplo, se você usar contas do Azure diferentes não pode configurar conexão Olá no portal de saudação. Consulte nesse caso, [configurar uma rede virtual a rede conexão usando Olá portal do Azure](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).

1. [Criar um controlador de domínio na nova região de saudação](../../../active-directory/active-directory-new-forest-virtual-machine.md).

   Esse controlador de domínio fornece autenticação se Olá controlador de domínio no site primário Olá não está disponível.

1. [Criar uma máquina virtual SQL Server na nova região de saudação](virtual-machines-windows-portal-sql-server-provision.md).

1. [Crie um balanceador de carga do Azure na rede de saudação na nova região de saudação](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).

   Este balanceador de carga deve:

   - Estar em Olá mesma rede e sub-rede como Olá nova máquina virtual.
   - Ter um endereço IP estático para o ouvinte do grupo de disponibilidade de saudação.
   - Inclua um pool de back-end consiste somente máquinas virtuais Olá Olá mesma região como Olá balanceador de carga.
   - Use um endereço IP TCP porta investigação toohello específico.
   - Ter uma regra toohello específicas do SQL Server na saudação de balanceamento de carga mesma região.  

1. [Adicionar toohello do recurso de cluster de Failover novo SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).

1. [Associar Olá novo SQL Server toohello domínio](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).

1. [Definir Olá toouse de conta de serviço novo SQL Server em uma conta de domínio](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).

1. [Adicionar toohello de SQL Server Olá novo Cluster de Failover do Windows Server](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).

1. Crie um recurso de endereço IP no cluster de saudação.

   Você pode criar o recurso de endereço IP Olá no Gerenciador de Cluster de Failover. Função de grupo de disponibilidade hello, clique **adicionar recurso**, **mais recursos**e clique em **endereço IP**.

   ![Criar endereço IP](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   Configure o endereço IP da seguinte maneira:

   - Use a rede de saudação do hello data center remoto.
   - Atribua o endereço IP de saudação do balanceador de carga do Azure nova hello. 

1. Em Olá novo SQL Server no SQL Server Configuration Manager, [habilitar grupos de disponibilidade AlwaysOn](http://msdn.microsoft.com/library/ff878259.aspx).

1. [Olá de portas de firewall aberta no novo servidor SQL](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).

   números de porta Olá necessário tooopen dependem de seu ambiente. Investigação de integridade do balanceador de carga de portas abertas para hello Azure e ponto de extremidade de espelhamento.

1. [Adicionar um grupo de réplica de disponibilidade toohello Olá novo SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).

   Para uma réplica em uma região remota do Azure, configurá-lo para a replicação assíncrona com failover manual.  

1. Adicione o recurso de endereço IP hello como uma dependência de cluster (nome de rede) do ponto de acesso de cliente do Olá ouvinte.

   Olá seguinte captura de tela mostra um recurso de cluster de endereço IP configurado corretamente:

   ![Grupo de Disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   >grupo de recursos de cluster de saudação inclui os dois endereços IP. Os dois endereços IP são as dependências para ponto de acesso para cliente Olá ouvinte. Saudação de uso **ou** operador na configuração de dependência de cluster hello.

1. [Definir parâmetros de cluster de saudação do PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).

Execute script do PowerShell Olá com nome de rede de cluster hello, endereço IP e porta de investigação configurado no balanceador de carga de saudação na nova região de saudação.

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster name for hello network in hello new region (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "<IPResourceName>" # hello cluster name for hello new IP Address resource.
   $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB) in hello new region. This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <nnnnn> # hello probe port you set on hello ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a>Definir conexão para várias sub-redes

réplica Olá Olá data center remoto é parte do grupo de disponibilidade de saudação, mas ele está em uma sub-rede diferente. Se essa réplica se tornar a réplica primária Olá, tempo limite de conexão do aplicativo pode ocorrer. Esse comportamento é Olá igual um grupo de disponibilidade local em uma implantação de várias sub-redes. tooallow conexões de aplicativos cliente, atualizar a conexão de cliente hello ou configurar a resolução de nome em cache no recurso de nome de rede de cluster hello.

De preferência, atualizar Olá tooset de cadeias de caracteres de conexão de cliente `MultiSubnetFailover=Yes`. Consulte [conectar-se ao MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).

Se você não pode modificar cadeias de caracteres de conexão hello, você pode configurar o cache de resolução de nome. Consulte [tempos limite de conexão no grupo de disponibilidade de várias sub-redes](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).

## <a name="fail-over-tooremote-region"></a>Failover tooremote região

tootest ouvinte conectividade toohello remoto região que você pode fazer failover região remota do toohello Olá réplica. Enquanto a réplica de saudação é assíncrona, o failover é vulnerável toopotential perda de dados. toofail failover sem perda de dados, alterar Olá toosynchronous de modo de disponibilidade e definir Olá tooautomatic de modo de failover. Olá Use as etapas a seguir:

1. Em **Pesquisador de objetos**, conecte-se a instância toohello do SQL Server que hospeda a réplica primária hello.
1. Em **grupos de disponibilidade do AlwaysOn**, **grupos de disponibilidade**, clique com botão direito seu grupo de disponibilidade e clique em **propriedades**.
1. Em Olá **geral** página em **réplicas de disponibilidade**, Olá de conjunto de réplica secundária no hello DR site toouse **confirmação síncrona** modo de disponibilidade e **Automático** modo de failover.
1. Se você tiver uma réplica secundária no mesmo site que a réplica primária para alta disponibilidade, defina esta réplica muito**confirmação assíncrona** e **Manual**.
1. Clique em OK.
1. Em **Pesquisador de objetos**, clique o grupo de disponibilidade hello e clique em **Mostrar painel**.
1. No painel de saudação, verifique se que Olá réplica no local de DR de saudação é sincronizada.
1. Em **Pesquisador de objetos**, clique o grupo de disponibilidade hello e clique em **Failover...** . Estúdios de gerenciamento do SQL Server abre um assistente toofail em relação ao SQL Server.  
1. Clique em **próximo**e a instância do SQL Server Olá selecione no site Olá DR. Clique em **Avançar** novamente.
1. Conecte-se toohello instância do SQL Server no site da saudação DR e clique em **próximo**.
1. Em Olá **resumo** , verifique as configurações de saudação e em **concluir**.

Depois de testar a conectividade, mova dados primário do hello réplica primária tooyour back center e definir Olá disponibilidade modo back tootheir configurações operacional normais. Olá tabela a seguir mostra configurações operacionais normal de Olá para arquitetura de saudação descritas neste documento:

| Local | Instância do servidor | Função | Modo de Disponibilidade | Modo de failover
| ----- | ----- | ----- | ----- | -----
| Data center principal | SQL-1 | Primário | Síncrono | Automático
| Data center principal | SQL-2 | Secundário | Síncrono | Automático
| Centro de dados remotos ou secundários | SQL-3 | Secundário | Assíncrono | Manual


### <a name="more-information-about-planned-and-forced-manual-failover"></a>Para obter mais informações sobre failover manual forçado e não planejado

Para obter mais informações, consulte Olá seguintes tópicos:

- [Executar um Failover Manual planejado de um grupo de disponibilidade (SQL Server)](http://msdn.microsoft.com/library/hh231018.aspx)
- [Executar um Failover Manual forçado de um grupo de disponibilidade (SQL Server)](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a>Links adicionais

* [Grupos de disponibilidade AlwaysOn](http://msdn.microsoft.com/library/hh510230.aspx)
* [Máquinas Virtuais do Azure](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [Balanceadores de Carga do Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [Conjuntos de Disponibilidade do Azure](../manage-availability.md)
