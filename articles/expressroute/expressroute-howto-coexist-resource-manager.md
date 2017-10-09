---
title: "Configurar as conexões de VPN ExpressRoute e Site a Site que possam coexistir: Resource Manager: Azure | Microsoft Docs"
description: "Este artigo o orienta na configuração da conexão VPN de Site a Site e do ExpressRoute que pode coexistir para o modelo do Gerenciador de Recursos."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7717b14-3da3-4a6d-b78e-a5020766bc2c
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: charwen,cherylmc
ms.openlocfilehash: efda9f89d95617c8c4e75af91b20631dc468d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a><span data-ttu-id="42506-103">Configurar conexões coexistentes Site a Site e do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="42506-103">Configure ExpressRoute and Site-to-Site coexisting connections</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="42506-104">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="42506-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="42506-105">PowerShell - clássico</span><span class="sxs-lookup"><span data-stu-id="42506-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="42506-106">Configurar conexões coexistentes VPN Site a Site e a ExpressRoute tem várias vantagens.</span><span class="sxs-lookup"><span data-stu-id="42506-106">Configuring Site-to-Site VPN and ExpressRoute coexisting connections has several advantages.</span></span> <span data-ttu-id="42506-107">Você pode configurar uma VPN Site a Site como um caminho de failover seguro para ExressRoute ou usar VPNs Site a Site tooconnect toosites que não estão conectados por meio de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="42506-107">You can configure a Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs tooconnect toosites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="42506-108">Abordaremos Olá etapas tooconfigure ambos os cenários neste artigo.</span><span class="sxs-lookup"><span data-stu-id="42506-108">We cover hello steps tooconfigure both scenarios in this article.</span></span> <span data-ttu-id="42506-109">Este artigo se aplica o modelo de implantação do Gerenciador de recursos de toohello e usa o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="42506-109">This article applies toohello Resource Manager deployment model and uses PowerShell.</span></span> <span data-ttu-id="42506-110">Essa configuração não está disponível no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="42506-110">This configuration is not available in hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="42506-111">Circuitos de rota expressa devem ser configurados previamente antes de seguir as instruções de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="42506-111">ExpressRoute circuits must be pre-configured before you follow hello instructions below.</span></span> <span data-ttu-id="42506-112">Certifique-se de que você seguiu Olá guias muito[criar um circuito ExpressRoute](expressroute-howto-circuit-arm.md) e [configurar o roteamento](expressroute-howto-routing-arm.md) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="42506-112">Make sure that you have followed hello guides too[create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [configure routing](expressroute-howto-routing-arm.md) before you proceed.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="42506-113">Limites e limitações</span><span class="sxs-lookup"><span data-stu-id="42506-113">Limits and limitations</span></span>
* <span data-ttu-id="42506-114">**Não há suporte para o roteamento do tráfego.**</span><span class="sxs-lookup"><span data-stu-id="42506-114">**Transit routing is not supported.**</span></span> <span data-ttu-id="42506-115">Não é possível fazer o roteamento (por meio do Azure) entre sua rede local conectada via VPN Site a Site e sua rede local conectada via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="42506-115">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="42506-116">**Não há suporte para o gateway SKU básico.**</span><span class="sxs-lookup"><span data-stu-id="42506-116">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="42506-117">Você deve usar um gateway de SKU não básica para ambos os Olá [gateway de rota expressa](expressroute-about-virtual-network-gateways.md) e hello [gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="42506-117">You must use a non-Basic SKU gateway for both hello [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and hello [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="42506-118">**Há suporte para apenas um gateway de VPN baseado em rotas.**</span><span class="sxs-lookup"><span data-stu-id="42506-118">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="42506-119">Você deve usar uma rota baseada no [Gateway de VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="42506-119">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="42506-120">**O roteamento estático deve ser configurado para o gateway de VPN.**</span><span class="sxs-lookup"><span data-stu-id="42506-120">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="42506-121">Se sua rede local está conectada tooboth ExpressRoute e uma Site a Site VPN, você deve ter uma rota estática configurada em sua rede local tooroute Olá Site a Site VPN conexão toohello Internet pública.</span><span class="sxs-lookup"><span data-stu-id="42506-121">If your local network is connected tooboth ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network tooroute hello Site-to-Site VPN connection toohello public Internet.</span></span>
* <span data-ttu-id="42506-122">**Gateway de rota expressa deve ser configurado primeiro e vinculados tooa circuito.**</span><span class="sxs-lookup"><span data-stu-id="42506-122">**ExpressRoute gateway must be configured first and linked tooa circuit.**</span></span> <span data-ttu-id="42506-123">Você deve primeiro criar o gateway de rota expressa hello e vinculá-la circuitos tooa antes de adicionar o gateway VPN Olá Site a Site.</span><span class="sxs-lookup"><span data-stu-id="42506-123">You must create hello ExpressRoute gateway first and link it tooa circuit before you add hello Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="42506-124">Designs de configuração</span><span class="sxs-lookup"><span data-stu-id="42506-124">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="42506-125">Configurar uma VPN site a site como um caminho de failover para o ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="42506-125">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="42506-126">Você pode configurar uma conexão VPN site a site como um backup para o ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="42506-126">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="42506-127">Isso se aplica apenas toovirtual redes vinculado toohello caminho de emparelhamento particular do Azure.</span><span class="sxs-lookup"><span data-stu-id="42506-127">This applies only toovirtual networks linked toohello Azure private peering path.</span></span> <span data-ttu-id="42506-128">Não há uma solução de failover com base em VPN para serviços acessíveis por meio de emparelhamentos público do Azure e da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="42506-128">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="42506-129">Olá circuito de rota expressa é sempre link principal hello.</span><span class="sxs-lookup"><span data-stu-id="42506-129">hello ExpressRoute circuit is always hello primary link.</span></span> <span data-ttu-id="42506-130">Fluxos de dados por meio do caminho VPN Site a Site Olá somente se Olá circuito ExpressRoute falhar.</span><span class="sxs-lookup"><span data-stu-id="42506-130">Data flows through hello Site-to-Site VPN path only if hello ExpressRoute circuit fails.</span></span>

> [!NOTE]
> <span data-ttu-id="42506-131">Enquanto circuito de rota expressa é preferível por VPN Site a Site quando ambas as rotas são Olá mesmo, o Azure usará hello mais longa correspondência toochoose Olá rota de prefixo para o destino do pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="42506-131">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are hello same, Azure will use hello longest prefix match toochoose hello route towards hello packet's destination.</span></span>
> 
> 

![Coexistência](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a><span data-ttu-id="42506-133">Configurar um toosites tooconnect VPN Site a Site não está conectado por meio de rota expressa</span><span class="sxs-lookup"><span data-stu-id="42506-133">Configure a Site-to-Site VPN tooconnect toosites not connected through ExpressRoute</span></span>
<span data-ttu-id="42506-134">Você pode configurar sua rede onde alguns sites se conectam diretamente tooAzure por VPN Site a Site, e alguns sites se conectam por meio de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="42506-134">You can configure your network where some sites connect directly tooAzure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Coexistência](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="42506-136">Não é possível configurar uma rede virtual como um roteador de trânsito.</span><span class="sxs-lookup"><span data-stu-id="42506-136">You cannot configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-hello-steps-toouse"></a><span data-ttu-id="42506-137">Selecionando Olá etapas toouse</span><span class="sxs-lookup"><span data-stu-id="42506-137">Selecting hello steps toouse</span></span>
<span data-ttu-id="42506-138">Há dois conjuntos diferentes de toochoose procedimentos de.</span><span class="sxs-lookup"><span data-stu-id="42506-138">There are two different sets of procedures toochoose from.</span></span> <span data-ttu-id="42506-139">procedimento de configuração de saudação selecionado depende se você tiver uma rede virtual existente que você deseja tooconnect para, ou você deseja toocreate uma nova rede virtual.</span><span class="sxs-lookup"><span data-stu-id="42506-139">hello configuration procedure that you select depends on whether you have an existing virtual network that you want tooconnect to, or you want toocreate a new virtual network.</span></span>

* <span data-ttu-id="42506-140">Não tem uma rede virtual e precisa toocreate um.</span><span class="sxs-lookup"><span data-stu-id="42506-140">I don't have a VNet and need toocreate one.</span></span>
  
    <span data-ttu-id="42506-141">Se você ainda não tiver uma rede virtual, esse procedimento explica como criar uma nova rede virtual usando o modelo de implantação do Gerenciador de Recursos e criando novas conexões de VPN Site a Site e de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="42506-141">If you don’t already have a virtual network, this procedure walks you through creating a new virtual network using Resource Manager deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="42506-142">tooconfigure uma rede virtual, execute as etapas de saudação em [toocreate uma nova rede virtual e conexões coexistentes](#new).</span><span class="sxs-lookup"><span data-stu-id="42506-142">tooconfigure a virtual network, follow hello steps in [toocreate a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="42506-143">Eu já tenho uma VNet do modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="42506-143">I already have a Resource Manager deployment model VNet.</span></span>
  
    <span data-ttu-id="42506-144">Talvez você já tenha uma rede virtual implementada com uma conexão de VPN Site a Site ou uma conexão de ExpressRoute existente.</span><span class="sxs-lookup"><span data-stu-id="42506-144">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="42506-145">Olá [conexões coexistentes do tooconfigure para uma rede virtual já existente](#add) seção orienta você por excluir gateway hello e, em seguida, criar novas conexões de VPN Site a Site e rota expressa.</span><span class="sxs-lookup"><span data-stu-id="42506-145">hello [tooconfigure coexisting connections for an already existing VNet](#add) section walks you through deleting hello gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="42506-146">Ao criar novas conexões de hello, etapas de saudação devem ser concluídas em uma ordem específica.</span><span class="sxs-lookup"><span data-stu-id="42506-146">When creating hello new connections, hello steps must be completed in a specific order.</span></span> <span data-ttu-id="42506-147">Não use instruções Olá toocreate outros artigos seus gateways e conexões.</span><span class="sxs-lookup"><span data-stu-id="42506-147">Don't use hello instructions in other articles toocreate your gateways and connections.</span></span>
  
    <span data-ttu-id="42506-148">Neste procedimento, a criação de conexões que podem coexistir requer que você toodelete seu gateway e configure novos gateways.</span><span class="sxs-lookup"><span data-stu-id="42506-148">In this procedure, creating connections that can coexist requires you toodelete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="42506-149">Você terá tempo de inatividade para as conexões entre locais enquanto você excluir e recria o gateway e conexões, mas você não precisará toomigrate qualquer uma das sua VMs ou serviços tooa nova rede virtual.</span><span class="sxs-lookup"><span data-stu-id="42506-149">You will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need toomigrate any of your VMs or services tooa new virtual network.</span></span> <span data-ttu-id="42506-150">Suas máquinas virtuais e serviços ainda serão toocommunicate capaz de saída por meio do balanceador de carga Olá enquanto você configurar seu gateway se eles estiverem toodo configurado assim.</span><span class="sxs-lookup"><span data-stu-id="42506-150">Your VMs and services will still be able toocommunicate out through hello load balancer while you configure your gateway if they are configured toodo so.</span></span>

## <span data-ttu-id="42506-151"><a name="new"></a>conexões coexistentes e toocreate uma nova rede virtual</span><span class="sxs-lookup"><span data-stu-id="42506-151"><a name="new"></a>toocreate a new virtual network and coexisting connections</span></span>
<span data-ttu-id="42506-152">Este procedimento orientará você na criação de uma VNet, bem como na criação das conexões Site a Site e de ExpressRoute que coexistirão.</span><span class="sxs-lookup"><span data-stu-id="42506-152">This procedure walks you through creating a VNet and Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="42506-153">Instale a versão mais recente Olá de saudação cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="42506-153">Install hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="42506-154">Para obter informações sobre como instalar os cmdlets hello, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="42506-154">For information about installing hello cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="42506-155">Olá cmdlets que você pode usar para essa configuração pode ser um pouco diferente do que você talvez esteja familiarizado com.</span><span class="sxs-lookup"><span data-stu-id="42506-155">hello cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="42506-156">Se toouse Olá cmdlets ser especificado nestas instruções.</span><span class="sxs-lookup"><span data-stu-id="42506-156">Be sure toouse hello cmdlets specified in these instructions.</span></span>
2. <span data-ttu-id="42506-157">Faça logon na conta de tooyour e configurar o ambiente de saudação.</span><span class="sxs-lookup"><span data-stu-id="42506-157">Log in tooyour account and set up hello environment.</span></span>

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. <span data-ttu-id="42506-158">Crie uma rede virtual incluindo uma Sub-rede de Gateway.</span><span class="sxs-lookup"><span data-stu-id="42506-158">Create a virtual network including Gateway Subnet.</span></span> <span data-ttu-id="42506-159">Para obter mais informações sobre a configuração de rede virtual hello, consulte [configuração de rede Virtual do Azure](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="42506-159">For more information about hello virtual network configuration, see [Azure Virtual Network configuration](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="42506-160">Olá sub-rede de Gateway deve ser /27 ou um prefixo mais curto (como /26 ou /25).</span><span class="sxs-lookup"><span data-stu-id="42506-160">hello Gateway Subnet must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   > 
   > 
   
    <span data-ttu-id="42506-161">Crie uma nova VNet.</span><span class="sxs-lookup"><span data-stu-id="42506-161">Create a new VNet.</span></span>

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    <span data-ttu-id="42506-162">Adicione sub-redes.</span><span class="sxs-lookup"><span data-stu-id="42506-162">Add subnets.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="42506-163">Salve a configuração da rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="42506-163">Save hello VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="42506-164"><a name="gw">
            </a>Crie um gateway de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="42506-164"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="42506-165">Para obter mais informações sobre a configuração de gateway de rota expressa hello, consulte [configuração de gateway de rota expressa](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="42506-165">For more information about hello ExpressRoute gateway configuration, see [ExpressRoute gateway configuration](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="42506-166">Olá GatewaySKU devem ser *padrão*, *HighPerformance*, ou *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="42506-166">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. <span data-ttu-id="42506-167">Vincule um circuito de rota expressa toohello do gateway de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="42506-167">Link hello ExpressRoute gateway toohello ExpressRoute circuit.</span></span> <span data-ttu-id="42506-168">Após essa etapa foi concluída, a conexão Olá entre sua rede local e o Azure, por meio do ExpressRoute, é estabelecida.</span><span class="sxs-lookup"><span data-stu-id="42506-168">After this step has been completed, hello connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span> <span data-ttu-id="42506-169">Para obter mais informações sobre a operação de vinculação hello, consulte [tooExpressRoute VNets Link](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="42506-169">For more information about hello link operation, see [Link VNets tooExpressRoute](expressroute-howto-linkvnet-arm.md).</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <span data-ttu-id="42506-170"><a name="vpngw"></a>Em seguida, crie seu gateway de VPN Site a Site.</span><span class="sxs-lookup"><span data-stu-id="42506-170"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="42506-171">Para obter mais informações sobre a configuração de gateway VPN hello, consulte [configurar uma rede virtual com uma conexão Site a Site](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="42506-171">For more information about hello VPN gateway configuration, see [Configure a VNet with a Site-to-Site connection](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span></span> <span data-ttu-id="42506-172">Olá GatewaySKU devem ser *padrão*, *HighPerformance*, ou *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="42506-172">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span> <span data-ttu-id="42506-173">Olá VpnType deve *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="42506-173">hello VpnType must *RouteBased*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    <span data-ttu-id="42506-174">O Gateway de VPN do Azure oferece suporte ao protocolo de roteamento BGP.</span><span class="sxs-lookup"><span data-stu-id="42506-174">Azure VPN gateway supports BGP routing protocol.</span></span> <span data-ttu-id="42506-175">Você pode especificar ASN (número) para essa rede Virtual adicionando switch de Asn - Olá Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="42506-175">You can specify ASN (AS Number) for that Virtual Network by adding hello -Asn switch in hello following command.</span></span> <span data-ttu-id="42506-176">Não especificar esse parâmetro será tooAS padrão de número das 65515.</span><span class="sxs-lookup"><span data-stu-id="42506-176">Not specifying that parameter will default tooAS number 65515.</span></span>

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    <span data-ttu-id="42506-177">Você pode encontrar hello BGP de emparelhamento IP e hello como o número que o Azure usa para o gateway VPN Olá em $azureVpn.BgpSettings.BgpPeeringAddress e $azureVpn.BgpSettings.Asn.</span><span class="sxs-lookup"><span data-stu-id="42506-177">You can find hello BGP peering IP and hello AS number that Azure uses for hello VPN gateway in $azureVpn.BgpSettings.BgpPeeringAddress and $azureVpn.BgpSettings.Asn.</span></span> <span data-ttu-id="42506-178">Para obter mais informações, consulte [Configurar BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) para o gateway de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="42506-178">For more information, see [Configure BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) for Azure VPN gateway.</span></span>
7. <span data-ttu-id="42506-179">Crie uma entidade de gateway de VPN de site local.</span><span class="sxs-lookup"><span data-stu-id="42506-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="42506-180">Esse comando não configura seu gateway de VPN local.</span><span class="sxs-lookup"><span data-stu-id="42506-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="42506-181">Em vez disso, permite configurações de gateway local tooprovide hello, como o IP público hello e hello local espaço de endereço, para que hello gateway VPN do Azure pode se conectar tooit.</span><span class="sxs-lookup"><span data-stu-id="42506-181">Rather, it allows you tooprovide hello local gateway settings, such as hello public IP and hello on-premises address space, so that hello Azure VPN gateway can connect tooit.</span></span>
   
    <span data-ttu-id="42506-182">Se seu dispositivo VPN local só dá suporte a roteamento estático, você pode configurar rotas estáticas Olá Olá maneira a seguir:</span><span class="sxs-lookup"><span data-stu-id="42506-182">If your local VPN device only supports static routing, you can configure hello static routes in hello following way:</span></span>

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    <span data-ttu-id="42506-183">Se seu dispositivo VPN local com suporte Olá BGP e você deseja que o roteamento dinâmico tooenable, será necessário tooknow Olá BGP emparelhamento IP e hello como sua VPN local de número que o dispositivo usa.</span><span class="sxs-lookup"><span data-stu-id="42506-183">If your local VPN device supports hello BGP and you want tooenable dynamic routing, you need tooknow hello BGP peering IP and hello AS number that your local VPN device uses.</span></span>

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for hello BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. <span data-ttu-id="42506-184">Configure seu dispositivo tooconnect toohello novo VPN do Azure gateway de VPN local.</span><span class="sxs-lookup"><span data-stu-id="42506-184">Configure your local VPN device tooconnect toohello new Azure VPN gateway.</span></span> <span data-ttu-id="42506-185">Para obter mais informações sobre a configuração de dispositivo VPN, consulte [Configuração do Dispositivo VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="42506-185">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
9. <span data-ttu-id="42506-186">Gateway VPN Site a Site link Olá no gateway local toohello do Azure.</span><span class="sxs-lookup"><span data-stu-id="42506-186">Link hello Site-to-Site VPN gateway on Azure toohello local gateway.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <span data-ttu-id="42506-187"><a name="add"></a>conexões de coexistentes tooconfigure para uma rede virtual já existente</span><span class="sxs-lookup"><span data-stu-id="42506-187"><a name="add"></a>tooconfigure coexisting connections for an already existing VNet</span></span>
<span data-ttu-id="42506-188">Se você tiver uma rede virtual existente, verifique o tamanho de sub-rede de gateway hello.</span><span class="sxs-lookup"><span data-stu-id="42506-188">If you have an existing virtual network, check hello gateway subnet size.</span></span> <span data-ttu-id="42506-189">Se a sub-rede do gateway Olá for /28 ou /29, primeiro exclua o gateway de rede virtual hello e aumentar o tamanho de sub-rede de gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="42506-189">If hello gateway subnet is /28 or /29, you must first delete hello virtual network gateway and increase hello gateway subnet size.</span></span> <span data-ttu-id="42506-190">Olá etapas nesta seção mostram como toodo que.</span><span class="sxs-lookup"><span data-stu-id="42506-190">hello steps in this section show you how toodo that.</span></span>

<span data-ttu-id="42506-191">Se a sub-rede do gateway de saudação é /27 ou maior e rede virtual Olá é conectado por meio de rota expressa, você pode ignorar as etapas de saudação abaixo e prosseguir muito["Etapa 6 – criar um gateway VPN Site a Site"](#vpngw) na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="42506-191">If hello gateway subnet is /27 or larger and hello virtual network is connected via ExpressRoute, you can skip hello steps below and proceed too["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in hello previous section.</span></span> 

> [!NOTE]
> <span data-ttu-id="42506-192">Quando você exclui um gateway existente Olá, seus locais perderá a rede virtual do hello conexão tooyour enquanto você trabalha nessa configuração.</span><span class="sxs-lookup"><span data-stu-id="42506-192">When you delete hello existing gateway, your local premises will lose hello connection tooyour virtual network while you are working on this configuration.</span></span> 
> 
> 

1. <span data-ttu-id="42506-193">Você precisará tooinstall Olá última versão do hello cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="42506-193">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="42506-194">Para obter mais informações sobre como instalar os cmdlets, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="42506-194">For more information about installing cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="42506-195">Olá cmdlets que você pode usar para essa configuração pode ser um pouco diferente do que você talvez esteja familiarizado com.</span><span class="sxs-lookup"><span data-stu-id="42506-195">hello cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="42506-196">Se toouse Olá cmdlets ser especificado nestas instruções.</span><span class="sxs-lookup"><span data-stu-id="42506-196">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="42506-197">Exclua gateway existente Olá rota expressa ou VPN Site a Site.</span><span class="sxs-lookup"><span data-stu-id="42506-197">Delete hello existing ExpressRoute or Site-to-Site VPN gateway.</span></span>

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. <span data-ttu-id="42506-198">Exclua a Sub-rede de Gateway.</span><span class="sxs-lookup"><span data-stu-id="42506-198">Delete Gateway Subnet.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="42506-199">Adicione uma Sub-rede de Gateway que seja /27 ou maior.</span><span class="sxs-lookup"><span data-stu-id="42506-199">Add a Gateway Subnet that is /27 or larger.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="42506-200">Se você não tiver endereços IP suficientes no tamanho de sub-rede de gateway sua rede virtual tooincrease hello, será necessário tooadd mais espaço de endereço IP.</span><span class="sxs-lookup"><span data-stu-id="42506-200">If you don't have enough IP addresses left in your virtual network tooincrease hello gateway subnet size, you need tooadd more IP address space.</span></span>
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="42506-201">Salve a configuração da rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="42506-201">Save hello VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="42506-202">Neste ponto, você terá uma VNet sem nenhum gateway.</span><span class="sxs-lookup"><span data-stu-id="42506-202">At this point, you have a VNet with no gateways.</span></span> <span data-ttu-id="42506-203">novos gateways do toocreate e concluir as conexões, você pode continuar com a [etapa 4 - criar um gateway de rota expressa](#gw), encontrado em Olá precede o conjunto de etapas.</span><span class="sxs-lookup"><span data-stu-id="42506-203">toocreate new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in hello preceding set of steps.</span></span>

## <a name="tooadd-point-to-site-configuration-toohello-vpn-gateway"></a><span data-ttu-id="42506-204">gateway VPN de toohello tooadd configuração ponto a site</span><span class="sxs-lookup"><span data-stu-id="42506-204">tooadd point-to-site configuration toohello VPN gateway</span></span>
<span data-ttu-id="42506-205">Você pode seguir as etapas de saudação abaixo gateway de VPN ponto a Site tooadd configuração tooyour em uma configuração de coexistência.</span><span class="sxs-lookup"><span data-stu-id="42506-205">You can follow hello steps below tooadd Point-to-Site configuration tooyour VPN gateway in a co-existence setup.</span></span>

1. <span data-ttu-id="42506-206">Adicione o pool de endereços do Cliente VPN.</span><span class="sxs-lookup"><span data-stu-id="42506-206">Add VPN Client address pool.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. <span data-ttu-id="42506-207">Carregar tooAzure de certificado de raiz Olá VPN para o gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="42506-207">Upload hello VPN root certificate tooAzure for your VPN gateway.</span></span> <span data-ttu-id="42506-208">Neste exemplo, presume-se que esse certificado de raiz de saudação é armazenado no computador local hello, onde Olá cmdlets do PowerShell a seguir é executado.</span><span class="sxs-lookup"><span data-stu-id="42506-208">In this example, it's assumed that hello root certificate is stored in hello local machine where hello following PowerShell cmdlets are run.</span></span>

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

<span data-ttu-id="42506-209">Para saber mais sobre a VPN de Ponto a Site, confira [Configurar uma conexão de Ponto a Site](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="42506-209">For more information on Point-to-Site VPN, see [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="42506-210">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="42506-210">Next steps</span></span>
<span data-ttu-id="42506-211">Para obter mais informações sobre a rota expressa, consulte Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="42506-211">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
