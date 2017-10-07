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
# <a name="configure-forced-tunneling-using-hello-azure-resource-manager-deployment-model"></a>Configurar o túnel forçado usando o modelo de implantação do Azure Resource Manager Olá

Forçado permite redirecionar ou "forçar" todos os direcionado à Internet tráfego tooyour back local através de um túnel VPN Site a Site para inspeção e auditoria de túnel. Esse é um requisito crítico de segurança para a maioria das políticas de TI empresariais. Sem o túnel forçado, o tráfego direcionado à Internet de suas VMs no Azure sempre atravessa da infraestrutura de rede do Azure diretamente out toohello Internet, sem Olá opção tooallow você tráfego de saudação tooinspect ou auditoria. Acesso não autorizado pode levar a divulgação de tooinformation ou outros tipos de violações de segurança.

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

Este artigo o orienta pela configuração forçado túnel para redes virtuais criadas usando o modelo de implantação do Gerenciador de recursos de saudação. O túnel forçado pode ser configurado usando o PowerShell, não por meio do portal de saudação. Se você quiser tooconfigure encapsulamento para o modelo de implantação clássico Olá forçado, selecione artigo clássico Olá lista suspensa a seguir:

> [!div class="op_single_selector"]
> * [PowerShell - clássico](vpn-gateway-about-forced-tunneling.md)
> * [PowerShell – Resource Manager](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a>Sobre túnel forçado

Olá diagrama a seguir ilustra os túneis forçados como funcionam. 

![Túnel forçado](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

O exemplo hello acima, Olá front-end subrede não será forçada encapsulado. cargas de trabalho Olá na sub-rede de front-end Olá podem continuar tooaccept e responde solicitações toocustomer de saudação Internet diretamente. Olá sub-redes de camada intermediária e back-end são forçados encapsulado. Quaisquer conexões de saída da toohello duas sub-redes Internet será tooan forçada ou redirecionado de volta no site local por meio de saudação que encapsulamentos VPN S2S.

Isso permite que você toorestrict e inspecione o acesso à Internet de suas máquinas virtuais ou serviços no Azure, de nuvem enquanto continua tooenable sua arquitetura de serviço de várias camadas necessária. Se não houver nenhuma carga de trabalho para a Internet em suas redes virtuais, você também pode aplicar forçado túnel toohello redes virtuais inteiras.

## <a name="requirements-and-considerations"></a>Requisitos e considerações

O túnel forçado no Azure é configurado por meio de rotas de rede virtual definidas pelo usuário. Redirecionar o tráfego tooan local do site é expressa como um gateway de VPN do Azure toohello rota padrão. Para saber mais sobre rotas definidas pelo usuário e redes virtuais, confira [Encaminhamento IP e rotas definidas pelo usuário](../virtual-network/virtual-networks-udr-overview.md).

* Cada sub-rede de rede virtual tem uma tabela de roteamento interna do sistema. tabela de roteamento de sistema Olá tem Olá três grupos de rotas a seguir:
  
  * **Rotas de rede virtual locais:** diretamente toohello VMs de destino na Olá mesma rede virtual.
  * **Rotas locais:** toohello gateway de VPN do Azure.
  * **Rota padrão:** toohello diretamente da Internet. Pacotes destinados toohello endereços IP privados não cobertos por rotas Olá dois anterior são removidos.
* Este procedimento usa as rotas definidas pelo usuário (UDR) toocreate um tooadd de tabela de roteamento uma rota padrão e, em seguida, associar Olá tabela tooyour VNet sub-redes tooenable forçado nessas sub-redes de encapsulamento de roteamento.
* O túnel forçado deve ser associado a uma Rede Virtual que tenha um Gateway de VPN de roteamento. É necessário tooset "site padrão" entre a rede virtual de toohello conectado Olá de sites locais entre locais. Além disso, Olá local do dispositivo VPN deve ser configurado usando 0.0.0.0/0 como seletores de tráfego. 
* Túnel forçado do ExpressRoute não está configurado por meio desse mecanismo, mas em vez disso, é habilitado por anuncia uma rota padrão por meio de saudação ExpressRoute BGP sessões de emparelhamento. Para obter mais informações, consulte Olá [documentação de rota expressa](https://azure.microsoft.com/documentation/services/expressroute/).

## <a name="configuration-overview"></a>Visão geral de configuração

Olá procedimento a seguir para criar um grupo de recursos e uma rede virtual. Em seguida, você criará um gateway de VPN e configurará um túnel forçado. Neste procedimento, a rede virtual de saudação 'MultiTier-VNet' tem três sub-redes: 'Front-end', 'Midtier' e 'Back-end', com quatro conexões entre locais: 'DefaultSiteHQ' e três ramificações.

etapas do procedimento Olá definir Olá 'DefaultSiteHQ' como conexão de site saudação padrão para túnel forçado e configurar hello 'Midtier' e 'Back-end' sub-redes toouse túnel forçado.

## <a name="before-you-begin"></a>Antes de começar

Instale a versão mais recente Olá de saudação cmdlets do PowerShell do Gerenciador de recursos do Azure. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre como instalar os cmdlets do PowerShell hello.

### <a name="toolog-in"></a>toolog em

[!INCLUDE [toolog in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a>Configurar o túnel forçado

1. Crie um grupos de recursos.

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. Crie uma rede virtual e especifique as sub-redes.

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. Crie hello gateways de rede local.

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. Crie regra de rota e de tabela de rota hello.

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. Associe Olá rota tabela toohello Midtier e sub-redes de back-end.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. Crie hello Gateway com um site padrão. Esta etapa leva alguns toocomplete de tempo, às vezes, 45 minutos ou mais, porque você está criando e configurando o gateway de saudação.<br> Olá **- GatewayDefaultSite** é Olá parâmetro de cmdlet que permite Olá forçado toowork de configuração de roteamento, portanto cuidado tooconfigure essa configuração adequadamente. Esse parâmetro está disponível no PowerShell 1.0 ou versão posterior.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. Estabelecer conexões de VPN Olá Site a Site.

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