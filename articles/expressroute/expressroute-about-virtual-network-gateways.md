---
title: Sobre gateways de rede virtual ExpressRoute | Microsoft Docs
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
ms.openlocfilehash: a6363fa380d0bab05d7500141cc6019d1d3f68b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a><span data-ttu-id="f231c-103">Sobre os gateways de rede virtual para ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f231c-103">About virtual network gateways for ExpressRoute</span></span>
<span data-ttu-id="f231c-104">O gateway de rede virtual é usado para enviar o tráfego de rede entre as redes virtuais do Azure e locais.</span><span class="sxs-lookup"><span data-stu-id="f231c-104">A virtual network gateway is used to send network traffic between Azure virtual networks and on-premises locations.</span></span> <span data-ttu-id="f231c-105">Quando você configura uma conexão ExpressRoute, é necessário criar e configurar um gateway de rede virtual e uma conexão de gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="f231c-105">When you configure an ExpressRoute connection, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

<span data-ttu-id="f231c-106">Quando você cria um gateway de rede virtual, especifica várias configurações.</span><span class="sxs-lookup"><span data-stu-id="f231c-106">When you create a virtual network gateway, you specify several settings.</span></span> <span data-ttu-id="f231c-107">Uma das configurações necessárias especifica se o gateway será usado para tráfego de ExpressRoute ou Tráfego VPN Site a Site.</span><span class="sxs-lookup"><span data-stu-id="f231c-107">One of the required settings specifies whether the gateway will be used for ExpressRoute or Site-to-Site VPN traffic.</span></span> <span data-ttu-id="f231c-108">No modelo de implantação do Resource Manager, a configuração é '-GatewayType'.</span><span class="sxs-lookup"><span data-stu-id="f231c-108">In the Resource Manager deployment model, the setting is '-GatewayType'.</span></span>

<span data-ttu-id="f231c-109">Quando o tráfego de rede é enviado em uma conexão privada, você pode usar o tipo de gateway 'ExpressRoute'.</span><span class="sxs-lookup"><span data-stu-id="f231c-109">When network traffic is sent on a private connection, you use the gateway type 'ExpressRoute'.</span></span> <span data-ttu-id="f231c-110">Isso também é referido como um gateway ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f231c-110">This is also referred to as an ExpressRoute gateway.</span></span> <span data-ttu-id="f231c-111">Quando o tráfego de rede é enviado criptografado na Internet pública, você pode usar o tipo de gateway 'Vpn'.</span><span class="sxs-lookup"><span data-stu-id="f231c-111">When network traffic is sent encrypted across the public Internet, you use the gateway type 'Vpn'.</span></span> <span data-ttu-id="f231c-112">Isso é referido como um gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="f231c-112">This is referred to as a VPN gateway.</span></span> <span data-ttu-id="f231c-113">As conexões Site a Site, Ponto a Site e VNet a VNet usam um gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="f231c-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span></span>

<span data-ttu-id="f231c-114">Cada rede virtual pode ter apenas um gateway de rede virtual por tipo de gateway.</span><span class="sxs-lookup"><span data-stu-id="f231c-114">Each virtual network can have only one virtual network gateway per gateway type.</span></span> <span data-ttu-id="f231c-115">Por exemplo, você pode ter um gateway de rede virtual que usa - GatewayType Vpn, e outro que usa -GatewayType ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f231c-115">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span></span> <span data-ttu-id="f231c-116">Este artigo se concentra no gateway de rede virtual ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f231c-116">This article focuses on the ExpressRoute virtual network gateway.</span></span>

## <span data-ttu-id="f231c-117"><a name="gwsku"></a>SKUs do Gateway</span><span class="sxs-lookup"><span data-stu-id="f231c-117"><a name="gwsku"></a>Gateway SKUs</span></span>
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

<span data-ttu-id="f231c-118">Se quiser atualizar o gateway para um SKU de gateway mais potente, na maioria dos casos, você pode usar o cmdlet do PowerShell 'Resize-AzureRmVirtualNetworkGateway'.</span><span class="sxs-lookup"><span data-stu-id="f231c-118">If you want to upgrade your gateway to a more powerful gateway SKU, in most cases you can use the 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span></span> <span data-ttu-id="f231c-119">Isso funcionará em atualizações para as SKUs Standard e HighPerformance.</span><span class="sxs-lookup"><span data-stu-id="f231c-119">This will work for upgrades to Standard and HighPerformance SKUs.</span></span> <span data-ttu-id="f231c-120">No entanto, para atualizar para a SKU UltraPerformance, você precisará recriar o gateway.</span><span class="sxs-lookup"><span data-stu-id="f231c-120">However, to upgrade to the UltraPerformance SKU, you will need to recreate the gateway.</span></span>

### <span data-ttu-id="f231c-121"><a name="aggthroughput"></a>Taxa de transferência agregada estimada por SKU de gateway</span><span class="sxs-lookup"><span data-stu-id="f231c-121"><a name="aggthroughput"></a>Estimated aggregate throughput by gateway SKU</span></span>
<span data-ttu-id="f231c-122">A tabela a seguir mostra os tipos de gateway e a produtividade agregada estimada.</span><span class="sxs-lookup"><span data-stu-id="f231c-122">The following table shows the gateway types and the estimated aggregate throughput.</span></span> <span data-ttu-id="f231c-123">Esta tabela aplica-se a ambos os modelos de implantação do Gerenciador de Recursos e clássico.</span><span class="sxs-lookup"><span data-stu-id="f231c-123">This table applies to both the Resource Manager and classic deployment models.</span></span>

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="f231c-124">A produtividade do aplicativo depende de vários fatores, como a latência de ponta a ponta e o número de fluxos de tráfego abertos pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f231c-124">Application throughput depends on multiple factors, such as the end-to-end latency, and the number of traffic flows the application opens.</span></span> <span data-ttu-id="f231c-125">Os números na tabela representam o limite superior que o aplicativo, teoricamente, pode atingir em um ambiente ideal.</span><span class="sxs-lookup"><span data-stu-id="f231c-125">The numbers in the table represent the upper limit that the application can theorectically achieve in an ideal environment.</span></span> 
> 
>

## <span data-ttu-id="f231c-126"><a name="resources"></a>Cmdlets do PowerShell e APIs REST</span><span class="sxs-lookup"><span data-stu-id="f231c-126"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="f231c-127">Para obter recursos técnicos adicionais e requisitos de sintaxe específicos ao usar cmdlets do PowerShell e APIs REST para configurações do gateway de rede virtual, veja as páginas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f231c-127">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see the following pages:</span></span>

| <span data-ttu-id="f231c-128">**Clássico**</span><span class="sxs-lookup"><span data-stu-id="f231c-128">**Classic**</span></span> | <span data-ttu-id="f231c-129">**Gerenciador de Recursos**</span><span class="sxs-lookup"><span data-stu-id="f231c-129">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="f231c-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f231c-130">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="f231c-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f231c-131">PowerShell</span></span>](https://msdn.microsoft.com/library/mt163510.aspx) |
| [<span data-ttu-id="f231c-132">API REST</span><span class="sxs-lookup"><span data-stu-id="f231c-132">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="f231c-133">API REST</span><span class="sxs-lookup"><span data-stu-id="f231c-133">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="f231c-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f231c-134">Next steps</span></span>
<span data-ttu-id="f231c-135">Consulte [Visão geral de ExpressRoute](expressroute-introduction.md) para saber mais sobre as configurações de conexão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="f231c-135">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span></span> 

