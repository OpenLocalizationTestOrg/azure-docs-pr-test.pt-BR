---
title: 'Vincular um circuito de rota expressa do tooan de rede virtual: PowerShell: Azure | Microsoft Docs'
description: "Este documento fornece uma visão geral de como toolink virtual redes circuitos de tooExpressRoute (VNets) usando o modelo de implantação do Gerenciador de recursos de saudação e PowerShell."
services: expressroute
documentationcenter: na
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: daacb6e5-705a-456f-9a03-c4fc3f8c1f7e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: ganesr
ms.openlocfilehash: e75a9f6b42fa8e1a579e4f19882ec99b277b545f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a>Conectar uma rede virtual de tooan circuito de rota expressa
> [!div class="op_single_selector"]
> * [Portal do Azure](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [CLI do Azure](howto-linkvnet-cli.md)
> * [Vídeo – Portal do Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (clássico)](expressroute-howto-linkvnet-classic.md)
>

Este artigo ajuda você a vincular circuitos do ExpressRoute tooAzure redes virtuais (VNets) usando o modelo de implantação do Gerenciador de recursos de saudação e PowerShell. Redes virtuais podem ser em Olá mesma assinatura ou parte de outra assinatura. Este artigo mostra como vincular tooupdate uma rede virtual. 

## <a name="before-you-begin"></a>Antes de começar
* Instale a versão mais recente Olá dos módulos do PowerShell do Azure hello. Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).
* Saudação de revisão [pré-requisitos](expressroute-prerequisites.md), [requisitos de roteamento](expressroute-routing.md), e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.
* Você deve ter um circuito do ExpressRoute ativo. 
  * Siga as instruções de saudação muito[criar um circuito de rota expressa](expressroute-howto-circuit-arm.md) e ter circuito Olá habilitado por seu provedor de conectividade. 
  * Verifique se o emparelhamento privado do Azure está configurado para seu circuito. Consulte Olá [configurar o roteamento](expressroute-howto-routing-arm.md) artigo para obter instruções de roteamentos. 
  * Certifique-se de que o emparelhamento particular do Azure está configurado e Olá emparelhamento via protocolo BGP entre sua rede e a Microsoft está ativo para que você pode habilitar a conectividade de ponta a ponta.
  * Verifique se tem uma rede virtual e um gateway de rede virtual criados e totalmente provisionados. Siga as instruções de saudação muito[criar um gateway de rede virtual para o ExpressRoute](expressroute-howto-add-gateway-resource-manager.md). Um gateway de rede virtual para a rota expressa usa Olá GatewayType 'ExpressRoute', não VPN.

* Você pode vincular o circuito de rota expressa padrão do too10 redes virtuais tooa. Todas as redes virtuais devem estar em Olá mesma região geopolíticas ao usar um circuito de rota expressa padrão. 

* Você pode vincular uma rede virtual fora da região geopolíticas Olá Olá circuito de rota expressa ou conectar-se um grande número de redes virtuais tooyour circuito de rota expressa se você habilitou o complemento do premium Olá rota expressa. Verificar Olá [perguntas frequentes sobre](expressroute-faqs.md) para obter mais detalhes sobre o complemento do premium Olá.


## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Conectar uma rede virtual no hello mesmo circuito de tooa de assinatura
Você pode se conectar a um gateway de rede virtual tooan circuito de rota expressa usando Olá cmdlet a seguir. Verifique se esse gateway de rede virtual Olá é criado e está pronto para vinculação antes de executar o cmdlet hello:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Conectar uma rede virtual em um circuito de tooa assinatura diferente
Você pode compartilhar um circuito do ExpressRoute entre várias assinaturas. Olá figura a seguir mostra um esquemático simples de como funciona o compartilhamento para circuitos ExpressRoute entre várias assinaturas.

Cada uma das nuvens menores de saudação dentro da nuvem grande Olá é toorepresent usadas assinaturas que pertencem a toodifferent departamentos dentro de uma organização. Cada um dos departamentos hello dentro da organização Olá pode usar sua própria assinatura para implantar seus serviços – mas eles podem compartilhar uma única rede rota expressa circuito tooconnect tooyour back local. Um único departamento (neste exemplo: IT) pode ter o circuito de rota expressa hello. Outras assinaturas dentro da organização Olá podem usar o circuito de rota expressa hello.

> [!NOTE]
> Encargos de largura de banda e conectividade para Olá circuito de rota expressa será o proprietário da assinatura toohello aplicado. Todas as redes virtuais compartilham Olá mesma largura de banda.
> 
> 

![Conectividade entre assinaturas](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a>Administração – proprietários e usuários do circuito

Olá 'proprietário do circuito' é um usuário autorizado Power Olá recursos de circuito de rota expressa. proprietário do circuito Olá pode criar autorizações que podem ser trocadas por 'usuários do circuito'. Os usuários do circuito são proprietários da rede virtual gateways que não estão no hello mesma assinatura conforme Olá circuito de rota expressa. Usuários do circuito podem resgatar autorizações (uma autorização por rede virtual).

proprietário do circuito Olá tem autorizações de toomodify e revoke power Olá a qualquer momento. Revogando uma resulta de autorização em todas as conexões de link que está sendo excluídas da assinatura de saudação cujo acesso foi revogado.

### <a name="circuit-owner-operations"></a>Operações do proprietário do circuito

**toocreate uma autorização**

proprietário do circuito Olá cria uma autorização. Isso resulta na criação de saudação de uma chave de autorização que pode ser usado por um tooconnect de usuário do circuito seu gateways de rede virtual toohello circuito de rota expressa. Uma autorização é válida apenas para uma conexão.

Olá trecho a seguir cmdlet mostra como toocreate uma autorização:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


Olá resposta toothis conterá o status e a chave de autorização de saudação:

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



**tooreview autorizações**

proprietário do circuito Olá pode revisar todas as autorizações que são emitidas em um circuito específico executando Olá cmdlet a seguir:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

**tooadd autorizações**

proprietário do circuito Olá pode adicionar autorizações usando Olá cmdlet a seguir:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

**toodelete autorizações**

proprietário do circuito Olá pode revogar/excluir autorizações toohello usuário executando Olá cmdlet a seguir:

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a>Operações do usuário do circuito

usuários do circuito Olá precisa Olá peer ID e uma chave de autorização do proprietário do circuito hello. chave de autorização de saudação é um GUID.

ID de mesmo nível pode ser verificada de saudação comando a seguir:

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

**tooredeem uma autorização de conexão**

usuários do circuito Olá podem executar Olá tooredeem cmdlet a seguir uma autorização de link:

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

**toorelease uma autorização de conexão**

Você pode liberar uma autorização Excluindo conexão Olá que vincula a rede virtual de toohello Olá de circuito ExpressRoute.

## <a name="modify-a-virtual-network-connection"></a>Modificar uma conexão de rede virtual
Você pode atualizar determinadas propriedades de uma conexão de rede virtual. 

**peso de conexão Olá tooupdate**

Sua rede virtual pode ser conectado toomultiple circuitos do ExpressRoute. Você pode receber o mesmo prefixo de saudação de mais de um circuito de rota expressa. toochoose o tráfego de toosend conexão destinado a esse prefixo, você pode alterar *RoutingWeight* de uma conexão. O tráfego será enviado na conexão Olá com hello mais alto *RoutingWeight*.

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

Olá intervalo de *RoutingWeight* é too32000 0. valor padrão de saudação é 0.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre a rota expressa, consulte Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).
