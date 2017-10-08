---
title: "o que é o Azure Application Insights de AAA? | Microsoft Docs"
description: Gerenciamento de desempenho de aplicativo e acompanhamento de uso do seu aplicativo web online.  Detectar, realizar triagem e diagnosticar problemas, entender como as pessoas usam o seu aplicativo.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 379721d1-0f82-445a-b416-45b94cb969ec
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/14/2017
ms.author: bwren
ms.openlocfilehash: d2596f53a36991fcd08551e6395ece68a5801e39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-application-insights"></a>O que é o Application Insights?
O Application Insights é um serviço de gerenciamento de desempenho de aplicativo (APM) extensível para desenvolvedores da Web em várias plataformas. Use-toomonitor seu aplicativo web em tempo real. Ele detectará anomalias de desempenho automaticamente. Ele inclui uma análise rigorosa ferramentas toohelp que diagnosticar problemas e toounderstand que os usuários, na verdade, fazem com seu aplicativo.  Ele é projetado toohelp você continuamente melhorar o desempenho e usabilidade. Ele funciona para aplicativos em uma ampla variedade de plataformas, incluindo .NET, Node.js e J2EE, hospedado no local ou na nuvem hello. Ele se integra ao seu processo de devOps e tem conexão pontos tooa variedade de ferramentas de desenvolvimento.

![Disponha em gráficos as estatísticas de atividade do usuário ou analise detalhadamente eventos específicos.](./media/app-insights-overview/00-sample.png)

