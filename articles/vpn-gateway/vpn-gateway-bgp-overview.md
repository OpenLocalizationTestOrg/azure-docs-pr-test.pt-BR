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
# <a name="overview-of-bgp-with-azure-vpn-gateways"></a>Visão geral de BGP com Gateways de VPN do Azure
Este artigo fornece uma visão geral do suporte a BGP (Border Gateway Protocol) em Gateways de VPN do Azure.

O BGP é Olá protocolo de roteamento padrão usado em Olá tooexchange roteamento e acessibilidade informações da Internet entre duas ou mais redes. Quando usada no contexto de saudação de redes virtuais do Azure, BGP permite Olá Gateways de VPN do Azure e os dispositivos VPN local, chamados de pares de BGP ou vizinhos, tooexchange "rotas" informará ambos os gateways na disponibilidade de saudação e acessibilidade para aqueles prefixos toogo por meio de gateways de saudação ou roteadores envolvidos. BGP também pode habilitar o roteamento de tráfego entre várias redes propagando rotas aprende um gateway BGP de um tooall de par BGP outros pares de BGP. 

## <a name="why-use-bgp"></a>Por que usar o BGP?
O BGP é um recurso opcional que você pode usar com gateways de VPN Baseados em Rota do Azure. Você também deve verificar se que os dispositivos VPN local oferece suporte ao BGP antes de habilitar o recurso de saudação. Você pode continuar toouse gateways de VPN do Azure e os dispositivos VPN local sem BGP. É Olá equivalente do uso de rotas estáticas (sem BGP) *versus* usando roteamento dinâmico com BGP entre suas redes e o Azure.

Há várias vantagens e novos recursos com o BGP:

### <a name="support-automatic-and-flexible-prefix-updates"></a>Suporte a atualizações prefixo flexíveis e automáticas
Com BGP, você só precisa toodeclare um par de BGP prefixo mínimo tooa específico no túnel de VPN S2S de IPsec hello. Ele pode ser tão pequeno quanto um prefixo de host (/ 32) do hello endereço IP do par BGP de seu dispositivo VPN local. Você pode controlar qual local prefixos de rede que você deseja tooadvertise tooAzure tooallow tooaccess sua rede Virtual do Azure.

Você também pode anunciar prefixos maiores que podem incluir alguns de seus prefixos de endereço de VNet, como um espaço de endereço IP privado grande (por exemplo, 10.0.0.0/8). Observe que os prefixos de saudação não podem ser idênticos com qualquer um dos seus prefixos de rede virtual. Essas rotas tooyour idênticos prefixos de rede virtual serão rejeitados.

### <a name="support-multiple-tunnels-between-a-vnet-and-an-on-premises-site-with-automatic-failover-based-on-bgp"></a>Suporte a vários túneis entre uma VNet e um site local com failover automático com base em BGP
Você pode estabelecer várias conexões entre sua rede virtual do Azure e os dispositivos VPN local no hello mesmo local. Esse recurso fornece vários túneis (caminhos) entre duas redes Olá em uma configuração ativo-ativo. Se um dos túneis Olá estiver desconectado, rotas correspondentes hello serão ser retiradas por meio de BGP e tráfego Olá muda automaticamente túneis restantes toohello.

Olá diagrama a seguir mostra um exemplo simples desta instalação altamente disponível:

![Vários caminhos ativos](./media/vpn-gateway-bgp-overview/multiple-active-tunnels.png)

### <a name="support-transit-routing-between-your-on-premises-networks-and-multiple-azure-vnets"></a>Suporte ao roteamento de trânsito entre as redes locais e várias VNets do Azure
BGP permite que vários toolearn de gateways e propagar os prefixos de redes diferentes, se eles estão direta ou indiretamente conectados. Isso pode habilitar o roteamento de tráfego com gateways de VPN do Azure entre os sites locais ou em várias Redes Virtuais do Azure.

Olá diagrama a seguir mostra um exemplo de uma topologia de vários salto com vários caminhos que podem trânsito de tráfego entre redes de dois locais Olá por meio de gateways de VPN do Azure em Olá Microsoft Networks:

![Trânsito com vários saltos](./media/vpn-gateway-bgp-overview/full-mesh-transit.png)

## <a name="bgp-faq"></a>PERGUNTAS FREQUENTES SOBRE O BGP
[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="next-steps"></a>Próximas etapas
Consulte [guia de Introdução com BGP em gateways de VPN do Azure](vpn-gateway-bgp-resource-manager-ps.md) para etapas tooconfigure BGP para suas conexões de VNet para VNet e entre locais.

