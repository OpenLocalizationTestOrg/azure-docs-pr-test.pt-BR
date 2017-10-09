---
title: aaaOverview de BGP com Gateways de VPN do Azure | Microsoft Docs
description: "Este artigo fornece uma visão geral do BGP com Gateways de VPN do Azure."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: f8c3985c-c128-4f34-835c-0e88742bf36e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/12/2017
ms.author: yushwang
ms.openlocfilehash: ced3f77ecd791c84fb72b96447e839be3bf94846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-bgp-with-azure-vpn-gateways"></a><span data-ttu-id="ac70e-103">Visão geral de BGP com Gateways de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="ac70e-103">Overview of BGP with Azure VPN Gateways</span></span>
<span data-ttu-id="ac70e-104">Este artigo fornece uma visão geral do suporte a BGP (Border Gateway Protocol) em Gateways de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac70e-104">This article provides an overview of BGP (Border Gateway Protocol) support in Azure VPN Gateways.</span></span>

<span data-ttu-id="ac70e-105">O BGP é Olá protocolo de roteamento padrão usado em Olá tooexchange roteamento e acessibilidade informações da Internet entre duas ou mais redes.</span><span class="sxs-lookup"><span data-stu-id="ac70e-105">BGP is hello standard routing protocol commonly used in hello Internet tooexchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="ac70e-106">Quando usada no contexto de saudação de redes virtuais do Azure, BGP permite Olá Gateways de VPN do Azure e os dispositivos VPN local, chamados de pares de BGP ou vizinhos, tooexchange "rotas" informará ambos os gateways na disponibilidade de saudação e acessibilidade para aqueles prefixos toogo por meio de gateways de saudação ou roteadores envolvidos.</span><span class="sxs-lookup"><span data-stu-id="ac70e-106">When used in hello context of Azure Virtual Networks, BGP enables hello Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, tooexchange "routes" that will inform both gateways on hello availability and reachability for those prefixes toogo through hello gateways or routers involved.</span></span> <span data-ttu-id="ac70e-107">BGP também pode habilitar o roteamento de tráfego entre várias redes propagando rotas aprende um gateway BGP de um tooall de par BGP outros pares de BGP.</span><span class="sxs-lookup"><span data-stu-id="ac70e-107">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer tooall other BGP peers.</span></span> 

## <a name="why-use-bgp"></a><span data-ttu-id="ac70e-108">Por que usar o BGP?</span><span class="sxs-lookup"><span data-stu-id="ac70e-108">Why use BGP?</span></span>
<span data-ttu-id="ac70e-109">O BGP é um recurso opcional que você pode usar com gateways de VPN Baseados em Rota do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac70e-109">BGP is an optional feature you can use with Azure Route-Based VPN gateways.</span></span> <span data-ttu-id="ac70e-110">Você também deve verificar se que os dispositivos VPN local oferece suporte ao BGP antes de habilitar o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac70e-110">You should also make sure your on-premises VPN devices support BGP before you enable hello feature.</span></span> <span data-ttu-id="ac70e-111">Você pode continuar toouse gateways de VPN do Azure e os dispositivos VPN local sem BGP.</span><span class="sxs-lookup"><span data-stu-id="ac70e-111">You can continue toouse Azure VPN gateways and your on-premises VPN devices without BGP.</span></span> <span data-ttu-id="ac70e-112">É Olá equivalente do uso de rotas estáticas (sem BGP) *versus* usando roteamento dinâmico com BGP entre suas redes e o Azure.</span><span class="sxs-lookup"><span data-stu-id="ac70e-112">It is hello equivalent of using static routes (without BGP) *vs.* using dynamic routing with BGP between your networks and Azure.</span></span>

<span data-ttu-id="ac70e-113">Há várias vantagens e novos recursos com o BGP:</span><span class="sxs-lookup"><span data-stu-id="ac70e-113">There are several advantages and new capabilities with BGP:</span></span>

### <a name="support-automatic-and-flexible-prefix-updates"></a><span data-ttu-id="ac70e-114">Suporte a atualizações prefixo flexíveis e automáticas</span><span class="sxs-lookup"><span data-stu-id="ac70e-114">Support automatic and flexible prefix updates</span></span>
<span data-ttu-id="ac70e-115">Com BGP, você só precisa toodeclare um par de BGP prefixo mínimo tooa específico no túnel de VPN S2S de IPsec hello.</span><span class="sxs-lookup"><span data-stu-id="ac70e-115">With BGP, you only need toodeclare a minimum prefix tooa specific BGP peer over hello IPsec S2S VPN tunnel.</span></span> <span data-ttu-id="ac70e-116">Ele pode ser tão pequeno quanto um prefixo de host (/ 32) do hello endereço IP do par BGP de seu dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="ac70e-116">It can be as small as a host prefix (/32) of hello BGP peer IP address of your on-premises VPN device.</span></span> <span data-ttu-id="ac70e-117">Você pode controlar qual local prefixos de rede que você deseja tooadvertise tooAzure tooallow tooaccess sua rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac70e-117">You can control which on-premises network prefixes you want tooadvertise tooAzure tooallow your Azure Virtual Network tooaccess.</span></span>

