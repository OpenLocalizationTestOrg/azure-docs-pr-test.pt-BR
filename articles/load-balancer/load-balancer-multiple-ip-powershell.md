---
title: "Balanceamento de carga em várias configurações de IP no Azure | Microsoft Docs"
description: "Balanceamento de carga entre as configurações de IP primárias e secundárias."
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: annahar
ms.openlocfilehash: a8550519f094ca7afcd868a14b313337627f97d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a><span data-ttu-id="e26ef-103">Balanceamento de carga em várias configurações de IP usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e26ef-103">Load balancing on multiple IP configurations using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e26ef-104">Portal</span><span class="sxs-lookup"><span data-stu-id="e26ef-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="e26ef-105">CLI</span><span class="sxs-lookup"><span data-stu-id="e26ef-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="e26ef-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e26ef-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="e26ef-107">Este artigo descreve como usar o Azure Load Balancer com vários endereços IP em uma interface de rede secundária (NIC).</span><span class="sxs-lookup"><span data-stu-id="e26ef-107">This article describes how to use Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="e26ef-108">Para este cenário, temos duas VMs executando o Windows, cada uma com uma NIC principal e uma secundária.</span><span class="sxs-lookup"><span data-stu-id="e26ef-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="e26ef-109">Cada uma das NICs secundárias possui duas configurações de IP.</span><span class="sxs-lookup"><span data-stu-id="e26ef-109">Each of the secondary NICs have two IP configurations.</span></span> <span data-ttu-id="e26ef-110">Cada VM hospeda os sites contoso.com e fabrikam.com. Cada site está associado a uma das configurações de IP na NIC secundária.</span><span class="sxs-lookup"><span data-stu-id="e26ef-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound to one of the IP configurations on the secondary NIC.</span></span> <span data-ttu-id="e26ef-111">Usamos o Azure Load Balancer para expor dois endereços IP front-end, um para cada site, a fim de distribuir o tráfego para a respectiva configuração de IP do site.</span><span class="sxs-lookup"><span data-stu-id="e26ef-111">We use Azure Load Balancer to expose two frontend IP addresses, one for each website, to distribute traffic to the respective IP configuration for the website.</span></span> <span data-ttu-id="e26ef-112">Esse cenário usa o mesmo número de porta entre os front-ends, bem como os dois endereços IP do pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="e26ef-112">This scenario uses the same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![Imagem de cenário do LB](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-to-load-balance-on-multiple-ip-configurations"></a><span data-ttu-id="e26ef-114">Etapas para o balanceamento de carga em várias configurações de IP</span><span class="sxs-lookup"><span data-stu-id="e26ef-114">Steps to load balance on multiple IP configurations</span></span>

<span data-ttu-id="e26ef-115">Execute as etapas abaixo para obter o cenário descrito neste artigo:</span><span class="sxs-lookup"><span data-stu-id="e26ef-115">Follow the steps below to achieve the scenario outlined in this article:</span></span>

