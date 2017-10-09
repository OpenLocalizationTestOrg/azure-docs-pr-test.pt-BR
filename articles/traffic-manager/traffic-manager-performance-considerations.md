---
title: "Considerações de aaaPerformance do Azure Traffic Manager | Microsoft Docs"
description: "Entender o desempenho no Gerenciador de tráfego e como tootest o desempenho do seu site ao usar o Gerenciador de tráfego"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 3ba5dfa1-2922-43f1-9a23-d06969c4a516
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: fd4e6cb221a2ceee63ec57237ee90fd714e91db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-considerations-for-traffic-manager"></a>Considerações de desempenho sobre Gerenciador de Tráfego

Esta página explica as considerações de desempenho usando o Gerenciador de Tráfego. Considere Olá cenário a seguir:

Você tem instâncias do site de saudação WestUS e EastAsia regiões. Uma das instâncias de saudação é Falha na verificação de integridade de saudação para investigação de Gerenciador de tráfego de saudação. Tráfego do aplicativo é a região Íntegro toohello direcionado. Esse failover é esperado, mas o desempenho pode ser um problema com base na latência de saudação do tráfego de saudação agora viajando região distante tooa.

## <a name="performance-considerations-for-traffic-manager"></a>Considerações de desempenho sobre Gerenciador de Tráfego

Olá somente impacto de desempenho que o Traffic Manager pode ter em seu site é pesquisa de DNS saudação inicial. Uma solicitação DNS para o nome de saudação do seu perfil do Gerenciador de tráfego é tratada pelo servidor de raiz de DNS da Microsoft hello zona hosts Olá trafficmanager.net. Gerenciador de tráfego preenche e atualiza regularmente, com base na política do Traffic Manager hello e resultados de teste de saudação servidores da Microsoft hello DNS raiz. Até mesmo durante a pesquisa DNS inicial hello, nenhuma consulta DNS é enviada tooTraffic Manager.

Gerenciador de tráfego é composto de vários componentes: nome de DNS, servidores, um serviço de API, camada de armazenamento hello e um ponto de extremidade de serviço de monitoramento. Se um componente de serviço do Gerenciador de tráfego falhar, não há nenhum efeito em nome DNS Olá associado com o perfil do Gerenciador de tráfego. registros de saudação em servidores de DNS da Microsoft hello permanecem inalterados. No entanto, o monitoramento de ponto de extremidade e a atualização de DNS não acontecem. Portanto, Gerenciador de tráfego não é capaz de tooupdate DNS toopoint tooyour failover site quando seu site primário falhar.

A resolução de nome DNS é rápida e os resultados são armazenados em cache. Olá velocidade de pesquisa de DNS saudação inicial depende Olá usa o cliente de saudação de servidores DNS para resolução de nome. Normalmente, um cliente pode concluir uma pesquisa de DNS em cerca de 50 ms. resultados de saudação da pesquisa de saudação são armazenados em cache durante Olá Olá DNS Time-to-live (TTL). padrão de saudação TTL do Traffic Manager é de 300 segundos.

O tráfego NÃO flui pelo Gerenciador de Tráfego. Quando a pesquisa de DNS Olá for concluída, o cliente de Olá tem um endereço IP para uma instância do seu site da web. cliente Olá toothat endereço conecta-se diretamente e não passa por meio do Gerenciador de tráfego. Olá política do Traffic Manager que você escolher tem não influenciam o desempenho do DNS hello. No entanto, um desempenho roteamento-método pode afetar negativamente a experiência de aplicativo hello. Por exemplo, se sua política redireciona o tráfego da América do Norte tooan instância hospedada na Ásia, latência de rede Olá para essas sessões pode ser um problema de desempenho.

## <a name="measuring-traffic-manager-performance"></a>Medindo o desempenho do Gerenciador de Tráfego

Há vários sites, você pode usar o desempenho de saudação toounderstand e o comportamento de um perfil do Gerenciador de tráfego. Muitos desses sites são gratuitos, mas podem ter limitações. Alguns sites oferecem monitoramento e relatórios aprimorados por uma taxa.

ferramentas de saudação nesses sites medem latências de DNS e exibição Olá resolver endereços IP para locais de cliente ao redor Olá, mundo. A maioria dessas ferramentas não armazenar em cache os resultados de DNS hello. Portanto, as ferramentas de Olá mostram a pesquisa de DNS completa Olá cada vez que um teste é executado. Quando você testar seu próprio cliente, você somente enfrentar desempenho pesquisa DNS de Olá completo uma vez durante a duração do tempo de vida de saudação.

## <a name="sample-tools-toomeasure-dns-performance"></a>Desempenho do DNS do exemplo ferramentas toomeasure

* [SolveDNS](http://www.solvedns.com/dns-comparison/)

    SolveDNS oferece várias ferramentas de desempenho. ferramenta de comparação de DNS Olá pode mostrar a você quanto tempo tooresolve seu nome DNS e como que compara tooother provedores de serviço DNS.

* [WebSitePulse](http://www.websitepulse.com/help/tools.php)

    Uma das ferramentas mais simples de saudação é WebSitePulse. Digite o tempo de resolução DNS do hello URL toosee, o primeiro Byte, o último Byte e outras estatísticas de desempenho. Você pode escolher entre três locais de teste diferentes. Neste exemplo, verá que execução primeiro Olá mostra que a pesquisa de DNS leva 0.204 s.

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse.png)

    Como Olá resultados são armazenados em cache, o segundo teste Olá para Olá mesma pesquisa de DNS do Traffic Manager ponto de extremidade Olá leva 0.002 s.

    ![pulse2](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse2.png)

* [Monitor Sintético de Aplicativo de AC](https://asm.ca.com/en/checkit.php)

    Anteriormente conhecido como ferramenta de Watchmouse seleção site hello, este site mostram Olá resolução de DNS de tempo de várias regiões geográficas simultaneamente. Insira o tempo de resolução DNS do hello URL toosee, o tempo de conexão e a velocidade de vários locais geográficos. Use este toosee teste qual serviço hospedado é retornado para diferentes locais ao redor Olá, mundo.

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-watchmouse.png)

* [Pingdom](http://tools.pingdom.com/)

    Essa ferramenta fornece estatísticas de desempenho para cada elemento de uma página da Web. Olá guia análise de página mostra o percentual de saudação do tempo gasto na pesquisa de DNS.

* [What's My DNS?](http://www.whatsmydns.net/)

    Este site faz uma pesquisa de DNS de 20 diferentes locais e exibe os resultados de saudação em um mapa.

* [Interface Dig Web](http://www.digwebinterface.com)

    Esse site mostra informações de DNS mais detalhadas, incluindo CNAMEs e registros A. Verifique se você verificar Olá 'Colorir output' e 'Estatísticas' em Opções e selecione 'Todos' em Nameservers.

## <a name="next-steps"></a>Próximas etapas

[Sobre os métodos de roteamento de tráfego do Gerenciador de Tráfego](traffic-manager-routing-methods.md)

[Teste as configurações do Gerenciador de Tráfego](traffic-manager-testing-settings.md)

[Operações no Gerenciador de Tráfego (referência de API REST)](http://go.microsoft.com/fwlink/?LinkId=313584)

[Cmdlets do Gerenciador de Tráfego do Azure](http://go.microsoft.com/fwlink/p/?LinkId=400769)

