---
title: requisitos de aaaNAT para circuitos ExpressRoute | Microsoft Docs
description: "Esta página fornece os requisitos detalhados para a configuração e o gerenciamento de NAT para circuitos do ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 867bf936-c851-485f-84c8-d8d6e33fee9f
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 09a0e841235de3f6b85e32172d7f99f20b5baf54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-nat-requirements"></a>Requisitos de NAT do ExpressRoute
tooconnect tooMicrosoft serviços de nuvem usando o ExpressRoute, você precisa tooset backup e gerenciar NATs. Alguns provedores de conectividade oferecem a configuração e o gerenciamento de NAT como um serviço gerenciado. Verifique com seu toosee do provedor de conectividade se eles oferecem um serviço. Caso contrário, é preciso cumprir os requisitos de toohello descritos abaixo. 

Saudação de revisão [ExpressRoute circuitos e domínios de roteamento](expressroute-circuit-peerings.md) página tooget uma visão geral da saudação vários domínios de roteamentos. toomeet Olá públicos requisitos de endereço IP para o público do Azure e emparelhamento da Microsoft, recomendamos que você configure o NAT entre sua rede e a Microsoft. Esta seção fornece uma descrição detalhada da infraestrutura NAT Olá que precisar tooset backup.

## <a name="nat-requirements-for-azure-public-peering"></a>Requisitos de NAT para o emparelhamento público do Azure
Olá caminho de emparelhamento público do Azure permite que você tooconnect tooall serviços hospedados no Azure em seus endereços IP públicos. Isso inclui serviços listados na Olá [ExpessRoute perguntas frequentes sobre](expressroute-faqs.md) e todos os serviços hospedados por ISVs no Microsoft Azure. 

> [!IMPORTANT]
> Serviços de conectividade tooMicrosoft Azure público emparelhamento é iniciada sempre da rede na rede da Microsoft hello. Portanto, não não possível iniciar sessões da rede do Microsoft Azure services tooyour através do ExpressRoute. Se você tentar, toothese pacotes enviados anunciado IPs usará Olá internet em vez de rota expressa.
> 

O tráfego destinado tooMicrosoft do Azure no emparelhamento público deve ser toovalid SNATed de endereços IPv4 públicos antes que eles entrem na rede do Microsoft hello. Figura Olá a seguir fornece uma imagem de alto nível de como Olá NAT pode ser configurado toomeet Olá acima requisito.

![](./media/expressroute-nat/expressroute-nat-azure-public.png) 

### <a name="nat-ip-pool-and-route-advertisements"></a>Pool de IP de NAT e anúncios de rota
Certifique-se de que o tráfego está inserindo Olá caminho de emparelhamento público do Azure com um endereço IPv4 público válido. Microsoft deve ser capaz de toovalidate propriedade Olá Olá pool de endereços IPv4 NAT em relação a um registro regional de roteamento da Internet (RIR) ou um registro de roteamento de Internet (IRR). Uma verificação será executada com base em hello como número sendo emparelhada com e Olá endereços IP usados para Olá NAT. Consulte toohello [requisitos de roteamento de rota expressa](expressroute-routing.md) página para obter informações sobre roteamento de registros.

Não existem restrições no tamanho da saudação do prefixo IP de NAT Olá anunciado por esse emparelhamento. Você deve monitorar o pool NAT hello e certifique-se de que você não tem necessidade de sessões NAT.

> [!IMPORTANT]
> Olá pool NAT IP anunciado tooMicrosoft não deve ser anunciado toohello da Internet. Isso interromperá a conectividade tooother da Microsoft.
> 
> 