1. <span data-ttu-id="e26ef-116">Instale o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="e26ef-116">Install Azure PowerShell.</span></span> <span data-ttu-id="e26ef-117">Confira [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview) para saber mais sobre como instalar a versão mais recente do Azure PowerShell, selecionar a assinatura e entrar em sua conta.</span><span class="sxs-lookup"><span data-stu-id="e26ef-117">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span></span>
2. <span data-ttu-id="e26ef-118">Crie um grupo de recursos usando as seguinte configurações:</span><span class="sxs-lookup"><span data-stu-id="e26ef-118">Create a resource group using the following settings:</span></span>

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    <span data-ttu-id="e26ef-119">Para saber mais, consulte a Etapa 2 [Criar um grupo de recursos](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e26ef-119">For more information, see Step 2 of [Create a Resource Group](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

3. <span data-ttu-id="e26ef-120">[Criar um conjunto de disponibilidade](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) para suas VMs.</span><span class="sxs-lookup"><span data-stu-id="e26ef-120">[Create an Availability Set](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) to contain your VMs.</span></span> <span data-ttu-id="e26ef-121">Para esse cenário, use o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e26ef-121">For this scenario, use the following command:</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. <span data-ttu-id="e26ef-122">Siga as instruções das etapas 3 a 5 no artigo [Criar uma VM do Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) para preparar a criação de uma VM com uma única NIC.</span><span class="sxs-lookup"><span data-stu-id="e26ef-122">Follow instructions steps 3 through 5 in [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) article to prepare the creation of a VM with a single NIC.</span></span> <span data-ttu-id="e26ef-123">Execute a etapa 6.1 e use o seguinte, em vez da etapa 6.2:</span><span class="sxs-lookup"><span data-stu-id="e26ef-123">Execute step 6.1, and use the following instead of step 6.2:</span></span>

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    <span data-ttu-id="e26ef-124">Em seguida, conclua as etapas 6.3 a 6.8 [Criar uma VM do Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e26ef-124">Then complete [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) steps 6.3 through 6.8.</span></span>

5. <span data-ttu-id="e26ef-125">Adicione uma segunda configuração de IP para cada uma das VMs.</span><span class="sxs-lookup"><span data-stu-id="e26ef-125">Add a second IP configuration to each of the VMs.</span></span> <span data-ttu-id="e26ef-126">Siga as instruções no artigo [Atribuir vários endereços IP para máquinas virtuais](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add).</span><span class="sxs-lookup"><span data-stu-id="e26ef-126">Follow the instructions in [Assign multiple IP addresses to virtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) article.</span></span> <span data-ttu-id="e26ef-127">Use as seguintes configurações:</span><span class="sxs-lookup"><span data-stu-id="e26ef-127">Use the following configuration settings:</span></span>

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    <span data-ttu-id="e26ef-128">Não é necessário associar as configurações de IP secundárias aos IPs públicos para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="e26ef-128">You do not need to associate the secondary IP configurations with public IPs for the purpose of this tutorial.</span></span> <span data-ttu-id="e26ef-129">Edite o comando para remover a parte pública de associação de IP.</span><span class="sxs-lookup"><span data-stu-id="e26ef-129">Edit the command to remove the public IP association part.</span></span>

6. <span data-ttu-id="e26ef-130">Conclua as etapas 4 a 6 deste artigo novamente para a VM2.</span><span class="sxs-lookup"><span data-stu-id="e26ef-130">Complete steps 4 through 6 of this article again for VM2.</span></span> <span data-ttu-id="e26ef-131">Substitua o nome da VM para VM2 ao fazer isso.</span><span class="sxs-lookup"><span data-stu-id="e26ef-131">Be sure to replace the VM name to VM2 when doing this.</span></span> <span data-ttu-id="e26ef-132">Observe que você não precisa criar uma rede virtual para a segunda VM.</span><span class="sxs-lookup"><span data-stu-id="e26ef-132">Note that you do not need to create a virtual network for the second VM.</span></span> <span data-ttu-id="e26ef-133">Você pode ou não criar uma nova sub-rede com base em seu caso de uso.</span><span class="sxs-lookup"><span data-stu-id="e26ef-133">You may or may not create a new subnet based on your use case.</span></span>

7. <span data-ttu-id="e26ef-134">Crie dois endereços IP públicos e armazene-os nas variáveis apropriadas, conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="e26ef-134">Create two public IP addresses and store them in the appropriate variables as shown:</span></span>

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. <span data-ttu-id="e26ef-135">Crie duas configurações de IP de front-end:</span><span class="sxs-lookup"><span data-stu-id="e26ef-135">Create two frontend IP configurations:</span></span>

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. <span data-ttu-id="e26ef-136">Crie os pools de endereços de back-end, uma investigação e regras de balanceamento de carga:</span><span class="sxs-lookup"><span data-stu-id="e26ef-136">Create your backend address pools, a probe, and your load balancing rules:</span></span>

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. <span data-ttu-id="e26ef-137">Após a criação desses recursos, crie o balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="e26ef-137">Once you have these resources created, create your load balancer:</span></span>

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. <span data-ttu-id="e26ef-138">Adicione o segundo pool de endereços back-end e a configuração de IP de front-end ao seu balanceador de carga recém-criado:</span><span class="sxs-lookup"><span data-stu-id="e26ef-138">Add the second backend address pool and frontend IP configuration to your newly created load balancer:</span></span>

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. <span data-ttu-id="e26ef-139">Os comandos a seguir obtêm as NICs e adicionam as duas configurações de IP de cada NIC ao pool de endereços de back-end do balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="e26ef-139">The commands below get the NICs and then add both IP configurations of each secondary NIC to the backend address pool of the load balancer:</span></span>

    ```powershell
    $nic1 = Get-AzureRmNetworkInterface -Name "VM1-NIC2" -ResourceGroupName "MyResourcegroup";
    $nic2 = Get-AzureRmNetworkInterface -Name "VM2-NIC2" -ResourceGroupName "MyResourcegroup";

    $nic1.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic1.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);
    $nic2.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic2.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);

    $mylb = $mylb | Set-AzureRmLoadBalancer

    $nic1 | Set-AzureRmNetworkInterface
    $nic2 | Set-AzureRmNetworkInterface
    ```

13. <span data-ttu-id="e26ef-140">Por fim, você deve configurar os registros de recurso DNS para apontar para o endereço IP do endereço IP front-end do Balanceador de Carga.</span><span class="sxs-lookup"><span data-stu-id="e26ef-140">Finally, you must configure DNS resource records to point to the respective frontend IP address of the Load Balancer.</span></span> <span data-ttu-id="e26ef-141">Você pode hospedar seus domínios no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="e26ef-141">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="e26ef-142">Para saber mais sobre como usar o DNS do Azure com o Load Balancer, confira [Usar o DNS do Azure com outros serviços do Azure](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="e26ef-142">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e26ef-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e26ef-143">Next steps</span></span>
- <span data-ttu-id="e26ef-144">Saiba mais sobre como combinar os serviços de balanceamento de carga no Azure em [Usando os serviços de balanceamento de carga no Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="e26ef-144">Learn more about how to combine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="e26ef-145">Saiba como é possível usar diferentes tipos de logs no Azure para gerenciar e solucionar problemas do balanceador de carga em [Análise de log para o Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="e26ef-145">Learn how you can use different types of logs in Azure to manage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
