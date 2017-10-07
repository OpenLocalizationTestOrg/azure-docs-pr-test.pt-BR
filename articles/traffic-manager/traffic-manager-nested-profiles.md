---
title: aaaNested perfis do Traffic Manager | Microsoft Docs
description: Este artigo explica o recurso de 'Perfis aninhados' hello do Azure Traffic Manager
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f1b112c4-a3b1-496e-90eb-41e235a49609
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: e476d58a82ed94d12731156280c9665f980de0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="nested-traffic-manager-profiles"></a>Perfis aninhados do Gerenciador de Tráfego

O Traffic Manager inclui uma variedade de métodos de roteamento de tráfego que permitem que você toocontrol como o Gerenciador de tráfego escolhe qual ponto de extremidade deve receber o tráfego de cada usuário final. Para obter mais informações, consulte [Métodos de roteamento de tráfego do Gerenciador de Tráfego](traffic-manager-routing-methods.md).

Cada perfil do Gerenciador de Tráfego especifica um único método de roteamento de tráfego. No entanto, há cenários que exigem mais sofisticadas roteamento de tráfego de roteamento Olá fornecido por um único perfil do Gerenciador de tráfego. Você pode aninhar os benefícios de saudação do Gerenciador de tráfego perfis toocombine de mais de um método de roteamento de tráfego. Perfis aninhados permitem que você toooverride saudação padrão do Traffic Manager comportamento toosupport maior e mais complexas implantações de aplicativos.

Olá exemplos a seguir ilustra como toouse aninhada perfis do Gerenciador de tráfego em vários cenários.

## <a name="example-1-combining-performance-and-weighted-traffic-routing"></a>Exemplo 1: combinando roteamento de tráfego de “Desempenho” e “Ponderado”

Suponha que você implantou um aplicativo hello regiões do Azure a seguir: Oeste dos EUA, Europa Ocidental e Ásia Oriental. Você usar do Gerenciador de tráfego "Desempenho" roteamento de tráfego método toodistribute tráfego toohello região mais próxima toohello usuário.

![Perfil único do Gerenciador de Tráfego][4]

Agora, vamos supor que você deseja um serviço de atualização de tooyour tootest antes de implantá-la mais amplamente. Você deseja toouse Olá 'ponderada' roteamento de tráfego método toodirect um pequeno percentual de implantação de teste de tooyour de tráfego. Configurar implantação de teste Olá junto com a implantação de produção existente Olá na Europa Ocidental.

Não é possível combinar roteamentos de tráfego “Ponderado” e por “Desempenho” em um único perfil. toosupport neste cenário, você cria um perfil do Gerenciador de tráfego usando pontos de extremidade do hello dois Ocidental e método hello roteamento de tráfego 'Ponderado'. Em seguida, você deve adicionar esse perfil 'child' como um perfil de toohello de ponto de extremidade 'pai'. perfil de pai Olá ainda usa Olá o método de roteamento de tráfego de desempenho e contém Olá outras implantações globais como pontos de extremidade.

Olá diagrama a seguir ilustra esse exemplo:

![Perfis aninhados do Gerenciador de Tráfego][2]

Nessa configuração, o tráfego direcionado por meio do perfil de pai Olá distribui tráfego entre regiões normalmente. Na Europa Ocidental, hello perfil aninhado distribui o tráfego toohello teste e produção pontos de extremidade de acordo com os pesos de toohello atribuídos.

