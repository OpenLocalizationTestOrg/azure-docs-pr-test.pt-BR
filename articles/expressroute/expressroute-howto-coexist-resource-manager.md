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
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a>Configurar conexões coexistentes Site a Site e do ExpressRoute
> [!div class="op_single_selector"]
> * [PowerShell – Resource Manager](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell - clássico](expressroute-howto-coexist-classic.md)
> 
> 

Configurar conexões coexistentes VPN Site a Site e a ExpressRoute tem várias vantagens. Você pode configurar uma VPN Site a Site como um caminho de failover seguro para ExressRoute ou usar VPNs Site a Site tooconnect toosites que não estão conectados por meio de rota expressa. Abordaremos Olá etapas tooconfigure ambos os cenários neste artigo. Este artigo se aplica o modelo de implantação do Gerenciador de recursos de toohello e usa o PowerShell. Essa configuração não está disponível no portal do Azure de saudação.

> [!IMPORTANT]
> Circuitos de rota expressa devem ser configurados previamente antes de seguir as instruções de saudação abaixo. Certifique-se de que você seguiu Olá guias muito[criar um circuito ExpressRoute](expressroute-howto-circuit-arm.md) e [configurar o roteamento](expressroute-howto-routing-arm.md) antes de continuar.
> 
> 

