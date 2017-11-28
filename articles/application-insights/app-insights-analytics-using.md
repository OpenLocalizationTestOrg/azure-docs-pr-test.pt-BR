---
title: "aaaUsing análise - Olá poderosa ferramenta de pesquisa de informações de aplicativo do Azure | Microsoft Docs"
description: "Usando Olá análise, a ferramenta de diagnóstico avançados de pesquisa de saudação do Application Insights. "
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
ms.openlocfilehash: 6e0246848457db368c57d08c47b5bf73f4e5e3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-analytics-in-application-insights"></a><span data-ttu-id="3abfc-103">Usando Análise no Application Insights</span><span class="sxs-lookup"><span data-stu-id="3abfc-103">Using Analytics in Application Insights</span></span>
<span data-ttu-id="3abfc-104">[Análise de](app-insights-analytics.md) é o recurso de pesquisa poderoso saudação do [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3abfc-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="3abfc-105">Essas páginas descrevem a linguagem de consulta do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3abfc-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="3abfc-106">**[Assistir ao vídeo introdutório Olá](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="3abfc-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="3abfc-107">**[Faça o test drive análise sobre nossos dados simulados](https://analytics.applicationinsights.io/demo)**  se seu aplicativo não esteja enviando dados tooApplication Insights ainda.</span><span class="sxs-lookup"><span data-stu-id="3abfc-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>

## <a name="open-analytics"></a><span data-ttu-id="3abfc-108">Abrir Análise</span><span class="sxs-lookup"><span data-stu-id="3abfc-108">Open Analytics</span></span>
<span data-ttu-id="3abfc-109">Do recurso de página inicial do seu aplicativo no Application Insights, clique em Análise.</span><span class="sxs-lookup"><span data-stu-id="3abfc-109">From your app's home resource in Application Insights, click Analytics.</span></span>

![Abra o portal.azure.com, abra o recurso do Application Insights e clique em Análise.](./media/app-insights-analytics-using/001.png)

<span data-ttu-id="3abfc-111">tutorial de embutido Olá oferece algumas ideias sobre o que você pode fazer.</span><span class="sxs-lookup"><span data-stu-id="3abfc-111">hello inline tutorial gives you some ideas about what you can do.</span></span>

<span data-ttu-id="3abfc-112">Há um [tour mais extenso aqui](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="3abfc-112">There's a [more extensive tour here](app-insights-analytics-tour.md).</span></span>

## <a name="query-your-telemetry"></a><span data-ttu-id="3abfc-113">Consultar sua telemetria</span><span class="sxs-lookup"><span data-stu-id="3abfc-113">Query your telemetry</span></span>
### <a name="write-a-query"></a><span data-ttu-id="3abfc-114">Escreva uma consulta</span><span class="sxs-lookup"><span data-stu-id="3abfc-114">Write a query</span></span>
![Exibição de esquema](./media/app-insights-analytics-using/150.png)

<span data-ttu-id="3abfc-116">Começar com nomes de saudação de qualquer uma das tabelas Olá listadas Olá esquerda (ou hello [intervalo](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) ou [união](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operadores).</span><span class="sxs-lookup"><span data-stu-id="3abfc-116">Begin with hello names of any of hello tables listed on hello left (or hello [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) or [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operators).</span></span> <span data-ttu-id="3abfc-117">Use `|` toocreate um pipeline de [operadores](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span><span class="sxs-lookup"><span data-stu-id="3abfc-117">Use `|` toocreate a pipeline of [operators](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span></span> 

<span data-ttu-id="3abfc-118">IntelliSense solicita operadores hello e elementos de expressão Olá que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="3abfc-118">IntelliSense prompts you with hello operators and hello expression elements that you can use.</span></span> <span data-ttu-id="3abfc-119">Clique o ícone de informações hello (ou pressione CTRL + espaço) tooget uma descrição mais detalhada e exemplos de como toouse cada elemento.</span><span class="sxs-lookup"><span data-stu-id="3abfc-119">Click hello information icon (or press CTRL+Space) tooget a longer description and examples of how toouse each element.</span></span>

<span data-ttu-id="3abfc-120">Consulte Olá [tour de idioma de análise](app-insights-analytics-tour.md) e [referência de linguagem](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="3abfc-120">See hello [Analytics language tour](app-insights-analytics-tour.md) and [language reference](app-insights-analytics-reference.md).</span></span>

### <a name="run-a-query"></a><span data-ttu-id="3abfc-121">Executar uma consulta</span><span class="sxs-lookup"><span data-stu-id="3abfc-121">Run a query</span></span>
![Executando uma consulta](./media/app-insights-analytics-using/130.png)

1. <span data-ttu-id="3abfc-123">Você pode usar quebras de linha simples em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="3abfc-123">You can use single line breaks in a query.</span></span>
2. <span data-ttu-id="3abfc-124">Coloque o cursor hello dentro ou no final de saudação da consulta Olá que ser toorun.</span><span class="sxs-lookup"><span data-stu-id="3abfc-124">Put hello cursor inside or at hello end of hello query you want toorun.</span></span>
3. <span data-ttu-id="3abfc-125">Verifique o intervalo de tempo de saudação da sua consulta.</span><span class="sxs-lookup"><span data-stu-id="3abfc-125">Check hello time range of your query.</span></span> <span data-ttu-id="3abfc-126">(Você pode alterá-lo ou substituí-lo, incluindo sua própria cláusula [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) em sua consulta.)</span><span class="sxs-lookup"><span data-stu-id="3abfc-126">(You can change it, or override it by including your own [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) clause in your query.)</span></span>
3. <span data-ttu-id="3abfc-127">Clique em Ir toorun Olá consulta.</span><span class="sxs-lookup"><span data-stu-id="3abfc-127">Click Go toorun hello query.</span></span>
4. <span data-ttu-id="3abfc-128">Não coloque linhas em branco em sua consulta.</span><span class="sxs-lookup"><span data-stu-id="3abfc-128">Don't put blank lines in your query.</span></span> <span data-ttu-id="3abfc-129">Você pode manter várias consultas separadas em uma guia de consulta separando-as com linhas em branco.</span><span class="sxs-lookup"><span data-stu-id="3abfc-129">You can keep several separated queries in one query tab by separating them with blank lines.</span></span> <span data-ttu-id="3abfc-130">Somente consulta Olá que tem um cursor de saudação é executada.</span><span class="sxs-lookup"><span data-stu-id="3abfc-130">Only hello query that has hello cursor runs.</span></span>

### <a name="save-a-query"></a><span data-ttu-id="3abfc-131">Salvar uma consulta</span><span class="sxs-lookup"><span data-stu-id="3abfc-131">Save a query</span></span>
![Salvando uma consulta](./media/app-insights-analytics-using/140.png)

1. <span data-ttu-id="3abfc-133">Salve o arquivo de consulta atual hello.</span><span class="sxs-lookup"><span data-stu-id="3abfc-133">Save hello current query file.</span></span>
2. <span data-ttu-id="3abfc-134">Abra um arquivo de consulta salva.</span><span class="sxs-lookup"><span data-stu-id="3abfc-134">Open a saved query file.</span></span>
3. <span data-ttu-id="3abfc-135">Crie um novo arquivo de consulta.</span><span class="sxs-lookup"><span data-stu-id="3abfc-135">Create a new query file.</span></span>

## <a name="see-hello-details"></a><span data-ttu-id="3abfc-136">Consulte os detalhes de saudação</span><span class="sxs-lookup"><span data-stu-id="3abfc-136">See hello details</span></span>
<span data-ttu-id="3abfc-137">Expanda qualquer linha hello resultados toosee sua lista completa das propriedades.</span><span class="sxs-lookup"><span data-stu-id="3abfc-137">Expand any row in hello results toosee its complete list of properties.</span></span> <span data-ttu-id="3abfc-138">Você pode expandir mais qualquer propriedade que é um valor estruturado - por exemplo, dimensões personalizadas ou pilha Olá listando em uma exceção.</span><span class="sxs-lookup"><span data-stu-id="3abfc-138">You can further expand any property that is a structured value - for example, custom dimensions, or hello stack listing in an exception.</span></span>

![Expandindo uma linha](./media/app-insights-analytics-using/070.png)

## <a name="arrange-hello-results"></a><span data-ttu-id="3abfc-140">Organizar os resultados de saudação</span><span class="sxs-lookup"><span data-stu-id="3abfc-140">Arrange hello results</span></span>
<span data-ttu-id="3abfc-141">Classificar, filtrar, paginação e agrupar resultados Olá retornados da consulta.</span><span class="sxs-lookup"><span data-stu-id="3abfc-141">You can sort, filter, paginate, and group hello results returned from your query.</span></span>

> [!NOTE]
> <span data-ttu-id="3abfc-142">Classificação, agrupamento e filtragem no navegador de saudação não execute novamente a consulta.</span><span class="sxs-lookup"><span data-stu-id="3abfc-142">Sorting, grouping, and filtering in hello browser don't re-run your query.</span></span> <span data-ttu-id="3abfc-143">Eles apenas reorganizar resultados Olá que foram retornados por sua última consulta.</span><span class="sxs-lookup"><span data-stu-id="3abfc-143">They only rearrange hello results that were returned by your last query.</span></span> 
> 
> <span data-ttu-id="3abfc-144">tooperform essas tarefas no servidor de saudação antes Olá resultados são retornados, gravar a consulta com hello [classificação](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [resumir](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) e [onde](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operadores.</span><span class="sxs-lookup"><span data-stu-id="3abfc-144">tooperform these tasks in hello server before hello results are returned, write your query with hello [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) and [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operators.</span></span>
> 
> 

<span data-ttu-id="3abfc-145">Escolher colunas Olá faria como toosee, arraste toorearrange de cabeçalhos de coluna-los e redimensionar colunas arrastando as bordas.</span><span class="sxs-lookup"><span data-stu-id="3abfc-145">Pick hello columns you'd like toosee, drag column headers toorearrange them, and resize columns by dragging their borders.</span></span>

![Organizando colunas](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a><span data-ttu-id="3abfc-147">Classificar e filtrar itens</span><span class="sxs-lookup"><span data-stu-id="3abfc-147">Sort and filter items</span></span>
<span data-ttu-id="3abfc-148">Classifica seus resultados clicando head saudação de uma coluna.</span><span class="sxs-lookup"><span data-stu-id="3abfc-148">Sort your results by clicking hello head of a column.</span></span> <span data-ttu-id="3abfc-149">Clique novamente em toosort Olá outra maneira, e clique em pela terceira vez toorevert toohello original ordenação retornado pela consulta.</span><span class="sxs-lookup"><span data-stu-id="3abfc-149">Click again toosort hello other way, and click a third time toorevert toohello original ordering returned by your query.</span></span>

<span data-ttu-id="3abfc-150">Use toonarrow de ícone de filtro Olá sua pesquisa.</span><span class="sxs-lookup"><span data-stu-id="3abfc-150">Use hello filter icon toonarrow your search.</span></span>

![Classificar e filtrar colunas](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a><span data-ttu-id="3abfc-152">Agrupar itens</span><span class="sxs-lookup"><span data-stu-id="3abfc-152">Group items</span></span>
<span data-ttu-id="3abfc-153">toosort por mais de uma coluna, use o agrupamento.</span><span class="sxs-lookup"><span data-stu-id="3abfc-153">toosort by more than one column, use grouping.</span></span> <span data-ttu-id="3abfc-154">Primeiro ativá-lo e arraste cabeçalhos de coluna para o espaço de saudação acima da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="3abfc-154">First enable it, and then drag column headers into hello space above hello table.</span></span>

![Agrupar](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a><span data-ttu-id="3abfc-156">Faltando alguns resultados?</span><span class="sxs-lookup"><span data-stu-id="3abfc-156">Missing some results?</span></span>

<span data-ttu-id="3abfc-157">Se você acha que você não vir todos os resultados de saudação esperado, há alguns motivos possíveis.</span><span class="sxs-lookup"><span data-stu-id="3abfc-157">If you think you're not seeing all hello results you expected, there are a couple of possible reasons.</span></span>

* <span data-ttu-id="3abfc-158">**Filtro de intervalo de tempo**.</span><span class="sxs-lookup"><span data-stu-id="3abfc-158">**Time range filter**.</span></span> <span data-ttu-id="3abfc-159">Por padrão, você só verá resultados de saudação últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="3abfc-159">By default, you will only see results from hello last 24 hours.</span></span> <span data-ttu-id="3abfc-160">Há um filtro automático que limita o intervalo de saudação de resultados que são recuperados das tabelas de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="3abfc-160">There is an automatic filter that limits hello range of results that are retrieved from hello source tables.</span></span> 

    <span data-ttu-id="3abfc-161">No entanto, você pode alterar o intervalo de tempo de saudação filtro usando o menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="3abfc-161">However, you can change hello time range filter by using hello drop-down menu.</span></span>

    <span data-ttu-id="3abfc-162">Ou você pode substituir o intervalo automático hello, incluindo sua própria [ `where  ... timestamp ...` cláusula](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) em sua consulta.</span><span class="sxs-lookup"><span data-stu-id="3abfc-162">Or you can override hello automatic range by including your own [`where  ... timestamp ...` clause](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) into your query.</span></span> <span data-ttu-id="3abfc-163">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3abfc-163">For example:</span></span>

    `requests | where timestamp > ago('2d')`

* <span data-ttu-id="3abfc-164">**Limite de resultados**.</span><span class="sxs-lookup"><span data-stu-id="3abfc-164">**Results limit**.</span></span> <span data-ttu-id="3abfc-165">Há um limite de 10 mil linhas nos resultados de saudação retornados do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="3abfc-165">There's a limit of about 10k rows on hello results returned from hello portal.</span></span> <span data-ttu-id="3abfc-166">Um aviso mostra se você vá acima do limite de saudação.</span><span class="sxs-lookup"><span data-stu-id="3abfc-166">A warning shows if you go over hello limit.</span></span> <span data-ttu-id="3abfc-167">Se isso acontecer, classificar seus resultados na tabela de saudação não sempre mostrará todos os Olá primeiro ou últimos resultados reais.</span><span class="sxs-lookup"><span data-stu-id="3abfc-167">If that happens, sorting your results in hello table won't always show you all hello actual first or last results.</span></span> 

    <span data-ttu-id="3abfc-168">É o limite de uma boa prática tooavoid atingir hello.</span><span class="sxs-lookup"><span data-stu-id="3abfc-168">It's good practice tooavoid hitting hello limit.</span></span> <span data-ttu-id="3abfc-169">Use o filtro de intervalo de tempo de saudação ou usar operadores, como:</span><span class="sxs-lookup"><span data-stu-id="3abfc-169">Use hello time range filter, or use operators such as:</span></span>

  * [<span data-ttu-id="3abfc-170">top 100 by timestamp</span><span class="sxs-lookup"><span data-stu-id="3abfc-170">top 100 by timestamp</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [<span data-ttu-id="3abfc-171">take 100</span><span class="sxs-lookup"><span data-stu-id="3abfc-171">take 100</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [<span data-ttu-id="3abfc-172">summarize </span><span class="sxs-lookup"><span data-stu-id="3abfc-172">summarize </span></span>](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [<span data-ttu-id="3abfc-173">where timestamp > ago(3d)</span><span class="sxs-lookup"><span data-stu-id="3abfc-173">where timestamp > ago(3d)</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

<span data-ttu-id="3abfc-174">(Quer de 10 mil linhas?</span><span class="sxs-lookup"><span data-stu-id="3abfc-174">(Want more than 10k rows?</span></span> <span data-ttu-id="3abfc-175">Considere usar [Exportação contínua](app-insights-export-telemetry.md) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="3abfc-175">Consider using [Continuous Export](app-insights-export-telemetry.md) instead.</span></span> <span data-ttu-id="3abfc-176">A análise foi projetada para análise, em vez de recuperar dados brutos.)</span><span class="sxs-lookup"><span data-stu-id="3abfc-176">Analytics is designed for analysis, rather than retrieving raw data.)</span></span>

## <a name="diagrams"></a><span data-ttu-id="3abfc-177">Diagramas</span><span class="sxs-lookup"><span data-stu-id="3abfc-177">Diagrams</span></span>
<span data-ttu-id="3abfc-178">Selecione o tipo de saudação do diagrama que deseja:</span><span class="sxs-lookup"><span data-stu-id="3abfc-178">Select hello type of diagram you'd like:</span></span>

![Selecionar um tipo de diagrama](./media/app-insights-analytics-using/230.png)

<span data-ttu-id="3abfc-180">Se você tiver várias colunas de tipos de saudação à direita, você pode escolher Olá x e eixos y e uma coluna de resultados de saudação toosplit dimensões por.</span><span class="sxs-lookup"><span data-stu-id="3abfc-180">If you have several columns of hello right types, you can choose hello x and y axes, and a column of dimensions toosplit hello results by.</span></span>

<span data-ttu-id="3abfc-181">Por padrão, resultados são inicialmente exibidos como uma tabela e você selecionar diagrama Olá manualmente.</span><span class="sxs-lookup"><span data-stu-id="3abfc-181">By default, results are initially displayed as a table, and you select hello diagram manually.</span></span> <span data-ttu-id="3abfc-182">Mas você pode usar o hello [renderizar diretiva](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) final Olá tooselect uma consulta um diagrama.</span><span class="sxs-lookup"><span data-stu-id="3abfc-182">But you can use hello [render directive](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) at hello end of a query tooselect a diagram.</span></span>

### <a name="analytics-diagnostics"></a><span data-ttu-id="3abfc-183">Diagnóstico de análise</span><span class="sxs-lookup"><span data-stu-id="3abfc-183">Analytics diagnostics</span></span>


<span data-ttu-id="3abfc-184">Em um timechart, se houver um aumento repentino ou a etapa em seus dados, você poderá ver um ponto realçado na linha de saudação.</span><span class="sxs-lookup"><span data-stu-id="3abfc-184">On a timechart, if there is a sudden spike or step in your data, you may see a highlighted point on hello line.</span></span> <span data-ttu-id="3abfc-185">Isso indica que o diagnóstico de análise de identificou uma combinação das propriedades filtrar alterações repentinas hello.</span><span class="sxs-lookup"><span data-stu-id="3abfc-185">This indicates that Analytics Diagnostics has identified a combination of properties that filter out hello sudden change.</span></span> <span data-ttu-id="3abfc-186">Clique em Olá ponto tooget obter mais detalhes sobre o filtro hello e toosee Olá filtrado versão.</span><span class="sxs-lookup"><span data-stu-id="3abfc-186">Click hello point tooget more detail on hello filter, and toosee hello filtered version.</span></span> <span data-ttu-id="3abfc-187">Isso pode ajudá-lo a identificar qual alteração Olá geradas.</span><span class="sxs-lookup"><span data-stu-id="3abfc-187">This may help you identify what caused hello change.</span></span> 

[<span data-ttu-id="3abfc-188">Saiba mais sobre o Diagnóstico de Análise</span><span class="sxs-lookup"><span data-stu-id="3abfc-188">Learn more about Analytics Diagnostics</span></span>](app-insights-analytics-diagnostics.md)


![Diagnóstico de análise](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-toodashboard"></a><span data-ttu-id="3abfc-190">PIN toodashboard</span><span class="sxs-lookup"><span data-stu-id="3abfc-190">Pin toodashboard</span></span>
<span data-ttu-id="3abfc-191">Você pode fixar um tooone diagrama ou tabela de seu [compartilhado painéis](app-insights-dashboards.md) -apenas clicar em fixar hello.</span><span class="sxs-lookup"><span data-stu-id="3abfc-191">You can pin a diagram or table tooone of your [shared dashboards](app-insights-dashboards.md) - just click hello pin.</span></span> <span data-ttu-id="3abfc-192">(Talvez seja necessário muito[atualização de pacote de preços do seu aplicativo](app-insights-pricing.md) tooturn sobre esse recurso.)</span><span class="sxs-lookup"><span data-stu-id="3abfc-192">(You might need too[upgrade your app's pricing package](app-insights-pricing.md) tooturn on this feature.)</span></span> 

![Clique em fixar Olá](./media/app-insights-analytics-using/pin-01.png)

<span data-ttu-id="3abfc-194">Isso significa que, quando você cria um toohelp painel você monitorar o desempenho de saudação ou o uso de serviços da web, você pode incluir análise bastante complexa junto com hello outras métricas.</span><span class="sxs-lookup"><span data-stu-id="3abfc-194">This means that, when you put together a dashboard toohelp you monitor hello performance or usage of your web services, you can include quite complex analysis alongside hello other metrics.</span></span> 

<span data-ttu-id="3abfc-195">Você pode fixar um painel de toohello de tabela, se ele tem quatro ou menos colunas.</span><span class="sxs-lookup"><span data-stu-id="3abfc-195">You can pin a table toohello dashboard, if it has four or fewer columns.</span></span> <span data-ttu-id="3abfc-196">Somente Olá sete linhas superiores são exibidas.</span><span class="sxs-lookup"><span data-stu-id="3abfc-196">Only hello top seven rows are displayed.</span></span>

### <a name="dashboard-refresh"></a><span data-ttu-id="3abfc-197">Atualização do painel</span><span class="sxs-lookup"><span data-stu-id="3abfc-197">Dashboard refresh</span></span>
<span data-ttu-id="3abfc-198">Olá gráfico fixado toohello painel é atualizado automaticamente, executando novamente Olá consulta aproximadamente a cada horas.</span><span class="sxs-lookup"><span data-stu-id="3abfc-198">hello chart pinned toohello dashboard is refreshed automatically by re-running hello query approximately every hours.</span></span> <span data-ttu-id="3abfc-199">Você também pode clicar em botão de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="3abfc-199">You can also click hello Refresh button.</span></span>

### <a name="automatic-simplifications"></a><span data-ttu-id="3abfc-200">Simplificações automáticas</span><span class="sxs-lookup"><span data-stu-id="3abfc-200">Automatic simplifications</span></span>

<span data-ttu-id="3abfc-201">Determinados simplificações são aplicadas tooa gráfico quando você fixa tooa painel.</span><span class="sxs-lookup"><span data-stu-id="3abfc-201">Certain simplifications are applied tooa chart when you pin it tooa dashboard.</span></span>

<span data-ttu-id="3abfc-202">**Restrição de tempo:** consultas são automaticamente limitado toohello últimos 14 dias.</span><span class="sxs-lookup"><span data-stu-id="3abfc-202">**Time restriction:** Queries are automatically limited toohello past 14 days.</span></span> <span data-ttu-id="3abfc-203">Olá efeito é Olá mesmo que sua consulta inclui `where timestamp > ago(14d)`.</span><span class="sxs-lookup"><span data-stu-id="3abfc-203">hello effect is hello same as if your query includes `where timestamp > ago(14d)`.</span></span>

<span data-ttu-id="3abfc-204">**Guardar a restrição de contagem:** se você exibir um gráfico que tem vários compartimentos discretos (normalmente um gráfico de barras), Olá menos compartimentos preenchidos automaticamente são agrupados em um único "outros" bin.</span><span class="sxs-lookup"><span data-stu-id="3abfc-204">**Bin count restriction:** If you display a chart that has a lot of discrete bins (typically a bar chart), hello less populated bins are automatically grouped into a single "others" bin.</span></span> <span data-ttu-id="3abfc-205">Por exemplo, esta consulta:</span><span class="sxs-lookup"><span data-stu-id="3abfc-205">For example, this query:</span></span>

    requests | summarize count_search = count() by client_CountryOrRegion

<span data-ttu-id="3abfc-206">tem esta aparência no Analytics:</span><span class="sxs-lookup"><span data-stu-id="3abfc-206">looks like this in Analytics:</span></span>

![Gráfico de cauda longa](./media/app-insights-analytics-using/pin-07.png)

<span data-ttu-id="3abfc-208">mas quando fixá-lo tooa painel, ele se parece com esta:</span><span class="sxs-lookup"><span data-stu-id="3abfc-208">but when you pin it tooa dashboard, it looks like this:</span></span>

![Gráfico com compartimentos limitados](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-tooexcel"></a><span data-ttu-id="3abfc-210">Exportar tooExcel</span><span class="sxs-lookup"><span data-stu-id="3abfc-210">Export tooExcel</span></span>
<span data-ttu-id="3abfc-211">Depois de executar uma consulta, você pode baixar um arquivo .csv.</span><span class="sxs-lookup"><span data-stu-id="3abfc-211">After you've run a query, you can download a .csv file.</span></span> <span data-ttu-id="3abfc-212">Clique em **Exportar, Excel**.</span><span class="sxs-lookup"><span data-stu-id="3abfc-212">Click **Export,  Excel**.</span></span>

## <a name="export-toopower-bi"></a><span data-ttu-id="3abfc-213">Exportar tooPower BI</span><span class="sxs-lookup"><span data-stu-id="3abfc-213">Export tooPower BI</span></span>
<span data-ttu-id="3abfc-214">Coloque o cursor de saudação em uma consulta e escolha **exportar, Power BI**.</span><span class="sxs-lookup"><span data-stu-id="3abfc-214">Put hello cursor in a query and choose **Export, Power BI**.</span></span>

![Exportar da análise tooPower BI](./media/app-insights-analytics-using/240.png)

<span data-ttu-id="3abfc-216">Você executa a consulta de saudação no Power BI.</span><span class="sxs-lookup"><span data-stu-id="3abfc-216">You run hello query in Power BI.</span></span> <span data-ttu-id="3abfc-217">Você pode definir toorefresh em uma agenda.</span><span class="sxs-lookup"><span data-stu-id="3abfc-217">You can set it toorefresh on a schedule.</span></span>

<span data-ttu-id="3abfc-218">Com o Power BI, você pode criar painéis que reúnem dados de uma grande variedade de fontes.</span><span class="sxs-lookup"><span data-stu-id="3abfc-218">With Power BI, you can create dashboards that bring together data from a wide variety of sources.</span></span>

[<span data-ttu-id="3abfc-219">Saiba mais sobre exportação tooPower BI</span><span class="sxs-lookup"><span data-stu-id="3abfc-219">Learn more about export tooPower BI</span></span>](app-insights-export-power-bi.md)

## <a name="deep-link"></a><span data-ttu-id="3abfc-220">Link profundo</span><span class="sxs-lookup"><span data-stu-id="3abfc-220">Deep link</span></span>

<span data-ttu-id="3abfc-221">Obter um link em **exportação, o vínculo de compartilhamento** que você pode enviar tooanother usuário.</span><span class="sxs-lookup"><span data-stu-id="3abfc-221">Get a link under **Export, Share link** that you can send tooanother user.</span></span> <span data-ttu-id="3abfc-222">Contanto que tenha o usuário Olá [grupo de recursos do acesso tooyour](app-insights-resources-roles-access-control.md), Olá consulta será aberta no hello análise da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="3abfc-222">Provided hello user has [access tooyour resource group](app-insights-resources-roles-access-control.md), hello query will open in hello Analytics UI.</span></span>

<span data-ttu-id="3abfc-223">(No link hello, texto de consulta Olá aparece após "? q =", compactado gzip e codificado na base 64.</span><span class="sxs-lookup"><span data-stu-id="3abfc-223">(In hello link, hello query text appears after "?q=", gzip compressed and base-64 encoded.</span></span> <span data-ttu-id="3abfc-224">Você pode escrever links profundos de toogenerate de código que você forneça toousers.</span><span class="sxs-lookup"><span data-stu-id="3abfc-224">You could write code toogenerate deep links that you provide toousers.</span></span> <span data-ttu-id="3abfc-225">No entanto, o hello recomendado é de maneira toorun análise de código usando Olá [API REST](https://dev.applicationinsights.io/).)</span><span class="sxs-lookup"><span data-stu-id="3abfc-225">However, hello recommended way toorun Analytics from code is by using hello [REST API](https://dev.applicationinsights.io/).)</span></span>


## <a name="automation"></a><span data-ttu-id="3abfc-226">Automação</span><span class="sxs-lookup"><span data-stu-id="3abfc-226">Automation</span></span>

<span data-ttu-id="3abfc-227">Saudação de uso [API REST de acesso a dados](https://dev.applicationinsights.io/) toorun consultas de análise.</span><span class="sxs-lookup"><span data-stu-id="3abfc-227">Use hello  [Data Access REST API](https://dev.applicationinsights.io/) toorun Analytics queries.</span></span> <span data-ttu-id="3abfc-228">[Por exemplo](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (usando o PowerShell):</span><span class="sxs-lookup"><span data-stu-id="3abfc-228">[For example](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (using PowerShell):</span></span>

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

<span data-ttu-id="3abfc-229">Ao contrário Olá análise da interface do usuário, Olá API REST não adiciona automaticamente as consultas de tooyour de limitação de carimbo de hora.</span><span class="sxs-lookup"><span data-stu-id="3abfc-229">Unlike hello Analytics UI, hello REST API does not automatically add any timestamp limitation tooyour queries.</span></span> <span data-ttu-id="3abfc-230">Lembre-se de tooadd seu próprios-cláusula where, tooavoid receber respostas enormes.</span><span class="sxs-lookup"><span data-stu-id="3abfc-230">Remember tooadd your own where-clause, tooavoid getting huge responses.</span></span>



## <a name="import-data"></a><span data-ttu-id="3abfc-231">Importar dados</span><span class="sxs-lookup"><span data-stu-id="3abfc-231">Import data</span></span>

<span data-ttu-id="3abfc-232">Você pode importar dados de um arquivo CSV.</span><span class="sxs-lookup"><span data-stu-id="3abfc-232">You can import data from a CSV file.</span></span> <span data-ttu-id="3abfc-233">Um uso típico é tooimport dados estáticos que você pode associar tabelas da sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="3abfc-233">A typical usage is tooimport static data that you can join with tables from your telemetry.</span></span> 

<span data-ttu-id="3abfc-234">Por exemplo, se os usuários autenticados são identificados em sua telemetria por um alias ou id ofuscado, pode importar uma tabela que mapeia nomes de tooreal aliases.</span><span class="sxs-lookup"><span data-stu-id="3abfc-234">For example, if authenticated users are identified in your telemetry by an alias or obfuscated id, you could import a table that maps aliases tooreal names.</span></span> <span data-ttu-id="3abfc-235">Executando uma junção em Telemetria de solicitação hello, você pode identificar os usuários por seus nomes reais em relatórios de análise de saudação.</span><span class="sxs-lookup"><span data-stu-id="3abfc-235">By performing a join on hello request telemetry, you can identify users by their real names in hello Analytics reports.</span></span>

### <a name="define-your-data-schema"></a><span data-ttu-id="3abfc-236">Definir o esquema de dados</span><span class="sxs-lookup"><span data-stu-id="3abfc-236">Define your data schema</span></span>

1. <span data-ttu-id="3abfc-237">Clique em **Configurações** (na parte superior esquerda) e, em seguida, **Fontes de dados**.</span><span class="sxs-lookup"><span data-stu-id="3abfc-237">Click **Settings** (at top left) and then **Data Sources**.</span></span> 
2. <span data-ttu-id="3abfc-238">Adicione uma fonte de dados, seguindo as instruções de saudação.</span><span class="sxs-lookup"><span data-stu-id="3abfc-238">Add a data source, following hello instructions.</span></span> <span data-ttu-id="3abfc-239">Será solicitado toosupply uma amostra de dados hello, que devem incluir pelo menos dez linhas.</span><span class="sxs-lookup"><span data-stu-id="3abfc-239">You are asked toosupply a sample of hello data, which should include at least ten rows.</span></span> <span data-ttu-id="3abfc-240">Você, em seguida, corrija o esquema hello.</span><span class="sxs-lookup"><span data-stu-id="3abfc-240">You then correct hello schema.</span></span>

<span data-ttu-id="3abfc-241">Isso define uma fonte de dados, em seguida, você pode usar tabelas individuais tooimport.</span><span class="sxs-lookup"><span data-stu-id="3abfc-241">This defines a data source, which you can then use tooimport individual tables.</span></span>

### <a name="import-a-table"></a><span data-ttu-id="3abfc-242">Importar uma tabela</span><span class="sxs-lookup"><span data-stu-id="3abfc-242">Import a table</span></span>

1. <span data-ttu-id="3abfc-243">Abra sua definição de fonte de dados da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="3abfc-243">Open your data source definition from hello list.</span></span>
2. <span data-ttu-id="3abfc-244">Clique em "Carregar" e siga a tabela de Olá Olá instruções tooupload.</span><span class="sxs-lookup"><span data-stu-id="3abfc-244">Click "Upload" and follow hello instructions tooupload hello table.</span></span> <span data-ttu-id="3abfc-245">Isso envolve tooa uma chamada de API REST e por isso, é fácil tooautomate.</span><span class="sxs-lookup"><span data-stu-id="3abfc-245">This involves a call tooa REST API, and so it is easy tooautomate.</span></span> 

<span data-ttu-id="3abfc-246">A tabela agora está disponível para uso em consultas de análise.</span><span class="sxs-lookup"><span data-stu-id="3abfc-246">Your table is now available for use in Analytics queries.</span></span> <span data-ttu-id="3abfc-247">Ele aparecerá na análise</span><span class="sxs-lookup"><span data-stu-id="3abfc-247">It will appear in Analytics</span></span> 

### <a name="use-hello-table"></a><span data-ttu-id="3abfc-248">Use a tabela de saudação</span><span class="sxs-lookup"><span data-stu-id="3abfc-248">Use hello table</span></span>

<span data-ttu-id="3abfc-249">Vamos supor que a definição de fonte de dados é chamada `usermap` e que ela possui dois campos, `realName` e `user_AuthenticatedId`.</span><span class="sxs-lookup"><span data-stu-id="3abfc-249">Let's suppose your data source definition is called `usermap`, and that it has two fields, `realName` and `user_AuthenticatedId`.</span></span> <span data-ttu-id="3abfc-250">Olá `requests` tabela também tem um campo chamado `user_AuthenticatedId`, portanto, é fácil toojoin-los:</span><span class="sxs-lookup"><span data-stu-id="3abfc-250">hello `requests` table also has a field named `user_AuthenticatedId`, so it's easy toojoin them:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
<span data-ttu-id="3abfc-251">a tabela resultante de solicitações Hello tem uma coluna adicional, `realName`.</span><span class="sxs-lookup"><span data-stu-id="3abfc-251">hello resulting table of requests has an additional column, `realName`.</span></span>

### <a name="import-from-logstash"></a><span data-ttu-id="3abfc-252">Importar do LogStash</span><span class="sxs-lookup"><span data-stu-id="3abfc-252">Import from LogStash</span></span>

<span data-ttu-id="3abfc-253">Se você usar [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), você pode usar a análise tooquery seus logs.</span><span class="sxs-lookup"><span data-stu-id="3abfc-253">If you use [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), you can use Analytics tooquery your logs.</span></span> <span data-ttu-id="3abfc-254">Saudação de uso [plug-in que canaliza os dados para análise de](https://github.com/Microsoft/logstash-output-application-insights).</span><span class="sxs-lookup"><span data-stu-id="3abfc-254">Use hello [plugin that pipes data into Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span></span> 

## <a name="video"></a><span data-ttu-id="3abfc-255">Vídeo</span><span class="sxs-lookup"><span data-stu-id="3abfc-255">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

