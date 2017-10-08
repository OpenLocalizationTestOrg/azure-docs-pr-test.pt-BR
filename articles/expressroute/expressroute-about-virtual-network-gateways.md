---
title: gateways de rede virtual de rota expressa aaaAbout | Microsoft Docs
description: Saiba mais sobre os gateways de rede virtual para ExpressRoute.
services: expressroute
documentationcenter: na
author: cherylmc
manager: carmonm
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: 7e0d9658-bc00-45b0-848f-f7a6da648635
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: cherylmc
ms.openlocfilehash: 4daf4f96b4fadb00683d8e536e51734853008c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a><span data-ttu-id="96f13-103">Sobre os gateways de rede virtual para ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="96f13-103">About virtual network gateways for ExpressRoute</span></span>
<span data-ttu-id="96f13-104">Um gateway de rede virtual é usado toosend o tráfego de rede entre redes virtuais do Azure e locais de local.</span><span class="sxs-lookup"><span data-stu-id="96f13-104">A virtual network gateway is used toosend network traffic between Azure virtual networks and on-premises locations.</span></span> <span data-ttu-id="96f13-105">Quando você configura uma conexão ExpressRoute, é necessário criar e configurar um gateway de rede virtual e uma conexão de gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="96f13-105">When you configure an ExpressRoute connection, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

<span data-ttu-id="96f13-106">Quando você cria um gateway de rede virtual, especifica várias configurações.</span><span class="sxs-lookup"><span data-stu-id="96f13-106">When you create a virtual network gateway, you specify several settings.</span></span> <span data-ttu-id="96f13-107">Uma das configurações necessárias de saudação especifica se o gateway de saudação será usado para o tráfego de rota expressa ou VPN Site a Site.</span><span class="sxs-lookup"><span data-stu-id="96f13-107">One of hello required settings specifies whether hello gateway will be used for ExpressRoute or Site-to-Site VPN traffic.</span></span> <span data-ttu-id="96f13-108">No modelo de implantação do Gerenciador de recursos de hello, configuração de saudação for '-GatewayType'.</span><span class="sxs-lookup"><span data-stu-id="96f13-108">In hello Resource Manager deployment model, hello setting is '-GatewayType'.</span></span>

<span data-ttu-id="96f13-109">Quando o tráfego de rede é enviado em uma conexão privada, use o tipo de gateway de saudação 'ExpressRoute'.</span><span class="sxs-lookup"><span data-stu-id="96f13-109">When network traffic is sent on a private connection, you use hello gateway type 'ExpressRoute'.</span></span> <span data-ttu-id="96f13-110">Isso também é chamado tooas um gateway de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="96f13-110">This is also referred tooas an ExpressRoute gateway.</span></span> <span data-ttu-id="96f13-111">Quando o tráfego é enviado criptografado em Olá Internet pública, use o tipo de gateway Olá 'Vpn'.</span><span class="sxs-lookup"><span data-stu-id="96f13-111">When network traffic is sent encrypted across hello public Internet, you use hello gateway type 'Vpn'.</span></span> <span data-ttu-id="96f13-112">Isso é chamado tooas um gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="96f13-112">This is referred tooas a VPN gateway.</span></span> <span data-ttu-id="96f13-113">As conexões Site a Site, Ponto a Site e VNet a VNet usam um gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="96f13-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span></span>

<span data-ttu-id="96f13-114">Cada rede virtual pode ter apenas um gateway de rede virtual por tipo de gateway.</span><span class="sxs-lookup"><span data-stu-id="96f13-114">Each virtual network can have only one virtual network gateway per gateway type.</span></span> <span data-ttu-id="96f13-115">Por exemplo, você pode ter um gateway de rede virtual que usa - GatewayType Vpn, e outro que usa -GatewayType ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="96f13-115">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span></span> <span data-ttu-id="96f13-116">Este artigo se concentra no gateway de rede virtual de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="96f13-116">This article focuses on hello ExpressRoute virtual network gateway.</span></span>

