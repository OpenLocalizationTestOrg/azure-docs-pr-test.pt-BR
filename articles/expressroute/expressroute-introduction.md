---
title: "Visão geral de rota expressa: Estender sua tooAzure de rede local através de uma conexão privada | Microsoft Docs"
description: "Esta visão geral técnica de rota expressa explica como uma conexão de rota expressa funciona tooextend seu tooAzure de rede local por uma conexão privada."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: fd95dcd5-df1d-41d6-85dd-e91d0091af05
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 01301e1205c12ecdab34dc9d9b92bc7489e7826c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-overview"></a>Visão geral do ExpressRoute
O Microsoft Azure ExpressRoute permite estender suas redes locais no hello nuvem da Microsoft em uma conexão privada facilitada por um provedor de conectividade. Com o ExpressRoute, você pode estabelecer serviços de nuvem de tooMicrosoft de conexões, como o Microsoft Azure, Office 365 e Dynamics 365.

A conectividade pode ocorrer de uma rede “qualquer para qualquer” (VPN IP), uma rede Ethernet ponto a ponto ou uma conexão cruzada virtual por meio de um provedor de conectividade em uma colocalização. Conexões de rota expressa não passam pela Olá Internet pública. Isso permite toooffer de conexões de rota expressa mais confiabilidade, velocidades mais rápidas, latências menores e maior segurança que as conexões típicas pela Internet da saudação. Para obter informações sobre como tooconnect seu tooMicrosoft de rede usando o ExpressRoute, consulte [modelos de conectividade de rota expressa](expressroute-connectivity-models.md).

![](./media/expressroute-introduction/expressroute-connection-overview.png)

## <a name="key-benefits"></a>Principais benefícios

* Conectividade de camada 3 entre sua rede local e Olá Microsoft Cloud através de um provedor de conectividade. A conectividade pode ocorrer de uma rede “qualquer para qualquer” (IPVPN), de uma conexão Ethernet ponto a ponto ou por meio de uma conexão cruzada virtual via troca Ethernet.
* Serviços de nuvem tooMicrosoft de conectividade em todas as regiões na região geopolíticas hello.
* Serviços de tooMicrosoft conectividade global em todas as regiões com complemento premium de rota expressa.
* Roteamento dinâmico entre sua rede e a Microsoft por meio de protocolos padrão da indústria (BGP).
* Redundância interna em cada local de emparelhamento para proporcionar maior confiabilidade.
* [SLA](https://azure.microsoft.com/support/legal/sla/)do tempo de atividade da conexão.
* Suporte a QoS para Skype for Business.

Para obter mais informações, consulte Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).

## <a name="features"></a>Recursos

### <a name="layer-3-connectivity"></a>Conectividade de Camada 3
Microsoft usa setor padrão dinâmico roteamento protocol (BGP) tooexchange rotas entre sua rede local, suas instâncias no Azure e a Microsoft endereços públicos.  Estabelecemos várias sessões BGP com sua rede para perfis de tráfego diferentes. Mais detalhes podem ser encontrados no hello [ExpressRoute circuito e domínios de roteamento](expressroute-circuit-peerings.md) artigo.

### <a name="redundancy"></a>Redundância
Cada circuito de rota expressa consiste em duas conexões tootwo Microsoft Enterprise edge roteadores (MSEEs) do provedor de conectividade Olá / sua borda da rede. A Microsoft exige dupla conexão BGP do provedor de conectividade de saudação / seu lado – um tooeach MSEE. Você pode escolher não toodeploy dispositivos redundantes / Ethernet circuitos seu final. No entanto, os provedores de conectividade usam tooensure dispositivos redundantes que as conexões são entregues tooMicrosoft de maneira redundante. Uma configuração de conectividade de camada 3 redundante é um requisito para nosso [SLA](https://azure.microsoft.com/support/legal/sla/) toobe válido.

### <a name="connectivity-toomicrosoft-cloud-services"></a>Serviços de nuvem tooMicrosoft conectividade
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

Conexões de rota expressa habilitar acesso toohello serviços a seguir:

* Serviços do Microsoft Azure
* Serviços do Microsoft Office 365
* Microsoft Dynamics 365

Você pode visitar Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md) página para obter uma lista detalhada dos serviços com suporte por meio do ExpressRoute.

### <a name="connectivity-tooall-regions-within-a-geopolitical-region"></a>Regiões de tooall de conectividade dentro de uma região geopolíticas
Você pode se conectar tooMicrosoft em um dos nossos [locais de emparelhamento](expressroute-locations.md) e ter acesso tooall regiões dentro de região geopolíticas hello. 

Por exemplo, se você conectou tooMicrosoft em Amsterdã por meio de rota expressa, você tem serviços de nuvem do acesso tooall Microsoft hospedados na Europa Norte e Europa Ocidental. Consulte Olá [ExpressRoute locais de emparelhamento e parceiros](expressroute-locations.md) artigo para uma visão geral de regiões geopolíticas hello, regiões de nuvem Microsoft associados e locais de emparelhamento de rota expressa correspondentes.

