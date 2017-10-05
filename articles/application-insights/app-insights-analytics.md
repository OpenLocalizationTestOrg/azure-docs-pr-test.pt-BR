---
title: "Analytics - a ferramenta de pesquisa avançada do Azure Application Insights | Microsoft Docs"
description: "Visão geral da Análise, a ferramenta de pesquisa avançada do Application Insights. "
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
ms.openlocfilehash: 8174745a00a107eea648b223a00466b6a7f37331
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="analytics-in-application-insights"></a><span data-ttu-id="aa9e2-103">Análise no Application Insights</span><span class="sxs-lookup"><span data-stu-id="aa9e2-103">Analytics in Application Insights</span></span>
<span data-ttu-id="aa9e2-104">O [Analytics](app-insights-analytics.md) é o recurso de pesquisa avançado do [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aa9e2-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="aa9e2-105">Essas páginas descrevem a linguagem de consulta do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="aa9e2-105">These pages describe the Log Analytics query language.</span></span> 

* <span data-ttu-id="aa9e2-106">**[Assista ao vídeo introdutório](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="aa9e2-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="aa9e2-107">**[Faça um test drive do Analytics com nossos dados simulados](https://analytics.applicationinsights.io/demo)** se seu aplicativo ainda não estiver enviando dados para o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="aa9e2-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>
* <span data-ttu-id="aa9e2-108">**[Roteiro dos usuários do SQL](https://aka.ms/sql-analytics)** converte as linguagens mais comuns.</span><span class="sxs-lookup"><span data-stu-id="aa9e2-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates the most common idioms.</span></span>
* <span data-ttu-id="aa9e2-109">**[Referência de linguagem](app-insights-analytics-reference.md)** Aprenda a usar todos os recursos eficientes da linguagem de consulta do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="aa9e2-109">**[Language Reference](app-insights-analytics-reference.md)** Learn how to use all the powerful features of the Log Analytics query language.</span></span>


## <a name="queries-in-analytics"></a><span data-ttu-id="aa9e2-110">Consultas na Análise</span><span class="sxs-lookup"><span data-stu-id="aa9e2-110">Queries in Analytics</span></span>
<span data-ttu-id="aa9e2-111">Uma consulta comum é uma tabela de *origem* seguida por vários *operadores* separados por `|`.</span><span class="sxs-lookup"><span data-stu-id="aa9e2-111">A typical query is a *source* table followed by a series of *operators* separated by `|`.</span></span> 

<span data-ttu-id="aa9e2-112">Por exemplo, vamos descobrir em qual hora do dia os cidadãos de Hyderabad experimentam usar nosso aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="aa9e2-112">For example, let's find out what time of day the citizens of Hyderabad try our web app.</span></span> <span data-ttu-id="aa9e2-113">E enquanto estamos fazendo isso, vamos ver quais códigos de resultado são retornados para suas solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="aa9e2-113">And while we're there, let's see what result codes are returned to their HTTP requests.</span></span> 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

<span data-ttu-id="aa9e2-114">Contamos endereços IP de cliente distintos, agrupando-os por hora do dia nos últimos 7 dias.</span><span class="sxs-lookup"><span data-stu-id="aa9e2-114">We count distinct client IP addresses, grouping them by the hour of the day over the past 7 days.</span></span> 

> [!NOTE]
> <span data-ttu-id="aa9e2-115">Para obter resultados fora das últimas 24h, inclua 'timestamp' explicitamente na consulta ou use o menu suspenso de intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="aa9e2-115">To get results outside the previous 24h, either include 'timestamp' explicitly in your query, or use the time range drop-down menu.</span></span>
>

<span data-ttu-id="aa9e2-116">Vamos exibir os resultados com a apresentação do gráfico de barras, optando por empilhar os resultados de códigos de resposta diferentes:</span><span class="sxs-lookup"><span data-stu-id="aa9e2-116">Let's display the results with the bar chart presentation, choosing to stack the results from different response codes:</span></span>

![Escolha o gráfico de barras, os eixos x e y e a segmentação](./media/app-insights-analytics/020.png)

<span data-ttu-id="aa9e2-118">Parece que nosso aplicativo é mais popular na hora do almoço e na hora de dormir em Hyderabad.</span><span class="sxs-lookup"><span data-stu-id="aa9e2-118">Looks like our app is most popular at lunchtime and bed-time in Hyderabad.</span></span> <span data-ttu-id="aa9e2-119">(Então, devemos investigar esses 500 códigos).</span><span class="sxs-lookup"><span data-stu-id="aa9e2-119">(And we should investigate those 500 codes.)</span></span>

<span data-ttu-id="aa9e2-120">Também há operações estatísticas avançadas:</span><span class="sxs-lookup"><span data-stu-id="aa9e2-120">There are also powerful statistical operations:</span></span>

![Resultados de consulta estatística](./media/app-insights-analytics/025.png)

<span data-ttu-id="aa9e2-122">A linguagem tem muitos recursos atrativos:</span><span class="sxs-lookup"><span data-stu-id="aa9e2-122">The language has many attractive features:</span></span>


* <span data-ttu-id="aa9e2-123">[Filtre](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) a telemetria bruta de aplicativos por qualquer campo, incluindo suas métricas e propriedades personalizadas.</span><span class="sxs-lookup"><span data-stu-id="aa9e2-123">[Filter](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) your raw app telemetry by any fields, including your custom properties and metrics.</span></span>
* <span data-ttu-id="aa9e2-124">[Una](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) várias tabelas: correlacione as solicitações com exibições de página, as chamadas de dependência, as exceções e os rastreamentos de log.</span><span class="sxs-lookup"><span data-stu-id="aa9e2-124">[Join](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) multiple tables – correlate requests with page views, dependency calls, exceptions and log traces.</span></span>
* <span data-ttu-id="aa9e2-125">[Agregações](https://docs.loganalytics.io/learn/tutorials/aggregations.html)estatísticas poderosas.</span><span class="sxs-lookup"><span data-stu-id="aa9e2-125">Powerful statistical [aggregations](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>
* <span data-ttu-id="aa9e2-126">Tão potente quando o SQL, mas muito fácil para consultas complexas: em vez de aninhar instruções, você redireciona os dados de uma operação elementar para a próxima.</span><span class="sxs-lookup"><span data-stu-id="aa9e2-126">Just as powerful as SQL, but much easier for complex queries: instead of nesting statements, you pipe the data from one elementary operation to the next.</span></span>
* <span data-ttu-id="aa9e2-127">Visualizações imediatas e eficientes.</span><span class="sxs-lookup"><span data-stu-id="aa9e2-127">Immediate and powerful visualizations.</span></span>
* <span data-ttu-id="aa9e2-128">[Fixe gráficos em painéis do Azure](app-insights-analytics-using.md#pin-to-dashboard).</span><span class="sxs-lookup"><span data-stu-id="aa9e2-128">[Pin charts to Azure dashboards](app-insights-analytics-using.md#pin-to-dashboard).</span></span>
* <span data-ttu-id="aa9e2-129">[Exporte as consultas para Power BI](app-insights-analytics-using.md#export-to-power-bi).</span><span class="sxs-lookup"><span data-stu-id="aa9e2-129">[Export queries to Power BI](app-insights-analytics-using.md#export-to-power-bi).</span></span>
* <span data-ttu-id="aa9e2-130">Há uma [API REST](https://dev.applicationinsights.io/) que você pode usar para executar consultas de modo programático; no Powershell, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="aa9e2-130">There's a [REST API](https://dev.applicationinsights.io/) that you can use to run queries programmatically, for example from Powershell.</span></span>


## <a name="connect-to-your-application-insights-data"></a><span data-ttu-id="aa9e2-131">Conectar-se aos dados do Application Insights</span><span class="sxs-lookup"><span data-stu-id="aa9e2-131">Connect to your Application Insights data</span></span>
<span data-ttu-id="aa9e2-132">Abra o Analytics na [folha de visão geral](app-insights-dashboards.md) de seu aplicativo no Application Insights:</span><span class="sxs-lookup"><span data-stu-id="aa9e2-132">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span> 

![Abra o portal.azure.com, abra o recurso do Application Insights e clique em Análise.](./media/app-insights-analytics/001.png)


## <a name="video"></a><span data-ttu-id="aa9e2-134">Vídeo</span><span class="sxs-lookup"><span data-stu-id="aa9e2-134">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a><span data-ttu-id="aa9e2-135">Exemplos de consulta</span><span class="sxs-lookup"><span data-stu-id="aa9e2-135">Query examples</span></span>

<span data-ttu-id="aa9e2-136">Tente usar essas explicações passo a passo que ilustram a eficiência do uso do Analytics:</span><span class="sxs-lookup"><span data-stu-id="aa9e2-136">Try these walkthroughs to illustrate the power of using Analytics:</span></span>

 *  [<span data-ttu-id="aa9e2-137">Diagnóstico automático de picos e etapas ignoradas nas durações de solicitações</span><span class="sxs-lookup"><span data-stu-id="aa9e2-137">Automatic diagnostics of spikes and step jumps in requests durations</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [<span data-ttu-id="aa9e2-138">Analisar degradações de desempenho com análise de série temporal</span><span class="sxs-lookup"><span data-stu-id="aa9e2-138">Analyzing performance degradations with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="aa9e2-139">Analisar as falhas do aplicativo com autocluster e diffpatterns</span><span class="sxs-lookup"><span data-stu-id="aa9e2-139">Analyzing application failures with autocluster and diffpatterns</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [<span data-ttu-id="aa9e2-140">Detecções de forma avançadas com análise de série temporal</span><span class="sxs-lookup"><span data-stu-id="aa9e2-140">Advanced shape detections with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="aa9e2-141">Usar operações de janela deslizante para analisar o uso do aplicativo (MAU/DAU contínuos, etc.)</span><span class="sxs-lookup"><span data-stu-id="aa9e2-141">Using sliding window operations to analyze application usage (rolling MAU/DAU etc)</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  <span data-ttu-id="aa9e2-142">[Detecção de interrupções de serviço com base na análise dos logs de depuração](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) e uma postagem de blog correspondente [aqui](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span><span class="sxs-lookup"><span data-stu-id="aa9e2-142">[Detection of service disruptions based on analysis of debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) and a matching blog post [here](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span></span>
 *  <span data-ttu-id="aa9e2-143">[Criação de perfil de desempenho de aplicativos usando logs de depuração simples](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) e uma postagem de blog correspondente [aqui](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span><span class="sxs-lookup"><span data-stu-id="aa9e2-143">[Profiling applications’ performance using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span></span>
 *  <span data-ttu-id="aa9e2-144">[Medir a duração de cada etapa no seu fluxo de código usando logs de depuração simples](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) e uma postagem de blog correspondente [aqui](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="aa9e2-144">[Measuring the duration for each step in your code flow using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span></span>
 *  <span data-ttu-id="aa9e2-145">[Analisar a simultaneidade usando logs de depuração simples](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) e uma postagem de blog correspondente [aqui](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="aa9e2-145">[Analyzing concurrency using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span></span>



## <a name="next-steps"></a><span data-ttu-id="aa9e2-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aa9e2-146">Next steps</span></span>
* <span data-ttu-id="aa9e2-147">É recomendável começar com o [tour de linguagem](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="aa9e2-147">We recommend you start with the [language tour](app-insights-analytics-tour.md).</span></span> 
* <span data-ttu-id="aa9e2-148">Saiba mais sobre [como usar a análise](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="aa9e2-148">More about [using Analytics](app-insights-analytics-using.md).</span></span> 
* <span data-ttu-id="aa9e2-149">[Referência da linguagem](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="aa9e2-149">[Language reference](app-insights-analytics-reference.md).</span></span> 
