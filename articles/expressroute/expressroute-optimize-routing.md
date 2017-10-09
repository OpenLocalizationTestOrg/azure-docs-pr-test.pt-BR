---
title: 'Otimizar o roteamento de ExpressRoute: Azure | Microsoft Docs'
description: "Esta página fornece detalhes sobre como toooptimize roteamento quando você tiver mais de um ExpressRoute circuitos que conectar-se entre a Microsoft e sua rede corp."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
ms.assetid: fca53249-d9c3-4cff-8916-f8749386a4dd
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/06/2017
ms.author: charwen
ms.openlocfilehash: ebcfb638f67a9ac78c3e476668bfd0bb0ffb9985
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-expressroute-routing"></a>Otimizar o roteamento do ExpressRoute
Quando você tiver vários circuitos de rota expressa, você tem mais de um tooMicrosoft tooconnect de caminho. Como resultado, roteamento abaixo do ideal pode acontecer - ou seja, o tráfego pode levar uma tooreach de caminho mais Microsoft e a rede da Microsoft tooyour. Olá mais Olá caminho de rede, latência mais alta de Olá Olá. A latência tem impacto direto na experiência de usuário e no desempenho do aplicativo. Este artigo ilustram esse problema e explicar como toooptimize roteamento usando Olá tecnologias padrão de roteamentos.

## <a name="suboptimal-routing-from-customer-toomicrosoft"></a>Qualidade inferior de roteamento do cliente tooMicrosoft
Vamos dar uma olhada Fechar ao problema de roteamento Olá por um exemplo. Imagine que você tem dois escritórios em Olá dos Estados Unidos, um em Los Angeles e um em Nova York. Seus escritórios estão conectados em uma WAN (rede de longa distância), que pode ser sua própria rede backbone ou VPN de IP do provedor de serviços. Você tem dois circuitos de rota expressa, um em US West e um em US East, que também estão conectados no hello WAN. Obviamente, você tem dois caminhos tooconnect toohello MSN. Agora imagine que você tem a implantação do Azure (por exemplo, o Serviço de Aplicativo do Azure) no Oeste dos EUA e no Leste dos EUA. Sua intenção é tooconnect seus usuários em Los Angeles tooAzure US West e seus usuários em Nova York tooAzure US East porque seu administrador de serviço anuncia que os usuários em cada acesso office Olá nas proximidades de serviços do Azure melhores experiências. Infelizmente, plano Olá estabelece bem para os usuários do hello Costa Leste, mas não para os usuários do hello Costa Oeste. Olá causa problema Olá é seguir hello. Cada circuito de rota expressa, podemos anunciar tooyou tanto prefixo Olá no Azure US East (23.100.0.0/16) e o prefixo de saudação no Azure US West (13.100.0.0/16). Se você não souber qual prefixo da qual região, você não é capaz de tootreat ele diferente. Sua rede WAN pode pensar dois prefixos de saudação são Leste tooUS mais próximo que US West e circular, portanto, os dois toohello de usuários do office circuito de rota expressa em US East. No final do hello, você terá muitos usuários insatisfeitos em Los Angeles office de hello.

![Problema de rota expressa caso 1 - qualidade inferior de roteamento do cliente tooMicrosoft](./media/expressroute-optimize-routing/expressroute-case1-problem.png)

### <a name="solution-use-bgp-communities"></a>Solução: usar comunidades BGP
toooptimize roteamento para os usuários do office, você precisa tooknow qual prefixo é do Azure US West e que do Azure US East. Nós codificamos essas informações usando [Valores da Comunidade BGP](expressroute-routing.md). Atribuímos um tooeach de valor exclusivo do BGP Community região do Azure, por exemplo "12076:51004" para o Leste dos EUA, "12076:51006" para o Oeste dos EUA. Agora que você sabe que prefixo é de que região do Azure, pode configurar qual circuito de ExpressRoute deve ser preferencial. Como podemos usar informações de roteamento Olá BGP tooexchange, você pode usar o roteamento do BGP preferência Local tooinfluence. Em nosso exemplo, você pode atribuir um maior preferência local valor too13.100.0.0/16 em US West que em US East e da mesma forma, um maior preferência local valor too23.100.0.0/16 em US East que em US West. Essa configuração garantirá que, quando ambos os tooMicrosoft caminhos estão disponíveis, os usuários em Los Angeles levará circuito de rota expressa Olá em US West tooconnect tooAzure US West enquanto os usuários em Nova York levar Olá rota expressa em US East tooAzure US East . O roteamento é otimizado em ambos os lados. 

