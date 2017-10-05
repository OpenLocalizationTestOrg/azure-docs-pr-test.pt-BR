---
title: Um tour pelo Analytics no Azure Application Insights | Microsoft Docs
description: "Exemplos curtos de todas as principais consultas na Análise, a ferramenta de pesquisa avançada do Application Insights."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: bddf4a6d-ea8d-4607-8531-1fe197cc57ad
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/06/2017
ms.author: bwren
ms.openlocfilehash: f5650d212eb2f8c460f062b3c11ae14c1e026ba6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="a-tour-of-analytics-in-application-insights"></a><span data-ttu-id="2d3af-103">Um tour pela Análise no Application Insights</span><span class="sxs-lookup"><span data-stu-id="2d3af-103">A tour of Analytics in Application Insights</span></span>
<span data-ttu-id="2d3af-104">O [Analytics](app-insights-analytics.md) é o recurso de pesquisa avançado do [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2d3af-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="2d3af-105">Essas páginas descrevem a linguagem de consulta do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2d3af-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="2d3af-106">**[Assista ao vídeo introdutório](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="2d3af-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="2d3af-107">**[Faça um test drive do Analytics com nossos dados simulados](https://analytics.applicationinsights.io/demo)** se seu aplicativo ainda não estiver enviando dados para o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2d3af-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>
* <span data-ttu-id="2d3af-108">**[Roteiro dos usuários do SQL](https://aka.ms/sql-analytics)** converte as linguagens mais comuns.</span><span class="sxs-lookup"><span data-stu-id="2d3af-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates the most common idioms.</span></span>

<span data-ttu-id="2d3af-109">Vamos analisar algumas consultas básicas para começar.</span><span class="sxs-lookup"><span data-stu-id="2d3af-109">Let's take a walk through some basic queries to get you started.</span></span>

## <a name="connect-to-your-application-insights-data"></a><span data-ttu-id="2d3af-110">Conectar-se aos dados do Application Insights</span><span class="sxs-lookup"><span data-stu-id="2d3af-110">Connect to your Application Insights data</span></span>
<span data-ttu-id="2d3af-111">Abra o Analytics na [folha de visão geral](app-insights-dashboards.md) de seu aplicativo no Application Insights:</span><span class="sxs-lookup"><span data-stu-id="2d3af-111">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span>

![Abra o portal.azure.com, abra o recurso do Application Insights e clique em Análise.](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a><span data-ttu-id="2d3af-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): mostre-me n linhas</span><span class="sxs-lookup"><span data-stu-id="2d3af-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): show me n rows</span></span>
<span data-ttu-id="2d3af-114">Os pontos de dados que registram em log operações de usuário (geralmente solicitações HTTP recebidas pelo seu aplicativo Web) são armazenados em uma tabela chamada `requests`.</span><span class="sxs-lookup"><span data-stu-id="2d3af-114">Data points that log user operations (typically HTTP requests received by your web app) are stored in a table called `requests`.</span></span> <span data-ttu-id="2d3af-115">Cada linha é um ponto de dados de telemetria recebido do SDK do Application Insights em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2d3af-115">Each row is a telemetry data point received from the Application Insights SDK in your app.</span></span>

<span data-ttu-id="2d3af-116">Vamos começar examinando algumas linhas de exemplo da tabela:</span><span class="sxs-lookup"><span data-stu-id="2d3af-116">Let's start by examining a few sample rows of the table:</span></span>

![results](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> <span data-ttu-id="2d3af-118">Coloque o cursor em algum lugar na instrução antes de clicar em Ir.</span><span class="sxs-lookup"><span data-stu-id="2d3af-118">Put the cursor somewhere in the statement before you click Go.</span></span> <span data-ttu-id="2d3af-119">Você pode dividir uma instrução em mais de uma linha, mas não coloque linhas em branco em uma instrução.</span><span class="sxs-lookup"><span data-stu-id="2d3af-119">You can split a statement over more than one line, but don't put blank lines in a statement.</span></span> <span data-ttu-id="2d3af-120">As linhas em branco são uma maneira conveniente de manter várias consultas separadas na janela.</span><span class="sxs-lookup"><span data-stu-id="2d3af-120">Blank lines are a convenient way to keep several separate queries in the window.</span></span>
>
>

<span data-ttu-id="2d3af-121">Escolha colunas, arraste-as, agrupe por colunas e filtre:</span><span class="sxs-lookup"><span data-stu-id="2d3af-121">Choose columns, drag them, group by columns, and filter:</span></span>

![Clique na seleção de coluna no canto superior direito dos resultados](./media/app-insights-analytics-tour/030.png)

<span data-ttu-id="2d3af-123">Expanda algum item para ver os detalhes:</span><span class="sxs-lookup"><span data-stu-id="2d3af-123">Expand any item to see the detail:</span></span>

![Escolha Tabela e use Configurar Colunas](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> <span data-ttu-id="2d3af-125">Clique no cabeçalho de uma coluna para reordenar os resultados disponíveis no navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="2d3af-125">Click the head of a column to re-order the results available in the web browser.</span></span> <span data-ttu-id="2d3af-126">Mas lembre-se de que, para um conjunto de resultados grande, o número de linhas baixadas para o navegador é limitado.</span><span class="sxs-lookup"><span data-stu-id="2d3af-126">But be aware that for a large result set, the number of rows downloaded to the browser is limited.</span></span> <span data-ttu-id="2d3af-127">Portanto, classificar dessa maneira não mostra sempre a você os reais itens maiores ou menores.</span><span class="sxs-lookup"><span data-stu-id="2d3af-127">Sorting this way doesn't always show you the actual highest or lowest items.</span></span> <span data-ttu-id="2d3af-128">Para classificar itens de forma confiável, use o `top` ou o operador `sort`.</span><span class="sxs-lookup"><span data-stu-id="2d3af-128">To sort items reliably, use the `top` or `sort` operator.</span></span>
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a><span data-ttu-id="2d3af-129">[Superior](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) e [classificação](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span><span class="sxs-lookup"><span data-stu-id="2d3af-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) and [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span></span>
<span data-ttu-id="2d3af-130">`take` é útil para obter um exemplo rápido de um resultado, mas mostra linhas da tabela sem uma ordem específica.</span><span class="sxs-lookup"><span data-stu-id="2d3af-130">`take` is useful to get a quick sample of a result, but it shows rows from the table in no particular order.</span></span> <span data-ttu-id="2d3af-131">Para obter uma exibição ordenada, use `top` (para obter um exemplo) ou `sort` (na tabela inteira).</span><span class="sxs-lookup"><span data-stu-id="2d3af-131">To get an ordered view, use `top` (for a sample) or `sort` (over the whole table).</span></span>

<span data-ttu-id="2d3af-132">Mostre-me as primeiras n linhas, ordenadas por uma coluna específica:</span><span class="sxs-lookup"><span data-stu-id="2d3af-132">Show me the first n rows, ordered by a particular column:</span></span>

```AIQL

    requests | top 10 by timestamp desc
```

* <span data-ttu-id="2d3af-133">*Sintaxe:* a maioria dos operadores têm parâmetros de palavra-chave, como `by`.</span><span class="sxs-lookup"><span data-stu-id="2d3af-133">*Syntax:* Most operators have keyword parameters such as `by`.</span></span>
* <span data-ttu-id="2d3af-134">`desc` = ordem decrescente, `asc` = ordem crescente.</span><span class="sxs-lookup"><span data-stu-id="2d3af-134">`desc` = descending order, `asc` = ascending.</span></span>

![](./media/app-insights-analytics-tour/260.png)

<span data-ttu-id="2d3af-135">`top...` é uma maneira mais eficaz de dizer `sort ... | take...`.</span><span class="sxs-lookup"><span data-stu-id="2d3af-135">`top...` is a more performant way of saying `sort ... | take...`.</span></span> <span data-ttu-id="2d3af-136">Poderíamos ter escrito:</span><span class="sxs-lookup"><span data-stu-id="2d3af-136">We could have written:</span></span>

```AIQL

    requests | sort by timestamp desc | take 10
```

<span data-ttu-id="2d3af-137">O resultado seria o mesmo, mas ele seria executado um pouco mais lentamente.</span><span class="sxs-lookup"><span data-stu-id="2d3af-137">The result would be the same, but it would run a bit more slowly.</span></span> <span data-ttu-id="2d3af-138">(Também é possível escrever `order`, que é um alias de `sort`.)</span><span class="sxs-lookup"><span data-stu-id="2d3af-138">(You could also write `order`, which is an alias of `sort`.)</span></span>

<span data-ttu-id="2d3af-139">Os cabeçalhos de coluna no modo de exibição de tabela também podem ser usados para classificar os resultados na tela.</span><span class="sxs-lookup"><span data-stu-id="2d3af-139">The column headers in the table view can also be used to sort the results on the screen.</span></span> <span data-ttu-id="2d3af-140">Mas, obviamente, se você usou `take` ou `top` para recuperar apenas parte de uma tabela, apenas os registros que foram recuperados serão reordenados.</span><span class="sxs-lookup"><span data-stu-id="2d3af-140">But of course, if you've used `take` or `top` to retrieve just part of a table, you'll only re-order the records you've retrieved.</span></span>

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a><span data-ttu-id="2d3af-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtragem de uma condição</span><span class="sxs-lookup"><span data-stu-id="2d3af-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtering on a condition</span></span>

<span data-ttu-id="2d3af-142">Vamos ver apenas as solicitações que retornaram um código de resultado específico:</span><span class="sxs-lookup"><span data-stu-id="2d3af-142">Let's see just requests that returned a particular result code:</span></span>

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

<span data-ttu-id="2d3af-143">O operador `where` usa uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="2d3af-143">The `where` operator takes a Boolean expression.</span></span> <span data-ttu-id="2d3af-144">Eis alguns pontos importantes sobre eles:</span><span class="sxs-lookup"><span data-stu-id="2d3af-144">Here are some key points about them:</span></span>

* <span data-ttu-id="2d3af-145">`and`, `or`: Operadores booleanos</span><span class="sxs-lookup"><span data-stu-id="2d3af-145">`and`, `or`: Boolean operators</span></span>
* <span data-ttu-id="2d3af-146">`==`, `<>`, `!=`: igual a e diferente de</span><span class="sxs-lookup"><span data-stu-id="2d3af-146">`==`, `<>`, `!=` : equal and not equal</span></span>
* <span data-ttu-id="2d3af-147">`=~`, `!~`: cadeia de caracteres que não diferencia maiúsculas de minúsculas "igual a" e "diferente de".</span><span class="sxs-lookup"><span data-stu-id="2d3af-147">`=~`, `!~` : case-insensitive string equal and not equal.</span></span> <span data-ttu-id="2d3af-148">Há muitos outros operadores de comparação de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="2d3af-148">There are lots more string comparison operators.</span></span>

<!---Read all about [scalar expressions]().--->

### <a name="getting-the-right-type"></a><span data-ttu-id="2d3af-149">Obtenção do tipo correto</span><span class="sxs-lookup"><span data-stu-id="2d3af-149">Getting the right type</span></span>
<span data-ttu-id="2d3af-150">Solicitações malsucedidas de localização:</span><span class="sxs-lookup"><span data-stu-id="2d3af-150">Find unsuccessful requests:</span></span>

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a><span data-ttu-id="2d3af-151">Hora</span><span class="sxs-lookup"><span data-stu-id="2d3af-151">Time</span></span>

<span data-ttu-id="2d3af-152">Por padrão, as consultas são restritas às últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="2d3af-152">By default, your queries are restricted to the last 24 hours.</span></span> <span data-ttu-id="2d3af-153">Mas você pode alterar esse intervalo:</span><span class="sxs-lookup"><span data-stu-id="2d3af-153">But you can change this range:</span></span>

![](./media/app-insights-analytics-tour/change-time-range.png)

<span data-ttu-id="2d3af-154">Substitua o intervalo de tempo escrevendo qualquer consulta que mencione `timestamp` em uma cláusula where.</span><span class="sxs-lookup"><span data-stu-id="2d3af-154">Override the time range by writing any query that mentions `timestamp` in a where-clause.</span></span> <span data-ttu-id="2d3af-155">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2d3af-155">For example:</span></span>

```AIQL

    // What were the slowest requests over the past 3 days?
    requests
    | where timestamp > ago(3d)  // Override the time range
    | top 5 by duration
```

<span data-ttu-id="2d3af-156">O recurso de intervalo de tempo é equivalente a uma cláusula 'where' inserida após cada menção de uma das tabelas de origem.</span><span class="sxs-lookup"><span data-stu-id="2d3af-156">The time range feature is equivalent to a 'where' clause inserted after each mention of one of the source tables.</span></span>

<span data-ttu-id="2d3af-157">`ago(3d)` significa 'três dias atrás'.</span><span class="sxs-lookup"><span data-stu-id="2d3af-157">`ago(3d)` means 'three days ago'.</span></span> <span data-ttu-id="2d3af-158">Outras unidades de tempo incluem horas (`2h`, `2.5h`), minutos (`25m`) e segundos (`10s`).</span><span class="sxs-lookup"><span data-stu-id="2d3af-158">Other units of time include hours (`2h`, `2.5h`), minutes (`25m`), and seconds (`10s`).</span></span>

<span data-ttu-id="2d3af-159">Outros exemplos:</span><span class="sxs-lookup"><span data-stu-id="2d3af-159">Other examples:</span></span>

```AIQL

    // Last calendar week:
    requests
    | where timestamp > startofweek(now()-7d)
        and timestamp < startofweek(now())
    | top 5 by duration

    // First hour of every day in past seven days:
    requests
    | where timestamp > ago(7d) and timestamp % 1d < 1h
    | top 5 by duration

    // Specific dates:
    requests
    | where timestamp > datetime(2016-11-19) and timestamp < datetime(2016-11-21)
    | top 5 by duration

```

<span data-ttu-id="2d3af-160">[Referência de datas e horas](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span><span class="sxs-lookup"><span data-stu-id="2d3af-160">[Dates and times reference](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span></span>


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a><span data-ttu-id="2d3af-161">[Projeto](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): selecionar, renomear e computar colunas</span><span class="sxs-lookup"><span data-stu-id="2d3af-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): select, rename, and compute columns</span></span>
<span data-ttu-id="2d3af-162">Use [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) para selecionar apenas as colunas desejadas:</span><span class="sxs-lookup"><span data-stu-id="2d3af-162">Use [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) to pick out just the columns you want:</span></span>

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

<span data-ttu-id="2d3af-163">Você também pode renomear e definir novas colunas:</span><span class="sxs-lookup"><span data-stu-id="2d3af-163">You can also rename columns and define new ones:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | project  
            name,
            response = resultCode,
            timestamp,
            ['time of day'] = floor(timestamp % 1d, 1s)
```

![result](./media/app-insights-analytics-tour/270.png)

* <span data-ttu-id="2d3af-165">Os nomes de coluna poderão incluir espaços ou símbolos se eles estiverem entre colchetes, desta forma: `['...']` ou `["..."]`</span><span class="sxs-lookup"><span data-stu-id="2d3af-165">Column names can include spaces or symbols if they are bracketed like this: `['...']` or `["..."]`</span></span>
* <span data-ttu-id="2d3af-166">`%` é o operador de módulo normal.</span><span class="sxs-lookup"><span data-stu-id="2d3af-166">`%` is the usual modulo operator.</span></span>
* <span data-ttu-id="2d3af-167">`1d` (que é o dígito um e um “d”) é um literal de timespan que significa um dia.</span><span class="sxs-lookup"><span data-stu-id="2d3af-167">`1d` (that's a digit one, then a 'd') is a timespan literal meaning one day.</span></span> <span data-ttu-id="2d3af-168">Aqui estão mais alguns literais de timespan: `12h`, `30m`, `10s` e `0.01s`.</span><span class="sxs-lookup"><span data-stu-id="2d3af-168">Here are some more timespan literals: `12h`, `30m`, `10s`, `0.01s`.</span></span>
* <span data-ttu-id="2d3af-169">`floor` (alias `bin`) arredonda um valor até o múltiplo mais próximo do valor de base fornecido.</span><span class="sxs-lookup"><span data-stu-id="2d3af-169">`floor` (alias `bin`) rounds a value down to the nearest multiple of the base value you provide.</span></span> <span data-ttu-id="2d3af-170">De modo que `floor(aTime, 1s)` arredonda um tempo até o segundo mais próximo.</span><span class="sxs-lookup"><span data-stu-id="2d3af-170">So `floor(aTime, 1s)` rounds a time down to the nearest second.</span></span>

<span data-ttu-id="2d3af-171">As expressões podem incluir todos os operadores comuns (`+`, `-`, ...) e há uma variedade de funções úteis.</span><span class="sxs-lookup"><span data-stu-id="2d3af-171">Expressions can include all the usual operators (`+`, `-`, ...), and there's a range of useful functions.</span></span>

## <a name="extend"></a><span data-ttu-id="2d3af-172">Extend</span><span class="sxs-lookup"><span data-stu-id="2d3af-172">Extend</span></span>
<span data-ttu-id="2d3af-173">Se quiser apenas adicionar colunas às existentes, use [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span><span class="sxs-lookup"><span data-stu-id="2d3af-173">If you just want to add columns to the existing ones, use [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

<span data-ttu-id="2d3af-174">O uso de [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) será menos detalhado do que o de [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) se você quiser manter todas as colunas existentes.</span><span class="sxs-lookup"><span data-stu-id="2d3af-174">Using [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) is less verbose than [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) if you want to keep all the existing columns.</span></span>

### <a name="convert-to-local-time"></a><span data-ttu-id="2d3af-175">Converter em hora local</span><span class="sxs-lookup"><span data-stu-id="2d3af-175">Convert to local time</span></span>

<span data-ttu-id="2d3af-176">Os carimbos de data e hora são sempre em UTC.</span><span class="sxs-lookup"><span data-stu-id="2d3af-176">Timestamps are always in UTC.</span></span> <span data-ttu-id="2d3af-177">Portanto, se estiver na costa do Pacífico nos EUA e for inverno, você terá algo semelhante a isto:</span><span class="sxs-lookup"><span data-stu-id="2d3af-177">So if you're on the US Pacific coast and it's winter, you might like this:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a><span data-ttu-id="2d3af-178">[Resumir](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): agregar grupos de linhas</span><span class="sxs-lookup"><span data-stu-id="2d3af-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): aggregate groups of rows</span></span>
<span data-ttu-id="2d3af-179">`Summarize` aplica uma *função de agregação* especificada em grupos de linhas.</span><span class="sxs-lookup"><span data-stu-id="2d3af-179">`Summarize` applies a specified *aggregation function* over groups of rows.</span></span>

<span data-ttu-id="2d3af-180">Por exemplo, o tempo que o seu aplicativo Web leva para responder a uma solicitação é informado no campo `duration`.</span><span class="sxs-lookup"><span data-stu-id="2d3af-180">For example, the time your web app takes to respond to a request is reported in the field `duration`.</span></span> <span data-ttu-id="2d3af-181">Vamos ver o tempo médio de resposta para todas as solicitações:</span><span class="sxs-lookup"><span data-stu-id="2d3af-181">Let's see the average response time to all requests:</span></span>

![](./media/app-insights-analytics-tour/410.png)

<span data-ttu-id="2d3af-182">Ou podemos separar o resultado em solicitações de nomes diferentes:</span><span class="sxs-lookup"><span data-stu-id="2d3af-182">Or we could separate the result into requests of different names:</span></span>

![](./media/app-insights-analytics-tour/420.png)

<span data-ttu-id="2d3af-183">`Summarize` coleta os pontos de dados no fluxo dos grupos para os quais a cláusula `by` é igualmente avaliada.</span><span class="sxs-lookup"><span data-stu-id="2d3af-183">`Summarize` collects the data points in the stream into groups for which the `by` clause evaluates equally.</span></span> <span data-ttu-id="2d3af-184">Cada valor na expressão `by` (cada nome de operação no exemplo acima) resulta em uma linha na tabela de resultados.</span><span class="sxs-lookup"><span data-stu-id="2d3af-184">Each value in the `by` expression - each operation name in the above example - results in a row in the result table.</span></span>

<span data-ttu-id="2d3af-185">Ou podemos agrupar os resultados por hora do dia:</span><span class="sxs-lookup"><span data-stu-id="2d3af-185">Or we could group results by time of day:</span></span>

![](./media/app-insights-analytics-tour/430.png)

<span data-ttu-id="2d3af-186">Observe como estamos usando a função `bin` (também conhecida como `floor`).</span><span class="sxs-lookup"><span data-stu-id="2d3af-186">Notice how we're using the `bin` function (aka `floor`).</span></span> <span data-ttu-id="2d3af-187">Se usássemos apenas `by timestamp`, cada linha de entrada acabaria em seu próprio pequeno grupo.</span><span class="sxs-lookup"><span data-stu-id="2d3af-187">If we just used `by timestamp`, every input row would end up in its own little group.</span></span> <span data-ttu-id="2d3af-188">Para qualquer escalar contínuo com horas ou números, é necessário dividir o intervalo contínuo em um número gerenciável de valores distintos.</span><span class="sxs-lookup"><span data-stu-id="2d3af-188">For any continuous scalar like times or numbers, we have to break the continuous range into a manageable number of discrete values.</span></span> <span data-ttu-id="2d3af-189">`bin`, que é simplesmente a conhecida função de arredondamento para baixo `floor`, é a maneira mais fácil de fazer isso.</span><span class="sxs-lookup"><span data-stu-id="2d3af-189">`bin` - which is just the familiar rounding-down `floor` function - is the easiest way to do that.</span></span>

<span data-ttu-id="2d3af-190">Podemos usar a mesma técnica para reduzir intervalos de cadeias de caracteres:</span><span class="sxs-lookup"><span data-stu-id="2d3af-190">We can use the same technique to reduce ranges of strings:</span></span>

![](./media/app-insights-analytics-tour/440.png)

<span data-ttu-id="2d3af-191">Observe que você pode usar `name=` para definir o nome de uma coluna de resultado, seja nas expressões de agregação, seja na cláusula by.</span><span class="sxs-lookup"><span data-stu-id="2d3af-191">Notice that you can use `name=` to set the name of a result column, either in the aggregation expressions or the by-clause.</span></span>

## <a name="counting-sampled-data"></a><span data-ttu-id="2d3af-192">Contando dados de amostra</span><span class="sxs-lookup"><span data-stu-id="2d3af-192">Counting sampled data</span></span>
<span data-ttu-id="2d3af-193">`sum(itemCount)` é a agregação recomendada para contar eventos.</span><span class="sxs-lookup"><span data-stu-id="2d3af-193">`sum(itemCount)` is the recommended aggregation to count events.</span></span> <span data-ttu-id="2d3af-194">Em muitos casos, itemCount==1, de modo que a função simplesmente conta até o número de linhas no grupo.</span><span class="sxs-lookup"><span data-stu-id="2d3af-194">In many cases, itemCount==1, so the function simply counts up the number of rows in the group.</span></span> <span data-ttu-id="2d3af-195">Contudo, quando a [amostragem](app-insights-sampling.md) estiver em operação, apenas uma fração dos eventos originais será retida como pontos de dados no Application Insights, de modo que para cada ponto de dados que você visualizar, haverá `itemCount` eventos.</span><span class="sxs-lookup"><span data-stu-id="2d3af-195">But when [sampling](app-insights-sampling.md) is in operation, only a fraction of the original events are retained as data points in Application Insights, so that for each data point you see, there are `itemCount` events.</span></span>

<span data-ttu-id="2d3af-196">Por exemplo, se a amostragem descartar 75% dos eventos originais, itemCount == 4 nos registros retidos - ou seja, para cada registro retido, houve quatro registros originais.</span><span class="sxs-lookup"><span data-stu-id="2d3af-196">For example, if sampling discards 75% of the original events, then itemCount==4 in the retained records - that is, for every retained record, there were four original records.</span></span>

<span data-ttu-id="2d3af-197">A amostragem adaptável fará com que itemCount seja maior durante períodos em que seu aplicativo estiver sendo muito usado.</span><span class="sxs-lookup"><span data-stu-id="2d3af-197">Adaptive sampling causes itemCount to be higher during periods when your application is being heavily used.</span></span>

<span data-ttu-id="2d3af-198">Portanto, a soma de itemCount dá uma boa estimativa do número original de eventos.</span><span class="sxs-lookup"><span data-stu-id="2d3af-198">Summing up itemCount therefore gives a good estimate of the original number of events.</span></span>

![](./media/app-insights-analytics-tour/510.png)

<span data-ttu-id="2d3af-199">Também há uma agregação `count()` (e uma operação de contagem), para casos em que você realmente quiser contar o número de linhas em um grupo.</span><span class="sxs-lookup"><span data-stu-id="2d3af-199">There's also a `count()` aggregation (and a count operation), for cases where you really do want to count the number of rows in a group.</span></span>

<span data-ttu-id="2d3af-200">Há uma série de [funções de agregação](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span><span class="sxs-lookup"><span data-stu-id="2d3af-200">There's a range of [aggregation functions](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>

## <a name="charting-the-results"></a><span data-ttu-id="2d3af-201">Colocando os resultados em gráficos</span><span class="sxs-lookup"><span data-stu-id="2d3af-201">Charting the results</span></span>
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

<span data-ttu-id="2d3af-202">Por padrão, os resultados são exibidos como uma tabela:</span><span class="sxs-lookup"><span data-stu-id="2d3af-202">By default, results display as a table:</span></span>

![](./media/app-insights-analytics-tour/225.png)

<span data-ttu-id="2d3af-203">Podemos fazer melhor do que a exibição de tabela.</span><span class="sxs-lookup"><span data-stu-id="2d3af-203">We can do better than the table view.</span></span> <span data-ttu-id="2d3af-204">Vamos examinar os resultados no modo de exibição de gráfico com a opção de barra vertical:</span><span class="sxs-lookup"><span data-stu-id="2d3af-204">Let's look at the results in the chart view with the vertical bar option:</span></span>

![Clique em Gráfico, escolha o gráfico de barras Vertical e atribua os eixos x e y](./media/app-insights-analytics-tour/230.png)

<span data-ttu-id="2d3af-206">Observe que, embora não tenhamos classificado os resultados por tempo (como você pode ver na exibição de tabela), a exibição de gráfico sempre mostra datetimes na ordem correta.</span><span class="sxs-lookup"><span data-stu-id="2d3af-206">Notice that although we didn't sort the results by time (as you can see in the table display), the chart display always shows datetimes in correct order.</span></span>


## <a name="timecharts"></a><span data-ttu-id="2d3af-207">Timecharts</span><span class="sxs-lookup"><span data-stu-id="2d3af-207">Timecharts</span></span>
<span data-ttu-id="2d3af-208">Mostra quantos eventos há a cada hora:</span><span class="sxs-lookup"><span data-stu-id="2d3af-208">Show how many events there are each hour:</span></span>

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

<span data-ttu-id="2d3af-209">Selecione a opção de exibição Gráfico:</span><span class="sxs-lookup"><span data-stu-id="2d3af-209">Select the Chart display option:</span></span>

![timechart](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a><span data-ttu-id="2d3af-211">Várias séries</span><span class="sxs-lookup"><span data-stu-id="2d3af-211">Multiple series</span></span>
<span data-ttu-id="2d3af-212">Várias expressões na cláusula `summarize` criam várias colunas.</span><span class="sxs-lookup"><span data-stu-id="2d3af-212">Multiple expressions in the `summarize` clause creates multiple columns.</span></span>

<span data-ttu-id="2d3af-213">Várias expressões na cláusula `by` criam várias linhas, uma para cada combinação de valores.</span><span class="sxs-lookup"><span data-stu-id="2d3af-213">Multiple expressions in the `by` clause creates multiple rows, one for each combination of values.</span></span>

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Tabela de solicitações por hora e local](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a><span data-ttu-id="2d3af-215">Segmentar um gráfico por dimensões</span><span class="sxs-lookup"><span data-stu-id="2d3af-215">Segment a chart by dimensions</span></span>
<span data-ttu-id="2d3af-216">Se você criar um gráfico de uma tabela que tenha uma coluna de cadeia de caracteres e uma coluna numérica, a cadeia de caracteres pode ser usada para dividir os dados numéricos em uma série de pontos separada.</span><span class="sxs-lookup"><span data-stu-id="2d3af-216">If you chart a table that has a string column and a numeric column, the string can be used to split the numeric data into separate series of points.</span></span> <span data-ttu-id="2d3af-217">Se houver mais de uma coluna de cadeia de caracteres, você poderá escolher qual coluna usar como o discriminador.</span><span class="sxs-lookup"><span data-stu-id="2d3af-217">If there's more than one string column, you can choose which column to use as the discriminator.</span></span>

![Segmentar um gráfico de análise](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a><span data-ttu-id="2d3af-219">Taxa de devolução</span><span class="sxs-lookup"><span data-stu-id="2d3af-219">Bounce rate</span></span>

<span data-ttu-id="2d3af-220">Converta um booliano em uma cadeia de caracteres para usá-la como um discriminador:</span><span class="sxs-lookup"><span data-stu-id="2d3af-220">Convert a boolean to a string to use it as a discriminator:</span></span>

```AIQL

    // Bounce rate: sessions with only one page view
    requests
    | where notempty(session_Id)
    | where tostring(operation_SyntheticSource) == "" // real users
    | summarize pagesInSession=sum(itemCount), sessionEnd=max(timestamp)
               by session_Id
    | extend isbounce= pagesInSession == 1
    | summarize count()
               by tostring(isbounce), bin (sessionEnd, 1h)
    | render timechart
```

### <a name="display-multiple-metrics"></a><span data-ttu-id="2d3af-221">Exibir várias métricas</span><span class="sxs-lookup"><span data-stu-id="2d3af-221">Display multiple metrics</span></span>
<span data-ttu-id="2d3af-222">Se você criar um gráfico de uma tabela com mais de uma coluna numérica, além de carimbo de data/hora, será possível exibir qualquer combinação desses itens.</span><span class="sxs-lookup"><span data-stu-id="2d3af-222">If you chart a table that has more than one numeric column, in addition to the timestamp, you can display any combination of them.</span></span>

![Segmentar um gráfico de análise](./media/app-insights-analytics-tour/110.png)

<span data-ttu-id="2d3af-224">Você deve selecionar **Não Dividir** antes de selecionar várias colunas numéricas.</span><span class="sxs-lookup"><span data-stu-id="2d3af-224">You must select **Don't Split** before you can select multiple numeric columns.</span></span> <span data-ttu-id="2d3af-225">Não é possível dividir por uma coluna de cadeia de caracteres ao mesmo tempo que exibe mais de uma coluna numérica.</span><span class="sxs-lookup"><span data-stu-id="2d3af-225">You can't split by a string column at the same time as displaying more than one numeric column.</span></span>

## <a name="daily-average-cycle"></a><span data-ttu-id="2d3af-226">Ciclo médio diário</span><span class="sxs-lookup"><span data-stu-id="2d3af-226">Daily average cycle</span></span>
<span data-ttu-id="2d3af-227">Como o uso varia na média diária?</span><span class="sxs-lookup"><span data-stu-id="2d3af-227">How does usage vary over the average day?</span></span>

<span data-ttu-id="2d3af-228">Conte solicitações pelo módulo de tempo de um dia, compartimentalizado por horas:</span><span class="sxs-lookup"><span data-stu-id="2d3af-228">Count requests by the time modulo one day, binned into hours:</span></span>

```AIQL

    requests
    | where timestamp > ago(30d)  // Override "Last 24h"
    | where tostring(operation_SyntheticSource) == "" // real users
    | extend hour = bin(timestamp % 1d , 1h)
          + datetime("2016-01-01") // Allow render on line chart
    | summarize event_count=sum(itemCount) by hour
```

![Gráfico de linhas de horas em um dia normal](./media/app-insights-analytics-tour/120.png)

> [!NOTE]
> <span data-ttu-id="2d3af-230">Observe que, no momento, temos que converter durações de tempo em datas/horas para exibir em um gráfico de linha.</span><span class="sxs-lookup"><span data-stu-id="2d3af-230">Notice that we currently have to convert time durations to datetimes in order to display on a line chart.</span></span>
>
>

## <a name="compare-multiple-daily-series"></a><span data-ttu-id="2d3af-231">Comparar várias séries diárias</span><span class="sxs-lookup"><span data-stu-id="2d3af-231">Compare multiple daily series</span></span>
<span data-ttu-id="2d3af-232">Como o uso varia de acordo com a hora do dia em diferentes países?</span><span class="sxs-lookup"><span data-stu-id="2d3af-232">How does usage vary over the time of day in different countries?</span></span>

```AIQL

     requests  
     | where timestamp > ago(30d)  // Override "Last 24h"
     | where tostring(operation_SyntheticSource) == "" // real users
     | extend hour= floor( timestamp % 1d , 1h)
           + datetime("2001-01-01")
     | summarize event_count=sum(itemCount)
       by hour, client_CountryOrRegion
     | render timechart
```

![Divisão por client_CountryOrRegion](./media/app-insights-analytics-tour/130.png)

## <a name="plot-a-distribution"></a><span data-ttu-id="2d3af-234">Plotar uma distribuição</span><span class="sxs-lookup"><span data-stu-id="2d3af-234">Plot a distribution</span></span>
<span data-ttu-id="2d3af-235">Quantas sessões existem de comprimentos diferentes?</span><span class="sxs-lookup"><span data-stu-id="2d3af-235">How many sessions are there of different lengths?</span></span>

```AIQL

    requests
    | where timestamp > ago(30d) // override "Last 24h"
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sessionDuration = max_timestamp - min_timestamp
    | where sessionDuration > 1s and sessionDuration < 3m
    | summarize count() by floor(sessionDuration, 3s)
    | project d = sessionDuration + datetime("2016-01-01"), count_
```

<span data-ttu-id="2d3af-236">A última linha é necessária para a conversão em datetime.</span><span class="sxs-lookup"><span data-stu-id="2d3af-236">The last line is required to convert to datetime.</span></span> <span data-ttu-id="2d3af-237">Atualmente, o eixo x de um gráfico só será exibido como um escalar se ele for um datetime.</span><span class="sxs-lookup"><span data-stu-id="2d3af-237">Currently the x axis of a chart is displayed as a scalar only if it is a datetime.</span></span>

<span data-ttu-id="2d3af-238">A cláusula `where` exclui sessões únicas (sessionDuration==0) e define o comprimento do eixo x.</span><span class="sxs-lookup"><span data-stu-id="2d3af-238">The `where` clause excludes one-shot sessions (sessionDuration==0) and sets the length of the x-axis.</span></span>

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[<span data-ttu-id="2d3af-239">Percentis</span><span class="sxs-lookup"><span data-stu-id="2d3af-239">Percentiles</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
<span data-ttu-id="2d3af-240">Quais intervalos de durações abordam diferentes porcentagens de sessões?</span><span class="sxs-lookup"><span data-stu-id="2d3af-240">What ranges of durations cover different percentages of sessions?</span></span>

<span data-ttu-id="2d3af-241">Use a consulta acima, mas substitua a última linha:</span><span class="sxs-lookup"><span data-stu-id="2d3af-241">Use the above query, but replace the last line:</span></span>

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s)
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
```

<span data-ttu-id="2d3af-242">Também removemos o limite máximo na cláusula where para obter números corretos, incluindo todas as sessões com mais de uma solicitação:</span><span class="sxs-lookup"><span data-stu-id="2d3af-242">We also removed the upper limit in the where clause, in order to get correct figures including all sessions with more than one request:</span></span>

![result](./media/app-insights-analytics-tour/180.png)

<span data-ttu-id="2d3af-244">O que nos mostra que:</span><span class="sxs-lookup"><span data-stu-id="2d3af-244">From which we can see that:</span></span>

* <span data-ttu-id="2d3af-245">5% das sessões têm uma duração de menos de 3 minutos e 34 segundos;</span><span class="sxs-lookup"><span data-stu-id="2d3af-245">5% of sessions have a duration of less than 3 minutes 34s;</span></span>
* <span data-ttu-id="2d3af-246">50% das sessões duram menos de 36 minutos;</span><span class="sxs-lookup"><span data-stu-id="2d3af-246">50% of sessions last less than 36 minutes;</span></span>
* <span data-ttu-id="2d3af-247">5% das sessões duram mais de 7 dias</span><span class="sxs-lookup"><span data-stu-id="2d3af-247">5% of sessions last more than 7 days</span></span>

<span data-ttu-id="2d3af-248">Para obter uma análise separada para cada país, temos apenas que trazer a coluna client_CountryOrRegion para ambos os operadores summarize:</span><span class="sxs-lookup"><span data-stu-id="2d3af-248">To get a separate breakdown for each country, we just have to bring the client_CountryOrRegion column separately through both summarize operators:</span></span>

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id, client_CountryOrRegion
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s), client_CountryOrRegion
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
      by client_CountryOrRegion
```

![](./media/app-insights-analytics-tour/190.png)

## <a name="join"></a><span data-ttu-id="2d3af-249">Ingressar</span><span class="sxs-lookup"><span data-stu-id="2d3af-249">Join</span></span>
<span data-ttu-id="2d3af-250">Temos acesso a várias tabelas, incluindo solicitações e exceções.</span><span class="sxs-lookup"><span data-stu-id="2d3af-250">We have access to several tables, including requests and exceptions.</span></span>

<span data-ttu-id="2d3af-251">Para encontrar as exceções relacionadas a uma solicitação que retornou uma resposta com falha, podemos unir as tabelas em `session_Id`:</span><span class="sxs-lookup"><span data-stu-id="2d3af-251">To find the exceptions related to a request that returned a failure response, we can join the tables on `session_Id`:</span></span>

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


<span data-ttu-id="2d3af-252">É uma prática recomendável usar `project` para selecionar apenas as colunas necessárias antes de executar a junção.</span><span class="sxs-lookup"><span data-stu-id="2d3af-252">It's good practice to use `project` to select just the columns we need before performing the join.</span></span>
<span data-ttu-id="2d3af-253">Renomeamos a coluna de carimbo de data/hora nas mesmas cláusulas.</span><span class="sxs-lookup"><span data-stu-id="2d3af-253">In the same clauses, we rename the timestamp column.</span></span>

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-to-a-variable"></a><span data-ttu-id="2d3af-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): atribuir um resultado a uma variável</span><span class="sxs-lookup"><span data-stu-id="2d3af-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): Assign a result to a variable</span></span>

<span data-ttu-id="2d3af-255">Use `let` para separar as partes da expressão anterior.</span><span class="sxs-lookup"><span data-stu-id="2d3af-255">Use `let` to separate out the parts of the previous expression.</span></span> <span data-ttu-id="2d3af-256">Os resultados não mudam:</span><span class="sxs-lookup"><span data-stu-id="2d3af-256">The results are unchanged:</span></span>

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> <span data-ttu-id="2d3af-257">No cliente do Analytics, não coloque linhas em branco entre as partes da consulta.</span><span class="sxs-lookup"><span data-stu-id="2d3af-257">In the Analytics client, don't put blank lines between the parts of the query.</span></span> <span data-ttu-id="2d3af-258">Execute tudo.</span><span class="sxs-lookup"><span data-stu-id="2d3af-258">Make sure to execute all of it.</span></span>
>

<span data-ttu-id="2d3af-259">Use `toscalar` para converter uma única célula de tabela em um valor:</span><span class="sxs-lookup"><span data-stu-id="2d3af-259">Use `toscalar` to convert a single table cell to a value:</span></span>

```AIQL
let topCities =  toscalar (
   requests
   | summarize count() by client_City 
   | top n by count_ 
   | summarize makeset(client_City));
requests
| where client_City in (topCities(3)) 
| summarize count() by client_City;
```


### <a name="functions"></a><span data-ttu-id="2d3af-260">Funções</span><span class="sxs-lookup"><span data-stu-id="2d3af-260">Functions</span></span>

<span data-ttu-id="2d3af-261">Use *Let* para definir uma função:</span><span class="sxs-lookup"><span data-stu-id="2d3af-261">Use *Let* to define a function:</span></span>

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a><span data-ttu-id="2d3af-262">Acessando objetos aninhados</span><span class="sxs-lookup"><span data-stu-id="2d3af-262">Accessing nested objects</span></span>
<span data-ttu-id="2d3af-263">Os objetos aninhados podem ser acessados facilmente.</span><span class="sxs-lookup"><span data-stu-id="2d3af-263">Nested objects can be accessed easily.</span></span> <span data-ttu-id="2d3af-264">Por exemplo, no fluxo de exceções, você verá objetos estruturados como este:</span><span class="sxs-lookup"><span data-stu-id="2d3af-264">For example, in the exceptions stream you can see structured objects like this:</span></span>

![result](./media/app-insights-analytics-tour/520.png)

<span data-ttu-id="2d3af-266">Você pode mesclá-lo escolhendo as propriedades que te interessam:</span><span class="sxs-lookup"><span data-stu-id="2d3af-266">You can flatten it by choosing the properties you're interested in:</span></span>

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="2d3af-267">Observe que você precisa converter o resultado no tipo apropriado.</span><span class="sxs-lookup"><span data-stu-id="2d3af-267">Note that you need to cast the result to the appropriate type.</span></span>


## <a name="custom-properties-and-measurements"></a><span data-ttu-id="2d3af-268">Medidas e propriedades personalizadas</span><span class="sxs-lookup"><span data-stu-id="2d3af-268">Custom properties and measurements</span></span>
<span data-ttu-id="2d3af-269">Se o seu aplicativo anexar [dimensões personalizadas (propriedades) e medidas personalizadas](app-insights-api-custom-events-metrics.md#properties) a eventos, você os verá nos objetos `customDimensions` e `customMeasurements`.</span><span class="sxs-lookup"><span data-stu-id="2d3af-269">If your application attaches [custom dimensions (properties) and custom measurements](app-insights-api-custom-events-metrics.md#properties) to events, then you will see them in the `customDimensions` and `customMeasurements` objects.</span></span>

<span data-ttu-id="2d3af-270">Por exemplo, se o seu aplicativo inclui:</span><span class="sxs-lookup"><span data-stu-id="2d3af-270">For example, if your app includes:</span></span>

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

<span data-ttu-id="2d3af-271">Para extrair esses valores na Análise:</span><span class="sxs-lookup"><span data-stu-id="2d3af-271">To extract these values in Analytics:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast to expected type

```

<span data-ttu-id="2d3af-272">Para verificar se uma dimensão personalizada é de um tipo específico:</span><span class="sxs-lookup"><span data-stu-id="2d3af-272">To verify whether a custom dimension is of a particular type:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a><span data-ttu-id="2d3af-273">Painéis</span><span class="sxs-lookup"><span data-stu-id="2d3af-273">Dashboards</span></span>
<span data-ttu-id="2d3af-274">Você pode fixar os resultados em um painel para reunir todos os seus gráficos e suas tabelas mais importantes.</span><span class="sxs-lookup"><span data-stu-id="2d3af-274">You can pin your results to a dashboard in order to bring together all your most important charts and tables.</span></span>

* <span data-ttu-id="2d3af-275">[Painel compartilhado do Azure](app-insights-dashboards.md#share-dashboards): clique no ícone de pino.</span><span class="sxs-lookup"><span data-stu-id="2d3af-275">[Azure shared dashboard](app-insights-dashboards.md#share-dashboards): Click the pin icon.</span></span> <span data-ttu-id="2d3af-276">Antes de fazer isso, você deve ter um painel compartilhado.</span><span class="sxs-lookup"><span data-stu-id="2d3af-276">Before you do this, you must have a shared dashboard.</span></span> <span data-ttu-id="2d3af-277">No portal do Azure, abra ou crie um painel e clique em Compartilhar.</span><span class="sxs-lookup"><span data-stu-id="2d3af-277">In the Azure portal, open or create a dashboard and click Share.</span></span>
* <span data-ttu-id="2d3af-278">[Painel do Power BI](app-insights-export-power-bi.md): clique em Exportar, Consulta do Power BI.</span><span class="sxs-lookup"><span data-stu-id="2d3af-278">[Power BI dashboard](app-insights-export-power-bi.md): Click Export, Power BI Query.</span></span> <span data-ttu-id="2d3af-279">Uma vantagem dessa alternativa é que você pode exibir sua consulta juntamente com outros resultados de uma ampla variedade de fontes.</span><span class="sxs-lookup"><span data-stu-id="2d3af-279">An advantage of this alternative is that you can display your query alongside other results from a wide range of sources.</span></span>

## <a name="combine-with-imported-data"></a><span data-ttu-id="2d3af-280">Combinar com dados importados</span><span class="sxs-lookup"><span data-stu-id="2d3af-280">Combine with imported data</span></span>

<span data-ttu-id="2d3af-281">Os relatórios do Analytics parecem ótimos no painel, mas, às vezes, você pode querer colocar os dados em um formato mais fácil de entender.</span><span class="sxs-lookup"><span data-stu-id="2d3af-281">Analytics reports look great on the dashboard, but sometimes you want to translate the data to a more digestible form.</span></span> <span data-ttu-id="2d3af-282">Por exemplo, suponha que os usuários autenticados sejam identificados na telemetria por um alias.</span><span class="sxs-lookup"><span data-stu-id="2d3af-282">For example, suppose your authenticated users are identified in the telemetry by an alias.</span></span> <span data-ttu-id="2d3af-283">Você gostaria de mostrar os nomes reais nos resultados.</span><span class="sxs-lookup"><span data-stu-id="2d3af-283">You'd like to show their real names in your results.</span></span> <span data-ttu-id="2d3af-284">Para fazer isso, você precisará de um arquivo CSV que mapeie os aliases para os nomes reais.</span><span class="sxs-lookup"><span data-stu-id="2d3af-284">To do this, you need a CSV file that maps from the aliases to the real names.</span></span>

<span data-ttu-id="2d3af-285">Você pode importar um arquivo de dados e usá-lo assim como qualquer uma das tabelas padrão (solicitações, exceções, etc.).</span><span class="sxs-lookup"><span data-stu-id="2d3af-285">You can import a data file and use it just like any of the standard tables (requests, exceptions, and so on).</span></span> <span data-ttu-id="2d3af-286">É possível consultá-la sozinha ou uni-la a outras tabelas.</span><span class="sxs-lookup"><span data-stu-id="2d3af-286">Either query it on its own, or join it with other tables.</span></span> <span data-ttu-id="2d3af-287">Por exemplo, se houver uma tabela chamada usermap e ela tiver as colunas `realName` e `userId`, você poderá usá-la para converter o campo `user_AuthenticatedId` na telemetria de solicitação:</span><span class="sxs-lookup"><span data-stu-id="2d3af-287">For example, if you have a table named usermap, and it has columns `realName` and `userId`, then you can use it to translate the `user_AuthenticatedId` field in the request telemetry:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get the realName field from the usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

<span data-ttu-id="2d3af-288">Para importar uma tabela, na folha Esquema, em **Outras Fontes de Dados**, siga as instruções para adicionar uma nova fonte de dados carregando uma amostra dos seus dados.</span><span class="sxs-lookup"><span data-stu-id="2d3af-288">To import a table, in the Schema blade, under **Other Data Sources**, follow the instructions to add a new data source, by uploading a sample of your data.</span></span> <span data-ttu-id="2d3af-289">Em seguida, você poderá usar essa definição para carregar as tabelas.</span><span class="sxs-lookup"><span data-stu-id="2d3af-289">Then you can use this definition to upload tables.</span></span>

<span data-ttu-id="2d3af-290">O recurso de importação está em visualização, por isso você verá inicialmente um link “Fale conosco” em “Outras fontes de dados”.</span><span class="sxs-lookup"><span data-stu-id="2d3af-290">The import feature is currently in preview, so you will initially see a "Contact us" link under "Other data sources."</span></span> <span data-ttu-id="2d3af-291">Use-o para se inscrever no programa de visualização e o link será substituído por um botão “Adicionar nova fonte de dados”.</span><span class="sxs-lookup"><span data-stu-id="2d3af-291">Use this to sign up to the preview program, and the link will then be replaced by an "Add new data source" button.</span></span>


## <a name="tables"></a><span data-ttu-id="2d3af-292">Tabelas</span><span class="sxs-lookup"><span data-stu-id="2d3af-292">Tables</span></span>
<span data-ttu-id="2d3af-293">O fluxo de telemetria recebido de seu aplicativo é acessível por meio de várias tabelas.</span><span class="sxs-lookup"><span data-stu-id="2d3af-293">The stream of telemetry received from your app is accessible through several tables.</span></span> <span data-ttu-id="2d3af-294">O esquema de propriedades disponível para cada tabela está visível na parte esquerda da janela.</span><span class="sxs-lookup"><span data-stu-id="2d3af-294">The schema of properties available for each table is visible at the left of the window.</span></span>

### <a name="requests-table"></a><span data-ttu-id="2d3af-295">Tabela de solicitações</span><span class="sxs-lookup"><span data-stu-id="2d3af-295">Requests table</span></span>
<span data-ttu-id="2d3af-296">Conte as solicitações HTTP para seu aplicativo Web e segmento por nome de página:</span><span class="sxs-lookup"><span data-stu-id="2d3af-296">Count HTTP requests to your web app and segment by page name:</span></span>

![Conte solicitações segmentadas por nome](./media/app-insights-analytics-tour/analytics-count-requests.png)

<span data-ttu-id="2d3af-298">Descubra as solicitações que mais falham:</span><span class="sxs-lookup"><span data-stu-id="2d3af-298">Find the requests that fail most:</span></span>

![Conte solicitações segmentadas por nome](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a><span data-ttu-id="2d3af-300">Tabela de eventos personalizada</span><span class="sxs-lookup"><span data-stu-id="2d3af-300">Custom events table</span></span>
<span data-ttu-id="2d3af-301">Se usar [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) para enviar seus próprios eventos, você poderá lê-los nessa tabela.</span><span class="sxs-lookup"><span data-stu-id="2d3af-301">If you use [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) to send your own events, you can read them from this table.</span></span>

<span data-ttu-id="2d3af-302">Vejamos um exemplo em que o código do aplicativo contém estas linhas:</span><span class="sxs-lookup"><span data-stu-id="2d3af-302">Let's take an example where your app code contains these lines:</span></span>

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

<span data-ttu-id="2d3af-303">Exiba a frequência destes eventos:</span><span class="sxs-lookup"><span data-stu-id="2d3af-303">Display the frequency of these events:</span></span>

![Taxa de exibição de eventos personalizados](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

<span data-ttu-id="2d3af-305">Extrair medidas e dimensões de eventos:</span><span class="sxs-lookup"><span data-stu-id="2d3af-305">Extract measurements and dimensions from the events:</span></span>

![Taxa de exibição de eventos personalizados](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a><span data-ttu-id="2d3af-307">Tabela de métricas personalizada</span><span class="sxs-lookup"><span data-stu-id="2d3af-307">Custom metrics table</span></span>
<span data-ttu-id="2d3af-308">Se estiver usando [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) para enviar seus próprios valores de métricas, você encontrará os resultados no fluxo **customMetrics**.</span><span class="sxs-lookup"><span data-stu-id="2d3af-308">If you are using [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) to send your own metric values, you’ll find its results in the **customMetrics** stream.</span></span> <span data-ttu-id="2d3af-309">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2d3af-309">For example:</span></span>  

![Métricas personalizadas na análise do Application Insights](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> <span data-ttu-id="2d3af-311">No [Metrics Explorer](app-insights-metrics-explorer.md), todas as medidas personalizadas anexadas a qualquer tipo de telemetria aparecem juntas na folha de métricas, juntamente com métricas enviadas usando `TrackMetric()`.</span><span class="sxs-lookup"><span data-stu-id="2d3af-311">In [Metrics Explorer](app-insights-metrics-explorer.md), all custom measurements attached to any type of telemetry appear together in the metrics blade along with metrics sent using `TrackMetric()`.</span></span> <span data-ttu-id="2d3af-312">No Analytics, no entanto, as medidas personalizadas ainda estão conectadas a qualquer tipo de telemetria no qual foram realizadas, eventos ou solicitações, entre outros, enquanto as métricas enviadas pelo TrackMetric são exibidas em seu próprio fluxo.</span><span class="sxs-lookup"><span data-stu-id="2d3af-312">But in Analytics, custom measurements are still attached to whichever type of telemetry they were carried on - events or requests, and so on - while metrics sent by TrackMetric appear in their own stream.</span></span>
>
>

### <a name="performance-counters-table"></a><span data-ttu-id="2d3af-313">Tabela de contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="2d3af-313">Performance counters table</span></span>
<span data-ttu-id="2d3af-314">Os [contadores de desempenho](app-insights-performance-counters.md) mostram métricas básicas do sistema para seu aplicativo, tais como CPU, memória e uso de rede.</span><span class="sxs-lookup"><span data-stu-id="2d3af-314">[Performance counters](app-insights-performance-counters.md) show you basic system metrics for your app, such as CPU, memory, and network utilization.</span></span> <span data-ttu-id="2d3af-315">Você pode configurar o SDK para enviar outros contadores, incluindo seus próprios contadores personalizados.</span><span class="sxs-lookup"><span data-stu-id="2d3af-315">You can configure the SDK to send additional counters, including your own custom counters.</span></span>

<span data-ttu-id="2d3af-316">O esquema **performanceCounters** expõe o nome `category`, `counter` e o nome `instance` de cada contador de desempenho.</span><span class="sxs-lookup"><span data-stu-id="2d3af-316">The **performanceCounters** schema exposes the `category`, `counter` name, and `instance` name of each performance counter.</span></span> <span data-ttu-id="2d3af-317">Nomes de instância do contador só são aplicáveis a alguns contadores de desempenho e geralmente indicam o nome do processo ao qual a contagem está relacionada.</span><span class="sxs-lookup"><span data-stu-id="2d3af-317">Counter instance names are only applicable to some performance counters, and typically indicate the name of the process to which the count relates.</span></span> <span data-ttu-id="2d3af-318">Na telemetria de cada aplicativo, você verá apenas os contadores para aquele aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2d3af-318">In the telemetry for each application, you’ll see only the counters for that application.</span></span> <span data-ttu-id="2d3af-319">Por exemplo, para ver quais contadores estão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="2d3af-319">For example, to see what counters are available:</span></span>

![Contadores de desempenho na análise do Application Insights](./media/app-insights-analytics-tour/analytics-performance-counters.png)

<span data-ttu-id="2d3af-321">Para obter um gráfico de memória disponível do período selecionado:</span><span class="sxs-lookup"><span data-stu-id="2d3af-321">To get a chart of available memory over the selected period:</span></span>

![Gráfico de tempo da memória na análise do Application Insights](./media/app-insights-analytics-tour/analytics-available-memory.png)

<span data-ttu-id="2d3af-323">Como outras telemetrias, o **performanceCounters** também tem uma coluna `cloud_RoleInstance` que indica a identidade do computador host no qual seu aplicativo está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="2d3af-323">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates the identity of the host machine on which your app is running.</span></span> <span data-ttu-id="2d3af-324">Por exemplo, para comparar o desempenho do seu aplicativo em diferentes computadores:</span><span class="sxs-lookup"><span data-stu-id="2d3af-324">For example, to compare the performance of your app on the different machines:</span></span>

![Desempenho segmentado por instância de função na análise do Application Insights](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a><span data-ttu-id="2d3af-326">Tabela de exceções</span><span class="sxs-lookup"><span data-stu-id="2d3af-326">Exceptions table</span></span>
<span data-ttu-id="2d3af-327">As [exceções relatadas pelo seu aplicativo](app-insights-asp-net-exceptions.md) estão disponíveis nessa tabela.</span><span class="sxs-lookup"><span data-stu-id="2d3af-327">[Exceptions reported by your app](app-insights-asp-net-exceptions.md) are available in this table.</span></span>

<span data-ttu-id="2d3af-328">Para localizar a solicitação HTTP que seu aplicativo estava manipulando quando a exceção foi gerada, ingresse em operation_Id:</span><span class="sxs-lookup"><span data-stu-id="2d3af-328">To find the HTTP request that your app was handling when the exception was raised, join on operation_Id:</span></span>

![Ingressar em exceções com solicitações em operation_Id](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a><span data-ttu-id="2d3af-330">Tabela de intervalos do navegador</span><span class="sxs-lookup"><span data-stu-id="2d3af-330">Browser timings table</span></span>
<span data-ttu-id="2d3af-331">`browserTimings` mostra os dados de carregamento de página coletados nos navegadores de seus usuários.</span><span class="sxs-lookup"><span data-stu-id="2d3af-331">`browserTimings` shows page load data collected in your users' browsers.</span></span>

<span data-ttu-id="2d3af-332">[Configure seu aplicativo para a telemetria do lado do cliente](app-insights-javascript.md) para ver essas métricas.</span><span class="sxs-lookup"><span data-stu-id="2d3af-332">[Set up your app for client-side telemetry](app-insights-javascript.md) in order to see these metrics.</span></span>

<span data-ttu-id="2d3af-333">O esquema inclui [métricas que indicam os comprimentos de diferentes etapas do processo de carregamento de página](app-insights-javascript.md#page-load-performance).</span><span class="sxs-lookup"><span data-stu-id="2d3af-333">The schema includes [metrics indicating the lengths of different stages of the page loading process](app-insights-javascript.md#page-load-performance).</span></span> <span data-ttu-id="2d3af-334">(Elas não indicam o tempo que os usuários levam para ler uma página.)</span><span class="sxs-lookup"><span data-stu-id="2d3af-334">(They don’t indicate the length of time your users read a page.)</span></span>  

<span data-ttu-id="2d3af-335">Mostrar a popularidade de diferentes páginas e o tempo de carregamento para cada página:</span><span class="sxs-lookup"><span data-stu-id="2d3af-335">Show the popularities of different pages, and load times for each page:</span></span>

![Tempos de carregamento de página no Analytics](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a><span data-ttu-id="2d3af-337">Tabela de resultados de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="2d3af-337">Availability results table</span></span>
<span data-ttu-id="2d3af-338">`availabilityResults` mostra os resultados de seus [testes da Web](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="2d3af-338">`availabilityResults` shows the results of your [web tests](app-insights-monitor-web-app-availability.md).</span></span> <span data-ttu-id="2d3af-339">Cada execução dos testes de cada local de teste é relatada separadamente.</span><span class="sxs-lookup"><span data-stu-id="2d3af-339">Each run of your tests from each test location is reported separately.</span></span>

![Tempos de carregamento de página no Analytics](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a><span data-ttu-id="2d3af-341">Tabela de dependências</span><span class="sxs-lookup"><span data-stu-id="2d3af-341">Dependencies table</span></span>
<span data-ttu-id="2d3af-342">Contém os resultados de chamadas que seu aplicativo fez para bancos de dados e APIs REST e outras chamadas para TrackDependency().</span><span class="sxs-lookup"><span data-stu-id="2d3af-342">Contains results of calls that your app makes to databases and REST APIs, and other calls to TrackDependency().</span></span> <span data-ttu-id="2d3af-343">Também inclui chamadas AJAX feitas no navegador.</span><span class="sxs-lookup"><span data-stu-id="2d3af-343">Also includes AJAX calls made from the browser.</span></span>

<span data-ttu-id="2d3af-344">Chamadas AJAX no navegador:</span><span class="sxs-lookup"><span data-stu-id="2d3af-344">AJAX calls from the browser:</span></span>

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

<span data-ttu-id="2d3af-345">Chamadas de dependência do servidor:</span><span class="sxs-lookup"><span data-stu-id="2d3af-345">Dependency calls from the server:</span></span>

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

<span data-ttu-id="2d3af-346">Os resultados de dependência no lado do servidor sempre mostrarão `success==False` se o Agente do Application Insights não estiver instalado.</span><span class="sxs-lookup"><span data-stu-id="2d3af-346">Server-side dependency results always show `success==False` if the Application Insights Agent is not installed.</span></span> <span data-ttu-id="2d3af-347">No entanto, os outros dados estarão corretos.</span><span class="sxs-lookup"><span data-stu-id="2d3af-347">However, the other data are correct.</span></span>

### <a name="traces-table"></a><span data-ttu-id="2d3af-348">Tabela de rastreamentos</span><span class="sxs-lookup"><span data-stu-id="2d3af-348">Traces table</span></span>
<span data-ttu-id="2d3af-349">Contém a telemetria enviada pelo seu aplicativo usando TrackTrace() ou [outras estruturas de registro](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="2d3af-349">Contains the telemetry sent by your app using TrackTrace(), or [other logging frameworks](app-insights-asp-net-trace-logs.md).</span></span>

## <a name="video"></a><span data-ttu-id="2d3af-350">Vídeo</span><span class="sxs-lookup"><span data-stu-id="2d3af-350">Video</span></span> 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

<span data-ttu-id="2d3af-351">Consultas avançadas:</span><span class="sxs-lookup"><span data-stu-id="2d3af-351">Advanced queries:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a><span data-ttu-id="2d3af-352">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2d3af-352">Next steps</span></span>
* [<span data-ttu-id="2d3af-353">Referência de linguagem de análise</span><span class="sxs-lookup"><span data-stu-id="2d3af-353">Analytics language reference</span></span>](app-insights-analytics-reference.md)
* <span data-ttu-id="2d3af-354">[Roteiro dos usuários do SQL](https://aka.ms/sql-analytics) converte as linguagens mais comuns.</span><span class="sxs-lookup"><span data-stu-id="2d3af-354">[SQL-users' cheat sheet](https://aka.ms/sql-analytics) translates the most common idioms.</span></span>

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
