---
title: "Recuperação de desastre - máquinas virtuais do Azure - grupos de disponibilidade do SQL Server | Microsoft Docs"
description: "Este artigo explica como configurar um grupo de disponibilidade do SQL Server em máquinas virtuais do Azure com uma réplica em uma região diferente."
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
ms.openlocfilehash: 1ce90cf4bae66bfd6387a2698fd9b1ba7fc64595
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a><span data-ttu-id="bc6b0-103">Configurar um Grupo de Disponibilidade Always On em máquinas virtuais do Azure em diferentes regiões</span><span class="sxs-lookup"><span data-stu-id="bc6b0-103">Configure an Always On availability group on Azure virtual machines in different regions</span></span>

<span data-ttu-id="bc6b0-104">Este artigo explica como configurar uma réplica do SQL Server sempre no grupo de disponibilidade em máquinas virtuais do Azure em uma localização remota do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-104">This article explains how to configure a SQL Server Always On availability group replica on Azure virtual machines in a remote Azure location.</span></span> <span data-ttu-id="bc6b0-105">Use essa configuração para dar suporte à recuperação de desastre.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-105">Use this configuration to support disaster recovery.</span></span>

<span data-ttu-id="bc6b0-106">Este artigo se aplica às máquinas virtuais do Azure no modo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-106">This article applies to Azure Virtual Machines in Resource Manager mode.</span></span>

