---
title: "Modelos de conectividade de rota expressa: conectar tooMicrosoft Azure por meio de provedores de serviço de rede, trocas e provedores de Ethernet | Microsoft Docs"
description: "Este artigo descreve os diferentes modos de saudação de conectividade entre serviços do Microsoft Azure, Office 365 e Dynamics 365 e de rede do cliente hello. Os clientes podem usar provedores de MPLS, trocas de nuvem e provedores de Ethernet."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2017
ms.author: cherylmc
ms.openlocfilehash: 2682e6e45b2892869068f132bedb4bb08e3f89a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-connectivity-models"></a>Modelos de conectividade do ExpressRoute
Você pode criar uma conexão entre sua rede local e hello nuvem da Microsoft de três maneiras diferentes, [CloudExchange colocalização](#CloudExchange), [ponto a ponto Ethernet Conexão](#Ethernet)e [(IPVPN) para qualquer Conexão](#IPVPN). Os provedores de conectividade podem oferecer um ou mais modelos de conectividade. Você pode trabalhar com o modelo de saudação de toopick provedor de conectividade que funciona melhor para você.
<br><br>

![Diagrama de modelo de conectividade do ExpressRoute](./media/expressroute-connectivity-models/expressroute-connectivity-models-diagram.png)

## <a name="CloudExchange"></a>Colocalizada em uma troca de nuvem
Se você estiver localizada em um recurso com uma troca de nuvem, você pode solicitar conexões cruzadas virtual toohello nuvem da Microsoft por meio do exchange de Ethernet do provedor de colocalização de saudação. Provedores de colocalização podem oferecer conexões cruzadas de camada 2 ou gerenciado camada 3 conexões cruzadas entre a sua infraestrutura na instalação de colocalização de saudação e de nuvem da Microsoft hello.

## <a name="Ethernet"></a>Conexões Ethernet ponto a ponto
Você pode conectar seu data centers/escritórios de local toohello nuvem da Microsoft por meio de links de Ethernet de ponto a ponto. Provedores de Ethernet de ponto a ponto podem oferecer conexões de camada 2 ou gerenciados conexões de camada 3 entre seu site e hello nuvem da Microsoft.

## <a name="IPVPN"></a>Redes Qualquer para Qualquer (IPVPN)
Você pode integrar sua WAN Olá nuvem da Microsoft. Os Provedores de IPVPN (normalmente, VPN MPLS) oferecem conectividade “qualquer para qualquer” entre suas filiais e datacenters. Olá Microsoft nuvem pode ser toomake WAN tooyour interconectadas, ele parecerá assim como qualquer outra filial. Normalmente, os provedores de rede WAN oferecem conectividade gerenciada de Camada 3. Recursos e funcionalidades de rota expressa são todos idênticos em todos os Olá acima modelos de conectividade. 

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre conexões e domínios de roteamento do ExpressRoute. Consulte [Circuitos e domínios de roteamento do ExpressRoute](expressroute-circuit-peerings.md).
* Saiba mais sobre recursos do ExpressRoute. Consulte Olá [visão geral técnica do ExpressRoute](expressroute-introduction.md)
* Encontrar um provedor de serviços. Consulte [Parceiros e locais de emparelhamento do ExpressRoute](expressroute-locations.md).
* Verifique se todos os pré-requisitos foram atendidos. Consulte [Pré-requisitos do ExpressRoute](expressroute-prerequisites.md).
* Consulte os requisitos de toohello para [roteamento](expressroute-routing.md), [NAT](expressroute-nat.md), e [QoS](expressroute-qos.md).
* Configurar sua conexão da Rota Expressa.
  * [Criar um circuito do ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md)
  * [Configurar o roteamento](expressroute-howto-routing-portal-resource-manager.md)
  * [Vincular um circuito de rota expressa do tooan de rede virtual](expressroute-howto-linkvnet-portal-resource-manager.md)
