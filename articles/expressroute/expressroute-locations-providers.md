---
title: 'Locais e provedores de conectividade: Azure ExpressRoute | Microsoft Docs'
description: "Este artigo fornece uma visão geral detalhada dos locais em que são oferecidos serviços e como tooconnect tooAzure regiões. Classificado por local."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
ms.assetid: feb67da3-5abc-4acb-bad4-f78e3c541ded
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2017
ms.author: kaanan
ms.openlocfilehash: 838d52701d177aa7f13e845b7bde66d07b5efed6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-partners-and-peering-locations"></a>Locais de emparelhamento e parceiros do ExpressRoute

> [!div class="op_single_selector"]
> * [Locais por provedor](expressroute-locations.md)
> * [Provedores por local](expressroute-locations-providers.md)


tabelas de saudação neste artigo fornecem informações sobre a rota expressa provedores de conectividade, cobertura geográfica de rota expressa, serviços de nuvem da Microsoft com suporte pela rota expressa e integradores de sistema de rota expressa (SIs).

## <a name="partners">
            </a>Provedores de conectividade do ExpressRoute
Há suporte para o ExpressRoute em todos os locais e regiões do Azure. Olá mapa a seguir fornece uma lista de regiões do Azure e locais de rota expressa. Locais de rota expressa consulte toothose onde Microsoft correspondentes com vários provedores de serviço.

![Mapa de localização][0]

Você terá acesso tooAzure serviços em todas as regiões dentro de uma região geopolíticas se conectado tooat menos um local de rota expressa na região geopolíticas hello. 

### <a name="azure-regions-tooexpressroute-locations-within-a-geopolitical-region"></a>Locais de tooExpressRoute regiões do Azure dentro de uma região geopolíticas
Olá, a tabela a seguir fornece um mapa das regiões do Azure tooExpressRoute locais dentro de uma região geopolíticas.

| **Região Geopolítica** | **Regiões do Azure** | **Locais de ExpressRoute** |
| --- | --- | --- |
| **América do Norte** |Leste dos EUA, Oeste dos EUA, Leste dos EUA 2, Oeste dos EUA 2, Centro dos EUA, Centro-Sul dos EUA, Centro-Norte dos EUA, Centro-Oeste dos EUA, Centro do Canadá, Leste do Canadá |Atlanta, Chicago, Dallas, Denver+, Las Vegas, Los Angeles, Miami, Nova York, San Antonio, Seattle, Vale do Silício, Washington D.C., Montreal, Cidade de Quebec, Toronto |
| **América do Sul** |Sul do Brasil |São Paulo |
| **Europa** |Europa Setentrional, Europa Ocidental, Oeste do Reino Unido, Sul do Reino Unido |Amsterdã, Dublin, Londres, Newport(Gales), Paris |
| **Ásia** |Ásia Oriental, Sudeste Asiático |Hong Kong, Cingapura |
| **Japão** |Oeste do Japão, Leste do Japão |Osaka, Tóquio |
| **Austrália** |Sudeste da Austrália, Leste da Austrália |Melbourne, Sydney |
| **Índia** |Oeste da Índia, Índia Central, Sul da Índia |Chennai, Mumbai |
| **Coreia do Sul** |Coreia Central, Sul da Coreia |Busan, Seul |

### <a name="regions-and-geopolitical-boundaries-for-national-clouds"></a>Regiões e limites geopolíticos para nuvens nacionais
tabela de saudação abaixo fornece informações sobre regiões e limites geopolíticos para nuvens nacionais.

| **Região Geopolítica** | **Regiões do Azure** | **Locais de ExpressRoute** |
| --- | --- | --- |
| **Nuvem do Governo dos EUA** |Gov. EUA - Iowa, Gov. EUA - Virgínia, US DoD Central, US DoD Leste  |Chicago, Dallas, Nova Iorque, Seattle, Vale do Silício, Washington D.C. |
| **China** |Norte da China, Leste da China |Pequim, Xangai |
| **Alemanha** |Alemanha Central, Alemanha Oriental |Berlim+, Frankfurt |

Não há suporte para conectividade entre regiões geopolíticas padrão Olá ExpressRoute SKU. Você precisará tooenable Olá rota expressa premium complemento toosupport conectividade global. Não há suporte para ambientes de nuvem toonational de conectividade. Você pode trabalhar com seu provedor de conectividade se surgir necessidade de fazê-lo.

## <a name="locations"></a>Locais de provedor de conectividade

