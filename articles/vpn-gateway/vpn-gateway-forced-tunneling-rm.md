---
title: "Configurar o túnel forçado para conexões Site a Site: Resource Manager | Microsoft Docs"
description: "Como tooyour voltar do tráfego de Internet associado do tooredirect ou 'force' todos os no local."
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
ms.openlocfilehash: 6bc52c04ab0749a674c9863be5e4f9a9f7c98df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-azure-resource-manager-deployment-model"></a><span data-ttu-id="0cfd5-103">Configurar o túnel forçado usando o modelo de implantação do Azure Resource Manager Olá</span><span class="sxs-lookup"><span data-stu-id="0cfd5-103">Configure forced tunneling using hello Azure Resource Manager deployment model</span></span>

<span data-ttu-id="0cfd5-104">Forçado permite redirecionar ou "forçar" todos os direcionado à Internet tráfego tooyour back local através de um túnel VPN Site a Site para inspeção e auditoria de túnel.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="0cfd5-105">Esse é um requisito crítico de segurança para a maioria das políticas de TI empresariais.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="0cfd5-106">Sem o túnel forçado, o tráfego direcionado à Internet de suas VMs no Azure sempre atravessa da infraestrutura de rede do Azure diretamente out toohello Internet, sem Olá opção tooallow você tráfego de saudação tooinspect ou auditoria.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure always traverses from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="0cfd5-107">Acesso não autorizado pode levar a divulgação de tooinformation ou outros tipos de violações de segurança.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-107">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

<span data-ttu-id="0cfd5-108">Este artigo o orienta pela configuração forçado túnel para redes virtuais criadas usando o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-108">This article walks you through configuring forced tunneling for virtual networks created using hello Resource Manager deployment model.</span></span> <span data-ttu-id="0cfd5-109">O túnel forçado pode ser configurado usando o PowerShell, não por meio do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-109">Forced tunneling can be configured by using PowerShell, not through hello portal.</span></span> <span data-ttu-id="0cfd5-110">Se você quiser tooconfigure encapsulamento para o modelo de implantação clássico Olá forçado, selecione artigo clássico Olá lista suspensa a seguir:</span><span class="sxs-lookup"><span data-stu-id="0cfd5-110">If you want tooconfigure forced tunneling for hello classic deployment model, select classic article from hello following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0cfd5-111">PowerShell - clássico</span><span class="sxs-lookup"><span data-stu-id="0cfd5-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="0cfd5-112">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0cfd5-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a><span data-ttu-id="0cfd5-113">Sobre túnel forçado</span><span class="sxs-lookup"><span data-stu-id="0cfd5-113">About forced tunneling</span></span>

<span data-ttu-id="0cfd5-114">Olá diagrama a seguir ilustra os túneis forçados como funcionam.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-114">hello following diagram illustrates how forced tunneling works.</span></span> 