### <a name="global-connectivity-with-expressroute-premium-add-on"></a>Conectividade global com o complemento premium do ExpressRoute
Você pode habilitar a conectividade do hello rota expressa premium complemento recurso tooextend limites geopolíticas. Por exemplo, se você estiver conectado tooMicrosoft em Amsterdã por meio de rota expressa, você terá hospedados em todas as regiões em Olá, mundo dos serviços de nuvem de Microsoft access tooall (national nuvens são excluídos). Você pode acessar serviços implantados na América do Sul ou Austrália Olá Olá a mesma forma que o Norte e regiões da Europa Ocidental.

### <a name="rich-connectivity-partner-ecosystem"></a>Ecossistema abundante de parceiros de conectividade
O ExpressRoute tem um ecossistema de provedores de conectividade e parceiros de SI em constante crescimento. Você pode consultar toohello [ExpressRoute provedores e locais](expressroute-locations.md) artigo para obter informações mais recentes de saudação.

### <a name="connectivity-toonational-clouds"></a>Nuvens de toonational de conectividade
A Microsoft opera ambientes de nuvem isolados para regiões geopolíticas e segmentos de clientes especiais. Consulte toohello [ExpressRoute provedores e locais](expressroute-locations.md) página para obter uma lista de nuvens nacionais e provedores.

### <a name="bandwidth-options"></a>Opções de largura de banda
É possível comprar circuitos do ExpressRoute para várias larguras de banda. As larguras de banda com suporte estão listadas abaixo. Ser toocheck-se com sua lista de saudação conectividade provedor toodetermine de larguras de banda suportadas que eles fornecem.

* 50 Mbps
* 100 Mbps
* 200 Mbps
* 500 Mbps
* 1 Gbps
* 2 Gbps
* 5 Gbps
* 10 Gbps

### <a name="dynamic-scaling-of-bandwidth"></a>Dimensionamento dinâmico de largura de banda
Você pode aumentar a largura de banda do circuito de rota expressa de saudação (no melhor esforço) sem a necessidade de tootear para baixo de suas conexões. 

### <a name="flexible-billing-models"></a>Modelos flexíveis de cobrança
Escolha o modelo de cobrança que funcione melhor para você. Escolha entre os modelos de cobrança Olá listados abaixo. Para obter mais informações, consulte Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).

* **Dados ilimitados**. Olá circuito de rota expressa é cobrado com base em uma taxa mensal e todas as transferências de dados de entrada e saída é incluída gratuitamente. 
* **Dados limitados**. Olá circuito de rota expressa é cobrado com base em uma taxa mensal. Todas as transferências de dados de entrada são gratuitas. A cobrança pelas transferências de dados de saída ocorrem de acordo com a quantidade de GB da transferência de dados. As taxas de transferência de dados variam de acordo com a região.
* **Complemento ExpressRoute premium**. premium de rota expressa Olá é um complemento Olá circuito de rota expressa. complemento do premium Olá rota expressa fornece Olá recursos a seguir: 
  * Limites de aumento de rota para pública e o Azure emparelhamento particular do Azure de 4.000 too10 de rotas, rotas, 000.
  * Conectividade global para serviços. Um circuito de rota expressa criado em qualquer região (excluindo as nuvens nacionais) terá acesso tooresources em qualquer outra região Olá, mundo. Por exemplo, uma rede virtual criada na Europa Ocidental pode ser acessada por meio de um circuito do ExpressRoute provisionado no Vale do Silício.
  * Aumento do número de links de rede virtual por circuito de rota expressa do limite de maior tooa 10, dependendo da largura de banda de saudação do circuito hello.

## <a name="faq"></a>Perguntas frequentes

Para perguntas frequentes sobre a rota expressa, consulte Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).

## <a name="next-steps"></a>Próximas etapas

* Saiba mais sobre [Modelos de conectividade do ExpressRoute](expressroute-connectivity-models.md).
* Saiba mais sobre conexões e domínios de roteamento do ExpressRoute. Consulte [Circuitos e domínios de roteamento do ExpressRoute](expressroute-circuit-peerings.md).
* Encontrar um provedor de serviços. Consulte [Parceiros e locais de emparelhamento do ExpressRoute](expressroute-locations.md).
* Verifique se todos os pré-requisitos foram atendidos. Consulte [Pré-requisitos do ExpressRoute](expressroute-prerequisites.md).
* Consulte os requisitos de toohello para [roteamento](expressroute-routing.md), [NAT](expressroute-nat.md), e [QoS](expressroute-qos.md).
* Configurar sua conexão da Rota Expressa.
  * [Criar um circuito do ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md)
  * [Configurar o emparelhamento para um circuito do ExpressRoute](expressroute-howto-routing-portal-resource-manager.md)
  * [Conectar uma rede virtual de tooan circuito de rota expressa](expressroute-howto-linkvnet-portal-resource-manager.md)
* Saiba mais sobre alguns dos Olá outra chave [recursos de rede](../networking/networking-overview.md) do Azure.
