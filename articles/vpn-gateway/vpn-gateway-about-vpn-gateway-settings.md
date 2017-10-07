---
title: "as configurações do gateway aaaVPN para conexões do Azure entre locais | Microsoft Docs"
description: "Saiba mais sobre as configurações do Gateway de VPN para gateways de rede virtual do Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: ae665bc5-0089-45d0-a0d5-bc0ab4e79899
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: cherylmc
ms.openlocfilehash: 01229d99fa37e30e00aa00f939f488d631b5593c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a>Sobre definições de configuração do Gateway de VPN

Um gateway de VPN é um tipo de gateway de rede virtual que envia o tráfego criptografado entre sua rede virtual e seu local em uma conexão pública. Você também pode usar um tráfego de toosend do gateway VPN entre redes virtuais em Olá backbone do Azure.

Uma conexão de gateway VPN depende da configuração de saudação de vários recursos, cada uma delas contém as definições configuráveis. seções neste artigo Olá abordam recursos hello e as configurações relacionadas tooa gateway VPN para uma rede virtual criada no modelo de implantação do Gerenciador de recursos. Você pode encontrar descrições e diagramas de topologia para cada solução de conexão do hello [sobre o Gateway de VPN](vpn-gateway-about-vpngateways.md) artigo.

## <a name="gwtype"></a>Tipos de gateway

Cada rede virtual pode ter apenas um gateway de rede virtual de cada tipo. Quando você estiver criando um gateway de rede virtual, você deve se certificar que o tipo de gateway de Olá está correto para sua configuração.

Olá - GatewayType em valores disponíveis é:

* Vpn
* ExpressRoute

Um gateway de VPN requer Olá `-GatewayType` *Vpn*.

Exemplo:

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <a name="gwsku"></a>SKUs do Gateway

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-hello-gateway-sku"></a>Configurar o gateway de saudação SKU

#### <a name="azure-portal"></a>Portal do Azure

Se você usar Olá toocreate portal do Azure um gateway de rede virtual do Gerenciador de recursos, você pode selecionar o SKU do gateway hello usando o menu suspenso de saudação. Opções de saudação que são apresentadas correspondem toohello tipo de Gateway e o tipo VPN que você selecionar.

#### <a name="powershell"></a>PowerShell

exemplo a seguir do PowerShell Hello Especifica Olá `-GatewaySku` como VpnGw1.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <a name="resize"></a>Alterar (redimensionar) uma SKU de gateway

Se você quiser que sua tooa SKU de gateway tooupgrade SKU mais avançado, você pode usar o hello `Resize-AzureRmVirtualNetworkGateway` cmdlet do PowerShell. Você também pode fazer o downgrade de tamanho SKU de gateway hello usando este cmdlet.

Olá PowerShell de exemplo a seguir mostra que um SKU de gateway, que está sendo redimensionada tooVpnGw2.

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <a name="connectiontype"></a>Tipos de conexão

No modelo de implantação do Gerenciador de recursos de hello, cada configuração requer um tipo de conexão de gateway de rede virtual específica. Olá disponíveis do Gerenciador de recursos do PowerShell valores para `-ConnectionType` são:

* IPsec
* Vnet2Vnet
* ExpressRoute
* VPNClient

Olá PowerShell de exemplo a seguir, criamos uma conexão S2S que requer o tipo de conexão Olá *IPsec*.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <a name="vpntype"></a>Tipos de VPN

Quando você cria um gateway de rede virtual Olá para uma configuração de gateway VPN, você deve especificar um tipo VPN. Olá tipo VPN que você escolher depende de topologia de conexão de saudação que você deseja toocreate. Por exemplo, uma conexão P2S requer um tipo de VPN RouteBased. Um tipo VPN também pode depender de hardware Olá que você está usando. As configurações S2S requerem um dispositivo VPN. Alguns dispositivos VPN recebem suporte apenas de um determinado tipo de VPN.

Olá tipo VPN que você selecionar deve satisfazer todos os requisitos de conexão Olá para solução de saudação que deseja toocreate. Por exemplo, se você quiser toocreate Olá uma conexão de gateway de VPN S2S e uma conexão de gateway VPN de P2S para a mesma rede virtual, você usaria o tipo de VPN *RouteBased* porque P2S requer um tipo RouteBased VPN. Também é necessário que o dispositivo VPN com suporte a uma conexão VPN RouteBased de tooverify. 

