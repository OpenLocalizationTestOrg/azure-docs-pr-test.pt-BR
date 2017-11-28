---
title: "aaaConfigure sempre em ouvintes de disponibilidade – Microsoft Azure | Microsoft Docs"
description: "Configure os ouvintes de grupo de disponibilidade no modelo do Azure Resource Manager hello, usando um balanceador de carga interno com um ou mais endereços IP."
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: 14b39cde-311c-4ddf-98f3-8694e01a7d3b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/22/2017
ms.author: mikeray
ms.openlocfilehash: 81edfe2c2ea536d8dcec466f36fccf8bc0e02c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a><span data-ttu-id="36a43-103">Configurar um ou mais ouvintes de grupo de disponibilidade AlwaysOn – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="36a43-103">Configure one or more Always On availability group listeners - Resource Manager</span></span>
<span data-ttu-id="36a43-104">Este tópico mostra como:</span><span class="sxs-lookup"><span data-stu-id="36a43-104">This topic shows how to:</span></span>

* <span data-ttu-id="36a43-105">Criar um balanceador de carga interno para grupos de disponibilidade do SQL Server usando cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="36a43-105">Create an internal load balancer for SQL Server availability groups using PowerShell cmdlets.</span></span>
* <span data-ttu-id="36a43-106">Adicione adicionais IP endereços tooa balanceador de carga para mais de um grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="36a43-106">Add additional IP addresses tooa load balancer for more than one availability group.</span></span> 

<span data-ttu-id="36a43-107">Um ouvinte de grupo de disponibilidade é um nome de rede virtual que os clientes se conectem toofor acesso de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="36a43-107">An availability group listener is a virtual network name that clients connect toofor database access.</span></span> <span data-ttu-id="36a43-108">Em máquinas virtuais do Azure, um balanceador de carga contém o endereço IP hello ouvinte Olá.</span><span class="sxs-lookup"><span data-stu-id="36a43-108">On Azure virtual machines, a load balancer holds hello IP address for hello listener.</span></span> <span data-ttu-id="36a43-109">rotas de Balanceador de carga Olá toohello instância do SQL Server está escutando na porta de investigação de saudação do tráfego.</span><span class="sxs-lookup"><span data-stu-id="36a43-109">hello load balancer routes traffic toohello instance of SQL Server that is listening on hello probe port.</span></span> <span data-ttu-id="36a43-110">Normalmente, um grupo de disponibilidade usa um balanceador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="36a43-110">Usually, an availability group uses an internal load balancer.</span></span> <span data-ttu-id="36a43-111">Um balanceador de carga interno do Azure pode hospedar um ou vários endereços IP.</span><span class="sxs-lookup"><span data-stu-id="36a43-111">An Azure internal load balancer can host one or many IP addresses.</span></span> <span data-ttu-id="36a43-112">Cada endereço IP usa uma porta de investigação específica.</span><span class="sxs-lookup"><span data-stu-id="36a43-112">Each IP address uses a specific probe port.</span></span> <span data-ttu-id="36a43-113">Este documento mostra como toouse PowerShell toocreate um balanceador de carga ou adicione endereços de IP tooan balanceador de carga existente para grupos de disponibilidade do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="36a43-113">This document shows how toouse PowerShell toocreate a load balancer, or add IP addresses tooan existing load balancer for SQL Server availability groups.</span></span> 

