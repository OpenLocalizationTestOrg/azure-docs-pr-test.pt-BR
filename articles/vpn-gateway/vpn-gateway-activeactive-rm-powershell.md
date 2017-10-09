---
title: "Configurar conexões VPN S2S ativa-ativa para Gateways de VPN: Azure Resource Manager: PowerShell | Microsoft Docs"
description: "Este artigo mostra como configurar conexões ativo-ativo com gateways de VPN do Azure usando o Azure Resource Manager e o PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: yushwang
ms.openlocfilehash: 964eedc7698e42bf0e082f0105845f2a339daf57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a>Configurar conexões VPN S2S ativa-ativa com Gateways de VPN

Este artigo orienta Olá etapas toocreate ativo-ativo entre locais e conexões de rede virtual a rede usando o modelo de implantação do Gerenciador de recursos de saudação e PowerShell.

## <a name="about-highly-available-cross-premises-connections"></a>Sobre conexões altamente disponíveis entre instalações
tooachieve alta disponibilidade para entre locais e a conectividade de rede virtual a rede, você deve implantar vários gateways VPN e estabelecer várias conexões paralelos entre suas redes e o Azure. Consulte [Conectividade Altamente Disponível entre os Locais e VNet para VNet](vpn-gateway-highlyavailable.md) para obter uma visão geral das opções de conectividade e topologia.

Este artigo fornece instruções de saudação tooset a um ativo-ativo entre locais conexão VPN e conexão ativa entre duas redes virtuais:

* [Parte 1 – Criar e configurar seu gateway de VPN do Azure no modo ativo-ativo](#aagateway)
* [Parte 2 – Estabelecer conexões entre os locais ativo-ativo](#aacrossprem)
* [Parte 3 – Estabelecer conexões VNet para VNet ativo-ativo](#aav2v)
* [Parte 4 – Atualizar o gateway existente entre ativo-ativo e ativo-em espera](#aaupdate)

Você pode combinar essas toobuild juntos uma topologia de rede mais complexa, altamente disponível que atenda às suas necessidades.

> [!IMPORTANT]
> Observe que o modo ativo-ativo Olá usa Olá somente SKUs a seguir: 
  * VpnGw1, VpnGw2, VpnGw3
  * HighPerformance (para SKUs herdados antigos)
> 
> 

## <a name ="aagateway"></a>Parte 1 – Criar e configurar os gateways de VPN ativo-ativo
Olá etapas a seguir configurará o gateway de VPN do Azure nos modos ativo-ativo. principais diferenças entre os gateways de ativo-ativo e ativa / em espera Olá Olá:

* Você precisa toocreate duas configurações de IP de Gateway com dois endereços IP públicos
* Você precisa definir o sinalizador de EnableActiveActiveFeature de saudação
* SKU do gateway Olá deve ser VpnGw1, VpnGw2, VpnGw3 ou alto desempenho (SKU herdado).

Olá outras propriedades são Olá mesmo como gateways de não-ativo-ativo hello. 

### <a name="before-you-begin"></a>Antes de começar
* Verifique se você tem uma assinatura do Azure. Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Você precisará tooinstall Olá Gerenciador de recursos de cmdlets do PowerShell Azure. Consulte [visão geral do Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre como instalar os cmdlets do PowerShell hello.

### <a name="step-1---create-and-configure-vnet1"></a>Etapa 1 - Criar e configurar VNet1
#### <a name="1-declare-your-variables"></a>1. Declare as variáveis
Para este exercício, começaremos declarando nossa variáveis. exemplo Hello abaixo declara variáveis hello usando valores de saudação para este exercício. Ser valores de saudação tooreplace-se com seu próprio durante a configuração de produção. Você pode usar essas variáveis, se você estiver executando a saudação etapas toobecome familiarizado com esse tipo de configuração. Modificar variáveis de Olá e, em seguida, copie e cole o console do PowerShell.

```powershell
$Sub1 = "Ross"
$RG1 = "TestAARG1"
$Location1 = "West US"
$VNetName1 = "TestVNet1"
$FESubName1 = "FrontEnd"
$BESubName1 = "Backend"
$GWSubName1 = "GatewaySubnet"
$VNetPrefix11 = "10.11.0.0/16"
$VNetPrefix12 = "10.12.0.0/16"
$FESubPrefix1 = "10.11.0.0/24"
$BESubPrefix1 = "10.12.0.0/24"
$GWSubPrefix1 = "10.12.255.0/27"
$VNet1ASN = 65010
$DNS1 = "8.8.8.8"
$GWName1 = "VNet1GW"
$GW1IPName1 = "VNet1GWIP1"
$GW1IPName2 = "VNet1GWIP2"
$GW1IPconf1 = "gw1ipconf1"
$GW1IPconf2 = "gw1ipconf2"
$Connection12 = "VNet1toVNet2"
$Connection151 = "VNet1toSite5_1"
$Connection152 = "VNet1toSite5_2"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Conecte-se a assinatura de tooyour e criar um novo grupo de recursos
Verifique se que você alternar Olá toouse de modo tooPowerShell cmdlets do Gerenciador de recursos. Para obter mais informações, consulte [Usando o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).

Abra o console do PowerShell e conecte-se a conta de tooyour. Use Olá toohelp de exemplo que você se conectar a seguir:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3. Criar TestVNet1
exemplo Hello abaixo cria uma rede virtual denominada TestVNet1 e três sub-redes, um GatewaySubnet chamado, um front-end chamado e back-end chamado um. Ao substituir valores, é importante você sempre nomear sua sub-rede de gateway especificamente como GatewaySubnet. Se você usar outro nome, a criação do gateway falhará.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a>Etapa 2: criar o gateway VPN Olá para TestVNet1 com modo ativo-ativo
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a>1. Criar os endereços IP públicos hello e as configurações de IP do gateway
Solicitação dois pública endereços toobe toohello alocado gateway IP que você criará para sua rede virtual. Você também definirá sub-rede hello e as configurações de IP necessárias.

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a>2. Criar gateway VPN Olá com configuração ativo-ativo
Crie gateway de rede virtual Olá para TestVNet1. Observe que há duas entradas GatewayIpConfig e Olá EnableActiveActiveFeature sinalizador é definido. Criar um gateway pode demorar um pouco (45 minutos ou mais toocomplete).

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a>3. Obter endereços IP públicos de gateway hello e um endereço de IP do par de BGP Olá
Depois de criar o gateway Olá, você precisará de endereço de IP do par de BGP tooobtain Olá em Olá Gateway de VPN do Azure. Esse endereço é necessário tooconfigure Olá Gateway de VPN do Azure como um par de BGP para seus dispositivos VPN local.

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

Use Olá cmdlets tooshow Olá dois endereços IP públicos alocados para o gateway VPN e seus endereços IP de par de BGP correspondentes para cada instância de gateway a seguir:

```powershell

    PS D:\> $gw1pip1.IpAddress
    40.112.190.5

    PS D:\> $gw1pip2.IpAddress
    138.91.156.129

    PS D:\> $vnet1gw.BgpSettingsText
    {
      "Asn": 65010,
      "BgpPeeringAddress": "10.12.255.4,10.12.255.5",
      "PeerWeight": 0
    }
```

ordem de saudação de endereços IP públicos de saudação para instâncias de gateway hello e hello correspondente endereços de emparelhamento BGP são Olá mesmo. Neste exemplo, gateway Olá VM com o IP público de 40.112.190.5 usará 10.12.255.4 como seu endereço de emparelhamento BGP e gateway Olá com 138.91.156.129 usará 10.12.255.5. Essas informações são necessárias quando você configura seu local dispositivos VPN conectando toohello gateway de ativo-ativo. gateway de saudação é mostrado no diagrama de saudação abaixo com todos os endereços:

![gateway ativo-ativo](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

Depois que o gateway de saudação é criado, você pode usar este gateway tooestablish ativo-ativo entre os locais ou a conexão de rede virtual a rede. Olá seções a seguir orientará Olá etapas toocomplete Olá exercício.

## <a name ="aacrossprem"></a>Parte 2 – Estabelecer uma conexão entre os locais ativo-ativo
tooestablish uma conexão entre locais, você precisa toocreate toorepresent um Gateway de rede Local seu dispositivo VPN no local e um gateway de VPN do Azure Conexão tooconnect Olá com o gateway de rede local hello. Neste exemplo, o gateway de VPN do Azure hello está no modo de ativo-ativo. Como resultado, mesmo que haja apenas um local o dispositivo VPN (gateway de rede local) e recursos de uma conexão, ambas as instâncias de gateway VPN do Azure estabelecerá túneis VPN S2S com o dispositivo do local de saudação.

Antes de prosseguir, verifique se você concluiu a [Parte 1](#aagateway) deste exercício.

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a>Etapa 1: criar e configurar o gateway de rede local Olá
#### <a name="1-declare-your-variables"></a>1. Declare as variáveis
Este exercício continuará a configuração de saudação toobuild mostrada no diagrama de saudação. Ser tooreplace se valores Olá Olá aqueles que você deseja toouse para sua configuração.

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

Algumas coisas toonote sobre parâmetros de gateway de rede local hello:

* gateway de rede local Olá pode estar em Olá mesmo ou outro local e o recurso grupo Olá gateway VPN. Este exemplo mostra-los em grupos de recursos diferentes, mas em Olá mesmo local do Azure.
* Se houver apenas um dispositivo VPN local, como mostrado acima, conexão de ativo-ativo Olá pode trabalhar com ou sem o protocolo BGP. Este exemplo usa o BGP para conexão do hello entre locais.
* Se o BGP é habilitado, o prefixo de saudação precisar toodeclare para gateway de rede local Olá é endereço do host de saudação do seu endereço IP de par de BGP em seu dispositivo VPN. Nesse caso, é um prefixo /32 de "10.52.255.253/32".
* Como lembrete, você deve usar diferentes ASNs BGP entre suas redes locais e a VNet do Azure. Se eles são hello mesmo, você precisará toochange sua VNet ASN se seu dispositivo VPN local já usa Olá ASN toopeer com outros vizinhos de BGP.

#### <a name="2-create-hello-local-network-gateway-for-site5"></a>2. Criar gateway de rede local Olá para Site5
Antes de continuar, verifique se que você está conectado ainda tooSubscription 1. Crie grupo de recursos de saudação se ainda não foi criado.

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a>Etapa 2: conectar-se o gateway de rede virtual hello e gateway de rede local
#### <a name="1-get-hello-two-gateways"></a>1. Obter Olá dois gateways

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a>2. Criar conexão de tooSite5 TestVNet1 Olá
Nesta etapa, você irá criar conexão Olá de TestVNet1 tooSite5_1 com "EnableBGP" definido muito$ True.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a>3. Parâmetros VPN e BGP para seu dispositivo VPN local
exemplo Hello abaixo lista os parâmetros de saudação que será informado no hello seção de configuração de BGP em seu dispositivo VPN local para este exercício:

    - Site5 ASN            : 65050
    - Site5 BGP IP         : 10.52.255.253
    - O prefixo tooannounce: (por exemplo) 10.51.0.0/16 e 10.52.0.0/16
    - Azure VNet ASN       : 65010
    - IP do BGP VNet do Azure 1: 10.12.255.4 para túnel too40.112.190.5
    - IP do BGP VNet do Azure 2: 10.12.255.5 para túnel too138.91.156.129
    - Rotas estáticas: destino 10.12.255.4/32, nexthop Olá VPN túnel interface too40.112.190.5 destino 10.12.255.5/32, nexthop Olá VPN túnel interface too138.91.156.129
    - eBGP Multihop: Verifique se a opção de "multihop" hello eBGP estiver habilitado no seu dispositivo, se necessário

deve ser estabelecida a conexão Olá após alguns minutos e a sessão de emparelhamento Olá BGP iniciará uma vez estabelecida a conexão IPsec de saudação. Este exemplo até o momento tiver configurado somente um dispositivo VPN local, resultando em um diagrama de saudação mostrado abaixo:

![ativo-ativo-entre-os-locais](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a>Etapa 3 - conectar dois em dispositivos toohello ativa VPN gateway de VPN local
Se você tiver dois dispositivos VPN Olá mesmo local rede, você pode obter redundância dupla conexão hello Azure toohello segundo VPN dispositivo de gateway VPN.

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a>1. Criar gateway de rede local segundo Olá para Site5
Observe que o endereço IP de gateway hello, prefixo de endereço e endereço emparelhamento BGP para gateway de rede local segundo Olá não devem sobrepor gateway de rede local anterior Olá para Olá mesmo rede no local.

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a>2. Conecte-se o gateway de rede virtual hello e segundo gateway de rede local Olá
Criar conexão de saudação do TestVNet1 tooSite5_2 com "EnableBGP" definido muito$ True

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a>3. Parâmetros VPN e BGP para seu segundo dispositivo VPN local
Da mesma forma, listas de parâmetros de saudação abaixo será informado no dispositivo VPN segundo hello:

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5
                         Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

Após o estabelecimento de conexão da saudação (túneis), você terá dois dispositivos VPN redundantes e túneis ao se conectar a sua rede local e o Azure:

![redundância-dupla-entre-os-locais](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <a name ="aav2v"></a>Parte 3 – Estabelecer uma conexão VNet para VNet ativo-ativo
Esta seção cria uma conexão VNet para VNet ativo-ativo com o BGP. 

instruções de saudação abaixo continuam nas etapas anteriores de Olá listadas acima. Você deve concluir [parte 1](#aagateway) toocreate configurar TestVNet1 e Olá Gateway de VPN com o BGP. 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a>Etapa 1 - criar TestVNet2 e hello gateway VPN
É importante toomake-se de que o espaço de endereço IP de saudação do hello nova rede virtual, TestVNet2, não coincide com nenhum dos seus intervalos de rede virtual.

Neste exemplo, redes virtuais Olá pertencem toohello mesma assinatura. Você pode configurar conexões de rede virtual a rede entre as diferentes assinaturas; Consulte também[configurar uma conexão de rede virtual a rede](vpn-gateway-vnet-vnet-rm-ps.md) toolearn mais detalhes. Certifique-se de adicionar hello "-EnableBgp $True" ao criar hello conexões tooenable BGP.

#### <a name="1-declare-your-variables"></a>1. Declare as variáveis
Ser tooreplace se valores Olá Olá aqueles que você deseja toouse para sua configuração.

```powershell
$RG2 = "TestAARG2"
$Location2 = "East US"
$VNetName2 = "TestVNet2"
$FESubName2 = "FrontEnd"
$BESubName2 = "Backend"
$GWSubName2 = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$VNet2ASN = 65020
$DNS2 = "8.8.8.8"
$GWName2 = "VNet2GW"
$GW2IPName1 = "VNet2GWIP1"
$GW2IPconf1 = "gw2ipconf1"
$GW2IPName2 = "VNet2GWIP2"
$GW2IPconf2 = "gw2ipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a>2. Criar TestVNet2 no novo grupo de recursos Olá

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a>3. Criar gateway VPN Olá ativo-ativo para TestVNet2
Solicitação dois pública endereços toobe toohello alocado gateway IP que você criará para sua rede virtual. Você também definirá sub-rede hello e as configurações de IP necessárias.

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

Crie gateway VPN Olá com hello como número e hello sinalizador de "EnableActiveActiveFeature". Observe que você deve substituir o padrão de saudação ASN em seus gateways de VPN do Azure. Olá ASNs para Olá conectado VNets deve ser diferente tooenable BGP e roteamento de tráfego.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a>Etapa 2: conectar gateways de TestVNet1 e TestVNet2 Olá
Neste exemplo, ambos os gateways estão em Olá mesma assinatura. Você pode concluir esta etapa no hello mesma sessão do PowerShell.

#### <a name="1-get-both-gateways"></a>1. Obter ambos os gateways
Certifique-se de entrar e conectar-se tooSubscription 1.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a>2. Criar ambas as conexões
Nesta etapa, você criará conexão Olá de TestVNet1 tooTestVNet2 e conexão de saudação do TestVNet2 tooTestVNet1.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> Ser tooenable se BGP para ambas as conexões.
> 
> 

Depois de concluir essas etapas, ser estabeleça conexão Olá em alguns minutos e sessão de emparelhamento de BGP hello serão backup após a conclusão da conexão Olá VNet para VNet com redundância dupla:

![ativo-ativo-v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <a name ="aaupdate"></a>Parte 4 – Atualizar o gateway existente entre ativo-ativo e ativo-em espera
última seção do Hello descrevem como você pode configurar um gateway de VPN do Azure existente ativo-ativo tooactive do modo de espera, ou vice-versa.

> [!NOTE]
> Esta seção inclui Olá etapas tooresize um herdado SKU (SKU antigo) de um gateway VPN já criado do tooHighPerformance padrão. Essas etapas não atualizarem um antigo tooone herdado de SKU de saudação SKUs de novo.
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a>Configurar um gateway ativa / em espera de tooactive-ativo
#### <a name="1-gateway-parameters"></a>1. Parâmetros do gateway
saudação de exemplo a seguir converte um gateway ativa / em espera em um gateway de ativo-ativo. Você precisa toocreate outro endereço IP público e adiciona uma segunda configuração de IP do Gateway. Abaixo mostra hello parâmetros usados:

```powershell
$GWName = "TestVNetAA1GW"
$VNetName = "TestVNetAA1"
$RG = "TestVPNActiveActive01"
$GWIPName2 = "gwpip2"
$GWIPconf2 = "gw1ipconf2"

$vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$location = $gw.Location
```

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a>2. Criar endereço IP público de saudação, em seguida, Adicionar configuração de IP de gateway segundo Olá

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a>3. Ativar Ativa modo e atualização de gateway de saudação
Você deve definir o objeto de gateway Olá atualização real do PowerShell tootrigger hello. Olá SKU do gateway de rede virtual Olá deve também ser alterado tooHighPerformance (redimensionado) desde que ele foi criado anteriormente como padrão.

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

Essa atualização pode levar 30 minutos too45.

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a>Configure um gateway de espera de tooactive gateway ativo-ativo
#### <a name="1-gateway-parameters"></a>1. Parâmetros do gateway
Use Olá mesmo parâmetros acima, obter o nome de Olá Olá da configuração de IP desejar tooremove.

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a>2. Remover configuração de IP de gateway hello e desativar o modo de ativo-ativo de saudação
Da mesma forma, você deve definir o objeto de gateway de saudação em atualização real do PowerShell tootrigger hello.

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

Essa atualização pode levar até too30 muito 45 minutos.

## <a name="next-steps"></a>Próximas etapas
Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais. Veja [Criar uma máquina virtual](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter as etapas.
