---
title: "Configurar o túnel forçado para conexões Site a Site: Resource Manager | Microsoft Docs"
description: "Como redirecionar ou 'forçar' todo o tráfego direcionado à Internet para sua localização local."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cbe58db8-b598-4c9f-ac88-62c865eb8721
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 207c53924863eb51ee369fe46d5ad12fb1905c53
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="configure-forced-tunneling-using-the-azure-resource-manager-deployment-model"></a><span data-ttu-id="f889b-103">Configurar o túnel forçado usando o modelo de implantação do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f889b-103">Configure forced tunneling using the Azure Resource Manager deployment model</span></span>

<span data-ttu-id="f889b-104">O túnel forçado permite redirecionar ou "forçar" todo o tráfego direcionado para a Internet de volta para seu local por meio de um túnel VPN de Site a Site para inspeção e auditoria.</span><span class="sxs-lookup"><span data-stu-id="f889b-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="f889b-105">Esse é um requisito crítico de segurança para a maioria das políticas de TI empresariais.</span><span class="sxs-lookup"><span data-stu-id="f889b-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="f889b-106">Sem o túnel forçado, o tráfego direcionado para Internet de suas VMs no Azure sempre percorrerão da infraestrutura de rede do Azure diretamente para a Internet, sem a opção para permitir que você inspecione ou audite o tráfego.</span><span class="sxs-lookup"><span data-stu-id="f889b-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure always traverses from Azure network infrastructure directly out to the Internet, without the option to allow you to inspect or audit the traffic.</span></span> <span data-ttu-id="f889b-107">O acesso não autorizado à Internet pode levar à divulgação de informações ou outros tipos de violações de segurança.</span><span class="sxs-lookup"><span data-stu-id="f889b-107">Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

<span data-ttu-id="f889b-108">Este artigo o guia pela configuração de túnel forçado para redes virtuais criadas usando o modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f889b-108">This article walks you through configuring forced tunneling for virtual networks created using the Resource Manager deployment model.</span></span> <span data-ttu-id="f889b-109">O túnel forçado pode ser configurado usando o PowerShell, não por meio do portal.</span><span class="sxs-lookup"><span data-stu-id="f889b-109">Forced tunneling can be configured by using PowerShell, not through the portal.</span></span> <span data-ttu-id="f889b-110">Se você quiser configurar o túnel forçado para o modelo de implantação clássica, selecione o artigo clássico na lista suspensa abaixo:</span><span class="sxs-lookup"><span data-stu-id="f889b-110">If you want to configure forced tunneling for the classic deployment model, select classic article from the following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f889b-111">PowerShell - clássico</span><span class="sxs-lookup"><span data-stu-id="f889b-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="f889b-112">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f889b-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a><span data-ttu-id="f889b-113">Sobre túnel forçado</span><span class="sxs-lookup"><span data-stu-id="f889b-113">About forced tunneling</span></span>

<span data-ttu-id="f889b-114">O diagrama a seguir ilustra o funcionamento do túnel forçado.</span><span class="sxs-lookup"><span data-stu-id="f889b-114">The following diagram illustrates how forced tunneling works.</span></span> 