Olá tabela a seguir mostra hello e locais de conectividade provedores de serviço para cada local. Se você quiser tooview provedores de serviços e locais de saudação para o qual eles podem fornecer o serviço, consulte [locais pelo provedor de serviços](expressroute-locations.md#locations). 


### <a name="production-azure"></a>Produção do Azure
| **Localidade** | **Provedores de Serviço** |
| --- | --- |
| **Amsterdã** |Aryaka Networks, AT&T NetBond, British Telecom, Colt, Equinix, euNetworks, GÉANT, InterCloud, Internet Solutions - Cloud Connect, Interxion, KPN, Level 3 Communications, Megaport, Orange, Tata Communications, TeleCity Group, Telefonica+, Telenor, Verizon, Zayo Group |
| **Atlanta** |Equinix |
| **Busan** |LG CNS |
| **Chennai** | Airtel+, Global CloudXchange (GCX), SIFY, Tata Communications |
| **Chicago** |AT&T NetBond, Comcast, Equinix, Level 3 Communications, Megaport, Verizon, Zayo Group |
| **Dallas** |Aryaka Networks, AT&T NetBond, Cologix, Equinix, Level 3 Communications, Megaport, Verizon, Zayo Group+ |
| **Denver** |CoreSite |
| **Dublim** |Colt, Interxion, Telecity Group |
| **Hong Kong** |Aryaka Networks, British Telecom, China Telecom Global, Equinix, Megaport, Orange, PCCW Global Limited, Tata Communications, Verizon |
| **Las Vegas** |Level 3 Communications, Megaport |
| **Londres** |AT&T NetBond, British Telecom, Colt, Equinix, InterCloud, Internet Solutions - Cloud Connect, Interxion, Jisc, Level 3 Communications, Megaport, MTN, NTT Communications, Orange, Tata Communications, Telecity Group, Telehouse - KDDI, Telenor, Verizon, Vodafone, Zayo Group+ |
| **Los Angeles** |CoreSite, Equinix, Megaport, NTT, Zayo Group |
| **Melbourne** |AARNet, Equinix, Megaport, NEXTDC, Telstra Corporation |
| **Miami** |C3ntro+, Megaport, Neutrona Networks |
| **Montreal** |Bell Canada, Cologix |
| **Mumbai** |Airtel+, Sify, Tata Communications |
| **Nova Iorque** |Coresite, Equinix, Megaport, Zayo Group |
| **Newport (País de Gales)** |Dados da Próxima Geração |
| **Osaka** |Equinix, Internet Initiative Japan Inc. - IIJ, NTT Communications, NTT SmartConnect, Softbank |
| **Paris** |Colt, Interxion, Equinix, Orange |
| **Cidade de Quebec** | Megaport |
| **San Antonio** |Megaport |
| **São Paulo** |Ascenty Data Centers+, Equinix, Level 3 Communications, Neutrona Networks, Telefonica, UOLDIVEO |
| **Seattle** |Equinix, Level 3 Communications, Megaport |
| **Seul** |KINX, LG CNS, Sejong Telecom |
| **Vale do Silício** |Aryaka Networks, AT&T NetBond, British Telecom, CenturyLink+, Comcast, Console, Equinix, Level 3 Communications, Megaport, Orange, Tata Communications, Verizon, Zayo Group |
| **Cingapura** |Aryaka Networks, AT&T NetBond, British Telecom, Equinix, InterCloud, Level 3 Communications, Megaport, NTT Communications, Orange, SingTel, Tata Communications, Verizon |
| **Sydney** |AARNet, AT&T NetBond, British Telecom, Equinix, Megaport, NEXTDC, Orange, Telstra Corporation, Verizon |
| **Tóquio** |Aryaka Networks, AT&T NetBond, British Telecom, Colt, Equinix, Internet Initiative Japan Inc. - IIJ, NTT Communications, Softbank, Verizon |
| **Toronto** |AT&T NetBond, Bell Canada, Cologix, Console, Equinix, Megaport, Telus, Zayo Group |
| **Washington, D.C.** |Aryaka Networks, AT&T NetBond, British Telecom, Comcast, Equinix, InterCloud, Level 3 Communications, Megaport, NTT Communications, Orange, Tata Communications, Verizon, Zayo Group |

 **+** indica que haverá em breve

### <a name="national-cloud-environments"></a>Ambientes de nuvem nacionais

### <a name="us-government-cloud"></a>Nuvem do Governo dos EUA
| **Localidade** | **Provedores de Serviço** |
| --- | --- |
| **Chicago** |AT&T NetBond, Equinix, Level 3 Communications, Verizon |
| **Dallas** |Equinix, Megaport, Verizon |
| **Nova Iorque** |Equinix, Level 3 Communications+, Verizon |
| **Vale do Silício** | Equinix, Level 3 Communications |
| **Seattle** | Equinix |
| **Washington, D.C.** |AT&T NetBond, Equinix, Level 3 Communications, Verizon |

### <a name="china"></a>China
| **Localidade** | **Provedores de Serviço** |
| --- | --- |
| **Pequim** |China Telecom |
| **Xangai** |China Telecom |

toolearn mais, consulte [rota expressa na China](http://www.windowsazure.cn/home/features/expressroute/)

### <a name="germany"></a>Alemanha
| **Localidade** | **Provedores de Serviço** |
| --- | --- |
| **Berlim** |Colt+, e-shelter, Megaport+, T-Systems |
| **Frankfurt** |Colt, Equinix, Interxion |

## <a name="c1partners"></a>Conectividade por meio de outros provedores do Exchange
Se seu provedor de conectividade não estiver listado em seções anteriores, você ainda pode criar uma conexão.

* Verifique com seu toosee do provedor de conectividade se eles estiverem conectado tooany trocas de saudação na tabela de saudação acima. Você pode verificar o seguinte Olá links toogather obter mais informações sobre os serviços oferecidos pelos provedores do exchange. Vários provedores de conectividade já estão conectados tooEthernet trocas.
  * [Cologix](http://www.cologix.com/)
  * [Console](https://www.consoleconnect.com/partners/cloudsaas/)
  * [CoreSite](http://www.coresite.com/)
  * [Equinix Cloud Exchange](http://www.equinix.com/services/interconnection-connectivity/cloud-exchange/)
  * [InterXion](http://www.interxion.com/)
  * [NextDC](http://www.nextdc.com/)
  * [Megaport](https://www.megaport.com/services/microsoft-expressroute/)
  * [TeleCity CloudIX](http://www.telecitygroup.com/colocation-services/cloud-ix.htm)
* Ter seu provedor de conectividade para estender sua rede toohello local do emparelhamento escolha.
  * Certifique-se de que seu provedor de conectividade estenda sua conectividade de maneira altamente disponível para que não exista nenhum ponto de falha.
* Solicite um circuito de rota expressa com o exchange hello como seu provedor de conectividade tooconnect tooMicrosoft.
  * Siga as etapas [criar um circuito de rota expressa](expressroute-howto-circuit-classic.md) tooset a conectividade.

## <a name="c1partners"></a>Conectividade por meio de provedores de serviço adicionais
| **Localidade** | **Exchange** | **Provedores de conectividade** |
| --- | --- | --- |
| **Amsterdã** | Equinix, Telecity | Eurofiber , Fastweb S.p.A, Nianet |
| **Chicago** | Equinix | Lightower, Windstream |
| **Dallas** | Equinix, Megaport | C3ntro Telecom, Cox Business, Data Foundry, Transtelco |
| **Frankfurt** | Telecity | Nianet, QSC AG |
| **Hong Kong** | Equinix | Macroview Telecom |
| **Londres** | Equinix, euNetworks, Telecity | Bezeq International Ltd., Epsilon, Exponential E, HSO, NexGen Networks, Tamares Telecom, Zain |
| **Los Angeles** | Equinix |Transtelco |
| **Madrid** | Level3 | Zertia |
| **Montreal** | Cologix, Equinix | Airgate Technologies. Inc, Cogeco Peer 1, Rogers, Zirro |
| **Nova Iorque** |Equinix, Megaport | Altice Business, Lightower, Webair |
| **Seattle** |Equinix | Alaska Communications |
| **Vale do Silício** |Equinix | Cox Business, Windstream |
| **Cingapura** |Equinix |1CLOUDSTAR, Epsilon Telecommunications Limited, LGA Telecom, United Information Highway (UIH) |
| **Slough** | Equinix | HSO|
| **Sydney** | Megaport | Macquarie Telecom Group|
| **Tóquio** | Equinix | ARTERIA Networks Corporation, BroadBand Tower, Inc. |
| **Toronto** | Equinix | Airgate Technologies. Inc, Cogeco Peer 1, Rogers, Thinktel, Zirro|
| **Washington, D.C.** |Equinix | Altice Business, Gtt Communications Inc, Epsilon, Lightower, Masergy, Windstream |

## <a name="expressroute-system-integrators"></a>Integradores de sistema de ExpressRoute
Habilitar a conectividade privada toofit que suas necessidades podem ser um desafio, com base em escala de saudação da sua rede. Você pode trabalhar com qualquer Olá integradores de sistema listados na Olá tooassist tabela a seguir você com integração tooExpressRoute.

| **Continent** | **Integradores do sistema** |
| --- | --- |
| **Ásia** |Avanade Inc., OneAs1a |
| **Austrália** | Ensyst, IT Consultancy, MOQdigital, Vigilant.IT |
| **Europa** |Avanade Inc., Altogee, Bright Skies GmbH, Inframon, MSG Services, New Signature, Nelite, Orange Networks, sol-tec |
| **América do Norte** |Avanade Inc., Equinix Professional Services, FlexManage, Perficient, Presidio |
| **América do Sul** |Avanade Inc. |
## <a name="next-steps"></a>Próximas etapas
* Para obter mais informações sobre a rota expressa, consulte Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).
* Certifique-se que todos os pré-requisitos foram atendidos. Consulte [Pré-requisitos do ExpressRoute](expressroute-prerequisites.md).

<!--Image References-->
[0]: ./media/expressroute-locations/expressroute-locations-map.png "Mapa de localização"