## <a name="limits-and-limitations"></a>Limites e limitações
* **Não há suporte para o roteamento do tráfego.** Não é possível fazer o roteamento (por meio do Azure) entre sua rede local conectada via VPN Site a Site e sua rede local conectada via ExpressRoute.
* **Não há suporte para o gateway SKU básico.** Você deve usar um gateway de SKU não básica para ambos os Olá [gateway de rota expressa](expressroute-about-virtual-network-gateways.md) e hello [gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **Há suporte para apenas um gateway de VPN baseado em rotas.** Você deve usar uma rota baseada no [Gateway de VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **O roteamento estático deve ser configurado para o gateway de VPN.** Se sua rede local está conectada tooboth ExpressRoute e uma Site a Site VPN, você deve ter uma rota estática configurada em sua rede local tooroute Olá Site a Site VPN conexão toohello Internet pública.
* **Gateway de rota expressa deve ser configurado primeiro e vinculados tooa circuito.** Você deve primeiro criar o gateway de rota expressa hello e vinculá-la circuitos tooa antes de adicionar o gateway VPN Olá Site a Site.

## <a name="configuration-designs"></a>Designs de configuração
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>Configurar uma VPN site a site como um caminho de failover para o ExpressRoute
Você pode configurar uma conexão VPN site a site como um backup para o ExpressRoute. Isso se aplica apenas toovirtual redes vinculado toohello caminho de emparelhamento particular do Azure. Não há uma solução de failover com base em VPN para serviços acessíveis por meio de emparelhamentos público do Azure e da Microsoft. Olá circuito de rota expressa é sempre link principal hello. Fluxos de dados por meio do caminho VPN Site a Site Olá somente se Olá circuito ExpressRoute falhar.

> [!NOTE]
> Enquanto circuito de rota expressa é preferível por VPN Site a Site quando ambas as rotas são Olá mesmo, o Azure usará hello mais longa correspondência toochoose Olá rota de prefixo para o destino do pacote de saudação.
> 
> 

![Coexistência](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a>Configurar um toosites tooconnect VPN Site a Site não está conectado por meio de rota expressa
Você pode configurar sua rede onde alguns sites se conectam diretamente tooAzure por VPN Site a Site, e alguns sites se conectam por meio de rota expressa. 

![Coexistência](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> Não é possível configurar uma rede virtual como um roteador de trânsito.
> 
> 

## <a name="selecting-hello-steps-toouse"></a>Selecionando Olá etapas toouse
Há dois conjuntos diferentes de toochoose procedimentos de. procedimento de configuração de saudação selecionado depende se você tiver uma rede virtual existente que você deseja tooconnect para, ou você deseja toocreate uma nova rede virtual.

* Não tem uma rede virtual e precisa toocreate um.
  
    Se você ainda não tiver uma rede virtual, esse procedimento explica como criar uma nova rede virtual usando o modelo de implantação do Gerenciador de Recursos e criando novas conexões de VPN Site a Site e de ExpressRoute. tooconfigure uma rede virtual, execute as etapas de saudação em [toocreate uma nova rede virtual e conexões coexistentes](#new).
* Eu já tenho uma VNet do modelo de implantação do Gerenciador de Recursos.
  
    Talvez você já tenha uma rede virtual implementada com uma conexão de VPN Site a Site ou uma conexão de ExpressRoute existente. Olá [conexões coexistentes do tooconfigure para uma rede virtual já existente](#add) seção orienta você por excluir gateway hello e, em seguida, criar novas conexões de VPN Site a Site e rota expressa. Ao criar novas conexões de hello, etapas de saudação devem ser concluídas em uma ordem específica. Não use instruções Olá toocreate outros artigos seus gateways e conexões.
  
    Neste procedimento, a criação de conexões que podem coexistir requer que você toodelete seu gateway e configure novos gateways. Você terá tempo de inatividade para as conexões entre locais enquanto você excluir e recria o gateway e conexões, mas você não precisará toomigrate qualquer uma das sua VMs ou serviços tooa nova rede virtual. Suas máquinas virtuais e serviços ainda serão toocommunicate capaz de saída por meio do balanceador de carga Olá enquanto você configurar seu gateway se eles estiverem toodo configurado assim.

## <a name="new"></a>conexões coexistentes e toocreate uma nova rede virtual
Este procedimento orientará você na criação de uma VNet, bem como na criação das conexões Site a Site e de ExpressRoute que coexistirão.

1. Instale a versão mais recente Olá de saudação cmdlets do PowerShell do Azure. Para obter informações sobre como instalar os cmdlets hello, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview). Olá cmdlets que você pode usar para essa configuração pode ser um pouco diferente do que você talvez esteja familiarizado com. Se toouse Olá cmdlets ser especificado nestas instruções.
2. Faça logon na conta de tooyour e configurar o ambiente de saudação.

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. Crie uma rede virtual incluindo uma Sub-rede de Gateway. Para obter mais informações sobre a configuração de rede virtual hello, consulte [configuração de rede Virtual do Azure](../virtual-network/virtual-networks-create-vnet-arm-ps.md).
   
   > [!IMPORTANT]
   > Olá sub-rede de Gateway deve ser /27 ou um prefixo mais curto (como /26 ou /25).
   > 
   > 
   
    Crie uma nova VNet.

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    Adicione sub-redes.

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    Salve a configuração da rede virtual hello.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <a name="gw">
            </a>Crie um gateway de ExpressRoute. Para obter mais informações sobre a configuração de gateway de rota expressa hello, consulte [configuração de gateway de rota expressa](expressroute-howto-add-gateway-resource-manager.md). Olá GatewaySKU devem ser *padrão*, *HighPerformance*, ou *UltraPerformance*.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. Vincule um circuito de rota expressa toohello do gateway de rota expressa hello. Após essa etapa foi concluída, a conexão Olá entre sua rede local e o Azure, por meio do ExpressRoute, é estabelecida. Para obter mais informações sobre a operação de vinculação hello, consulte [tooExpressRoute VNets Link](expressroute-howto-linkvnet-arm.md).

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <a name="vpngw"></a>Em seguida, crie seu gateway de VPN Site a Site. Para obter mais informações sobre a configuração de gateway VPN hello, consulte [configurar uma rede virtual com uma conexão Site a Site](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md). Olá GatewaySKU devem ser *padrão*, *HighPerformance*, ou *UltraPerformance*. Olá VpnType deve *RouteBased*.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    O Gateway de VPN do Azure oferece suporte ao protocolo de roteamento BGP. Você pode especificar ASN (número) para essa rede Virtual adicionando switch de Asn - Olá Olá comando a seguir. Não especificar esse parâmetro será tooAS padrão de número das 65515.

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    Você pode encontrar hello BGP de emparelhamento IP e hello como o número que o Azure usa para o gateway VPN Olá em $azureVpn.BgpSettings.BgpPeeringAddress e $azureVpn.BgpSettings.Asn. Para obter mais informações, consulte [Configurar BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) para o gateway de VPN do Azure.
7. Crie uma entidade de gateway de VPN de site local. Esse comando não configura seu gateway de VPN local. Em vez disso, permite configurações de gateway local tooprovide hello, como o IP público hello e hello local espaço de endereço, para que hello gateway VPN do Azure pode se conectar tooit.
   
    Se seu dispositivo VPN local só dá suporte a roteamento estático, você pode configurar rotas estáticas Olá Olá maneira a seguir:

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    Se seu dispositivo VPN local com suporte Olá BGP e você deseja que o roteamento dinâmico tooenable, será necessário tooknow Olá BGP emparelhamento IP e hello como sua VPN local de número que o dispositivo usa.

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for hello BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. Configure seu dispositivo tooconnect toohello novo VPN do Azure gateway de VPN local. Para obter mais informações sobre a configuração de dispositivo VPN, consulte [Configuração do Dispositivo VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md).
9. Gateway VPN Site a Site link Olá no gateway local toohello do Azure.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <a name="add"></a>conexões de coexistentes tooconfigure para uma rede virtual já existente
Se você tiver uma rede virtual existente, verifique o tamanho de sub-rede de gateway hello. Se a sub-rede do gateway Olá for /28 ou /29, primeiro exclua o gateway de rede virtual hello e aumentar o tamanho de sub-rede de gateway de saudação. Olá etapas nesta seção mostram como toodo que.

Se a sub-rede do gateway de saudação é /27 ou maior e rede virtual Olá é conectado por meio de rota expressa, você pode ignorar as etapas de saudação abaixo e prosseguir muito["Etapa 6 – criar um gateway VPN Site a Site"](#vpngw) na seção anterior hello. 

> [!NOTE]
> Quando você exclui um gateway existente Olá, seus locais perderá a rede virtual do hello conexão tooyour enquanto você trabalha nessa configuração. 
> 
> 

1. Você precisará tooinstall Olá última versão do hello cmdlets do PowerShell do Azure. Para obter mais informações sobre como instalar os cmdlets, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview). Olá cmdlets que você pode usar para essa configuração pode ser um pouco diferente do que você talvez esteja familiarizado com. Se toouse Olá cmdlets ser especificado nestas instruções. 
2. Exclua gateway existente Olá rota expressa ou VPN Site a Site.

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. Exclua a Sub-rede de Gateway.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. Adicione uma Sub-rede de Gateway que seja /27 ou maior.
   
   > [!NOTE]
   > Se você não tiver endereços IP suficientes no tamanho de sub-rede de gateway sua rede virtual tooincrease hello, será necessário tooadd mais espaço de endereço IP.
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    Salve a configuração da rede virtual hello.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. Neste ponto, você terá uma VNet sem nenhum gateway. novos gateways do toocreate e concluir as conexões, você pode continuar com a [etapa 4 - criar um gateway de rota expressa](#gw), encontrado em Olá precede o conjunto de etapas.

## <a name="tooadd-point-to-site-configuration-toohello-vpn-gateway"></a>gateway VPN de toohello tooadd configuração ponto a site
Você pode seguir as etapas de saudação abaixo gateway de VPN ponto a Site tooadd configuração tooyour em uma configuração de coexistência.

1. Adicione o pool de endereços do Cliente VPN.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. Carregar tooAzure de certificado de raiz Olá VPN para o gateway VPN. Neste exemplo, presume-se que esse certificado de raiz de saudação é armazenado no computador local hello, onde Olá cmdlets do PowerShell a seguir é executado.

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

Para saber mais sobre a VPN de Ponto a Site, confira [Configurar uma conexão de Ponto a Site](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre a rota expressa, consulte Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).