![Túnel forçado](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

<span data-ttu-id="0cfd5-116">O exemplo hello acima, Olá front-end subrede não será forçada encapsulado.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-116">In hello example above, hello Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="0cfd5-117">cargas de trabalho Olá na sub-rede de front-end Olá podem continuar tooaccept e responde solicitações toocustomer de saudação Internet diretamente.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-117">hello workloads in hello Frontend subnet can continue tooaccept and respond toocustomer requests from hello Internet directly.</span></span> <span data-ttu-id="0cfd5-118">Olá sub-redes de camada intermediária e back-end são forçados encapsulado.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-118">hello Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="0cfd5-119">Quaisquer conexões de saída da toohello duas sub-redes Internet será tooan forçada ou redirecionado de volta no site local por meio de saudação que encapsulamentos VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-119">Any outbound connections from these two subnets toohello Internet will be forced or redirected back tooan on-premises site via one of hello S2S VPN tunnels.</span></span>

<span data-ttu-id="0cfd5-120">Isso permite que você toorestrict e inspecione o acesso à Internet de suas máquinas virtuais ou serviços no Azure, de nuvem enquanto continua tooenable sua arquitetura de serviço de várias camadas necessária.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-120">This allows you toorestrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing tooenable your multi-tier service architecture required.</span></span> <span data-ttu-id="0cfd5-121">Se não houver nenhuma carga de trabalho para a Internet em suas redes virtuais, você também pode aplicar forçado túnel toohello redes virtuais inteiras.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-121">If there are no Internet-facing workloads in your virtual networks, you also can apply forced tunneling toohello entire virtual networks.</span></span>

## <a name="requirements-and-considerations"></a><span data-ttu-id="0cfd5-122">Requisitos e considerações</span><span class="sxs-lookup"><span data-stu-id="0cfd5-122">Requirements and considerations</span></span>

<span data-ttu-id="0cfd5-123">O túnel forçado no Azure é configurado por meio de rotas de rede virtual definidas pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-123">Forced tunneling in Azure is configured via virtual network user-defined routes.</span></span> <span data-ttu-id="0cfd5-124">Redirecionar o tráfego tooan local do site é expressa como um gateway de VPN do Azure toohello rota padrão.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-124">Redirecting traffic tooan on-premises site is expressed as a Default Route toohello Azure VPN gateway.</span></span> <span data-ttu-id="0cfd5-125">Para saber mais sobre rotas definidas pelo usuário e redes virtuais, confira [Encaminhamento IP e rotas definidas pelo usuário](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0cfd5-125">For more information about user-defined routing and virtual networks, see [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>

* <span data-ttu-id="0cfd5-126">Cada sub-rede de rede virtual tem uma tabela de roteamento interna do sistema.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-126">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="0cfd5-127">tabela de roteamento de sistema Olá tem Olá três grupos de rotas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0cfd5-127">hello system routing table has hello following three groups of routes:</span></span>
  
  * <span data-ttu-id="0cfd5-128">**Rotas de rede virtual locais:** diretamente toohello VMs de destino na Olá mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-128">**Local VNet routes:** Directly toohello destination VMs in hello same virtual network.</span></span>
  * <span data-ttu-id="0cfd5-129">**Rotas locais:** toohello gateway de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-129">**On-premises routes:** toohello Azure VPN gateway.</span></span>
  * <span data-ttu-id="0cfd5-130">**Rota padrão:** toohello diretamente da Internet.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-130">**Default route:** Directly toohello Internet.</span></span> <span data-ttu-id="0cfd5-131">Pacotes destinados toohello endereços IP privados não cobertos por rotas Olá dois anterior são removidos.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-131">Packets destined toohello private IP addresses not covered by hello previous two routes are dropped.</span></span>
* <span data-ttu-id="0cfd5-132">Este procedimento usa as rotas definidas pelo usuário (UDR) toocreate um tooadd de tabela de roteamento uma rota padrão e, em seguida, associar Olá tabela tooyour VNet sub-redes tooenable forçado nessas sub-redes de encapsulamento de roteamento.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-132">This procedure uses user-defined routes (UDR) toocreate a routing table tooadd a default route, and then associate hello routing table tooyour VNet subnet(s) tooenable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="0cfd5-133">O túnel forçado deve ser associado a uma Rede Virtual que tenha um Gateway de VPN de roteamento.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-133">Forced tunneling must be associated with a VNet that has a route-based VPN gateway.</span></span> <span data-ttu-id="0cfd5-134">É necessário tooset "site padrão" entre a rede virtual de toohello conectado Olá de sites locais entre locais.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-134">You need tooset a "default site" among hello cross-premises local sites connected toohello virtual network.</span></span> <span data-ttu-id="0cfd5-135">Além disso, Olá local do dispositivo VPN deve ser configurado usando 0.0.0.0/0 como seletores de tráfego.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-135">Also, hello on-premises VPN device must be configured using 0.0.0.0/0 as traffic selectors.</span></span> 
* <span data-ttu-id="0cfd5-136">Túnel forçado do ExpressRoute não está configurado por meio desse mecanismo, mas em vez disso, é habilitado por anuncia uma rota padrão por meio de saudação ExpressRoute BGP sessões de emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-136">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via hello ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="0cfd5-137">Para obter mais informações, consulte Olá [documentação de rota expressa](https://azure.microsoft.com/documentation/services/expressroute/).</span><span class="sxs-lookup"><span data-stu-id="0cfd5-137">For more information, see hello [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/).</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="0cfd5-138">Visão geral de configuração</span><span class="sxs-lookup"><span data-stu-id="0cfd5-138">Configuration overview</span></span>

<span data-ttu-id="0cfd5-139">Olá procedimento a seguir para criar um grupo de recursos e uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-139">hello following procedure helps you create a resource group and a VNet.</span></span> <span data-ttu-id="0cfd5-140">Em seguida, você criará um gateway de VPN e configurará um túnel forçado.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-140">You'll then create a VPN gateway and configure forced tunneling.</span></span> <span data-ttu-id="0cfd5-141">Neste procedimento, a rede virtual de saudação 'MultiTier-VNet' tem três sub-redes: 'Front-end', 'Midtier' e 'Back-end', com quatro conexões entre locais: 'DefaultSiteHQ' e três ramificações.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-141">In this procedure, hello virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend', with four cross-premises connections: 'DefaultSiteHQ', and three Branches.</span></span>

<span data-ttu-id="0cfd5-142">etapas do procedimento Olá definir Olá 'DefaultSiteHQ' como conexão de site saudação padrão para túnel forçado e configurar hello 'Midtier' e 'Back-end' sub-redes toouse túnel forçado.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-142">hello procedure steps set hello 'DefaultSiteHQ' as hello default site connection for forced tunneling, and configure hello 'Midtier' and 'Backend' subnets toouse forced tunneling.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0cfd5-143">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="0cfd5-143">Before you begin</span></span>

<span data-ttu-id="0cfd5-144">Instale a versão mais recente Olá de saudação cmdlets do PowerShell do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-144">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="0cfd5-145">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre como instalar os cmdlets do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-145">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <a name="toolog-in"></a><span data-ttu-id="0cfd5-146">toolog em</span><span class="sxs-lookup"><span data-stu-id="0cfd5-146">toolog in</span></span>

[!INCLUDE [toolog in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a><span data-ttu-id="0cfd5-147">Configurar o túnel forçado</span><span class="sxs-lookup"><span data-stu-id="0cfd5-147">Configure forced tunneling</span></span>

1. <span data-ttu-id="0cfd5-148">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-148">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. <span data-ttu-id="0cfd5-149">Crie uma rede virtual e especifique as sub-redes.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-149">Create a virtual network and specify subnets.</span></span>

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. <span data-ttu-id="0cfd5-150">Crie hello gateways de rede local.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-150">Create hello local network gateways.</span></span>

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. <span data-ttu-id="0cfd5-151">Crie regra de rota e de tabela de rota hello.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-151">Create hello route table and route rule.</span></span>

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. <span data-ttu-id="0cfd5-152">Associe Olá rota tabela toohello Midtier e sub-redes de back-end.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-152">Associate hello route table toohello Midtier and Backend subnets.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="0cfd5-153">Crie hello Gateway com um site padrão.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-153">Create hello Gateway with a default site.</span></span> <span data-ttu-id="0cfd5-154">Esta etapa leva alguns toocomplete de tempo, às vezes, 45 minutos ou mais, porque você está criando e configurando o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-154">This step takes some time toocomplete, sometimes 45 minutes or more, because you are creating and configuring hello gateway.</span></span><br> <span data-ttu-id="0cfd5-155">Olá **- GatewayDefaultSite** é Olá parâmetro de cmdlet que permite Olá forçado toowork de configuração de roteamento, portanto cuidado tooconfigure essa configuração adequadamente.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-155">hello **-GatewayDefaultSite** is hello cmdlet parameter that allows hello forced routing configuration toowork, so take care tooconfigure this setting properly.</span></span> <span data-ttu-id="0cfd5-156">Esse parâmetro está disponível no PowerShell 1.0 ou versão posterior.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-156">This parameter is available in PowerShell 1.0 or later.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. <span data-ttu-id="0cfd5-157">Estabelecer conexões de VPN Olá Site a Site.</span><span class="sxs-lookup"><span data-stu-id="0cfd5-157">Establish hello Site-to-Site VPN connections.</span></span>

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