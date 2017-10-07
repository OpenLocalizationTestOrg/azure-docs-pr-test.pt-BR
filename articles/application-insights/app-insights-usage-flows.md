---
title: "padrões de navegação do usuário aaaAnalyze com fluxos de usuário no Azure Application Insights | Documentos da Microsoft"
description: "Analise como os usuários navegam entre páginas de saudação e os recursos de seu aplicativo web."
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 08/02/2017
ms.author: cfreeman
ms.openlocfilehash: d3f35dc78e9874e4b7974604bf91c40a5e5b78eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-user-navigation-patterns-with-user-flows-in-application-insights"></a>Analisar padrões de navegação do usuário com o Fluxos de Usuário no Azure Application Insights

![Ferramenta Fluxos de Usuário do Application Insights](./media/app-insights-usage-flows/flows.png)

ferramenta de usuário flui Olá visualiza como usuários navegam entre páginas hello e recursos do seu site. Isso é ótimo para responder a perguntas como:
* Como os usuários navegam para outra página em seu site?
* Em que os usuários clicam em uma página em seu site?
* Onde estão Olá coloca usuários variação maior parte do seu site?
* Há locais onde os usuários repetição Olá mesma ação repetidamente?

ferramenta de usuário flui Olá começa em um modo de exibição de página inicial ou um evento que você especificar. Este modo de exibição de página ou evento personalizado, o usuário flui determinado mostra Olá modos de exibição de página e eventos personalizados que os usuários enviados imediatamente depois durante uma sessão, duas etapas posteriormente, e assim por diante. Linhas de espessura variada mostram quantas vezes cada caminho foi seguido por usuários. Nós especiais "Sessão foi finalizada" mostram quantos usuários enviados sem exibições de página ou eventos personalizados após Olá precede o nó, realce que os usuários provavelmente deixam seu site.



> [!NOTE]
> O recurso do Application Insights deve conter exibições de página ou ferramenta de usuário flui de saudação do eventos personalizados toouse. [Saiba como tooset sua página de toocollect aplicativo exibe automaticamente com hello SDK de JavaScript do Application Insights](app-insights-javascript.md).
> 
> 

## <a name="start-by-choosing-an-initial-page-view-or-custom-event"></a>Comece escolhendo uma exibição de página ou um evento personalizado inicial

![Escolha um evento inicial para o Fluxos de Usuário](./media/app-insights-usage-flows/flows-initial-event.png)

tooget iniciado a responder perguntas com a ferramenta de usuário flui Olá, escolha um modo de exibição de página inicial ou tooserve do evento personalizado como Olá ponto de partida para visualização de saudação:
1. Clique em link Olá Olá "o que os usuários fazer depois de...?" título ou botão de edição de hello. 
2. Na lista suspensa de "Evento inicial" Olá, selecione um modo de exibição de página ou o evento personalizado.
3. Clique em "Criar gráfico".

coluna de "Etapa 1" de saudação de visualização de saudação mostra o que os usuários foram com mais frequência logo após o evento inicial hello, ordenadas de cima para baixo de tooleast mais frequente. Olá "Etapa 2" e mostrar as colunas subsequentes que os usuários foram depois disso, criando uma imagem de todos os usuários de maneiras Olá navegar por meio de seu site.

Por padrão, a ferramenta de usuário flui de saudação a amostra aleatória somente Olá últimas 24 horas de modos de exibição de página e o evento personalizado do seu site. Você pode aumentar o intervalo de tempo de saudação e alterar Olá equilíbrio entre desempenho e precisão para amostragem aleatória, no menu de Editar saudação.

Se alguns dos modos de exibição de página hello e eventos personalizados não tooyou relevante, clique em hello "X" em nós Olá deseja toohide. Depois de selecionar nós Olá você deseja toohide, clique botão de "Criar gráfico" hello abaixo visualização hello. toosee todos os nós de saudação você ocultou, clique botão de edição hello e examine a seção de "Excluído eventos" hello.

Se os modos de exibição de página eventos personalizados estão faltando ou que você espera que toosee na visualização de saudação:
* Consulte a seção "Excluídos eventos" hello no menu de Editar saudação.
* Use controle de "Nível de detalhe" hello em Olá Editar tooinclude menos frequente eventos na visualização de saudação.
* Se o modo de exibição de página hello ou evento personalizado que você espera que é enviado com pouca frequência pelos usuários, tente crescentes intervalo de tempo de saudação de visualização de saudação no menu de Editar saudação.
* Certifique-se de que modo de exibição de página de saudação ou eventos personalizados que você espera que está configurada toobe coletado pelo Olá SDK do Application Insights no código-fonte do seu site Olá. [Saiba mais sobre como coletar eventos personalizados.](app-insights-api-custom-events-metrics.md)

Se você quiser toosee mais etapas na visualização hello, use hello "Número de etapas" deslizante no hello menu Editar.

