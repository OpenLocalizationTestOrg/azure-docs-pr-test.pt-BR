---
title: aaaCreate um Azure voltados para Internet carregar balanceador - PowerShell | Microsoft Docs
description: Saiba como toocreate um voltados para Internet balanceador de carga no Gerenciador de recursos usando o PowerShell
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 8257f548-7019-417f-b15f-d004a1eec826
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e4e0e5271bc83c23fc62c0910e784c57d2b30065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="a4938-103"><a name="get-started"></a>Criar um balanceador de carga para a Internet no Resource Manager usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4938-103"><a name="get-started"></a>Creating an Internet-facing load balancer in Resource Manager by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4938-104">Portal</span><span class="sxs-lookup"><span data-stu-id="a4938-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="a4938-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4938-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="a4938-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a4938-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="a4938-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="a4938-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="a4938-108">Este artigo aborda o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4938-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="a4938-109">Você também pode [Saiba como toocreate um voltados para Internet balanceador de carga usando o modelo de implantação clássico Olá](load-balancer-get-started-internet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a4938-109">You can also [learn how toocreate an Internet-facing load balancer by using hello classic deployment model](load-balancer-get-started-internet-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-by-using-azure-powershell"></a><span data-ttu-id="a4938-110">Implantação de solução de saudação usando o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="a4938-110">Deploying hello solution by using Azure PowerShell</span></span>

<span data-ttu-id="a4938-111">Olá procedimentos a seguir explica como toocreate um voltados para Internet balanceador de carga usando o Gerenciador de recursos do Azure com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4938-111">hello following procedures explain how toocreate an Internet-facing load balancer by using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="a4938-112">No Gerenciador de recursos do Azure, cada recurso é criado e configurado individualmente e juntar toocreate um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="a4938-112">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a load balancer.</span></span>

<span data-ttu-id="a4938-113">Você deve criar e configurar Olá objetos toodeploy um balanceador de carga a seguir:</span><span class="sxs-lookup"><span data-stu-id="a4938-113">You must create and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="a4938-114">Configuração de IP de front-end: contém PIPs ( endereços IP públicos) para o tráfego de rede de entrada.</span><span class="sxs-lookup"><span data-stu-id="a4938-114">Front-end IP configuration: contains public IP (PIP) addresses for incoming network traffic.</span></span>
* <span data-ttu-id="a4938-115">Pool de endereços de back-end: contém as interfaces de rede (NICs) para tráfego de rede de tooreceive Olá máquinas virtuais do balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4938-115">Back-end address pool: contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="a4938-116">Regras de balanceamento de carga: contém regras que mapeiam uma porta pública na porta tooa do balanceador de carga Olá no pool de endereços de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4938-116">Load-balancing rules: contains rules that map a public port on hello load balancer tooa port in hello back-end address pool.</span></span>
* <span data-ttu-id="a4938-117">Regras NAT de entrada: contém regras que mapeiam uma porta pública na porta tooa do balanceador de carga Olá para uma máquina virtual no pool de endereços de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4938-117">Inbound NAT rules: contains rules that map a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="a4938-118">Testes: contém integridade investigações usadas toocheck disponibilidade das instâncias de máquina virtual no pool de endereços de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4938-118">Probes: contains health probes used toocheck availability of virtual machine instances in hello back-end address pool.</span></span>

<span data-ttu-id="a4938-119">Para saber mais, confira [Suporte do Azure Resource Manager para Balanceador de Carga](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="a4938-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-toouse-resource-manager"></a><span data-ttu-id="a4938-120">Configurar o PowerShell toouse Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="a4938-120">Set up PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="a4938-121">Verifique se que você tem a versão mais recente de produção saudação do módulo do Azure Resource Manager Olá do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a4938-121">Make sure you have hello latest production version of hello Azure Resource Manager module for PowerShell:</span></span>

1. <span data-ttu-id="a4938-122">Entrar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a4938-122">Sign in tooAzure.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="a4938-123">Insira suas credenciais quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="a4938-123">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="a4938-124">Verificar as assinaturas de saudação para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4938-124">Check hello subscriptions for hello account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="a4938-125">Escolha qual toouse suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4938-125">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="a4938-126">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="a4938-126">Create a resource group.</span></span> <span data-ttu-id="a4938-127">(Ignore esta etapa se está usando um grupo de recursos existente.)</span><span class="sxs-lookup"><span data-stu-id="a4938-127">(Skip this step if you're using an existing resource group.)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="a4938-128">Criar uma rede virtual e um endereço IP público para o pool de IP de front-end de saudação</span><span class="sxs-lookup"><span data-stu-id="a4938-128">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="a4938-129">Criar uma sub-rede e uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="a4938-129">Create a subnet and a virtual network.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="a4938-130">Criar Azure público recurso de endereço IP, denominado **PublicIP**, toobe usado por um pool IP de front-end com o nome DNS Olá **loadbalancernrp.westus.cloudapp.azure.com**. Olá comando a seguir usa Olá tipo de alocação estática.</span><span class="sxs-lookup"><span data-stu-id="a4938-130">Create an Azure public IP address resource, named **PublicIP**, toobe used by a front-end IP pool with hello DNS name **loadbalancernrp.westus.cloudapp.azure.com**. hello following command uses hello static allocation type.</span></span>

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="a4938-131">Balanceador de carga de saudação usa o rótulo de domínio de saudação do IP público hello como um prefixo para o FQDN.</span><span class="sxs-lookup"><span data-stu-id="a4938-131">hello load balancer uses hello domain label of hello public IP as a prefix for its FQDN.</span></span> <span data-ttu-id="a4938-132">Isso é diferente do modelo de implantação clássico hello, que usa o serviço de nuvem Olá Olá FQDN do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="a4938-132">This is different from hello classic deployment model, which uses hello cloud service as hello load balancer FQDN.</span></span>
   > <span data-ttu-id="a4938-133">Neste exemplo, hello FQDN é **loadbalancernrp.westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="a4938-133">In this example, hello FQDN is **loadbalancernrp.westus.cloudapp.azure.com**.</span></span>

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a><span data-ttu-id="a4938-134">Criar um pool de IPs de front-end e um pool de endereços de back-end</span><span class="sxs-lookup"><span data-stu-id="a4938-134">Create a front-end IP pool and a back-end address pool</span></span>

1. <span data-ttu-id="a4938-135">Criar um pool IP de front-end denominado **LB Frontend** que usa Olá **PublicIp** recursos.</span><span class="sxs-lookup"><span data-stu-id="a4938-135">Create a front-end IP pool named **LB-Frontend** that uses hello **PublicIp** resource.</span></span>

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. <span data-ttu-id="a4938-136">Crie um pool de endereços de back-end chamado **LB-backend**.</span><span class="sxs-lookup"><span data-stu-id="a4938-136">Create a back-end address pool named **LB-backend**.</span></span>

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a><span data-ttu-id="a4938-137">Criar regras NAT, uma regra de balanceador de carga, uma investigação e um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="a4938-137">Create NAT rules, a load balancer rule, a probe, and a load balancer</span></span>

<span data-ttu-id="a4938-138">Este exemplo cria Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="a4938-138">This example creates hello following items:</span></span>

* <span data-ttu-id="a4938-139">Um tootranslate de regra NAT todas as solicitações de tráfego na porta 3441 tooport 3389</span><span class="sxs-lookup"><span data-stu-id="a4938-139">A NAT rule tootranslate all incoming traffic on port 3441 tooport 3389</span></span>
* <span data-ttu-id="a4938-140">Um tootranslate de regra NAT todas as solicitações de tráfego na porta 3442 tooport 3389</span><span class="sxs-lookup"><span data-stu-id="a4938-140">A NAT rule tootranslate all incoming traffic on port 3442 tooport 3389</span></span>
* <span data-ttu-id="a4938-141">Um status de integridade de saudação do teste regra toocheck em uma página chamada **HealthProbe.aspx**</span><span class="sxs-lookup"><span data-stu-id="a4938-141">A probe rule toocheck hello health status on a page named **HealthProbe.aspx**</span></span>
* <span data-ttu-id="a4938-142">Um toobalance de regra de Balanceador de carga de todo o tráfego de entrada na porta 80 tooport 80 em Olá endereços no pool de back-end Olá</span><span class="sxs-lookup"><span data-stu-id="a4938-142">A load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool</span></span>
* <span data-ttu-id="a4938-143">Um balanceador de carga que usa todos esses objetos</span><span class="sxs-lookup"><span data-stu-id="a4938-143">A load balancer that uses all these objects</span></span>

<span data-ttu-id="a4938-144">Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="a4938-144">Use these steps:</span></span>

1. <span data-ttu-id="a4938-145">Crie regras NAT de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4938-145">Create hello NAT rules.</span></span>

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. <span data-ttu-id="a4938-146">Crie um teste de integridade.</span><span class="sxs-lookup"><span data-stu-id="a4938-146">Create a health probe.</span></span> <span data-ttu-id="a4938-147">Há dois tooconfigure de maneiras uma investigação:</span><span class="sxs-lookup"><span data-stu-id="a4938-147">There are two ways tooconfigure a probe:</span></span>

    <span data-ttu-id="a4938-148">Investigação HTTP</span><span class="sxs-lookup"><span data-stu-id="a4938-148">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="a4938-149">Investigação TCP</span><span class="sxs-lookup"><span data-stu-id="a4938-149">TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. <span data-ttu-id="a4938-150">Crie uma regra de balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="a4938-150">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. <span data-ttu-id="a4938-151">Crie balanceador de carga hello usando objetos Olá criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a4938-151">Create hello load balancer by using hello previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a><span data-ttu-id="a4938-152">Criar NICs</span><span class="sxs-lookup"><span data-stu-id="a4938-152">Create NICs</span></span>

<span data-ttu-id="a4938-153">Criar interfaces de rede (ou modificar as existentes) e, em seguida, associá-los tooNAT regras, regras de Balanceador de carga e investigações:</span><span class="sxs-lookup"><span data-stu-id="a4938-153">Create network interfaces (or modify existing ones) and then associate them tooNAT rules, load balancer rules, and probes:</span></span>

1. <span data-ttu-id="a4938-154">Obter Olá uma rede virtual e uma sub-rede de rede virtual, onde Olá NICs necessário toobe criado.</span><span class="sxs-lookup"><span data-stu-id="a4938-154">Get hello virtual network and a virtual network subnet, where hello NICs need toobe created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="a4938-155">Criar uma NIC denominada **lb-nic1 ser**e associá-lo a primeira regra NAT hello e pool de endereços de back-end de primeira (e única) do hello.</span><span class="sxs-lookup"><span data-stu-id="a4938-155">Create a NIC named **lb-nic1-be**, and associate it with hello first NAT rule and hello first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. <span data-ttu-id="a4938-156">Criar uma NIC denominada **lb-nic2 ser**e associá-lo a segunda regra NAT hello e pool de endereços de back-end de primeira (e única) do hello.</span><span class="sxs-lookup"><span data-stu-id="a4938-156">Create a NIC named **lb-nic2-be**, and associate it with hello second NAT rule and hello first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. <span data-ttu-id="a4938-157">Verifique as NICs de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4938-157">Check hello NICs.</span></span>

        $backendnic1

    <span data-ttu-id="a4938-158">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="a4938-158">Expected output:</span></span>

        Name                 : lb-nic1-be
        ResourceGroupName    : NRP-RG
        Location             : westus
        Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
        ResourceGuid         : 896cac4f-152a-40b9-b079-3e2201a5906e
        ProvisioningState    : Succeeded
        Tags                 :
        VirtualMachine       : null
        IpConfigurations     : [
                            {
                            "Name": "ipconfig1",
                            "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                            "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1",
                            "PrivateIpAddress": "10.0.2.6",
                            "PrivateIpAllocationMethod": "Static",
                            "Subnet": {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                            },
                            "ProvisioningState": "Succeeded",
                            "PrivateIpAddressVersion": "IPv4",
                            "PublicIpAddress": {
                                "Id": null
                            },
                            "LoadBalancerBackendAddressPools": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                                }
                            ],
                            "LoadBalancerInboundNatRules": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                                }
                            ],
                            "Primary": true,
                            "ApplicationGatewayBackendAddressPools": []
                            }
                        ]
        DnsSettings          : {
                            "DnsServers": [],
                            "AppliedDnsServers": [],
                            "InternalDomainNameSuffix": "prcwibzcuvie5hnxav0yjks2cd.dx.internal.cloudapp.net"
                        }
        EnableIPForwarding   : False
        NetworkSecurityGroup : null
        Primary              :

