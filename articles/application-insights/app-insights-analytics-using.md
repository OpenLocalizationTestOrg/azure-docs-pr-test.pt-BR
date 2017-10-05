---
title: "Usando o Analytics – a ferramenta de pesquisa avançada do Azure Application Insights | Microsoft Docs"
description: "Usando a Análise, a ferramenta de pesquisa e diagnóstico avançada do Application Insights. "
services: application-insights
documentationcenter: 
author: danhadari
manager: carmonm
ms.assetid: c3b34430-f592-4c32-b900-e9f50ca096b3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9f7c1744db52b1c2f374fd5655e2c66b5f61bacf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="using-analytics-in-application-insights"></a><span data-ttu-id="a1cec-103">Usando Análise no Application Insights</span><span class="sxs-lookup"><span data-stu-id="a1cec-103">Using Analytics in Application Insights</span></span>
<span data-ttu-id="a1cec-104">O [Analytics](app-insights-analytics.md) é o recurso de pesquisa avançado do [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a1cec-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="a1cec-105">Essas páginas descrevem a linguagem de consulta do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a1cec-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="a1cec-106">**[Assista ao vídeo introdutório](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="a1cec-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="a1cec-107">**[Faça um test drive do Analytics com nossos dados simulados](https://analytics.applicationinsights.io/demo)** se seu aplicativo ainda não estiver enviando dados para o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a1cec-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>

## <a name="open-analytics"></a><span data-ttu-id="a1cec-108">Abrir Análise</span><span class="sxs-lookup"><span data-stu-id="a1cec-108">Open Analytics</span></span>
<span data-ttu-id="a1cec-109">Do recurso de página inicial do seu aplicativo no Application Insights, clique em Análise.</span><span class="sxs-lookup"><span data-stu-id="a1cec-109">From your app's home resource in Application Insights, click Analytics.</span></span>

![Abra o portal.azure.com, abra o recurso do Application Insights e clique em Análise.](./media/app-insights-analytics-using/001.png)

<span data-ttu-id="a1cec-111">O tutorial embutido oferece algumas ideias sobre o que você pode fazer.</span><span class="sxs-lookup"><span data-stu-id="a1cec-111">The inline tutorial gives you some ideas about what you can do.</span></span>

<span data-ttu-id="a1cec-112">Há um [tour mais extenso aqui](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="a1cec-112">There's a [more extensive tour here](app-insights-analytics-tour.md).</span></span>

## <a name="query-your-telemetry"></a><span data-ttu-id="a1cec-113">Consultar sua telemetria</span><span class="sxs-lookup"><span data-stu-id="a1cec-113">Query your telemetry</span></span>
### <a name="write-a-query"></a><span data-ttu-id="a1cec-114">Escreva uma consulta</span><span class="sxs-lookup"><span data-stu-id="a1cec-114">Write a query</span></span>
![Exibição de esquema](./media/app-insights-analytics-using/150.png)

<span data-ttu-id="a1cec-116">Comece com os nomes de uma das tabelas listadas à esquerda (ou os operadores [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) ou [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html)).</span><span class="sxs-lookup"><span data-stu-id="a1cec-116">Begin with the names of any of the tables listed on the left (or the [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) or [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operators).</span></span> <span data-ttu-id="a1cec-117">Use `|` para criar um pipeline de [operadores](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span><span class="sxs-lookup"><span data-stu-id="a1cec-117">Use `|` to create a pipeline of [operators](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span></span> 

<span data-ttu-id="a1cec-118">O IntelliSense mostrará os operadores e os elementos de expressão que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="a1cec-118">IntelliSense prompts you with the operators and the expression elements that you can use.</span></span> <span data-ttu-id="a1cec-119">Clique no ícone de informações (ou pressione CTRL + espaço) para obter uma descrição mais detalhada e exemplos de como usar cada elemento.</span><span class="sxs-lookup"><span data-stu-id="a1cec-119">Click the information icon (or press CTRL+Space) to get a longer description and examples of how to use each element.</span></span>

<span data-ttu-id="a1cec-120">Confira a [tour da linguagem do Analytics](app-insights-analytics-tour.md) e a [referência da linguagem](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="a1cec-120">See the [Analytics language tour](app-insights-analytics-tour.md) and [language reference](app-insights-analytics-reference.md).</span></span>

### <a name="run-a-query"></a><span data-ttu-id="a1cec-121">Executar uma consulta</span><span class="sxs-lookup"><span data-stu-id="a1cec-121">Run a query</span></span>
![Executando uma consulta](./media/app-insights-analytics-using/130.png)

1. <span data-ttu-id="a1cec-123">Você pode usar quebras de linha simples em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="a1cec-123">You can use single line breaks in a query.</span></span>
2. <span data-ttu-id="a1cec-124">Coloque o cursor na ou no final da consulta que você deseja executar.</span><span class="sxs-lookup"><span data-stu-id="a1cec-124">Put the cursor inside or at the end of the query you want to run.</span></span>
3. <span data-ttu-id="a1cec-125">Verifique o intervalo de tempo da consulta.</span><span class="sxs-lookup"><span data-stu-id="a1cec-125">Check the time range of your query.</span></span> <span data-ttu-id="a1cec-126">(Você pode alterá-lo ou substituí-lo, incluindo sua própria cláusula [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) em sua consulta.)</span><span class="sxs-lookup"><span data-stu-id="a1cec-126">(You can change it, or override it by including your own [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) clause in your query.)</span></span>
3. <span data-ttu-id="a1cec-127">Clique em Ir para executar a consulta.</span><span class="sxs-lookup"><span data-stu-id="a1cec-127">Click Go to run the query.</span></span>
4. <span data-ttu-id="a1cec-128">Não coloque linhas em branco em sua consulta.</span><span class="sxs-lookup"><span data-stu-id="a1cec-128">Don't put blank lines in your query.</span></span> <span data-ttu-id="a1cec-129">Você pode manter várias consultas separadas em uma guia de consulta separando-as com linhas em branco.</span><span class="sxs-lookup"><span data-stu-id="a1cec-129">You can keep several separated queries in one query tab by separating them with blank lines.</span></span> <span data-ttu-id="a1cec-130">Somente a consulta que possui o cursor é executada.</span><span class="sxs-lookup"><span data-stu-id="a1cec-130">Only the query that has the cursor runs.</span></span>

### <a name="save-a-query"></a><span data-ttu-id="a1cec-131">Salvar uma consulta</span><span class="sxs-lookup"><span data-stu-id="a1cec-131">Save a query</span></span>
![Salvando uma consulta](./media/app-insights-analytics-using/140.png)

1. <span data-ttu-id="a1cec-133">Salve o arquivo de consulta atual.</span><span class="sxs-lookup"><span data-stu-id="a1cec-133">Save the current query file.</span></span>
2. <span data-ttu-id="a1cec-134">Abra um arquivo de consulta salva.</span><span class="sxs-lookup"><span data-stu-id="a1cec-134">Open a saved query file.</span></span>
3. <span data-ttu-id="a1cec-135">Crie um novo arquivo de consulta.</span><span class="sxs-lookup"><span data-stu-id="a1cec-135">Create a new query file.</span></span>

## <a name="see-the-details"></a><span data-ttu-id="a1cec-136">Confierir os detalhes</span><span class="sxs-lookup"><span data-stu-id="a1cec-136">See the details</span></span>
<span data-ttu-id="a1cec-137">Expanda qualquer linha nos resultados para ver a lista completa das propriedades.</span><span class="sxs-lookup"><span data-stu-id="a1cec-137">Expand any row in the results to see its complete list of properties.</span></span> <span data-ttu-id="a1cec-138">Você pode expandir qualquer propriedade que seja um valor estruturado; por exemplo, dimensões personalizadas ou a pilha de listagem em uma exceção.</span><span class="sxs-lookup"><span data-stu-id="a1cec-138">You can further expand any property that is a structured value - for example, custom dimensions, or the stack listing in an exception.</span></span>

![Expandindo uma linha](./media/app-insights-analytics-using/070.png)

## <a name="arrange-the-results"></a><span data-ttu-id="a1cec-140">Organizar os resultados</span><span class="sxs-lookup"><span data-stu-id="a1cec-140">Arrange the results</span></span>
<span data-ttu-id="a1cec-141">Você pode classificar, filtrar, paginar e agrupar os resultados retornados da sua consulta.</span><span class="sxs-lookup"><span data-stu-id="a1cec-141">You can sort, filter, paginate, and group the results returned from your query.</span></span>

> [!NOTE]
> <span data-ttu-id="a1cec-142">A classificação, o agrupamento e a filtragem no navegador não executam a consulta novamente.</span><span class="sxs-lookup"><span data-stu-id="a1cec-142">Sorting, grouping, and filtering in the browser don't re-run your query.</span></span> <span data-ttu-id="a1cec-143">Eles apenas reorganizam os resultados que foram retornados por sua última consulta.</span><span class="sxs-lookup"><span data-stu-id="a1cec-143">They only rearrange the results that were returned by your last query.</span></span> 
> 
> <span data-ttu-id="a1cec-144">Para executar essas tarefas no servidor antes que os resultados sejam retornados, escreva sua consulta com os operadores [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) e [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html).</span><span class="sxs-lookup"><span data-stu-id="a1cec-144">To perform these tasks in the server before the results are returned, write your query with the [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) and [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operators.</span></span>
> 
> 

<span data-ttu-id="a1cec-145">Selecione as colunas que você gostaria de ver, arraste os cabeçalhos de coluna para reorganizá-las e redimensione as colunas arrastando suas bordas.</span><span class="sxs-lookup"><span data-stu-id="a1cec-145">Pick the columns you'd like to see, drag column headers to rearrange them, and resize columns by dragging their borders.</span></span>

![Organizando colunas](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a><span data-ttu-id="a1cec-147">Classificar e filtrar itens</span><span class="sxs-lookup"><span data-stu-id="a1cec-147">Sort and filter items</span></span>
<span data-ttu-id="a1cec-148">Classifique os resultados clicando no cabeçalho de uma coluna.</span><span class="sxs-lookup"><span data-stu-id="a1cec-148">Sort your results by clicking the head of a column.</span></span> <span data-ttu-id="a1cec-149">Clique novamente para classificar de outra forma e clique uma terceira vez para reverter à ordem original retornada pela consulta.</span><span class="sxs-lookup"><span data-stu-id="a1cec-149">Click again to sort the other way, and click a third time to revert to the original ordering returned by your query.</span></span>

<span data-ttu-id="a1cec-150">Use o ícone de filtro para restringir sua pesquisa.</span><span class="sxs-lookup"><span data-stu-id="a1cec-150">Use the filter icon to narrow your search.</span></span>

![Classificar e filtrar colunas](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a><span data-ttu-id="a1cec-152">Agrupar itens</span><span class="sxs-lookup"><span data-stu-id="a1cec-152">Group items</span></span>
<span data-ttu-id="a1cec-153">Para classificar por mais de uma coluna, use o agrupamento.</span><span class="sxs-lookup"><span data-stu-id="a1cec-153">To sort by more than one column, use grouping.</span></span> <span data-ttu-id="a1cec-154">Primeiro habilite-o e arraste cabeçalhos de coluna para o espaço acima da tabela.</span><span class="sxs-lookup"><span data-stu-id="a1cec-154">First enable it, and then drag column headers into the space above the table.</span></span>

![Agrupar](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a><span data-ttu-id="a1cec-156">Faltando alguns resultados?</span><span class="sxs-lookup"><span data-stu-id="a1cec-156">Missing some results?</span></span>

<span data-ttu-id="a1cec-157">Se você acha que não está vendo todos os resultados esperados, há alguns motivos possíveis.</span><span class="sxs-lookup"><span data-stu-id="a1cec-157">If you think you're not seeing all the results you expected, there are a couple of possible reasons.</span></span>

* <span data-ttu-id="a1cec-158">**Filtro de intervalo de tempo**.</span><span class="sxs-lookup"><span data-stu-id="a1cec-158">**Time range filter**.</span></span> <span data-ttu-id="a1cec-159">Por padrão, você verá apenas os resultados das últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="a1cec-159">By default, you will only see results from the last 24 hours.</span></span> <span data-ttu-id="a1cec-160">Há um filtro automático que limita o número de resultados que são recuperados das tabelas de origem.</span><span class="sxs-lookup"><span data-stu-id="a1cec-160">There is an automatic filter that limits the range of results that are retrieved from the source tables.</span></span> 

    <span data-ttu-id="a1cec-161">No entanto, você pode alterar o filtro de intervalo de tempo usando o menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="a1cec-161">However, you can change the time range filter by using the drop-down menu.</span></span>

    <span data-ttu-id="a1cec-162">Ou você pode substituir o intervalo automático incluindo sua própria [`where  ... timestamp ...` cláusula](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) em sua consulta.</span><span class="sxs-lookup"><span data-stu-id="a1cec-162">Or you can override the automatic range by including your own [`where  ... timestamp ...` clause](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) into your query.</span></span> <span data-ttu-id="a1cec-163">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1cec-163">For example:</span></span>

    `requests | where timestamp > ago('2d')`

* <span data-ttu-id="a1cec-164">**Limite de resultados**.</span><span class="sxs-lookup"><span data-stu-id="a1cec-164">**Results limit**.</span></span> <span data-ttu-id="a1cec-165">Há um limite de 10 mil linhas nos resultados retornados do portal.</span><span class="sxs-lookup"><span data-stu-id="a1cec-165">There's a limit of about 10k rows on the results returned from the portal.</span></span> <span data-ttu-id="a1cec-166">Será exibido um aviso se você ultrapassar o limite.</span><span class="sxs-lookup"><span data-stu-id="a1cec-166">A warning shows if you go over the limit.</span></span> <span data-ttu-id="a1cec-167">Se isso acontecer, os resultados na tabela de classificação não mostrarão sempre todos os primeiros ou últimos resultados reais.</span><span class="sxs-lookup"><span data-stu-id="a1cec-167">If that happens, sorting your results in the table won't always show you all the actual first or last results.</span></span> 

    <span data-ttu-id="a1cec-168">É recomendável evitar atingir o limite.</span><span class="sxs-lookup"><span data-stu-id="a1cec-168">It's good practice to avoid hitting the limit.</span></span> <span data-ttu-id="a1cec-169">Use o filtro de intervalo de tempo ou operadores como:</span><span class="sxs-lookup"><span data-stu-id="a1cec-169">Use the time range filter, or use operators such as:</span></span>

  * [<span data-ttu-id="a1cec-170">top 100 by timestamp</span><span class="sxs-lookup"><span data-stu-id="a1cec-170">top 100 by timestamp</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [<span data-ttu-id="a1cec-171">take 100</span><span class="sxs-lookup"><span data-stu-id="a1cec-171">take 100</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [<span data-ttu-id="a1cec-172">summarize </span><span class="sxs-lookup"><span data-stu-id="a1cec-172">summarize </span></span>](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [<span data-ttu-id="a1cec-173">where timestamp > ago(3d)</span><span class="sxs-lookup"><span data-stu-id="a1cec-173">where timestamp > ago(3d)</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

<span data-ttu-id="a1cec-174">(Quer de 10 mil linhas?</span><span class="sxs-lookup"><span data-stu-id="a1cec-174">(Want more than 10k rows?</span></span> <span data-ttu-id="a1cec-175">Considere usar [Exportação contínua](app-insights-export-telemetry.md) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="a1cec-175">Consider using [Continuous Export](app-insights-export-telemetry.md) instead.</span></span> <span data-ttu-id="a1cec-176">A análise foi projetada para análise, em vez de recuperar dados brutos.)</span><span class="sxs-lookup"><span data-stu-id="a1cec-176">Analytics is designed for analysis, rather than retrieving raw data.)</span></span>

## <a name="diagrams"></a><span data-ttu-id="a1cec-177">Diagramas</span><span class="sxs-lookup"><span data-stu-id="a1cec-177">Diagrams</span></span>
<span data-ttu-id="a1cec-178">Selecione o tipo de diagrama que você deseja:</span><span class="sxs-lookup"><span data-stu-id="a1cec-178">Select the type of diagram you'd like:</span></span>

![Selecionar um tipo de diagrama](./media/app-insights-analytics-using/230.png)

<span data-ttu-id="a1cec-180">Se você tiver várias colunas dos tipos corretos, você poderá escolher os eixos x e y, e uma coluna de dimensões pelas quais dividir os resultados.</span><span class="sxs-lookup"><span data-stu-id="a1cec-180">If you have several columns of the right types, you can choose the x and y axes, and a column of dimensions to split the results by.</span></span>

<span data-ttu-id="a1cec-181">Por padrão, os resultados são exibidos inicialmente como uma tabela e você seleciona o diagrama manualmente.</span><span class="sxs-lookup"><span data-stu-id="a1cec-181">By default, results are initially displayed as a table, and you select the diagram manually.</span></span> <span data-ttu-id="a1cec-182">Mas você pode usar a [diretiva de renderização](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) ao final de uma consulta para selecionar um diagrama.</span><span class="sxs-lookup"><span data-stu-id="a1cec-182">But you can use the [render directive](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) at the end of a query to select a diagram.</span></span>

### <a name="analytics-diagnostics"></a><span data-ttu-id="a1cec-183">Diagnóstico de análise</span><span class="sxs-lookup"><span data-stu-id="a1cec-183">Analytics diagnostics</span></span>


<span data-ttu-id="a1cec-184">Em um gráfico de tempo, se houver uma alteração ou pico repentino em seus dados, você poderá ver um ponto em destaque na linha.</span><span class="sxs-lookup"><span data-stu-id="a1cec-184">On a timechart, if there is a sudden spike or step in your data, you may see a highlighted point on the line.</span></span> <span data-ttu-id="a1cec-185">Isso indica que o Diagnóstico de Análise identificou uma combinação de propriedades que filtra a alteração repentina.</span><span class="sxs-lookup"><span data-stu-id="a1cec-185">This indicates that Analytics Diagnostics has identified a combination of properties that filter out the sudden change.</span></span> <span data-ttu-id="a1cec-186">Clique no ponto para obter mais detalhes sobre o filtro e para ver a versão filtrada.</span><span class="sxs-lookup"><span data-stu-id="a1cec-186">Click the point to get more detail on the filter, and to see the filtered version.</span></span> <span data-ttu-id="a1cec-187">Isso pode ajudar a identificar o que causou a alteração.</span><span class="sxs-lookup"><span data-stu-id="a1cec-187">This may help you identify what caused the change.</span></span> 

[<span data-ttu-id="a1cec-188">Saiba mais sobre o Diagnóstico de Análise</span><span class="sxs-lookup"><span data-stu-id="a1cec-188">Learn more about Analytics Diagnostics</span></span>](app-insights-analytics-diagnostics.md)


![Diagnóstico de análise](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-to-dashboard"></a><span data-ttu-id="a1cec-190">Fixar no painel</span><span class="sxs-lookup"><span data-stu-id="a1cec-190">Pin to dashboard</span></span>
<span data-ttu-id="a1cec-191">Você pode fixar um diagrama ou tabela em um dos seus [painéis compartilhados](app-insights-dashboards.md) , basta clicar no marcador.</span><span class="sxs-lookup"><span data-stu-id="a1cec-191">You can pin a diagram or table to one of your [shared dashboards](app-insights-dashboards.md) - just click the pin.</span></span> <span data-ttu-id="a1cec-192">(Talvez seja necessário [atualizar o pacote de preços do seu aplicativo](app-insights-pricing.md) para ativar esse recurso).</span><span class="sxs-lookup"><span data-stu-id="a1cec-192">(You might need to [upgrade your app's pricing package](app-insights-pricing.md) to turn on this feature.)</span></span> 

![Clicar no marcador](./media/app-insights-analytics-using/pin-01.png)

<span data-ttu-id="a1cec-194">Isso significa que, quando você monta um painel para ajudar a monitorar o desempenho ou o uso de seus serviços Web, pode incluir análise bastante complexa juntamente com outras métricas.</span><span class="sxs-lookup"><span data-stu-id="a1cec-194">This means that, when you put together a dashboard to help you monitor the performance or usage of your web services, you can include quite complex analysis alongside the other metrics.</span></span> 

<span data-ttu-id="a1cec-195">Você poderá fixar uma tabela no painel, se ele tiver quatro ou menos colunas.</span><span class="sxs-lookup"><span data-stu-id="a1cec-195">You can pin a table to the dashboard, if it has four or fewer columns.</span></span> <span data-ttu-id="a1cec-196">Somente as primeiras sete linhas são exibidas.</span><span class="sxs-lookup"><span data-stu-id="a1cec-196">Only the top seven rows are displayed.</span></span>

### <a name="dashboard-refresh"></a><span data-ttu-id="a1cec-197">Atualização do painel</span><span class="sxs-lookup"><span data-stu-id="a1cec-197">Dashboard refresh</span></span>
<span data-ttu-id="a1cec-198">O gráfico fixado no painel é atualizado de forma automática ao executar novamente a consulta aproximadamente a cada hora.</span><span class="sxs-lookup"><span data-stu-id="a1cec-198">The chart pinned to the dashboard is refreshed automatically by re-running the query approximately every hours.</span></span> <span data-ttu-id="a1cec-199">Você também pode clicar no botão Atualizar.</span><span class="sxs-lookup"><span data-stu-id="a1cec-199">You can also click the Refresh button.</span></span>

### <a name="automatic-simplifications"></a><span data-ttu-id="a1cec-200">Simplificações automáticas</span><span class="sxs-lookup"><span data-stu-id="a1cec-200">Automatic simplifications</span></span>

<span data-ttu-id="a1cec-201">Certas simplificações são aplicadas a um gráfico quando ele é fixado em um painel.</span><span class="sxs-lookup"><span data-stu-id="a1cec-201">Certain simplifications are applied to a chart when you pin it to a dashboard.</span></span>

<span data-ttu-id="a1cec-202">**Restrição de tempo:** As consultas são limitadas automaticamente aos últimos 14 dias.</span><span class="sxs-lookup"><span data-stu-id="a1cec-202">**Time restriction:** Queries are automatically limited to the past 14 days.</span></span> <span data-ttu-id="a1cec-203">O efeito é o mesmo que se sua consulta incluísse `where timestamp > ago(14d)`.</span><span class="sxs-lookup"><span data-stu-id="a1cec-203">The effect is the same as if your query includes `where timestamp > ago(14d)`.</span></span>

<span data-ttu-id="a1cec-204">**Restrição de contagem de compartimentos:** Se você exibir um gráfico que tenha muitos compartimentos distintos (normalmente um gráfico de barras), os compartimentos menos ocupados são automaticamente agrupados em um único compartimento do tipo "outros".</span><span class="sxs-lookup"><span data-stu-id="a1cec-204">**Bin count restriction:** If you display a chart that has a lot of discrete bins (typically a bar chart), the less populated bins are automatically grouped into a single "others" bin.</span></span> <span data-ttu-id="a1cec-205">Por exemplo, esta consulta:</span><span class="sxs-lookup"><span data-stu-id="a1cec-205">For example, this query:</span></span>

    requests | summarize count_search = count() by client_CountryOrRegion

<span data-ttu-id="a1cec-206">tem esta aparência no Analytics:</span><span class="sxs-lookup"><span data-stu-id="a1cec-206">looks like this in Analytics:</span></span>

![Gráfico de cauda longa](./media/app-insights-analytics-using/pin-07.png)

<span data-ttu-id="a1cec-208">mas quando você a fixa a um painel, ela fica assim:</span><span class="sxs-lookup"><span data-stu-id="a1cec-208">but when you pin it to a dashboard, it looks like this:</span></span>

![Gráfico com compartimentos limitados](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-to-excel"></a><span data-ttu-id="a1cec-210">Exportar para o Excel</span><span class="sxs-lookup"><span data-stu-id="a1cec-210">Export to Excel</span></span>
<span data-ttu-id="a1cec-211">Depois de executar uma consulta, você pode baixar um arquivo .csv.</span><span class="sxs-lookup"><span data-stu-id="a1cec-211">After you've run a query, you can download a .csv file.</span></span> <span data-ttu-id="a1cec-212">Clique em **Exportar, Excel**.</span><span class="sxs-lookup"><span data-stu-id="a1cec-212">Click **Export,  Excel**.</span></span>

## <a name="export-to-power-bi"></a><span data-ttu-id="a1cec-213">Exportar para o Power BI</span><span class="sxs-lookup"><span data-stu-id="a1cec-213">Export to Power BI</span></span>
<span data-ttu-id="a1cec-214">Coloque o cursor em uma consulta e escolha **Exportar, Power BI**.</span><span class="sxs-lookup"><span data-stu-id="a1cec-214">Put the cursor in a query and choose **Export, Power BI**.</span></span>

![Exportar do Analytics para o Power BI](./media/app-insights-analytics-using/240.png)

<span data-ttu-id="a1cec-216">Execute a consulta no Power BI.</span><span class="sxs-lookup"><span data-stu-id="a1cec-216">You run the query in Power BI.</span></span> <span data-ttu-id="a1cec-217">Você pode configurá-lo para atualizar em uma agenda.</span><span class="sxs-lookup"><span data-stu-id="a1cec-217">You can set it to refresh on a schedule.</span></span>

<span data-ttu-id="a1cec-218">Com o Power BI, você pode criar painéis que reúnem dados de uma grande variedade de fontes.</span><span class="sxs-lookup"><span data-stu-id="a1cec-218">With Power BI, you can create dashboards that bring together data from a wide variety of sources.</span></span>

[<span data-ttu-id="a1cec-219">Saiba mais sobre como exportar para o Power BI</span><span class="sxs-lookup"><span data-stu-id="a1cec-219">Learn more about export to Power BI</span></span>](app-insights-export-power-bi.md)

## <a name="deep-link"></a><span data-ttu-id="a1cec-220">Link profundo</span><span class="sxs-lookup"><span data-stu-id="a1cec-220">Deep link</span></span>

<span data-ttu-id="a1cec-221">Obtenha um link em **Exportar, Compartilhar link** que você possa enviar a outro usuário.</span><span class="sxs-lookup"><span data-stu-id="a1cec-221">Get a link under **Export, Share link** that you can send to another user.</span></span> <span data-ttu-id="a1cec-222">Desde que o usuário tenha [acesso ao seu grupo de recursos](app-insights-resources-roles-access-control.md), a consulta será aberta na interface do usuário do Analytics.</span><span class="sxs-lookup"><span data-stu-id="a1cec-222">Provided the user has [access to your resource group](app-insights-resources-roles-access-control.md), the query will open in the Analytics UI.</span></span>

<span data-ttu-id="a1cec-223">(No link, o texto da consulta aparece após "?q=", gzip compactado e codificado em base 64.</span><span class="sxs-lookup"><span data-stu-id="a1cec-223">(In the link, the query text appears after "?q=", gzip compressed and base-64 encoded.</span></span> <span data-ttu-id="a1cec-224">Você pode escrever código para gerar links profundos que fornece aos usuários.</span><span class="sxs-lookup"><span data-stu-id="a1cec-224">You could write code to generate deep links that you provide to users.</span></span> <span data-ttu-id="a1cec-225">No entanto, a maneira recomendada para executar o Analytics com código é usando a [API REST](https://dev.applicationinsights.io/).)</span><span class="sxs-lookup"><span data-stu-id="a1cec-225">However, the recommended way to run Analytics from code is by using the [REST API](https://dev.applicationinsights.io/).)</span></span>


## <a name="automation"></a><span data-ttu-id="a1cec-226">Automação</span><span class="sxs-lookup"><span data-stu-id="a1cec-226">Automation</span></span>

<span data-ttu-id="a1cec-227">Use a [API REST de Acesso a Dados](https://dev.applicationinsights.io/) para executar consultas do Analytics.</span><span class="sxs-lookup"><span data-stu-id="a1cec-227">Use the  [Data Access REST API](https://dev.applicationinsights.io/) to run Analytics queries.</span></span> <span data-ttu-id="a1cec-228">[Por exemplo](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (usando o PowerShell):</span><span class="sxs-lookup"><span data-stu-id="a1cec-228">[For example](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (using PowerShell):</span></span>

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

<span data-ttu-id="a1cec-229">Diferentemente da interface do usuário do Analytics, a API REST não adiciona automaticamente nenhuma limitação de carimbo de data/hora às suas consultas.</span><span class="sxs-lookup"><span data-stu-id="a1cec-229">Unlike the Analytics UI, the REST API does not automatically add any timestamp limitation to your queries.</span></span> <span data-ttu-id="a1cec-230">Lembre-se de adicionar sua própria cláusula where para evitar receber respostas enormes.</span><span class="sxs-lookup"><span data-stu-id="a1cec-230">Remember to add your own where-clause, to avoid getting huge responses.</span></span>



## <a name="import-data"></a><span data-ttu-id="a1cec-231">Importar dados</span><span class="sxs-lookup"><span data-stu-id="a1cec-231">Import data</span></span>

<span data-ttu-id="a1cec-232">Você pode importar dados de um arquivo CSV.</span><span class="sxs-lookup"><span data-stu-id="a1cec-232">You can import data from a CSV file.</span></span> <span data-ttu-id="a1cec-233">Normalmente, importam-se dados estáticos que você pode associar a tabelas de sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="a1cec-233">A typical usage is to import static data that you can join with tables from your telemetry.</span></span> 

<span data-ttu-id="a1cec-234">Por exemplo, se usuários autenticados são identificados em sua telemetria por um alias ou ID ofuscado, você pode importar uma tabela que mapeie os aliases para nomes reais.</span><span class="sxs-lookup"><span data-stu-id="a1cec-234">For example, if authenticated users are identified in your telemetry by an alias or obfuscated id, you could import a table that maps aliases to real names.</span></span> <span data-ttu-id="a1cec-235">Ao realizar uma junção na telemetria de solicitação, você pode identificar os usuários por seus nomes reais nos relatórios de análise.</span><span class="sxs-lookup"><span data-stu-id="a1cec-235">By performing a join on the request telemetry, you can identify users by their real names in the Analytics reports.</span></span>

### <a name="define-your-data-schema"></a><span data-ttu-id="a1cec-236">Definir o esquema de dados</span><span class="sxs-lookup"><span data-stu-id="a1cec-236">Define your data schema</span></span>

1. <span data-ttu-id="a1cec-237">Clique em **Configurações** (na parte superior esquerda) e, em seguida, **Fontes de dados**.</span><span class="sxs-lookup"><span data-stu-id="a1cec-237">Click **Settings** (at top left) and then **Data Sources**.</span></span> 
2. <span data-ttu-id="a1cec-238">Adicione uma fonte de dados de acordo com as instruções a seguir.</span><span class="sxs-lookup"><span data-stu-id="a1cec-238">Add a data source, following the instructions.</span></span> <span data-ttu-id="a1cec-239">Será solicitado que você forneça uma amostra dos dados, que devem incluir pelo menos dez linhas.</span><span class="sxs-lookup"><span data-stu-id="a1cec-239">You are asked to supply a sample of the data, which should include at least ten rows.</span></span> <span data-ttu-id="a1cec-240">Em seguida, você corrige o esquema.</span><span class="sxs-lookup"><span data-stu-id="a1cec-240">You then correct the schema.</span></span>

<span data-ttu-id="a1cec-241">Isso define uma fonte de dados que você pode usar para importar as tabelas individuais.</span><span class="sxs-lookup"><span data-stu-id="a1cec-241">This defines a data source, which you can then use to import individual tables.</span></span>

### <a name="import-a-table"></a><span data-ttu-id="a1cec-242">Importar uma tabela</span><span class="sxs-lookup"><span data-stu-id="a1cec-242">Import a table</span></span>

1. <span data-ttu-id="a1cec-243">Abra sua definição de fonte de dados da lista.</span><span class="sxs-lookup"><span data-stu-id="a1cec-243">Open your data source definition from the list.</span></span>
2. <span data-ttu-id="a1cec-244">Clique em "Carregar" e siga as instruções para carregar a tabela.</span><span class="sxs-lookup"><span data-stu-id="a1cec-244">Click "Upload" and follow the instructions to upload the table.</span></span> <span data-ttu-id="a1cec-245">Isso envolve uma chamada a uma API REST e, portanto é fácil de automatizar.</span><span class="sxs-lookup"><span data-stu-id="a1cec-245">This involves a call to a REST API, and so it is easy to automate.</span></span> 

<span data-ttu-id="a1cec-246">A tabela agora está disponível para uso em consultas de análise.</span><span class="sxs-lookup"><span data-stu-id="a1cec-246">Your table is now available for use in Analytics queries.</span></span> <span data-ttu-id="a1cec-247">Ele aparecerá na análise</span><span class="sxs-lookup"><span data-stu-id="a1cec-247">It will appear in Analytics</span></span> 

### <a name="use-the-table"></a><span data-ttu-id="a1cec-248">Use a tabela</span><span class="sxs-lookup"><span data-stu-id="a1cec-248">Use the table</span></span>

<span data-ttu-id="a1cec-249">Vamos supor que a definição de fonte de dados é chamada `usermap` e que ela possui dois campos, `realName` e `user_AuthenticatedId`.</span><span class="sxs-lookup"><span data-stu-id="a1cec-249">Let's suppose your data source definition is called `usermap`, and that it has two fields, `realName` and `user_AuthenticatedId`.</span></span> <span data-ttu-id="a1cec-250">A tabela `requests` também tem um campo chamado `user_AuthenticatedId`, portanto, é fácil uni-los:</span><span class="sxs-lookup"><span data-stu-id="a1cec-250">The `requests` table also has a field named `user_AuthenticatedId`, so it's easy to join them:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
<span data-ttu-id="a1cec-251">A tabela resultante de solicitações tem uma coluna adicional, `realName`.</span><span class="sxs-lookup"><span data-stu-id="a1cec-251">The resulting table of requests has an additional column, `realName`.</span></span>

### <a name="import-from-logstash"></a><span data-ttu-id="a1cec-252">Importar do LogStash</span><span class="sxs-lookup"><span data-stu-id="a1cec-252">Import from LogStash</span></span>

<span data-ttu-id="a1cec-253">Se você usar [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), você poderá usar a análise para consultar seus logs.</span><span class="sxs-lookup"><span data-stu-id="a1cec-253">If you use [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), you can use Analytics to query your logs.</span></span> <span data-ttu-id="a1cec-254">Use o [plug-in que redireciona os dados para análise](https://github.com/Microsoft/logstash-output-application-insights).</span><span class="sxs-lookup"><span data-stu-id="a1cec-254">Use the [plugin that pipes data into Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span></span> 

## <a name="video"></a><span data-ttu-id="a1cec-255">Vídeo</span><span class="sxs-lookup"><span data-stu-id="a1cec-255">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

