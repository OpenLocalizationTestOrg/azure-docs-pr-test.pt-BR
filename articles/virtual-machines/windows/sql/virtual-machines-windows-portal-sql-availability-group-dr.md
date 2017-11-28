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
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a><span data-ttu-id="ea0fc-103">Configurar um Grupo de Disponibilidade Always On em máquinas virtuais do Azure em diferentes regiões</span><span class="sxs-lookup"><span data-stu-id="ea0fc-103">Configure an Always On availability group on Azure virtual machines in different regions</span></span>

<span data-ttu-id="ea0fc-104">Este artigo explica como tooconfigure uma disponibilidade de SQL Server Always On agrupar réplica em máquinas virtuais do Azure em um local remoto do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-104">This article explains how tooconfigure a SQL Server Always On availability group replica on Azure virtual machines in a remote Azure location.</span></span> <span data-ttu-id="ea0fc-105">Use a recuperação de desastres de toosupport de configuração.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-105">Use this configuration toosupport disaster recovery.</span></span>

<span data-ttu-id="ea0fc-106">Este artigo se aplica a tooAzure máquinas virtuais no modo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-106">This article applies tooAzure Virtual Machines in Resource Manager mode.</span></span>

<span data-ttu-id="ea0fc-107">Olá imagem a seguir mostra uma implementação comum de um grupo de disponibilidade em máquinas virtuais do Azure:</span><span class="sxs-lookup"><span data-stu-id="ea0fc-107">hello following image shows a common deployment of an availability group on Azure virtual machines:</span></span>

   ![Grupo de Disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

<span data-ttu-id="ea0fc-109">Nessa implantação, todas as máquinas virtuais estão em uma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-109">In this deployment, all virtual machines are in one Azure region.</span></span> <span data-ttu-id="ea0fc-110">réplicas de grupo de disponibilidade Olá podem ter de confirmação síncrona com failover automático no SQL-1 e 2 do SQL.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-110">hello availability group replicas can have synchronous commit with automatic failover on SQL-1 and SQL-2.</span></span> <span data-ttu-id="ea0fc-111">toobuild essa arquitetura, consulte [modelo do grupo de disponibilidade ou tutorial](virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ea0fc-111">toobuild this architecture, see [Availability Group template or tutorial](virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

<span data-ttu-id="ea0fc-112">Essa arquitetura é vulnerável toodowntime se Olá região do Azure torna-se inacessível.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-112">This architecture is vulnerable toodowntime if hello Azure region becomes inaccessible.</span></span> <span data-ttu-id="ea0fc-113">tooovercome essa vulnerabilidade, adicionar uma réplica em uma região do Azure diferente.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-113">tooovercome this vulnerability, add a replica in a different Azure region.</span></span> <span data-ttu-id="ea0fc-114">Olá diagrama a seguir mostra como seria a nova arquitetura de saudação:</span><span class="sxs-lookup"><span data-stu-id="ea0fc-114">hello following diagram shows how hello new architecture would look:</span></span>

   ![Recuperação de desastre de grupo de disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

<span data-ttu-id="ea0fc-116">Olá diagrama anterior mostra uma nova máquina virtual chamada SQL-3.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-116">hello preceding diagram shows a new virtual machine called SQL-3.</span></span> <span data-ttu-id="ea0fc-117">SQL-3 está em outra região do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-117">SQL-3 is in a different Azure region.</span></span> <span data-ttu-id="ea0fc-118">SQL-3 é adicionado toohello Cluster de Failover do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-118">SQL-3 is added toohello Windows Server Failover Cluster.</span></span> <span data-ttu-id="ea0fc-119">SQL-3 pode hospedar uma réplica do grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-119">SQL-3 can host an availability group replica.</span></span> <span data-ttu-id="ea0fc-120">Finalmente, observe que a região do Azure para o SQL-3 Olá tem um novo balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-120">Finally, notice that hello Azure region for SQL-3 has a new Azure load balancer.</span></span>

>[!NOTE]
> <span data-ttu-id="ea0fc-121">Um conjunto de disponibilidade do Azure é necessário quando mais de uma máquina virtual está em Olá mesma região.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-121">An Azure availability set is required when more than one virtual machine is in hello same region.</span></span> <span data-ttu-id="ea0fc-122">Se houver apenas uma máquina virtual na região hello, Olá conjunto de disponibilidade não é necessário.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-122">If only one virtual machine is in hello region, then hello availability set is not required.</span></span> <span data-ttu-id="ea0fc-123">Você só pode colocar uma máquina virtual em um momento da criação do conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-123">You can only place a virtual machine in an availability set at creation time.</span></span> <span data-ttu-id="ea0fc-124">Se a máquina virtual de saudação já está em um conjunto de disponibilidade, você pode adicionar uma máquina virtual para uma réplica adicional mais tarde.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-124">If hello virtual machine is already in an availability set, you can add a virtual machine for an additional replica later.</span></span>

<span data-ttu-id="ea0fc-125">Nessa arquitetura, réplica Olá na região remota Olá normalmente é configurada com o modo de disponibilidade de confirmação assíncrona e modo de failover manual.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-125">In this architecture, hello replica in hello remote region is normally configured with asynchronous commit availability mode and manual failover mode.</span></span>

<span data-ttu-id="ea0fc-126">Quando as réplicas de grupo de disponibilidade em máquinas virtuais do Azure em diferentes regiões do Azure, requer que cada região:</span><span class="sxs-lookup"><span data-stu-id="ea0fc-126">When availability group replicas are on Azure virtual machines in different Azure regions, each region requires:</span></span>

* <span data-ttu-id="ea0fc-127">Um gateway de rede virtual</span><span class="sxs-lookup"><span data-stu-id="ea0fc-127">A virtual network gateway</span></span>
* <span data-ttu-id="ea0fc-128">Uma conexão de gateway de rede virtual</span><span class="sxs-lookup"><span data-stu-id="ea0fc-128">A virtual network gateway connection</span></span>

<span data-ttu-id="ea0fc-129">Olá diagrama a seguir mostra como redes de saudação se comunicam entre data centers.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-129">hello following diagram shows how hello networks communicate between data centers.</span></span>

   ![Grupo de Disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
><span data-ttu-id="ea0fc-131">Essa arquitetura incorre em encargos de dados de saída para os dados replicados entre regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-131">This architecture incurs outbound data charges for data replicated between Azure regions.</span></span> <span data-ttu-id="ea0fc-132">Veja [Preços de Largura de Banda](http://azure.microsoft.com/pricing/details/bandwidth/).</span><span class="sxs-lookup"><span data-stu-id="ea0fc-132">See [Bandwidth Pricing](http://azure.microsoft.com/pricing/details/bandwidth/).</span></span>  

## <a name="create-remote-replica"></a><span data-ttu-id="ea0fc-133">Criar réplica remota</span><span class="sxs-lookup"><span data-stu-id="ea0fc-133">Create remote replica</span></span>

<span data-ttu-id="ea0fc-134">Olá toocreate uma réplica em um data center remoto, as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ea0fc-134">toocreate a replica in a remote data center, do hello following steps:</span></span>

1. <span data-ttu-id="ea0fc-135">[Criar uma rede virtual na nova região de saudação](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="ea0fc-135">[Create a virtual network in hello new region](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

1. <span data-ttu-id="ea0fc-136">[Configurar uma conexão de rede virtual a rede usando o portal do Azure de saudação](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ea0fc-136">[Configure a VNet-to-VNet connection using hello Azure portal](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span></span>

   >[!NOTE]
   ><span data-ttu-id="ea0fc-137">Em alguns casos, você pode ter a conexão de rede virtual a rede toouse PowerShell toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-137">In some cases, you may have toouse PowerShell toocreate hello VNet-to-VNet connection.</span></span> <span data-ttu-id="ea0fc-138">Por exemplo, se você usar contas do Azure diferentes não pode configurar conexão Olá no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-138">For example, if you use different Azure accounts you cannot configure hello connection in hello portal.</span></span> <span data-ttu-id="ea0fc-139">Consulte nesse caso, [configurar uma rede virtual a rede conexão usando Olá portal do Azure](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ea0fc-139">In this case see, [Configure a VNet-to-VNet connection using hello Azure portal](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

1. <span data-ttu-id="ea0fc-140">[Criar um controlador de domínio na nova região de saudação](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="ea0fc-140">[Create a domain controller in hello new region](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span></span>

   <span data-ttu-id="ea0fc-141">Esse controlador de domínio fornece autenticação se Olá controlador de domínio no site primário Olá não está disponível.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-141">This domain controller provides authentication if hello domain controller in hello primary site is not available.</span></span>

1. <span data-ttu-id="ea0fc-142">[Criar uma máquina virtual SQL Server na nova região de saudação](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="ea0fc-142">[Create a SQL Server virtual machine in hello new region](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

1. <span data-ttu-id="ea0fc-143">[Crie um balanceador de carga do Azure na rede de saudação na nova região de saudação](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="ea0fc-143">[Create an Azure load balancer in hello network on hello new region](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

   <span data-ttu-id="ea0fc-144">Este balanceador de carga deve:</span><span class="sxs-lookup"><span data-stu-id="ea0fc-144">This load balancer must:</span></span>

   - <span data-ttu-id="ea0fc-145">Estar em Olá mesma rede e sub-rede como Olá nova máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-145">Be in hello same network and subnet as hello new virtual machine.</span></span>
   - <span data-ttu-id="ea0fc-146">Ter um endereço IP estático para o ouvinte do grupo de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-146">Have a static IP address for hello availability group listener.</span></span>
   - <span data-ttu-id="ea0fc-147">Inclua um pool de back-end consiste somente máquinas virtuais Olá Olá mesma região como Olá balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-147">Include a backend pool consisting of only hello virtual machines in hello same region as hello load balancer.</span></span>
   - <span data-ttu-id="ea0fc-148">Use um endereço IP TCP porta investigação toohello específico.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-148">Use a TCP port probe specific toohello IP address.</span></span>
   - <span data-ttu-id="ea0fc-149">Ter uma regra toohello específicas do SQL Server na saudação de balanceamento de carga mesma região.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-149">Have a load balancing rule specific toohello SQL Server in hello same region.</span></span>  

1. <span data-ttu-id="ea0fc-150">[Adicionar toohello do recurso de cluster de Failover novo SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="ea0fc-150">[Add Failover Clustering feature toohello new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

1. <span data-ttu-id="ea0fc-151">[Associar Olá novo SQL Server toohello domínio](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="ea0fc-151">[Join hello new SQL Server toohello domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

1. <span data-ttu-id="ea0fc-152">[Definir Olá toouse de conta de serviço novo SQL Server em uma conta de domínio](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span><span class="sxs-lookup"><span data-stu-id="ea0fc-152">[Set hello new SQL Server service account toouse a domain account](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span></span>

1. <span data-ttu-id="ea0fc-153">[Adicionar toohello de SQL Server Olá novo Cluster de Failover do Windows Server](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span><span class="sxs-lookup"><span data-stu-id="ea0fc-153">[Add hello new SQL Server toohello Windows Server Failover Cluster](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span></span>

1. <span data-ttu-id="ea0fc-154">Crie um recurso de endereço IP no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-154">Create an IP address resource on hello cluster.</span></span>

   <span data-ttu-id="ea0fc-155">Você pode criar o recurso de endereço IP Olá no Gerenciador de Cluster de Failover.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-155">You can create hello IP address resource in Failover Cluster Manager.</span></span> <span data-ttu-id="ea0fc-156">Função de grupo de disponibilidade hello, clique **adicionar recurso**, **mais recursos**e clique em **endereço IP**.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-156">Right-click hello availability group role, click **Add Resource**, **More Resources**, and click **IP Address**.</span></span>

   ![Criar endereço IP](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   <span data-ttu-id="ea0fc-158">Configure o endereço IP da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="ea0fc-158">Configure this IP address as follows:</span></span>

   - <span data-ttu-id="ea0fc-159">Use a rede de saudação do hello data center remoto.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-159">Use hello network from hello remote data center.</span></span>
   - <span data-ttu-id="ea0fc-160">Atribua o endereço IP de saudação do balanceador de carga do Azure nova hello.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-160">Assign hello IP address from hello new Azure load balancer.</span></span> 

1. <span data-ttu-id="ea0fc-161">Em Olá novo SQL Server no SQL Server Configuration Manager, [habilitar grupos de disponibilidade AlwaysOn](http://msdn.microsoft.com/library/ff878259.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea0fc-161">On hello new SQL Server in SQL Server Configuration Manager, [enable Always On Availability Groups](http://msdn.microsoft.com/library/ff878259.aspx).</span></span>

1. <span data-ttu-id="ea0fc-162">[Olá de portas de firewall aberta no novo servidor SQL](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="ea0fc-162">[Open firewall ports on hello new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

   <span data-ttu-id="ea0fc-163">números de porta Olá necessário tooopen dependem de seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-163">hello port numbers you need tooopen depend on your environment.</span></span> <span data-ttu-id="ea0fc-164">Investigação de integridade do balanceador de carga de portas abertas para hello Azure e ponto de extremidade de espelhamento.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-164">Open ports for hello mirroring endpoint and Azure load balancer health probe.</span></span>

1. <span data-ttu-id="ea0fc-165">[Adicionar um grupo de réplica de disponibilidade toohello Olá novo SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea0fc-165">[Add a replica toohello availability group on hello new SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).</span></span>

   <span data-ttu-id="ea0fc-166">Para uma réplica em uma região remota do Azure, configurá-lo para a replicação assíncrona com failover manual.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-166">For a replica in a remote Azure region, set it for asynchronous replication with manual failover.</span></span>  

1. <span data-ttu-id="ea0fc-167">Adicione o recurso de endereço IP hello como uma dependência de cluster (nome de rede) do ponto de acesso de cliente do Olá ouvinte.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-167">Add hello IP address resource as a dependency for hello listener client access point (network name) cluster.</span></span>

   <span data-ttu-id="ea0fc-168">Olá seguinte captura de tela mostra um recurso de cluster de endereço IP configurado corretamente:</span><span class="sxs-lookup"><span data-stu-id="ea0fc-168">hello following screenshot shows a properly configured IP address cluster resource:</span></span>

   ![Grupo de Disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   ><span data-ttu-id="ea0fc-170">grupo de recursos de cluster de saudação inclui os dois endereços IP.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-170">hello cluster resource group includes both IP addresses.</span></span> <span data-ttu-id="ea0fc-171">Os dois endereços IP são as dependências para ponto de acesso para cliente Olá ouvinte.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-171">Both IP addresses are dependencies for hello listener client access point.</span></span> <span data-ttu-id="ea0fc-172">Saudação de uso **ou** operador na configuração de dependência de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-172">Use hello **OR** operator in hello cluster dependency configuration.</span></span>

1. <span data-ttu-id="ea0fc-173">[Definir parâmetros de cluster de saudação do PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span><span class="sxs-lookup"><span data-stu-id="ea0fc-173">[Set hello cluster parameters in PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span></span>

<span data-ttu-id="ea0fc-174">Execute script do PowerShell Olá com nome de rede de cluster hello, endereço IP e porta de investigação configurado no balanceador de carga de saudação na nova região de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-174">Run hello PowerShell script with hello cluster network name, IP address, and probe port that you configured on hello load balancer in hello new region.</span></span>

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster name for hello network in hello new region (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "<IPResourceName>" # hello cluster name for hello new IP Address resource.
   $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB) in hello new region. This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <nnnnn> # hello probe port you set on hello ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a><span data-ttu-id="ea0fc-175">Definir conexão para várias sub-redes</span><span class="sxs-lookup"><span data-stu-id="ea0fc-175">Set connection for multiple subnets</span></span>

<span data-ttu-id="ea0fc-176">réplica Olá Olá data center remoto é parte do grupo de disponibilidade de saudação, mas ele está em uma sub-rede diferente.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-176">hello replica in hello remote data center is part of hello availability group but it is in a different subnet.</span></span> <span data-ttu-id="ea0fc-177">Se essa réplica se tornar a réplica primária Olá, tempo limite de conexão do aplicativo pode ocorrer.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-177">If this replica becomes hello primary replica, application connection time-outs may occur.</span></span> <span data-ttu-id="ea0fc-178">Esse comportamento é Olá igual um grupo de disponibilidade local em uma implantação de várias sub-redes.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-178">This behavior is hello same as an on-premises availability group in a multi-subnet deployment.</span></span> <span data-ttu-id="ea0fc-179">tooallow conexões de aplicativos cliente, atualizar a conexão de cliente hello ou configurar a resolução de nome em cache no recurso de nome de rede de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-179">tooallow connections from client applications, either update hello client connection or configure name resolution caching on hello cluster network name resource.</span></span>

<span data-ttu-id="ea0fc-180">De preferência, atualizar Olá tooset de cadeias de caracteres de conexão de cliente `MultiSubnetFailover=Yes`.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-180">Preferably, update hello client connection strings tooset `MultiSubnetFailover=Yes`.</span></span> <span data-ttu-id="ea0fc-181">Consulte [conectar-se ao MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="ea0fc-181">See [Connecting With MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span></span>

<span data-ttu-id="ea0fc-182">Se você não pode modificar cadeias de caracteres de conexão hello, você pode configurar o cache de resolução de nome.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-182">If you cannot modify hello connection strings, you can configure name resolution caching.</span></span> <span data-ttu-id="ea0fc-183">Consulte [tempos limite de conexão no grupo de disponibilidade de várias sub-redes](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span><span class="sxs-lookup"><span data-stu-id="ea0fc-183">See [Connection Timeouts in Multi-subnet Availability Group](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span></span>

## <a name="fail-over-tooremote-region"></a><span data-ttu-id="ea0fc-184">Failover tooremote região</span><span class="sxs-lookup"><span data-stu-id="ea0fc-184">Fail over tooremote region</span></span>

<span data-ttu-id="ea0fc-185">tootest ouvinte conectividade toohello remoto região que você pode fazer failover região remota do toohello Olá réplica.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-185">tootest listener connectivity toohello remote region, you can fail over hello replica toohello remote region.</span></span> <span data-ttu-id="ea0fc-186">Enquanto a réplica de saudação é assíncrona, o failover é vulnerável toopotential perda de dados.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-186">While hello replica is asynchronous, failover is vulnerable toopotential data loss.</span></span> <span data-ttu-id="ea0fc-187">toofail failover sem perda de dados, alterar Olá toosynchronous de modo de disponibilidade e definir Olá tooautomatic de modo de failover.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-187">toofail over without data loss, change hello availability mode toosynchronous and set hello failover mode tooautomatic.</span></span> <span data-ttu-id="ea0fc-188">Olá Use as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ea0fc-188">Use hello following steps:</span></span>

1. <span data-ttu-id="ea0fc-189">Em **Pesquisador de objetos**, conecte-se a instância toohello do SQL Server que hospeda a réplica primária hello.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-189">In **Object Explorer**, connect toohello instance of SQL Server that hosts hello primary replica.</span></span>
1. <span data-ttu-id="ea0fc-190">Em **grupos de disponibilidade do AlwaysOn**, **grupos de disponibilidade**, clique com botão direito seu grupo de disponibilidade e clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-190">Under **AlwaysOn Availability Groups**, **Availability Groups**, right-click your availability group and click **Properties**.</span></span>
1. <span data-ttu-id="ea0fc-191">Em Olá **geral** página em **réplicas de disponibilidade**, Olá de conjunto de réplica secundária no hello DR site toouse **confirmação síncrona** modo de disponibilidade e **Automático** modo de failover.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-191">On hello **General** page, under **Availability Replicas**, set hello secondary replica in hello DR site toouse **Synchronous Commit** availability mode and **Automatic** failover mode.</span></span>
1. <span data-ttu-id="ea0fc-192">Se você tiver uma réplica secundária no mesmo site que a réplica primária para alta disponibilidade, defina esta réplica muito**confirmação assíncrona** e **Manual**.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-192">If you have a secondary replica in same site as your primary replica for high availability, set this replica too**Asynchronous Commit** and **Manual**.</span></span>
1. <span data-ttu-id="ea0fc-193">Clique em OK.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-193">Click OK.</span></span>
1. <span data-ttu-id="ea0fc-194">Em **Pesquisador de objetos**, clique o grupo de disponibilidade hello e clique em **Mostrar painel**.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-194">In **Object Explorer**, right-click hello availability group, and click **Show Dashboard**.</span></span>
1. <span data-ttu-id="ea0fc-195">No painel de saudação, verifique se que Olá réplica no local de DR de saudação é sincronizada.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-195">On hello dashboard, verify that hello replica on hello DR site is synchronized.</span></span>
1. <span data-ttu-id="ea0fc-196">Em **Pesquisador de objetos**, clique o grupo de disponibilidade hello e clique em **Failover...** . Estúdios de gerenciamento do SQL Server abre um assistente toofail em relação ao SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-196">In **Object Explorer**, right-click hello availability group, and click **Failover...**. SQL Server Management Studios opens a wizard toofail over SQL Server.</span></span>  
1. <span data-ttu-id="ea0fc-197">Clique em **próximo**e a instância do SQL Server Olá selecione no site Olá DR.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-197">Click **Next**, and select hello SQL Server instance in hello DR site.</span></span> <span data-ttu-id="ea0fc-198">Clique em **Avançar** novamente.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-198">Click **Next** again.</span></span>
1. <span data-ttu-id="ea0fc-199">Conecte-se toohello instância do SQL Server no site da saudação DR e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-199">Connect toohello SQL Server instance in hello DR site and click **Next**.</span></span>
1. <span data-ttu-id="ea0fc-200">Em Olá **resumo** , verifique as configurações de saudação e em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-200">On hello **Summary** page, verify hello settings and click **Finish**.</span></span>

<span data-ttu-id="ea0fc-201">Depois de testar a conectividade, mova dados primário do hello réplica primária tooyour back center e definir Olá disponibilidade modo back tootheir configurações operacional normais.</span><span class="sxs-lookup"><span data-stu-id="ea0fc-201">After testing connectivity, move hello primary replica back tooyour primary data center and set hello availability mode back tootheir normal operating settings.</span></span> <span data-ttu-id="ea0fc-202">Olá tabela a seguir mostra configurações operacionais normal de Olá para arquitetura de saudação descritas neste documento:</span><span class="sxs-lookup"><span data-stu-id="ea0fc-202">hello following table shows hello normal operational settings for hello architecture described in this document:</span></span>

| <span data-ttu-id="ea0fc-203">Local</span><span class="sxs-lookup"><span data-stu-id="ea0fc-203">Location</span></span> | <span data-ttu-id="ea0fc-204">Instância do servidor</span><span class="sxs-lookup"><span data-stu-id="ea0fc-204">Server Instance</span></span> | <span data-ttu-id="ea0fc-205">Função</span><span class="sxs-lookup"><span data-stu-id="ea0fc-205">Role</span></span> | <span data-ttu-id="ea0fc-206">Modo de Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="ea0fc-206">Availability Mode</span></span> | <span data-ttu-id="ea0fc-207">Modo de failover</span><span class="sxs-lookup"><span data-stu-id="ea0fc-207">Failover Mode</span></span>
| ----- | ----- | ----- | ----- | -----
| <span data-ttu-id="ea0fc-208">Data center principal</span><span class="sxs-lookup"><span data-stu-id="ea0fc-208">Primary data center</span></span> | <span data-ttu-id="ea0fc-209">SQL-1</span><span class="sxs-lookup"><span data-stu-id="ea0fc-209">SQL-1</span></span> | <span data-ttu-id="ea0fc-210">Primário</span><span class="sxs-lookup"><span data-stu-id="ea0fc-210">Primary</span></span> | <span data-ttu-id="ea0fc-211">Síncrono</span><span class="sxs-lookup"><span data-stu-id="ea0fc-211">Synchronous</span></span> | <span data-ttu-id="ea0fc-212">Automático</span><span class="sxs-lookup"><span data-stu-id="ea0fc-212">Automatic</span></span>
| <span data-ttu-id="ea0fc-213">Data center principal</span><span class="sxs-lookup"><span data-stu-id="ea0fc-213">Primary data center</span></span> | <span data-ttu-id="ea0fc-214">SQL-2</span><span class="sxs-lookup"><span data-stu-id="ea0fc-214">SQL-2</span></span> | <span data-ttu-id="ea0fc-215">Secundário</span><span class="sxs-lookup"><span data-stu-id="ea0fc-215">Secondary</span></span> | <span data-ttu-id="ea0fc-216">Síncrono</span><span class="sxs-lookup"><span data-stu-id="ea0fc-216">Synchronous</span></span> | <span data-ttu-id="ea0fc-217">Automático</span><span class="sxs-lookup"><span data-stu-id="ea0fc-217">Automatic</span></span>
| <span data-ttu-id="ea0fc-218">Centro de dados remotos ou secundários</span><span class="sxs-lookup"><span data-stu-id="ea0fc-218">Secondary or remote data center</span></span> | <span data-ttu-id="ea0fc-219">SQL-3</span><span class="sxs-lookup"><span data-stu-id="ea0fc-219">SQL-3</span></span> | <span data-ttu-id="ea0fc-220">Secundário</span><span class="sxs-lookup"><span data-stu-id="ea0fc-220">Secondary</span></span> | <span data-ttu-id="ea0fc-221">Assíncrono</span><span class="sxs-lookup"><span data-stu-id="ea0fc-221">Asynchronous</span></span> | <span data-ttu-id="ea0fc-222">Manual</span><span class="sxs-lookup"><span data-stu-id="ea0fc-222">Manual</span></span>


### <a name="more-information-about-planned-and-forced-manual-failover"></a><span data-ttu-id="ea0fc-223">Para obter mais informações sobre failover manual forçado e não planejado</span><span class="sxs-lookup"><span data-stu-id="ea0fc-223">More information about planned and forced manual failover</span></span>

<span data-ttu-id="ea0fc-224">Para obter mais informações, consulte Olá seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="ea0fc-224">For more information, see hello following topics:</span></span>

- [<span data-ttu-id="ea0fc-225">Executar um Failover Manual planejado de um grupo de disponibilidade (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="ea0fc-225">Perform a Planned Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/hh231018.aspx)
- [<span data-ttu-id="ea0fc-226">Executar um Failover Manual forçado de um grupo de disponibilidade (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="ea0fc-226">Perform a Forced Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a><span data-ttu-id="ea0fc-227">Links adicionais</span><span class="sxs-lookup"><span data-stu-id="ea0fc-227">Additional Links</span></span>

* [<span data-ttu-id="ea0fc-228">Grupos de disponibilidade AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="ea0fc-228">Always On Availability Groups</span></span>](http://msdn.microsoft.com/library/hh510230.aspx)
* [<span data-ttu-id="ea0fc-229">Máquinas Virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="ea0fc-229">Azure Virtual Machines</span></span>](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [<span data-ttu-id="ea0fc-230">Balanceadores de Carga do Azure</span><span class="sxs-lookup"><span data-stu-id="ea0fc-230">Azure Load Balancers</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [<span data-ttu-id="ea0fc-231">Conjuntos de Disponibilidade do Azure</span><span class="sxs-lookup"><span data-stu-id="ea0fc-231">Azure Availability Sets</span></span>](../manage-availability.md)
