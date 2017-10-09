---
title: NAT para Azure ExpressRoute | Microsoft Docs
description: "Esta página fornece requisitos detalhados para a configuração e gerenciamento de roteamento para circuitos do ExpressRoute."
documentationcenter: na
services: expressroute
author: osamazia
manager: ganesr
editor: 
ms.assetid: eaaf0393-d384-4496-9a5c-328e94c262a7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: osamam
ms.openlocfilehash: 7a8b760df90b545b5fbde2f614aef62dd3985bb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="nat-for-expressroute"></a>NAT para ExpressRoute

tooconnect tooMicrosoft serviços de nuvem usando o ExpressRoute, você precisa tooset backup e gerenciar o roteamento. Alguns provedores de conectividade oferecem a configuração e o gerenciamento de roteamento como um serviço gerenciado. Verifique com seu toosee do provedor de conectividade se eles oferecem esse serviço. Caso contrário, é preciso cumprir toohello requisitos a seguir. 

Consulte toohello [circuitos e domínios de roteamento](expressroute-circuit-peerings.md) artigo para obter uma descrição de roteamento Olá sessões que precisam toobe configurar conectividade toofacilitate.

> [!NOTE]
> A Microsoft não dá suporte aos protocolos de redundância do roteador (por exemplo, HSRP e VRRP) para as configurações de alta disponibilidade. Contamos com um par redundante de sessões BGP por emparelhamento para alta disponibilidade.
> 
> 

## <a name="ip-addresses-used-for-peerings"></a>Endereços IP usados para emparelhamentos

Você precisa tooreserve alguns blocos de IP endereços tooconfigure roteamento entre sua rede e roteadores de borda (MSEEs) corporativos da Microsoft. Esta seção fornece uma lista de requisitos e descreve Olá regras sobre como esses endereços IP devem ser adquiridos e usados.

### <a name="ip-addresses-used-for-azure-private-peering"></a>Endereços IP usados para o emparelhamento privado do Azure

Você pode usar endereços IP particulares ou públicos endereços tooconfigure Olá emparelhamentos IP. intervalo de endereços Olá usado para configurar rotas não deve sobrepor endereço intervalos usados toocreate redes virtuais no Azure. 

