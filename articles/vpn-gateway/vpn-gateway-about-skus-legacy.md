---
title: gateway de rede virtual do Azure aaaLegacy SKUs | Microsoft Docs
description: SKUs de gateway de rede virtual anteriores.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 710417581423d2fbc62827cab7949f2e137c5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a>Trabalhar com SKUs de gateway de rede virtual (SKUs herdadas)

Este artigo contém informações sobre o gateway de rede virtual (antigo) SKUs herdados hello. herdado de saudação SKUs ainda funcionam em ambos os modelos de implantação de gateways VPN que já foram criados. Gateways VPN clássicos continuam toouse Olá SKUs herdados, para gateways existentes e para novos gateways. Ao criar o novo Gerenciador de recursos de VPN gateways, use o novo gateway de saudação SKUs. Para obter informações sobre Olá novo SKUs, consulte [sobre o Gateway de VPN](vpn-gateway-about-vpngateways.md).

## <a name="gwsku"></a>SKUs do Gateway

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <a name="agg"></a>Taxa de transferência agregada estimada por SKU

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <a name="config"></a>Configurações com suporte pelo tipo de SKU e de VPN

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <a name="resize"></a>Redimensionar um gateway (alterar uma SKU de gateway)

Você pode redimensionar um SKU de gateway em Olá mesma família SKU. Por exemplo, se você tiver um SKU padrão, você pode redimensionar tooa HighPerformance SKU. Você não pode redimensionar o VPN gateways entre Olá SKUs antigos e Olá novas famílias SKU. Por exemplo, você não pode ir de um tooa VpnGw2 SKU do SKU padrão. 

tooresize um SKU de gateway para o modelo de implantação clássico hello, use Olá comando a seguir:

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

tooresize um SKU de gateway para Olá modelo de implantação do Gerenciador de recursos, use Olá comando a seguir:

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="migrate"></a>Migrar toohello novo gateway SKUs

Se você estiver trabalhando com o modelo de implantação do Gerenciador de recursos de saudação, você pode migrar toohello novo gateway SKUS. Se você estiver trabalhando com o modelo de implantação clássico hello, você não pode migrar toohello SKUs novo e, em vez disso, deve continuar toouse Olá SKUs herdados.

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá novo SKUs de Gateway, consulte [SKUs de Gateway](vpn-gateway-about-vpngateways.md#gwsku).

Para saber mais sobre definições de configuração, veja [Sobre definições de configuração do Gateway de VPN](vpn-gateway-about-vpn-gateway-settings.md).