## <span data-ttu-id="96f13-117"><a name="gwsku"></a>SKUs do Gateway</span><span class="sxs-lookup"><span data-stu-id="96f13-117"><a name="gwsku"></a>Gateway SKUs</span></span>
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

<span data-ttu-id="96f13-118">Se você quiser tooupgrade tooa seu gateway mais poderoso gateway SKU, na maioria dos casos, você pode usar Olá cmdlet do PowerShell 'Redimensionamento AzureRmVirtualNetworkGateway'.</span><span class="sxs-lookup"><span data-stu-id="96f13-118">If you want tooupgrade your gateway tooa more powerful gateway SKU, in most cases you can use hello 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span></span> <span data-ttu-id="96f13-119">Isso funcionará para atualizações tooStandard e SKUs de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="96f13-119">This will work for upgrades tooStandard and HighPerformance SKUs.</span></span> <span data-ttu-id="96f13-120">No entanto, tooupgrade toohello UltraPerformance SKU, você precisará de gateway de saudação toorecreate.</span><span class="sxs-lookup"><span data-stu-id="96f13-120">However, tooupgrade toohello UltraPerformance SKU, you will need toorecreate hello gateway.</span></span>

### <span data-ttu-id="96f13-121"><a name="aggthroughput"></a>Taxa de transferência agregada estimada por SKU de gateway</span><span class="sxs-lookup"><span data-stu-id="96f13-121"><a name="aggthroughput"></a>Estimated aggregate throughput by gateway SKU</span></span>
<span data-ttu-id="96f13-122">Olá tabela a seguir mostra os tipos de gateway hello e Olá estimado taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="96f13-122">hello following table shows hello gateway types and hello estimated aggregate throughput.</span></span> <span data-ttu-id="96f13-123">Esta tabela se aplica a saudação tooboth Gerenciador de recursos e modelos de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="96f13-123">This table applies tooboth hello Resource Manager and classic deployment models.</span></span>

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="96f13-124">Taxa de transferência de aplicativos depende de vários fatores, como latência de ponta a ponta Olá, e o número de saudação do tráfego de flui Olá aplicativo aberto.</span><span class="sxs-lookup"><span data-stu-id="96f13-124">Application throughput depends on multiple factors, such as hello end-to-end latency, and hello number of traffic flows hello application opens.</span></span> <span data-ttu-id="96f13-125">obtêm números Olá Olá tabela representam Olá limite superior que o aplicativo hello pode theorectically em um ambiente ideal.</span><span class="sxs-lookup"><span data-stu-id="96f13-125">hello numbers in hello table represent hello upper limit that hello application can theorectically achieve in an ideal environment.</span></span> 
> 
>

## <span data-ttu-id="96f13-126"><a name="resources"></a>Cmdlets do PowerShell e APIs REST</span><span class="sxs-lookup"><span data-stu-id="96f13-126"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="96f13-127">Para obter recursos técnicos adicionais e requisitos de sintaxe específica ao usar APIs REST e cmdlets do PowerShell para configurações de gateway de rede virtual, consulte Olá páginas a seguir:</span><span class="sxs-lookup"><span data-stu-id="96f13-127">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see hello following pages:</span></span>

| <span data-ttu-id="96f13-128">**Clássico**</span><span class="sxs-lookup"><span data-stu-id="96f13-128">**Classic**</span></span> | <span data-ttu-id="96f13-129">**Gerenciador de Recursos**</span><span class="sxs-lookup"><span data-stu-id="96f13-129">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="96f13-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="96f13-130">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="96f13-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="96f13-131">PowerShell</span></span>](https://msdn.microsoft.com/library/mt163510.aspx) |
| [<span data-ttu-id="96f13-132">API REST</span><span class="sxs-lookup"><span data-stu-id="96f13-132">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="96f13-133">API REST</span><span class="sxs-lookup"><span data-stu-id="96f13-133">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="96f13-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="96f13-134">Next steps</span></span>
<span data-ttu-id="96f13-135">Consulte [Visão geral de ExpressRoute](expressroute-introduction.md) para saber mais sobre as configurações de conexão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="96f13-135">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span></span> 

