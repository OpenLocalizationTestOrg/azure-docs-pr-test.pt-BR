---
title: 'Conecte-se a sua rede de local tooan rede virtual do Azure: VPN Site a Site: PowerShell | Microsoft Docs'
description: "Etapas toocreate uma conexão IPsec de seu local de rede tooan rede virtual do Azure sobre Olá Internet pública. Essas etapas o ajudarão a criar uma conexão de Gateway de VPN Site a Site entre locais usando o PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: cb8db1dab3a5488816a7f7e8e63908a4c02f55db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a>Criar uma Rede Virtual com uma conexão VPN site a site usando o PowerShell

Este artigo mostra como toouse conexão de gateway VPN do PowerShell toocreate uma Site a Site do seu local de rede toohello VNet. Olá etapas neste artigo se aplicam a modelo de implantação do Gerenciador de recursos de toohello. Você também pode criar essa configuração usando uma ferramenta de implantação diferente ou um modelo de implantação, selecionando uma opção diferente de saudação lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portal do Azure (clássico)](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [Portal clássico (clássico)](vpn-gateway-site-to-site-create.md)
> 
>


Uma conexão de gateway VPN Site a Site é usado tooconnect seu local de rede tooan rede virtual do Azure por um túnel VPN IPsec/IKE (IKEv1 ou IKEv2). Esse tipo de conexão exige um VPN de dispositivos localizado localmente que tenha uma tooit de endereço atribuído de IP público externamente. Para saber mais sobre os gateways de VPN, veja [Sobre o gateway de VPN](vpn-gateway-about-vpngateways.md).

![Diagrama de conexão Site a Site de Gateway de VPN entre locais](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <a name="before"></a>Antes de começar

Verifique se você atendeu a saudação critérios a seguir antes de começar a configuração:

* Verifique se você tem um dispositivo VPN compatível e alguém que é capaz de tooconfigure-lo. Para obter mais informações sobre dispositivos VPN compatíveis e a configuração de dispositivo, confira [Sobre dispositivos VPN](vpn-gateway-about-vpn-devices.md).
* Verifique se você possui um endereço IPv4 público voltado para o exterior para seu dispositivo VPN. Esse endereço IP não pode estar localizado atrás de um NAT.
* Se você não estiver familiarizado com intervalos de endereços IP de saudação localizados na configuração de rede local, é necessário toocoordinate com alguém que possa fornecer os detalhes para você. Quando você criar essa configuração, você deve especificar os prefixos de intervalo endereço IP hello Azure encaminhe tooyour no local. Nenhuma das sub-redes Olá da sua rede local pode ser sobre colo com sub-redes de rede virtual Olá que você deseja tooconnect para.
* Instale a versão mais recente Olá de saudação cmdlets do PowerShell do Gerenciador de recursos do Azure. Cmdlets do PowerShell são atualizados com frequência e você geralmente precisará tooupdate sua funcionalidade de recurso mais recente de saudação do PowerShell cmdlets tooget. Se você não atualizar seus cmdlets do PowerShell, valores hello especificados poderão falhar. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre como baixar e instalar os cmdlets do PowerShell.

### <a name="example"></a>Valores de exemplo

Olá exemplos neste artigo usam Olá valores a seguir. Você pode usar esses valores toocreate um ambiente de teste, ou consulte toothem toobetter entender exemplos Olá neste artigo.

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <a name="Login"></a>1. Conecte-se a assinatura de tooyour

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="VNet"></a>2. Criar uma rede virtual e uma sub-rede de gateway

Se você ainda não tiver uma rede virtual, crie uma. Ao criar uma rede virtual, certifique-se de que os espaços de endereço Olá que você especificar não se sobrepõem a nenhum Olá dos espaços de endereço que você tem em sua rede local.

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="vnet"></a>toocreate uma rede virtual e uma sub-rede do gateway

O exemplo a seguir cria uma rede virtual e uma sub-rede de gateway. Se você já tiver uma rede virtual que você precisa tooadd uma sub-rede do gateway para ver [tooadd uma gateway sub-rede tooa rede virtual já tiver criado](#gatewaysubnet).

Crie um grupo de recursos:

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

Criar sua rede virtual.

1. Definir variáveis de saudação.

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. Crie hello VNet.

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <a name="gatewaysubnet"></a>tooadd uma rede virtual do gateway sub-rede tooa você já criou

1. Definir variáveis de saudação.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. Crie uma sub-rede de gateway hello.

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. Definir a configuração de saudação.

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## 3. <a name="localnet"></a>Criar gateway de rede local Olá

Normalmente, o gateway de rede local Olá refere-se tooyour no local. Atribuir o site Olá um nome pelo qual Azure pode consulte tooit e especifique o endereço IP de saudação do hello toowhich de dispositivo VPN de local, você criará uma conexão. Você também pode especificar prefixos de endereço IP de saudação que serão encaminhados através do dispositivo de VPN toohello do gateway VPN hello. especificar os prefixos de endereço Olá são prefixos Olá localizados em sua rede local. Se sua rede local for alterada, você pode atualizar facilmente prefixos hello.

Use Olá valores a seguir:

* Olá *GatewayIPAddress* é o endereço IP de saudação do seu dispositivo VPN local. O dispositivo VPN não pode estar localizado atrás de um NAT.
* Olá *AddressPrefix* é espaço de endereço de seu local.

tooadd um gateway de rede local com um único prefixo de endereço:

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

tooadd um gateway de rede local com vários prefixos de endereço:

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

prefixos de endereço IP de toomodify para o gateway de rede local:<br>
Às vezes, os prefixos de gateway de rede local são alterados. etapas de saudação você tomar toomodify seu endereço IP prefixos dependem se você tiver criado uma conexão de gateway VPN. Consulte Olá [prefixos de endereço IP modificar para um gateway de rede local](#modify) deste artigo.

## <a name="PublicIP"></a>4. Solicite um endereço IP público

Um gateway de VPN deve ter um endereço IP público. Você primeiro solicitar o recurso de endereço IP hello e, em seguida, consulte tooit ao criar o gateway de rede virtual. endereço IP de saudação é atribuído dinamicamente recursos toohello ao gateway de VPN Olá é criado. O gateway de VPN atualmente suporta apenas alocação de endereços IP público *Dinâmico*. Você não pode solicitar uma atribuição de endereço IP Público Estático. No entanto, isso não significa que o endereço IP de saudação alterado depois que ele foi atribuído tooyour gateway VPN. somente tempo de saudação alterações de endereço IP público hello quando é Olá gateway é excluído e criado novamente. Isso não altera o redimensionamento, a redefinição ou outras manutenções/atualizações internas do seu gateway de VPN.

Solicite um endereço IP público que será atribuído tooyour de gateway VPN de rede virtual.

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <a name="GatewayIPConfig"></a>5. Criar a configuração de endereçamento de IP de gateway Olá

configuração do gateway Olá define sub-rede hello e toouse de endereço IP público hello. Use sua configuração de gateway de Olá toocreate de exemplo a seguir:

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <a name="CreateGateway"></a>6. Criar gateway VPN Olá

Crie gateway de VPN de rede virtual hello. Criar um gateway VPN pode demorar até too45 minutos ou mais toocomplete.

Use Olá valores a seguir:

* Olá *- GatewayType* para uma Site a Site configuração é *Vpn*. tipo de gateway Olá é sempre configuração toohello específico que você está implementando. Por exemplo, outras configurações de gateway podem exigir -GatewayType ExpressRoute.
* Olá *- VpnType* pode ser *RouteBased* (conhecida tooas um Gateway dinâmico em alguns documentos), ou *PolicyBased* (chamado tooas um Gateway estático em alguns documentos ). Para saber mais sobre os tipos de gateway de VPN, veja [Sobre o Gateway de VPN](vpn-gateway-about-vpngateways.md).
* Selecione Olá SKU de Gateway que você deseja toouse. Há limitações de configuração para alguns SKUs. Para obter mais informações, confira [SKUs de gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku). Se você receber um erro ao criar o gateway VPN Olá sobre Olá - GatewaySku, verifique se você instalou a versão mais recente Olá Olá de cmdlets do PowerShell.

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <a name="ConfigureVPNDevice"></a>7. Configurar o dispositivo de VPN

Rede de local de tooan conexões site a Site requer um dispositivo VPN. Nesta etapa, você deve configurar seu dispositivo VPN. Ao configurar seu dispositivo VPN, você precisa seguir hello:

- Uma chave compartilhada. Isso é Olá mesmo chave que você especificar ao criar sua conexão VPN Site a Site. Em nossos exemplos, usamos uma chave compartilhada básica. É recomendável que você gerar um toouse chave mais complexa.
- Olá endereço IP público do seu gateway de rede virtual. Você pode exibir o endereço IP público de saudação usando Olá portal do Azure, PowerShell ou CLI. Olá toofind endereço IP público do seu gateway de rede virtual usando o PowerShell, use Olá exemplo a seguir:

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>8. Criar conexão de VPN Olá

Em seguida, crie uma conexão de VPN Site a Site Olá entre o gateway de rede virtual e seu dispositivo VPN. Ser valores de saudação tooreplace-se com seus próprios. chave compartilhada Olá deve corresponder o valor de saudação usado para a sua configuração de dispositivo VPN. Observe que Olá '-ConnectionType' para o Site a Site é *IPsec*.

1. Definir variáveis de saudação.
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. Crie conexão hello.
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

Após um instante, Olá conexão será estabelecida.

## <a name="toverify"></a>9. Verifique se a conexão de VPN Olá

Há alguns tooverify de maneiras diferentes de sua conexão VPN.

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="connectVM"></a>máquina de virtual tooa tooconnect

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <a name="modify"></a>Modifique os prefixos do endereço IP para um gateway de rede local

Se alterar de prefixos de endereço IP hello ser roteada tooyour local, você pode modificar o gateway de rede local hello. São fornecidos dois conjuntos de instruções. instruções de saudação que você escolher dependem se você já criou sua conexão de gateway.

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="modifygwipaddress"></a>Modificar o endereço IP do gateway Olá para um gateway de rede local

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>Próximas etapas

*  Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais. Para saber mais, veja [Máquinas virtuais](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Para obter informações sobre o BGP, consulte Olá [visão geral de BGP](vpn-gateway-bgp-overview.md) e [como tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