## <a name="after-visiting-a-page-or-feature-where-do-users-go-and-what-do-they-click"></a>Depois de visitar uma página ou um recurso, para onde os usuários vão e no que eles clicam?

![Use o usuário flui toounderstand onde os usuários clicam em](./media/app-insights-usage-flows/flows-one-step.png)

Se o evento inicial é uma exibição de página, Olá primeira coluna ("etapa 1") de visualização de saudação é um toounderstand de maneira rápida que os usuários foram imediatamente depois de visitar a página hello. Tente abrir o site em um toohello de próxima janela Visualização de usuário flui. Compare suas expectativas de como os usuários interagem com lista de toohello Olá página de eventos na coluna do hello "Etapa 1". Geralmente, um elemento de interface do usuário na página de saudação que pareça insignificante tooyour equipe pode ser entre hello mais usadas na página de saudação. Pode ser um ponto de partida excelente para o site de tooyour de melhorias de design.

Se o evento inicial é um evento personalizado, a saudação primeira coluna mostra a quais usuários tinha apenas depois de executar essa ação. Assim como acontece com modos de exibição de página, considere se Olá observado o comportamento dos usuários corresponde expectativas e metas da sua equipe. Se o evento inicial selecionado é "Item adicionado tooShopping carrinho", por exemplo, procure toosee se "Go tooCheckout" e "Concluída compra" aparecem na visualização de saudação logo depois. Se o comportamento do usuário é muito diferente de suas expectativas, use Olá visualização toounderstand como os usuários estão obtendo "capturados" por design atual do site.

## <a name="where-are-hello-places-that-users-churn-most-from-your-site"></a>Onde estão Olá coloca usuários variação maior parte do seu site?

Observação para os nós "Sessão foi finalizada" que aparecem alto-up de uma coluna em visualização hello, especialmente no início em um fluxo. Isso significa que muitos usuários provavelmente formados do seu site depois de seguir Olá caminho anterior de páginas e interações de interface do usuário. Algumas vezes a rotatividade é esperada – depois de concluir uma compra em um site de comércio eletrônico, por exemplo – mas geralmente a rotatividade é um sinal de problemas de design, baixo desempenho ou outros problemas com seu site, os quais podem ser melhorados.

Tenha em mente que nós "Sessão finalizada" são baseados apenas na telemetria coletada por esse recurso do Application Insights. Se Application Insights não receber a telemetria para determinados interações do usuário, os usuários podem ainda têm interagir com seu site essas formas depois que a ferramenta de usuário flui de saudação diz Olá sessão foi finalizada.

## <a name="are-there-places-where-users-repeat-hello-same-action-over-and-over"></a>Há locais onde os usuários repetição Olá mesma ação repetidamente?

Procure uma exibição de página ou um evento personalizado que é repetido por muitos usuários em etapas posteriores em visualização hello. Geralmente, isso significa que os usuários estão executando ações repetitivas no seu site. Se você encontrar a repetição, pense sobre design de saudação do seu site de alteração ou adição de repetição de tooreduce nova funcionalidade. Por exemplo, adicione a funcionalidade de edição em massa se você encontrar usuários executando ações repetitivas em cada linha de um elemento de tabela.

## <a name="common-questions"></a>Perguntas comuns

### <a name="why-do-steps-appear-disconnected"></a>Por que as etapas aparecem desconectadas?

![Fluxos de Usuário com etapas desconectadas](./media/app-insights-usage-flows/flows-disconnected.png)

Se etapas (colunas) em uma visualização de usuário flui são desconectadas, significa que nenhum dos caminhos de saudação executados por usuários entre etapas Olá foram frequente o bastante toobe mostrado. tooshow menos eventos frequentes na visualização de saudação para que etapas de saudação aparecem conectadas, ajuste o controle deslizante de "Nível de detalhe" de saudação no menu de Editar saudação.

### <a name="does-hello-initial-event-represent-hello-first-time-hello-event-appears-in-a-session-or-any-time-it-appears-in-a-session"></a>Olá evento inicial representam Olá primeiro tempo Olá evento é exibido em uma sessão ou qualquer momento ele aparece em uma sessão?

evento de saudação inicial na visualização de saudação representa apenas Olá primeira vez que um usuário que enviou essa exibição de página ou um evento personalizado durante uma sessão. Se os usuários podem enviar o evento inicial Olá várias vezes em uma sessão, então a coluna de "Etapa 1" hello apenas mostra como os usuários se comportam após Olá *primeiro* instância do evento inicial, nem todas as instâncias.

## <a name="next-steps"></a>Próximas etapas

* [Visão geral do uso](app-insights-usage-overview.md)
* [Usuários, Sessões e Eventos](app-insights-usage-segmentation.md)
* [Retenção](app-insights-usage-retention.md)
* [Adicionando eventos personalizados tooyour aplicativo](app-insights-api-custom-events-metrics.md)