## <a name="nat-requirements-for-microsoft-peering"></a>Requisitos de NAT para emparelhamento da Microsoft
caminho de emparelhamento de Microsoft Hello permite a conexão tooMicrosoft serviços de nuvem que não são suportados por meio de saudação caminho de emparelhamento público do Azure. lista de saudação de serviços inclui serviços do Office 365, como o Exchange Online, SharePoint Online, Skype for Business e Dynamics 365. A Microsoft espera conectividade bidirecional toosupport Olá emparelhamento da Microsoft. O tráfego destinado tooMicrosoft os serviços de nuvem devem ser toovalid SNATed de endereços IPv4 públicos antes que eles entrem na rede do Microsoft hello. O tráfego destinado tooyour rede dos serviços de nuvem da Microsoft deve ser SNATed em seu tooprevent de borda de Internet [roteamento assimétrico](expressroute-asymmetric-routing.md). Figura de saudação abaixo fornece uma visão de alto nível da como Olá NAT deve ser configurados para emparelhamento da Microsoft.

![](./media/expressroute-nat/expressroute-nat-microsoft.png) 

### <a name="traffic-originating-from-your-network-destined-toomicrosoft"></a>Tráfego originado em sua rede destinado tooMicrosoft
* Certifique-se de que o tráfego está inserindo o caminho de emparelhamento Microsoft hello com um endereço IPv4 público válido. Microsoft deve ser capaz de toovalidate proprietário Olá Olá pool de endereços IPv4 NAT contra Olá registro regional de roteamento da internet (RIR) ou um registro de roteamento de internet (IRR). Uma verificação será executada com base em hello como número sendo emparelhada com e Olá endereços IP usados para Olá NAT. Consulte toohello [requisitos de roteamento de rota expressa](expressroute-routing.md) página para obter informações sobre roteamento de registros.
* Endereços IP usados para Olá configuração de emparelhamento pública do Azure e outros circuitos do ExpressRoute não devem ser anunciado tooMicrosoft por meio da sessão BGP de saudação. Não há nenhuma restrição de comprimento de saudação do prefixo IP de NAT de Olá anunciado por esse emparelhamento.
  
  > [!IMPORTANT]
  > Olá pool NAT IP anunciado tooMicrosoft não deve ser anunciado toohello da Internet. Isso interromperá a conectividade tooother da Microsoft.
  > 
  > 

### <a name="traffic-originating-from-microsoft-destined-tooyour-network"></a>Tráfego originado de rede destinado tooyour da Microsoft
* Alguns cenários exigem Microsoft tooinitiate conectividade tooservice pontos de extremidade hospedados dentro de sua rede. Um exemplo típico de cenário Olá seria servidores tooADFS de conectividade hospedados em sua rede do Office 365. Nesses casos, você deve deixar vazar prefixos apropriados da sua rede no emparelhamento da Microsoft hello. 
* Você deve tráfego do Microsoft SNAT no hello borda de Internet para pontos de extremidade de serviço dentro de sua rede tooprevent [roteamento assimétrico](expressroute-asymmetric-routing.md). Solicitações **e respostas** com um destino IP que correspondam a uma rota recebida por meio do ExpressRoute serão sempre enviadas por meio do ExpressaRoute. Roteamento assimétrico existe se Olá solicitação é recebida por meio de saudação da Internet com hello resposta enviada através de rota expressa. SNATing Olá Microsoft tráfego de entrada em Olá borda Internet força toohello borda de Internet, resolvendo o problema de saudação do back de tráfego de resposta.

![Roteamento assimétrico com o ExpressRoute](./media/expressroute-asymmetric-routing/AsymmetricRouting2.png)

## <a name="next-steps"></a>Próximas etapas
* Consulte os requisitos de toohello para [roteamento](expressroute-routing.md) e [QoS](expressroute-qos.md).
* Para obter informações sobre o fluxo de trabalho, consulte [Fluxos de trabalho de provisionamento e estados do circuito do ExpressRoute](expressroute-workflows.md).
* Configurar sua conexão do ExpressRoute.
  
  * [Criar um circuito do ExpressRoute](expressroute-howto-circuit-classic.md)
  * [Configurar o roteamento](expressroute-howto-routing-classic.md)
  * [Vincular um circuito de rota expressa do tooan de rede virtual](expressroute-howto-linkvnet-classic.md)

