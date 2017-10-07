---
title: "aaaLoad balanceamento em várias configurações de IP no Azure | Microsoft Docs"
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
ms.openlocfilehash: fe1cdb317350942ff759229491c2025e98dd24a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a><span data-ttu-id="e7e43-103">Balanceamento de carga em várias configurações de IP usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7e43-103">Load balancing on multiple IP configurations using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e7e43-104">Portal</span><span class="sxs-lookup"><span data-stu-id="e7e43-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="e7e43-105">CLI</span><span class="sxs-lookup"><span data-stu-id="e7e43-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="e7e43-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7e43-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="e7e43-107">Este artigo descreve como toouse balanceador de carga do Azure com o IP de vários endereços em uma interface de rede secundária (NIC).</span><span class="sxs-lookup"><span data-stu-id="e7e43-107">This article describes how toouse Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="e7e43-108">Para este cenário, temos duas VMs executando o Windows, cada uma com uma NIC principal e uma secundária.</span><span class="sxs-lookup"><span data-stu-id="e7e43-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="e7e43-109">Cada um dos secundários de saudação NICs têm duas configurações de IP.</span><span class="sxs-lookup"><span data-stu-id="e7e43-109">Each of hello secondary NICs have two IP configurations.</span></span> <span data-ttu-id="e7e43-110">Cada VM hospeda os sites contoso.com e fabrikam.com. Cada site é associado tooone Olá de configurações de IP em uma NIC secundário. Olá</span><span class="sxs-lookup"><span data-stu-id="e7e43-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound tooone of hello IP configurations on hello secondary NIC.</span></span> <span data-ttu-id="e7e43-111">Usamos o balanceador de carga do Azure tooexpose dois front-end endereços IP, uma para cada site, toodistribute tráfego toohello respectiva configuração de IP para o site de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7e43-111">We use Azure Load Balancer tooexpose two frontend IP addresses, one for each website, toodistribute traffic toohello respective IP configuration for hello website.</span></span> <span data-ttu-id="e7e43-112">Esse cenário usa Olá o mesmo número de porta entre os front-ends, bem como os dois endereços IP do pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="e7e43-112">This scenario uses hello same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![Imagem de cenário do LB](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a><span data-ttu-id="e7e43-114">Saldo de tooload etapas em várias configurações de IP</span><span class="sxs-lookup"><span data-stu-id="e7e43-114">Steps tooload balance on multiple IP configurations</span></span>

<span data-ttu-id="e7e43-115">Siga as próximas etapas, Olá cenário de saudação tooachieve descritos neste artigo:</span><span class="sxs-lookup"><span data-stu-id="e7e43-115">Follow hello steps below tooachieve hello scenario outlined in this article:</span></span>

1. <span data-ttu-id="e7e43-116">Instale o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7e43-116">Install Azure PowerShell.</span></span> <span data-ttu-id="e7e43-117">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter informações sobre como instalar a versão mais recente de saudação do PowerShell do Azure, selecione sua assinatura e tooyour conta de assinatura.</span><span class="sxs-lookup"><span data-stu-id="e7e43-117">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>
2. <span data-ttu-id="e7e43-118">Crie um grupo de recursos usando Olá configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7e43-118">Create a resource group using hello following settings:</span></span>

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    <span data-ttu-id="e7e43-119">Para saber mais, consulte a Etapa 2 [Criar um grupo de recursos](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e7e43-119">For more information, see Step 2 of [Create a Resource Group](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

3. <span data-ttu-id="e7e43-120">[Criar um conjunto de disponibilidade](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain suas VMs.</span><span class="sxs-lookup"><span data-stu-id="e7e43-120">[Create an Availability Set](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain your VMs.</span></span> <span data-ttu-id="e7e43-121">Para este cenário, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7e43-121">For this scenario, use hello following command:</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. <span data-ttu-id="e7e43-122">Siga as instruções as etapas de 3 a 5 [criar uma VM do Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) artigo tooprepare criação de saudação de uma VM com uma única placa de rede.</span><span class="sxs-lookup"><span data-stu-id="e7e43-122">Follow instructions steps 3 through 5 in [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) article tooprepare hello creation of a VM with a single NIC.</span></span> <span data-ttu-id="e7e43-123">Execute a etapa 6.1 e use o seguinte Olá em vez de etapa 6.2:</span><span class="sxs-lookup"><span data-stu-id="e7e43-123">Execute step 6.1, and use hello following instead of step 6.2:</span></span>

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    <span data-ttu-id="e7e43-124">Em seguida, conclua as etapas 6.3 a 6.8 [Criar uma VM do Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e7e43-124">Then complete [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) steps 6.3 through 6.8.</span></span>

5. <span data-ttu-id="e7e43-125">Adicione um segundo tooeach de configuração de IP de saudação VMs.</span><span class="sxs-lookup"><span data-stu-id="e7e43-125">Add a second IP configuration tooeach of hello VMs.</span></span> <span data-ttu-id="e7e43-126">Siga as instruções de saudação em [atribuir vários endereços IP máquinas toovirtual](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) artigo.</span><span class="sxs-lookup"><span data-stu-id="e7e43-126">Follow hello instructions in [Assign multiple IP addresses toovirtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) article.</span></span> <span data-ttu-id="e7e43-127">Use Olá definições de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7e43-127">Use hello following configuration settings:</span></span>

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    <span data-ttu-id="e7e43-128">Não é necessário tooassociate Olá secundário as configurações de IP com IPs públicos para finalidade de saudação deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="e7e43-128">You do not need tooassociate hello secondary IP configurations with public IPs for hello purpose of this tutorial.</span></span> <span data-ttu-id="e7e43-129">Edite saudação comando tooremove Olá IP associação parte pública.</span><span class="sxs-lookup"><span data-stu-id="e7e43-129">Edit hello command tooremove hello public IP association part.</span></span>

6. <span data-ttu-id="e7e43-130">Conclua as etapas 4 a 6 deste artigo novamente para a VM2.</span><span class="sxs-lookup"><span data-stu-id="e7e43-130">Complete steps 4 through 6 of this article again for VM2.</span></span> <span data-ttu-id="e7e43-131">Ser tooreplace se Olá VM nome tooVM2 ao fazer isso.</span><span class="sxs-lookup"><span data-stu-id="e7e43-131">Be sure tooreplace hello VM name tooVM2 when doing this.</span></span> <span data-ttu-id="e7e43-132">Observe que você não precisa toocreate uma rede virtual para Olá segundo VM.</span><span class="sxs-lookup"><span data-stu-id="e7e43-132">Note that you do not need toocreate a virtual network for hello second VM.</span></span> <span data-ttu-id="e7e43-133">Você pode ou não criar uma nova sub-rede com base em seu caso de uso.</span><span class="sxs-lookup"><span data-stu-id="e7e43-133">You may or may not create a new subnet based on your use case.</span></span>

7. <span data-ttu-id="e7e43-134">Crie dois endereços IP públicos e armazená-los em variáveis apropriadas hello, conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="e7e43-134">Create two public IP addresses and store them in hello appropriate variables as shown:</span></span>

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. <span data-ttu-id="e7e43-135">Crie duas configurações de IP de front-end:</span><span class="sxs-lookup"><span data-stu-id="e7e43-135">Create two frontend IP configurations:</span></span>

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. <span data-ttu-id="e7e43-136">Crie os pools de endereços de back-end, uma investigação e regras de balanceamento de carga:</span><span class="sxs-lookup"><span data-stu-id="e7e43-136">Create your backend address pools, a probe, and your load balancing rules:</span></span>

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. <span data-ttu-id="e7e43-137">Após a criação desses recursos, crie o balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="e7e43-137">Once you have these resources created, create your load balancer:</span></span>

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. <span data-ttu-id="e7e43-138">Adicione Olá segundo back-end endereço front-end e pool de IP configuration tooyour recém-criado balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="e7e43-138">Add hello second backend address pool and frontend IP configuration tooyour newly created load balancer:</span></span>

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. <span data-ttu-id="e7e43-139">comandos de saudação abaixo obtém Olá NICs e, em seguida, adicione o que balanceador de carga de ambas as configurações de IP cada secundário NIC toohello back-end do pool de endereços de saudação:</span><span class="sxs-lookup"><span data-stu-id="e7e43-139">hello commands below get hello NICs and then add both IP configurations of each secondary NIC toohello backend address pool of hello load balancer:</span></span>

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

13. <span data-ttu-id="e7e43-140">Por fim, você deve configurar o recurso registros toopoint toohello front-end respectivo endereço IP de DNS Olá balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="e7e43-140">Finally, you must configure DNS resource records toopoint toohello respective frontend IP address of hello Load Balancer.</span></span> <span data-ttu-id="e7e43-141">Você pode hospedar seus domínios no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7e43-141">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="e7e43-142">Para saber mais sobre como usar o DNS do Azure com o Load Balancer, confira [Usar o DNS do Azure com outros serviços do Azure](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="e7e43-142">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7e43-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e7e43-143">Next steps</span></span>
- <span data-ttu-id="e7e43-144">Saiba mais sobre como o balanceamento de carga de toocombine serviços no Azure em [usando os serviços de balanceamento de carga no Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="e7e43-144">Learn more about how toocombine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="e7e43-145">Saiba como você pode usar diferentes tipos de logs no Azure toomanage e solucionar problemas de Balanceador de carga no [de análise de Log para o balanceador de carga do Azure](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="e7e43-145">Learn how you can use different types of logs in Azure toomanage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
