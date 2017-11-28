---
title: "Criar um ouvinte do grupo de disponibilidade do SQL Server nas máquinas virtuais do Azure | Microsoft Docs"
description: "Instruções passo a passo de como criar um ouvinte para um grupo de disponibilidade Always On para SQL Server em máquinas virtuais do Azure"
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: d1f291e9-9af2-41ba-9d29-9541e3adcfcf
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/01/2017
ms.author: mikeray
ms.openlocfilehash: 09fed7e785708d4afe64905de973becc188181d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-load-balancer-for-an-always-on-availability-group-in-azure"></a><span data-ttu-id="54ac0-103">Configurar um balanceador de carga para um grupo de disponibilidade Always On no Azure</span><span class="sxs-lookup"><span data-stu-id="54ac0-103">Configure a load balancer for an Always On availability group in Azure</span></span>
<span data-ttu-id="54ac0-104">Este artigo explica como criar um balanceador de carga para um grupo de disponibilidade Always On do SQL Server em máquinas virtuais do Azure em execução com o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="54ac0-104">This article explains how to create a load balancer for a SQL Server Always On availability group in Azure virtual machines that are running with Azure Resource Manager.</span></span> <span data-ttu-id="54ac0-105">Um grupo de disponibilidade exige um balanceador de carga quando as instâncias do SQL Server estão em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="54ac0-105">An availability group requires a load balancer when the SQL Server instances are on Azure virtual machines.</span></span> <span data-ttu-id="54ac0-106">O balanceador de carga armazena o endereço IP do ouvinte do grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="54ac0-106">The load balancer stores the IP address for the availability group listener.</span></span> <span data-ttu-id="54ac0-107">Se um grupo de disponibilidade abranger várias regiões, cada região precisará de um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="54ac0-107">If an availability group spans multiple regions, each region needs a load balancer.</span></span>

<span data-ttu-id="54ac0-108">Para concluir essa tarefa, você precisa ter um grupo de disponibilidade do SQL Server implantado em máquinas virtuais do Azure em execução com o Resource Manager .</span><span class="sxs-lookup"><span data-stu-id="54ac0-108">To complete this task, you need to have a SQL Server availability group deployed on Azure virtual machines that are running with Resource Manager.</span></span> <span data-ttu-id="54ac0-109">As máquinas virtuais do SQL Server devem pertencer ao mesmo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="54ac0-109">Both SQL Server virtual machines must belong to the same availability set.</span></span> <span data-ttu-id="54ac0-110">Você pode usar o [modelo da Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) para criar automaticamente o grupo de disponibilidade no Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="54ac0-110">You can use the [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) to automatically create the availability group in Resource Manager.</span></span> <span data-ttu-id="54ac0-111">Este modelo cria automaticamente um balanceador de carga interno para você.</span><span class="sxs-lookup"><span data-stu-id="54ac0-111">This template automatically creates an internal load balancer for you.</span></span> 