![Túnel forçado](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

<span data-ttu-id="f889b-116">No exemplo acima, a sub-rede Front-end não é um túnel forçado.</span><span class="sxs-lookup"><span data-stu-id="f889b-116">In the example above, the Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="f889b-117">As cargas de trabalho na sub-rede do front-end podem continuar a aceitar e a responder diretamente às solicitações de clientes da Internet.</span><span class="sxs-lookup"><span data-stu-id="f889b-117">The workloads in the Frontend subnet can continue to accept and respond to customer requests from the Internet directly.</span></span> <span data-ttu-id="f889b-118">As sub-redes de Camada intermediária e Back-end são túneis forçados.</span><span class="sxs-lookup"><span data-stu-id="f889b-118">The Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="f889b-119">As conexões de saída dessas duas sub-redes com a Internet serão forçadas ou redirecionadas de volta ao site local por meio de túneis de VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="f889b-119">Any outbound connections from these two subnets to the Internet will be forced or redirected back to an on-premises site via one of the S2S VPN tunnels.</span></span>

<span data-ttu-id="f889b-120">Isso permite que você restrinja e inspecione o acesso à Internet de suas máquinas virtuais ou serviços de nuvem no Azure, continuando a habilitar a arquitetura de serviço de várias camadas necessária.</span><span class="sxs-lookup"><span data-stu-id="f889b-120">This allows you to restrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing to enable your multi-tier service architecture required.</span></span> <span data-ttu-id="f889b-121">Se não houver cargas de trabalho voltadas para a Internet em suas redes virtuais, você também poderá aplicar o túnel forçado às redes virtuais inteiras.</span><span class="sxs-lookup"><span data-stu-id="f889b-121">If there are no Internet-facing workloads in your virtual networks, you also can apply forced tunneling to the entire virtual networks.</span></span>

## <a name="requirements-and-considerations"></a><span data-ttu-id="f889b-122">Requisitos e considerações</span><span class="sxs-lookup"><span data-stu-id="f889b-122">Requirements and considerations</span></span>

<span data-ttu-id="f889b-123">O túnel forçado no Azure é configurado por meio de rotas de rede virtual definidas pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="f889b-123">Forced tunneling in Azure is configured via virtual network user-defined routes.</span></span> <span data-ttu-id="f889b-124">Redirecionar o tráfego para um site local é expressado como uma Rota Padrão para o gateway de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="f889b-124">Redirecting traffic to an on-premises site is expressed as a Default Route to the Azure VPN gateway.</span></span> <span data-ttu-id="f889b-125">Para saber mais sobre rotas definidas pelo usuário e redes virtuais, confira [Encaminhamento IP e rotas definidas pelo usuário](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f889b-125">For more information about user-defined routing and virtual networks, see [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>

* <span data-ttu-id="f889b-126">Cada sub-rede de rede virtual tem uma tabela de roteamento interna do sistema.</span><span class="sxs-lookup"><span data-stu-id="f889b-126">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="f889b-127">A tabela de roteamento do sistema tem estes três grupos de rotas:</span><span class="sxs-lookup"><span data-stu-id="f889b-127">The system routing table has the following three groups of routes:</span></span>
  
  * <span data-ttu-id="f889b-128">**Rotas locais de Rede Virtual:** diretamente para as VMs de destino na mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="f889b-128">**Local VNet routes:** Directly to the destination VMs in the same virtual network.</span></span>
  * <span data-ttu-id="f889b-129">**Rotas locais:** para o gateway de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="f889b-129">**On-premises routes:** To the Azure VPN gateway.</span></span>
  * <span data-ttu-id="f889b-130">**Rota padrão:** diretamente para a Internet.</span><span class="sxs-lookup"><span data-stu-id="f889b-130">**Default route:** Directly to the Internet.</span></span> <span data-ttu-id="f889b-131">Os pacotes destinados para os endereços IP privados não cobertos pelas duas rotas anteriores serão removidos.</span><span class="sxs-lookup"><span data-stu-id="f889b-131">Packets destined to the private IP addresses not covered by the previous two routes are dropped.</span></span>
* <span data-ttu-id="f889b-132">Este procedimento usa rotas definidas pelo usuário (UDR) a fim de criar uma tabela de roteamento para adicionar uma rota padrão e associar a tabela de roteamento às sub-redes de VNet para habilitar o túnel forçado nessas sub-redes.</span><span class="sxs-lookup"><span data-stu-id="f889b-132">This procedure uses user-defined routes (UDR) to create a routing table to add a default route, and then associate the routing table to your VNet subnet(s) to enable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="f889b-133">O túnel forçado deve ser associado a uma Rede Virtual que tenha um Gateway de VPN de roteamento.</span><span class="sxs-lookup"><span data-stu-id="f889b-133">Forced tunneling must be associated with a VNet that has a route-based VPN gateway.</span></span> <span data-ttu-id="f889b-134">Você precisa definir um "site padrão" entre sites locais entre locais conectado à rede virtual.</span><span class="sxs-lookup"><span data-stu-id="f889b-134">You need to set a "default site" among the cross-premises local sites connected to the virtual network.</span></span> <span data-ttu-id="f889b-135">Além disso, o dispositivo VPN local deve ser configurado usando 0.0.0.0/0 como seletores de tráfego.</span><span class="sxs-lookup"><span data-stu-id="f889b-135">Also, the on-premises VPN device must be configured using 0.0.0.0/0 as traffic selectors.</span></span> 
* <span data-ttu-id="f889b-136">O túnel forçado do ExpressRoute não é configurado por meio deste mecanismo, mas é habilitado por meio do anúncio de uma rota padrão por meio de sessões de emparelhamento via protocolo BGP do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f889b-136">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via the ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="f889b-137">Para saber mais, veja a [documentação do ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).</span><span class="sxs-lookup"><span data-stu-id="f889b-137">For more information, see the [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/).</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="f889b-138">Visão geral de configuração</span><span class="sxs-lookup"><span data-stu-id="f889b-138">Configuration overview</span></span>

<span data-ttu-id="f889b-139">O procedimento a seguir o ajudará a criar um grupo de recursos e uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="f889b-139">The following procedure helps you create a resource group and a VNet.</span></span> <span data-ttu-id="f889b-140">Em seguida, você criará um gateway de VPN e configurará um túnel forçado.</span><span class="sxs-lookup"><span data-stu-id="f889b-140">You'll then create a VPN gateway and configure forced tunneling.</span></span> <span data-ttu-id="f889b-141">Nesse procedimento, a rede virtual "MultiTier-VNet" tem três sub-redes: ‘Frontend’, ‘Midtier’ e ‘Backend’, com quatro conexões entre locais: ‘DefaultSiteHQ’ e três Branches.</span><span class="sxs-lookup"><span data-stu-id="f889b-141">In this procedure, the virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend', with four cross-premises connections: 'DefaultSiteHQ', and three Branches.</span></span>

<span data-ttu-id="f889b-142">As etapas do procedimento definem ‘DefaultSiteHQ’ como a conexão de site padrão para o túnel forçado e configuram as sub-redes Midtier e Back-end para usarem túnel forçado.</span><span class="sxs-lookup"><span data-stu-id="f889b-142">The procedure steps set the 'DefaultSiteHQ' as the default site connection for forced tunneling, and configure the 'Midtier' and 'Backend' subnets to use forced tunneling.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f889b-143">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="f889b-143">Before you begin</span></span>

<span data-ttu-id="f889b-144">Instale a versão mais recente dos cmdlets do PowerShell do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f889b-144">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="f889b-145">Consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview) para saber mais sobre como instalar os cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f889b-145">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span>

### <a name="to-log-in"></a><span data-ttu-id="f889b-146">Para fazer logon</span><span class="sxs-lookup"><span data-stu-id="f889b-146">To log in</span></span>

[!INCLUDE [To log in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a><span data-ttu-id="f889b-147">Configurar o túnel forçado</span><span class="sxs-lookup"><span data-stu-id="f889b-147">Configure forced tunneling</span></span>

1. <span data-ttu-id="f889b-148">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="f889b-148">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. <span data-ttu-id="f889b-149">Crie uma rede virtual e especifique as sub-redes.</span><span class="sxs-lookup"><span data-stu-id="f889b-149">Create a virtual network and specify subnets.</span></span>

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. <span data-ttu-id="f889b-150">Crie os gateways de rede local.</span><span class="sxs-lookup"><span data-stu-id="f889b-150">Create the local network gateways.</span></span>

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. <span data-ttu-id="f889b-151">Crie uma regra e uma tabela de rotas.</span><span class="sxs-lookup"><span data-stu-id="f889b-151">Create the route table and route rule.</span></span>

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. <span data-ttu-id="f889b-152">Associe a tabela de rotas criada acima às sub-redes Mid-Tier e Back-end.</span><span class="sxs-lookup"><span data-stu-id="f889b-152">Associate the route table to the Midtier and Backend subnets.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="f889b-153">Crie o gateway com um site padrão.</span><span class="sxs-lookup"><span data-stu-id="f889b-153">Create the Gateway with a default site.</span></span> <span data-ttu-id="f889b-154">Essa etapa de criação e configuração do gateway leva cerca de 45 minutos ou mais para ser concluída, pois você está criando e configurando o gateway.</span><span class="sxs-lookup"><span data-stu-id="f889b-154">This step takes some time to complete, sometimes 45 minutes or more, because you are creating and configuring the gateway.</span></span><br> <span data-ttu-id="f889b-155">O **-GatewayDefaultSite** é o parâmetro cmdlet que permite a configuração de roteamento forçada funcionar, portanto, atente-se para configurar corretamente essa configuração.</span><span class="sxs-lookup"><span data-stu-id="f889b-155">The **-GatewayDefaultSite** is the cmdlet parameter that allows the forced routing configuration to work, so take care to configure this setting properly.</span></span> <span data-ttu-id="f889b-156">Esse parâmetro está disponível no PowerShell 1.0 ou versão posterior.</span><span class="sxs-lookup"><span data-stu-id="f889b-156">This parameter is available in PowerShell 1.0 or later.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. <span data-ttu-id="f889b-157">Estabeleça as conexões VPN Site a Site.</span><span class="sxs-lookup"><span data-stu-id="f889b-157">Establish the Site-to-Site VPN connections.</span></span>

  ```powershell
  $gateway = Get-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling"
  $lng1 = Get-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" 
  $lng2 = Get-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" 
  $lng3 = Get-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" 
  $lng4 = Get-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" 
    
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng1 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng2 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng3 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection4" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng4 -ConnectionType IPsec -SharedKey "preSharedKey"
    
  Get-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling"
  ```