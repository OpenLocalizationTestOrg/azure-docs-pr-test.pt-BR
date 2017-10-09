---
title: "Balanceador de carga aaaCreate um Azure voltados à Internet com o IPv6 - PowerShell | Microsoft Docs"
description: "Saiba como toocreate um voltados à Internet carregar balanceador com IPv6 usando o PowerShell para o Gerenciador de recursos"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "ipv6, azure load balancer, pilha dual, ip público, ipv6 nativo, móvel, iot"
ms.assetid: d4c649e3-84ad-4343-8b6a-0e89f0b9e518
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 6ebb108399b070e06dddc33b7a774481eb44d717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a><span data-ttu-id="9dfff-104">Introdução à criação de um balanceador de carga para a Internet com IPv6 usando o PowerShell para Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9dfff-104">Get started creating an Internet facing load balancer with IPv6 using PowerShell for Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9dfff-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9dfff-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="9dfff-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9dfff-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="9dfff-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="9dfff-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="9dfff-108">Um Azure Load Balancer é um balanceador de carga de Camada 4 (TCP, UDP).</span><span class="sxs-lookup"><span data-stu-id="9dfff-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="9dfff-109">o balanceador de carga Olá fornece alta disponibilidade através da distribuição de tráfego de entrada entre instâncias do serviço de integridade em serviços de nuvem ou máquinas virtuais em um conjunto de Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="9dfff-109">hello load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="9dfff-110">O Azure Load Balancer também pode apresentar esses serviços em várias portas, vários endereços IP ou ambos.</span><span class="sxs-lookup"><span data-stu-id="9dfff-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="9dfff-111">Exemplo de cenário de implantação</span><span class="sxs-lookup"><span data-stu-id="9dfff-111">Example deployment scenario</span></span>

<span data-ttu-id="9dfff-112">Olá diagrama a seguir ilustra Olá solução balanceamento de carga que está sendo implantada neste artigo.</span><span class="sxs-lookup"><span data-stu-id="9dfff-112">hello following diagram illustrates hello load balancing solution being deployed in this article.</span></span>

