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
# <a name="a-tour-of-analytics-in-application-insights"></a>Um tour pela Análise no Application Insights
[Análise de](app-insights-analytics.md) é o recurso de pesquisa poderoso saudação do [Application Insights](app-insights-overview.md). Essas páginas descrevem a linguagem de consulta do Log Analytics.

* **[Assistir ao vídeo introdutório Olá](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Faça o test drive análise sobre nossos dados simulados](https://analytics.applicationinsights.io/demo)**  se seu aplicativo não esteja enviando dados tooApplication Insights ainda.
* **[Roteiro de SQL-usuários](https://aka.ms/sql-analytics)**  converte as linguagens mais comuns de saudação.

Vamos dar um passo a passo tooget algumas consultas básicas que você iniciou.

## <a name="connect-tooyour-application-insights-data"></a>Conecte-se a dados do Application Insights tooyour
Abra o Analytics na [folha de visão geral](app-insights-dashboards.md) de seu aplicativo no Application Insights:

![Abra o portal.azure.com, abra o recurso do Application Insights e clique em Análise.](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a>[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): mostre-me n linhas
Os pontos de dados que registram em log operações de usuário (geralmente solicitações HTTP recebidas pelo seu aplicativo Web) são armazenados em uma tabela chamada `requests`. Cada linha é um ponto de dados de telemetria recebido do hello Application Insights SDK em seu aplicativo.

Vamos começar examinando algumas linhas de exemplo de tabela hello:

![results](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> Coloque o cursor de saudação em algum lugar na instrução de saudação antes de clicar em Ir. Você pode dividir uma instrução em mais de uma linha, mas não coloque linhas em branco em uma instrução. Linhas em branco são uma maneira conveniente de tookeep várias separam consultas na janela de saudação.
>
>

Escolha colunas, arraste-as, agrupe por colunas e filtre:

![Clique na seleção de coluna no canto superior direito dos resultados](./media/app-insights-analytics-tour/030.png)

Expanda detalhes item toosee hello:

![Escolha Tabela e use Configurar Colunas](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> Clique em início de saudação de uma coluna ordem toore Olá resulta disponíveis no navegador da web de saudação. Mas, lembre-se de que, para um conjunto de resultados grande, número de saudação do navegador de toohello baixado de linhas é limitado. Classificando dessa maneira não mostra sempre Olá real maior ou menor de itens. itens de toosort confiável, usam Olá `top` ou `sort` operador.
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a>[Superior](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) e [classificação](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)
`take`é um exemplo rápido de um resultado de tooget útil, mas mostra linhas da tabela de saudação em nenhuma ordem específica. tooget uma exibição ordenada, use `top` (para obter um exemplo) ou `sort` (pela tabela inteira de saudação).

Mostre-me primeiras linhas n hello, ordenadas por uma coluna específica:

```AIQL

    requests | top 10 by timestamp desc
```

* *Sintaxe:* a maioria dos operadores têm parâmetros de palavra-chave, como `by`.
* `desc` = ordem decrescente, `asc` = ordem crescente.

![](./media/app-insights-analytics-tour/260.png)

`top...` é uma maneira mais eficaz de dizer `sort ... | take...`. Poderíamos ter escrito:

```AIQL

    requests | sort by timestamp desc | take 10
```

resultado de saudação seria Olá mesmo, mas ele será executado um pouco mais lenta. (Também é possível escrever `order`, que é um alias de `sort`.)

cabeçalhos de coluna Olá no modo de tabela Olá também podem ser usado toosort Olá resultados na tela hello. Mas certamente, se você usou `take` ou `top` tooretrieve apenas parte de uma tabela, você terá apenas reordenar Olá registros recuperar.

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a>[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtragem de uma condição

Vamos ver apenas as solicitações que retornaram um código de resultado específico:

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

Olá `where` operador obtém uma expressão booleana. Eis alguns pontos importantes sobre eles:

* `and`, `or`: Operadores booleanos
* `==`, `<>`, `!=`: igual a e diferente de
* `=~`, `!~`: cadeia de caracteres que não diferencia maiúsculas de minúsculas "igual a" e "diferente de". Há muitos outros operadores de comparação de cadeia de caracteres.

<!---Read all about [scalar expressions]().--->

### <a name="getting-hello-right-type"></a>Obtendo o tipo correto de saudação
Solicitações malsucedidas de localização:

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a>Hora

Por padrão, as consultas são restrito toohello últimas 24 horas. Mas você pode alterar esse intervalo:

![](./media/app-insights-analytics-tour/change-time-range.png)

Substituir o intervalo de tempo de saudação escrevendo qualquer consulta que menciona `timestamp` em uma cláusula where. Por exemplo:

```AIQL

    // What were hello slowest requests over hello past 3 days?
    requests
    | where timestamp > ago(3d)  // Override hello time range
    | top 5 by duration
```

recurso de intervalo de tempo de saudação é equivalente tooa 'where' cláusula inserida após cada uma das tabelas de origem Olá mencionado.

`ago(3d)` significa 'três dias atrás'. Outras unidades de tempo incluem horas (`2h`, `2.5h`), minutos (`25m`) e segundos (`10s`).

Outros exemplos:

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

[Referência de datas e horas](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a>[Projeto](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): selecionar, renomear e computar colunas
Use [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick apenas colunas Olá desejado:

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

Você também pode renomear e definir novas colunas:

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

* Os nomes de coluna poderão incluir espaços ou símbolos se eles estiverem entre colchetes, desta forma: `['...']` ou `["..."]`
* `%`Olá é algo comum do operador de módulo.
* `1d` (que é o dígito um e um “d”) é um literal de timespan que significa um dia. Aqui estão mais alguns literais de timespan: `12h`, `30m`, `10s` e `0.01s`.
* `floor`(alias `bin`) Arredonda um valor para baixo toohello múltiplo mais próximo de valor de base Olá você fornecer. Portanto `floor(aTime, 1s)` Arredonda vez toohello mais próximo segundo.

Expressões podem incluir todos os operadores de saudação normal (`+`, `-`,...), e há uma variedade de funções úteis.

## <a name="extend"></a>Extend
Se você quiser apenas tooadd toohello de colunas existentes, use [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

Usando [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) é menos detalhada que [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) se você quiser tookeep todos Olá colunas existentes.

### <a name="convert-toolocal-time"></a>Converter o horário de toolocal

Os carimbos de data e hora são sempre em UTC. Então se você estiver em Costa do Pacífico nos hello e é inverno, talvez você goste isso:

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a>[Resumir](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): agregar grupos de linhas
`Summarize` aplica uma *função de agregação* especificada em grupos de linhas.

Por exemplo, tempo de saudação toorespond tooa solicitação entra em seu aplicativo web é informado no campo de saudação `duration`. Vamos ver médio de resposta Olá tooall solicitações de tempo:

![](./media/app-insights-analytics-tour/410.png)

Ou podemos pode separar resultado Olá em solicitações de nomes diferentes:

![](./media/app-insights-analytics-tour/420.png)

`Summarize`coleta Olá pontos de dados no fluxo de saudação em grupos para os quais Olá `by` cláusula avalia igualmente. Cada valor na Olá `by` expressão - cada nome de operação em Olá acima exemplo - resulta em uma linha na tabela de resultados de saudação.

Ou podemos agrupar os resultados por hora do dia:

![](./media/app-insights-analytics-tour/430.png)

Observe como estamos usando Olá `bin` função (também conhecido como `floor`). Se usássemos apenas `by timestamp`, cada linha de entrada acabaria em seu próprio pequeno grupo. Para qualquer escalar contínua vezes like ou números, temos toobreak Olá série em um número gerenciável de valores discretos. `bin`-que é apenas Olá familiar arredondamento para baixo `floor` função - é Olá toodo de maneira mais fácil que.

Podemos usar Olá mesmos intervalos de tooreduce técnica de cadeias de caracteres:

![](./media/app-insights-analytics-tour/440.png)

Observe que você pode usar `name=` tooset nome de saudação de uma coluna de resultados, em expressões de agregação de saudação ou Olá por cláusula.

## <a name="counting-sampled-data"></a>Contando dados de amostra
`sum(itemCount)`é Olá recomendada agregação toocount eventos. Em muitos casos, itemCount = = 1, para a função hello simplesmente conta número Olá de linhas no grupo de saudação. Mas quando [amostragem](app-insights-sampling.md) está em operação, apenas uma fração de eventos original Olá são mantidas como pontos de dados no Application Insights para que para cada ponto de dados que você vê, existem `itemCount` eventos.

Por exemplo, se a amostragem descarta 75% de eventos original hello, itemCount = = 4 em registros de saudação retido - ou seja, para cada registro retido, havia quatro registros originais.

Amostragem adaptável faz com que itemCount toobe mais alta durante os períodos em que seu aplicativo está sendo usado intensamente.

Resumindo itemCount, portanto, fornece uma boa estimativa do número original de saudação de eventos.

![](./media/app-insights-analytics-tour/510.png)

Também há um `count()` agregação (e uma operação de contagem), para casos onde você realmente deseja toocount Olá número de linhas em um grupo.

Há uma série de [funções de agregação](https://docs.loganalytics.io/learn/tutorials/aggregations.html).

## <a name="charting-hello-results"></a>Gráficos de resultados de saudação
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

Por padrão, os resultados são exibidos como uma tabela:

![](./media/app-insights-analytics-tour/225.png)

Podemos fazer melhor do que o modo de exibição de tabela hello. Vamos analisar resultados Olá no modo de exibição de gráfico de saudação com opção de barra vertical hello:

![Clique em Gráfico, escolha o gráfico de barras Vertical e atribua os eixos x e y](./media/app-insights-analytics-tour/230.png)

Observe que embora nós não classificar resultados de Olá por hora (como você pode ver na exibição da tabela Olá), exibição de gráfico de saudação sempre mostra datetimes na ordem correta.


## <a name="timecharts"></a>Timecharts
Mostra quantos eventos há a cada hora:

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

Selecione a opção de exibição de gráfico de saudação:

![timechart](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a>Várias séries
Várias expressões em Olá `summarize` cláusula cria várias colunas.

Várias expressões em Olá `by` cláusula cria várias linhas, uma para cada combinação de valores.

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Tabela de solicitações por hora e local](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a>Segmentar um gráfico por dimensões
Se gráfico uma tabela que tenha uma coluna de cadeia de caracteres e uma coluna numérica, a cadeia de caracteres hello puder ser dados numéricos do hello toosplit usadas em séries distintas de pontos. Se houver mais de uma coluna de cadeia de caracteres, você pode escolher qual coluna toouse como discriminador de saudação.

![Segmentar um gráfico de análise](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a>Taxa de devolução

Converter um toouse de cadeia de caracteres booliana tooa-lo como um discriminador:

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

### <a name="display-multiple-metrics"></a>Exibir várias métricas
Se o gráfico de uma tabela que tem mais de uma coluna numérica, em adição toohello timestamp, você pode exibir qualquer combinação desses itens.

![Segmentar um gráfico de análise](./media/app-insights-analytics-tour/110.png)

Você deve selecionar **Não Dividir** antes de selecionar várias colunas numéricas. Não é possível dividir, uma coluna de cadeia de caracteres no hello mesmo tempo como exibir mais de uma coluna numérica.

## <a name="daily-average-cycle"></a>Ciclo médio diário
Como o uso variar ao longo do dia médio Olá?

Solicitações de contagem por tempo de saudação módulo um dia, guardadas em horas:

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
> Observe que no momento temos tooconvert toodatetimes de durações de tempo em ordem toodisplay em um gráfico de linha.
>
>

## <a name="compare-multiple-daily-series"></a>Comparar várias séries diárias
Como o uso variar ao longo do tempo de saudação do dia em países diferentes?

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

## <a name="plot-a-distribution"></a>Plotar uma distribuição
Quantas sessões existem de comprimentos diferentes?

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

última linha de saudação é necessário tooconvert toodatetime. No momento eixo Olá x de um gráfico é exibido como um valor escalar somente se ele for uma data e hora.

Olá `where` cláusula exclui sessões única (sessionDuration = = 0) e conjuntos de Olá comprimento do eixo x da saudação.

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[Percentis](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
Quais intervalos de durações abordam diferentes porcentagens de sessões?

Usar Olá acima de consulta, mas substitua a última linha de saudação:

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

Também é removida limite superior Olá Olá onde cláusula, na ordem tooget corrigir ilustrações, incluindo todas as sessões com mais de uma solicitação:

![result](./media/app-insights-analytics-tour/180.png)

O que nos mostra que:

* 5% das sessões têm uma duração de menos de 3 minutos e 34 segundos;
* 50% das sessões duram menos de 36 minutos;
* 5% das sessões duram mais de 7 dias

tooget uma análise separada para cada país, apenas temos toobring Olá client_CountryOrRegion coluna separadamente através de ambos resumir operadores:

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

## <a name="join"></a>Ingressar
Temos acesso tooseveral tabelas, incluindo solicitações e exceções.

toofind Olá exceções relacionadas tooa solicitação retornou uma resposta de falha, pode unir tabelas de saudação em `session_Id`:

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


É uma boa prática toouse `project` tooselect colunas de saudação apenas precisamos antes de executar Olá junção.
Em Olá mesmas cláusulas, podemos renomear a coluna de carimbo de hora de saudação.

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-tooa-variable"></a>[Permitir que](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): atribuir uma variável de tooa de resultado

Use `let` tooseparate partes de saudação da expressão anterior hello. resultados de saudação não foram modificados:

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> No cliente de análise hello, não coloque as linhas em branco entre as partes de saudação de consulta de saudação. Verifique tooexecute-se de que todos eles.
>

Use `toscalar` tooconvert um valor de tooa de célula de tabela única:

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


### <a name="functions"></a>Funções

Use *permitem* toodefine uma função:

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a>Acessando objetos aninhados
Os objetos aninhados podem ser acessados facilmente. Por exemplo, no fluxo de exceções hello, você pode ver objetos estruturados como este:

![result](./media/app-insights-analytics-tour/520.png)

Você pode mesclá-la escolhendo Propriedades Olá em que você estiver interessado:

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

Observe que você precisa que o tipo apropriado do toohello toocast Olá resultado.


## <a name="custom-properties-and-measurements"></a>Medidas e propriedades personalizadas
Se seu aplicativo anexa [dimensões personalizadas (Propriedades) e medidas personalizadas](app-insights-api-custom-events-metrics.md#properties) tooevents, em seguida, você vai vê-los no hello `customDimensions` e `customMeasurements` objetos.

Por exemplo, se o seu aplicativo inclui:

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

tooextract esses valores na análise:

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast tooexpected type

```

tooverify se uma dimensão personalizada é de um tipo específico:

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a>Painéis
Você pode fixar o painel resultados em ordem toobring tooa juntos todos os seus gráficos e tabelas mais importantes.

* [Painel compartilhado do Azure](app-insights-dashboards.md#share-dashboards): clique no ícone de pino hello. Antes de fazer isso, você deve ter um painel compartilhado. No portal do Azure de Olá, abrir ou criar um painel e clicar em compartilhamento.
* [Painel do Power BI](app-insights-export-power-bi.md): clique em Exportar, Consulta do Power BI. Uma vantagem dessa alternativa é que você pode exibir sua consulta juntamente com outros resultados de uma ampla variedade de fontes.

## <a name="combine-with-imported-data"></a>Combinar com dados importados

Relatórios de análise uma aparência excelentes no painel hello, mas, às vezes, você deseja tootranslate Olá dados tooa mais de forma fácil de entender. Por exemplo, suponha que os usuários autenticados são identificados na telemetria Olá por um alias. Você gostaria que tooshow seu real nomes em seus resultados. toodo isso, é necessário um arquivo CSV que mapeia de nomes reais da saudação aliases toohello.

Você pode importar um arquivo de dados e usá-lo como qualquer uma das tabelas de saudação padrão (solicitações, exceções e assim por diante). É possível consultá-la sozinha ou uni-la a outras tabelas. Por exemplo, se você tiver uma tabela chamada usermap e ele tem colunas `realName` e `userId`, e em seguida, você pode usá-lo Olá tootranslate `user_AuthenticatedId` campo telemetria de solicitação hello:

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get hello realName field from hello usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

tooimport uma tabela, na folha de esquema hello, em **outras fontes de dados**, siga Olá instruções tooadd uma nova fonte de dados, carregando um exemplo dos dados. Em seguida, você pode usar tabelas de tooupload essa definição.

o recurso de importação Hello está atualmente em visualização, portanto, inicialmente, você verá um link "Entre em contato conosco" em "Outras fontes de dados." Use este toosign toohello programa de visualização e link hello será substituído por um botão "Adicionar nova fonte de dados".


## <a name="tables"></a>Tabelas
saudação de telemetria recebida do seu aplicativo está acessível por meio de várias tabelas. esquema de saudação de propriedades disponíveis para cada tabela é visível à esquerda de saudação da janela de saudação.

### <a name="requests-table"></a>Tabela de solicitações
Tooyour web app e o segmento de solicitações HTTP de contagem por nome de página:

![Conte solicitações segmentadas por nome](./media/app-insights-analytics-tour/analytics-count-requests.png)

Localiza as solicitações de saudação que falham mais:

![Conte solicitações segmentadas por nome](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a>Tabela de eventos personalizada
Se você usar [Trackevent](app-insights-api-custom-events-metrics.md#trackevent) toosend seus próprios eventos, você pode lê-los desta tabela.

Vejamos um exemplo em que o código do aplicativo contém estas linhas:

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

Frequência de saudação desses eventos de exibição:

![Taxa de exibição de eventos personalizados](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

Extrai eventos Olá medidas e dimensões:

![Taxa de exibição de eventos personalizados](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a>Tabela de métricas personalizada
Se você estiver usando [Trackmetric](app-insights-api-custom-events-metrics.md#trackmetric) toosend seus próprios valores da métrica, você encontrará seus resultados no hello **customMetrics** fluxo. Por exemplo:  

![Métricas personalizadas na análise do Application Insights](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> Em [Metrics Explorer](app-insights-metrics-explorer.md), todas as medidas personalizadas anexado tooany tipo de telemetria aparecem juntas na folha de métricas de saudação juntamente com métricas enviadas usando `TrackMetric()`. Mas na análise, medidas personalizadas ainda estão anexados toowhichever tipo de telemetria que foram executadas nos eventos ou solicitações e assim por diante - enquanto métricas enviadas pelo TrackMetric aparecem em seu próprio fluxo.
>
>

### <a name="performance-counters-table"></a>Tabela de contadores de desempenho
Os [contadores de desempenho](app-insights-performance-counters.md) mostram métricas básicas do sistema para seu aplicativo, tais como CPU, memória e uso de rede. Você pode configurar Olá SDK toosend contadores adicionais, incluindo seus próprios contadores personalizados.

Olá **performanceCounters** esquema expõe Olá `category`, `counter` nome, e `instance` nome de contador de desempenho. Nomes de instância do contador são somente os contadores de desempenho toosome aplicável e geralmente indicam o nome de saudação do hello processo toowhich Olá contagem está relacionada. Telemetria Olá para cada aplicativo, você verá apenas os contadores Olá para o aplicativo. Por exemplo, toosee quais contadores estão disponíveis:

![Contadores de desempenho na análise do Application Insights](./media/app-insights-analytics-tour/analytics-performance-counters.png)

tooget um gráfico de memória disponível em Olá período selecionado:

![Gráfico de tempo da memória na análise do Application Insights](./media/app-insights-analytics-tour/analytics-available-memory.png)

Como outros telemetria **performanceCounters** também tem uma coluna `cloud_RoleInstance` que indica Olá identidade da máquina de host de saudação em que seu aplicativo é executado. Por exemplo, toocompare Olá desempenho do aplicativo em máquinas diferentes hello:

![Desempenho segmentado por instância de função na análise do Application Insights](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a>Tabela de exceções
As [exceções relatadas pelo seu aplicativo](app-insights-asp-net-exceptions.md) estão disponíveis nessa tabela.

toofind Olá solicitação HTTP que seu aplicativo estava manipulando quando Olá exceção foi gerada, ingressar em operation_Id:

![Ingressar em exceções com solicitações em operation_Id](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a>Tabela de intervalos do navegador
`browserTimings` mostra os dados de carregamento de página coletados nos navegadores de seus usuários.

[Configurar seu aplicativo de telemetria do lado do cliente](app-insights-javascript.md) em ordem toosee essas métricas.

esquema de saudação inclui [métricas indicando comprimentos de saudação das diferentes fases do processo de carregamento de página de saudação](app-insights-javascript.md#page-load-performance). (Elas não indicam Olá período que os usuários ler uma página).  

Mostrar popularities Olá de diferentes páginas e tempos para cada página de carregamento:

![Tempos de carregamento de página no Analytics](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a>Tabela de resultados de disponibilidade
`availabilityResults`mostra Olá resultados de sua [testes na web](app-insights-monitor-web-app-availability.md). Cada execução dos testes de cada local de teste é relatada separadamente.

![Tempos de carregamento de página no Analytics](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a>Tabela de dependências
Contém os resultados de chamadas que seu aplicativo torna toodatabases e APIs REST e outros chama tooTrackDependency(). Também inclui chamadas AJAX feitas do navegador de saudação.

Chamadas AJAX de navegador hello:

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

Chamadas de dependência do servidor de saudação:

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

Sempre mostram resultados de dependência do lado do servidor `success==False` se hello Application Insights Agent não está instalado. No entanto, hello outros dados estão corretos.

### <a name="traces-table"></a>Tabela de rastreamentos
Contém a telemetria de saudação enviada pelo seu aplicativo usando tracktrace (), ou [outras estruturas de registro em log](app-insights-asp-net-trace-logs.md).

## <a name="video"></a>Vídeo 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

Consultas avançadas:

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a>Próximas etapas
* [Referência de linguagem de análise](app-insights-analytics-reference.md)
* [Roteiro de SQL-usuários](https://aka.ms/sql-analytics) converte as linguagens mais comuns de saudação.

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