Quando um gateway de rede virtual tiver sido criado, você não pode alterar o tipo VPN hello. Você tem toodelete Olá gateway de rede virtual e criar um novo. Há dois tipos de VPN:

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

exemplo a seguir do PowerShell Hello Especifica Olá `-VpnType` como *RouteBased*. Quando você estiver criando um gateway, você deve garantir que Olá - VpnType está correto para a sua configuração.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <a name="requirements"></a>Requisitos do gateway

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <a name="gwsub"></a>Sub-rede do gateway

Antes de criar um gateway de VPN, crie uma sub-rede de gateway. sub-rede de gateway Olá contém endereços IP hello esse gateway de rede virtual Olá VMs e serviços usam. Quando você criar o gateway de rede virtual, gateway VMs são sub-rede do gateway toohello implantado e configurado com as configurações de gateway VPN Olá necessário. Você nunca deve implantar a sub-rede de gateway toohello qualquer outra transação (por exemplo, VMs adicionais). sub-rede de gateway Olá deve ser nomeado 'GatewaySubnet' toowork corretamente. Azure nomenclatura sub-rede de gateway Olá 'GatewaySubnet' permite saber que este é o gateway de rede virtual Olá sub-rede toodeploy Olá VMs e serviços.

Quando você cria a sub-rede de gateway hello, você especificar Olá número de endereços IP que Olá sub-rede contém. endereços IP de saudação na sub-rede de gateway Olá são toohello alocado gateway VMs e serviços de gateway. Algumas configurações exigem mais endereços IP do que outras. Examinar as instruções de saudação para Olá a configuração que você deseja toocreate e verifique a sub-rede de gateway que Olá deseja toocreate atende a esses requisitos. Além disso, talvez você queira toomake-se de que sua sub-rede de gateway contém suficiente IP endereços tooaccommodate possíveis futuras configurações adicionais. Embora seja possível criar uma sub-rede de gateway tão pequena quanto /29, é recomendável criar uma sub-rede de gateway de /28 ou maior (/28, /27, /26 etc.). Dessa forma, se você adicionar funcionalidade de saudação futura, você não ter tootear seu gateway, em seguida, exclua e recrie Olá tooallow de sub-rede de gateway de mais endereços IP.

Olá, exemplo do PowerShell do Gerenciador de recursos a seguir mostra uma sub-rede de gateway denominada GatewaySubnet. Você pode ver a notação CIDR Olá Especifica um /27, que permite endereços IP suficientes para a maioria das configurações existentes no momento.

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <a name="lng"></a>Gateways de rede locais

Ao criar uma configuração de gateway VPN, o gateway de rede local Olá geralmente representa sua localização no local. No modelo de implantação clássico hello, gateway de rede local Olá foi chamado tooas um Site Local. 

Dê um nome de gateway de rede local hello, Olá endereço IP público do dispositivo VPN local hello e especificar prefixos de endereço de saudação que estão localizados em Olá no local. Azure examina os prefixos de endereço de destino Olá para o tráfego de rede, consulta configuração Olá que você especificou para o gateway de rede local e encaminha pacotes adequadamente. Você também especifica os gateways de rede para configurações de rede virtual para rede virtual que usam uma conexão de gateway de VPN.

Olá PowerShell de exemplo a seguir cria um novo gateway de rede local:

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

Às vezes você precisa de configurações de gateway de rede local toomodify hello. Por exemplo, quando você adiciona ou modificar o intervalo de endereços hello, ou se o endereço IP de saudação do dispositivo VPN Olá mudar. Para uma rede virtual clássica, você pode alterar essas configurações no portal clássico do hello na página de redes locais hello. Para o Resource Manager, confira [Modificar as configurações de gateway de rede local usando o PowerShell](vpn-gateway-modify-local-network-gateway.md).

## <a name="resources"></a>Cmdlets do PowerShell e APIs REST

Para obter recursos técnicos adicionais e requisitos de sintaxe específica ao usar APIs REST, os cmdlets do PowerShell ou CLI do Azure para configurações de Gateway de VPN, consulte Olá páginas a seguir:

| **Clássico** | **Gerenciador de Recursos** |
| --- | --- |
| [PowerShell](/powershell/module/azure#networking) |[PowerShell](/powershell/module/azurerm.network#vpn) |
| [API REST](https://msdn.microsoft.com/library/jj154113) |[API REST](/rest/api/network/virtualnetworkgateways) |
| Sem suporte | [CLI do Azure](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre as configurações de conexão disponíveis, confira [Sobre o Gateway de VPN](vpn-gateway-about-vpngateways.md).