![Cenário com o balanceador de carga](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

<span data-ttu-id="9dfff-114">Nesse cenário, você criará hello Azure recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="9dfff-114">In this scenario you will create hello following Azure resources:</span></span>

* <span data-ttu-id="9dfff-115">um balanceador de carga voltado para a Internet com um IPv4 e um endereço IP público IPv6</span><span class="sxs-lookup"><span data-stu-id="9dfff-115">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="9dfff-116">dois carregar balanceamento regras toomap Olá VIPs toohello privados pontos de extremidade públicos</span><span class="sxs-lookup"><span data-stu-id="9dfff-116">two load balancing rules toomap hello public VIPs toohello private endpoints</span></span>
* <span data-ttu-id="9dfff-117">um conjunto de disponibilidade toothat contém Olá duas VMs</span><span class="sxs-lookup"><span data-stu-id="9dfff-117">an Availability Set toothat contains hello two VMs</span></span>
* <span data-ttu-id="9dfff-118">duas VMs (máquinas virtuais)</span><span class="sxs-lookup"><span data-stu-id="9dfff-118">two virtual machines (VMs)</span></span>
* <span data-ttu-id="9dfff-119">uma interface de rede virtual para cada VM com endereços IPv4 e IPv6 atribuídos</span><span class="sxs-lookup"><span data-stu-id="9dfff-119">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>

## <a name="deploying-hello-solution-using-hello-azure-powershell"></a><span data-ttu-id="9dfff-120">Implantar solução hello usando hello Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9dfff-120">Deploying hello solution using hello Azure PowerShell</span></span>

<span data-ttu-id="9dfff-121">Olá etapas a seguir mostra como toocreate um voltados à Internet carregar balanceador usando o Gerenciador de recursos do Azure com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9dfff-121">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="9dfff-122">No Gerenciador de recursos do Azure, cada recurso é criado e configurado individualmente, em seguida, juntar toocreate um recurso.</span><span class="sxs-lookup"><span data-stu-id="9dfff-122">With Azure Resource Manager, each resource is created and configured individually, then put together toocreate a resource.</span></span>

<span data-ttu-id="9dfff-123">toodeploy um balanceador de carga, que você crie e configure Olá seguintes objetos:</span><span class="sxs-lookup"><span data-stu-id="9dfff-123">toodeploy a load balancer, you create and configure hello following objects:</span></span>

* <span data-ttu-id="9dfff-124">Configuração de IP de front-end – contém endereços IP públicos para o tráfego de rede de entrada.</span><span class="sxs-lookup"><span data-stu-id="9dfff-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="9dfff-125">Pool de endereços de back-end - contém interfaces de rede (NICs) para tráfego de rede de tooreceive Olá máquinas virtuais do balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="9dfff-125">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="9dfff-126">Regras de balanceamento de carga - contém regras de mapeamento de uma porta pública em Olá tooport de Balanceador de carga no pool de endereços de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="9dfff-126">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="9dfff-127">Regras NAT de entrada - contém regras de mapeamento de uma porta pública na porta tooa do balanceador de carga Olá para uma máquina virtual no pool de endereços de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="9dfff-127">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="9dfff-128">Testes - contém integridade investigações usadas toocheck disponibilidade das instâncias de máquinas virtuais no pool de endereços de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="9dfff-128">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="9dfff-129">Para saber mais, confira [Suporte do Azure Resource Manager para Balanceador de Carga](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="9dfff-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-toouse-resource-manager"></a><span data-ttu-id="9dfff-130">Configurar o PowerShell toouse Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="9dfff-130">Set up PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="9dfff-131">Verifique se que você tem a versão mais recente de produção saudação do módulo do Azure Resource Manager Olá para o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9dfff-131">Make sure you have hello latest production version of hello Azure Resource Manager module for PowerShell.</span></span>

1. <span data-ttu-id="9dfff-132">Entrar no Azure</span><span class="sxs-lookup"><span data-stu-id="9dfff-132">Sign into Azure</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="9dfff-133">Insira suas credenciais quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="9dfff-133">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="9dfff-134">Verificar as assinaturas de saudação conta Olá</span><span class="sxs-lookup"><span data-stu-id="9dfff-134">Check hello subscriptions for hello account</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="9dfff-135">Escolha qual toouse suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="9dfff-135">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="9dfff-136">Crie um grupo de recursos (pule esta etapa se você estiver usando um grupo de recursos existente)</span><span class="sxs-lookup"><span data-stu-id="9dfff-136">Create a resource group (skip this step if using an existing resource group)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="9dfff-137">Criar uma rede virtual e um endereço IP público para o pool de IP de front-end de saudação</span><span class="sxs-lookup"><span data-stu-id="9dfff-137">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="9dfff-138">Criar uma rede virtual com uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="9dfff-138">Create a virtual network with a subnet.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="9dfff-139">Crie endereço IP público do Azure recursos (PIP) para o pool de endereços IP front-end hello.</span><span class="sxs-lookup"><span data-stu-id="9dfff-139">Create Azure Public IP address (PIP) resources for hello front-end IP address pool.</span></span>

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="9dfff-140">Balanceador de carga de saudação usa o rótulo de domínio de saudação do IP público hello como prefixo para o FQDN.</span><span class="sxs-lookup"><span data-stu-id="9dfff-140">hello load balancer uses hello domain label of hello public IP as prefix for its FQDN.</span></span> <span data-ttu-id="9dfff-141">Neste exemplo, Olá FQDNs são *lbnrpipv4.westus.cloudapp.azure.com* e *lbnrpipv6.westus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="9dfff-141">In this example, hello FQDNs are *lbnrpipv4.westus.cloudapp.azure.com* and *lbnrpipv6.westus.cloudapp.azure.com*.</span></span>

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a><span data-ttu-id="9dfff-142">Criar configurações de IP de front-end e um pool de endereços de back-end</span><span class="sxs-lookup"><span data-stu-id="9dfff-142">Create a Front-End IP configurations and a Back-End Address Pool</span></span>

1. <span data-ttu-id="9dfff-143">Crie configuração de endereço front-end que usa endereços IP públicos de saudação criado por você.</span><span class="sxs-lookup"><span data-stu-id="9dfff-143">Create front-end address configuration that uses hello Public IP addresses you created.</span></span>

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. <span data-ttu-id="9dfff-144">Crie um pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="9dfff-144">Create back-end address pools.</span></span>

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a><span data-ttu-id="9dfff-145">Criar regras de LB, regras NAT, um teste e um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="9dfff-145">Create LB rules, NAT rules, a probe, and a load balancer</span></span>

<span data-ttu-id="9dfff-146">Este exemplo cria Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="9dfff-146">This example creates hello following items:</span></span>

* <span data-ttu-id="9dfff-147">regra de NAT tootranslate todo o tráfego de entrada na porta 443 tooport 4443</span><span class="sxs-lookup"><span data-stu-id="9dfff-147">a NAT rule tootranslate all incoming traffic on port 443 tooport 4443</span></span>
* <span data-ttu-id="9dfff-148">um toobalance de regra de Balanceador de carga todo o tráfego de entrada na porta 80 tooport 80 em Olá endereços no pool de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="9dfff-148">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>
* <span data-ttu-id="9dfff-149">uma carga balanceador regra tooallow RDP conexão toohello VMs na porta 3389.</span><span class="sxs-lookup"><span data-stu-id="9dfff-149">a load balancer rule tooallow RDP connection toohello VMs on port 3389.</span></span>
* <span data-ttu-id="9dfff-150">um status de integridade de saudação do teste regra toocheck em uma página chamada *HealthProbe.aspx* ou um serviço na porta 8080</span><span class="sxs-lookup"><span data-stu-id="9dfff-150">a probe rule toocheck hello health status on a page named *HealthProbe.aspx* or a service on port 8080</span></span>
* <span data-ttu-id="9dfff-151">um balanceador de carga que usa todos esses objetos</span><span class="sxs-lookup"><span data-stu-id="9dfff-151">a load balancer that uses all these objects</span></span>

1. <span data-ttu-id="9dfff-152">Crie regras NAT de saudação.</span><span class="sxs-lookup"><span data-stu-id="9dfff-152">Create hello NAT rules.</span></span>

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. <span data-ttu-id="9dfff-153">Crie um teste de integridade.</span><span class="sxs-lookup"><span data-stu-id="9dfff-153">Create a health probe.</span></span> <span data-ttu-id="9dfff-154">Há dois tooconfigure de maneiras uma investigação:</span><span class="sxs-lookup"><span data-stu-id="9dfff-154">There are two ways tooconfigure a probe:</span></span>

    <span data-ttu-id="9dfff-155">Investigação HTTP</span><span class="sxs-lookup"><span data-stu-id="9dfff-155">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="9dfff-156">ou Investigação TCP</span><span class="sxs-lookup"><span data-stu-id="9dfff-156">or TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="9dfff-157">Neste exemplo, vamos toouse Olá que sondas de TCP.</span><span class="sxs-lookup"><span data-stu-id="9dfff-157">For this example, we are going toouse hello TCP probes.</span></span>

3. <span data-ttu-id="9dfff-158">Crie uma regra de balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="9dfff-158">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. <span data-ttu-id="9dfff-159">Crie o balanceador de carga hello usando objetos Olá criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9dfff-159">Create hello load balancer using hello previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-hello-back-end-vms"></a><span data-ttu-id="9dfff-160">Criar NICs para Olá VMs de back-end</span><span class="sxs-lookup"><span data-stu-id="9dfff-160">Create NICs for hello back-end VMs</span></span>

1. <span data-ttu-id="9dfff-161">Obter Olá rede Virtual e a sub-rede de rede Virtual, onde Olá NICs necessário toobe criado.</span><span class="sxs-lookup"><span data-stu-id="9dfff-161">Get hello Virtual Network and Virtual Network Subnet, where hello NICs need toobe created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="9dfff-162">Crie NICs e as configurações de IP para VMs de saudação.</span><span class="sxs-lookup"><span data-stu-id="9dfff-162">Create IP configurations and NICs for hello VMs.</span></span>

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-hello-newly-created-nics"></a><span data-ttu-id="9dfff-163">Criar máquinas virtuais e atribuir Olá recém-criado NICs</span><span class="sxs-lookup"><span data-stu-id="9dfff-163">Create virtual machines and assign hello newly created NICs</span></span>

<span data-ttu-id="9dfff-164">Para obter mais informações sobre como criar uma VM, consulte [Criar e pré-configurar uma máquina virtual do Windows com o Gerenciador de Recursos e o Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="9dfff-164">For more information about creating a VM, see [Create and preconfigure a Windows Virtual Machine with Resource Manager and Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="9dfff-165">Criar um conjunto de disponibilidade e a conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="9dfff-165">Create an Availability Set and Storage account</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. <span data-ttu-id="9dfff-166">Criar cada VM e atribuir Olá anterior criada NICs</span><span class="sxs-lookup"><span data-stu-id="9dfff-166">Create each VM and assign hello previous created NICs</span></span>

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type hello username and password of hello local administrator account."

    $vm1 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM0' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm1 = Set-AzureRmVMOperatingSystem -VM $vm1 -Windows -ComputerName 'myNrpIPv6VM0' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm1 = Set-AzureRmVMSourceImage -VM $vm1 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm1 = Add-AzureRmVMNetworkInterface -VM $vm1 -Id $nic1.Id -Primary
    $osDisk1Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM0osdisk.vhd"
    $vm1 = Set-AzureRmVMOSDisk -VM $vm1 -Name 'myNrpIPv6VM0osdisk' -VhdUri $osDisk1Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm1

    $vm2 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM1' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm2 = Set-AzureRmVMOperatingSystem -VM $vm2 -Windows -ComputerName 'myNrpIPv6VM1' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm2 = Set-AzureRmVMSourceImage -VM $vm2 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm2 = Add-AzureRmVMNetworkInterface -VM $vm2 -Id $nic2.Id -Primary
    $osDisk2Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM1osdisk.vhd"
    $vm2 = Set-AzureRmVMOSDisk -VM $vm2 -Name 'myNrpIPv6VM1osdisk' -VhdUri $osDisk2Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm2
    ```

## <a name="next-steps"></a><span data-ttu-id="9dfff-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9dfff-167">Next steps</span></span>

[<span data-ttu-id="9dfff-168">Introdução à configuração de um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="9dfff-168">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="9dfff-169">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="9dfff-169">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="9dfff-170">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="9dfff-170">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