* Você deve reservar uma sub-rede /29 ou duas sub-redes /30 para interfaces de roteamento.
* sub-redes de saudação para roteamento podem ser endereços IP privados ou endereços IP públicos.
* sub-redes de saudação não devem entrar em conflito com intervalo de saudação reservado pelo cliente Olá para uso em nuvem da Microsoft hello.
* Se uma sub-rede /29 for usada, será dividida em duas sub-redes /30. 
  * Olá primeiro/30 sub-rede será usada para o link primário hello e Olá /30 segunda sub-rede será usada para o link secundário hello.
  * Para cada uma das sub-redes Olá /30, você deve usar o primeiro endereço IP hello da sub-rede Olá /30 no roteador. A Microsoft usará o endereço IP da segunda Olá de saudação /30 sub-rede tooset uma sessão BGP.
  * Você deve configurar ambas as sessões BGP para nosso [SLA de disponibilidade](https://azure.microsoft.com/support/legal/sla/) toobe válido.  

#### <a name="example-for-private-peering"></a>Exemplo para emparelhamento privado

Se você escolher toouse a.b.c.d/29 tooset backup Olá emparelhamento, ele será dividido em dois /30 sub-redes. O exemplo hello abaixo, examinaremos como subrede a.b.c.d/29 Olá é usado. 

a.b.c.d/29 será dividido tooa.b.c.d/30 e a.b.c.d+4/30 e passada tooMicrosoft por meio de APIs de provisionamento de saudação. Você usará a.b.c.d+1 como Olá VRF IP para hello PE primário e Microsoft consumirá a.b.c.d+2 como Olá VRF IP para Olá MSEE primário. Você usará a.b.c.d+5 como hello VRF IP para hello PE secundário e a Microsoft usará a.b.c.d+6 como Olá VRF IP para Olá MSEE secundário.

Considere um caso em que você selecionar tooset 192.168.100.128/29 o emparelhamento privado. 192.168.100.128/29 inclui endereços de 192.168.100.128 too192.168.100.135, entre os quais:

* 192.168.100.128/30 será atribuído toolink1, com o provedor usando 192.168.100.129 e Microsoft usando 192.168.100.130.
* 192.168.100.132/30 será atribuído toolink2, com o provedor usando 192.168.100.133 e Microsoft usando 192.168.100.134.

### <a name="ip-addresses-used-for-azure-public-and-microsoft-peering"></a>Endereços IP usados para o emparelhamento público do Azure e o emparelhamento da Microsoft

Você deve usar endereços IP públicos que você possui para configurar sessões BGP hello. Microsoft deve ser de propriedade de saudação tooverify capaz de endereços IP hello por meio de registros de roteamento de Internet e roteamento de registros de Internet. 

* Você deve usar uma única/29 sub-rede ou tooset duas /30 sub-redes a saudação BGP de emparelhamento para cada emparelhamento por circuito de rota expressa (se você tiver mais de um). 
* Se uma sub-rede /29 for usada, será dividida em duas sub-redes /30. 
  * Olá primeiro/30 sub-rede será usada para o link primário hello e Olá /30 segunda sub-rede será usada para o link secundário hello.
  * Para cada uma das sub-redes Olá /30, você deve usar o primeiro endereço IP hello da sub-rede Olá /30 no roteador. A Microsoft usará o endereço IP da segunda Olá de saudação /30 sub-rede tooset uma sessão BGP.
  * Você deve configurar ambas as sessões BGP para nosso [SLA de disponibilidade](https://azure.microsoft.com/support/legal/sla/) toobe válido.

## <a name="public-ip-address-requirement"></a>Requisito do endereço IP público

### <a name="private-peering"></a>Emparelhamento privado

Você pode escolher toouse públicos ou privados endereços IPv4 para emparelhamento privado. Podemos fornecer um isolamento de ponta a ponta do tráfego para que a sobreposição dos endereços com outros clientes não seja possível no caso do emparelhamento privado. Estes endereços não são tooInternet anunciado. 

### <a name="public-peering"></a>Emparelhamento público

Olá caminho de emparelhamento público do Azure permite que você tooconnect tooall serviços hospedados no Azure em seus endereços IP públicos. Isso inclui serviços listados na Olá [ExpessRoute perguntas frequentes sobre](expressroute-faqs.md) e todos os serviços hospedados por ISVs no Microsoft Azure. Serviços de conectividade tooMicrosoft Azure público emparelhamento é iniciada sempre da rede na rede da Microsoft hello. Você deve usar endereços IP públicos para Olá tráfego destinado tooMicrosoft de rede.

### <a name="microsoft-peering"></a>Emparelhamento da Microsoft

caminho de emparelhamento de Microsoft Hello permite a conexão tooMicrosoft serviços de nuvem que não são suportados por meio de saudação caminho de emparelhamento público do Azure. lista de saudação de serviços inclui serviços do Office 365, como o Exchange Online, SharePoint Online, Skype for Business e Dynamics 365. A Microsoft oferece suporte conectividade bidirecional Olá emparelhamento da Microsoft. Serviços de nuvem do tráfego destinado tooMicrosoft devem usar endereços IPv4 públicos válidos antes que eles entrem na rede do Microsoft hello.

Certifique-se de que seu endereço IP e como número são tooyou registrado em um dos registros de saudação listados abaixo.

* [ARIN](https://www.arin.net/)
* [APNIC](https://www.apnic.net/)
* [AFRINIC](https://www.afrinic.net/)
* [LACNIC](http://www.lacnic.net/)
* [RIPENCC](https://www.ripe.net/)
* [RADB](http://www.radb.net/)
* [ALTDB](http://altdb.net/)

> [!IMPORTANT]
> IP público endereços anunciado tooMicrosoft através do ExpressRoute não deve ser anunciado toohello da Internet. Isso pode interromper os serviços de conectividade do Microsoft tooother. No entanto, os endereços IP Públicos usados pelos servidores em sua rede que se comunicam com os pontos de extremidade do O365 da Microsoft podem ser divulgados no ExpressRoute. 
> 
> 

## <a name="dynamic-route-exchange"></a>Intercâmbio de roteamento dinâmico

O intercâmbio de roteamento será por meio do protocolo eBGP. As sessões EBGP são estabelecidas entre MSEEs hello e os roteadores. A autenticação de sessões BGP não é um requisito. Se necessário, um hash MD5 pode ser configurado. Consulte Olá [Configurar roteamento](expressroute-howto-routing-classic.md) e [circuito fluxos de trabalho de provisionamento e estados de circuito](expressroute-workflows.md) para obter informações sobre como configurar sessões BGP.

## <a name="autonomous-system-numbers"></a>Números de sistema autônomos

A Microsoft usará AS 12076 para o emparelhamento público do Azure, o emparelhamento privado do Azure e o emparelhamento da Microsoft . Nós reservamos ASNs de too65520 65515 para uso interno. Há suporte para números AS de 16 e 32 bits.

Não há requisitos de simetria de transferência de dados. caminhos de avanço e retorno Olá podem atravessar pares diferentes do roteador. Rotas idênticas devem ser anunciadas de qualquer um dos lados entre vários pares de circuitos que pertencem a você. Métrica não é necessária toobe idêntico.

## <a name="route-aggregation-and-prefix-limits"></a>Agregação de rotas e limites de prefixo

Há suporte para backup too4000 prefixos anunciados toous por meio de saudação emparelhamento particular do Azure. Isso pode ser aumentado se too10, prefixos 000 se o complemento do premium Olá ExpressRoute está habilitado. Podemos aceitar too200 prefixos por sessão BGP para o público do Azure e emparelhamento da Microsoft. 

sessão BGP de saudação será removida se o número de saudação de prefixos excede o limite de saudação. Aceitaremos em Olá emparelhamento link privado apenas as rotas padrão. Provedor deve filtrar a rota padrão e endereços IP privados (RFC 1918) do hello pública do Azure e caminhos de emparelhamento da Microsoft. 

## <a name="transit-routing-and-cross-region-routing"></a>Roteamento de tráfego e de roteamento entre regiões

A Rota Expressa não pode ser configurada como roteadores de tráfego. Você terá toorely no seu provedor de conectividade para serviços de roteamento de tráfego.

## <a name="advertising-default-routes"></a>Anunciando rotas padrão

As rotas padrão são permitidas apenas em sessões de emparelhamento privado do Azure. Nesse caso, estamos roteará todo o tráfego de rede de tooyour Olá redes virtuais associadas. Anunciar rotas padrão para emparelhamento privado resultará no caminho de internet de saudação do Azure que está sendo bloqueado. Você deve se basear em seu tráfego de tooroute de borda corporativo do e toohello internet para serviços hospedados no Azure. 

 tooenable tooother de conectividade do Azure services e serviços de infraestrutura, você deve verificar se um dos itens a seguir de saudação está em vigor:

* O emparelhamento público do Azure é habilitado tooroute tráfego toopublic pontos de extremidade
* Você pode usar definido pelo usuário roteamento tooallow conectividade com a internet cada sub-rede que exigem conectividade da Internet.

> [!NOTE]
> Anunciar rotas padrão irá interromper o Windows e outra ativação de licença da VM. Siga as instruções [aqui](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx) toowork esse problema.
> 
> 

## <a name="support-for-bgp-communities-preview"></a>Suporte a comunidades BGP (visualização)

Esta seção fornece uma visão geral de como as comunidades BGP serão usadas com a Rota Expressa. Microsoft anunciará rotas hello público e caminhos de emparelhamento da Microsoft com rotas marcadas com valores apropriados de comunidade. Olá lógica para fazer isso e Olá detalhes na comunidade valores são descritos abaixo. Microsoft, no entanto, não aceita qualquer comunidade tooroutes marcado valores anunciado tooMicrosoft.

Se você estiver se conectando tooMicrosoft por meio de rota expressa em qualquer um emparelhamento local dentro de uma região geopolíticas, você terá acesso tooall serviços em nuvem Microsoft em todas as regiões dentro de limites geopolíticas hello. 

Por exemplo, se você conectou tooMicrosoft em Amsterdã por meio de rota expressa, você terá serviços de nuvem do acesso tooall Microsoft hospedados na Europa Norte e Europa Ocidental. 

Consulte toohello [ExpressRoute locais de emparelhamento e parceiros](expressroute-locations.md) página para uma lista detalhada das regiões geopolíticas, regiões do Azure associados e rota expressa correspondente emparelhamento locais.

Você pode adquirir mais de um circuito da Rota Expressa por região geopolítica. Ter várias conexões oferece benefícios significativos em alta disponibilidade toogeo devido a redundância. Em casos em que você tiver vários circuitos de rota expressa, você receberá Olá mesmo conjunto de prefixos anunciado da Microsoft no emparelhamento público do hello e caminhos de emparelhamento da Microsoft. Isso significa que você terá vários caminhos de sua rede até a Microsoft. Isso pode causar roteamento abaixo do ideal toobe de decisões feita em sua rede. Como resultado, você pode enfrentar conectividade abaixo do ideal experiências toodifferent serviços. 

Microsoft marcar os prefixos anunciados através do emparelhamento público e Microsoft emparelhamento com valores apropriados de comunidade BGP indicando prefixos de Olá Olá região é hospedado em. Você pode confiar em Olá comunidade valores toomake apropriado roteamento decisões toooffer [toocustomers roteamento ideal](expressroute-optimize-routing.md).

| **Região Geopolítica** | **Região do Microsoft Azure** | **Valor de comunidade BGP** |
| --- | --- | --- |
| **América do Norte** | | |
| Leste dos EUA |12076:51004 | |
| Leste dos EUA 2 |12076:51005 | |
| Oeste dos EUA |12076:51006 | |
| Oeste dos EUA 2 |12076:51026 | |
| Centro-Oeste dos EUA |12076:51027 | |
| Centro-Norte dos EUA |12076:51007 | |
| Centro-Sul dos Estados Unidos |12076:51008 | |
| Centro dos EUA |12076:51009 | |
| Canadá Central |12076:51020 | |
| Leste do Canadá |12076:51021 | |
| **América do Sul** | | |
| Sul do Brasil |12076:51014 | |
| **Europa** | | |
| Norte da Europa |12076:51003 | |
| Europa Ocidental |12076:51002 | |
| **Pacífico Asiático** | | |
| Ásia Oriental |12076:51010 | |
| Sudeste Asiático |12076:51011 | |
| **Japão** | | |
| Leste do Japão |12076:51012 | |
| Oeste do Japão |12076:51013 | |
| **Austrália** | | |
| Leste da Austrália |12076:51015 | |
| Sudeste da Austrália |12076:51016 | |
| **Índia** | | |
| Sul da Índia |12076:51019 | |
| Oeste da Índia |12076:51018 | |
| Centro da Índia |12076:51017 | |

Todas as rotas anunciadas da Microsoft serão marcadas com o valor de comunidade apropriado hello. 

> [!IMPORTANT]
> Os prefixos globais serão marcados com um valor apropriado de comunidade e serão anunciados somente quando o complemento premium da Rota Expressa estiver habilitado.
> 
> 

Além disso toohello acima, Microsoft será também marca prefixos com base no serviço Olá pertencerem a. Isso se aplica somente emparelhamento da Microsoft toohello. Olá tabela a seguir fornece um mapeamento de valor de comunidade do serviço tooBGP.

| **Serviço** | **Valor de comunidade BGP** |
| --- | --- |
| **Exchange** |12076:5010 |
| **SharePoint** |12076:5020 |
| **Skype For Business** |12076:5030 |
| **Dynamics 365** |12076:5040 |
| **Outros serviços do Office 365** |12076:5100 |

> [!NOTE]
> Microsoft não aceita valores de comunidade BGP definida Olá rotas anunciado tooMicrosoft.
> 
> 

## <a name="next-steps"></a>Próximas etapas

* Configurar sua conexão da Rota Expressa.
  
  * [Criar um circuito de rota expressa para o modelo de implantação clássico Olá](expressroute-howto-circuit-classic.md) ou [criar e modificar um circuito de rota expressa usando o Gerenciador de recursos do Azure](expressroute-howto-circuit-arm.md)
  * [Configurar o roteamento para o modelo de implantação clássico Olá](expressroute-howto-routing-classic.md) ou [configurar o roteamento para o modelo de implantação do Gerenciador de recursos de saudação](expressroute-howto-routing-arm.md)
  * [Vincular um tooan de rede virtual circuito de rota expressa clássico](expressroute-howto-linkvnet-classic.md) ou [Link tooan um Gerenciador de recursos de VNet circuito de rota expressa](expressroute-howto-linkvnet-arm.md)