[Dê uma olhada animação de Introdução Olá](https://www.youtube.com/watch?v=fX2NtGrh-Y0).

## <a name="how-does-application-insights-work"></a>Como funciona o Application Insights?
Instalar um pacote de instrumentação pequeno em seu aplicativo e configurar um recurso do Application Insights no portal do Microsoft Azure hello. instrumentação Olá monitora seu aplicativo e envia o portal de toohello de dados de telemetria. (Olá aplicativo pode ser executado em qualquer lugar - ele não tem toobe hospedado no Azure.)

Você pode instrumentar não apenas aplicativo de serviço da web hello, mas também os componentes do plano de fundo e Olá JavaScript em páginas da web de saudação próprios. 

![Instrumentação de informações do aplicativo em seu aplicativo enviará telemetria tooyour recurso do Application Insights.](./media/app-insights-overview/01-scheme.png)


Além disso, você pode efetuar pull de telemetria de ambientes de host hello como contadores de desempenho, o diagnóstico do Azure ou logs de Docker. Você também pode configurar testes da web que periodicamente enviar solicitações sintéticas tooyour serviço de web.

Todos esses fluxos de telemetria são integrados no hello portal do Azure, onde você pode aplicar poderosa analíticos e dados brutos de toohello de ferramentas de pesquisa.


### <a name="whats-hello-overhead"></a>O que é a sobrecarga de Olá?
impacto de Olá no desempenho do aplicativo é muito pequeno. As chamadas de acompanhamento não são bloqueadas, além de serem colocadas em lote e enviadas em um thread separado.

## <a name="what-does-application-insights-monitor"></a>O que o Application Insights monitora?

Informações do aplicativo é destinado a equipe de desenvolvimento hello, toohelp você entender o desempenho do seu aplicativo e como ele está sendo usado. Ele monitora:

* **Taxas de solicitação, tempos de resposta e taxas de falha** - descubra quais páginas estão mais populares, em que momentos do dia, e onde os usuários estão. Confira as páginas que têm melhor desempenho. Se as taxas de falha e os tempos de resposta ficam altos quando há mais solicitações, possivelmente você tem um problema de alocação de recursos. 
* **Taxas de dependência, tempos de resposta e taxas de falha** - descubra se os serviços externos estão atrasando você.
* **Exceções** - analisar estatísticas de saudação agregada, ou selecionar instâncias específicas e analisar o rastreamento de pilha hello e solicitações relacionadas. A maioria das exceções de navegador e servidor são relatadas.
* **Exibições de página e o desempenho de carregamento** - relatados por navegadores dos usuários.
* **Chamadas AJAX** de páginas da web - taxas, tempos de resposta e taxas de falha.
* **Contagens de seção e usuários**.
* **Contadores de desempenho** de suas máquinas de servidor Linux ou Windows server, como CPU, memória e uso da rede. 
* **Diagnósticos de host** do Docker ou do Azure. 
* **Logs de rastreamento de diagnóstico** do seu aplicativo - para que você possa correlacionar eventos de rastreamento com solicitações.
* **Eventos personalizados e métricas** que você escreva por conta própria no código de cliente ou servidor hello, tootrack eventos de negócios, como itens vendidos ou jogos ganha.

## <a name="where-do-i-see-my-telemetry"></a>Onde posso encontrar minha telemetria?

Há maneiras tooexplore seus dados. Confira estes artigos:

|  |  |
| --- | --- |
| [**Detecção inteligente e alertas manuais**](app-insights-proactive-diagnostics.md)<br/>Alertas automáticos adaptar padrões normais de tooyour do aplicativo de telemetria e o gatilho quando há algo fora saudação padrão. Você também pode [definir alertas](app-insights-alerts.md) em níveis específicos de métricas padrão ou personalizadas. |![Exemplo de alerta](./media/app-insights-overview/alerts-tn.png) |
| [**Mapa do aplicativo**](app-insights-app-map.md)<br/>componentes de saudação do seu aplicativo, com as principais métricas e alertas. |![Mapa do aplicativo](./media/app-insights-overview/appmap-tn.png)  |
| [**Criador de perfil**](app-insights-profiler.md)<br/>Inspecione os perfis de execução de saudação de solicitações de amostras. |![Criador de perfil](./media/app-insights-overview/profiler.png) |
| [**Análise de uso**](app-insights-usage-overview.md)<br/>Analise a retenção e a segmentação de usuários.|![Ferramenta de retenção](./media/app-insights-overview/retention.png) |
| [**Pesquisa de diagnóstico para dados da instância**](app-insights-diagnostic-search.md)<br/>pesquise e filtre eventos como solicitações, exceções, chamadas de dependência, rastreamentos de log e exibições de página.  |![Como pesquisar telemetria](./media/app-insights-overview/search-tn.png) |
| [**Metrics Explorer para os dados agregados**](app-insights-metrics-explorer.md)<br/>explore, filtre e segmente dados agregados, como taxas de solicitações, falhas e exceções; tempos de resposta e tempos de carregamento de página. |![Métricas](./media/app-insights-overview/metrics-tn.png) |
| [**Painéis**](app-insights-dashboards.md#dashboards)<br/>faça um mashup de dados de vários recursos e compartilhe com outras pessoas. Excelente para aplicativos de vários componentes e para a exibição contínua em sala de equipe hello. |![Exemplos de painéis](./media/app-insights-overview/dashboard-tn.png) |
| [**Live Metrics Stream**](app-insights-live-stream.md)<br/>Quando você implanta uma nova compilação, assista a esses toomake de indicadores de desempenho em tempo quase real se tudo está funcionando conforme o esperado. |![Exemplo de métricas ao vivo](./media/app-insights-overview/live-metrics-tn.png) |
| [**Analytics**](app-insights-analytics.md)<br/>responda perguntas difíceis sobre o desempenho e o uso do seu aplicativo usando essa poderosa linguagem de consulta. |![Exemplo de análise](./media/app-insights-overview/analytics-tn.png) |
| [**Visual Studio**](app-insights-visual-studio.md)<br/>Ver os dados de desempenho no código de saudação. Vá toocode de rastreamentos de pilha.|![Visual Studio](./media/app-insights-overview/visual-studio-tn.png) |
| [**Depurador de instantâneo**](app-insights-snapshot-debugger.md)<br/>Depure instantâneos tirado como exemplo de operações ao vivo, com valores de parâmetro.|![Visual Studio](./media/app-insights-overview/snapshot.png) |
| [**Power BI**](app-insights-export-power-bi.md)<br/>Integre as métricas de uso com outro business intelligence.| ![Power BI](./media/app-insights-overview/power-bi.png)|
| [**REST API**](https://dev.applicationinsights.io/)<br/>Escreva código toorun consultas sobre o métricas e os dados brutos.| ![API REST](./media/app-insights-overview/rest-tn.png) |
| [**Exportação contínua**](app-insights-export-telemetry.md)<br/>Exportação em massa de dados brutos toostorage assim que elas chegam. |![Exportação](./media/app-insights-overview/export-tn.png) |

## <a name="how-do-i-use-application-insights"></a>Como usar o Application Insights?

### <a name="monitor"></a>Monitoramento
Instale o Application Insights no seu aplicativo, configure os [testes de disponibilidade da web](app-insights-monitor-web-app-availability.md) e:

* Configurar um [painel](app-insights-dashboards.md) sua tookeep de sala da equipe de olho na carga, a capacidade de resposta e o desempenho de saudação de suas dependências, página carregamentos e chamadas AJAX.
* Descobrir quais são hello mais lenta e a maioria das solicitações com falha.
* Inspecionar [fluxo ao vivo](app-insights-live-stream.md) quando você implanta uma nova versão, tooknow imediatamente sobre qualquer degradação.

### <a name="detect-diagnose"></a>Detectar, diagnosticar
Quando você recebe um alerta ou descobre um problema:

* Avalie quantos usuários são afetados.
* Correlacione falhas a exceções, a chamadas de dependência e a rastreamentos.
* Examine o criador de perfil, instantâneos, despejos de pilha e logs de rastreamento.

### <a name="build-measure-learn"></a>Compilar, medir, aprender
[Medir a eficácia do hello](app-insights-usage-overview.md) de cada novo recurso que você implanta.

* Planejar toomeasure como os clientes usam UX novo ou recursos de negócios.
* Escreva a telemetria personalizada em seu código.
* Ciclo de desenvolvimento Avançar Olá base na evidência de disco rígida da sua telemetria.

## <a name="get-started"></a>Introdução
Application Insights é um dos muitos serviços hospedados no Microsoft Azure e telemetria é enviado existe para análise e apresentação de saudação. Portanto, antes de fazer qualquer outra coisa, você precisará de uma assinatura muito[Microsoft Azure](http://azure.com). Cabe toosign livre e se você escolher Olá básico [preços plano](https://azure.microsoft.com/pricing/details/application-insights/) do Application Insights, há nenhum encargo até que seu aplicativo aumentou uso substancial toohave. Se sua organização já tiver uma assinatura, eles podem adicionar sua tooit de conta da Microsoft.

Há várias maneiras tooget iniciado. Comece com o que funciona melhor para você. Você pode adicionar Olá outros mais tarde.

* **No tempo de execução: instrumentar seu aplicativo web no servidor de saudação.** Evita qualquer código de toohello de atualização. É necessário um servidor de tooyour de acesso de administrador.
  * [**IIS local ou em uma VM**](app-insights-monitor-performance-live-website-now.md)
  * [**Aplicativo Web ou VM do Azure**](app-insights-monitor-performance-live-website-now.md)
  * [**J2EE**](app-insights-java-live.md)
* **No tempo de desenvolvimento: Adicione código de tooyour do Application Insights.** Permite que você toowrite telemetria e tooinstrument back-end e de área de trabalho aplicativos personalizados.
  * [Visual Studio](app-insights-asp-net.md) 2013 atualização 2 ou posterior.
  * Java no [Eclipse](app-insights-java-eclipse.md) ou em [outras ferramentas](app-insights-java-get-started.md)
  * [Node.js](app-insights-nodejs.md)
  * [Outras plataformas](app-insights-platforms.md)
* **[Instrumentar suas páginas da Web](app-insights-javascript.md)** para exibição de página, AJAX e outras telemetrias do lado do cliente.
* **[Testes de disponibilidade](app-insights-monitor-web-app-availability.md)** - execute o ping de seu site regularmente de nossos servidores.


## <a name="next-steps"></a>Próximas etapas
Introdução ao tempo de execução com:

* [Servidor IIS](app-insights-monitor-performance-live-website-now.md)
* [Servidor J2EE](app-insights-java-live.md)

Introdução ao tempo de desenvolvimento com:

* [ASP.NET](app-insights-asp-net.md)
* [Java](app-insights-java-get-started.md)
* [Node.js](app-insights-nodejs.md)

## <a name="support-and-feedback"></a>Suporte e comentários
* Perguntas e problemas:
  * [Solução de problemas][qna]
  * [Fórum do MSDN](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=ApplicationInsights)
  * [StackOverflow](http://stackoverflow.com/questions/tagged/ms-application-insights)
* Suas sugestões:
  * [UserVoice](https://visualstudio.uservoice.com/forums/357324)
* Blog:
  * [Blog do Application Insights](https://azure.microsoft.com/blog/tag/application-insights)

## <a name="videos"></a>Vídeos

[![Introdução animada](./media/app-insights-overview/video-front-1.png)](https://www.youtube.com/watch?v=fX2NtGrh-Y0)

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

<!--Link references-->

[android]: https://github.com/Microsoft/ApplicationInsights-Android
[azure]: ../insights-perf-analytics.md
[client]: app-insights-javascript.md
[desktop]: app-insights-windows-desktop.md
[detect]: app-insights-detect-triage-diagnose.md
[greenbrown]: app-insights-asp-net.md
[ios]: https://github.com/Microsoft/ApplicationInsights-iOS
[java]: app-insights-java-get-started.md
[knowUsers]: app-insights-web-track-usage.md
[platforms]: app-insights-platforms.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
