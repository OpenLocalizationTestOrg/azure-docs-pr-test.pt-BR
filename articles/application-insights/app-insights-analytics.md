---
title: "aaaAnalytics - Olá poderosa ferramenta de pesquisa de informações de aplicativo do Azure | Microsoft Docs"
description: "Visão geral da análise, a ferramenta de diagnóstico avançados de pesquisa de saudação do Application Insights. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 0a2f6011-5bcf-47b7-8450-40f284274b24
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: d2b41e2fff7cc786e11fa3dfe94fc46f1b86e9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analytics-in-application-insights"></a>Análise no Application Insights
[Análise de](app-insights-analytics.md) é o recurso de pesquisa poderoso saudação do [Application Insights](app-insights-overview.md). Essas páginas descrevem a linguagem de consulta do Log Analytics. 

* **[Assistir ao vídeo introdutório Olá](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Faça o test drive análise sobre nossos dados simulados](https://analytics.applicationinsights.io/demo)**  se seu aplicativo não esteja enviando dados tooApplication Insights ainda.
* **[Roteiro de SQL-usuários](https://aka.ms/sql-analytics)**  converte as linguagens mais comuns de saudação.
* **[Referência de linguagem](app-insights-analytics-reference.md)**  Saiba como toouse todos os Olá recursos avançados do hello linguagem de consulta de análise de Log.


## <a name="queries-in-analytics"></a>Consultas na Análise
Uma consulta comum é uma tabela de *origem* seguida por vários *operadores* separados por `|`. 

Por exemplo, vamos descobrir qual período do cidadãos Olá dia Hyderabad tente nosso aplicativo web. E, enquanto estiver lá, vamos ver quais códigos de resultado são retornados solicitações tootheir HTTP. 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

Podemos contar endereços IP de cliente distintos, agrupá-los por hora de saudação do dia de saudação sobre Olá últimos 7 dias. 

> [!NOTE]
> resultados tooget fora Olá 24h anterior, inclua 'timestamp' explicitamente na consulta ou usar o menu suspenso do hello tempo intervalo.
>

Vamos exibir resultados de saudação com hello barra apresentação do gráfico, escolhendo toostack resultados Olá códigos de resposta diferentes:

![Escolha o gráfico de barras, os eixos x e y e a segmentação](./media/app-insights-analytics/020.png)

Parece que nosso aplicativo é mais popular na hora do almoço e na hora de dormir em Hyderabad. (Então, devemos investigar esses 500 códigos).

Também há operações estatísticas avançadas:

![Resultados de consulta estatística](./media/app-insights-analytics/025.png)

idioma Olá tem muitos recursos atraentes:


* [Filtre](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) a telemetria bruta de aplicativos por qualquer campo, incluindo suas métricas e propriedades personalizadas.
* [Una](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) várias tabelas: correlacione as solicitações com exibições de página, as chamadas de dependência, as exceções e os rastreamentos de log.
* [Agregações](https://docs.loganalytics.io/learn/tutorials/aggregations.html)estatísticas poderosas.
* Tão poderosos quanto SQL, mas muito mais fácil para consultas complexas: em vez de aninhamento de instruções, você direcionar dados de saudação do toohello de uma operação elementares lado.
* Visualizações imediatas e eficientes.
* [Fixar gráficos painéis tooAzure](app-insights-analytics-using.md#pin-to-dashboard).
* [Exportar consultas tooPower BI](app-insights-analytics-using.md#export-to-power-bi).
* Há um [API REST](https://dev.applicationinsights.io/) que você pode usar consultas toorun programaticamente, por exemplo do Powershell.


## <a name="connect-tooyour-application-insights-data"></a>Conecte-se a dados do Application Insights tooyour
Abra o Analytics na [folha de visão geral](app-insights-dashboards.md) de seu aplicativo no Application Insights: 

![Abra o portal.azure.com, abra o recurso do Application Insights e clique em Análise.](./media/app-insights-analytics/001.png)


## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a>Exemplos de consulta

Tente esses power de saudação tooillustrate explicações passo a passo do uso de análise:

 *  [Diagnóstico automático de picos e etapas ignoradas nas durações de solicitações](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [Analisar degradações de desempenho com análise de série temporal](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [Analisar as falhas do aplicativo com autocluster e diffpatterns](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [Detecções de forma avançadas com análise de série temporal](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [Usando deslizante janela operações tooanalyze uso do aplicativo (sem interrupção MAU/DAU etc)](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  [Detecção de interrupções de serviço com base na análise dos logs de depuração](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) e uma postagem de blog correspondente [aqui](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).
 *  [Criação de perfil de desempenho de aplicativos usando logs de depuração simples](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) e uma postagem de blog correspondente [aqui](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)
 *  [Medindo a duração de saudação para cada etapa no fluxo de código usando logs de depuração simples](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) e uma postagem de blog correspondente [aqui](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)
 *  [Analisar a simultaneidade usando logs de depuração simples](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) e uma postagem de blog correspondente [aqui](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)



## <a name="next-steps"></a>Próximas etapas
* É recomendável iniciar com hello [tour de idioma](app-insights-analytics-tour.md). 
* Saiba mais sobre [como usar a análise](app-insights-analytics-using.md). 
* [Referência da linguagem](app-insights-analytics-reference.md). 