<span data-ttu-id="54ac0-112">Se preferir, você poderá [configurar manualmente um grupo de disponibilidade](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="54ac0-112">If you prefer, you can [manually configure an availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="54ac0-113">Este artigo exige que os grupos de disponibilidade já estejam configurados.</span><span class="sxs-lookup"><span data-stu-id="54ac0-113">This article requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="54ac0-114">Os tópicos relacionados incluem:</span><span class="sxs-lookup"><span data-stu-id="54ac0-114">Related topics include:</span></span>

* [<span data-ttu-id="54ac0-115">Configurar os grupos de disponibilidade Always On na VM do Azure (GUI)</span><span class="sxs-lookup"><span data-stu-id="54ac0-115">Configure Always On availability groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="54ac0-116">Configurar uma conexão de rede virtual com rede virtual usando o PowerShell e o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="54ac0-116">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

<span data-ttu-id="54ac0-117">Ao seguir este artigo, você cria e configura um balanceador de carga no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="54ac0-117">By walking through this article, you create and configure a load balancer in the Azure portal.</span></span> <span data-ttu-id="54ac0-118">Após a conclusão desse processo, você configura o cluster para usar o endereço IP do balanceador de carga no ouvinte do grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="54ac0-118">After the process is complete, you configure the cluster to use the IP address from the load balancer for the availability group listener.</span></span>

## <a name="create-and-configure-the-load-balancer-in-the-azure-portal"></a><span data-ttu-id="54ac0-119">Criar e configurar o balanceador de carga no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="54ac0-119">Create and configure the load balancer in the Azure portal</span></span>
<span data-ttu-id="54ac0-120">Nesta parte da tarefa, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="54ac0-120">In this portion of the task, do the following:</span></span>

1. <span data-ttu-id="54ac0-121">No Portal do Azure, crie o balanceador de carga e configure o endereço IP.</span><span class="sxs-lookup"><span data-stu-id="54ac0-121">In the Azure portal, create the load balancer and configure the IP address.</span></span>
2. <span data-ttu-id="54ac0-122">Configure o pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="54ac0-122">Configure the back-end pool.</span></span>
3. <span data-ttu-id="54ac0-123">Crie a investigação.</span><span class="sxs-lookup"><span data-stu-id="54ac0-123">Create the probe.</span></span> 
4. <span data-ttu-id="54ac0-124">Definir as regras de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="54ac0-124">Set the load balancing rules.</span></span>

> [!NOTE]
> <span data-ttu-id="54ac0-125">Se as instâncias do SQL Server estiverem em vários grupos de recursos e regiões, execute cada etapa duas vezes, uma vez em cada grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="54ac0-125">If the SQL Server instances are in multiple resource groups and regions, perform each step twice, once in each resource group.</span></span>
> 
> 

### <a name="step-1-create-the-load-balancer-and-configure-the-ip-address"></a><span data-ttu-id="54ac0-126">Etapa 1: Criar o balanceador de carga e configurar o endereço IP</span><span class="sxs-lookup"><span data-stu-id="54ac0-126">Step 1: Create the load balancer and configure the IP address</span></span>
<span data-ttu-id="54ac0-127">Primeiro, crie o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="54ac0-127">First, create the load balancer.</span></span> 

1. <span data-ttu-id="54ac0-128">No Portal do Azure, abra o grupo de recursos que contém as máquinas virtuais do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="54ac0-128">In the Azure portal, open the resource group that contains the SQL Server virtual machines.</span></span> 

2. <span data-ttu-id="54ac0-129">No grupo de recursos, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-129">In the resource group, click **Add**.</span></span>

3. <span data-ttu-id="54ac0-130">Pesquise por **balanceador de carga** e, em seguida, nos resultados da pesquisa, selecione **Balanceador de Carga**, que é publicado pela **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-130">Search for **load balancer** and then, in the search results, select **Load Balancer**, which is published by **Microsoft**.</span></span>

4. <span data-ttu-id="54ac0-131">Na folha **Balanceador de Carga**, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-131">On the **Load Balancer** blade, click **Create**.</span></span>

5. <span data-ttu-id="54ac0-132">Na caixa de diálogo **Criar balanceador de carga**, configure o balanceador de carga da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="54ac0-132">In the **Create load balancer** dialog box, configure the load balancer as follows:</span></span>

   | <span data-ttu-id="54ac0-133">Configuração</span><span class="sxs-lookup"><span data-stu-id="54ac0-133">Setting</span></span> | <span data-ttu-id="54ac0-134">Valor</span><span class="sxs-lookup"><span data-stu-id="54ac0-134">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="54ac0-135">**Nome**</span><span class="sxs-lookup"><span data-stu-id="54ac0-135">**Name**</span></span> |<span data-ttu-id="54ac0-136">Um nome de texto que representa o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="54ac0-136">A text name representing the load balancer.</span></span> <span data-ttu-id="54ac0-137">Por exemplo, **sqlLB**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-137">For example, **sqlLB**.</span></span> |
   | <span data-ttu-id="54ac0-138">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="54ac0-138">**Type**</span></span> |<span data-ttu-id="54ac0-139">**Interno**: a maioria das implementações usa um balanceador de carga interno que permite a conexão dos aplicativos dentro da mesma rede virtual ao grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="54ac0-139">**Internal**: Most implementations use an internal load balancer, which allows applications within the same virtual network to connect to the availability group.</span></span>  </br> <span data-ttu-id="54ac0-140">**Externo**: permite que os aplicativos se conectem ao grupo de disponibilidade por meio de uma conexão de Internet pública.</span><span class="sxs-lookup"><span data-stu-id="54ac0-140">**External**: Allows applications to connect to the availability group through a public Internet connection.</span></span> |
   | <span data-ttu-id="54ac0-141">**Rede virtual**</span><span class="sxs-lookup"><span data-stu-id="54ac0-141">**Virtual network**</span></span> |<span data-ttu-id="54ac0-142">Selecione a rede virtual na qual estão as instâncias do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="54ac0-142">Select the virtual network that the SQL Server intances are in.</span></span> |
   | <span data-ttu-id="54ac0-143">**Sub-rede**</span><span class="sxs-lookup"><span data-stu-id="54ac0-143">**Subnet**</span></span> |<span data-ttu-id="54ac0-144">Selecione a sub-rede na qual estão as instâncias do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="54ac0-144">Select the subnet that the SQL Server instances are in.</span></span> |
   | <span data-ttu-id="54ac0-145">**Atribuição de endereço IP**</span><span class="sxs-lookup"><span data-stu-id="54ac0-145">**IP address assignment**</span></span> |<span data-ttu-id="54ac0-146">**Estático**</span><span class="sxs-lookup"><span data-stu-id="54ac0-146">**Static**</span></span> |
   | <span data-ttu-id="54ac0-147">**Endereço IP privado**</span><span class="sxs-lookup"><span data-stu-id="54ac0-147">**Private IP address**</span></span> |<span data-ttu-id="54ac0-148">Especifique um endereço IP disponível na sub-rede.</span><span class="sxs-lookup"><span data-stu-id="54ac0-148">Specify an available IP address from the subnet.</span></span> <span data-ttu-id="54ac0-149">Você usa esse endereço IP ao criar um ouvinte no cluster.</span><span class="sxs-lookup"><span data-stu-id="54ac0-149">Use this IP address when you create a listener on the cluster.</span></span> <span data-ttu-id="54ac0-150">Em um script do PowerShell posterior neste artigo, use esse endereço para a variável `$ILBIP`.</span><span class="sxs-lookup"><span data-stu-id="54ac0-150">In a PowerShell script, later in this article, use this address for the `$ILBIP` variable.</span></span> |
   | <span data-ttu-id="54ac0-151">**Assinatura**</span><span class="sxs-lookup"><span data-stu-id="54ac0-151">**Subscription**</span></span> |<span data-ttu-id="54ac0-152">Se você tiver várias assinaturas, este campo poderá aparecer.</span><span class="sxs-lookup"><span data-stu-id="54ac0-152">If you have multiple subscriptions, this field might appear.</span></span> <span data-ttu-id="54ac0-153">Selecione a assinatura que você deseja associar a esse recurso.</span><span class="sxs-lookup"><span data-stu-id="54ac0-153">Select the subscription that you want to associate with this resource.</span></span> <span data-ttu-id="54ac0-154">Normalmente, trata-se da mesma assinatura de todos os recursos do grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="54ac0-154">It is normally the same subscription as all the resources for the availability group.</span></span> |
   | <span data-ttu-id="54ac0-155">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="54ac0-155">**Resource group**</span></span> |<span data-ttu-id="54ac0-156">Selecione o grupo de recursos no qual estão as instâncias do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="54ac0-156">Select the resource group that the SQL Server instances are in.</span></span> |
   | <span data-ttu-id="54ac0-157">**Localidade**</span><span class="sxs-lookup"><span data-stu-id="54ac0-157">**Location**</span></span> |<span data-ttu-id="54ac0-158">Selecione o local do Azure no qual estão as instâncias do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="54ac0-158">Select the Azure location that the SQL Server instances are in.</span></span> |

6. <span data-ttu-id="54ac0-159">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-159">Click **Create**.</span></span> 

<span data-ttu-id="54ac0-160">O Azure cria o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="54ac0-160">Azure creates the load balancer.</span></span> <span data-ttu-id="54ac0-161">O balanceador de carga pertence a uma rede, sub-rede, grupo de recursos e local específicos.</span><span class="sxs-lookup"><span data-stu-id="54ac0-161">The load balancer belongs to a specific network, subnet, resource group, and location.</span></span> <span data-ttu-id="54ac0-162">Após o Azure concluir a tarefa, verifique as configurações do balanceador de carga no Azure.</span><span class="sxs-lookup"><span data-stu-id="54ac0-162">After Azure completes the task, verify the load balancer settings in Azure.</span></span> 

### <a name="step-2-configure-the-back-end-pool"></a><span data-ttu-id="54ac0-163">Etapa 2: Configurar o pool de back-ends</span><span class="sxs-lookup"><span data-stu-id="54ac0-163">Step 2: Configure the back-end pool</span></span>
<span data-ttu-id="54ac0-164">O Azure chama o *pool de back-ends* do pool de endereços back-end.</span><span class="sxs-lookup"><span data-stu-id="54ac0-164">Azure calls the back-end address pool *backend pool*.</span></span> <span data-ttu-id="54ac0-165">Nesse caso, o pool de back-ends é composto por endereços das duas instâncias do SQL Server em seu grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="54ac0-165">In this case, the back-end pool is the addresses of the two SQL Server instances in your availability group.</span></span> 

1. <span data-ttu-id="54ac0-166">No grupo de recursos, clique no balanceador de carga que você criou.</span><span class="sxs-lookup"><span data-stu-id="54ac0-166">In your resource group, click the load balancer that you created.</span></span> 

2. <span data-ttu-id="54ac0-167">Em **Configurações**, clique em **Pools de back-end**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-167">On **Settings**, click **Backend pools**.</span></span>

3. <span data-ttu-id="54ac0-168">Em **Pools de back-end**, clique em **Adicionar** para criar um pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="54ac0-168">On **Backend pools**, click **Add** to create a back-end address pool.</span></span> 

4. <span data-ttu-id="54ac0-169">Em **Adicionar pool de back-ends**, sob **Nome**, digite um nome para o pool de back-ends.</span><span class="sxs-lookup"><span data-stu-id="54ac0-169">On **Add backend pool**, under **Name**, type a name for the back-end pool.</span></span>

5. <span data-ttu-id="54ac0-170">Em **Máquinas virtuais**, clique em **Adicionar uma máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-170">Under **Virtual machines**, click **Add a virtual machine**.</span></span> 

6. <span data-ttu-id="54ac0-171">Em **Escolher máquinas virtuais**, clique em **Escolher um conjunto de disponibilidade** e especifique o conjunto de disponibilidade ao qual as máquinas virtuais do SQL Server pertencem.</span><span class="sxs-lookup"><span data-stu-id="54ac0-171">Under **Choose virtual machines**, click **Choose an availability set**, and then specify the availability set that the SQL Server virtual machines belong to.</span></span>

7. <span data-ttu-id="54ac0-172">Depois de escolher o conjunto de disponibilidade, clique em **Escolher as máquinas virtuais**, selecione as duas máquinas virtuais que hospedam as instâncias do SQL Server no grupo de disponibilidade e clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-172">After you have chosen the availability set, click **Choose the virtual machines**, select the two virtual machines that host the SQL Server instances in the availability group, and then click **Select**.</span></span> 

8. <span data-ttu-id="54ac0-173">Clique em **OK** para fechar as folhas para **Escolher as máquinas virtuais** e, então, em **Adicionar pool de back-end**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-173">Click **OK** to close the blades for **Choose virtual machines**, and **Add backend pool**.</span></span> 

<span data-ttu-id="54ac0-174">O Azure atualiza as configurações para o pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="54ac0-174">Azure updates the settings for the back-end address pool.</span></span> <span data-ttu-id="54ac0-175">Agora seu conjunto de disponibilidade tem um pool de duas instâncias do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="54ac0-175">Now your availability set has a pool of two SQL Server instances.</span></span>

### <a name="step-3-create-a-probe"></a><span data-ttu-id="54ac0-176">Etapa 3: Criar uma investigação</span><span class="sxs-lookup"><span data-stu-id="54ac0-176">Step 3: Create a probe</span></span>
<span data-ttu-id="54ac0-177">A investigação define como o Azure verifica qual das instâncias do SQL Server é proprietária atual do ouvinte do grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="54ac0-177">The probe defines how Azure verifies which of the SQL Server instances currently owns the availability group listener.</span></span> <span data-ttu-id="54ac0-178">O Azure investiga o serviço com base no endereço IP em uma porta que você define quando cria o teste.</span><span class="sxs-lookup"><span data-stu-id="54ac0-178">Azure probes the service based on the IP address on a port that you define when you create the probe.</span></span>

1. <span data-ttu-id="54ac0-179">Na folha **Configurações** do balanceador de carga, clique em **Investigações de integridade**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-179">On the load balancer **Settings** blade, click **Health probes**.</span></span> 

2. <span data-ttu-id="54ac0-180">Na folha **Investigações de integridade**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-180">On the **Health probes** blade, click **Add**.</span></span>

3. <span data-ttu-id="54ac0-181">Configure a investigação na folha **Adicionar investigação** .</span><span class="sxs-lookup"><span data-stu-id="54ac0-181">Configure the probe on the **Add probe** blade.</span></span> <span data-ttu-id="54ac0-182">Use os valores a seguir para configurar a investigação:</span><span class="sxs-lookup"><span data-stu-id="54ac0-182">Use the following values to configure the probe:</span></span>

   | <span data-ttu-id="54ac0-183">Configuração</span><span class="sxs-lookup"><span data-stu-id="54ac0-183">Setting</span></span> | <span data-ttu-id="54ac0-184">Valor</span><span class="sxs-lookup"><span data-stu-id="54ac0-184">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="54ac0-185">**Nome**</span><span class="sxs-lookup"><span data-stu-id="54ac0-185">**Name**</span></span> |<span data-ttu-id="54ac0-186">Um nome de texto que representa a investigação.</span><span class="sxs-lookup"><span data-stu-id="54ac0-186">A text name representing the probe.</span></span> <span data-ttu-id="54ac0-187">Por exemplo, **SQLAlwaysOnEndPointProbe**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-187">For example, **SQLAlwaysOnEndPointProbe**.</span></span> |
   | <span data-ttu-id="54ac0-188">**Protocolo**</span><span class="sxs-lookup"><span data-stu-id="54ac0-188">**Protocol**</span></span> |<span data-ttu-id="54ac0-189">**TCP**</span><span class="sxs-lookup"><span data-stu-id="54ac0-189">**TCP**</span></span> |
   | <span data-ttu-id="54ac0-190">**Porta**</span><span class="sxs-lookup"><span data-stu-id="54ac0-190">**Port**</span></span> |<span data-ttu-id="54ac0-191">Você pode usar qualquer porta disponível.</span><span class="sxs-lookup"><span data-stu-id="54ac0-191">You can use any available port.</span></span> <span data-ttu-id="54ac0-192">Por exemplo, *59999*.</span><span class="sxs-lookup"><span data-stu-id="54ac0-192">For example, *59999*.</span></span> |
   | <span data-ttu-id="54ac0-193">**Intervalo**</span><span class="sxs-lookup"><span data-stu-id="54ac0-193">**Interval**</span></span> |<span data-ttu-id="54ac0-194">*5*</span><span class="sxs-lookup"><span data-stu-id="54ac0-194">*5*</span></span> |
   | <span data-ttu-id="54ac0-195">**Limite não íntegro**</span><span class="sxs-lookup"><span data-stu-id="54ac0-195">**Unhealthy threshold**</span></span> |<span data-ttu-id="54ac0-196">*2*</span><span class="sxs-lookup"><span data-stu-id="54ac0-196">*2*</span></span> |

4.  <span data-ttu-id="54ac0-197">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-197">Click **OK**.</span></span> 

> [!NOTE]
> <span data-ttu-id="54ac0-198">Verifique se a porta especificada está aberta no firewall das duas instâncias do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="54ac0-198">Make sure that the port you specify is open on the firewall of both SQL Server instances.</span></span> <span data-ttu-id="54ac0-199">As duas instâncias exigem uma regra de entrada para a porta TCP que você usa.</span><span class="sxs-lookup"><span data-stu-id="54ac0-199">Both instances require an inbound rule for the TCP port that you use.</span></span> <span data-ttu-id="54ac0-200">Para saber mais, confira [Adicionar ou editar regra de firewall](http://technet.microsoft.com/library/cc753558.aspx).</span><span class="sxs-lookup"><span data-stu-id="54ac0-200">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span> 
> 
> 

<span data-ttu-id="54ac0-201">O Azure cria a investigação e a usa para testar qual instância do SQL Server tem o ouvinte do grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="54ac0-201">Azure creates the probe and then uses it to test which SQL Server instance has the listener for the availability group.</span></span>

### <a name="step-4-set-the-load-balancing-rules"></a><span data-ttu-id="54ac0-202">Etapa 4: Definir as regras de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="54ac0-202">Step 4: Set the load balancing rules</span></span>
<span data-ttu-id="54ac0-203">As regras de balanceamento de carga configuram como o balanceador de carga encaminha o tráfego para as instâncias do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="54ac0-203">The load balancing rules configure how the load balancer routes traffic to the SQL Server instances.</span></span> <span data-ttu-id="54ac0-204">Para este balanceador de carga, habilite o retorno de servidor direto, pois somente uma das duas instâncias do SQL Servers é proprietária do recurso de ouvinte do grupo de disponibilidade por vez.</span><span class="sxs-lookup"><span data-stu-id="54ac0-204">For this load balancer, you enable direct server return because only one of the two SQL Server instances owns the availability group listener resource at a time.</span></span>

1. <span data-ttu-id="54ac0-205">Na folha **Configurações** do balanceador de carga, clique em **Regras de balanceamento de carga**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-205">On the load balancer **Settings** blade, click **Load balancing rules**.</span></span> 

2. <span data-ttu-id="54ac0-206">Na folha **Regras de balanceamento de carga**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-206">On the **Load balancing rules** blade, click **Add**.</span></span>

3. <span data-ttu-id="54ac0-207">Na folha **Adicionar regras de balanceamento de carga**, configure a regra de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="54ac0-207">On the **Add load balancing rules** blade, configure the load balancing rule.</span></span> <span data-ttu-id="54ac0-208">Use as configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="54ac0-208">Use the following settings:</span></span> 

   | <span data-ttu-id="54ac0-209">Configuração</span><span class="sxs-lookup"><span data-stu-id="54ac0-209">Setting</span></span> | <span data-ttu-id="54ac0-210">Valor</span><span class="sxs-lookup"><span data-stu-id="54ac0-210">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="54ac0-211">**Nome**</span><span class="sxs-lookup"><span data-stu-id="54ac0-211">**Name**</span></span> |<span data-ttu-id="54ac0-212">Um nome de texto que representa as regras de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="54ac0-212">A text name representing the load balancing rules.</span></span> <span data-ttu-id="54ac0-213">Por exemplo, **SQLAlwaysOnEndPointListener**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-213">For example, **SQLAlwaysOnEndPointListener**.</span></span> |
   | <span data-ttu-id="54ac0-214">**Protocolo**</span><span class="sxs-lookup"><span data-stu-id="54ac0-214">**Protocol**</span></span> |<span data-ttu-id="54ac0-215">**TCP**</span><span class="sxs-lookup"><span data-stu-id="54ac0-215">**TCP**</span></span> |
   | <span data-ttu-id="54ac0-216">**Porta**</span><span class="sxs-lookup"><span data-stu-id="54ac0-216">**Port**</span></span> |<span data-ttu-id="54ac0-217">*1433*</span><span class="sxs-lookup"><span data-stu-id="54ac0-217">*1433*</span></span> |
   | <span data-ttu-id="54ac0-218">**Porta de back-end**</span><span class="sxs-lookup"><span data-stu-id="54ac0-218">**Backend Port**</span></span> |<span data-ttu-id="54ac0-219">*1433*. Esse valor é ignorado porque essa regra usa **IP flutuante (retorno de servidor direto)**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-219">*1433*. This value is ignored because this rule uses **Floating IP (direct server return)**.</span></span> |
   | <span data-ttu-id="54ac0-220">**Investigação**</span><span class="sxs-lookup"><span data-stu-id="54ac0-220">**Probe**</span></span> |<span data-ttu-id="54ac0-221">Use o nome da investigação que você criou para este balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="54ac0-221">Use the name of the probe that you created for this load balancer.</span></span> |
   | <span data-ttu-id="54ac0-222">**Persistência de sessão**</span><span class="sxs-lookup"><span data-stu-id="54ac0-222">**Session persistence**</span></span> |<span data-ttu-id="54ac0-223">**Nenhum**</span><span class="sxs-lookup"><span data-stu-id="54ac0-223">**None**</span></span> |
   | <span data-ttu-id="54ac0-224">**Tempo limite de ociosidade (minutos)**</span><span class="sxs-lookup"><span data-stu-id="54ac0-224">**Idle timeout (minutes)**</span></span> |<span data-ttu-id="54ac0-225">*4*</span><span class="sxs-lookup"><span data-stu-id="54ac0-225">*4*</span></span> |
   | <span data-ttu-id="54ac0-226">**IP flutuante (retorno de servidor direto)**</span><span class="sxs-lookup"><span data-stu-id="54ac0-226">**Floating IP (direct server return)**</span></span> |<span data-ttu-id="54ac0-227">**Habilitado**</span><span class="sxs-lookup"><span data-stu-id="54ac0-227">**Enabled**</span></span> |

   > [!NOTE]
   > <span data-ttu-id="54ac0-228">Talvez você precise rolar a folha para baixo para ver todas as configurações.</span><span class="sxs-lookup"><span data-stu-id="54ac0-228">You might have to scroll down the blade to view all the settings.</span></span>
   > 

4. <span data-ttu-id="54ac0-229">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-229">Click **OK**.</span></span> 
5. <span data-ttu-id="54ac0-230">O Azure configura a regra de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="54ac0-230">Azure configures the load balancing rule.</span></span> <span data-ttu-id="54ac0-231">Agora, o balanceador de carga está configurado para rotear o tráfego para a instância do SQL Server que hospeda o ouvinte para o grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="54ac0-231">Now the load balancer is configured to route traffic to the SQL Server instance that hosts the listener for the availability group.</span></span> 

<span data-ttu-id="54ac0-232">Neste ponto, o grupo de recursos tem um balanceador de carga que se conecta em ambas as máquinas do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="54ac0-232">At this point, the resource group has a load balancer that connects to both SQL Server machines.</span></span> <span data-ttu-id="54ac0-233">O balanceador de carga também contém um endereço IP para o ouvinte do grupo de disponibilidade AlwaysOn do SQL Server para que o computador possa responder às solicitações para os grupos de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="54ac0-233">The load balancer also contains an IP address for the SQL Server Always On availability group listener, so that either machine can respond to requests for the availability groups.</span></span>

> [!NOTE]
> <span data-ttu-id="54ac0-234">Se suas instâncias do SQL Server estiverem em duas regiões separadas, repita as etapas na outra região.</span><span class="sxs-lookup"><span data-stu-id="54ac0-234">If your SQL Server instances are in two separate regions, repeat the steps in the other region.</span></span> <span data-ttu-id="54ac0-235">Cada região exige um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="54ac0-235">Each region requires a load balancer.</span></span> 
> 
> 

## <a name="configure-the-cluster-to-use-the-load-balancer-ip-address"></a><span data-ttu-id="54ac0-236">Configure o cluster para usar o endereço IP do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="54ac0-236">Configure the cluster to use the load balancer IP address</span></span>
<span data-ttu-id="54ac0-237">A próxima etapa é configurar o ouvinte no cluster e colocar o ouvinte online.</span><span class="sxs-lookup"><span data-stu-id="54ac0-237">The next step is to configure the listener on the cluster, and bring the listener online.</span></span> <span data-ttu-id="54ac0-238">Faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="54ac0-238">Do the following:</span></span> 

1. <span data-ttu-id="54ac0-239">Crie o ouvinte do grupo de disponibilidade no cluster de failover.</span><span class="sxs-lookup"><span data-stu-id="54ac0-239">Create the availability group listener on the failover cluster.</span></span> 

2. <span data-ttu-id="54ac0-240">Coloque o ouvinte online.</span><span class="sxs-lookup"><span data-stu-id="54ac0-240">Bring the listener online.</span></span>

### <a name="step-5-create-the-availability-group-listener-on-the-failover-cluster"></a><span data-ttu-id="54ac0-241">Etapa 5: Criar o ouvinte do grupo de disponibilidade no cluster de failover</span><span class="sxs-lookup"><span data-stu-id="54ac0-241">Step 5: Create the availability group listener on the failover cluster</span></span>
<span data-ttu-id="54ac0-242">Nesta etapa, você cria manualmente o ouvinte do grupo de disponibilidade no Gerenciador de Cluster de Failover e no Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="54ac0-242">In this step, you manually create the availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

### <a name="verify-the-configuration-of-the-listener"></a><span data-ttu-id="54ac0-243">Verifique a configuração do ouvinte</span><span class="sxs-lookup"><span data-stu-id="54ac0-243">Verify the configuration of the listener</span></span>

<span data-ttu-id="54ac0-244">Se os recursos e as dependências do cluster forem configurados corretamente, você poderá ver o ouvinte no SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="54ac0-244">If the cluster resources and dependencies are correctly configured, you should be able to view the listener in SQL Server Management Studio.</span></span> <span data-ttu-id="54ac0-245">Para definir a porta do ouvinte, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="54ac0-245">To set the listener port, do the following:</span></span>

1. <span data-ttu-id="54ac0-246">Inicie o SQL Server Management Studio e conecte-se à réplica principal.</span><span class="sxs-lookup"><span data-stu-id="54ac0-246">Start SQL Server Management Studio, and then connect to the primary replica.</span></span>

2. <span data-ttu-id="54ac0-247">Vá até **Alta Disponibilidade do AlwaysOn** > **Grupos de Disponibilidade** > **Ouvintes do Grupo de Disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-247">Go to **AlwaysOn High Availability** > **Availability Groups** > **Availability Group Listeners**.</span></span>  
    <span data-ttu-id="54ac0-248">Agora você deve ver o nome do ouvinte que você criou no Gerenciador de Cluster de Failover.</span><span class="sxs-lookup"><span data-stu-id="54ac0-248">You should now see the listener name that you created in Failover Cluster Manager.</span></span> 

3. <span data-ttu-id="54ac0-249">Clique com o botão direito do mouse no nome do ouvinte e, em seguida, clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-249">Right-click the listener name, and then click **Properties**.</span></span>

4. <span data-ttu-id="54ac0-250">Na caixa **Porta**, especifique o número da porta para o ouvinte do grupo de disponibilidade usando o $EndpointPort usado anteriormente (1433 era o padrão) e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-250">In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort you used earlier (1433 was the default), and then click **OK**.</span></span>

<span data-ttu-id="54ac0-251">Agora você tem um grupo de disponibilidade nas máquinas virtuais do Azure em execução no modo Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="54ac0-251">You now have an availability group in Azure virtual machines running in Resource Manager mode.</span></span> 

## <a name="test-the-connection-to-the-listener"></a><span data-ttu-id="54ac0-252">Testar a conexão com o ouvinte</span><span class="sxs-lookup"><span data-stu-id="54ac0-252">Test the connection to the listener</span></span>
<span data-ttu-id="54ac0-253">Teste a conexão fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="54ac0-253">Test the connection by doing the following:</span></span>

1. <span data-ttu-id="54ac0-254">RDP para uma instância do SQL Server que está na mesma rede virtual, mas não é proprietário da réplica.</span><span class="sxs-lookup"><span data-stu-id="54ac0-254">RDP to a SQL Server instance that is in the same virtual network, but does not own the replica.</span></span> <span data-ttu-id="54ac0-255">Esse servidor pode ser a outra instância do SQL Server no cluster.</span><span class="sxs-lookup"><span data-stu-id="54ac0-255">This server can be the other SQL Server instance in the cluster.</span></span>

2. <span data-ttu-id="54ac0-256">Use o utilitário **sqlcmd** para testar a conexão.</span><span class="sxs-lookup"><span data-stu-id="54ac0-256">Use **sqlcmd** utility to test the connection.</span></span> <span data-ttu-id="54ac0-257">Por exemplo, o script a seguir estabelece uma conexão de **sqlcmd** com a réplica primária por meio do ouvinte com autenticação do Windows:</span><span class="sxs-lookup"><span data-stu-id="54ac0-257">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span></span>
   
        sqlcmd -S <listenerName> -E

<span data-ttu-id="54ac0-258">A conexão SQLCMD se conecta automaticamente a qualquer instância do SQL Server que hospede a réplica primária.</span><span class="sxs-lookup"><span data-stu-id="54ac0-258">The SQLCMD connection automatically connects to the SQL Server instance that hosts the primary replica.</span></span> 

## <a name="create-an-ip-address-for-an-additional-availability-group"></a><span data-ttu-id="54ac0-259">Criar um endereço IP para um grupo de disponibilidade adicional</span><span class="sxs-lookup"><span data-stu-id="54ac0-259">Create an IP address for an additional availability group</span></span>

<span data-ttu-id="54ac0-260">Cada grupo de disponibilidade usa um ouvinte separado.</span><span class="sxs-lookup"><span data-stu-id="54ac0-260">Each availability group uses a separate listener.</span></span> <span data-ttu-id="54ac0-261">Cada ouvinte tem seu próprio endereço IP.</span><span class="sxs-lookup"><span data-stu-id="54ac0-261">Each listener has its own IP address.</span></span> <span data-ttu-id="54ac0-262">Use o mesmo balanceador de carga para manter o endereço IP para ouvintes adicionais.</span><span class="sxs-lookup"><span data-stu-id="54ac0-262">Use the same load balancer to hold the IP address for additional listeners.</span></span> <span data-ttu-id="54ac0-263">Depois de criar um grupo de disponibilidade, adicione o endereço IP ao balanceador de carga e, em seguida, configure o ouvinte.</span><span class="sxs-lookup"><span data-stu-id="54ac0-263">After you create an availability group, add the IP address to the load balancer, and then configure the listener.</span></span>

<span data-ttu-id="54ac0-264">Para adicionar um endereço IP a um balanceador de carga com o Portal do Azure, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="54ac0-264">To add an IP address to a load balancer with the Azure portal, do the following:</span></span>

1. <span data-ttu-id="54ac0-265">No Portal do Azure, abra o grupo de recursos que contém o balanceador de carga e clique o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="54ac0-265">In the Azure portal, open the resource group that contains the load balancer, and then click the load balancer.</span></span> 

2. <span data-ttu-id="54ac0-266">Em **CONFIGURAÇÕES**, clique em **Pool IP de front-ends** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-266">Under **SETTINGS**, click **Frontend IP pool**, and then click **Add**.</span></span> 

3. <span data-ttu-id="54ac0-267">Em **Adicionar endereço IP de front-end**, atribua um nome para o front-end.</span><span class="sxs-lookup"><span data-stu-id="54ac0-267">Under **Add frontend IP address**, assign a name for the front end.</span></span> 

4. <span data-ttu-id="54ac0-268">Verifique se a **Rede virtual** e a **Sub-rede** são as mesmas das instâncias do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="54ac0-268">Verify that the **Virtual network** and the **Subnet** are the same as the SQL Server instances.</span></span>

5. <span data-ttu-id="54ac0-269">Defina o endereço IP para o ouvinte.</span><span class="sxs-lookup"><span data-stu-id="54ac0-269">Set the IP address for the listener.</span></span> 
   
   >[!TIP]
   ><span data-ttu-id="54ac0-270">Você pode definir o endereço IP como estático e digitar um endereço que atualmente não está sendo usado na sub-rede.</span><span class="sxs-lookup"><span data-stu-id="54ac0-270">You can set the IP address to static and type an address that is not currently used in the subnet.</span></span> <span data-ttu-id="54ac0-271">Como alternativa, é possível definir o endereço IP como dinâmico e salvar o novo pool IP de front-ends.</span><span class="sxs-lookup"><span data-stu-id="54ac0-271">Alternatively, you can set the IP address to dynamic and save the new front-end IP pool.</span></span> <span data-ttu-id="54ac0-272">Quando você faz isso, o Portal do Azure atribui automaticamente um endereço IP disponível ao pool.</span><span class="sxs-lookup"><span data-stu-id="54ac0-272">When you do so, the Azure portal automatically assigns an available IP address to the pool.</span></span> <span data-ttu-id="54ac0-273">Em seguida, é possível reabrir o pool IP de front-end e alterar a atribuição para estática.</span><span class="sxs-lookup"><span data-stu-id="54ac0-273">You can then reopen the front-end IP pool and change the assignment to static.</span></span> 

6. <span data-ttu-id="54ac0-274">Salve o endereço IP para o ouvinte.</span><span class="sxs-lookup"><span data-stu-id="54ac0-274">Save the IP address for the listener.</span></span> 

7. <span data-ttu-id="54ac0-275">Adicione uma investigação de integridade usando as seguintes configurações:</span><span class="sxs-lookup"><span data-stu-id="54ac0-275">Add a health probe by using the following settings:</span></span>

   |<span data-ttu-id="54ac0-276">Configuração</span><span class="sxs-lookup"><span data-stu-id="54ac0-276">Setting</span></span> |<span data-ttu-id="54ac0-277">Valor</span><span class="sxs-lookup"><span data-stu-id="54ac0-277">Value</span></span>
   |:-----|:----
   |<span data-ttu-id="54ac0-278">**Nome**</span><span class="sxs-lookup"><span data-stu-id="54ac0-278">**Name**</span></span> |<span data-ttu-id="54ac0-279">Um nome para identificar a investigação.</span><span class="sxs-lookup"><span data-stu-id="54ac0-279">A name to identify the probe.</span></span>
   |<span data-ttu-id="54ac0-280">**Protocolo**</span><span class="sxs-lookup"><span data-stu-id="54ac0-280">**Protocol**</span></span> |<span data-ttu-id="54ac0-281">TCP</span><span class="sxs-lookup"><span data-stu-id="54ac0-281">TCP</span></span>
   |<span data-ttu-id="54ac0-282">**Porta**</span><span class="sxs-lookup"><span data-stu-id="54ac0-282">**Port**</span></span> |<span data-ttu-id="54ac0-283">Uma porta TCP não usada, que deve estar disponível em todas as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="54ac0-283">An unused TCP port, which must be available on all virtual machines.</span></span> <span data-ttu-id="54ac0-284">Não pode ser usada para qualquer outra finalidade.</span><span class="sxs-lookup"><span data-stu-id="54ac0-284">It cannot be used for any other purpose.</span></span> <span data-ttu-id="54ac0-285">Dois ouvintes não podem usar a mesma porta de investigação.</span><span class="sxs-lookup"><span data-stu-id="54ac0-285">No two listeners can use the same probe port.</span></span> 
   |<span data-ttu-id="54ac0-286">**Intervalo**</span><span class="sxs-lookup"><span data-stu-id="54ac0-286">**Interval**</span></span> |<span data-ttu-id="54ac0-287">O tempo entre as tentativas de investigação.</span><span class="sxs-lookup"><span data-stu-id="54ac0-287">The amount of time between probe attempts.</span></span> <span data-ttu-id="54ac0-288">Use o (5) padrão.</span><span class="sxs-lookup"><span data-stu-id="54ac0-288">Use the default (5).</span></span>
   |<span data-ttu-id="54ac0-289">**Limite não íntegro**</span><span class="sxs-lookup"><span data-stu-id="54ac0-289">**Unhealthy threshold**</span></span> |<span data-ttu-id="54ac0-290">O número de limites consecutivos que devem falhar antes que uma máquina virtual seja considerada não íntegra.</span><span class="sxs-lookup"><span data-stu-id="54ac0-290">The number of consecutive thresholds that should fail before a virtual machine is considered unhealthy.</span></span>

8. <span data-ttu-id="54ac0-291">Clique em **OK** para salvar a investigação.</span><span class="sxs-lookup"><span data-stu-id="54ac0-291">Click **OK** to save the probe.</span></span> 

9. <span data-ttu-id="54ac0-292">Criar uma regra de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="54ac0-292">Create a load balancing rule.</span></span> <span data-ttu-id="54ac0-293">Clique em **Regras de balanceamento de carga** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-293">Click **Load balancing rules**, and then click **Add**.</span></span>

10. <span data-ttu-id="54ac0-294">Defina a nova regra de balanceamento de carga usando as seguintes configurações:</span><span class="sxs-lookup"><span data-stu-id="54ac0-294">Configure the new load balancing rule by using the following settings:</span></span>

   |<span data-ttu-id="54ac0-295">Configuração</span><span class="sxs-lookup"><span data-stu-id="54ac0-295">Setting</span></span> |<span data-ttu-id="54ac0-296">Valor</span><span class="sxs-lookup"><span data-stu-id="54ac0-296">Value</span></span>
   |:-----|:----
   |<span data-ttu-id="54ac0-297">**Nome**</span><span class="sxs-lookup"><span data-stu-id="54ac0-297">**Name**</span></span> |<span data-ttu-id="54ac0-298">Um nome para identificar a regra de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="54ac0-298">A name to identify the load balancing rule.</span></span> 
   |<span data-ttu-id="54ac0-299">**Endereço IP de front-end**</span><span class="sxs-lookup"><span data-stu-id="54ac0-299">**Frontend IP address**</span></span> |<span data-ttu-id="54ac0-300">Selecione o endereço IP que você criou.</span><span class="sxs-lookup"><span data-stu-id="54ac0-300">Select the IP address you created.</span></span> 
   |<span data-ttu-id="54ac0-301">**Protocolo**</span><span class="sxs-lookup"><span data-stu-id="54ac0-301">**Protocol**</span></span> |<span data-ttu-id="54ac0-302">TCP</span><span class="sxs-lookup"><span data-stu-id="54ac0-302">TCP</span></span>
   |<span data-ttu-id="54ac0-303">**Porta**</span><span class="sxs-lookup"><span data-stu-id="54ac0-303">**Port**</span></span> |<span data-ttu-id="54ac0-304">Use a porta que as instâncias do SQL Server estão usando.</span><span class="sxs-lookup"><span data-stu-id="54ac0-304">Use the port that the SQL Server instances are using.</span></span> <span data-ttu-id="54ac0-305">Uma instância padrão usa a porta 1433, a menos que você tenha alterado.</span><span class="sxs-lookup"><span data-stu-id="54ac0-305">A default instance uses port 1433, unless you changed it.</span></span> 
   |<span data-ttu-id="54ac0-306">**Porta de back-end**</span><span class="sxs-lookup"><span data-stu-id="54ac0-306">**Backend port**</span></span> |<span data-ttu-id="54ac0-307">Use o mesmo valor de **porta**.</span><span class="sxs-lookup"><span data-stu-id="54ac0-307">Use the same value as **Port**.</span></span>
   |<span data-ttu-id="54ac0-308">**Pool de back-end**</span><span class="sxs-lookup"><span data-stu-id="54ac0-308">**Backend pool**</span></span> |<span data-ttu-id="54ac0-309">O pool que contém as máquinas virtuais com instâncias do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="54ac0-309">The pool that contains the virtual machines with the SQL Server instances.</span></span> 
   |<span data-ttu-id="54ac0-310">**Investigação de integridade**</span><span class="sxs-lookup"><span data-stu-id="54ac0-310">**Health probe**</span></span> |<span data-ttu-id="54ac0-311">Escolha a investigação que você criou.</span><span class="sxs-lookup"><span data-stu-id="54ac0-311">Choose the probe you created.</span></span>
   |<span data-ttu-id="54ac0-312">**Persistência de sessão**</span><span class="sxs-lookup"><span data-stu-id="54ac0-312">**Session persistence**</span></span> |<span data-ttu-id="54ac0-313">Nenhum</span><span class="sxs-lookup"><span data-stu-id="54ac0-313">None</span></span>
   |<span data-ttu-id="54ac0-314">**Tempo limite de ociosidade (minutos)**</span><span class="sxs-lookup"><span data-stu-id="54ac0-314">**Idle timeout (minutes)**</span></span> |<span data-ttu-id="54ac0-315">(4) padrão</span><span class="sxs-lookup"><span data-stu-id="54ac0-315">Default (4)</span></span>
   |<span data-ttu-id="54ac0-316">**IP flutuante (retorno de servidor direto)**</span><span class="sxs-lookup"><span data-stu-id="54ac0-316">**Floating IP (direct server return)**</span></span> | <span data-ttu-id="54ac0-317">habilitado</span><span class="sxs-lookup"><span data-stu-id="54ac0-317">Enabled</span></span>

### <a name="configure-the-availability-group-to-use-the-new-ip-address"></a><span data-ttu-id="54ac0-318">Configurar o grupo de disponibilidade para usar o novo endereço IP</span><span class="sxs-lookup"><span data-stu-id="54ac0-318">Configure the availability group to use the new IP address</span></span>

<span data-ttu-id="54ac0-319">Para concluir a configuração do cluster, repita as etapas que seguiu quando criou o primeiro grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="54ac0-319">To finish configuring the cluster, repeat the steps that you followed when you made the first availability group.</span></span> <span data-ttu-id="54ac0-320">Ou seja, configure o [cluster para usar o novo endereço IP](#configure-the-cluster-to-use-the-load-balancer-ip-address).</span><span class="sxs-lookup"><span data-stu-id="54ac0-320">That is, configure the [cluster to use the new IP address](#configure-the-cluster-to-use-the-load-balancer-ip-address).</span></span> 

<span data-ttu-id="54ac0-321">Depois de adicionar um endereço IP para o ouvinte, você poderá configurar o grupo de disponibilidade adicional fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="54ac0-321">After you have added an IP address for the listener, configure the additional availability group by doing the following:</span></span> 

1. <span data-ttu-id="54ac0-322">Verifique se a porta de investigação para o novo endereço IP está aberta em ambas as máquinas virtuais do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="54ac0-322">Verify that the probe port for the new IP address is open on both SQL Server virtual machines.</span></span> 

2. <span data-ttu-id="54ac0-323">[No Gerenciador de Clusters, adicione o ponto de acesso do cliente](#addcap).</span><span class="sxs-lookup"><span data-stu-id="54ac0-323">[In Cluster Manager, add the client access point](#addcap).</span></span>

3. <span data-ttu-id="54ac0-324">[Configurar o recurso de IP do grupo de disponibilidade](#congroup).</span><span class="sxs-lookup"><span data-stu-id="54ac0-324">[Configure the IP resource for the availability group](#congroup).</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="54ac0-325">Quando você cria o endereço IP, use o endereço IP que adicionou ao balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="54ac0-325">When you create the IP address, use the IP address that you added to the load balancer.</span></span>  

4. <span data-ttu-id="54ac0-326">[Torne o recurso de grupo de disponibilidade do SQL Server dependente do ponto de acesso para cliente](#dependencyGroup).</span><span class="sxs-lookup"><span data-stu-id="54ac0-326">[Make the SQL Server availability group resource dependent on the client access point](#dependencyGroup).</span></span>

5. <span data-ttu-id="54ac0-327">[Torne o recurso de ponto de acesso de cliente dependente do endereço IP](#listname).</span><span class="sxs-lookup"><span data-stu-id="54ac0-327">[Make the client access point resource dependent on the IP address](#listname).</span></span>
 
6. <span data-ttu-id="54ac0-328">[Definir os parâmetros do cluster no PowerShell](#setparam).</span><span class="sxs-lookup"><span data-stu-id="54ac0-328">[Set the cluster parameters in PowerShell](#setparam).</span></span>

<span data-ttu-id="54ac0-329">Depois de configurar o grupo de disponibilidade para usar o novo endereço IP, configure a conexão para o ouvinte.</span><span class="sxs-lookup"><span data-stu-id="54ac0-329">After you configure the availability group to use the new IP address, configure the connection to the listener.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="54ac0-330">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="54ac0-330">Next steps</span></span>

- [<span data-ttu-id="54ac0-331">Configurar um Grupo de Disponibilidade Always On do SQL Server em Máquinas Virtuais do Azure em diferentes regiões</span><span class="sxs-lookup"><span data-stu-id="54ac0-331">Configure a SQL Server Always On availability group on Azure virtual machines in different regions</span></span>](virtual-machines-windows-portal-sql-availability-group-dr.md)
