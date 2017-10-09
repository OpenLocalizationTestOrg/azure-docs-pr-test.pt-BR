---
title: 'Vincular um circuito de rota expressa do tooan de rede virtual: CLI: Azure | Microsoft Docs'
description: "Este documento fornece uma visão geral de como toolink virtual redes circuitos de tooExpressRoute (VNets) usando o modelo de implantação do Gerenciador de recursos de saudação e a CLI."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlit
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 1251f016d9b94d3fee81de1df164cb085cbe9d78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-cli"></a>Conecte-se a um circuito de rota expressa do tooan de rede virtual usando a CLI

Este artigo ajuda você a vincular circuitos do ExpressRoute tooAzure redes virtuais (VNets) usando a CLI. toolink usando a CLI do Azure, redes virtuais Olá devem ser criadas usando o modelo de implantação do Gerenciador de recursos de saudação. Eles podem ser em Olá mesma assinatura, ou parte de outra assinatura. Se você quiser toouse tooconnect um método diferente tooan sua rede virtual circuito de rota expressa, você pode selecionar um artigo Olá lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [CLI do Azure](howto-linkvnet-cli.md)
> * [Vídeo – Portal do Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (clássico)](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a>Pré-requisitos de configuração

* Você precisa Olá a versão mais recente do hello interface de linha de comando (CLI). Para obter mais informações, consulte [Instalar a CLI do Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).
* Você precisa Olá tooreview [pré-requisitos](expressroute-prerequisites.md), [requisitos de roteamento](expressroute-routing.md), e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.
* Você deve ter um circuito do ExpressRoute ativo. 
  * Siga as instruções de saudação muito[criar um circuito de rota expressa](howto-circuit-cli.md) e ter circuito Olá habilitado por seu provedor de conectividade. 
  * Verifique se o emparelhamento privado do Azure está configurado para seu circuito. Consulte Olá [configurar o roteamento](howto-routing-cli.md) artigo para obter instruções de roteamentos. 
  * Verifique se o emparelhamento particular do Azure está configurado. Olá emparelhamento via protocolo BGP entre sua rede e da Microsoft deve estar ativos para que você pode habilitar a conectividade de ponta a ponta.
  * Verifique se tem uma rede virtual e um gateway de rede virtual criados e totalmente provisionados. Siga as instruções de saudação muito[configurar um gateway de rede virtual para o ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli). Ser toouse se `--gateway-type ExpressRoute`.

* Você pode vincular o circuito de rota expressa padrão do too10 redes virtuais tooa. Todas as redes virtuais devem estar em Olá mesma região geopolíticas ao usar um circuito de rota expressa padrão. 

* Se você habilitar o complemento do premium Olá rota expressa, você pode vincular uma rede virtual fora da região geopolíticas Olá Olá circuito de rota expressa ou conectar-se um grande número de redes virtuais tooyour circuito de rota expressa. Para obter mais informações sobre o complemento do premium Olá, consulte Olá [perguntas frequentes sobre](expressroute-faqs.md).

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Conectar uma rede virtual no hello mesmo circuito de tooa de assinatura

Você pode se conectar a um circuito de rota expressa de tooan de gateway de rede virtual usando o exemplo hello. Verifique se esse gateway de rede virtual Olá é criado e está pronto para vinculação antes de executar o comando hello.

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Conectar uma rede virtual em um circuito de tooa assinatura diferente

Você pode compartilhar um circuito do ExpressRoute entre várias assinaturas. a Figura Olá abaixo mostra um esquemático simples de como funciona o compartilhamento para circuitos ExpressRoute entre várias assinaturas.

Cada uma das nuvens menores de saudação dentro da nuvem grande Olá é toorepresent usadas assinaturas que pertencem a toodifferent departamentos dentro de uma organização. Cada um dos departamentos hello dentro da organização Olá pode usar sua própria assinatura para implantar seus serviços – mas eles podem compartilhar uma única rede rota expressa circuito tooconnect tooyour back local. Um único departamento (neste exemplo: IT) pode ter o circuito de rota expressa hello. Outras assinaturas dentro da organização Olá podem usar o circuito de rota expressa hello.

> [!NOTE]
> Encargos de largura de banda e conectividade para o circuito dedicado de saudação será aplicado toohello proprietário do circuito de rota expressa. Todas as redes virtuais compartilham Olá mesma largura de banda.
> 
> 

![Conectividade entre assinaturas](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a>Administração – proprietários e usuários do circuito

Olá proprietário do circuito é um usuário autorizado Power Olá recursos de circuito de rota expressa. Olá proprietário do circuito pode criar autorizações que podem ser trocadas por 'Usuários do circuito'. Os usuários do circuito são proprietários da rede virtual gateways que não estão no hello mesma assinatura conforme Olá circuito de rota expressa. Usuários do circuito podem resgatar autorizações (uma autorização por rede virtual).

Olá proprietário do circuito tem autorizações de toomodify e revoke power Olá a qualquer momento. Quando uma autorização é revogada, todas as conexões de link são excluídas da assinatura Olá cujo acesso foi revogado.

### <a name="circuit-owner-operations"></a>Operações do proprietário do circuito

**toocreate uma autorização**

Olá proprietário do circuito cria uma autorização, que cria uma chave de autorização que pode ser usado por um usuário do circuito tooconnect seu gateways de rede virtual toohello circuito de rota expressa. Uma autorização é válida apenas para uma conexão.

Olá mostrado no exemplo a seguir como toocreate uma autorização:

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

resposta de saudação contém o status e a chave de autorização de saudação:

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

**tooreview autorizações**

Olá proprietário do circuito pode revisar todas as autorizações que são emitidas em um circuito específico executando Olá exemplo a seguir:

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

**tooadd autorizações**

Olá proprietário do circuito pode adicionar autorizações usando Olá exemplo a seguir:

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

**toodelete autorizações**

Olá proprietário do circuito pode revogar/excluir autorizações toohello usuário executando Olá exemplo a seguir:

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a>Operações do usuário do circuito

Olá usuários do circuito precisa Olá peer ID e uma chave de autorização do proprietário do circuito de saudação. chave de autorização de saudação é um GUID.

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

**tooredeem uma autorização de conexão**

Olá usuários do circuito pode executar Olá tooredeem de exemplo a seguir uma autorização de link:

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

**toorelease uma autorização de conexão**

Você pode liberar uma autorização Excluindo conexão Olá que vincula a rede virtual de toohello Olá de circuito ExpressRoute.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre a rota expressa, consulte Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).
