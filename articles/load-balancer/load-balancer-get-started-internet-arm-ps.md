---
title: Criar um balanceador de carga voltado para a Internet do Azure - PowerShell | Microsoft Docs
description: Saiba como criar um balanceador de carga para a Internet no Gerenciador de Recursos usando o PowerShell
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
ms.openlocfilehash: f610afbdfac7b5dd9a1a5eb6812c86d8ce0d63e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="c3554-103"><a name="get-started"></a>Criar um balanceador de carga para a Internet no Resource Manager usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3554-103"><a name="get-started"></a>Creating an Internet-facing load balancer in Resource Manager by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c3554-104">Portal</span><span class="sxs-lookup"><span data-stu-id="c3554-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="c3554-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3554-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="c3554-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c3554-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="c3554-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="c3554-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="c3554-108">Este artigo aborda o modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="c3554-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="c3554-109">Também é possível [Saber como criar um balanceador de carga para a Internet usando o modelo de implantação clássica](load-balancer-get-started-internet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c3554-109">You can also [learn how to create an Internet-facing load balancer by using the classic deployment model](load-balancer-get-started-internet-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-the-solution-by-using-azure-powershell"></a><span data-ttu-id="c3554-110">Implantando a solução usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3554-110">Deploying the solution by using Azure PowerShell</span></span>

<span data-ttu-id="c3554-111">Os procedimentos a seguir explicam como criar um balanceador de carga para a Internet usando o Azure Resource Manager com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c3554-111">The following procedures explain how to create an Internet-facing load balancer by using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="c3554-112">Com o Azure Resource Manager, todos os recursos são criados e configurados individualmente e colocados juntos para criar um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="c3554-112">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a load balancer.</span></span>

<span data-ttu-id="c3554-113">Você precisa criar e configurar os seguintes objetos para implantar um balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="c3554-113">You must create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="c3554-114">Configuração de IP de front-end: contém PIPs ( endereços IP públicos) para o tráfego de rede de entrada.</span><span class="sxs-lookup"><span data-stu-id="c3554-114">Front-end IP configuration: contains public IP (PIP) addresses for incoming network traffic.</span></span>
* <span data-ttu-id="c3554-115">Pool de endereços de back-end: contém NICs (interfaces de rede) para que as máquinas virtuais recebam o tráfego de rede do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="c3554-115">Back-end address pool: contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="c3554-116">Regras de balanceamento de carga: contém regras que mapeiam uma porta pública no balanceador de carga para uma porta no pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="c3554-116">Load-balancing rules: contains rules that map a public port on the load balancer to a port in the back-end address pool.</span></span>
* <span data-ttu-id="c3554-117">Regras NAT de entrada: contém regras que mapeiam uma porta pública no balanceador de carga para uma porta de uma máquina virtual específica no pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="c3554-117">Inbound NAT rules: contains rules that map a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="c3554-118">Investigações: contém investigações de integridade usadas para verificar a disponibilidade de instâncias de máquinas virtuais no pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="c3554-118">Probes: contains health probes used to check availability of virtual machine instances in the back-end address pool.</span></span>

<span data-ttu-id="c3554-119">Para saber mais, confira [Suporte do Azure Resource Manager para Balanceador de Carga](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="c3554-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-to-use-resource-manager"></a><span data-ttu-id="c3554-120">Configurar o PowerShell para usar o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="c3554-120">Set up PowerShell to use Resource Manager</span></span>

<span data-ttu-id="c3554-121">Verifique se você tem a versão de produção mais recente do módulo Azure Resource Manager para o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c3554-121">Make sure you have the latest production version of the Azure Resource Manager module for PowerShell:</span></span>

1. <span data-ttu-id="c3554-122">Entre no Azure.</span><span class="sxs-lookup"><span data-stu-id="c3554-122">Sign in to Azure.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="c3554-123">Insira suas credenciais quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="c3554-123">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="c3554-124">Verificar as assinaturas da conta.</span><span class="sxs-lookup"><span data-stu-id="c3554-124">Check the subscriptions for the account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="c3554-125">Escolha quais das suas assinaturas do Azure deseja usar.</span><span class="sxs-lookup"><span data-stu-id="c3554-125">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="c3554-126">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="c3554-126">Create a resource group.</span></span> <span data-ttu-id="c3554-127">(Ignore esta etapa se está usando um grupo de recursos existente.)</span><span class="sxs-lookup"><span data-stu-id="c3554-127">(Skip this step if you're using an existing resource group.)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-the-front-end-ip-pool"></a><span data-ttu-id="c3554-128">Criar uma rede virtual e um endereço IP público para o pool de IPs de front-end</span><span class="sxs-lookup"><span data-stu-id="c3554-128">Create a virtual network and a public IP address for the front-end IP pool</span></span>

1. <span data-ttu-id="c3554-129">Criar uma sub-rede e uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c3554-129">Create a subnet and a virtual network.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="c3554-130">Crie um recurso de endereço IP público do Azure chamado **PublicIP** a ser usado por um pool de IPs de front-end com o nome DNS **loadbalancernrp.westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="c3554-130">Create an Azure public IP address resource, named **PublicIP**, to be used by a front-end IP pool with the DNS name **loadbalancernrp.westus.cloudapp.azure.com**.</span></span> <span data-ttu-id="c3554-131">O comando a seguir usa o tipo de alocação estática.</span><span class="sxs-lookup"><span data-stu-id="c3554-131">The following command uses the static allocation type.</span></span>

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="c3554-132">O balanceador de carga usa o rótulo de domínio do IP público como prefixo para seu FQDN.</span><span class="sxs-lookup"><span data-stu-id="c3554-132">The load balancer uses the domain label of the public IP as a prefix for its FQDN.</span></span> <span data-ttu-id="c3554-133">Isso é diferente do modelo de implantação clássica, que usa o serviço de nuvem como o FQDN do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="c3554-133">This is different from the classic deployment model, which uses the cloud service as the load balancer FQDN.</span></span>
   > <span data-ttu-id="c3554-134">Neste exemplo, o FQDN é **loadbalancernrp.westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="c3554-134">In this example, the FQDN is **loadbalancernrp.westus.cloudapp.azure.com**.</span></span>

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a><span data-ttu-id="c3554-135">Criar um pool de IPs de front-end e um pool de endereços de back-end</span><span class="sxs-lookup"><span data-stu-id="c3554-135">Create a front-end IP pool and a back-end address pool</span></span>

1. <span data-ttu-id="c3554-136">Crie um pool de IPs de front-end chamado **LB-Frontend** que usa o recurso **PublicIp**.</span><span class="sxs-lookup"><span data-stu-id="c3554-136">Create a front-end IP pool named **LB-Frontend** that uses the **PublicIp** resource.</span></span>

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. <span data-ttu-id="c3554-137">Crie um pool de endereços de back-end chamado **LB-backend**.</span><span class="sxs-lookup"><span data-stu-id="c3554-137">Create a back-end address pool named **LB-backend**.</span></span>

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a><span data-ttu-id="c3554-138">Criar regras NAT, uma regra de balanceador de carga, uma investigação e um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="c3554-138">Create NAT rules, a load balancer rule, a probe, and a load balancer</span></span>

<span data-ttu-id="c3554-139">Este exemplo cria os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="c3554-139">This example creates the following items:</span></span>

* <span data-ttu-id="c3554-140">Uma regra NAT para converter todo o tráfego de entrada na porta 3441 para a porta 3389</span><span class="sxs-lookup"><span data-stu-id="c3554-140">A NAT rule to translate all incoming traffic on port 3441 to port 3389</span></span>
* <span data-ttu-id="c3554-141">Uma regra NAT para converter todo o tráfego de entrada na porta 3442 para a porta 3389</span><span class="sxs-lookup"><span data-stu-id="c3554-141">A NAT rule to translate all incoming traffic on port 3442 to port 3389</span></span>
* <span data-ttu-id="c3554-142">Uma regra de teste que verifica o status de integridade em uma página denominada **HealthProbe.aspx**</span><span class="sxs-lookup"><span data-stu-id="c3554-142">A probe rule to check the health status on a page named **HealthProbe.aspx**</span></span>
* <span data-ttu-id="c3554-143">Uma regra de balanceador de carga para equilibrar todo o tráfego de entrada na porta 80 para a porta 80 de endereços no pool de back-end</span><span class="sxs-lookup"><span data-stu-id="c3554-143">A load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool</span></span>
* <span data-ttu-id="c3554-144">Um balanceador de carga que usa todos esses objetos</span><span class="sxs-lookup"><span data-stu-id="c3554-144">A load balancer that uses all these objects</span></span>

<span data-ttu-id="c3554-145">Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="c3554-145">Use these steps:</span></span>

1. <span data-ttu-id="c3554-146">Criar regras NAT.</span><span class="sxs-lookup"><span data-stu-id="c3554-146">Create the NAT rules.</span></span>

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. <span data-ttu-id="c3554-147">Crie um teste de integridade.</span><span class="sxs-lookup"><span data-stu-id="c3554-147">Create a health probe.</span></span> <span data-ttu-id="c3554-148">Há duas maneiras de configurar uma investigação:</span><span class="sxs-lookup"><span data-stu-id="c3554-148">There are two ways to configure a probe:</span></span>

    <span data-ttu-id="c3554-149">Investigação HTTP</span><span class="sxs-lookup"><span data-stu-id="c3554-149">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="c3554-150">Investigação TCP</span><span class="sxs-lookup"><span data-stu-id="c3554-150">TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. <span data-ttu-id="c3554-151">Crie uma regra de balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="c3554-151">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. <span data-ttu-id="c3554-152">Crie o balanceador de carga usando os objetos criados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c3554-152">Create the load balancer by using the previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a><span data-ttu-id="c3554-153">Criar NICs</span><span class="sxs-lookup"><span data-stu-id="c3554-153">Create NICs</span></span>

<span data-ttu-id="c3554-154">Crie interfaces de rede (ou modificar as existentes) e as associe às regras NAT, às regras do balanceador de carga e às investigações:</span><span class="sxs-lookup"><span data-stu-id="c3554-154">Create network interfaces (or modify existing ones) and then associate them to NAT rules, load balancer rules, and probes:</span></span>

1. <span data-ttu-id="c3554-155">Obtenha a rede virtual e a sub-rede da rede virtual, onde as NICs precisam ser criadas.</span><span class="sxs-lookup"><span data-stu-id="c3554-155">Get the virtual network and a virtual network subnet, where the NICs need to be created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="c3554-156">Crie uma NIC chamada **lb-nic1-be**e associe-a à primeira regra NAT e ao primeiro (e único) pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="c3554-156">Create a NIC named **lb-nic1-be**, and associate it with the first NAT rule and the first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. <span data-ttu-id="c3554-157">Crie uma NIC chamada **lb-nic2-be**e a associe à segunda regra NAT e ao primeiro (e único) pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="c3554-157">Create a NIC named **lb-nic2-be**, and associate it with the second NAT rule and the first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. <span data-ttu-id="c3554-158">Conferir as NICs.</span><span class="sxs-lookup"><span data-stu-id="c3554-158">Check the NICs.</span></span>

        $backendnic1

    <span data-ttu-id="c3554-159">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="c3554-159">Expected output:</span></span>

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

5. <span data-ttu-id="c3554-160">Use o cmdlet `Add-AzureRmVMNetworkInterface` para atribuir as NICs a VMs diferentes.</span><span class="sxs-lookup"><span data-stu-id="c3554-160">Use the `Add-AzureRmVMNetworkInterface` cmdlet to assign the NICs to different VMs.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="c3554-161">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c3554-161">Create a virtual machine</span></span>

<span data-ttu-id="c3554-162">Para obter orientação sobre como criar uma máquina virtual e atribuir uma NIC, confira [Criar uma VM do Azure usando o PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c3554-162">For guidance on creating a virtual machine and assigning a NIC, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-the-network-interface-to-the-load-balancer"></a><span data-ttu-id="c3554-163">Adicionar a interface de rede ao balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="c3554-163">Add the network interface to the load balancer</span></span>

1. <span data-ttu-id="c3554-164">Recupere o balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3554-164">Retrieve the load balancer from Azure.</span></span>

    <span data-ttu-id="c3554-165">Carregue o recurso de balanceador de carga em uma variável (se ainda não tiver feito isso).</span><span class="sxs-lookup"><span data-stu-id="c3554-165">Load the load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="c3554-166">A variável é chamada **$lb**. Use os mesmos nomes de recurso balanceador de carga que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c3554-166">The variable is called **$lb**. Use the same names from the load balancer resource that you created earlier.</span></span>

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. <span data-ttu-id="c3554-167">Carregue a configuração de back-end em uma variável.</span><span class="sxs-lookup"><span data-stu-id="c3554-167">Load the back-end configuration to a variable.</span></span>

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. <span data-ttu-id="c3554-168">Carregue a interface de rede já criada em uma variável.</span><span class="sxs-lookup"><span data-stu-id="c3554-168">Load the already created network interface into a variable.</span></span> <span data-ttu-id="c3554-169">O nome da variável é **$nic**.</span><span class="sxs-lookup"><span data-stu-id="c3554-169">The variable name is **$nic**.</span></span> <span data-ttu-id="c3554-170">O nome da interface de rede é o mesmo do exemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="c3554-170">The network interface name is the same one from the earlier example.</span></span>

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. <span data-ttu-id="c3554-171">Altere a configuração de back-end na interface de rede.</span><span class="sxs-lookup"><span data-stu-id="c3554-171">Change the back-end configuration on the network interface.</span></span>

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. <span data-ttu-id="c3554-172">Salve o objeto de interface de rede.</span><span class="sxs-lookup"><span data-stu-id="c3554-172">Save the network interface object.</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    <span data-ttu-id="c3554-173">Depois que uma interface de rede é adicionada ao pool de back-end do balanceador de carga, ela começa a receber tráfego de rede com base nas regras de balanceamento de carga para esse recurso de balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="c3554-173">After a network interface is added to the load balancer back-end pool, it starts receiving network traffic based on the load-balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="c3554-174">Atualizar um balanceador de carga existente</span><span class="sxs-lookup"><span data-stu-id="c3554-174">Update an existing load balancer</span></span>

1. <span data-ttu-id="c3554-175">Usando o balanceador de carga do exemplo anterior, atribua um objeto do balanceador de carga à variável **$slb** usando `Get-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="c3554-175">By using the load balancer from the earlier example, assign a load balancer object to the variable **$slb** by using `Get-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. <span data-ttu-id="c3554-176">No exemplo a seguir, você adiciona uma regra de NAT de entrada, usando a porta 81 no pool de front-end e a porta 8181 no pool de back-end, a um balanceador de carga existente.</span><span class="sxs-lookup"><span data-stu-id="c3554-176">In the following example, you add an inbound NAT rule--by using port 81 in the front-end pool and port 8181 for the back-end pool--to an existing load balancer.</span></span>

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. <span data-ttu-id="c3554-177">Salve a nova configuração usando `Set-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="c3554-177">Save the new configuration by using `Set-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="c3554-178">Remover um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="c3554-178">Remove a load balancer</span></span>

<span data-ttu-id="c3554-179">Use o comando `Remove-AzureLoadBalancer` para excluir um balanceador de carga criado anteriormente chamado **NRP-LB** em um grupo de recursos chamado **NRP-RG**.</span><span class="sxs-lookup"><span data-stu-id="c3554-179">Use the command `Remove-AzureLoadBalancer` to delete a previously created load balancer named **NRP-LB** in a resource group called **NRP-RG**.</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="c3554-180">Você pode usar a opção **-Force** para evitar a solicitação de exclusão.</span><span class="sxs-lookup"><span data-stu-id="c3554-180">You can use the optional switch **-Force** to avoid the prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3554-181">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c3554-181">Next steps</span></span>

[<span data-ttu-id="c3554-182">Introdução à configuração de um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="c3554-182">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="c3554-183">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="c3554-183">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="c3554-184">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="c3554-184">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