<span data-ttu-id="36a43-114">Olá capacidade tooassign vários balanceador de carga interno de tooan para endereços IP é tooAzure novo e está disponível apenas no modelo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="36a43-114">hello ability tooassign multiple IP addresses tooan internal load balancer is new tooAzure and is only available in Resource Manager model.</span></span> <span data-ttu-id="36a43-115">toocomplete nesta tarefa, você precisa toohave implantado de um grupo de disponibilidade do SQL Server em máquinas virtuais do Azure no modelo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="36a43-115">toocomplete this task, you need toohave a SQL Server availability group deployed on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="36a43-116">Máquinas virtuais do SQL Server deve pertencer toohello mesmo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="36a43-116">Both SQL Server virtual machines must belong toohello same availability set.</span></span> <span data-ttu-id="36a43-117">Você pode usar o hello [modelo Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically criar grupo de disponibilidade de saudação no Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="36a43-117">You can use hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically create hello availability group in Azure Resource Manager.</span></span> <span data-ttu-id="36a43-118">Este modelo cria automaticamente o grupo de disponibilidade hello, incluindo o balanceador de carga interno Olá para você.</span><span class="sxs-lookup"><span data-stu-id="36a43-118">This template automatically creates hello availability group, including hello internal load balancer for you.</span></span> <span data-ttu-id="36a43-119">Se preferir, você poderá [configurar manualmente um grupo de disponibilidade AlwaysOn](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="36a43-119">If you prefer, you can [manually configure an Always On availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="36a43-120">Este tópico exige que os grupos de disponibilidade já estejam configurados.</span><span class="sxs-lookup"><span data-stu-id="36a43-120">This topic requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="36a43-121">Os tópicos relacionados incluem:</span><span class="sxs-lookup"><span data-stu-id="36a43-121">Related topics include:</span></span>

* [<span data-ttu-id="36a43-122">Configurar os Grupos de Disponibilidade AlwaysOn na VM do Azure (GUI)</span><span class="sxs-lookup"><span data-stu-id="36a43-122">Configure AlwaysOn Availability Groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="36a43-123">Configurar uma conexão de rede virtual com rede virtual usando o PowerShell e o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="36a43-123">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-hello-windows-firewall"></a><span data-ttu-id="36a43-124">Configurar Olá Firewall do Windows</span><span class="sxs-lookup"><span data-stu-id="36a43-124">Configure hello Windows Firewall</span></span>
<span data-ttu-id="36a43-125">Configure o acesso ao SQL Server tooallow Firewall do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="36a43-125">Configure hello Windows Firewall tooallow SQL Server access.</span></span> <span data-ttu-id="36a43-126">as regras de firewall Olá permitem o usam de portas de toohello conexões TCP por instância do SQL Server hello e investigação do ouvinte hello.</span><span class="sxs-lookup"><span data-stu-id="36a43-126">hello firewall rules allow TCP connections toohello ports use by hello SQL Server instance, and hello listener probe.</span></span> <span data-ttu-id="36a43-127">Para obter instruções detalhadas, confira [Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="36a43-127">For detailed instructions, see [Configure a Windows Firewall for Database Engine Access](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span></span> <span data-ttu-id="36a43-128">Crie uma regra de entrada para Olá porta do SQL Server e para a porta de investigação de saudação.</span><span class="sxs-lookup"><span data-stu-id="36a43-128">Create an inbound rule for hello SQL Server port and for hello probe port.</span></span>

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a><span data-ttu-id="36a43-129">Script de exemplo: criar um balanceador de carga interno usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="36a43-129">Example Script: Create an internal load balancer with PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="36a43-130">Se você criou o grupo de disponibilidade com hello [modelo Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), o balanceador de carga interno Olá já foi criado.</span><span class="sxs-lookup"><span data-stu-id="36a43-130">If you created your availability group with hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), hello internal load balancer was already created.</span></span> 
> 
> 

<span data-ttu-id="36a43-131">Olá seguinte script do PowerShell cria um balanceador de carga interno, configura regras de balanceamento de carga de saudação e define um endereço IP hello balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="36a43-131">hello following PowerShell script creates an internal load balancer, configures hello load balancing rules, and sets an IP address for hello load balancer.</span></span> <span data-ttu-id="36a43-132">script de saudação toorun, abra o Windows PowerShell ISE e cole o script hello no painel de Script hello.</span><span class="sxs-lookup"><span data-stu-id="36a43-132">toorun hello script, open Windows PowerShell ISE, and paste hello script in hello Script pane.</span></span> <span data-ttu-id="36a43-133">Use `Login-AzureRMAccount` toolog em tooPowerShell.</span><span class="sxs-lookup"><span data-stu-id="36a43-133">Use `Login-AzureRMAccount` toolog in tooPowerShell.</span></span> <span data-ttu-id="36a43-134">Se você tiver várias assinaturas do Azure, use `Select-AzureRmSubscription ` tooset assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="36a43-134">If you have multiple Azure subscriptions, use `Select-AzureRmSubscription ` tooset hello subscription.</span></span> 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<Resource Group Name>" # Resource group name
$VNetName = "<Virtual Network Name>"         # Virtual network name
$SubnetName = "<Subnet Name>"                # Subnet name
$ILBName = "<Load Balancer Name>"            # ILB name
$Location = "<Azure Region>"                 # Azure location
$VMNames = "<VM1>","<VM2>"                   # Virtual machine names

$ILBIP = "<n.n.n.n>"                         # IP address
[int]$ListenerPort = "<nnnn>"                # AG listener port
[int]$ProbePort = "<nnnn>"                   # Probe port

$LBProbeName ="ILBPROBE_$ListenerPort"       # hello Load balancer Probe Object Name              
$LBConfigRuleName = "ILBCR_$ListenerPort"    # hello Load Balancer Rule Object Name

$FrontEndConfigurationName = "FE_SQLAGILB_1" # Object name for hello front-end configuration 
$BackEndConfigurationName ="BE_SQLAGILB_1"   # Object name for hello back-end configuration

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 

$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName 

$FEConfig = New-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.id

$BEConfig = New-AzureRMLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName 

$SQLHealthProbe = New-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -Protocol tcp -Port $ProbePort -IntervalInSeconds 15 -ProbeCount 2

$ILBRule = New-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP 

$ILB= New-AzureRmLoadBalancer -Location $Location -Name $ILBName -ResourceGroupName $ResourceGroupName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -LoadBalancingRule $ILBRule -Probe $SQLHealthProbe 

$bepool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB 

foreach($VMName in $VMNames)
    {
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName 
        $NICName = ($vm.NetworkProfile.NetworkInterfaces.Id.split('/') | select -last 1)
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools = $BEPool
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name 
    }
```

## <span data-ttu-id="36a43-135"><a name="Add-IP"></a>Script de exemplo: adicionar um IP endereço tooan balanceador de carga com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="36a43-135"><a name="Add-IP"></a> Example script: Add an IP address tooan existing load balancer with PowerShell</span></span>
<span data-ttu-id="36a43-136">toouse mais de um grupo de disponibilidade, adicione um balanceador de carga adicional toohello de endereço IP.</span><span class="sxs-lookup"><span data-stu-id="36a43-136">toouse more than one availability group, add an additional IP address toohello load balancer.</span></span> <span data-ttu-id="36a43-137">Cada endereço IP requer sua própria regra de balanceamento de carga, porta de investigação e porta de front-end.</span><span class="sxs-lookup"><span data-stu-id="36a43-137">Each IP address requires its own load balancing rule, probe port, and front port.</span></span>

<span data-ttu-id="36a43-138">Olá front-end porta é Olá que aplicativos usam a instância do SQL Server toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="36a43-138">hello front-end port is hello port that applications use tooconnect toohello SQL Server instance.</span></span> <span data-ttu-id="36a43-139">Endereços IP para diferentes grupos de disponibilidade podem use Olá a mesma porta de front-end.</span><span class="sxs-lookup"><span data-stu-id="36a43-139">IP addresses for different availability groups can use hello same front-end port.</span></span>

> [!NOTE]
> <span data-ttu-id="36a43-140">Para grupos de disponibilidade do SQL Server, cada endereço IP exige uma porta de investigação específica.</span><span class="sxs-lookup"><span data-stu-id="36a43-140">For SQL Server availability groups, each IP address requires a specific probe port.</span></span> <span data-ttu-id="36a43-141">Por exemplo, se um endereço IP em um balanceador de carga usa a porta de investigação 59999, nenhum outro endereço IP nesse balanceador de carga pode usar essa porta de investigação.</span><span class="sxs-lookup"><span data-stu-id="36a43-141">For example, if one IP address on a load balancer uses probe port 59999, no other IP addresses on that load balancer can use probe port 59999.</span></span>

* <span data-ttu-id="36a43-142">Para saber mais sobre os limites do balanceador de carga, confira **IP privado front-end por balanceador de carga** em [Limites de Rede – Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="36a43-142">For information about load balancer limits, see **Private front end IP per load balancer** under [Networking Limits - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span></span>
* <span data-ttu-id="36a43-143">Para saber mais sobre os limites de grupo de disponibilidade, confira [Restrições (Grupos de Disponibilidade)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span><span class="sxs-lookup"><span data-stu-id="36a43-143">For information about availability group limits, see [Restrictions (Availability Groups)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span></span>

<span data-ttu-id="36a43-144">Olá, script a seguir adiciona um novo IP endereço tooan balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="36a43-144">hello following script adds a new IP address tooan existing load balancer.</span></span> <span data-ttu-id="36a43-145">Olá ILB usa a porta de escuta Olá Olá balanceamento de carga porta de front-end.</span><span class="sxs-lookup"><span data-stu-id="36a43-145">hello ILB uses hello listener port for hello load balancing front-end port.</span></span> <span data-ttu-id="36a43-146">Essa porta pode ser Olá que o SQL Server está escutando.</span><span class="sxs-lookup"><span data-stu-id="36a43-146">This port can be hello port that SQL Server is listening on.</span></span> <span data-ttu-id="36a43-147">Para instâncias padrão do SQL Server, a porta de saudação é 1433.</span><span class="sxs-lookup"><span data-stu-id="36a43-147">For default instances of SQL Server, hello port is 1433.</span></span> <span data-ttu-id="36a43-148">regra para um grupo de disponibilidade de balanceamento de carga de saudação requer um IP flutuante (retorno de servidor direto) para a porta de back-end de saudação é Olá mesmo como portas de front-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="36a43-148">hello load balancing rule for an availability group requires a floating IP (direct server return) so hello back-end port is hello same as hello front-end port.</span></span> <span data-ttu-id="36a43-149">Atualize as variáveis de saudação para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="36a43-149">Update hello variables for your environment.</span></span> 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<ResourceGroup>"          # Resource group name
$VNetName = "<VirtualNetwork>"                  # Virtual network name
$SubnetName = "<Subnet>"                        # Subnet name
$ILBName = "<ILBName>"                          # ILB name                      

$ILBIP = "<n.n.n.n>"                            # IP address
[int]$ListenerPort = "<nnnn>"                   # AG listener port
[int]$ProbePort = "<nnnnn>"                     # Probe port 

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName 

$count = $ILB.FrontendIpConfigurations.Count+1
$FrontEndConfigurationName ="FE_SQLAGILB_$count"  

$LBProbeName = "ILBPROBE_$count"
$LBConfigrulename = "ILBCR_$count"

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id 

$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 15  | Set-AzureRmLoadBalancer 

$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB

$SQLHealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $ILB.BackendAddressPools[0].Name -LoadBalancer $ILB 

$ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort  $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP | Set-AzureRmLoadBalancer   
```

## <a name="configure-hello-listener"></a><span data-ttu-id="36a43-150">Configurar ouvinte Olá</span><span class="sxs-lookup"><span data-stu-id="36a43-150">Configure hello listener</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-hello-listener-port-in-sql-server-management-studio"></a><span data-ttu-id="36a43-151">Defina a porta do ouvinte Olá no SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="36a43-151">Set hello listener port in SQL Server Management Studio</span></span>

1. <span data-ttu-id="36a43-152">Inicie o SQL Server Management Studio e conecte-se a réplica primária toohello.</span><span class="sxs-lookup"><span data-stu-id="36a43-152">Launch SQL Server Management Studio and connect toohello primary replica.</span></span>

1. <span data-ttu-id="36a43-153">Navegue muito**alta disponibilidade AlwaysOn** | **grupos de disponibilidade** | **ouvintes do grupo de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="36a43-153">Navigate too**AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span> 

1. <span data-ttu-id="36a43-154">Agora você deve ver o nome do ouvinte Olá que você criou no Gerenciador de Cluster de Failover.</span><span class="sxs-lookup"><span data-stu-id="36a43-154">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="36a43-155">Nome do ouvinte de saudação de mouse e clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="36a43-155">Right-click hello listener name and click **Properties**.</span></span>

1. <span data-ttu-id="36a43-156">Em Olá **porta** , especifique o número da porta saudação do ouvinte do grupo de disponibilidade Olá usando Olá $EndpointPort utilizado antes (1433 foi padrão Olá), em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="36a43-156">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort you used earlier (1433 was hello default), then click **OK**.</span></span>

## <a name="test-hello-connection-toohello-listener"></a><span data-ttu-id="36a43-157">Ouvinte de toohello de conexão de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="36a43-157">Test hello connection toohello listener</span></span>

<span data-ttu-id="36a43-158">conexão de saudação tootest:</span><span class="sxs-lookup"><span data-stu-id="36a43-158">tootest hello connection:</span></span>

1. <span data-ttu-id="36a43-159">RDP tooa SQL Server que está em Olá mesmo virtual de rede, mas não não réplica Olá próprio.</span><span class="sxs-lookup"><span data-stu-id="36a43-159">RDP tooa SQL Server that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="36a43-160">Isso pode ser Olá outros SQL Server em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="36a43-160">This can be hello other SQL Server in hello cluster.</span></span>

1. <span data-ttu-id="36a43-161">Use **sqlcmd** conexão de saudação do utilitário tootest.</span><span class="sxs-lookup"><span data-stu-id="36a43-161">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="36a43-162">Por exemplo, a saudação script a seguir estabelece uma **sqlcmd** réplica primária de toohello de conexão por meio do ouvinte Olá com autenticação do Windows:</span><span class="sxs-lookup"><span data-stu-id="36a43-162">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    <span data-ttu-id="36a43-163">Se o ouvinte Olá estiver usando uma porta diferente de Olá padrão (1433) de porta, especifique a porta Olá na cadeia de caracteres de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="36a43-163">If hello listener is using a port other than hello default port (1433), specify hello port in hello connection string.</span></span> <span data-ttu-id="36a43-164">Por exemplo, hello seguinte comando sqlcmd conecta tooa escuta na porta 1435:</span><span class="sxs-lookup"><span data-stu-id="36a43-164">For example, hello following sqlcmd command connects tooa listener at port 1435:</span></span> 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="36a43-165">Olá conexão SQLCMD conecta-se automaticamente toowhichever instância do SQL Server hospeda Olá a réplica primária.</span><span class="sxs-lookup"><span data-stu-id="36a43-165">hello SQLCMD connection automatically connects toowhichever instance of SQL Server hosts hello primary replica.</span></span> 

> [!NOTE]
> <span data-ttu-id="36a43-166">Certifique-se de que a porta de Olá especificado é aberta no firewall Olá de ambos os servidores SQL.</span><span class="sxs-lookup"><span data-stu-id="36a43-166">Make sure that hello port you specify is open on hello firewall of both SQL Servers.</span></span> <span data-ttu-id="36a43-167">Ambos os servidores exigem uma regra de entrada para Olá a porta TCP que você usa.</span><span class="sxs-lookup"><span data-stu-id="36a43-167">Both servers require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="36a43-168">Veja [Adicionar ou Editar Regra de Firewall](http://technet.microsoft.com/library/cc753558.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="36a43-168">See [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx) for more information.</span></span> 
> 
> 

## <a name="guidelines-and-limitations"></a><span data-ttu-id="36a43-169">Diretrizes e limitações</span><span class="sxs-lookup"><span data-stu-id="36a43-169">Guidelines and limitations</span></span>
<span data-ttu-id="36a43-170">Observe Olá diretrizes no ouvinte do grupo de disponibilidade no Azure usando o balanceador de carga interno a seguir:</span><span class="sxs-lookup"><span data-stu-id="36a43-170">Note hello following guidelines on availability group listener in Azure using internal load balancer:</span></span>

* <span data-ttu-id="36a43-171">Com um balanceador de carga interno, apenas acesso ouvinte Olá de dentro de saudação mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="36a43-171">With an internal load balancer, you only access hello listener from within hello same virtual network.</span></span>


## <a name="for-more-information"></a><span data-ttu-id="36a43-172">Para obter mais informações</span><span class="sxs-lookup"><span data-stu-id="36a43-172">For more information</span></span>
<span data-ttu-id="36a43-173">Para saber mais, confira [Configure Always On availability group in Azure VM manually](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md) (Configurar grupo de disponibilidade Always On na VM do Azure manualmente).</span><span class="sxs-lookup"><span data-stu-id="36a43-173">For more information, see [Configure Always On availability group in Azure VM manually](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="36a43-174">Cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="36a43-174">PowerShell cmdlets</span></span>
<span data-ttu-id="36a43-175">Use Olá toocreate de cmdlets do PowerShell um balanceador de carga interno para máquinas virtuais do Azure a seguir.</span><span class="sxs-lookup"><span data-stu-id="36a43-175">Use hello following PowerShell cmdlets toocreate an internal load balancer for Azure virtual machines.</span></span>

* <span data-ttu-id="36a43-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) cria um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="36a43-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) creates a load balancer.</span></span> 
* <span data-ttu-id="36a43-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) cria uma configuração de IP de front-end para um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="36a43-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) creates a front-end IP configuration for a load balancer.</span></span> 
* <span data-ttu-id="36a43-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) cria uma configuração de regra para um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="36a43-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) creates a rule configuration for a load balancer.</span></span> 
* <span data-ttu-id="36a43-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) cria uma configuração de pool de endereços de back-end para um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="36a43-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) creates a backend address pool configuration for a load balancer.</span></span> 
* <span data-ttu-id="36a43-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) cria uma configuração de investigação para um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="36a43-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) creates a probe configuration for a load balancer.</span></span>
* <span data-ttu-id="36a43-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) remove um balanceador de carga de um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="36a43-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) removes a load balancer from an Azure resource group.</span></span>