<span data-ttu-id="bc6b0-107">A imagem a seguir mostra uma implementação comum de um grupo de disponibilidade em máquinas virtuais do Azure:</span><span class="sxs-lookup"><span data-stu-id="bc6b0-107">The following image shows a common deployment of an availability group on Azure virtual machines:</span></span>

   ![Grupo de disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

<span data-ttu-id="bc6b0-109">Nessa implantação, todas as máquinas virtuais estão em uma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-109">In this deployment, all virtual machines are in one Azure region.</span></span> <span data-ttu-id="bc6b0-110">As réplicas do grupo de disponibilidade podem ter de confirmação síncrona com failover automático no SQL-1 e SQL-2.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-110">The availability group replicas can have synchronous commit with automatic failover on SQL-1 and SQL-2.</span></span> <span data-ttu-id="bc6b0-111">Para criar essa arquitetura, veja [Modelo ou tutorial de Grupo de Disponibilidade](virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bc6b0-111">To build this architecture, see [Availability Group template or tutorial](virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

<span data-ttu-id="bc6b0-112">Essa arquitetura é vulnerável a tempo de inatividade se a região do Azure se tornar inacessível.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-112">This architecture is vulnerable to downtime if the Azure region becomes inaccessible.</span></span> <span data-ttu-id="bc6b0-113">Para superar essa vulnerabilidade, adicione uma réplica em uma região do Azure diferente.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-113">To overcome this vulnerability, add a replica in a different Azure region.</span></span> <span data-ttu-id="bc6b0-114">O diagrama a seguir mostra como a nova arquitetura:</span><span class="sxs-lookup"><span data-stu-id="bc6b0-114">The following diagram shows how the new architecture would look:</span></span>

   ![Recuperação de desastre de grupo de disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

<span data-ttu-id="bc6b0-116">O diagrama acima mostra uma nova máquina virtual chamada SQL-3.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-116">The preceding diagram shows a new virtual machine called SQL-3.</span></span> <span data-ttu-id="bc6b0-117">SQL-3 está em outra região do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-117">SQL-3 is in a different Azure region.</span></span> <span data-ttu-id="bc6b0-118">SQL-3 é adicionado para o Cluster de Failover do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-118">SQL-3 is added to the Windows Server Failover Cluster.</span></span> <span data-ttu-id="bc6b0-119">SQL-3 pode hospedar uma réplica do grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-119">SQL-3 can host an availability group replica.</span></span> <span data-ttu-id="bc6b0-120">Finalmente, observe que a região do Azure para o SQL-3 tem um novo balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-120">Finally, notice that the Azure region for SQL-3 has a new Azure load balancer.</span></span>

>[!NOTE]
> <span data-ttu-id="bc6b0-121">Um conjunto de disponibilidade do Azure é necessário quando mais de uma máquina virtual está na mesma região.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-121">An Azure availability set is required when more than one virtual machine is in the same region.</span></span> <span data-ttu-id="bc6b0-122">Se houver apenas uma máquina virtual na região, o conjunto de disponibilidade não é necessário.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-122">If only one virtual machine is in the region, then the availability set is not required.</span></span> <span data-ttu-id="bc6b0-123">Você só pode colocar uma máquina virtual em um momento da criação do conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-123">You can only place a virtual machine in an availability set at creation time.</span></span> <span data-ttu-id="bc6b0-124">Se a máquina virtual já estiver em um conjunto de disponibilidade, você poderá adicionar uma máquina virtual para fazer uma réplica adicional mais tarde.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-124">If the virtual machine is already in an availability set, you can add a virtual machine for an additional replica later.</span></span>

<span data-ttu-id="bc6b0-125">Nesta arquitetura, a réplica na região remota normalmente é configurada com o modo de disponibilidade de confirmação assíncrona e modo de failover manual.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-125">In this architecture, the replica in the remote region is normally configured with asynchronous commit availability mode and manual failover mode.</span></span>

<span data-ttu-id="bc6b0-126">Quando as réplicas de grupo de disponibilidade em máquinas virtuais do Azure em diferentes regiões do Azure, requer que cada região:</span><span class="sxs-lookup"><span data-stu-id="bc6b0-126">When availability group replicas are on Azure virtual machines in different Azure regions, each region requires:</span></span>

* <span data-ttu-id="bc6b0-127">Um gateway de rede virtual</span><span class="sxs-lookup"><span data-stu-id="bc6b0-127">A virtual network gateway</span></span>
* <span data-ttu-id="bc6b0-128">Uma conexão de gateway de rede virtual</span><span class="sxs-lookup"><span data-stu-id="bc6b0-128">A virtual network gateway connection</span></span>

<span data-ttu-id="bc6b0-129">O diagrama a seguir mostra como as redes se comunicam entre data centers.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-129">The following diagram shows how the networks communicate between data centers.</span></span>

   ![Grupo de Disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
><span data-ttu-id="bc6b0-131">Essa arquitetura incorre em encargos de dados de saída para os dados replicados entre regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-131">This architecture incurs outbound data charges for data replicated between Azure regions.</span></span> <span data-ttu-id="bc6b0-132">Veja [Preços de Largura de Banda](http://azure.microsoft.com/pricing/details/bandwidth/).</span><span class="sxs-lookup"><span data-stu-id="bc6b0-132">See [Bandwidth Pricing](http://azure.microsoft.com/pricing/details/bandwidth/).</span></span>  

## <a name="create-remote-replica"></a><span data-ttu-id="bc6b0-133">Criar réplica remota</span><span class="sxs-lookup"><span data-stu-id="bc6b0-133">Create remote replica</span></span>

<span data-ttu-id="bc6b0-134">Para criar uma réplica em um data center remoto, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="bc6b0-134">To create a replica in a remote data center, do the following steps:</span></span>

1. <span data-ttu-id="bc6b0-135">[Criar uma rede virtual na nova região](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="bc6b0-135">[Create a virtual network in the new region](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

1. <span data-ttu-id="bc6b0-136">[Configurar uma conexão de rede virtual usando o portal do Azure](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bc6b0-136">[Configure a VNet-to-VNet connection using the Azure portal](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span></span>

   >[!NOTE]
   ><span data-ttu-id="bc6b0-137">Em alguns casos, você talvez precise usar o PowerShell para criar a conexão de VNet para VNet.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-137">In some cases, you may have to use PowerShell to create the VNet-to-VNet connection.</span></span> <span data-ttu-id="bc6b0-138">Por exemplo, se você usar diferentes contas do Azure, será possível configurar a conexão no portal.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-138">For example, if you use different Azure accounts you cannot configure the connection in the portal.</span></span> <span data-ttu-id="bc6b0-139">Neste caso, veja [Configurar uma conexão de Rede Virtual para Rede Virtual usando o portal do Azure](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="bc6b0-139">In this case see, [Configure a VNet-to-VNet connection using the Azure portal](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

1. <span data-ttu-id="bc6b0-140">[Crie um controlador de domínio na nova região](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="bc6b0-140">[Create a domain controller in the new region](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span></span>

   <span data-ttu-id="bc6b0-141">Esse controlador de domínio fornecerá autenticação se o controlador de domínio no site primário não estiver disponível.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-141">This domain controller provides authentication if the domain controller in the primary site is not available.</span></span>

1. <span data-ttu-id="bc6b0-142">[Criar uma máquina virtual do SQL Server na nova região](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="bc6b0-142">[Create a SQL Server virtual machine in the new region](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

1. <span data-ttu-id="bc6b0-143">[Criar um balanceador de carga do Azure na rede em que a nova região](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="bc6b0-143">[Create an Azure load balancer in the network on the new region](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

   <span data-ttu-id="bc6b0-144">Este balanceador de carga deve:</span><span class="sxs-lookup"><span data-stu-id="bc6b0-144">This load balancer must:</span></span>

   - <span data-ttu-id="bc6b0-145">Estar na mesma rede e sub-rede como a nova máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-145">Be in the same network and subnet as the new virtual machine.</span></span>
   - <span data-ttu-id="bc6b0-146">Ter um endereço IP estático para o ouvinte do grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-146">Have a static IP address for the availability group listener.</span></span>
   - <span data-ttu-id="bc6b0-147">Inclua um pool de back-end que consiste somente as máquinas virtuais na mesma região que o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-147">Include a backend pool consisting of only the virtual machines in the same region as the load balancer.</span></span>
   - <span data-ttu-id="bc6b0-148">Use um teste de porta TCP específico para o endereço IP.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-148">Use a TCP port probe specific to the IP address.</span></span>
   - <span data-ttu-id="bc6b0-149">Ter uma regra específica para o SQL Server na mesma região balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-149">Have a load balancing rule specific to the SQL Server in the same region.</span></span>  

1. <span data-ttu-id="bc6b0-150">[Adicionar o recurso cluster de Failover para o novo servidor SQL](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="bc6b0-150">[Add Failover Clustering feature to the new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

1. <span data-ttu-id="bc6b0-151">[Adicionar o novo SQL Server ao domínio](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="bc6b0-151">[Join the new SQL Server to the domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

1. <span data-ttu-id="bc6b0-152">[Definir a nova conta de serviço do SQL Server para usar uma conta de domínio](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span><span class="sxs-lookup"><span data-stu-id="bc6b0-152">[Set the new SQL Server service account to use a domain account](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span></span>

1. <span data-ttu-id="bc6b0-153">[Adicionar o novo SQL Server para o Cluster de Failover do Windows Server](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span><span class="sxs-lookup"><span data-stu-id="bc6b0-153">[Add the new SQL Server to the Windows Server Failover Cluster](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span></span>

1. <span data-ttu-id="bc6b0-154">Crie um recurso de endereço IP do cluster.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-154">Create an IP address resource on the cluster.</span></span>

   <span data-ttu-id="bc6b0-155">Você pode criar o recurso de endereço IP no Gerenciador de Cluster de Failover.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-155">You can create the IP address resource in Failover Cluster Manager.</span></span> <span data-ttu-id="bc6b0-156">Clique a função do grupo de disponibilidade, clique em **adicionar recurso**, **mais recursos**e clique em **endereço IP**.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-156">Right-click the availability group role, click **Add Resource**, **More Resources**, and click **IP Address**.</span></span>

   ![Criar endereço IP](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   <span data-ttu-id="bc6b0-158">Configure o endereço IP da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="bc6b0-158">Configure this IP address as follows:</span></span>

   - <span data-ttu-id="bc6b0-159">Use a rede do data center remoto.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-159">Use the network from the remote data center.</span></span>
   - <span data-ttu-id="bc6b0-160">Atribua o endereço IP do balanceador de carga do Azure novo.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-160">Assign the IP address from the new Azure load balancer.</span></span> 

1. <span data-ttu-id="bc6b0-161">No novo servidor SQL no SQL Server Configuration Manager, [habilitar grupos de disponibilidade AlwaysOn](http://msdn.microsoft.com/library/ff878259.aspx).</span><span class="sxs-lookup"><span data-stu-id="bc6b0-161">On the new SQL Server in SQL Server Configuration Manager, [enable Always On Availability Groups](http://msdn.microsoft.com/library/ff878259.aspx).</span></span>

1. <span data-ttu-id="bc6b0-162">[Abrir portas de firewall no novo servidor SQL](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="bc6b0-162">[Open firewall ports on the new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

   <span data-ttu-id="bc6b0-163">Os números de porta que você precisa abrir dependem de seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-163">The port numbers you need to open depend on your environment.</span></span> <span data-ttu-id="bc6b0-164">Investigação de integridade do balanceador de carga de portas abertas para o ponto de extremidade de espelhamento e o Azure.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-164">Open ports for the mirroring endpoint and Azure load balancer health probe.</span></span>

1. <span data-ttu-id="bc6b0-165">[Adicionar uma réplica para o grupo de disponibilidade no novo servidor SQL](http://msdn.microsoft.com/library/hh213239.aspx).</span><span class="sxs-lookup"><span data-stu-id="bc6b0-165">[Add a replica to the availability group on the new SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).</span></span>

   <span data-ttu-id="bc6b0-166">Para uma réplica em uma região remota do Azure, configurá-lo para a replicação assíncrona com failover manual.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-166">For a replica in a remote Azure region, set it for asynchronous replication with manual failover.</span></span>  

1. <span data-ttu-id="bc6b0-167">Adicione o recurso de endereço IP como uma dependência para o cluster do ouvinte cliente acesso ponto (nome da rede).</span><span class="sxs-lookup"><span data-stu-id="bc6b0-167">Add the IP address resource as a dependency for the listener client access point (network name) cluster.</span></span>

   <span data-ttu-id="bc6b0-168">Captura de tela a seguir mostra um recurso de cluster de endereço IP configurado corretamente:</span><span class="sxs-lookup"><span data-stu-id="bc6b0-168">The following screenshot shows a properly configured IP address cluster resource:</span></span>

   ![Grupo de Disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   ><span data-ttu-id="bc6b0-170">O grupo de recursos de cluster inclui os dois endereços IP.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-170">The cluster resource group includes both IP addresses.</span></span> <span data-ttu-id="bc6b0-171">Os dois endereços IP são dependências para o ponto de acesso de cliente do ouvinte.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-171">Both IP addresses are dependencies for the listener client access point.</span></span> <span data-ttu-id="bc6b0-172">Use o **ou** operador na configuração de dependência do cluster.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-172">Use the **OR** operator in the cluster dependency configuration.</span></span>

1. <span data-ttu-id="bc6b0-173">[Definir os parâmetros do cluster no PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span><span class="sxs-lookup"><span data-stu-id="bc6b0-173">[Set the cluster parameters in PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span></span>

<span data-ttu-id="bc6b0-174">Execute o script do PowerShell com o nome de rede do cluster, o endereço IP e a porta de investigação configurado no balanceador de carga na nova região.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-174">Run the PowerShell script with the cluster network name, IP address, and probe port that you configured on the load balancer in the new region.</span></span>

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # The cluster name for the network in the new region (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name).
   $IPResourceName = "<IPResourceName>" # The cluster name for the new IP Address resource.
   $ILBIP = “<n.n.n.n>” # The IP Address of the Internal Load Balancer (ILB) in the new region. This is the static IP address for the load balancer you configured in the Azure portal.
   [int]$ProbePort = <nnnnn> # The probe port you set on the ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a><span data-ttu-id="bc6b0-175">Definir conexão para várias sub-redes</span><span class="sxs-lookup"><span data-stu-id="bc6b0-175">Set connection for multiple subnets</span></span>

<span data-ttu-id="bc6b0-176">A réplica no data center remoto é parte do grupo de disponibilidade, mas ele está em uma sub-rede diferente.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-176">The replica in the remote data center is part of the availability group but it is in a different subnet.</span></span> <span data-ttu-id="bc6b0-177">Se essa réplica se tornar a réplica primária, tempo limite de conexão do aplicativo podem ocorrer.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-177">If this replica becomes the primary replica, application connection time-outs may occur.</span></span> <span data-ttu-id="bc6b0-178">Esse comportamento é o mesmo que um grupo de disponibilidade local em uma implantação de várias sub-redes.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-178">This behavior is the same as an on-premises availability group in a multi-subnet deployment.</span></span> <span data-ttu-id="bc6b0-179">Para permitir conexões de cliente de aplicativos, atualize a conexão de cliente ou configurar a resolução de nome do recurso de nome de rede de cluster de cache.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-179">To allow connections from client applications, either update the client connection or configure name resolution caching on the cluster network name resource.</span></span>

<span data-ttu-id="bc6b0-180">Preferencialmente, atualize as cadeias de conexão do cliente para definir `MultiSubnetFailover=Yes`.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-180">Preferably, update the client connection strings to set `MultiSubnetFailover=Yes`.</span></span> <span data-ttu-id="bc6b0-181">Consulte [conectar-se ao MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="bc6b0-181">See [Connecting With MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span></span>

<span data-ttu-id="bc6b0-182">Se você não pode modificar as cadeias de conexão, você pode configurar o cache de resolução de nome.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-182">If you cannot modify the connection strings, you can configure name resolution caching.</span></span> <span data-ttu-id="bc6b0-183">Consulte [tempos limite de conexão no grupo de disponibilidade de várias sub-redes](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span><span class="sxs-lookup"><span data-stu-id="bc6b0-183">See [Connection Timeouts in Multi-subnet Availability Group](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span></span>

## <a name="fail-over-to-remote-region"></a><span data-ttu-id="bc6b0-184">Failover para região remota</span><span class="sxs-lookup"><span data-stu-id="bc6b0-184">Fail over to remote region</span></span>

<span data-ttu-id="bc6b0-185">Para testar a conectividade do ouvinte para a região remota, é possível realizar failover da réplica para a região remota.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-185">To test listener connectivity to the remote region, you can fail over the replica to the remote region.</span></span> <span data-ttu-id="bc6b0-186">Enquanto a réplica é assíncrona, o failover é vulnerável à perda de dados.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-186">While the replica is asynchronous, failover is vulnerable to potential data loss.</span></span> <span data-ttu-id="bc6b0-187">Para fazer failover sem perda de dados, alterar o modo de disponibilidade para síncrono e defina o modo de failover como automático.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-187">To fail over without data loss, change the availability mode to synchronous and set the failover mode to automatic.</span></span> <span data-ttu-id="bc6b0-188">Use as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="bc6b0-188">Use the following steps:</span></span>

1. <span data-ttu-id="bc6b0-189">Em **Pesquisador**, conecte-se à instância do SQL Server que hospeda a réplica primária.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-189">In **Object Explorer**, connect to the instance of SQL Server that hosts the primary replica.</span></span>
1. <span data-ttu-id="bc6b0-190">Em **grupos de disponibilidade do AlwaysOn**, **grupos de disponibilidade**, clique com botão direito seu grupo de disponibilidade e clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-190">Under **AlwaysOn Availability Groups**, **Availability Groups**, right-click your availability group and click **Properties**.</span></span>
1. <span data-ttu-id="bc6b0-191">No **geral** página, em **réplicas de disponibilidade**, definir a réplica secundária no site para usar a recuperação de desastres **confirmação síncrona** modo de disponibilidade e **automáticas** modo de failover.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-191">On the **General** page, under **Availability Replicas**, set the secondary replica in the DR site to use **Synchronous Commit** availability mode and **Automatic** failover mode.</span></span>
1. <span data-ttu-id="bc6b0-192">Se você tiver uma réplica secundária no mesmo site que a réplica primária para alta disponibilidade, definido desta réplica como **confirmação assíncrona** e **Manual**.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-192">If you have a secondary replica in same site as your primary replica for high availability, set this replica to **Asynchronous Commit** and **Manual**.</span></span>
1. <span data-ttu-id="bc6b0-193">Clique em OK.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-193">Click OK.</span></span>
1. <span data-ttu-id="bc6b0-194">Em **Pesquisador**, com o botão direito no grupo de disponibilidade e clique em **Mostrar painel**.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-194">In **Object Explorer**, right-click the availability group, and click **Show Dashboard**.</span></span>
1. <span data-ttu-id="bc6b0-195">No painel, verifique se a réplica no site de recuperação de desastre está sincronizada.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-195">On the dashboard, verify that the replica on the DR site is synchronized.</span></span>
1. <span data-ttu-id="bc6b0-196">Em **Pesquisador**, com o botão direito no grupo de disponibilidade e clique **Failover...** .</span><span class="sxs-lookup"><span data-stu-id="bc6b0-196">In **Object Explorer**, right-click the availability group, and click **Failover...**.</span></span> <span data-ttu-id="bc6b0-197">SQL Server Management Studio abre um Assistente de failover do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-197">SQL Server Management Studios opens a wizard to fail over SQL Server.</span></span>  
1. <span data-ttu-id="bc6b0-198">Clique em **Avançar** e selecione a instância do SQL Server no site de recuperação de desastre.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-198">Click **Next**, and select the SQL Server instance in the DR site.</span></span> <span data-ttu-id="bc6b0-199">Clique em **Avançar** novamente.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-199">Click **Next** again.</span></span>
1. <span data-ttu-id="bc6b0-200">Conecte-se à instância do SQL Server no site de recuperação de desastre e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-200">Connect to the SQL Server instance in the DR site and click **Next**.</span></span>
1. <span data-ttu-id="bc6b0-201">Sobre o **resumo** página, verifique as configurações e clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-201">On the **Summary** page, verify the settings and click **Finish**.</span></span>

<span data-ttu-id="bc6b0-202">Depois de testar a conectividade, mova a réplica primária de volta para seu data center principal e definir o modo de disponibilidade para suas configurações operacionais normais.</span><span class="sxs-lookup"><span data-stu-id="bc6b0-202">After testing connectivity, move the primary replica back to your primary data center and set the availability mode back to their normal operating settings.</span></span> <span data-ttu-id="bc6b0-203">A tabela a seguir mostra as configurações operacionais normais para a arquitetura descrita neste documento:</span><span class="sxs-lookup"><span data-stu-id="bc6b0-203">The following table shows the normal operational settings for the architecture described in this document:</span></span>

| <span data-ttu-id="bc6b0-204">Local</span><span class="sxs-lookup"><span data-stu-id="bc6b0-204">Location</span></span> | <span data-ttu-id="bc6b0-205">Instância do servidor</span><span class="sxs-lookup"><span data-stu-id="bc6b0-205">Server Instance</span></span> | <span data-ttu-id="bc6b0-206">Função</span><span class="sxs-lookup"><span data-stu-id="bc6b0-206">Role</span></span> | <span data-ttu-id="bc6b0-207">Modo de Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="bc6b0-207">Availability Mode</span></span> | <span data-ttu-id="bc6b0-208">Modo de failover</span><span class="sxs-lookup"><span data-stu-id="bc6b0-208">Failover Mode</span></span>
| ----- | ----- | ----- | ----- | -----
| <span data-ttu-id="bc6b0-209">Data center principal</span><span class="sxs-lookup"><span data-stu-id="bc6b0-209">Primary data center</span></span> | <span data-ttu-id="bc6b0-210">SQL-1</span><span class="sxs-lookup"><span data-stu-id="bc6b0-210">SQL-1</span></span> | <span data-ttu-id="bc6b0-211">Primário</span><span class="sxs-lookup"><span data-stu-id="bc6b0-211">Primary</span></span> | <span data-ttu-id="bc6b0-212">Síncrono</span><span class="sxs-lookup"><span data-stu-id="bc6b0-212">Synchronous</span></span> | <span data-ttu-id="bc6b0-213">Automático</span><span class="sxs-lookup"><span data-stu-id="bc6b0-213">Automatic</span></span>
| <span data-ttu-id="bc6b0-214">Data center principal</span><span class="sxs-lookup"><span data-stu-id="bc6b0-214">Primary data center</span></span> | <span data-ttu-id="bc6b0-215">SQL-2</span><span class="sxs-lookup"><span data-stu-id="bc6b0-215">SQL-2</span></span> | <span data-ttu-id="bc6b0-216">Secundário</span><span class="sxs-lookup"><span data-stu-id="bc6b0-216">Secondary</span></span> | <span data-ttu-id="bc6b0-217">Síncrono</span><span class="sxs-lookup"><span data-stu-id="bc6b0-217">Synchronous</span></span> | <span data-ttu-id="bc6b0-218">Automático</span><span class="sxs-lookup"><span data-stu-id="bc6b0-218">Automatic</span></span>
| <span data-ttu-id="bc6b0-219">Centro de dados remotos ou secundários</span><span class="sxs-lookup"><span data-stu-id="bc6b0-219">Secondary or remote data center</span></span> | <span data-ttu-id="bc6b0-220">SQL-3</span><span class="sxs-lookup"><span data-stu-id="bc6b0-220">SQL-3</span></span> | <span data-ttu-id="bc6b0-221">Secundário</span><span class="sxs-lookup"><span data-stu-id="bc6b0-221">Secondary</span></span> | <span data-ttu-id="bc6b0-222">Assíncrono</span><span class="sxs-lookup"><span data-stu-id="bc6b0-222">Asynchronous</span></span> | <span data-ttu-id="bc6b0-223">Manual</span><span class="sxs-lookup"><span data-stu-id="bc6b0-223">Manual</span></span>


### <a name="more-information-about-planned-and-forced-manual-failover"></a><span data-ttu-id="bc6b0-224">Para obter mais informações sobre failover manual forçado e não planejado</span><span class="sxs-lookup"><span data-stu-id="bc6b0-224">More information about planned and forced manual failover</span></span>

<span data-ttu-id="bc6b0-225">Para saber mais, consulte os tópicos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bc6b0-225">For more information, see the following topics:</span></span>

- [<span data-ttu-id="bc6b0-226">Executar um Failover Manual planejado de um grupo de disponibilidade (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="bc6b0-226">Perform a Planned Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/hh231018.aspx)
- [<span data-ttu-id="bc6b0-227">Executar um Failover Manual forçado de um grupo de disponibilidade (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="bc6b0-227">Perform a Forced Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a><span data-ttu-id="bc6b0-228">Links adicionais</span><span class="sxs-lookup"><span data-stu-id="bc6b0-228">Additional Links</span></span>

* [<span data-ttu-id="bc6b0-229">Grupos de disponibilidade AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="bc6b0-229">Always On Availability Groups</span></span>](http://msdn.microsoft.com/library/hh510230.aspx)
* [<span data-ttu-id="bc6b0-230">Máquinas Virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="bc6b0-230">Azure Virtual Machines</span></span>](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [<span data-ttu-id="bc6b0-231">Balanceadores de Carga do Azure</span><span class="sxs-lookup"><span data-stu-id="bc6b0-231">Azure Load Balancers</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [<span data-ttu-id="bc6b0-232">Conjuntos de Disponibilidade do Azure</span><span class="sxs-lookup"><span data-stu-id="bc6b0-232">Azure Availability Sets</span></span>](../manage-availability.md)
