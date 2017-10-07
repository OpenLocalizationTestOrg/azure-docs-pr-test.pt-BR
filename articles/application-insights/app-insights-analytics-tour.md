---
title: "tour aaaA por meio de análise no Insights de aplicativo do Azure | Microsoft Docs"
description: "Exemplos curtos de todas as consultas de saudação principal na análise, Olá poderosa ferramenta de pesquisa do Application Insights."
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
ms.openlocfilehash: c268e26c6bf93ac2ee2a9d5e83613150dcf90b04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="a-tour-of-analytics-in-application-insights"></a><span data-ttu-id="b2d58-103">Um tour pela Análise no Application Insights</span><span class="sxs-lookup"><span data-stu-id="b2d58-103">A tour of Analytics in Application Insights</span></span>
<span data-ttu-id="b2d58-104">[Análise de](app-insights-analytics.md) é o recurso de pesquisa poderoso saudação do [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b2d58-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="b2d58-105">Essas páginas descrevem a linguagem de consulta do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b2d58-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="b2d58-106">**[Assistir ao vídeo introdutório Olá](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="b2d58-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="b2d58-107">**[Faça o test drive análise sobre nossos dados simulados](https://analytics.applicationinsights.io/demo)**  se seu aplicativo não esteja enviando dados tooApplication Insights ainda.</span><span class="sxs-lookup"><span data-stu-id="b2d58-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>
* <span data-ttu-id="b2d58-108">**[Roteiro de SQL-usuários](https://aka.ms/sql-analytics)**  converte as linguagens mais comuns de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2d58-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates hello most common idioms.</span></span>

<span data-ttu-id="b2d58-109">Vamos dar um passo a passo tooget algumas consultas básicas que você iniciou.</span><span class="sxs-lookup"><span data-stu-id="b2d58-109">Let's take a walk through some basic queries tooget you started.</span></span>

## <a name="connect-tooyour-application-insights-data"></a><span data-ttu-id="b2d58-110">Conecte-se a dados do Application Insights tooyour</span><span class="sxs-lookup"><span data-stu-id="b2d58-110">Connect tooyour Application Insights data</span></span>
<span data-ttu-id="b2d58-111">Abra o Analytics na [folha de visão geral](app-insights-dashboards.md) de seu aplicativo no Application Insights:</span><span class="sxs-lookup"><span data-stu-id="b2d58-111">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span>

![Abra o portal.azure.com, abra o recurso do Application Insights e clique em Análise.](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a><span data-ttu-id="b2d58-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): mostre-me n linhas</span><span class="sxs-lookup"><span data-stu-id="b2d58-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): show me n rows</span></span>
<span data-ttu-id="b2d58-114">Os pontos de dados que registram em log operações de usuário (geralmente solicitações HTTP recebidas pelo seu aplicativo Web) são armazenados em uma tabela chamada `requests`.</span><span class="sxs-lookup"><span data-stu-id="b2d58-114">Data points that log user operations (typically HTTP requests received by your web app) are stored in a table called `requests`.</span></span> <span data-ttu-id="b2d58-115">Cada linha é um ponto de dados de telemetria recebido do hello Application Insights SDK em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b2d58-115">Each row is a telemetry data point received from hello Application Insights SDK in your app.</span></span>

<span data-ttu-id="b2d58-116">Vamos começar examinando algumas linhas de exemplo de tabela hello:</span><span class="sxs-lookup"><span data-stu-id="b2d58-116">Let's start by examining a few sample rows of hello table:</span></span>

![results](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> <span data-ttu-id="b2d58-118">Coloque o cursor de saudação em algum lugar na instrução de saudação antes de clicar em Ir.</span><span class="sxs-lookup"><span data-stu-id="b2d58-118">Put hello cursor somewhere in hello statement before you click Go.</span></span> <span data-ttu-id="b2d58-119">Você pode dividir uma instrução em mais de uma linha, mas não coloque linhas em branco em uma instrução.</span><span class="sxs-lookup"><span data-stu-id="b2d58-119">You can split a statement over more than one line, but don't put blank lines in a statement.</span></span> <span data-ttu-id="b2d58-120">Linhas em branco são uma maneira conveniente de tookeep várias separam consultas na janela de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2d58-120">Blank lines are a convenient way tookeep several separate queries in hello window.</span></span>
>
>

<span data-ttu-id="b2d58-121">Escolha colunas, arraste-as, agrupe por colunas e filtre:</span><span class="sxs-lookup"><span data-stu-id="b2d58-121">Choose columns, drag them, group by columns, and filter:</span></span>

![Clique na seleção de coluna no canto superior direito dos resultados](./media/app-insights-analytics-tour/030.png)

<span data-ttu-id="b2d58-123">Expanda detalhes item toosee hello:</span><span class="sxs-lookup"><span data-stu-id="b2d58-123">Expand any item toosee hello detail:</span></span>

![Escolha Tabela e use Configurar Colunas](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> <span data-ttu-id="b2d58-125">Clique em início de saudação de uma coluna ordem toore Olá resulta disponíveis no navegador da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2d58-125">Click hello head of a column toore-order hello results available in hello web browser.</span></span> <span data-ttu-id="b2d58-126">Mas, lembre-se de que, para um conjunto de resultados grande, número de saudação do navegador de toohello baixado de linhas é limitado.</span><span class="sxs-lookup"><span data-stu-id="b2d58-126">But be aware that for a large result set, hello number of rows downloaded toohello browser is limited.</span></span> <span data-ttu-id="b2d58-127">Classificando dessa maneira não mostra sempre Olá real maior ou menor de itens.</span><span class="sxs-lookup"><span data-stu-id="b2d58-127">Sorting this way doesn't always show you hello actual highest or lowest items.</span></span> <span data-ttu-id="b2d58-128">itens de toosort confiável, usam Olá `top` ou `sort` operador.</span><span class="sxs-lookup"><span data-stu-id="b2d58-128">toosort items reliably, use hello `top` or `sort` operator.</span></span>
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a><span data-ttu-id="b2d58-129">[Superior](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) e [classificação](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span><span class="sxs-lookup"><span data-stu-id="b2d58-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) and [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span></span>
<span data-ttu-id="b2d58-130">`take`é um exemplo rápido de um resultado de tooget útil, mas mostra linhas da tabela de saudação em nenhuma ordem específica.</span><span class="sxs-lookup"><span data-stu-id="b2d58-130">`take` is useful tooget a quick sample of a result, but it shows rows from hello table in no particular order.</span></span> <span data-ttu-id="b2d58-131">tooget uma exibição ordenada, use `top` (para obter um exemplo) ou `sort` (pela tabela inteira de saudação).</span><span class="sxs-lookup"><span data-stu-id="b2d58-131">tooget an ordered view, use `top` (for a sample) or `sort` (over hello whole table).</span></span>

<span data-ttu-id="b2d58-132">Mostre-me primeiras linhas n hello, ordenadas por uma coluna específica:</span><span class="sxs-lookup"><span data-stu-id="b2d58-132">Show me hello first n rows, ordered by a particular column:</span></span>

```AIQL

    requests | top 10 by timestamp desc
```

* <span data-ttu-id="b2d58-133">*Sintaxe:* a maioria dos operadores têm parâmetros de palavra-chave, como `by`.</span><span class="sxs-lookup"><span data-stu-id="b2d58-133">*Syntax:* Most operators have keyword parameters such as `by`.</span></span>
* <span data-ttu-id="b2d58-134">`desc` = ordem decrescente, `asc` = ordem crescente.</span><span class="sxs-lookup"><span data-stu-id="b2d58-134">`desc` = descending order, `asc` = ascending.</span></span>

![](./media/app-insights-analytics-tour/260.png)

<span data-ttu-id="b2d58-135">`top...` é uma maneira mais eficaz de dizer `sort ... | take...`.</span><span class="sxs-lookup"><span data-stu-id="b2d58-135">`top...` is a more performant way of saying `sort ... | take...`.</span></span> <span data-ttu-id="b2d58-136">Poderíamos ter escrito:</span><span class="sxs-lookup"><span data-stu-id="b2d58-136">We could have written:</span></span>

```AIQL

    requests | sort by timestamp desc | take 10
```

<span data-ttu-id="b2d58-137">resultado de saudação seria Olá mesmo, mas ele será executado um pouco mais lenta.</span><span class="sxs-lookup"><span data-stu-id="b2d58-137">hello result would be hello same, but it would run a bit more slowly.</span></span> <span data-ttu-id="b2d58-138">(Também é possível escrever `order`, que é um alias de `sort`.)</span><span class="sxs-lookup"><span data-stu-id="b2d58-138">(You could also write `order`, which is an alias of `sort`.)</span></span>

<span data-ttu-id="b2d58-139">cabeçalhos de coluna Olá no modo de tabela Olá também podem ser usado toosort Olá resultados na tela hello.</span><span class="sxs-lookup"><span data-stu-id="b2d58-139">hello column headers in hello table view can also be used toosort hello results on hello screen.</span></span> <span data-ttu-id="b2d58-140">Mas certamente, se você usou `take` ou `top` tooretrieve apenas parte de uma tabela, você terá apenas reordenar Olá registros recuperar.</span><span class="sxs-lookup"><span data-stu-id="b2d58-140">But of course, if you've used `take` or `top` tooretrieve just part of a table, you'll only re-order hello records you've retrieved.</span></span>

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a><span data-ttu-id="b2d58-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtragem de uma condição</span><span class="sxs-lookup"><span data-stu-id="b2d58-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtering on a condition</span></span>

<span data-ttu-id="b2d58-142">Vamos ver apenas as solicitações que retornaram um código de resultado específico:</span><span class="sxs-lookup"><span data-stu-id="b2d58-142">Let's see just requests that returned a particular result code:</span></span>

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

<span data-ttu-id="b2d58-143">Olá `where` operador obtém uma expressão booleana.</span><span class="sxs-lookup"><span data-stu-id="b2d58-143">hello `where` operator takes a Boolean expression.</span></span> <span data-ttu-id="b2d58-144">Eis alguns pontos importantes sobre eles:</span><span class="sxs-lookup"><span data-stu-id="b2d58-144">Here are some key points about them:</span></span>

* <span data-ttu-id="b2d58-145">`and`, `or`: Operadores booleanos</span><span class="sxs-lookup"><span data-stu-id="b2d58-145">`and`, `or`: Boolean operators</span></span>
* <span data-ttu-id="b2d58-146">`==`, `<>`, `!=`: igual a e diferente de</span><span class="sxs-lookup"><span data-stu-id="b2d58-146">`==`, `<>`, `!=` : equal and not equal</span></span>
* <span data-ttu-id="b2d58-147">`=~`, `!~`: cadeia de caracteres que não diferencia maiúsculas de minúsculas "igual a" e "diferente de".</span><span class="sxs-lookup"><span data-stu-id="b2d58-147">`=~`, `!~` : case-insensitive string equal and not equal.</span></span> <span data-ttu-id="b2d58-148">Há muitos outros operadores de comparação de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b2d58-148">There are lots more string comparison operators.</span></span>

<!---Read all about [scalar expressions]().--->

### <a name="getting-hello-right-type"></a><span data-ttu-id="b2d58-149">Obtendo o tipo correto de saudação</span><span class="sxs-lookup"><span data-stu-id="b2d58-149">Getting hello right type</span></span>
<span data-ttu-id="b2d58-150">Solicitações malsucedidas de localização:</span><span class="sxs-lookup"><span data-stu-id="b2d58-150">Find unsuccessful requests:</span></span>

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a><span data-ttu-id="b2d58-151">Hora</span><span class="sxs-lookup"><span data-stu-id="b2d58-151">Time</span></span>

<span data-ttu-id="b2d58-152">Por padrão, as consultas são restrito toohello últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="b2d58-152">By default, your queries are restricted toohello last 24 hours.</span></span> <span data-ttu-id="b2d58-153">Mas você pode alterar esse intervalo:</span><span class="sxs-lookup"><span data-stu-id="b2d58-153">But you can change this range:</span></span>

![](./media/app-insights-analytics-tour/change-time-range.png)

<span data-ttu-id="b2d58-154">Substituir o intervalo de tempo de saudação escrevendo qualquer consulta que menciona `timestamp` em uma cláusula where.</span><span class="sxs-lookup"><span data-stu-id="b2d58-154">Override hello time range by writing any query that mentions `timestamp` in a where-clause.</span></span> <span data-ttu-id="b2d58-155">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b2d58-155">For example:</span></span>

```AIQL

    // What were hello slowest requests over hello past 3 days?
    requests
    | where timestamp > ago(3d)  // Override hello time range
    | top 5 by duration
```

<span data-ttu-id="b2d58-156">recurso de intervalo de tempo de saudação é equivalente tooa 'where' cláusula inserida após cada uma das tabelas de origem Olá mencionado.</span><span class="sxs-lookup"><span data-stu-id="b2d58-156">hello time range feature is equivalent tooa 'where' clause inserted after each mention of one of hello source tables.</span></span>

<span data-ttu-id="b2d58-157">`ago(3d)` significa 'três dias atrás'.</span><span class="sxs-lookup"><span data-stu-id="b2d58-157">`ago(3d)` means 'three days ago'.</span></span> <span data-ttu-id="b2d58-158">Outras unidades de tempo incluem horas (`2h`, `2.5h`), minutos (`25m`) e segundos (`10s`).</span><span class="sxs-lookup"><span data-stu-id="b2d58-158">Other units of time include hours (`2h`, `2.5h`), minutes (`25m`), and seconds (`10s`).</span></span>

<span data-ttu-id="b2d58-159">Outros exemplos:</span><span class="sxs-lookup"><span data-stu-id="b2d58-159">Other examples:</span></span>

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

<span data-ttu-id="b2d58-160">[Referência de datas e horas](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span><span class="sxs-lookup"><span data-stu-id="b2d58-160">[Dates and times reference](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span></span>


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a><span data-ttu-id="b2d58-161">[Projeto](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): selecionar, renomear e computar colunas</span><span class="sxs-lookup"><span data-stu-id="b2d58-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): select, rename, and compute columns</span></span>
<span data-ttu-id="b2d58-162">Use [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick apenas colunas Olá desejado:</span><span class="sxs-lookup"><span data-stu-id="b2d58-162">Use [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick out just hello columns you want:</span></span>

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

<span data-ttu-id="b2d58-163">Você também pode renomear e definir novas colunas:</span><span class="sxs-lookup"><span data-stu-id="b2d58-163">You can also rename columns and define new ones:</span></span>

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

* <span data-ttu-id="b2d58-165">Os nomes de coluna poderão incluir espaços ou símbolos se eles estiverem entre colchetes, desta forma: `['...']` ou `["..."]`</span><span class="sxs-lookup"><span data-stu-id="b2d58-165">Column names can include spaces or symbols if they are bracketed like this: `['...']` or `["..."]`</span></span>
* <span data-ttu-id="b2d58-166">`%`Olá é algo comum do operador de módulo.</span><span class="sxs-lookup"><span data-stu-id="b2d58-166">`%` is hello usual modulo operator.</span></span>
* <span data-ttu-id="b2d58-167">`1d` (que é o dígito um e um “d”) é um literal de timespan que significa um dia.</span><span class="sxs-lookup"><span data-stu-id="b2d58-167">`1d` (that's a digit one, then a 'd') is a timespan literal meaning one day.</span></span> <span data-ttu-id="b2d58-168">Aqui estão mais alguns literais de timespan: `12h`, `30m`, `10s` e `0.01s`.</span><span class="sxs-lookup"><span data-stu-id="b2d58-168">Here are some more timespan literals: `12h`, `30m`, `10s`, `0.01s`.</span></span>
* <span data-ttu-id="b2d58-169">`floor`(alias `bin`) Arredonda um valor para baixo toohello múltiplo mais próximo de valor de base Olá você fornecer.</span><span class="sxs-lookup"><span data-stu-id="b2d58-169">`floor` (alias `bin`) rounds a value down toohello nearest multiple of hello base value you provide.</span></span> <span data-ttu-id="b2d58-170">Portanto `floor(aTime, 1s)` Arredonda vez toohello mais próximo segundo.</span><span class="sxs-lookup"><span data-stu-id="b2d58-170">So `floor(aTime, 1s)` rounds a time down toohello nearest second.</span></span>

<span data-ttu-id="b2d58-171">Expressões podem incluir todos os operadores de saudação normal (`+`, `-`,...), e há uma variedade de funções úteis.</span><span class="sxs-lookup"><span data-stu-id="b2d58-171">Expressions can include all hello usual operators (`+`, `-`, ...), and there's a range of useful functions.</span></span>

## <a name="extend"></a><span data-ttu-id="b2d58-172">Extend</span><span class="sxs-lookup"><span data-stu-id="b2d58-172">Extend</span></span>
<span data-ttu-id="b2d58-173">Se você quiser apenas tooadd toohello de colunas existentes, use [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span><span class="sxs-lookup"><span data-stu-id="b2d58-173">If you just want tooadd columns toohello existing ones, use [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

<span data-ttu-id="b2d58-174">Usando [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) é menos detalhada que [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) se você quiser tookeep todos Olá colunas existentes.</span><span class="sxs-lookup"><span data-stu-id="b2d58-174">Using [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) is less verbose than [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) if you want tookeep all hello existing columns.</span></span>

### <a name="convert-toolocal-time"></a><span data-ttu-id="b2d58-175">Converter o horário de toolocal</span><span class="sxs-lookup"><span data-stu-id="b2d58-175">Convert toolocal time</span></span>

<span data-ttu-id="b2d58-176">Os carimbos de data e hora são sempre em UTC.</span><span class="sxs-lookup"><span data-stu-id="b2d58-176">Timestamps are always in UTC.</span></span> <span data-ttu-id="b2d58-177">Então se você estiver em Costa do Pacífico nos hello e é inverno, talvez você goste isso:</span><span class="sxs-lookup"><span data-stu-id="b2d58-177">So if you're on hello US Pacific coast and it's winter, you might like this:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a><span data-ttu-id="b2d58-178">[Resumir](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): agregar grupos de linhas</span><span class="sxs-lookup"><span data-stu-id="b2d58-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): aggregate groups of rows</span></span>
<span data-ttu-id="b2d58-179">`Summarize` aplica uma *função de agregação* especificada em grupos de linhas.</span><span class="sxs-lookup"><span data-stu-id="b2d58-179">`Summarize` applies a specified *aggregation function* over groups of rows.</span></span>

<span data-ttu-id="b2d58-180">Por exemplo, tempo de saudação toorespond tooa solicitação entra em seu aplicativo web é informado no campo de saudação `duration`.</span><span class="sxs-lookup"><span data-stu-id="b2d58-180">For example, hello time your web app takes toorespond tooa request is reported in hello field `duration`.</span></span> <span data-ttu-id="b2d58-181">Vamos ver médio de resposta Olá tooall solicitações de tempo:</span><span class="sxs-lookup"><span data-stu-id="b2d58-181">Let's see hello average response time tooall requests:</span></span>

![](./media/app-insights-analytics-tour/410.png)

<span data-ttu-id="b2d58-182">Ou podemos pode separar resultado Olá em solicitações de nomes diferentes:</span><span class="sxs-lookup"><span data-stu-id="b2d58-182">Or we could separate hello result into requests of different names:</span></span>

![](./media/app-insights-analytics-tour/420.png)

<span data-ttu-id="b2d58-183">`Summarize`coleta Olá pontos de dados no fluxo de saudação em grupos para os quais Olá `by` cláusula avalia igualmente.</span><span class="sxs-lookup"><span data-stu-id="b2d58-183">`Summarize` collects hello data points in hello stream into groups for which hello `by` clause evaluates equally.</span></span> <span data-ttu-id="b2d58-184">Cada valor na Olá `by` expressão - cada nome de operação em Olá acima exemplo - resulta em uma linha na tabela de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2d58-184">Each value in hello `by` expression - each operation name in hello above example - results in a row in hello result table.</span></span>

<span data-ttu-id="b2d58-185">Ou podemos agrupar os resultados por hora do dia:</span><span class="sxs-lookup"><span data-stu-id="b2d58-185">Or we could group results by time of day:</span></span>

![](./media/app-insights-analytics-tour/430.png)

<span data-ttu-id="b2d58-186">Observe como estamos usando Olá `bin` função (também conhecido como `floor`).</span><span class="sxs-lookup"><span data-stu-id="b2d58-186">Notice how we're using hello `bin` function (aka `floor`).</span></span> <span data-ttu-id="b2d58-187">Se usássemos apenas `by timestamp`, cada linha de entrada acabaria em seu próprio pequeno grupo.</span><span class="sxs-lookup"><span data-stu-id="b2d58-187">If we just used `by timestamp`, every input row would end up in its own little group.</span></span> <span data-ttu-id="b2d58-188">Para qualquer escalar contínua vezes like ou números, temos toobreak Olá série em um número gerenciável de valores discretos.</span><span class="sxs-lookup"><span data-stu-id="b2d58-188">For any continuous scalar like times or numbers, we have toobreak hello continuous range into a manageable number of discrete values.</span></span> <span data-ttu-id="b2d58-189">`bin`-que é apenas Olá familiar arredondamento para baixo `floor` função - é Olá toodo de maneira mais fácil que.</span><span class="sxs-lookup"><span data-stu-id="b2d58-189">`bin` - which is just hello familiar rounding-down `floor` function - is hello easiest way toodo that.</span></span>

<span data-ttu-id="b2d58-190">Podemos usar Olá mesmos intervalos de tooreduce técnica de cadeias de caracteres:</span><span class="sxs-lookup"><span data-stu-id="b2d58-190">We can use hello same technique tooreduce ranges of strings:</span></span>

![](./media/app-insights-analytics-tour/440.png)

<span data-ttu-id="b2d58-191">Observe que você pode usar `name=` tooset nome de saudação de uma coluna de resultados, em expressões de agregação de saudação ou Olá por cláusula.</span><span class="sxs-lookup"><span data-stu-id="b2d58-191">Notice that you can use `name=` tooset hello name of a result column, either in hello aggregation expressions or hello by-clause.</span></span>

## <a name="counting-sampled-data"></a><span data-ttu-id="b2d58-192">Contando dados de amostra</span><span class="sxs-lookup"><span data-stu-id="b2d58-192">Counting sampled data</span></span>
<span data-ttu-id="b2d58-193">`sum(itemCount)`é Olá recomendada agregação toocount eventos.</span><span class="sxs-lookup"><span data-stu-id="b2d58-193">`sum(itemCount)` is hello recommended aggregation toocount events.</span></span> <span data-ttu-id="b2d58-194">Em muitos casos, itemCount = = 1, para a função hello simplesmente conta número Olá de linhas no grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2d58-194">In many cases, itemCount==1, so hello function simply counts up hello number of rows in hello group.</span></span> <span data-ttu-id="b2d58-195">Mas quando [amostragem](app-insights-sampling.md) está em operação, apenas uma fração de eventos original Olá são mantidas como pontos de dados no Application Insights para que para cada ponto de dados que você vê, existem `itemCount` eventos.</span><span class="sxs-lookup"><span data-stu-id="b2d58-195">But when [sampling](app-insights-sampling.md) is in operation, only a fraction of hello original events are retained as data points in Application Insights, so that for each data point you see, there are `itemCount` events.</span></span>

<span data-ttu-id="b2d58-196">Por exemplo, se a amostragem descarta 75% de eventos original hello, itemCount = = 4 em registros de saudação retido - ou seja, para cada registro retido, havia quatro registros originais.</span><span class="sxs-lookup"><span data-stu-id="b2d58-196">For example, if sampling discards 75% of hello original events, then itemCount==4 in hello retained records - that is, for every retained record, there were four original records.</span></span>

<span data-ttu-id="b2d58-197">Amostragem adaptável faz com que itemCount toobe mais alta durante os períodos em que seu aplicativo está sendo usado intensamente.</span><span class="sxs-lookup"><span data-stu-id="b2d58-197">Adaptive sampling causes itemCount toobe higher during periods when your application is being heavily used.</span></span>

<span data-ttu-id="b2d58-198">Resumindo itemCount, portanto, fornece uma boa estimativa do número original de saudação de eventos.</span><span class="sxs-lookup"><span data-stu-id="b2d58-198">Summing up itemCount therefore gives a good estimate of hello original number of events.</span></span>

![](./media/app-insights-analytics-tour/510.png)

<span data-ttu-id="b2d58-199">Também há um `count()` agregação (e uma operação de contagem), para casos onde você realmente deseja toocount Olá número de linhas em um grupo.</span><span class="sxs-lookup"><span data-stu-id="b2d58-199">There's also a `count()` aggregation (and a count operation), for cases where you really do want toocount hello number of rows in a group.</span></span>

<span data-ttu-id="b2d58-200">Há uma série de [funções de agregação](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span><span class="sxs-lookup"><span data-stu-id="b2d58-200">There's a range of [aggregation functions](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>

## <a name="charting-hello-results"></a><span data-ttu-id="b2d58-201">Gráficos de resultados de saudação</span><span class="sxs-lookup"><span data-stu-id="b2d58-201">Charting hello results</span></span>
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

<span data-ttu-id="b2d58-202">Por padrão, os resultados são exibidos como uma tabela:</span><span class="sxs-lookup"><span data-stu-id="b2d58-202">By default, results display as a table:</span></span>

![](./media/app-insights-analytics-tour/225.png)

<span data-ttu-id="b2d58-203">Podemos fazer melhor do que o modo de exibição de tabela hello.</span><span class="sxs-lookup"><span data-stu-id="b2d58-203">We can do better than hello table view.</span></span> <span data-ttu-id="b2d58-204">Vamos analisar resultados Olá no modo de exibição de gráfico de saudação com opção de barra vertical hello:</span><span class="sxs-lookup"><span data-stu-id="b2d58-204">Let's look at hello results in hello chart view with hello vertical bar option:</span></span>

![Clique em Gráfico, escolha o gráfico de barras Vertical e atribua os eixos x e y](./media/app-insights-analytics-tour/230.png)

<span data-ttu-id="b2d58-206">Observe que embora nós não classificar resultados de Olá por hora (como você pode ver na exibição da tabela Olá), exibição de gráfico de saudação sempre mostra datetimes na ordem correta.</span><span class="sxs-lookup"><span data-stu-id="b2d58-206">Notice that although we didn't sort hello results by time (as you can see in hello table display), hello chart display always shows datetimes in correct order.</span></span>


## <a name="timecharts"></a><span data-ttu-id="b2d58-207">Timecharts</span><span class="sxs-lookup"><span data-stu-id="b2d58-207">Timecharts</span></span>
<span data-ttu-id="b2d58-208">Mostra quantos eventos há a cada hora:</span><span class="sxs-lookup"><span data-stu-id="b2d58-208">Show how many events there are each hour:</span></span>

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

<span data-ttu-id="b2d58-209">Selecione a opção de exibição de gráfico de saudação:</span><span class="sxs-lookup"><span data-stu-id="b2d58-209">Select hello Chart display option:</span></span>

![timechart](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a><span data-ttu-id="b2d58-211">Várias séries</span><span class="sxs-lookup"><span data-stu-id="b2d58-211">Multiple series</span></span>
<span data-ttu-id="b2d58-212">Várias expressões em Olá `summarize` cláusula cria várias colunas.</span><span class="sxs-lookup"><span data-stu-id="b2d58-212">Multiple expressions in hello `summarize` clause creates multiple columns.</span></span>

<span data-ttu-id="b2d58-213">Várias expressões em Olá `by` cláusula cria várias linhas, uma para cada combinação de valores.</span><span class="sxs-lookup"><span data-stu-id="b2d58-213">Multiple expressions in hello `by` clause creates multiple rows, one for each combination of values.</span></span>

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Tabela de solicitações por hora e local](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a><span data-ttu-id="b2d58-215">Segmentar um gráfico por dimensões</span><span class="sxs-lookup"><span data-stu-id="b2d58-215">Segment a chart by dimensions</span></span>
<span data-ttu-id="b2d58-216">Se gráfico uma tabela que tenha uma coluna de cadeia de caracteres e uma coluna numérica, a cadeia de caracteres hello puder ser dados numéricos do hello toosplit usadas em séries distintas de pontos.</span><span class="sxs-lookup"><span data-stu-id="b2d58-216">If you chart a table that has a string column and a numeric column, hello string can be used toosplit hello numeric data into separate series of points.</span></span> <span data-ttu-id="b2d58-217">Se houver mais de uma coluna de cadeia de caracteres, você pode escolher qual coluna toouse como discriminador de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2d58-217">If there's more than one string column, you can choose which column toouse as hello discriminator.</span></span>

![Segmentar um gráfico de análise](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a><span data-ttu-id="b2d58-219">Taxa de devolução</span><span class="sxs-lookup"><span data-stu-id="b2d58-219">Bounce rate</span></span>

<span data-ttu-id="b2d58-220">Converter um toouse de cadeia de caracteres booliana tooa-lo como um discriminador:</span><span class="sxs-lookup"><span data-stu-id="b2d58-220">Convert a boolean tooa string toouse it as a discriminator:</span></span>

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

### <a name="display-multiple-metrics"></a><span data-ttu-id="b2d58-221">Exibir várias métricas</span><span class="sxs-lookup"><span data-stu-id="b2d58-221">Display multiple metrics</span></span>
<span data-ttu-id="b2d58-222">Se o gráfico de uma tabela que tem mais de uma coluna numérica, em adição toohello timestamp, você pode exibir qualquer combinação desses itens.</span><span class="sxs-lookup"><span data-stu-id="b2d58-222">If you chart a table that has more than one numeric column, in addition toohello timestamp, you can display any combination of them.</span></span>

![Segmentar um gráfico de análise](./media/app-insights-analytics-tour/110.png)

<span data-ttu-id="b2d58-224">Você deve selecionar **Não Dividir** antes de selecionar várias colunas numéricas.</span><span class="sxs-lookup"><span data-stu-id="b2d58-224">You must select **Don't Split** before you can select multiple numeric columns.</span></span> <span data-ttu-id="b2d58-225">Não é possível dividir, uma coluna de cadeia de caracteres no hello mesmo tempo como exibir mais de uma coluna numérica.</span><span class="sxs-lookup"><span data-stu-id="b2d58-225">You can't split by a string column at hello same time as displaying more than one numeric column.</span></span>

## <a name="daily-average-cycle"></a><span data-ttu-id="b2d58-226">Ciclo médio diário</span><span class="sxs-lookup"><span data-stu-id="b2d58-226">Daily average cycle</span></span>
<span data-ttu-id="b2d58-227">Como o uso variar ao longo do dia médio Olá?</span><span class="sxs-lookup"><span data-stu-id="b2d58-227">How does usage vary over hello average day?</span></span>

<span data-ttu-id="b2d58-228">Solicitações de contagem por tempo de saudação módulo um dia, guardadas em horas:</span><span class="sxs-lookup"><span data-stu-id="b2d58-228">Count requests by hello time modulo one day, binned into hours:</span></span>

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
> <span data-ttu-id="b2d58-230">Observe que no momento temos tooconvert toodatetimes de durações de tempo em ordem toodisplay em um gráfico de linha.</span><span class="sxs-lookup"><span data-stu-id="b2d58-230">Notice that we currently have tooconvert time durations toodatetimes in order toodisplay on a line chart.</span></span>
>
>

## <a name="compare-multiple-daily-series"></a><span data-ttu-id="b2d58-231">Comparar várias séries diárias</span><span class="sxs-lookup"><span data-stu-id="b2d58-231">Compare multiple daily series</span></span>
<span data-ttu-id="b2d58-232">Como o uso variar ao longo do tempo de saudação do dia em países diferentes?</span><span class="sxs-lookup"><span data-stu-id="b2d58-232">How does usage vary over hello time of day in different countries?</span></span>

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

## <a name="plot-a-distribution"></a><span data-ttu-id="b2d58-234">Plotar uma distribuição</span><span class="sxs-lookup"><span data-stu-id="b2d58-234">Plot a distribution</span></span>
<span data-ttu-id="b2d58-235">Quantas sessões existem de comprimentos diferentes?</span><span class="sxs-lookup"><span data-stu-id="b2d58-235">How many sessions are there of different lengths?</span></span>

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

<span data-ttu-id="b2d58-236">última linha de saudação é necessário tooconvert toodatetime.</span><span class="sxs-lookup"><span data-stu-id="b2d58-236">hello last line is required tooconvert toodatetime.</span></span> <span data-ttu-id="b2d58-237">No momento eixo Olá x de um gráfico é exibido como um valor escalar somente se ele for uma data e hora.</span><span class="sxs-lookup"><span data-stu-id="b2d58-237">Currently hello x axis of a chart is displayed as a scalar only if it is a datetime.</span></span>

<span data-ttu-id="b2d58-238">Olá `where` cláusula exclui sessões única (sessionDuration = = 0) e conjuntos de Olá comprimento do eixo x da saudação.</span><span class="sxs-lookup"><span data-stu-id="b2d58-238">hello `where` clause excludes one-shot sessions (sessionDuration==0) and sets hello length of hello x-axis.</span></span>

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[<span data-ttu-id="b2d58-239">Percentis</span><span class="sxs-lookup"><span data-stu-id="b2d58-239">Percentiles</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
<span data-ttu-id="b2d58-240">Quais intervalos de durações abordam diferentes porcentagens de sessões?</span><span class="sxs-lookup"><span data-stu-id="b2d58-240">What ranges of durations cover different percentages of sessions?</span></span>

<span data-ttu-id="b2d58-241">Usar Olá acima de consulta, mas substitua a última linha de saudação:</span><span class="sxs-lookup"><span data-stu-id="b2d58-241">Use hello above query, but replace hello last line:</span></span>

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

<span data-ttu-id="b2d58-242">Também é removida limite superior Olá Olá onde cláusula, na ordem tooget corrigir ilustrações, incluindo todas as sessões com mais de uma solicitação:</span><span class="sxs-lookup"><span data-stu-id="b2d58-242">We also removed hello upper limit in hello where clause, in order tooget correct figures including all sessions with more than one request:</span></span>

![result](./media/app-insights-analytics-tour/180.png)

<span data-ttu-id="b2d58-244">O que nos mostra que:</span><span class="sxs-lookup"><span data-stu-id="b2d58-244">From which we can see that:</span></span>

* <span data-ttu-id="b2d58-245">5% das sessões têm uma duração de menos de 3 minutos e 34 segundos;</span><span class="sxs-lookup"><span data-stu-id="b2d58-245">5% of sessions have a duration of less than 3 minutes 34s;</span></span>
* <span data-ttu-id="b2d58-246">50% das sessões duram menos de 36 minutos;</span><span class="sxs-lookup"><span data-stu-id="b2d58-246">50% of sessions last less than 36 minutes;</span></span>
* <span data-ttu-id="b2d58-247">5% das sessões duram mais de 7 dias</span><span class="sxs-lookup"><span data-stu-id="b2d58-247">5% of sessions last more than 7 days</span></span>

<span data-ttu-id="b2d58-248">tooget uma análise separada para cada país, apenas temos toobring Olá client_CountryOrRegion coluna separadamente através de ambos resumir operadores:</span><span class="sxs-lookup"><span data-stu-id="b2d58-248">tooget a separate breakdown for each country, we just have toobring hello client_CountryOrRegion column separately through both summarize operators:</span></span>

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

## <a name="join"></a><span data-ttu-id="b2d58-249">Ingressar</span><span class="sxs-lookup"><span data-stu-id="b2d58-249">Join</span></span>
<span data-ttu-id="b2d58-250">Temos acesso tooseveral tabelas, incluindo solicitações e exceções.</span><span class="sxs-lookup"><span data-stu-id="b2d58-250">We have access tooseveral tables, including requests and exceptions.</span></span>

<span data-ttu-id="b2d58-251">toofind Olá exceções relacionadas tooa solicitação retornou uma resposta de falha, pode unir tabelas de saudação em `session_Id`:</span><span class="sxs-lookup"><span data-stu-id="b2d58-251">toofind hello exceptions related tooa request that returned a failure response, we can join hello tables on `session_Id`:</span></span>

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


<span data-ttu-id="b2d58-252">É uma boa prática toouse `project` tooselect colunas de saudação apenas precisamos antes de executar Olá junção.</span><span class="sxs-lookup"><span data-stu-id="b2d58-252">It's good practice toouse `project` tooselect just hello columns we need before performing hello join.</span></span>
<span data-ttu-id="b2d58-253">Em Olá mesmas cláusulas, podemos renomear a coluna de carimbo de hora de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2d58-253">In hello same clauses, we rename hello timestamp column.</span></span>

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-tooa-variable"></a><span data-ttu-id="b2d58-254">[Permitir que](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): atribuir uma variável de tooa de resultado</span><span class="sxs-lookup"><span data-stu-id="b2d58-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): Assign a result tooa variable</span></span>

<span data-ttu-id="b2d58-255">Use `let` tooseparate partes de saudação da expressão anterior hello.</span><span class="sxs-lookup"><span data-stu-id="b2d58-255">Use `let` tooseparate out hello parts of hello previous expression.</span></span> <span data-ttu-id="b2d58-256">resultados de saudação não foram modificados:</span><span class="sxs-lookup"><span data-stu-id="b2d58-256">hello results are unchanged:</span></span>

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> <span data-ttu-id="b2d58-257">No cliente de análise hello, não coloque as linhas em branco entre as partes de saudação de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2d58-257">In hello Analytics client, don't put blank lines between hello parts of hello query.</span></span> <span data-ttu-id="b2d58-258">Verifique tooexecute-se de que todos eles.</span><span class="sxs-lookup"><span data-stu-id="b2d58-258">Make sure tooexecute all of it.</span></span>
>

<span data-ttu-id="b2d58-259">Use `toscalar` tooconvert um valor de tooa de célula de tabela única:</span><span class="sxs-lookup"><span data-stu-id="b2d58-259">Use `toscalar` tooconvert a single table cell tooa value:</span></span>

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


### <a name="functions"></a><span data-ttu-id="b2d58-260">Funções</span><span class="sxs-lookup"><span data-stu-id="b2d58-260">Functions</span></span>

<span data-ttu-id="b2d58-261">Use *permitem* toodefine uma função:</span><span class="sxs-lookup"><span data-stu-id="b2d58-261">Use *Let* toodefine a function:</span></span>

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a><span data-ttu-id="b2d58-262">Acessando objetos aninhados</span><span class="sxs-lookup"><span data-stu-id="b2d58-262">Accessing nested objects</span></span>
<span data-ttu-id="b2d58-263">Os objetos aninhados podem ser acessados facilmente.</span><span class="sxs-lookup"><span data-stu-id="b2d58-263">Nested objects can be accessed easily.</span></span> <span data-ttu-id="b2d58-264">Por exemplo, no fluxo de exceções hello, você pode ver objetos estruturados como este:</span><span class="sxs-lookup"><span data-stu-id="b2d58-264">For example, in hello exceptions stream you can see structured objects like this:</span></span>

![result](./media/app-insights-analytics-tour/520.png)

<span data-ttu-id="b2d58-266">Você pode mesclá-la escolhendo Propriedades Olá em que você estiver interessado:</span><span class="sxs-lookup"><span data-stu-id="b2d58-266">You can flatten it by choosing hello properties you're interested in:</span></span>

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="b2d58-267">Observe que você precisa que o tipo apropriado do toohello toocast Olá resultado.</span><span class="sxs-lookup"><span data-stu-id="b2d58-267">Note that you need toocast hello result toohello appropriate type.</span></span>


## <a name="custom-properties-and-measurements"></a><span data-ttu-id="b2d58-268">Medidas e propriedades personalizadas</span><span class="sxs-lookup"><span data-stu-id="b2d58-268">Custom properties and measurements</span></span>
<span data-ttu-id="b2d58-269">Se seu aplicativo anexa [dimensões personalizadas (Propriedades) e medidas personalizadas](app-insights-api-custom-events-metrics.md#properties) tooevents, em seguida, você vai vê-los no hello `customDimensions` e `customMeasurements` objetos.</span><span class="sxs-lookup"><span data-stu-id="b2d58-269">If your application attaches [custom dimensions (properties) and custom measurements](app-insights-api-custom-events-metrics.md#properties) tooevents, then you will see them in hello `customDimensions` and `customMeasurements` objects.</span></span>

<span data-ttu-id="b2d58-270">Por exemplo, se o seu aplicativo inclui:</span><span class="sxs-lookup"><span data-stu-id="b2d58-270">For example, if your app includes:</span></span>

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

<span data-ttu-id="b2d58-271">tooextract esses valores na análise:</span><span class="sxs-lookup"><span data-stu-id="b2d58-271">tooextract these values in Analytics:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast tooexpected type

```

<span data-ttu-id="b2d58-272">tooverify se uma dimensão personalizada é de um tipo específico:</span><span class="sxs-lookup"><span data-stu-id="b2d58-272">tooverify whether a custom dimension is of a particular type:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a><span data-ttu-id="b2d58-273">Painéis</span><span class="sxs-lookup"><span data-stu-id="b2d58-273">Dashboards</span></span>
<span data-ttu-id="b2d58-274">Você pode fixar o painel resultados em ordem toobring tooa juntos todos os seus gráficos e tabelas mais importantes.</span><span class="sxs-lookup"><span data-stu-id="b2d58-274">You can pin your results tooa dashboard in order toobring together all your most important charts and tables.</span></span>

* <span data-ttu-id="b2d58-275">[Painel compartilhado do Azure](app-insights-dashboards.md#share-dashboards): clique no ícone de pino hello.</span><span class="sxs-lookup"><span data-stu-id="b2d58-275">[Azure shared dashboard](app-insights-dashboards.md#share-dashboards): Click hello pin icon.</span></span> <span data-ttu-id="b2d58-276">Antes de fazer isso, você deve ter um painel compartilhado.</span><span class="sxs-lookup"><span data-stu-id="b2d58-276">Before you do this, you must have a shared dashboard.</span></span> <span data-ttu-id="b2d58-277">No portal do Azure de Olá, abrir ou criar um painel e clicar em compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="b2d58-277">In hello Azure portal, open or create a dashboard and click Share.</span></span>
* <span data-ttu-id="b2d58-278">[Painel do Power BI](app-insights-export-power-bi.md): clique em Exportar, Consulta do Power BI.</span><span class="sxs-lookup"><span data-stu-id="b2d58-278">[Power BI dashboard](app-insights-export-power-bi.md): Click Export, Power BI Query.</span></span> <span data-ttu-id="b2d58-279">Uma vantagem dessa alternativa é que você pode exibir sua consulta juntamente com outros resultados de uma ampla variedade de fontes.</span><span class="sxs-lookup"><span data-stu-id="b2d58-279">An advantage of this alternative is that you can display your query alongside other results from a wide range of sources.</span></span>

## <a name="combine-with-imported-data"></a><span data-ttu-id="b2d58-280">Combinar com dados importados</span><span class="sxs-lookup"><span data-stu-id="b2d58-280">Combine with imported data</span></span>

<span data-ttu-id="b2d58-281">Relatórios de análise uma aparência excelentes no painel hello, mas, às vezes, você deseja tootranslate Olá dados tooa mais de forma fácil de entender.</span><span class="sxs-lookup"><span data-stu-id="b2d58-281">Analytics reports look great on hello dashboard, but sometimes you want tootranslate hello data tooa more digestible form.</span></span> <span data-ttu-id="b2d58-282">Por exemplo, suponha que os usuários autenticados são identificados na telemetria Olá por um alias.</span><span class="sxs-lookup"><span data-stu-id="b2d58-282">For example, suppose your authenticated users are identified in hello telemetry by an alias.</span></span> <span data-ttu-id="b2d58-283">Você gostaria que tooshow seu real nomes em seus resultados.</span><span class="sxs-lookup"><span data-stu-id="b2d58-283">You'd like tooshow their real names in your results.</span></span> <span data-ttu-id="b2d58-284">toodo isso, é necessário um arquivo CSV que mapeia de nomes reais da saudação aliases toohello.</span><span class="sxs-lookup"><span data-stu-id="b2d58-284">toodo this, you need a CSV file that maps from hello aliases toohello real names.</span></span>

<span data-ttu-id="b2d58-285">Você pode importar um arquivo de dados e usá-lo como qualquer uma das tabelas de saudação padrão (solicitações, exceções e assim por diante).</span><span class="sxs-lookup"><span data-stu-id="b2d58-285">You can import a data file and use it just like any of hello standard tables (requests, exceptions, and so on).</span></span> <span data-ttu-id="b2d58-286">É possível consultá-la sozinha ou uni-la a outras tabelas.</span><span class="sxs-lookup"><span data-stu-id="b2d58-286">Either query it on its own, or join it with other tables.</span></span> <span data-ttu-id="b2d58-287">Por exemplo, se você tiver uma tabela chamada usermap e ele tem colunas `realName` e `userId`, e em seguida, você pode usá-lo Olá tootranslate `user_AuthenticatedId` campo telemetria de solicitação hello:</span><span class="sxs-lookup"><span data-stu-id="b2d58-287">For example, if you have a table named usermap, and it has columns `realName` and `userId`, then you can use it tootranslate hello `user_AuthenticatedId` field in hello request telemetry:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get hello realName field from hello usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

<span data-ttu-id="b2d58-288">tooimport uma tabela, na folha de esquema hello, em **outras fontes de dados**, siga Olá instruções tooadd uma nova fonte de dados, carregando um exemplo dos dados.</span><span class="sxs-lookup"><span data-stu-id="b2d58-288">tooimport a table, in hello Schema blade, under **Other Data Sources**, follow hello instructions tooadd a new data source, by uploading a sample of your data.</span></span> <span data-ttu-id="b2d58-289">Em seguida, você pode usar tabelas de tooupload essa definição.</span><span class="sxs-lookup"><span data-stu-id="b2d58-289">Then you can use this definition tooupload tables.</span></span>

<span data-ttu-id="b2d58-290">o recurso de importação Hello está atualmente em visualização, portanto, inicialmente, você verá um link "Entre em contato conosco" em "Outras fontes de dados."</span><span class="sxs-lookup"><span data-stu-id="b2d58-290">hello import feature is currently in preview, so you will initially see a "Contact us" link under "Other data sources."</span></span> <span data-ttu-id="b2d58-291">Use este toosign toohello programa de visualização e link hello será substituído por um botão "Adicionar nova fonte de dados".</span><span class="sxs-lookup"><span data-stu-id="b2d58-291">Use this toosign up toohello preview program, and hello link will then be replaced by an "Add new data source" button.</span></span>


## <a name="tables"></a><span data-ttu-id="b2d58-292">Tabelas</span><span class="sxs-lookup"><span data-stu-id="b2d58-292">Tables</span></span>
<span data-ttu-id="b2d58-293">saudação de telemetria recebida do seu aplicativo está acessível por meio de várias tabelas.</span><span class="sxs-lookup"><span data-stu-id="b2d58-293">hello stream of telemetry received from your app is accessible through several tables.</span></span> <span data-ttu-id="b2d58-294">esquema de saudação de propriedades disponíveis para cada tabela é visível à esquerda de saudação da janela de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2d58-294">hello schema of properties available for each table is visible at hello left of hello window.</span></span>

### <a name="requests-table"></a><span data-ttu-id="b2d58-295">Tabela de solicitações</span><span class="sxs-lookup"><span data-stu-id="b2d58-295">Requests table</span></span>
<span data-ttu-id="b2d58-296">Tooyour web app e o segmento de solicitações HTTP de contagem por nome de página:</span><span class="sxs-lookup"><span data-stu-id="b2d58-296">Count HTTP requests tooyour web app and segment by page name:</span></span>

![Conte solicitações segmentadas por nome](./media/app-insights-analytics-tour/analytics-count-requests.png)

<span data-ttu-id="b2d58-298">Localiza as solicitações de saudação que falham mais:</span><span class="sxs-lookup"><span data-stu-id="b2d58-298">Find hello requests that fail most:</span></span>

![Conte solicitações segmentadas por nome](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a><span data-ttu-id="b2d58-300">Tabela de eventos personalizada</span><span class="sxs-lookup"><span data-stu-id="b2d58-300">Custom events table</span></span>
<span data-ttu-id="b2d58-301">Se você usar [Trackevent](app-insights-api-custom-events-metrics.md#trackevent) toosend seus próprios eventos, você pode lê-los desta tabela.</span><span class="sxs-lookup"><span data-stu-id="b2d58-301">If you use [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend your own events, you can read them from this table.</span></span>

<span data-ttu-id="b2d58-302">Vejamos um exemplo em que o código do aplicativo contém estas linhas:</span><span class="sxs-lookup"><span data-stu-id="b2d58-302">Let's take an example where your app code contains these lines:</span></span>

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

<span data-ttu-id="b2d58-303">Frequência de saudação desses eventos de exibição:</span><span class="sxs-lookup"><span data-stu-id="b2d58-303">Display hello frequency of these events:</span></span>

![Taxa de exibição de eventos personalizados](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

<span data-ttu-id="b2d58-305">Extrai eventos Olá medidas e dimensões:</span><span class="sxs-lookup"><span data-stu-id="b2d58-305">Extract measurements and dimensions from hello events:</span></span>

![Taxa de exibição de eventos personalizados](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a><span data-ttu-id="b2d58-307">Tabela de métricas personalizada</span><span class="sxs-lookup"><span data-stu-id="b2d58-307">Custom metrics table</span></span>
<span data-ttu-id="b2d58-308">Se você estiver usando [Trackmetric](app-insights-api-custom-events-metrics.md#trackmetric) toosend seus próprios valores da métrica, você encontrará seus resultados no hello **customMetrics** fluxo.</span><span class="sxs-lookup"><span data-stu-id="b2d58-308">If you are using [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend your own metric values, you’ll find its results in hello **customMetrics** stream.</span></span> <span data-ttu-id="b2d58-309">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b2d58-309">For example:</span></span>  

![Métricas personalizadas na análise do Application Insights](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> <span data-ttu-id="b2d58-311">Em [Metrics Explorer](app-insights-metrics-explorer.md), todas as medidas personalizadas anexado tooany tipo de telemetria aparecem juntas na folha de métricas de saudação juntamente com métricas enviadas usando `TrackMetric()`.</span><span class="sxs-lookup"><span data-stu-id="b2d58-311">In [Metrics Explorer](app-insights-metrics-explorer.md), all custom measurements attached tooany type of telemetry appear together in hello metrics blade along with metrics sent using `TrackMetric()`.</span></span> <span data-ttu-id="b2d58-312">Mas na análise, medidas personalizadas ainda estão anexados toowhichever tipo de telemetria que foram executadas nos eventos ou solicitações e assim por diante - enquanto métricas enviadas pelo TrackMetric aparecem em seu próprio fluxo.</span><span class="sxs-lookup"><span data-stu-id="b2d58-312">But in Analytics, custom measurements are still attached toowhichever type of telemetry they were carried on - events or requests, and so on - while metrics sent by TrackMetric appear in their own stream.</span></span>
>
>

### <a name="performance-counters-table"></a><span data-ttu-id="b2d58-313">Tabela de contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="b2d58-313">Performance counters table</span></span>
<span data-ttu-id="b2d58-314">Os [contadores de desempenho](app-insights-performance-counters.md) mostram métricas básicas do sistema para seu aplicativo, tais como CPU, memória e uso de rede.</span><span class="sxs-lookup"><span data-stu-id="b2d58-314">[Performance counters](app-insights-performance-counters.md) show you basic system metrics for your app, such as CPU, memory, and network utilization.</span></span> <span data-ttu-id="b2d58-315">Você pode configurar Olá SDK toosend contadores adicionais, incluindo seus próprios contadores personalizados.</span><span class="sxs-lookup"><span data-stu-id="b2d58-315">You can configure hello SDK toosend additional counters, including your own custom counters.</span></span>

<span data-ttu-id="b2d58-316">Olá **performanceCounters** esquema expõe Olá `category`, `counter` nome, e `instance` nome de contador de desempenho.</span><span class="sxs-lookup"><span data-stu-id="b2d58-316">hello **performanceCounters** schema exposes hello `category`, `counter` name, and `instance` name of each performance counter.</span></span> <span data-ttu-id="b2d58-317">Nomes de instância do contador são somente os contadores de desempenho toosome aplicável e geralmente indicam o nome de saudação do hello processo toowhich Olá contagem está relacionada.</span><span class="sxs-lookup"><span data-stu-id="b2d58-317">Counter instance names are only applicable toosome performance counters, and typically indicate hello name of hello process toowhich hello count relates.</span></span> <span data-ttu-id="b2d58-318">Telemetria Olá para cada aplicativo, você verá apenas os contadores Olá para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b2d58-318">In hello telemetry for each application, you’ll see only hello counters for that application.</span></span> <span data-ttu-id="b2d58-319">Por exemplo, toosee quais contadores estão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="b2d58-319">For example, toosee what counters are available:</span></span>

![Contadores de desempenho na análise do Application Insights](./media/app-insights-analytics-tour/analytics-performance-counters.png)

<span data-ttu-id="b2d58-321">tooget um gráfico de memória disponível em Olá período selecionado:</span><span class="sxs-lookup"><span data-stu-id="b2d58-321">tooget a chart of available memory over hello selected period:</span></span>

![Gráfico de tempo da memória na análise do Application Insights](./media/app-insights-analytics-tour/analytics-available-memory.png)

<span data-ttu-id="b2d58-323">Como outros telemetria **performanceCounters** também tem uma coluna `cloud_RoleInstance` que indica Olá identidade da máquina de host de saudação em que seu aplicativo é executado.</span><span class="sxs-lookup"><span data-stu-id="b2d58-323">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates hello identity of hello host machine on which your app is running.</span></span> <span data-ttu-id="b2d58-324">Por exemplo, toocompare Olá desempenho do aplicativo em máquinas diferentes hello:</span><span class="sxs-lookup"><span data-stu-id="b2d58-324">For example, toocompare hello performance of your app on hello different machines:</span></span>

![Desempenho segmentado por instância de função na análise do Application Insights](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a><span data-ttu-id="b2d58-326">Tabela de exceções</span><span class="sxs-lookup"><span data-stu-id="b2d58-326">Exceptions table</span></span>
<span data-ttu-id="b2d58-327">As [exceções relatadas pelo seu aplicativo](app-insights-asp-net-exceptions.md) estão disponíveis nessa tabela.</span><span class="sxs-lookup"><span data-stu-id="b2d58-327">[Exceptions reported by your app](app-insights-asp-net-exceptions.md) are available in this table.</span></span>

<span data-ttu-id="b2d58-328">toofind Olá solicitação HTTP que seu aplicativo estava manipulando quando Olá exceção foi gerada, ingressar em operation_Id:</span><span class="sxs-lookup"><span data-stu-id="b2d58-328">toofind hello HTTP request that your app was handling when hello exception was raised, join on operation_Id:</span></span>

![Ingressar em exceções com solicitações em operation_Id](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a><span data-ttu-id="b2d58-330">Tabela de intervalos do navegador</span><span class="sxs-lookup"><span data-stu-id="b2d58-330">Browser timings table</span></span>
<span data-ttu-id="b2d58-331">`browserTimings` mostra os dados de carregamento de página coletados nos navegadores de seus usuários.</span><span class="sxs-lookup"><span data-stu-id="b2d58-331">`browserTimings` shows page load data collected in your users' browsers.</span></span>

<span data-ttu-id="b2d58-332">[Configurar seu aplicativo de telemetria do lado do cliente](app-insights-javascript.md) em ordem toosee essas métricas.</span><span class="sxs-lookup"><span data-stu-id="b2d58-332">[Set up your app for client-side telemetry](app-insights-javascript.md) in order toosee these metrics.</span></span>

<span data-ttu-id="b2d58-333">esquema de saudação inclui [métricas indicando comprimentos de saudação das diferentes fases do processo de carregamento de página de saudação](app-insights-javascript.md#page-load-performance).</span><span class="sxs-lookup"><span data-stu-id="b2d58-333">hello schema includes [metrics indicating hello lengths of different stages of hello page loading process](app-insights-javascript.md#page-load-performance).</span></span> <span data-ttu-id="b2d58-334">(Elas não indicam Olá período que os usuários ler uma página).</span><span class="sxs-lookup"><span data-stu-id="b2d58-334">(They don’t indicate hello length of time your users read a page.)</span></span>  

<span data-ttu-id="b2d58-335">Mostrar popularities Olá de diferentes páginas e tempos para cada página de carregamento:</span><span class="sxs-lookup"><span data-stu-id="b2d58-335">Show hello popularities of different pages, and load times for each page:</span></span>

![Tempos de carregamento de página no Analytics](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a><span data-ttu-id="b2d58-337">Tabela de resultados de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="b2d58-337">Availability results table</span></span>
<span data-ttu-id="b2d58-338">`availabilityResults`mostra Olá resultados de sua [testes na web](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="b2d58-338">`availabilityResults` shows hello results of your [web tests](app-insights-monitor-web-app-availability.md).</span></span> <span data-ttu-id="b2d58-339">Cada execução dos testes de cada local de teste é relatada separadamente.</span><span class="sxs-lookup"><span data-stu-id="b2d58-339">Each run of your tests from each test location is reported separately.</span></span>

![Tempos de carregamento de página no Analytics](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a><span data-ttu-id="b2d58-341">Tabela de dependências</span><span class="sxs-lookup"><span data-stu-id="b2d58-341">Dependencies table</span></span>
<span data-ttu-id="b2d58-342">Contém os resultados de chamadas que seu aplicativo torna toodatabases e APIs REST e outros chama tooTrackDependency().</span><span class="sxs-lookup"><span data-stu-id="b2d58-342">Contains results of calls that your app makes toodatabases and REST APIs, and other calls tooTrackDependency().</span></span> <span data-ttu-id="b2d58-343">Também inclui chamadas AJAX feitas do navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2d58-343">Also includes AJAX calls made from hello browser.</span></span>

<span data-ttu-id="b2d58-344">Chamadas AJAX de navegador hello:</span><span class="sxs-lookup"><span data-stu-id="b2d58-344">AJAX calls from hello browser:</span></span>

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

<span data-ttu-id="b2d58-345">Chamadas de dependência do servidor de saudação:</span><span class="sxs-lookup"><span data-stu-id="b2d58-345">Dependency calls from hello server:</span></span>

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

<span data-ttu-id="b2d58-346">Sempre mostram resultados de dependência do lado do servidor `success==False` se hello Application Insights Agent não está instalado.</span><span class="sxs-lookup"><span data-stu-id="b2d58-346">Server-side dependency results always show `success==False` if hello Application Insights Agent is not installed.</span></span> <span data-ttu-id="b2d58-347">No entanto, hello outros dados estão corretos.</span><span class="sxs-lookup"><span data-stu-id="b2d58-347">However, hello other data are correct.</span></span>

### <a name="traces-table"></a><span data-ttu-id="b2d58-348">Tabela de rastreamentos</span><span class="sxs-lookup"><span data-stu-id="b2d58-348">Traces table</span></span>
<span data-ttu-id="b2d58-349">Contém a telemetria de saudação enviada pelo seu aplicativo usando tracktrace (), ou [outras estruturas de registro em log](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="b2d58-349">Contains hello telemetry sent by your app using TrackTrace(), or [other logging frameworks](app-insights-asp-net-trace-logs.md).</span></span>

## <a name="video"></a><span data-ttu-id="b2d58-350">Vídeo</span><span class="sxs-lookup"><span data-stu-id="b2d58-350">Video</span></span> 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

<span data-ttu-id="b2d58-351">Consultas avançadas:</span><span class="sxs-lookup"><span data-stu-id="b2d58-351">Advanced queries:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a><span data-ttu-id="b2d58-352">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b2d58-352">Next steps</span></span>
* [<span data-ttu-id="b2d58-353">Referência de linguagem de análise</span><span class="sxs-lookup"><span data-stu-id="b2d58-353">Analytics language reference</span></span>](app-insights-analytics-reference.md)
* <span data-ttu-id="b2d58-354">[Roteiro de SQL-usuários](https://aka.ms/sql-analytics) converte as linguagens mais comuns de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2d58-354">[SQL-users' cheat sheet](https://aka.ms/sql-analytics) translates hello most common idioms.</span></span>

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