Quando o perfil pai de saudação usa o método de roteamento de tráfego de 'Desempenho' hello, cada ponto de extremidade deve ser atribuído a um local. local de saudação é atribuído quando você configura o ponto de extremidade de saudação. Escolha a implantação de tooyour mais próxima do hello região do Azure. Hello regiões do Azure são valores de local de Olá Olá tabela de latência de Internet com suporte. Para obter mais informações, consulte [Método de roteamento de tráfego por “Desempenho” do Gerenciador de Tráfego](traffic-manager-routing-methods.md#performance).

## <a name="example-2-endpoint-monitoring-in-nested-profiles"></a>Exemplo 2: monitoramento de ponto de extremidade em Perfis Aninhados

Traffic Manager monitora ativamente a integridade de saudação de cada ponto de extremidade de serviço. Se um ponto de extremidade não está íntegro, o Traffic Manager direciona os usuários tooalternative pontos de extremidade toopreserve Olá a disponibilidade do seu serviço. Esse comportamento de failover e monitoramento de ponto de extremidade se aplica a tooall métodos de roteamento de tráfego. Para obter mais informações, consulte [Monitoramento do Ponto de Extremidade do Gerenciador de Tráfego](traffic-manager-monitoring.md). O monitoramento de ponto de extremidade funciona de forma diferente para perfis aninhados. Com perfis aninhados, perfil pai de saudação não executa verificações de integridade no filho Olá diretamente. Em vez disso, a integridade de saudação de pontos de extremidade do perfil do hello filho é toocalculate usado Olá a integridade geral do perfil do hello filho. Essas informações de integridade são propagadas Olá aninhado perfil hierarquia. Olá perfil pai usa essa integridade agregada toodetermine se o perfil toodirect tráfego toohello filho. Consulte Olá [perguntas frequentes sobre](traffic-manager-FAQs.md#traffic-manager-nested-profiles) para obter detalhes completos sobre o monitoramento de integridade de perfis aninhados.

Retornando o exemplo anterior toohello, suponha que a falha de implantação de produção de hello na Europa Ocidental. Por padrão, o perfil de 'child' hello direciona todas as implantações de teste de toohello de tráfego. Se a implantação de teste Olá também falhar, o perfil de pai de saudação determina que o perfil filho Olá não deve receber tráfego desde que todos os pontos de extremidade filho estão em estado íntegros. Em seguida, perfil pai de saudação distribui tráfego toohello outras regiões.

![Failover de perfil aninhado (comportamento padrão)][3]

Talvez você esteja satisfeito com essa organização. Ou você pode se preocupar que todo o tráfego de Ocidental agora será toohello implantação de teste em vez do tráfego de um subconjunto limitado. Independentemente de integridade de saudação do hello testar a implantação, você desejar toofail pela toohello outras regiões quando ocorre falha na implantação de produção de hello na Europa Ocidental. tooenable esse failover, você pode especificar o parâmetro de 'MinChildEndpoints' hello ao configurar o perfil do hello filho como um ponto de extremidade no perfil do pai de saudação. parâmetro Hello determina o número mínimo de saudação de pontos de extremidade disponíveis no perfil filho de saudação. valor padrão de saudação é '1'. Para este cenário, você deve definir Olá too2 de valor de MinChildEndpoints. Abaixo desse limite, o perfil de pai de saudação considera Olá filho todo perfil toobe indisponível e direciona o tráfego toohello outros pontos de extremidade.

Olá figura a seguir ilustra essa configuração:

![Failover de Perfil Aninhado com “MinChildEndpoints” = 2][4]

> [!NOTE]
> Olá método de roteamento de tráfego 'Priority' distribui todos os tráfego tooa único ponto de extremidade. Portanto, não há muita utilidade em uma configuração de MinChildEndpoints diferente de “1” para um perfil filho.

## <a name="example-3-prioritized-failover-regions-in-performance-traffic-routing"></a>Exemplo 3: regiões de failover priorizadas no roteamento de tráfego de "Desempenho"

comportamento padrão Olá Olá método de roteamento de tráfego 'Desempenho' é projetado tooavoid excesso carregar Olá lado mais próximo ponto de extremidade e fazendo com que uma série de falhas em cascata. Quando um ponto de extremidade falha, o todo o tráfego que poderia ter sido direcionado toothat de ponto de extremidade é igualmente distribuído toohello outros pontos de extremidade em todas as regiões.

![Roteamento de tráfego por “desempenho” com failover padrão][5]

No entanto, suponha que você preferir Olá Ocidental tráfego failover tooWest nos e direcionar somente regiões do tráfego tooother quando ambos os pontos de extremidade não estão disponíveis. Você pode criar essa solução com um perfil filho Olá método de roteamento de tráfego 'Priority'.

![Tráfego de roteamento de “Desempenho” com failover preferencial][6]

Como ponto de extremidade do hello Ocidental tem prioridade maior do que o ponto de extremidade do hello Oeste dos EUA, todo o tráfego é enviado o ponto de extremidade do toohello Ocidental quando ambos os pontos de extremidade estão online. Se Ocidental falhar, o tráfego é direcionado tooWest dos EUA. Com perfil Olá aninhado, o tráfego é direcionado tooEast Ásia somente quando falharem Ocidental e Oeste dos EUA.

É possível repetir esse padrão para todas as regiões. Substitua todos os três pontos de extremidade no perfil de pai Olá três perfis filho, cada uma delas fornecendo uma sequência com prioridade de failover.

## <a name="example-4-controlling-performance-traffic-routing-between-multiple-endpoints-in-hello-same-region"></a>Exemplo 4: Controlando o tráfego "Desempenho" roteamento entre vários pontos de extremidade Olá mesmo região

Suponha que Olá 'Desempenho' do método de roteamento de tráfego é usado em um perfil que tem mais de um ponto de extremidade em uma determinada região. Por padrão, o tráfego direcionado toothat região é distribuído uniformemente em todos os pontos de extremidade disponíveis nessa região.

![Roteamento de tráfego por “desempenho” com distribuição de tráfego na região (comportamento padrão)][7]

Em vez de adicionar vários pontos de extremidade na Europa Ocidental, esses pontos de extremidade são fechados em um perfil filho separado. perfil do Hello filho é adicionado toohello pai como ponto de extremidade somente na Europa Ocidental hello. as configurações de saudação no perfil de filho de saudação podem controlar a distribuição de tráfego Olá com Europa Ocidental habilitando o roteamento de tráfego baseado em prioridade ou ponderado dentro dessa região.

![Roteamento de tráfego por “desempenho” com distribuição de tráfego na região personalizado][8]

## <a name="example-5-per-endpoint-monitoring-settings"></a>Exemplo 5: configurações de monitoramento por ponto de extremidade

Suponha que você está usando Traffic Manager toosmoothly migrar tráfego de uma local herdados site da web tooa novo baseado em nuvem versão hospedada no Azure. Para o site herdado do hello, você deseja toouse Olá HomePage URI toomonitor a integridade do site. Mas para a nova versão baseada em nuvem Olá você estiver implementando uma página de monitoramento personalizada (caminho ' / monitor.aspx') que inclui verificações adicionais.

![Monitoramento do ponto de extremidade do Gerenciador de Tráfego (comportamento padrão)][9]

configurações de monitoramento de saudação em um perfil do Gerenciador de tráfego se aplicam a pontos de extremidade tooall dentro de um único perfil. Com perfis aninhados, você usa um perfil diferente filho por site toodefine diferente configurações de monitoramento.

![Monitoramento do ponto de extremidade do Gerenciador de Tráfego com definições por ponto de extremidade][10]

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre [perfis do Gerenciador de Tráfego](traffic-manager-overview.md)

Saiba como muito[criar um perfil do Gerenciador de tráfego](traffic-manager-create-profile.md)

<!--Image references-->
[1]: ./media/traffic-manager-nested-profiles/figure-1.png
[2]: ./media/traffic-manager-nested-profiles/figure-2.png
[3]: ./media/traffic-manager-nested-profiles/figure-3.png
[4]: ./media/traffic-manager-nested-profiles/figure-4.png
[5]: ./media/traffic-manager-nested-profiles/figure-5.png
[6]: ./media/traffic-manager-nested-profiles/figure-6.png
[7]: ./media/traffic-manager-nested-profiles/figure-7.png
[8]: ./media/traffic-manager-nested-profiles/figure-8.png
[9]: ./media/traffic-manager-nested-profiles/figure-9.png
[10]: ./media/traffic-manager-nested-profiles/figure-10.png