<span data-ttu-id="ac70e-118">Você também pode anunciar prefixos maiores que podem incluir alguns de seus prefixos de endereço de VNet, como um espaço de endereço IP privado grande (por exemplo, 10.0.0.0/8).</span><span class="sxs-lookup"><span data-stu-id="ac70e-118">You can also advertise larger prefixes that may include some of your VNet address prefixes, such as a large private IP address space (for example, 10.0.0.0/8).</span></span> <span data-ttu-id="ac70e-119">Observe que os prefixos de saudação não podem ser idênticos com qualquer um dos seus prefixos de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="ac70e-119">Note though hello prefixes cannot be identical with any one of your VNet prefixes.</span></span> <span data-ttu-id="ac70e-120">Essas rotas tooyour idênticos prefixos de rede virtual serão rejeitados.</span><span class="sxs-lookup"><span data-stu-id="ac70e-120">Those routes identical tooyour VNet prefixes will be rejected.</span></span>

### <a name="support-multiple-tunnels-between-a-vnet-and-an-on-premises-site-with-automatic-failover-based-on-bgp"></a><span data-ttu-id="ac70e-121">Suporte a vários túneis entre uma VNet e um site local com failover automático com base em BGP</span><span class="sxs-lookup"><span data-stu-id="ac70e-121">Support multiple tunnels between a VNet and an on-premises site with automatic failover based on BGP</span></span>
<span data-ttu-id="ac70e-122">Você pode estabelecer várias conexões entre sua rede virtual do Azure e os dispositivos VPN local no hello mesmo local.</span><span class="sxs-lookup"><span data-stu-id="ac70e-122">You can establish multiple connections between your Azure VNet and your on-premises VPN devices in hello same location.</span></span> <span data-ttu-id="ac70e-123">Esse recurso fornece vários túneis (caminhos) entre duas redes Olá em uma configuração ativo-ativo.</span><span class="sxs-lookup"><span data-stu-id="ac70e-123">This capability provides multiple tunnels (paths) between hello two networks in an active-active configuration.</span></span> <span data-ttu-id="ac70e-124">Se um dos túneis Olá estiver desconectado, rotas correspondentes hello serão ser retiradas por meio de BGP e tráfego Olá muda automaticamente túneis restantes toohello.</span><span class="sxs-lookup"><span data-stu-id="ac70e-124">If one of hello tunnels is disconnected, hello corresponding routes will be withdrawn via BGP and hello traffic automatically shifts toohello remaining tunnels.</span></span>

<span data-ttu-id="ac70e-125">Olá diagrama a seguir mostra um exemplo simples desta instalação altamente disponível:</span><span class="sxs-lookup"><span data-stu-id="ac70e-125">hello following diagram shows a simple example of this highly available setup:</span></span>

![Vários caminhos ativos](./media/vpn-gateway-bgp-overview/multiple-active-tunnels.png)

### <a name="support-transit-routing-between-your-on-premises-networks-and-multiple-azure-vnets"></a><span data-ttu-id="ac70e-127">Suporte ao roteamento de trânsito entre as redes locais e várias VNets do Azure</span><span class="sxs-lookup"><span data-stu-id="ac70e-127">Support transit routing between your on-premises networks and multiple Azure VNets</span></span>
<span data-ttu-id="ac70e-128">BGP permite que vários toolearn de gateways e propagar os prefixos de redes diferentes, se eles estão direta ou indiretamente conectados.</span><span class="sxs-lookup"><span data-stu-id="ac70e-128">BGP enables multiple gateways toolearn and propagate prefixes from different networks, whether they are directly or indirectly connected.</span></span> <span data-ttu-id="ac70e-129">Isso pode habilitar o roteamento de tráfego com gateways de VPN do Azure entre os sites locais ou em várias Redes Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac70e-129">This can enable transit routing with Azure VPN gateways between your on-premises sites or across multiple Azure Virtual Networks.</span></span>

<span data-ttu-id="ac70e-130">Olá diagrama a seguir mostra um exemplo de uma topologia de vários salto com vários caminhos que podem trânsito de tráfego entre redes de dois locais Olá por meio de gateways de VPN do Azure em Olá Microsoft Networks:</span><span class="sxs-lookup"><span data-stu-id="ac70e-130">hello following diagram shows an example of a multi-hop topology with multiple paths that can transit traffic between hello two on-premises networks through Azure VPN gateways within hello Microsoft Networks:</span></span>

![Trânsito com vários saltos](./media/vpn-gateway-bgp-overview/full-mesh-transit.png)

## <a name="bgp-faq"></a><span data-ttu-id="ac70e-132">PERGUNTAS FREQUENTES SOBRE O BGP</span><span class="sxs-lookup"><span data-stu-id="ac70e-132">BGP FAQ</span></span>
[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="ac70e-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ac70e-133">Next steps</span></span>
<span data-ttu-id="ac70e-134">Consulte [guia de Introdução com BGP em gateways de VPN do Azure](vpn-gateway-bgp-resource-manager-ps.md) para etapas tooconfigure BGP para suas conexões de VNet para VNet e entre locais.</span><span class="sxs-lookup"><span data-stu-id="ac70e-134">See [Getting started with BGP on Azure VPN gateways](vpn-gateway-bgp-resource-manager-ps.md) for steps tooconfigure BGP for your cross-premises and VNet-to-VNet connections.</span></span>

