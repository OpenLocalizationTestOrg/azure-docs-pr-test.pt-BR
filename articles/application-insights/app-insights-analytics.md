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
# <a name="analytics-in-application-insights"></a><span data-ttu-id="d3e0f-103">Análise no Application Insights</span><span class="sxs-lookup"><span data-stu-id="d3e0f-103">Analytics in Application Insights</span></span>
<span data-ttu-id="d3e0f-104">[Análise de](app-insights-analytics.md) é o recurso de pesquisa poderoso saudação do [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d3e0f-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="d3e0f-105">Essas páginas descrevem a linguagem de consulta do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="d3e0f-105">These pages describe the Log Analytics query language.</span></span> 

* <span data-ttu-id="d3e0f-106">**[Assistir ao vídeo introdutório Olá](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="d3e0f-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="d3e0f-107">**[Faça o test drive análise sobre nossos dados simulados](https://analytics.applicationinsights.io/demo)**  se seu aplicativo não esteja enviando dados tooApplication Insights ainda.</span><span class="sxs-lookup"><span data-stu-id="d3e0f-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>
* <span data-ttu-id="d3e0f-108">**[Roteiro de SQL-usuários](https://aka.ms/sql-analytics)**  converte as linguagens mais comuns de saudação.</span><span class="sxs-lookup"><span data-stu-id="d3e0f-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates hello most common idioms.</span></span>
* <span data-ttu-id="d3e0f-109">**[Referência de linguagem](app-insights-analytics-reference.md)**  Saiba como toouse todos os Olá recursos avançados do hello linguagem de consulta de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="d3e0f-109">**[Language Reference](app-insights-analytics-reference.md)** Learn how toouse all hello powerful features of hello Log Analytics query language.</span></span>


## <a name="queries-in-analytics"></a><span data-ttu-id="d3e0f-110">Consultas na Análise</span><span class="sxs-lookup"><span data-stu-id="d3e0f-110">Queries in Analytics</span></span>
<span data-ttu-id="d3e0f-111">Uma consulta comum é uma tabela de *origem* seguida por vários *operadores* separados por `|`.</span><span class="sxs-lookup"><span data-stu-id="d3e0f-111">A typical query is a *source* table followed by a series of *operators* separated by `|`.</span></span> 

<span data-ttu-id="d3e0f-112">Por exemplo, vamos descobrir qual período do cidadãos Olá dia Hyderabad tente nosso aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="d3e0f-112">For example, let's find out what time of day hello citizens of Hyderabad try our web app.</span></span> <span data-ttu-id="d3e0f-113">E, enquanto estiver lá, vamos ver quais códigos de resultado são retornados solicitações tootheir HTTP.</span><span class="sxs-lookup"><span data-stu-id="d3e0f-113">And while we're there, let's see what result codes are returned tootheir HTTP requests.</span></span> 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

<span data-ttu-id="d3e0f-114">Podemos contar endereços IP de cliente distintos, agrupá-los por hora de saudação do dia de saudação sobre Olá últimos 7 dias.</span><span class="sxs-lookup"><span data-stu-id="d3e0f-114">We count distinct client IP addresses, grouping them by hello hour of hello day over hello past 7 days.</span></span> 

> [!NOTE]
> <span data-ttu-id="d3e0f-115">resultados tooget fora Olá 24h anterior, inclua 'timestamp' explicitamente na consulta ou usar o menu suspenso do hello tempo intervalo.</span><span class="sxs-lookup"><span data-stu-id="d3e0f-115">tooget results outside hello previous 24h, either include 'timestamp' explicitly in your query, or use hello time range drop-down menu.</span></span>
>

<span data-ttu-id="d3e0f-116">Vamos exibir resultados de saudação com hello barra apresentação do gráfico, escolhendo toostack resultados Olá códigos de resposta diferentes:</span><span class="sxs-lookup"><span data-stu-id="d3e0f-116">Let's display hello results with hello bar chart presentation, choosing toostack hello results from different response codes:</span></span>

![Escolha o gráfico de barras, os eixos x e y e a segmentação](./media/app-insights-analytics/020.png)

<span data-ttu-id="d3e0f-118">Parece que nosso aplicativo é mais popular na hora do almoço e na hora de dormir em Hyderabad.</span><span class="sxs-lookup"><span data-stu-id="d3e0f-118">Looks like our app is most popular at lunchtime and bed-time in Hyderabad.</span></span> <span data-ttu-id="d3e0f-119">(Então, devemos investigar esses 500 códigos).</span><span class="sxs-lookup"><span data-stu-id="d3e0f-119">(And we should investigate those 500 codes.)</span></span>

<span data-ttu-id="d3e0f-120">Também há operações estatísticas avançadas:</span><span class="sxs-lookup"><span data-stu-id="d3e0f-120">There are also powerful statistical operations:</span></span>

![Resultados de consulta estatística](./media/app-insights-analytics/025.png)

<span data-ttu-id="d3e0f-122">idioma Olá tem muitos recursos atraentes:</span><span class="sxs-lookup"><span data-stu-id="d3e0f-122">hello language has many attractive features:</span></span>


* <span data-ttu-id="d3e0f-123">[Filtre](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) a telemetria bruta de aplicativos por qualquer campo, incluindo suas métricas e propriedades personalizadas.</span><span class="sxs-lookup"><span data-stu-id="d3e0f-123">[Filter](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) your raw app telemetry by any fields, including your custom properties and metrics.</span></span>
* <span data-ttu-id="d3e0f-124">[Una](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) várias tabelas: correlacione as solicitações com exibições de página, as chamadas de dependência, as exceções e os rastreamentos de log.</span><span class="sxs-lookup"><span data-stu-id="d3e0f-124">[Join](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) multiple tables – correlate requests with page views, dependency calls, exceptions and log traces.</span></span>
* <span data-ttu-id="d3e0f-125">[Agregações](https://docs.loganalytics.io/learn/tutorials/aggregations.html)estatísticas poderosas.</span><span class="sxs-lookup"><span data-stu-id="d3e0f-125">Powerful statistical [aggregations](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>
* <span data-ttu-id="d3e0f-126">Tão poderosos quanto SQL, mas muito mais fácil para consultas complexas: em vez de aninhamento de instruções, você direcionar dados de saudação do toohello de uma operação elementares lado.</span><span class="sxs-lookup"><span data-stu-id="d3e0f-126">Just as powerful as SQL, but much easier for complex queries: instead of nesting statements, you pipe hello data from one elementary operation toohello next.</span></span>
* <span data-ttu-id="d3e0f-127">Visualizações imediatas e eficientes.</span><span class="sxs-lookup"><span data-stu-id="d3e0f-127">Immediate and powerful visualizations.</span></span>
* <span data-ttu-id="d3e0f-128">[Fixar gráficos painéis tooAzure](app-insights-analytics-using.md#pin-to-dashboard).</span><span class="sxs-lookup"><span data-stu-id="d3e0f-128">[Pin charts tooAzure dashboards](app-insights-analytics-using.md#pin-to-dashboard).</span></span>
* <span data-ttu-id="d3e0f-129">[Exportar consultas tooPower BI](app-insights-analytics-using.md#export-to-power-bi).</span><span class="sxs-lookup"><span data-stu-id="d3e0f-129">[Export queries tooPower BI](app-insights-analytics-using.md#export-to-power-bi).</span></span>
* <span data-ttu-id="d3e0f-130">Há um [API REST](https://dev.applicationinsights.io/) que você pode usar consultas toorun programaticamente, por exemplo do Powershell.</span><span class="sxs-lookup"><span data-stu-id="d3e0f-130">There's a [REST API](https://dev.applicationinsights.io/) that you can use toorun queries programmatically, for example from Powershell.</span></span>


## <a name="connect-tooyour-application-insights-data"></a><span data-ttu-id="d3e0f-131">Conecte-se a dados do Application Insights tooyour</span><span class="sxs-lookup"><span data-stu-id="d3e0f-131">Connect tooyour Application Insights data</span></span>
<span data-ttu-id="d3e0f-132">Abra o Analytics na [folha de visão geral](app-insights-dashboards.md) de seu aplicativo no Application Insights:</span><span class="sxs-lookup"><span data-stu-id="d3e0f-132">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span> 

![Abra o portal.azure.com, abra o recurso do Application Insights e clique em Análise.](./media/app-insights-analytics/001.png)


## <a name="video"></a><span data-ttu-id="d3e0f-134">Vídeo</span><span class="sxs-lookup"><span data-stu-id="d3e0f-134">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a><span data-ttu-id="d3e0f-135">Exemplos de consulta</span><span class="sxs-lookup"><span data-stu-id="d3e0f-135">Query examples</span></span>

<span data-ttu-id="d3e0f-136">Tente esses power de saudação tooillustrate explicações passo a passo do uso de análise:</span><span class="sxs-lookup"><span data-stu-id="d3e0f-136">Try these walkthroughs tooillustrate hello power of using Analytics:</span></span>

 *  [<span data-ttu-id="d3e0f-137">Diagnóstico automático de picos e etapas ignoradas nas durações de solicitações</span><span class="sxs-lookup"><span data-stu-id="d3e0f-137">Automatic diagnostics of spikes and step jumps in requests durations</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [<span data-ttu-id="d3e0f-138">Analisar degradações de desempenho com análise de série temporal</span><span class="sxs-lookup"><span data-stu-id="d3e0f-138">Analyzing performance degradations with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="d3e0f-139">Analisar as falhas do aplicativo com autocluster e diffpatterns</span><span class="sxs-lookup"><span data-stu-id="d3e0f-139">Analyzing application failures with autocluster and diffpatterns</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [<span data-ttu-id="d3e0f-140">Detecções de forma avançadas com análise de série temporal</span><span class="sxs-lookup"><span data-stu-id="d3e0f-140">Advanced shape detections with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="d3e0f-141">Usando deslizante janela operações tooanalyze uso do aplicativo (sem interrupção MAU/DAU etc)</span><span class="sxs-lookup"><span data-stu-id="d3e0f-141">Using sliding window operations tooanalyze application usage (rolling MAU/DAU etc)</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  <span data-ttu-id="d3e0f-142">[Detecção de interrupções de serviço com base na análise dos logs de depuração](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) e uma postagem de blog correspondente [aqui](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span><span class="sxs-lookup"><span data-stu-id="d3e0f-142">[Detection of service disruptions based on analysis of debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) and a matching blog post [here](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span></span>
 *  <span data-ttu-id="d3e0f-143">[Criação de perfil de desempenho de aplicativos usando logs de depuração simples](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) e uma postagem de blog correspondente [aqui](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span><span class="sxs-lookup"><span data-stu-id="d3e0f-143">[Profiling applications’ performance using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span></span>
 *  <span data-ttu-id="d3e0f-144">[Medindo a duração de saudação para cada etapa no fluxo de código usando logs de depuração simples](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) e uma postagem de blog correspondente [aqui](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="d3e0f-144">[Measuring hello duration for each step in your code flow using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span></span>
 *  <span data-ttu-id="d3e0f-145">[Analisar a simultaneidade usando logs de depuração simples](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) e uma postagem de blog correspondente [aqui](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="d3e0f-145">[Analyzing concurrency using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span></span>



## <a name="next-steps"></a><span data-ttu-id="d3e0f-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d3e0f-146">Next steps</span></span>
* <span data-ttu-id="d3e0f-147">É recomendável iniciar com hello [tour de idioma](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="d3e0f-147">We recommend you start with hello [language tour](app-insights-analytics-tour.md).</span></span> 
* <span data-ttu-id="d3e0f-148">Saiba mais sobre [como usar a análise](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="d3e0f-148">More about [using Analytics](app-insights-analytics-using.md).</span></span> 
* <span data-ttu-id="d3e0f-149">[Referência da linguagem](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="d3e0f-149">[Language reference](app-insights-analytics-reference.md).</span></span> 