5. <span data-ttu-id="a4938-159">Saudação de uso `Add-AzureRmVMNetworkInterface` cmdlet tooassign Olá NICs toodifferent VMs.</span><span class="sxs-lookup"><span data-stu-id="a4938-159">Use hello `Add-AzureRmVMNetworkInterface` cmdlet tooassign hello NICs toodifferent VMs.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="a4938-160">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="a4938-160">Create a virtual machine</span></span>

<span data-ttu-id="a4938-161">Para obter orientação sobre como criar uma máquina virtual e atribuir uma NIC, confira [Criar uma VM do Azure usando o PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a4938-161">For guidance on creating a virtual machine and assigning a NIC, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-hello-network-interface-toohello-load-balancer"></a><span data-ttu-id="a4938-162">Adicionar balanceador de carga Olá rede interface toohello</span><span class="sxs-lookup"><span data-stu-id="a4938-162">Add hello network interface toohello load balancer</span></span>

1. <span data-ttu-id="a4938-163">Recupere o balanceador de carga de saudação do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4938-163">Retrieve hello load balancer from Azure.</span></span>

    <span data-ttu-id="a4938-164">Carregar o recurso de Balanceador de carga de saudação em uma variável (se você ainda não tiver feito isso ainda).</span><span class="sxs-lookup"><span data-stu-id="a4938-164">Load hello load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="a4938-165">variável de saudação é chamado **$lb**. Use Olá mesmo nomes de recurso Olá de Balanceador de carga que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a4938-165">hello variable is called **$lb**. Use hello same names from hello load balancer resource that you created earlier.</span></span>

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. <span data-ttu-id="a4938-166">Variável de tooa de configuração de back-end de Olá de carga.</span><span class="sxs-lookup"><span data-stu-id="a4938-166">Load hello back-end configuration tooa variable.</span></span>

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. <span data-ttu-id="a4938-167">Carregar a interface de rede Olá já criado em uma variável.</span><span class="sxs-lookup"><span data-stu-id="a4938-167">Load hello already created network interface into a variable.</span></span> <span data-ttu-id="a4938-168">é o nome da variável Olá **$nic**.</span><span class="sxs-lookup"><span data-stu-id="a4938-168">hello variable name is **$nic**.</span></span> <span data-ttu-id="a4938-169">Olá nome da interface de rede é Olá mesmo da saudação exemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="a4938-169">hello network interface name is hello same one from hello earlier example.</span></span>

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. <span data-ttu-id="a4938-170">Alterar configuração de back-end de saudação na interface de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4938-170">Change hello back-end configuration on hello network interface.</span></span>

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. <span data-ttu-id="a4938-171">Salve o objeto de interface de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4938-171">Save hello network interface object.</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    <span data-ttu-id="a4938-172">Depois que uma interface de rede é adicionada toohello pool de back-end do balanceador de carga, ele começa a receber o tráfego de rede com base em regras de balanceamento de carga Olá para esse recurso de Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="a4938-172">After a network interface is added toohello load balancer back-end pool, it starts receiving network traffic based on hello load-balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="a4938-173">Atualizar um balanceador de carga existente</span><span class="sxs-lookup"><span data-stu-id="a4938-173">Update an existing load balancer</span></span>

1. <span data-ttu-id="a4938-174">Usando Olá de Balanceador de carga Olá exemplo anterior, atribua uma variável de toohello de objeto de Balanceador de carga **$slb** usando `Get-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="a4938-174">By using hello load balancer from hello earlier example, assign a load balancer object toohello variable **$slb** by using `Get-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. <span data-ttu-id="a4938-175">Saudação de exemplo a seguir, você adiciona uma regra NAT de entrada – usando a porta 81 no pool de front-end hello e 8181 a porta para o pool de back-end hello – tooan balanceador de carga existente.</span><span class="sxs-lookup"><span data-stu-id="a4938-175">In hello following example, you add an inbound NAT rule--by using port 81 in hello front-end pool and port 8181 for hello back-end pool--tooan existing load balancer.</span></span>

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. <span data-ttu-id="a4938-176">Salvar a nova configuração de saudação usando `Set-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="a4938-176">Save hello new configuration by using `Set-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="a4938-177">Remover um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="a4938-177">Remove a load balancer</span></span>

<span data-ttu-id="a4938-178">Use o comando Olá `Remove-AzureLoadBalancer` toodelete um balanceador de carga criado anteriormente denominado **NRP LB** em um grupo de recursos chamado **NRP RG**.</span><span class="sxs-lookup"><span data-stu-id="a4938-178">Use hello command `Remove-AzureLoadBalancer` toodelete a previously created load balancer named **NRP-LB** in a resource group called **NRP-RG**.</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="a4938-179">Você pode usar a opção Olá **-Force** tooavoid prompt de saudação para exclusão.</span><span class="sxs-lookup"><span data-stu-id="a4938-179">You can use hello optional switch **-Force** tooavoid hello prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4938-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a4938-180">Next steps</span></span>

[<span data-ttu-id="a4938-181">Introdução à configuração de um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="a4938-181">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="a4938-182">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="a4938-182">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="a4938-183">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="a4938-183">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
