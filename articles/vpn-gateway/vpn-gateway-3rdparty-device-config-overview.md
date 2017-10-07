---
title: "aaaAbout 3ª parte dispositivo configuração tooconnect tooAzure VPN gateways VPN | Microsoft Docs"
description: "Este artigo fornece uma visão geral das configurações de dispositivo VPN parte 3º para conectar-se tooAzure gateways de VPN."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: 3bb4fc94bc625386c2d0a02e1dcbdeb38ee0665e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-3rd-party-vpn-device-configurations"></a>Visão geral das configurações de dispositivo VPN de terceiros
Este artigo fornece uma visão geral das configurações de dispositivo VPN local para conectar-se tooAzure gateways de VPN. exemplo Hello rede virtual do Azure e a VPN gateway configuração será usada tooconnect toodifferent dispositivos VPN local com hello os mesmos parâmetros.

## <a name="device-requirements"></a>Requisitos do dispositivo
Gateways VPN do Azure usam conjuntos padrão de protocolo IPsec/IKE para túneis VPN S2S. Consulte também[sobre dispositivos VPN](vpn-gateway-about-vpn-devices.md) para Olá detalhadas parâmetros do protocolo IPsec/IKE e algoritmos de criptografia padrão para gateways de VPN do Azure. Você pode opcionalmente especificar combinação exata de saudação de algoritmos de criptografia e restrições de chave para uma conexão específica, conforme descrito em [sobre os requisitos de criptografia](vpn-gateway-about-compliance-crypto.md).

## <a name ="singletunnel"></a>Túnel VPN único
topologia primeiro Olá consiste em um único túnel VPN S2S entre um gateway de VPN do Azure e o dispositivo VPN local. Opcionalmente você pode configurar o BGP em túnel VPN hello.

![túnel único](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

Consulte também[configurar conexão site a site](vpn-gateway-howto-site-to-site-resource-manager-portal.md) para obter orientações detalhadas, passo a passo. Hello seções a seguir listam os parâmetros de saudação e fornecem um toohelp de script do PowerShell de exemplo que você a começar.

### <a name="network-and-vpn-gateway-information"></a>Informações de gateway de VPN e de rede
Esta seção lista parâmetros Olá para obter exemplos de saudação acima.

| **Parâmetro**                | **Valor**                    |
| ---                          | ---                          |
| Prefixos de endereços da VNET        | 10.11.0.0/16<br>10.12.0.0/16 |
| IP do gateway de VPN do Azure         | IP do Gateway de VPN do Azure         |
| Prefixos de endereço local | 10.51.0.0/16<br>10.52.0.0/16 |
| IP do dispositivo VPN local    | IP do dispositivo VPN local    |
| *ASN de BGP da VNet                | 65010                        |
| *IP de par no nível de protocolo BGP do Azure           | 10.12.255.30                 |
| * ASN de BGP local         | 65050                        |
| * IP de par no nível de protocolo BGP local     | 10.52.255.254                |

* (*) Parâmetros opcionais apenas para o BGP

### <a name="sample-powershell-script"></a>Exemplo de script do PowerShell
[Criar uma conexão VPN S2S usando o PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) possui Olá instruções detalhadas. Esta seção fornece uma tooget de script de exemplo que é iniciado.

```powershell
# Declare your variables

$Sub1          = "Replace_With_Your_Subcription_Name"
$RG1           = "TestRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$VNet1ASN      = 65010
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GWIPName1     = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection15  = "VNet1toSite5"
$LNGName5      = "Site5"
$LNGPrefix50   = "10.52.255.254/32"
$LNGPrefix51   = "10.51.0.0/16"
$LNGPrefix52   = "10.52.0.0/16"
$LNGIP5        = "Your_VPN_Device_IP"
$LNGASN5       = 65050
$BGPPeerIP5    = "10.52.255.254"

# Connect tooyour subscription and create a new resource group

Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1

# Create virtual network

$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

# Create VPN gateway

$gwpip1    = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1     = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN

# Create local network gateway

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix51,$LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5

# Create hello S2S VPN connection

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False
```

### <a name ="policybased"></a>[Opcional] Usar a política IPsec/IKE personalizada com "UsePolicyBasedTrafficSelectors"
Se os dispositivos VPN não dão suporte a seletores de tráfego "para qualquer" (com base em/VTI-baseadas em rota configuração), será necessário toocreate uma política personalizada do IPsec/IKE e configurar a opção "UsePolicyBasedTrafficSelectors" conforme descrito em [neste artigo ](vpn-gateway-connect-multiple-policybased-rm-ps.md).

> [!IMPORTANT]
> Você precisa de toocreate uma política de IPsec/IKE na ordem tooenable opção "UsePolicyBasedTrafficSelectors" na conexão hello.

script de exemplo Hello abaixo cria uma política de IPsec/IKE com hello algoritmos e os parâmetros a seguir:
* IKEv2: AES256, SHA384, DHGroup24
* IPsec: AES256, SHA1, PFS24, SA Tempo de vida 7.200 segundos e 20.480.000 KB (20 GB)

Ele aplica a política de saudação e habilita "UesPolicyBasedTrafficSelectors" em conexão hello.

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <a name ="bgp"></a>[Opcional] Usar BGP na conexão VPN S2S
Opcionalmente, você pode usar o BGP na conexão de saudação. Consulte [BGP para gateway de VPN](vpn-gateway-bgp-resource-manager-ps.md). Há duas diferenças:

prefixos de endereço local Olá podem ser um endereço de host único, o endereço IP do par BGP do hello local:

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

Você deve definir "-EnableBGP" muito$ True ao criar conexão hello:

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a>Próximas etapas
Consulte [Gateways de VPN configuração ativa-ativa para conexões de rede virtual a rede e entre locais](vpn-gateway-activeactive-rm-powershell.md) para conexões de rede virtual a rede e etapas tooconfigure ativo-ativo entre locais.

