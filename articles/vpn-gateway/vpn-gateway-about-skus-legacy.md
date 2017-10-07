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
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a><span data-ttu-id="f4fc7-103">Trabalhar com SKUs de gateway de rede virtual (SKUs herdadas)</span><span class="sxs-lookup"><span data-stu-id="f4fc7-103">Working with virtual network gateway SKUs (legacy SKUs)</span></span>

<span data-ttu-id="f4fc7-104">Este artigo contém informações sobre o gateway de rede virtual (antigo) SKUs herdados hello.</span><span class="sxs-lookup"><span data-stu-id="f4fc7-104">This article contains information about hello legacy (old) virtual network gateway SKUs.</span></span> <span data-ttu-id="f4fc7-105">herdado de saudação SKUs ainda funcionam em ambos os modelos de implantação de gateways VPN que já foram criados.</span><span class="sxs-lookup"><span data-stu-id="f4fc7-105">hello legacy SKUs still work in both deployment models for VPN gateways that have already been created.</span></span> <span data-ttu-id="f4fc7-106">Gateways VPN clássicos continuam toouse Olá SKUs herdados, para gateways existentes e para novos gateways.</span><span class="sxs-lookup"><span data-stu-id="f4fc7-106">Classic VPN gateways continue toouse hello legacy SKUs, both for existing gateways, and for new gateways.</span></span> <span data-ttu-id="f4fc7-107">Ao criar o novo Gerenciador de recursos de VPN gateways, use o novo gateway de saudação SKUs.</span><span class="sxs-lookup"><span data-stu-id="f4fc7-107">When creating new Resource Manager VPN gateways, use hello new gateway SKUs.</span></span> <span data-ttu-id="f4fc7-108">Para obter informações sobre Olá novo SKUs, consulte [sobre o Gateway de VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="f4fc7-108">For information about hello new SKUs, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <span data-ttu-id="f4fc7-109"><a name="gwsku"></a>SKUs do Gateway</span><span class="sxs-lookup"><span data-stu-id="f4fc7-109"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <span data-ttu-id="f4fc7-110"><a name="agg"></a>Taxa de transferência agregada estimada por SKU</span><span class="sxs-lookup"><span data-stu-id="f4fc7-110"><a name="agg"></a>Estimated aggregate throughput by SKU</span></span>

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <span data-ttu-id="f4fc7-111"><a name="config"></a>Configurações com suporte pelo tipo de SKU e de VPN</span><span class="sxs-lookup"><span data-stu-id="f4fc7-111"><a name="config"></a>Supported configurations by SKU and VPN type</span></span>

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <span data-ttu-id="f4fc7-112"><a name="resize"></a>Redimensionar um gateway (alterar uma SKU de gateway)</span><span class="sxs-lookup"><span data-stu-id="f4fc7-112"><a name="resize"></a>Resize a gateway (change a gateway SKU)</span></span>

<span data-ttu-id="f4fc7-113">Você pode redimensionar um SKU de gateway em Olá mesma família SKU.</span><span class="sxs-lookup"><span data-stu-id="f4fc7-113">You can resize a gateway SKU within hello same SKU family.</span></span> <span data-ttu-id="f4fc7-114">Por exemplo, se você tiver um SKU padrão, você pode redimensionar tooa HighPerformance SKU.</span><span class="sxs-lookup"><span data-stu-id="f4fc7-114">For example, if you have a Standard SKU, you can resize tooa HighPerformance SKU.</span></span> <span data-ttu-id="f4fc7-115">Você não pode redimensionar o VPN gateways entre Olá SKUs antigos e Olá novas famílias SKU.</span><span class="sxs-lookup"><span data-stu-id="f4fc7-115">You can't resize your VPN gateways between hello old SKUs and hello new SKU families.</span></span> <span data-ttu-id="f4fc7-116">Por exemplo, você não pode ir de um tooa VpnGw2 SKU do SKU padrão.</span><span class="sxs-lookup"><span data-stu-id="f4fc7-116">For example, you can't go from a Standard SKU tooa VpnGw2 SKU.</span></span> 

<span data-ttu-id="f4fc7-117">tooresize um SKU de gateway para o modelo de implantação clássico hello, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f4fc7-117">tooresize a gateway SKU for hello classic deployment model, use hello following command:</span></span>

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

<span data-ttu-id="f4fc7-118">tooresize um SKU de gateway para Olá modelo de implantação do Gerenciador de recursos, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f4fc7-118">tooresize a gateway SKU for hello Resource Manager deployment model, use hello following command:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <span data-ttu-id="f4fc7-119"><a name="migrate"></a>Migrar toohello novo gateway SKUs</span><span class="sxs-lookup"><span data-stu-id="f4fc7-119"><a name="migrate"></a>Migrate toohello new gateway SKUs</span></span>

<span data-ttu-id="f4fc7-120">Se você estiver trabalhando com o modelo de implantação do Gerenciador de recursos de saudação, você pode migrar toohello novo gateway SKUS.</span><span class="sxs-lookup"><span data-stu-id="f4fc7-120">If you are working with hello Resource Manager deployment model, you can migrate toohello new gateway SKUS.</span></span> <span data-ttu-id="f4fc7-121">Se você estiver trabalhando com o modelo de implantação clássico hello, você não pode migrar toohello SKUs novo e, em vez disso, deve continuar toouse Olá SKUs herdados.</span><span class="sxs-lookup"><span data-stu-id="f4fc7-121">If you are working with hello classic deployment model, you can't migrate toohello new SKUs and must instead continue toouse hello legacy SKUs.</span></span>

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a><span data-ttu-id="f4fc7-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f4fc7-122">Next steps</span></span>

<span data-ttu-id="f4fc7-123">Para obter mais informações sobre Olá novo SKUs de Gateway, consulte [SKUs de Gateway](vpn-gateway-about-vpngateways.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="f4fc7-123">For more information about hello new Gateway SKUs, see [Gateway SKUs](vpn-gateway-about-vpngateways.md#gwsku).</span></span>

<span data-ttu-id="f4fc7-124">Para saber mais sobre definições de configuração, veja [Sobre definições de configuração do Gateway de VPN](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="f4fc7-124">For more information about configuration settings, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>