![Solução de ExpressRoute, Caso 1 - usar Comunidades BGP](./media/expressroute-optimize-routing/expressroute-case1-solution.png)

> [!NOTE]
> Olá a mesma técnica, com preferência Local, pode ser aplicada toorouting do cliente tooAzure rede Virtual. Nós não marcar os prefixos de toohello de valor de comunidade de BGP anunciados da rede tooyour do Azure. No entanto, como você sabe que a implantação de rede Virtual toowhich fechar seu escritório, você pode configurar seus roteadores adequadamente tooprefer um tooanother de circuito de rota expressa.
>
>

## <a name="suboptimal-routing-from-microsoft-toocustomer"></a>Qualidade inferior de roteamento do Microsoft toocustomer
Aqui está outro exemplo em que conexões da Microsoft levar uma tooreach de caminho mais sua rede. Nesse caso, você usa servidores Exchange locais e o Exchange Online em um [ambiente híbrido](https://technet.microsoft.com/library/jj200581%28v=exchg.150%29.aspx). Do escritório é conectado tooa WAN. Anunciar prefixos Olá dos seus servidores locais no seu tooMicrosoft escritórios através de circuitos do ExpressRoute Olá dois. Exchange Online será iniciada servidores de locais de toohello conexões em casos como migração de caixa de correio. Infelizmente, Olá conexão tooyour Los Angeles office é roteado toohello circuito de rota expressa em US East antes de desvio Costa do hello todo toohello back continente Oeste. causa do problema de Olá Olá é semelhante toohello um primeiro. Sem qualquer dica, a rede da Microsoft hello não pode determinar qual prefixo de cliente é Leste tooUS fechar e qual delas é fechar tooUS Oeste. Isso acontece office de tooyour de caminho errado toopick Olá em Los Angeles.

![Rota expressa caso 2 - qualidade inferior de roteamento do Microsoft toocustomer](./media/expressroute-optimize-routing/expressroute-case2-problem.png)

### <a name="solution-use-as-path-prepending"></a>Solução: usar precedência de caminho AS
Há dois problemas toohello de soluções. Olá primeiro um é que você simplesmente anunciar seu prefixo de local de escritório Los Angeles, 177.2.0.0/31, no circuito de rota expressa Olá em US West e o local do prefixo para o escritório de Nova York, 177.2.0.2/31, no circuito de rota expressa Olá em US East. Como resultado, há apenas um caminho para o Microsoft tooconnect tooeach dos seus escritórios. Não há nenhuma ambiguidade e o roteamento é otimizado. Com esse design, você precisa toothink sobre sua estratégia de failover. Olá evento Olá tooMicrosoft caminho por meio de rota expressa é interrompido, será necessário toomake-se de que o Exchange Online ainda pode se conectar servidores de locais tooyour. 

Olá segunda solução é que continuar tooadvertise de prefixos de saudação em ambos os circuitos de rota expressa e, além de fornecer uma dica do qual prefixo é toowhich fechar um de seus escritórios. Porque há suporte para o caminho do BGP porque acrescentando, você pode configurar hello como caminho para o roteamento de tooinfluence de prefixo. Neste exemplo, você pode aumentar hello como caminho para 172.2.0.0/31 em US East para que podemos prefiram circuito de rota expressa Olá em US West para o tráfego destinado a esse prefixo (como rede será considerado toothis prefixo da saudação é menor no Oeste Olá). Da mesma forma, você pode aumentar hello como caminho para 172.2.0.2/31 em US West para que é preferível circuito de rota expressa Olá em US East. O roteamento é otimizado para ambos os escritórios. Com esse design, se um circuito do ExpressRoute for interrompido, o Exchange Online poderá ainda acessá-lo por meio de outro circuito do ExpressRoute e sua WAN. 

> [!IMPORTANT]
> Removemos particulares como números em hello como caminho de prefixos de saudação recebida no Microsoft Peering. Você precisa tooappend público como números em Olá caminho porque tooinfluence roteamento para Peering Microsoft.
> 
> 

![Solução de ExpressRoute, caso 2 - usar precedência de AS PATH](./media/expressroute-optimize-routing/expressroute-case2-solution.png)

> [!NOTE]
> Enquanto os exemplos de Olá fornecidos aqui são para a Microsoft e emparelhamentos públicos, há suporte para Olá os mesmos recursos para o emparelhamento privado hello. Além disso, Olá caminho porque acrescentando funciona dentro de um único circuito de rota expressa, seleção de saudação tooinfluence dos caminhos de saudação primários e secundários.
> 
> 

## <a name="suboptimal-routing-between-virtual-networks"></a>Qualidade inferior de roteamento entre redes virtuais
Com o ExpressRoute, você pode habilitar a rede Virtual tooVirtual rede (que também é conhecido como "VNet") comunicação vinculando tooan circuito de rota expressa. Quando você vinculá-los circuitos do ExpressRoute toomultiple, roteamento abaixo do ideal pode ocorrer entre hello VNets. Vamos considerar um exemplo. Você tem dois circuitos de ExpressRoute, um no Oeste dos EUA e outro no Leste dos EUA. Em cada região, você tem duas VNets. Os servidores web são implantados em uma VNet e servidores de aplicativo hello outros. Para redundância, você vincular Olá dois VNets no circuito de rota expressa local cada região tooboth hello e Olá remoto circuito de rota expressa. Como pode ser visto abaixo, de cada VNet existem dois toohello de caminhos outras redes. Olá VNets não sabe qual circuito de rota expressa é local e qual é remoto. Consequentemente, como igual-custo-Multi-Path (ECMP) roteamento tooload-VNet inter balancear, alguns fluxos de tráfego levará o caminho mais longo de saudação e no circuito de rota expressa Olá remoto podem ser roteados.

![ExpressRoute, Caso 3 - qualidade inferior de roteamento entre redes virtuais](./media/expressroute-optimize-routing/expressroute-case3-problem.png)

### <a name="solution-assign-a-high-weight-toolocal-connection"></a>Solução: atribuir uma conexão de toolocal peso alta
solução de saudação é simple. Como você sabe onde estão os circuitos de VNets e Olá Olá, você pode Conte-nos qual caminho deve preferir a cada rede virtual. Especificamente para este exemplo, você atribui uma conexão de local de toohello superior do peso de conexão remota toohello (consulte o exemplo de configuração hello [aqui](expressroute-howto-linkvnet-arm.md#modify-a-virtual-network-connection)). Quando uma rede virtual recebe prefixo Olá Olá outras redes em várias conexões prefiram conexão Olá com hello maior peso toosend tráfego destinado a esse prefixo.

![Solução de rota expressa caso 3 - atribuir peso alta toolocal conexão](./media/expressroute-optimize-routing/expressroute-case3-solution.png)

> [!NOTE]
> Você também pode influenciar o roteamento da rede de local de tooyour de rede virtual, se você tiver vários circuitos de rota expressa, configurando o peso de saudação de uma conexão em vez de aplicar AS PATH acrescentando uma técnica descrita Olá segundo cenário acima. Para cada prefixo sempre examinaremos peso de conexão Olá antes Olá comprimento de caminho porque ao decidir como toosend tráfego.
>
>
