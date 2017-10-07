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
# <a name="overview-of-3rd-party-vpn-device-configurations"></a><span data-ttu-id="6154e-103">Visão geral das configurações de dispositivo VPN de terceiros</span><span class="sxs-lookup"><span data-stu-id="6154e-103">Overview of 3rd party VPN device configurations</span></span>
<span data-ttu-id="6154e-104">Este artigo fornece uma visão geral das configurações de dispositivo VPN local para conectar-se tooAzure gateways de VPN.</span><span class="sxs-lookup"><span data-stu-id="6154e-104">This article provides an overview of on-premises VPN device configurations for connecting tooAzure VPN gateways.</span></span> <span data-ttu-id="6154e-105">exemplo Hello rede virtual do Azure e a VPN gateway configuração será usada tooconnect toodifferent dispositivos VPN local com hello os mesmos parâmetros.</span><span class="sxs-lookup"><span data-stu-id="6154e-105">hello sample Azure virtual network and VPN gateway setup will be used tooconnect toodifferent on-premises VPN devices with hello same parameters.</span></span>

## <a name="device-requirements"></a><span data-ttu-id="6154e-106">Requisitos do dispositivo</span><span class="sxs-lookup"><span data-stu-id="6154e-106">Device requirements</span></span>
<span data-ttu-id="6154e-107">Gateways VPN do Azure usam conjuntos padrão de protocolo IPsec/IKE para túneis VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="6154e-107">Azure VPN gateways use standard IPsec/IKE protocol suites for S2S VPN tunnels.</span></span> <span data-ttu-id="6154e-108">Consulte também[sobre dispositivos VPN](vpn-gateway-about-vpn-devices.md) para Olá detalhadas parâmetros do protocolo IPsec/IKE e algoritmos de criptografia padrão para gateways de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="6154e-108">Refer too[About VPN devices](vpn-gateway-about-vpn-devices.md) for hello detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="6154e-109">Você pode opcionalmente especificar combinação exata de saudação de algoritmos de criptografia e restrições de chave para uma conexão específica, conforme descrito em [sobre os requisitos de criptografia](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="6154e-109">You can optionally specify hello exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span>

## <span data-ttu-id="6154e-110"><a name ="singletunnel"></a>Túnel VPN único</span><span class="sxs-lookup"><span data-stu-id="6154e-110"><a name ="singletunnel"></a>Single VPN tunnel</span></span>
<span data-ttu-id="6154e-111">topologia primeiro Olá consiste em um único túnel VPN S2S entre um gateway de VPN do Azure e o dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="6154e-111">hello first topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="6154e-112">Opcionalmente você pode configurar o BGP em túnel VPN hello.</span><span class="sxs-lookup"><span data-stu-id="6154e-112">You can optionally configure BGP across hello VPN tunnel.</span></span>

![túnel único](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

<span data-ttu-id="6154e-114">Consulte também[configurar conexão site a site](vpn-gateway-howto-site-to-site-resource-manager-portal.md) para obter orientações detalhadas, passo a passo.</span><span class="sxs-lookup"><span data-stu-id="6154e-114">Refer too[Configure site-to-site connection](vpn-gateway-howto-site-to-site-resource-manager-portal.md) for detailed, step-by-step guidance.</span></span> <span data-ttu-id="6154e-115">Hello seções a seguir listam os parâmetros de saudação e fornecem um toohelp de script do PowerShell de exemplo que você a começar.</span><span class="sxs-lookup"><span data-stu-id="6154e-115">hello following sections list hello parameters and provide a sample PowerShell script toohelp you get started.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="6154e-116">Informações de gateway de VPN e de rede</span><span class="sxs-lookup"><span data-stu-id="6154e-116">Network and VPN gateway information</span></span>
<span data-ttu-id="6154e-117">Esta seção lista parâmetros Olá para obter exemplos de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="6154e-117">This section list hello parameters for hello examples above.</span></span>

| <span data-ttu-id="6154e-118">**Parâmetro**</span><span class="sxs-lookup"><span data-stu-id="6154e-118">**Parameter**</span></span>                | <span data-ttu-id="6154e-119">**Valor**</span><span class="sxs-lookup"><span data-stu-id="6154e-119">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="6154e-120">Prefixos de endereços da VNET</span><span class="sxs-lookup"><span data-stu-id="6154e-120">VNet address prefixes</span></span>        | <span data-ttu-id="6154e-121">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="6154e-121">10.11.0.0/16</span></span><br><span data-ttu-id="6154e-122">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="6154e-122">10.12.0.0/16</span></span> |
| <span data-ttu-id="6154e-123">IP do gateway de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="6154e-123">Azure VPN gateway IP</span></span>         | <span data-ttu-id="6154e-124">IP do Gateway de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="6154e-124">Azure VPN Gateway IP</span></span>         |
| <span data-ttu-id="6154e-125">Prefixos de endereço local</span><span class="sxs-lookup"><span data-stu-id="6154e-125">On-premises address prefixes</span></span> | <span data-ttu-id="6154e-126">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="6154e-126">10.51.0.0/16</span></span><br><span data-ttu-id="6154e-127">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="6154e-127">10.52.0.0/16</span></span> |
| <span data-ttu-id="6154e-128">IP do dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="6154e-128">On-premises VPN device IP</span></span>    | <span data-ttu-id="6154e-129">IP do dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="6154e-129">On-premises VPN device IP</span></span>    |
| <span data-ttu-id="6154e-130">*ASN de BGP da VNet</span><span class="sxs-lookup"><span data-stu-id="6154e-130">*VNet BGP ASN</span></span>                | <span data-ttu-id="6154e-131">65010</span><span class="sxs-lookup"><span data-stu-id="6154e-131">65010</span></span>                        |
| <span data-ttu-id="6154e-132">*IP de par no nível de protocolo BGP do Azure</span><span class="sxs-lookup"><span data-stu-id="6154e-132">*Azure BGP peer IP</span></span>           | <span data-ttu-id="6154e-133">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="6154e-133">10.12.255.30</span></span>                 |
| <span data-ttu-id="6154e-134">* ASN de BGP local</span><span class="sxs-lookup"><span data-stu-id="6154e-134">*On-premises BGP ASN</span></span>         | <span data-ttu-id="6154e-135">65050</span><span class="sxs-lookup"><span data-stu-id="6154e-135">65050</span></span>                        |
| <span data-ttu-id="6154e-136">* IP de par no nível de protocolo BGP local</span><span class="sxs-lookup"><span data-stu-id="6154e-136">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="6154e-137">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="6154e-137">10.52.255.254</span></span>                |

* <span data-ttu-id="6154e-138">(*) Parâmetros opcionais apenas para o BGP</span><span class="sxs-lookup"><span data-stu-id="6154e-138">(*) Optional parameters for BGP only</span></span>

### <a name="sample-powershell-script"></a><span data-ttu-id="6154e-139">Exemplo de script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="6154e-139">Sample PowerShell script</span></span>
<span data-ttu-id="6154e-140">[Criar uma conexão VPN S2S usando o PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) possui Olá instruções detalhadas.</span><span class="sxs-lookup"><span data-stu-id="6154e-140">[Create a S2S VPN connection using PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) has hello detailed instructions.</span></span> <span data-ttu-id="6154e-141">Esta seção fornece uma tooget de script de exemplo que é iniciado.</span><span class="sxs-lookup"><span data-stu-id="6154e-141">This section provides a sample script tooget you started.</span></span>

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

### <span data-ttu-id="6154e-142"><a name ="policybased"></a>[Opcional] Usar a política IPsec/IKE personalizada com "UsePolicyBasedTrafficSelectors"</span><span class="sxs-lookup"><span data-stu-id="6154e-142"><a name ="policybased"></a> [Optional] Use custom IPsec/IKE policy with "UsePolicyBasedTrafficSelectors"</span></span>
<span data-ttu-id="6154e-143">Se os dispositivos VPN não dão suporte a seletores de tráfego "para qualquer" (com base em/VTI-baseadas em rota configuração), será necessário toocreate uma política personalizada do IPsec/IKE e configurar a opção "UsePolicyBasedTrafficSelectors" conforme descrito em [neste artigo ](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="6154e-143">If your VPN devices do not support "any-to-any" traffic selectors (route-based/VTI-based configuration), you will need toocreate a custom IPsec/IKE policy and configure "UsePolicyBasedTrafficSelectors" option as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6154e-144">Você precisa de toocreate uma política de IPsec/IKE na ordem tooenable opção "UsePolicyBasedTrafficSelectors" na conexão hello.</span><span class="sxs-lookup"><span data-stu-id="6154e-144">You need toocreate an IPsec/IKE policy in order tooenable "UsePolicyBasedTrafficSelectors" option on hello connection.</span></span>

<span data-ttu-id="6154e-145">script de exemplo Hello abaixo cria uma política de IPsec/IKE com hello algoritmos e os parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="6154e-145">hello sample script below creates an IPsec/IKE policy with hello following algorithms and parameters:</span></span>
* <span data-ttu-id="6154e-146">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="6154e-146">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="6154e-147">IPsec: AES256, SHA1, PFS24, SA Tempo de vida 7.200 segundos e 20.480.000 KB (20 GB)</span><span class="sxs-lookup"><span data-stu-id="6154e-147">IPsec: AES256, SHA1, PFS24, SA Lifetime 7200 seconds & 20480000KB (20GB)</span></span>

<span data-ttu-id="6154e-148">Ele aplica a política de saudação e habilita "UesPolicyBasedTrafficSelectors" em conexão hello.</span><span class="sxs-lookup"><span data-stu-id="6154e-148">It then applies hello policy and enables "UesPolicyBasedTrafficSelectors" on hello connection.</span></span>

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <span data-ttu-id="6154e-149"><a name ="bgp"></a>[Opcional] Usar BGP na conexão VPN S2S</span><span class="sxs-lookup"><span data-stu-id="6154e-149"><a name ="bgp"></a>[Optional] Use BGP on S2S VPN connection</span></span>
<span data-ttu-id="6154e-150">Opcionalmente, você pode usar o BGP na conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="6154e-150">You can optionally use BGP on hello connection.</span></span> <span data-ttu-id="6154e-151">Consulte [BGP para gateway de VPN](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="6154e-151">See [BGP for VPN gateway](vpn-gateway-bgp-resource-manager-ps.md).</span></span> <span data-ttu-id="6154e-152">Há duas diferenças:</span><span class="sxs-lookup"><span data-stu-id="6154e-152">There are two differences:</span></span>

<span data-ttu-id="6154e-153">prefixos de endereço local Olá podem ser um endereço de host único, o endereço IP do par BGP do hello local:</span><span class="sxs-lookup"><span data-stu-id="6154e-153">hello on-premises address prefixes can be a single host address, hello on-premises BGP peer IP address:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

<span data-ttu-id="6154e-154">Você deve definir "-EnableBGP" muito$ True ao criar conexão hello:</span><span class="sxs-lookup"><span data-stu-id="6154e-154">You must set "-EnableBGP" too$True when creating hello connection:</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a><span data-ttu-id="6154e-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6154e-155">Next steps</span></span>
<span data-ttu-id="6154e-156">Consulte [Gateways de VPN configuração ativa-ativa para conexões de rede virtual a rede e entre locais](vpn-gateway-activeactive-rm-powershell.md) para conexões de rede virtual a rede e etapas tooconfigure ativo-ativo entre locais.</span><span class="sxs-lookup"><span data-stu-id="6154e-156">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps tooconfigure active-active cross-premises and VNet-to-VNet connections.</span></span>

