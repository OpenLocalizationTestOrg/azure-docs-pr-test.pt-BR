---
title: "Tendências de aaaAnalyzing no Visual Studio | Microsoft Docs"
description: "Analisar, visualizar e explorar tendências em sua telemetria do Application Insights no Visual Studio."
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 3150c6fc-2691-44f6-a290-fc5cd68e692a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: 5c623ec040363f05e80ca927dc8855eb016adc99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyzing-trends-in-visual-studio"></a>Análise de tendências no Visual Studio
ferramenta do Application Insights Trends Olá visualiza como eventos de telemetria importantes do seu aplicativo web mudam ao longo do tempo, ajudando você a identificar rapidamente problemas e anomalias. Vinculando toomore diagnósticas informações detalhadas, tendências podem ajudá-lo a melhorar o desempenho do seu aplicativo, rastrear as causas de saudação de exceções e descobrir ideias de seus eventos personalizados.

![Janela de Tendências de exemplo](./media/app-insights-visual-studio-trends/app-insights-trends-hero-750.png)

## <a name="configure-your-web-app-for-application-insights"></a>Configurar seu aplicativo Web para o Application Insights

Se você ainda não fez isso, [configure seu aplicativo Web para o Application Insights](app-insights-overview.md). Isso permite que ele portal do Application Insights do toosend telemetria toohello. ferramenta de tendências de saudação lê telemetria hello a partir daí.

A ferramenta Tendências do Application Insights está disponível no Visual Studio 2015 atualização 3 e posteriores.

## <a name="open-application-insights-trends"></a>Abrir o Application Insights Trends
janela do Application Insights Trends de saudação tooopen:

* No botão de barra de ferramentas do Application Insights hello, escolha **explorar tendências de telemetria**, ou
* No menu de contexto do projeto hello, escolha **Application Insights > explorar tendências de telemetria**, ou
* Na barra de menus do Visual Studio hello, escolha **exibição > outras janelas > Application Insights Trends**.

Você pode ver um tooselect solicitar um recurso. Clique em **selecione um recurso**, entrar com uma assinatura do Azure, em seguida, escolha um recurso do Application Insights na lista Olá para o qual você gostaria de tendências de telemetria tooanalyze.

## <a name="choose-a-trend-analysis"></a>Escolha uma análise de tendência
![Menu dos tipos comuns de análise de tendência](./media/app-insights-visual-studio-trends/app-insights-trends-1-750.png)

Introdução ao escolher uma das cinco análises tendência comuns, cada analisando dados de saudação últimas 24 horas:

* **Investigar problemas de desempenho com suas solicitações do servidor** -solicitações feitas tooyour serviço, agrupado por tempos de resposta
* **Analise os erros em suas solicitações do servidor** -solicitações feitas tooyour serviço, agrupado por código de resposta HTTP
* **Examine as exceções de saudação em seu aplicativo** -exceções a partir de seu serviço, agrupados por tipo de exceção
* **Verificar o desempenho de saudação de dependências do aplicativo** -serviços chamados por seu serviço, agrupados por tempos de resposta
* **Inspecionar seus eventos personalizados** - eventos personalizados que você configurou para o serviço, agrupados por tipo de evento.

Pré-compilado análises estiverem disponíveis de saudação **exibir tipos comuns de análise de telemetria** botão no canto superior esquerdo de saudação da janela de tendências de saudação.

## <a name="visualize-trends-in-your-application"></a>Visualizar tendências em seu aplicativo
O Application Insights Trends cria uma visualização de série de tempo de telemetria de seu aplicativo. Cada visualização de série de tempo exibe um tipo de telemetria, agrupado por uma propriedade dessa telemetria, em algum intervalo de tempo. Por exemplo, convém tooview solicitações ao servidor, agrupadas por país de saudação do qual foram originados, sobre Olá últimas 24 horas. Neste exemplo, cada bolha na visualização de saudação representa uma contagem de solicitações do servidor de saudação para alguns país/região durante uma hora.

Use controles de saudação na parte superior de saudação do hello janela tooadjust quais tipos de telemetria exibir. Primeiro, escolha os tipos de telemetria Olá no qual você está interessado:

* **Tipo de telemetria** - solicitações ao servidor, exceções, dependências ou eventos personalizados
* **Intervalo de tempo** - em qualquer lugar da saudação de últimos 30 minutos toohello últimos 3 dias
* **Agrupar por** - tipo de exceção, ID do problema, país/região e muito mais.

Em seguida, clique em **analisar a telemetria** toorun consulta de saudação.

toonavigate entre bolhas em visualização hello:

* Clique em tooselect uma bolha, que atualiza os filtros de saudação na parte inferior da saudação da janela hello, resumindo os eventos de saudação apenas que ocorreram durante um período de tempo específico
* Clique duas vezes em uma ferramenta de pesquisa bolhas toonavigate toohello e ver todos os eventos de telemetria individuais Olá que ocorreram durante o período de tempo
* CTRL + clique bolhas toode-select na visualização de saudação.

> [!TIP]
> Olá tendências e pesquisa ferramentas funcionam em conjunto toohelp você identificar as causas de saudação de problemas em seu serviço entre milhares de eventos de telemetria. Por exemplo, se uma tarde os clientes observarem que seu aplicativo está respondendo menos, comece com Tendências. Analise solicitações feitas tooyour serviço sobre Olá últimas horas, agrupados pelo tempo de resposta. Verifique se há um cluster excepcionalmente alto de solicitações lentas. Em seguida, clique duas vezes em que bolhas toogo toohello a ferramenta de pesquisa, eventos de solicitação toothose filtrado. Da pesquisa, você pode explorar o conteúdo de saudação dessas solicitações e navegar pelo código toohello envolvidos tooresolve problema de saudação.
> 
> 

## <a name="filter"></a>Filter
Descobrir tendências mais específicas com controles de filtro de saudação na parte inferior da saudação da janela de saudação. tooapply um filtro, clique em seu nome. Você pode alternar rapidamente entre as tendências de toodiscover filtros diferentes que podem ser ocultas em uma dimensão específica da sua telemetria. Se você aplicar um filtro em uma dimensão, como o tipo de exceção, os filtros em outras dimensões permanecem clicáveis mesmo que aparecer esmaecida. tooun-aplicar um filtro, clique nele novamente. CTRL + clique tooselect Olá de vários filtros na mesma dimensão.

![Filtros de tendência](./media/app-insights-visual-studio-trends/TrendsFiltering-750.png)

E se você quiser tooapply vários filtros? 

1. Aplica filtro primeiro hello. 
2. Clique em Olá **aplique os filtros selecionados e consulte novamente** botão por nome de saudação da dimensão de saudação do primeiro filtro. Isso fará a consulta novamente sua telemetria para apenas os eventos que correspondem ao filtro de primeira hello. 
3. Aplique um segundo filtro. 
4. Repita as tendências de toofind de processo de saudação em subconjuntos específicos de sua telemetria. Por exemplo, solicitações ao servidor denominadas "GET Home/Index" *e* que veio da Alemanha *e* que recebeu um código de resposta 500. 

tooun-aplicar um desses filtros, clique em Olá **remover filtros selecionados e consulte novamente** botão para a dimensão de saudação.

![Vários filtros](./media/app-insights-visual-studio-trends/TrendsFiltering2-750.png)

## <a name="find-anomalies"></a>Encontrar anomalias
ferramenta de tendências de saudação pode realçar bolhas de eventos que são bolhas anormais tooother comparados em Olá mesma série temporal. No menu suspenso tipo de exibição de saudação, escolha **contagens em bucket de tempo (destacar anomalias)** ou **porcentagens em bucket de tempo (destacar anomalias)**. Bolhas vermelhas são anomalias. Anomalias são definidas como bolhas com contagens/porcentagens superiores 2.1 vezes Olá desvio padrão de saudação contagens/porcentagens que ocorreram em Olá últimos dois períodos de tempo (48 horas se você estiver exibindo Olá últimos 24 horas, etc.).

![Pontos coloridos indicam anomalias](./media/app-insights-visual-studio-trends/TrendsAnomalies-750.png)

> [!TIP]
> O realce de anomalias é particularmente útil para localizar exceções na série de tempo de bolhas pequenas que podem parecer ter o mesmo tamanho.  
> 
> 

## <a name="next"></a>Próximas etapas
|  |  |
| --- | --- |
| **[Trabalhando com o Application Insights no Visual Studio](app-insights-visual-studio.md)**<br/>Pesquisar telemetria, ver dados em CodeLens e configurar o Application Insights. Tudo no Visual Studio. |![Clique com botão direito hello e escolha o Application Insights, pesquisa](./media/app-insights-visual-studio-trends/34.png) |
| **[Adicionar mais dados](app-insights-asp-net-more.md)**<br/>Monitorar o uso, a disponibilidade, as dependências e as exceções. Integrar rastreamentos de estruturas de logs. Escrever telemetria personalizada. |![Visual Studio](./media/app-insights-visual-studio-trends/64.png) |
| **[Trabalhando com o portal do Application Insights Olá](app-insights-dashboards.md)**<br/>Painéis, poderosas ferramentas de diagnóstico e análise, alertas, um mapa de dependências em tempo real de seu aplicativo e a exportação de telemetria. |![Visual Studio](./media/app-insights-visual-studio-trends/62.png) |

