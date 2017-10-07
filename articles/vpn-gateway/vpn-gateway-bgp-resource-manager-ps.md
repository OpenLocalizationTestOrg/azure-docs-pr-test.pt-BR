---
title: 'Configurar o BGP em Gateways de VPN: Gerenciador de Recursos: PowerShell | Microsoft Docs'
description: Este artigo mostra como configurar o BGP com Gateways de VPN do Azure usando o Azure Resource Manager e o PowerShell.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 905b11a7-1333-482c-820b-0fd0f44238e5
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: yushwang
ms.openlocfilehash: a9d13ae6b319e2efa8965dc2955c9b89ac3fd12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-bgp-on-azure-vpn-gateways-using-powershell"></a>Como tooconfigure BGP em Gateways de VPN do Azure usando o PowerShell
Este artigo orienta Olá etapas tooenable BGP em uma conexão de VPN Site a Site (S2S) entre locais e uma conexão de rede virtual a rede usando o modelo de implantação do Gerenciador de recursos de saudação e PowerShell.

## <a name="about-bgp"></a>Sobre o BGP
O BGP é Olá protocolo de roteamento padrão usado em Olá tooexchange roteamento e acessibilidade informações da Internet entre duas ou mais redes. Habilita o BGP Olá Gateways de VPN do Azure e os dispositivos VPN local, chamados de pares de BGP ou vizinhos, tooexchange "rotas" informará ambos os gateways na disponibilidade hello e acessibilidade para os prefixos toogo por meio de gateways de saudação ou roteadores envolvidos. BGP também pode habilitar o roteamento de tráfego entre várias redes propagando rotas aprende um gateway BGP de um tooall de par BGP outros pares de BGP.

Consulte [visão geral do BGP com Gateways de VPN do Azure](vpn-gateway-bgp-overview.md) para obter mais detalhes sobre os benefícios do BGP e toounderstand requisitos técnicos de saudação e considerações do uso de BGP.

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a>Introdução ao BGP em gateways de VPN do Azure

Este artigo orienta Olá Olá de toodo etapas seguintes tarefas:

* [Parte 1 - Habilitar o BGP em seu gateway de VPN do Azure](#enablebgp)
* [Parte 2 - Estabelecer uma conexão entre instalações com BGP](#crossprembgp)
* [Parte 3 - Estabelecer uma conexão VNet para VNet com BGP](#v2vbgp)

Cada parte de instruções Olá constitui um bloco de construção básico para habilitar o BGP em sua conectividade de rede. Se você concluir todas as três partes, criar uma topologia de hello, conforme mostrado no diagrama a seguir de saudação:

![Topologia BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

Você pode combinar partes juntos toobuild uma rede de trânsito mais complexos e de vários saltos, que atende às suas necessidades.

## <a name ="enablebgp"></a>Parte 1 - configurar o BGP Olá Gateway de VPN do Azure
etapas de configuração de saudação configurar Olá parâmetros de BGP de gateway de VPN do Azure Olá conforme mostrado no diagrama a seguir de saudação:

![Gateway BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a>Antes de começar
* Verifique se você tem uma assinatura do Azure. Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Instale os cmdlets do PowerShell do Azure Resource Manager hello. Para obter mais informações sobre como instalar os cmdlets do PowerShell hello, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview). 

### <a name="step-1---create-and-configure-vnet1"></a>Etapa 1 - Criar e configurar VNet1
#### <a name="1-declare-your-variables"></a>1. Declare as variáveis
Para este exercício, começaremos declarando nossa variáveis. Olá, exemplo a seguir declara variáveis hello usando valores de saudação para este exercício. Ser valores de saudação tooreplace-se com seu próprio durante a configuração de produção. Você pode usar essas variáveis, se você estiver executando a saudação etapas toobecome familiarizado com esse tipo de configuração. Modificar variáveis de Olá e, em seguida, copie e cole o console do PowerShell.

```powershell
$Sub1 = "Replace_With_Your_Subcription_Name"
$RG1 = "TestBGPRG1"
$Location1 = "East US"
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
$GWIPName1 = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection12 = "VNet1toVNet2"
$Connection15 = "VNet1toSite5"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Conecte-se a assinatura de tooyour e criar um novo grupo de recursos
toouse Olá cmdlets do Gerenciador de recursos, verifique se você alternar o modo de tooPowerShell. Para obter mais informações, consulte [Usando o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).

Abra o console do PowerShell e conecte-se a conta de tooyour. Use Olá toohelp de exemplo que você se conectar a seguir:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3. Criar TestVNet1
Olá, exemplo a seguir cria uma rede virtual denominada TestVNet1 e três sub-redes, um GatewaySubnet chamado, um front-end chamado e back-end chamado um. Ao substituir valores, é importante você sempre nomear sua sub-rede de gateway especificamente como GatewaySubnet. Se você usar outro nome, a criação do gateway falhará.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-bgp-parameters"></a>Etapa 2: criar hello Gateway VPN para TestVNet1 com parâmetros de BGP
#### <a name="1-create-hello-ip-and-subnet-configurations"></a>1. Criar configurações de IP e a sub-rede de saudação
Solicite um público endereço toobe toohello alocado gateway IP que você criará para sua rede virtual. Você também definirá sub-rede Olá necessário e as configurações de IP.

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-hello-vpn-gateway-with-hello-as-number"></a>2. Criar gateway VPN Olá com hello como número
Crie gateway de rede virtual Olá para TestVNet1. BGP requer um baseadas em rota gateway VPN e o parâmetro hello adição - Asn tooset Olá ASN (número) para TestVNet1. Se você não definir parâmetro ASN hello, ASN 65515 é atribuído. Criar um gateway pode demorar um pouco (30 minutos ou mais toocomplete).

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-hello-azure-bgp-peer-ip-address"></a>3. Obter o endereço de IP de par de BGP Azure Olá
Depois de criar gateway Olá, é necessário tooobtain Olá BGP Peer endereço IP de saudação Gateway de VPN do Azure. Esse endereço é necessário tooconfigure Olá Gateway de VPN do Azure como um par de BGP para seus dispositivos VPN local.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

comando último Olá mostra configurações de BGP correspondentes da saudação no hello Gateway de VPN do Azure; Por exemplo:

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

Depois que o gateway de saudação é criado, você pode usar esta conexão do gateway tooestablish entre locais ou a conexão de rede virtual a rede com BGP. Olá seções a seguir percorrer Olá etapas toocomplete Olá exercício.

## <a name ="crossprembbgp"></a>Parte 2 - Estabelecer uma conexão entre instalações com BGP

tooestablish uma conexão entre locais, você precisa toocreate toorepresent um Gateway de rede Local seu dispositivo VPN no local e um gateway VPN de saudação tooconnect Conexão com o gateway de rede local hello. Enquanto há artigos que orientá-lo através dessas etapas, este artigo contém parâmetros de configuração de BGP Olá propriedades adicionais necessárias toospecify hello.

![BGP para entre instalações](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

Antes de prosseguir, verifique se você concluiu a [Parte 1](#enablebgp) deste exercício.

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a>Etapa 1: criar e configurar o gateway de rede local Olá

#### <a name="1-declare-your-variables"></a>1. Declare as variáveis

Este exercício continua a configuração de saudação toobuild mostrada no diagrama de saudação. Ser tooreplace se valores Olá Olá aqueles que você deseja toouse para sua configuração.

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

Algumas coisas toonote sobre parâmetros de gateway de rede local hello:

* gateway de rede local Olá pode estar em Olá mesmo ou outro local e o recurso grupo Olá gateway VPN. Este exemplo os mostra em grupos de recursos diferentes em locais diferentes.
* prefixo de mínimo Olá precisar toodeclare para gateway de rede local Olá é endereço do host de saudação do seu endereço IP de par de BGP em seu dispositivo VPN. Nesse caso, é um prefixo /32 de "10.52.255.254/32".
* Como lembrete, você deve usar diferentes ASNs BGP entre suas redes locais e a VNet do Azure. Se eles são hello mesmo, você precisará toochange sua VNet ASN se seu dispositivo VPN local já usa Olá ASN toopeer com outros vizinhos de BGP.

Antes de continuar, verifique se que você está conectado ainda tooSubscription 1.

#### <a name="2-create-hello-local-network-gateway-for-site5"></a>2. Criar gateway de rede local Olá para Site5

Ser-se de grupo de recursos de saudação toocreate se ele não for criado, antes de criar o gateway de rede local hello. Observe os parâmetros adicionais de saudação dois para gateway de rede local Olá: Asn e BgpPeerAddress.

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a>Etapa 2: conectar-se o gateway de rede virtual hello e gateway de rede local

#### <a name="1-get-hello-two-gateways"></a>1. Obter Olá dois gateways

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a>2. Criar conexão de tooSite5 TestVNet1 Olá

Nesta etapa, você pode criar conexão de saudação do TestVNet1 tooSite5. Você deve especificar "-EnableBGP $True" tooenable BGP para esta conexão. Como discutido anteriormente, é possível toohave conexões de BGP e BGP não Olá mesmo Gateway de VPN do Azure. A menos que o BGP é habilitado na propriedade de conexão Olá, Azure não irá habilitar BGP para esta conexão, embora os parâmetros BGP já estão configurados em ambos os gateways.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

Olá exemplo a seguir lista os parâmetros de saudação inseridos na seção de configuração de BGP de saudação em seu dispositivo VPN local para este exercício:

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being hello VPN tunnel interface on your device
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

conexão de saudação é estabelecida após alguns minutos e inicia Olá BGP de emparelhamento sessão uma vez estabelecida a conexão IPsec de saudação.

## <a name ="v2vbgp"></a>Parte 3 - Estabelecer uma conexão VNet para VNet com BGP

Esta seção adiciona uma conexão de rede virtual a rede com BGP, conforme mostrado no diagrama a seguir de saudação:

![BGP de VNet para VNet](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

Olá seguindo instruções continuar nas etapas anteriores hello. Você deve concluir [parte I](#enablebgp) toocreate configurar TestVNet1 e Olá Gateway de VPN com o BGP. 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a>Etapa 1 - criar TestVNet2 e hello gateway VPN

É importante toomake-se de que o espaço de endereço IP de saudação do hello nova rede virtual, TestVNet2, não coincide com nenhum dos seus intervalos de rede virtual.

Neste exemplo, redes virtuais Olá pertencem toohello mesma assinatura. Você pode configurar conexões de rede virtual a rede entre assinaturas diferentes. Para saber mais, veja [Configurar uma conexão VNet com VNet](vpn-gateway-vnet-vnet-rm-ps.md). Certifique-se de adicionar hello "-EnableBgp $True" ao criar hello conexões tooenable BGP.

#### <a name="1-declare-your-variables"></a>1. Declare as variáveis

Ser tooreplace se valores Olá Olá aqueles que você deseja toouse para sua configuração.

```powershell
$RG2 = "TestBGPRG2"
$Location2 = "West US"
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
$GWIPName2 = "VNet2GWIP"
$GWIPconfName2 = "gwipconf2"
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

#### <a name="3-create-hello-vpn-gateway-for-testvnet2-with-bgp-parameters"></a>3. Criar gateway VPN Olá para TestVNet2 com parâmetros de BGP

Solicite um público endereço toobe toohello alocado gateway IP você criará para a sua rede virtual e defina a sub-rede Olá necessário e as configurações de IP.

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

Criar gateway VPN Olá com hello como número. Você deve substituir o padrão de saudação ASN em seus gateways de VPN do Azure. Olá ASNs para Olá conectado VNets deve ser diferente tooenable BGP e roteamento de tráfego.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
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

Nesta etapa, você criar conexão de saudação do TestVNet1 tooTestVNet2 e conexão de saudação do TestVNet2 tooTestVNet1.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> Ser tooenable se BGP para ambas as conexões.
> 
> 

Depois de concluir essas etapas, é estabelecida conexão Olá após alguns minutos. sessão de emparelhamento Olá BGP é concluída Olá conexão de rede virtual a rede.

Se você concluiu todas as três partes para este exercício, estabelecer Olá topologia de rede a seguir:

![BGP de VNet para VNet](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a>Próximas etapas

Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais. Veja [Criar uma máquina virtual](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter as etapas.
