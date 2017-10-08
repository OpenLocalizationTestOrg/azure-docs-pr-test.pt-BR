---
title: "aaaApplication Insights API para eventos personalizados e métricas | Microsoft Docs"
description: "Insira algumas linhas de código em seu uso tootrack dispositivo ou aplicativo de área de trabalho, página da Web ou serviço e diagnosticar problemas."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: f3d207a47bb4825efda806a19dd0c26540db7bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a>API do Application Insights para métricas e eventos personalizados

Insira algumas linhas de código no seu toofind aplicativo out que os usuários estão fazendo com que ele ou toohelp diagnosticar problemas. Você pode enviar telemetria de aplicativos da área de trabalho e de dispositivo, clientes Web e servidores Web. Saudação de uso [Azure Application Insights](app-insights-overview.md) principais eventos personalizados do API de telemetria toosend e métricas e suas próprias versões da telemetria padrão. Essa API é Olá mesma API esse padrão Olá usam os coletores de dados do Application Insights.

## <a name="api-summary"></a>Resumo da API
Olá API é uniforme em todas as plataformas, além de algumas pequenas variações.

| Método | Usado para |
| --- | --- |
| [`TrackPageView`](#page-views) |Páginas, telas, folhas ou formulários. |
| [`TrackEvent`](#trackevent) |Ações de usuário e outros eventos. Usado tootrack desempenho de comportamento ou toomonitor do usuário. |
| [`TrackMetric`](#trackmetric) |Medidas de desempenho, como comprimentos de fila de eventos de toospecific não relacionados. |
| [`TrackException`](#trackexception) |Registrar em log as exceções para diagnóstico. Rastreamento onde eles ocorrem em eventos de tooother de relação e examine os rastreamentos de pilha. |
| [`TrackRequest`](#trackrequest) |Registro em log frequência hello e duração de solicitações de servidor para análise de desempenho. |
| [`TrackTrace`](#tracktrace) |Mensagens de log de diagnóstico. Você também pode capturar logs de terceiros. |
| [`TrackDependency`](#trackdependency) |Duração de saudação do registro e a frequência de componentes de tooexternal de chamadas que seu aplicativo depende. |

Você pode [anexar propriedades e métricas](#properties) toomost dessas chamadas de telemetria.

## <a name="prep"></a>Antes de começar
Se você ainda não tem uma referência no SDK do Application Insights:

* Adicione projeto de tooyour do SDK do Application Insights hello:

  * [Projeto do ASP.NET](app-insights-asp-net.md)
  * [Projeto Java](app-insights-java-get-started.md)
  * [JavaScript em cada página da Web](app-insights-javascript.md) 
* Em seu código de servidor Web ou dispositivo, inclua:

    *C#:* `using Microsoft.ApplicationInsights;`

    *Visual Basic:* `Imports Microsoft.ApplicationInsights`

    *Java:* `import com.microsoft.applicationinsights.TelemetryClient;`

## <a name="constructing-a-telemetryclient-instance"></a>Construção de uma instância de TelemetryClient
Construa uma instância de `TelemetryClient` (exceto em JavaScript nas páginas da Web):

*C#*

    private TelemetryClient telemetry = new TelemetryClient();

*Visual Basic*

    Private Dim telemetry As New TelemetryClient

*Java*

    private TelemetryClient telemetry = new TelemetryClient();

TelemetryClient é thread-safe.

É recomendável usar uma instância de TelemetryClient para cada módulo do seu aplicativo. Por exemplo, você pode ter uma instância de TelemetryClient em seu web service tooreport solicitações HTTP de entrada e outro em eventos de lógica de negócios um middleware classe tooreport. Você pode definir propriedades, como `TelemetryClient.Context.User.Id` tootrack usuários e sessões, ou `TelemetryClient.Context.Device.Id` tooidentify máquina de saudação. Essas informações são eventos anexados tooall Olá envios de instância.

## <a name="trackevent"></a>TrackEvent
No Application Insights, um *evento personalizado* é um ponto de dados que você pode exibir no [Metrics Explorer](app-insights-metrics-explorer.md) como uma contagem agregada e na [Pesquisa de Diagnóstico](app-insights-diagnostic-search.md) como ocorrências individuais. (Não é relacionado tooMVC ou outros framework "eventos".)

Inserir `TrackEvent` chamadas em seu código toocount vários eventos. Com que frequência os usuários escolhem um determinado recurso, com que frequência eles atingem metas específicas ou talvez com que frequência cometem tipos de erro específicos.

Por exemplo, em um aplicativo de jogo, envie um evento sempre que um usuário wins jogo hello:

*JavaScript*

    appInsights.trackEvent("WinGame");

*C#*

    telemetry.TrackEvent("WinGame");

*Visual Basic*

    telemetry.TrackEvent("WinGame")

*Java*

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a>Exibir os eventos no portal do Microsoft Azure Olá
toosee uma contagem de seus eventos, abra um [Metrics Explorer](app-insights-metrics-explorer.md) folha, adicionar um novo gráfico e selecione **eventos**.  

![Ver uma contagem de eventos personalizados](./media/app-insights-api-custom-events-metrics/01-custom.png)

contagens de saudação toocompare eventos diferentes, definir o tipo de gráfico de saudação muito**grade**e de grupo pelo nome do evento:

![Defina o tipo de gráfico de saudação e agrupamento](./media/app-insights-api-custom-events-metrics/07-grid.png)

Na grade de hello, clique em um nome toosee individuais as ocorrências de eventos que o evento. toosee mais detalham - clique em qualquer ocorrência na lista de saudação.

![Drill-through eventos Olá](./media/app-insights-api-custom-events-metrics/03-instances.png)

toofocus em eventos específicos em pesquisa ou Metrics Explorer filtro toohello nomes de evento do conjunto Olá folha que você estiver interessado em:

![Abra Filtros, expanda o Nome do evento e selecione um ou mais valores](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a>Eventos personalizados na Análise

Telemetria Hello está disponível no hello `customEvents` tabela [aplicativo Insights análise](app-insights-analytics.md). Cada linha representa uma chamada muito`trackEvent(..)` em seu aplicativo. 

Se [amostragem](app-insights-sampling.md) está em operação, a propriedade itemCount de saudação mostra um valor maior que 1. Para exemplo itemCount = = 10 significa que de 10 chamadas tootrackEvent(), processo de amostragem Olá transmitido apenas um deles. tooget uma contagem correta de eventos personalizados, você deve usar, portanto, usar o código como `customEvent | summarize sum(itemCount)`.


## <a name="trackmetric"></a>TrackMetric

Application Insights pode métricas que não estão anexados tooparticular eventos do gráfico. Por exemplo, você pode monitorar um comprimento de fila em intervalos regulares. Com métricas, medidas individuais Olá são menos interessantes que variações hello e tendências e então estatísticos gráficos são úteis.

Em ordem toosend métricas tooApplication Insights, você pode usar o hello `TrackMetric(..)` API. Há dois toosend de maneiras uma métrica: 

* Valor único. Toda vez que você realiza uma medida em seu aplicativo, você enviar valor correspondente Olá tooApplication Insights. Por exemplo, suponha que você tenha uma métrica que descreve o número de saudação de itens em um contêiner. Durante um período de tempo específico, você primeiro colocar três itens em contêiner hello e, em seguida, remova dois itens. Da mesma forma, você poderia chamar `TrackMetric` duas vezes: primeiro passar o valor de saudação `3` e, em seguida, Olá valor `-2`. O Application Insights armazena os dois valores em seu nome. 

* Agregação. Ao trabalhar com as métricas, raramente há interesse em cada medida. Em vez disso, um resumo do que aconteceu durante um determinado período de tempo é importante. Esse tipo de resumo é chamado de _agregação_. Olá, o exemplo acima, Olá métrica soma de agregação daquele período de tempo é `1` e contagem de Olá Olá dos valores das métricas é `2`. Ao usar a abordagem de agregação hello, apenas invocar `TrackMetric` uma vez por hora período e enviar Olá valores de agregação. Isso é hello abordagem recomendada, pois ele pode reduzir significativamente o custo de saudação e desempenho sobrecarga enviando dados menos pontos tooApplication Insights, enquanto ainda coleta todas as informações relevantes.

### <a name="examples"></a>Exemplos:

#### <a name="single-values"></a>Valores únicos

toosend um único valor de métrica:

*JavaScript*

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

*C#, Java*

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a>Métricas de agregação

É recomendável tooaggregate métricas antes de enviá-los do seu aplicativo, largura de banda tooreduce, tooimprove e o custo de desempenho.
Aqui está um exemplo de código de agregação:

*C#*

```C#
using System;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;

namespace MetricAggregationExample
{
    /// <summary>
    /// Aggregates metric values for a single time period.
    /// </summary>
    internal class MetricAggregator
    {
        private SpinLock _trackLock = new SpinLock();

        public DateTimeOffset StartTimestamp    { get; }
        public int Count                        { get; private set; }
        public double Sum                       { get; private set; }
        public double SumOfSquares              { get; private set; }
        public double Min                       { get; private set; }
        public double Max                       { get; private set; }
        public double Average                   { get { return (Count == 0) ? 0 : (Sum / Count); } }
        public double Variance                  { get { return (Count == 0) ? 0 : (SumOfSquares / Count)
                                                                                  - (Average * Average); } }
        public double StandardDeviation         { get { return Math.Sqrt(Variance); } }

        public MetricAggregator(DateTimeOffset startTimestamp)
        {
            this.StartTimestamp = startTimestamp;
        }

        public void TrackValue(double value)
        {
            bool lockAcquired = false;

            try
            {
                _trackLock.Enter(ref lockAcquired);

                if ((Count == 0) || (value < Min))  { Min = value; }
                if ((Count == 0) || (value > Max))  { Max = value; }
                Count++;
                Sum += value;
                SumOfSquares += value * value;
            }
            finally
            {
                if (lockAcquired)
                {
                    _trackLock.Exit();
                }
            }
        }
    }   // internal class MetricAggregator

    /// <summary>
    /// Accepts metric values and sends hello aggregated values at 1-minute intervals.
    /// </summary>
    public sealed class Metric : IDisposable
    {
        private static readonly TimeSpan AggregationPeriod = TimeSpan.FromSeconds(60);

        private bool _isDisposed = false;
        private MetricAggregator _aggregator = null;
        private readonly TelemetryClient _telemetryClient;

        public string Name { get; }

        public Metric(string name, TelemetryClient telemetryClient)
        {
            this.Name = name ?? "null";
            this._aggregator = new MetricAggregator(DateTimeOffset.UtcNow);
            this._telemetryClient = telemetryClient ?? throw new ArgumentNullException(nameof(telemetryClient));

            Task.Run(this.AggregatorLoopAsync);
        }

        public void TrackValue(double value)
        {
            MetricAggregator currAggregator = _aggregator;
            if (currAggregator != null)
            {
                currAggregator.TrackValue(value);
            }
        }

        private async Task AggregatorLoopAsync()
        {
            while (_isDisposed == false)
            {
                try
                {
                    // Wait for end end of hello aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap hello current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute hello actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct hello metric telemetry item and send:
                        var aggregatedMetricTelemetry = new MetricTelemetry(
                                Name,
                                prevAggregator.Count,
                                prevAggregator.Sum,
                                prevAggregator.Min,
                                prevAggregator.Max,
                                prevAggregator.StandardDeviation);
                        aggregatedMetricTelemetry.Properties["AggregationPeriod"] = aggPeriod.ToString("c");

                        _telemetryClient.Track(aggregatedMetricTelemetry);
                    }
                }
                catch(Exception ex)
                {
                    // log ex as appropriate for your application
                }
            }
        }

        void IDisposable.Dispose()
        {
            _isDisposed = true;
            _aggregator = null;
        }
    }   // public sealed class Metric
}
```

### <a name="custom-metrics-in-metrics-explorer"></a>Métricas personalizadas no Metrics Explorer

resultados de saudação toosee, abra Metrics Explorer e adicione um novo gráfico. Edite saudação gráfico tooshow sua métrica.

> [!NOTE]
> A métrica personalizada pode levar vários tooappear de minutos na lista de saudação de métricas disponíveis.
>

![Adicionar um novo gráfico ou escolher um e, em Personalizar, escolher a métrica](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a>Métricas personalizadas no Analytics

Telemetria Hello está disponível no hello `customMetrics` tabela [aplicativo Insights análise](app-insights-analytics.md). Cada linha representa uma chamada muito`trackMetric(..)` em seu aplicativo.
* `valueSum`-Esta é a soma de saudação de medidas de saudação. valor médio tooget hello, divisão por `valueCount`.
* `valueCount`-Olá número de medidas que foram agregados em isso `trackMetric(..)` chamar.

## <a name="page-views"></a>Visualizações de página
Em um aplicativo de página da Web ou dispositivo, a telemetria de exibição de páginas é enviada por padrão quando cada tela ou página é carregada. Mas você pode alterar modos de exibição de página que tootrack em horários adicionais ou diferentes. Por exemplo, em um aplicativo que exibe as guias ou em folhas, convém tootrack uma página sempre que o usuário Olá abre uma nova folha.

![Lentes de Utilização na folha Visão geral](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

Dados de usuário e a sessão são enviados como propriedades junto com os modos de exibição de página, portanto Olá gráficos de usuário e a sessão ficar ativos quando não há telemetria de exibição de página.

### <a name="custom-page-views"></a>Exibições de páginas personalizadas
*JavaScript*

    appInsights.trackPageView("tab1");

*C#*

    telemetry.TrackPageView("GameReviewPage");

*Visual Basic*

    telemetry.TrackPageView("GameReviewPage")


Se você tiver várias guias em diferentes páginas HTML, você pode especificar a URL de saudação muito:

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a>Definindo o tempo das exibições de página
Por padrão, os tempos de saudação relatado como **tempo de carregamento da exibição de página** são medidas da quando navegador Olá envia a solicitação de hello, até que o evento de carregamento de página do navegador Olá é chamado.

Em vez disso, é possível:

* Defina uma duração explícita em Olá [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) chamar: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.
* Use chamadas de intervalo de exibição de página Olá `startTrackPage` e `stopTrackPage`.

*JavaScript*

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

...

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

Olá nome que você usa como o primeiro parâmetro de saudação associa início hello e parar de chamadas. O padrão é o nome de página atual toohello.

carregamento de página resultante Olá durações exibidas no Gerenciador de métricas são derivadas do intervalo de saudação entre hello iniciar e parar de chamadas. É o tooyou o intervalo de tempo realmente.

### <a name="page-telemetry-in-analytics"></a>Telemetria de página na Análise

Na [Análise](app-insights-analytics.md), duas tabelas mostram dados das operações do navegador:

* Olá `pageViews` tabela contém dados sobre Olá URL e título da página
* Olá `browserTimings` tabela contém dados sobre o desempenho do cliente, como tooprocess de tempo gasto Olá Olá os dados de entrada

toofind quanto tempo o navegador Olá leva tooprocess páginas diferentes:

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

toodiscover popularities de saudação de navegadores diferentes:

```
pageViews | summarize count() by client_Browser
```

chamadas de tooAJAX de modos de exibição de página tooassociate, junção com dependências:

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a>TrackRequest
servidor de saudação SDK usa solicitações HTTP toolog TrackRequest.

Você também pode chamá-lo por conta própria se você quiser toosimulate solicitações em um contexto em que você não tem Olá web serviço módulo está em execução.

No entanto, a saudação recomendado telemetria de solicitação do modo toosend é onde a solicitação de saudação atua como um <a href="#operation-context">contexto de operação</a>.

## <a name="operation-context"></a>Contexto de operação
Você pode associar itens de telemetria juntos anexando toothem uma ID de operação comum. módulo de rastreamento de solicitação padrão Olá faz isso para exceções e outros eventos que são enviados enquanto uma solicitação HTTP está sendo processada. Em [pesquisa](app-insights-diagnostic-search.md) e [análise](app-insights-analytics.md), você pode usar todos os eventos associados à solicitação Olá Olá ID tooeasily localizar.

Olá mais fácil maneira tooset Olá ID é tooset um contexto de operação usando esse padrão:

*C#*

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use hello same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

Junto com a configuração de um contexto de operação, `StartOperation` cria um item de telemetria do tipo hello que você especificar. Ele envia a telemetria Olá item quando você descartar operação hello, ou se você chamar explicitamente `StopOperation`. Se você usar `RequestTelemetry` como tipo de telemetria hello, sua duração é definir o intervalo de toohello atingiu o tempo entre o início e parada.

Contextos de operação não podem ser aninhados. Se já há um contexto de operação, sua ID é associado a todos os itens de saudação contido, inclusive Olá item criado com `StartOperation`.

Na pesquisa, o contexto de operação de saudação é Olá toocreate usado **itens relacionados** lista:

![Itens relacionados](./media/app-insights-api-custom-events-metrics/21.png)

Consulte [application-insights-custom-operations-tracking.md] para obter mais informações sobre operações personalizadas de acompanhamento.

### <a name="requests-in-analytics"></a>Consultas na Análise 

Em [análises do aplicativo Insights](app-insights-analytics.md), solicitações de mostrar o em Olá `requests` tabela.

Se [amostragem](app-insights-sampling.md) está em operação, propriedade itemCount de saudação mostrará um valor maior que 1. Para exemplo itemCount = = 10 significa que de 10 chamadas tootrackRequest(), processo de amostragem Olá transmitido apenas um deles. uma contagem correta das solicitações e duração média de tooget segmentadas por nomes de solicitação, use um código como:

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a>TrackException
Envie exceções tooApplication Insights:

* muito[contar](app-insights-metrics-explorer.md), como uma indicação de frequência de saudação de um problema.
* muito[examinar ocorrências individuais](app-insights-diagnostic-search.md).

Olá relatórios incluem rastreamentos de pilha de saudação.

*C#*

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

*JavaScript*

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

Olá SDKs catch muitas exceções automaticamente, para que você não tenha sempre toocall TrackException explicitamente.

* ASP.NET: [escrever código exceções toocatch](app-insights-asp-net-exceptions.md).
* J2EE: [as exceções são capturadas automaticamente](app-insights-java-get-started.md#exceptions-and-request-failures).
* JavaScript: exceções são capturadas automaticamente. Coleta automática de toodisable, adicione um trecho de código toohello de linha que você inserir em suas páginas da Web:

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a>Exceções na Análise

Em [aplicativo Insights análise](app-insights-analytics.md), exceções aparecem no hello `exceptions` tabela.

Se [amostragem](app-insights-sampling.md) está em operação, hello `itemCount` propriedade mostra um valor maior que 1. Para exemplo itemCount = = 10 significa que de 10 chamadas tootrackException(), processo de amostragem Olá transmitido apenas um deles. tooget uma contagem correta de exceções segmentadas por tipo de exceção, use um código como:

```
exceptions | summarize sum(itemCount) by type
```

A maioria das Olá importante informações de pilha já são extraídas em variáveis separadas, mas você pode extrair Olá separar `details` estrutura tooget mais. Como essa estrutura é dinâmica, você deve converter o tipo de toohello do hello resultado esperado. Por exemplo:

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

exceções de tooassociate com suas solicitações relacionadas, use uma junção:

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a>TrackTrace
Use TrackTrace toohelp diagnosticar problemas enviando um tooApplication "trilha de navegação estrutural" Insights. Você pode enviar partes de dados de diagnóstico e inspecioná-los na [Pesquisa de Diagnóstico](app-insights-diagnostic-search.md).

[Adaptadores de log](app-insights-asp-net-trace-logs.md) usar este portal de toohello API toosend logs de terceiros.

*C#*

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


Você pode pesquisar no conteúdo da mensagem, mas (diferentemente de valores de propriedade) não é possível filtrar nele.

limite de tamanho de saudação no `message` é muito maior do que o limite de saudação em Propriedades.
Uma vantagem de TrackTrace é que você pode colocar dados relativamente longos na mensagem de saudação. Por exemplo, você pode codificar dados POST.  

Além disso, você pode adicionar uma mensagem de tooyour nível de severidade. E, como outros telemetria, você pode adicionar toohelp de valores de propriedade que você filtrar ou pesquisar para diferentes conjuntos de rastreamentos. Por exemplo:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

Em [pesquisa](app-insights-diagnostic-search.md), você pode, em seguida, facilmente filtrar todas as mensagens de saudação de um nível de severidade específico que se relacionam tooa determinado banco de dados.


### <a name="traces-in-analytics"></a>Rastreamentos na Análise

Em [aplicativo Insights análise](app-insights-analytics.md), chama tooTrackTrace Mostrar em Olá `traces` tabela.

Se [amostragem](app-insights-sampling.md) está em operação, a propriedade itemCount de saudação mostra um valor maior que 1. Para exemplo itemCount = = 10 significa que de 10 chamadas muito`trackTrace()`, processo de amostragem Olá transmitido apenas um deles. tooget uma contagem correta de chamadas de rastreamento, você deve usar, portanto, código, como `traces | summarize sum(itemCount)`.

## <a name="trackdependency"></a>TrackDependency
Olá Use TrackDependency chamar tempos de resposta de saudação tootrack e taxas de sucesso de parte externa de tooan de chamadas do código. os resultados de saudação aparecem nos gráficos de dependência Olá no portal de saudação.

```C#
var success = false;
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
try
{
    success = dependency.Call();
}
finally
{
    timer.Stop();
    telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
}
```

Lembre-se de servidor Olá SDKs incluem um [módulo de dependência](app-insights-asp-net-dependencies.md) que detecta e rastreia determinadas chamadas de dependência automaticamente – por exemplo, toodatabases e APIs REST. Você tem um agente em seu módulo de saudação do servidor toomake de tooinstall trabalhar. Você usar essa chamada chamadas tootrack Olá controle automatizada não catch, ou se não deseja que o agente de saudação tooinstall.

Editar tooturn fora do módulo de controle de dependência padrão hello, [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md) e excluir referência Olá muito`DependencyCollector.DependencyTrackingTelemetryModule`.

### <a name="dependencies-in-analytics"></a>Dependências na Análise

Em [aplicativo Insights análise](app-insights-analytics.md), chamadas trackDependency aparecem no hello `dependencies` tabela.

Se [amostragem](app-insights-sampling.md) está em operação, a propriedade itemCount de saudação mostra um valor maior que 1. Para exemplo itemCount = = 10 significa que de 10 chamadas tootrackDependency(), processo de amostragem Olá transmitido apenas um deles. tooget uma contagem correta de dependências segmentadas por componente de destino, use um código como:

```
dependencies | summarize sum(itemCount) by target
```

dependências de tooassociate com suas solicitações relacionadas, use uma junção:

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a>Liberando dados
Normalmente, Olá SDK envia dados às vezes escolhidos o impacto de saudação toominimize usuário hello. No entanto, em alguns casos, convém buffer de saudação tooflush – por exemplo, se você estiver usando Olá SDK em um aplicativo que é desligado.

*C#*

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

Observe que a função hello é assíncrona para Olá [canal de telemetria de servidor](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).

## <a name="authenticated-users"></a>usuários autenticados
Em um aplicativo Web, os usuários são (por padrão) identificados por cookies. Um usuário pode ser contado mais de uma vez se ele acessar seu aplicativo de um computador ou navegador diferente, ou se ele excluir cookies.

Se os usuários entrarem no aplicativo tooyour, você pode obter uma contagem mais precisa, definindo Olá autenticado ID de usuário no código de saudação do navegador:

*JavaScript*

```JS
// Called when my app has identified hello user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

Em um aplicativo MVC Web ASP.NET, por exemplo:

*Razor*

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

Não é necessário toouse Olá nome do usuário real entrar. Ele só tem toobe uma ID de usuário toothat exclusivo. Não é possível incluir espaços ou caracteres de saudação `,;=|`.

ID de usuário Olá também é definido em um cookie de sessão e enviado toohello server. Se o servidor de saudação SDK está instalado, Olá autenticado usuário que ID é enviado como parte das propriedades de contexto de saudação de telemetria de cliente e servidor. Assim, você poderá filtrar e pesquisar nele.

Se seu aplicativo de grupos de usuários de contas, você também pode passar um identificador para a conta de saudação (com hello mesmo caractere restrições).

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

No [Metrics Explorer](app-insights-metrics-explorer.md), você pode criar um gráfico que contabiliza **Usuários Autenticados** e **Contas de usuário**.

Você também pode [pesquisar](app-insights-diagnostic-search.md) por pontos de dados do cliente com contas e nomes de usuário específicos.

## <a name="properties"></a>Filtragem, pesquisa e segmentação de dados usando propriedades
Você pode anexar as medidas e propriedades tooyour eventos (e também toometrics, modos de exibição de página, exceções e outros dados de telemetria).

*Propriedades* são valores de cadeia de caracteres que você pode usar toofilter sua telemetria nos relatórios de uso de saudação. Por exemplo, se seu aplicativo oferece diversos jogos, pode anexar nome saudação do evento de jogo tooeach Olá para que você possa ver os jogos que são mais populares.

Há um limite de 8192 para o comprimento da cadeia de caracteres hello. (Se você quiser toosend grandes quantidades de dados, use o parâmetro de mensagem de saudação do [TrackTrace](#track-trace).)

*Métricas* são valores numéricos que podem ser apresentados graficamente. Por exemplo, convém toosee se não houver um aumento gradual pontuações de saudação atingir seu jogadores. gráficos de saudação podem ser segmentados por Olá propriedades que são enviadas com o evento hello, para que você possa obter separam ou empilhados gráficos de jogos diferentes.

Para toobe de valores da métrica exibido corretamente, eles devem ser too0 maior que ou igual.

Há alguns [limites no número de saudação de propriedades, valores de propriedade e métricas](#limits) que você pode usar.

*JavaScript*

    appInsights.trackEvent
      ("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

    appInsights.trackPageView
        ("page name", "http://fabrikam.com/pageurl.html",
          // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );


*C#*

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


*Visual Basic*

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics)


*Java*

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> Tome cuidado toolog informações de identificação pessoal em Propriedades.
>
>

*Se você usou métricas*, abra Metrics Explorer e selecione a métrica de saudação do hello **personalizado** grupo:

![Abra o Explorer métricas de gráfico selecione Olá e selecione a métrica Olá](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> Se a métrica não aparecer, ou se hello **personalizado** título não estiver lá, folha de seleção Olá fechar e tente novamente mais tarde. As métricas, às vezes, podem levar uma hora toobe agregados por meio do pipeline de saudação.

*Se você usou propriedades e métricas*, segmentar métrica Olá pela propriedade hello:

![Definir o agrupamento e, em seguida, selecione a propriedade Olá em Agrupar por](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

*Na pesquisa de diagnóstico*, você pode exibir as propriedades de saudação e métricas de ocorrências individuais de um evento.

![Selecionar uma instância e, em seguida, "..."](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

Saudação de uso **pesquisa** campo toosee ocorrências de eventos que têm um valor de propriedade em particular.

![Digite um termo em Pesquisar](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

[Saiba mais sobre as expressões de pesquisa](app-insights-diagnostic-search.md).

### <a name="alternative-way-tooset-properties-and-metrics"></a>Propriedades de tooset de maneira alternativa e métricas
Se for mais conveniente, você pode coletar parâmetros de saudação de um evento em um objeto separado:

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> Não reutilizar Olá mesma instância de item de telemetria (`event` neste exemplo) toocall Track*() várias vezes. Isso pode causar toobe telemetria enviada com a configuração incorreta.
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a>Medidas personalizadas e propriedades na Análise

Em [análise](app-insights-analytics.md), métricas personalizadas e propriedades mostram em Olá `customMeasurements` e `customDimensions` atributos de cada registro de telemetria.

Por exemplo, se você adicionou uma propriedade chamada "jogo" tooyour telemetria de solicitação, essa consulta contagens de ocorrências de saudação de valores diferentes de "jogo" e mostrar a média de saudação de saudação métrica personalizada "pontuação":

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

Observe que:

* Quando você extrai um valor de saudação customDimensions ou customMeasurements JSON, ele tem o tipo dinâmico e portanto você deve converter `tostring` ou `todouble`.
* conta de tootake da possibilidade de saudação do [amostragem](app-insights-sampling.md), você deve usar `sum(itemCount)`, não `count()`.



## <a name="timed"></a> Eventos de tempo
Às vezes, você deseja toochart quanto tempo demora tooperform uma ação. Por exemplo, você talvez queira tooknow quanto tempo os usuários tomem tooconsider escolhas em um jogo. Você pode usar o parâmetro de medição de saudação para isso.

*C#*

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform hello timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send hello event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <a name="defaults"></a>Propriedades padrão para telemetria personalizada
Se você quiser tooset valores de propriedade de padrão para alguns dos Olá eventos personalizados que você escreve, você pode defini-las em uma instância de TelemetryClient. Eles são anexados tooevery item de telemetria que é enviada do cliente.

*C#*

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

*Visual Basic*

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

*Java*

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



Chamadas de telemetria individuais podem substituir valores de padrão de Olá nos dicionários de sua propriedade.

*Para clientes Web JavaScript*, [use inicializadores de telemetria JavaScript](#js-initializer).

*Telemetria de tooall propriedades tooadd*, incluindo dados de saudação de módulos de coleção padrão [implementar `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties).

## <a name="sampling-filtering-and-processing-telemetry"></a>Amostragem, filtragem e processamento da telemetria
Você pode escrever código tooprocess sua telemetria antes do envio de saudação SDK. processamento de saudação inclui dados que são enviados de módulos de telemetria padrão hello, como coleta de solicitação HTTP e a coleção de dependência.

[Adicionar propriedades](app-insights-api-filtering-sampling.md#add-properties) tootelemetry implementando `ITelemetryInitializer`. Por exemplo, é possível adicionar números de versão ou valores que são calculados de outras propriedades.

[Filtragem](app-insights-api-filtering-sampling.md#filtering) pode modificar ou descartar telemetria antes do envio de saudação SDK implementando `ITelemetryProcesor`. Controlar o que é enviado ou descartado, mas tem tooaccount para efeito de saudação em suas métricas. Dependendo de como você descartar itens, você poderá perder Olá capacidade toonavigate entre itens relacionados.

[Amostragem](app-insights-api-filtering-sampling.md) tooreduce solução Olá do volume dos dados que são enviados de seu portal de toohello do aplicativo. Isso é feito sem afetar as métricas de saudação exibida. E isso é feito sem afetar os problemas de capacidade toodiagnose navegando entre itens relacionados, como exceções, solicitações e modos de exibição de página.

[Saiba mais](app-insights-api-filtering-sampling.md).

## <a name="disabling-telemetry"></a>Desabilitando a telemetria
muito*dinamicamente parar e iniciar* Olá coleta e transmissão de telemetria:

*C#*

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

muito*desabilitar os coletores padrão selecionados*– por exemplo, contadores de desempenho, as solicitações HTTP ou dependências – exclua ou comente a linhas relevantes Olá [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md). Você pode fazer isso, por exemplo, se você quiser toosend seus próprios dados TrackRequest.

## <a name="debug"></a>Modo de desenvolvedor
Durante a depuração, é útil toohave sua telemetria acelerada por meio do pipeline de saudação para que você possa ver os resultados imediatamente. Você também obter mensagens adicionais que ajudarão a rastrear problemas com a telemetria hello. Desative-a na produção, pois isso pode tornar seu aplicativo mais lento.

*C#*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

*Visual Basic*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <a name="ikey"></a>Definindo a chave de instrumentação Olá para telemetria personalizada selecionada
*C#*

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <a name="dynamic-ikey"></a> Chave de instrumentação dinâmica
tooavoid mistura de telemetria de desenvolvimento, teste e ambientes de produção, você pode [criar recursos do Application Insights separados](app-insights-create-new-resource.md) e altere suas chaves, dependendo do ambiente de saudação.

Em vez de obter a chave de instrumentação Olá Olá do arquivo de configuração, você pode definir no seu código. Chave de saudação definida em um método de inicialização, como global.aspx.cs em um serviço ASP.NET:

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

*JavaScript*

    appInsights.config.instrumentationKey = myKey;



Em páginas da Web, você pode querer tooset do servidor da web hello estado, em vez de codificá-lo literalmente em script hello. Por exemplo, em uma página da Web gerada em um aplicativo ASP.NET:

*JavaScript no Razor*

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a>TelemetryContext
TelemetryClient tem uma propriedade de Contexto, que contém valores que serão enviadas com todos os dados de telemetria. Eles normalmente são definidos pelos módulos de telemetria padrão hello, mas você pode também defini-las por conta própria. Por exemplo:

    telemetry.Context.Operation.Name = "MyOperationName";

Se você definir esses valores por conta própria, considere remover a linha relevante de saudação do [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md), de modo que seus valores e valores padrão de saudação não fiquem confusos.

* **Componente**: Olá aplicativo e sua versão.
* **Dispositivo**: dados sobre o dispositivo Olá onde o aplicativo hello está sendo executado. (Em aplicativos da web, isso é servidor hello ou dispositivo de cliente enviado da telemetria hello.)
* **InstrumentationKey**: Olá recurso do Application Insights no Azure, onde a telemetria Olá aparecem. Normalmente, escolhido no Applicationinsights.config.
* **Local**: Olá localização geográfica do dispositivo hello.
* **Operação**: em aplicativos da web, Olá solicitação HTTP atual. Em outros tipos de aplicativo, você pode definir essa eventos toogroup juntos.
  * **ID**: um valor gerado que correlaciona eventos diferentes para que, ao inspecionar qualquer evento na Pesquisa de Diagnóstico, você possa localizar itens relacionados.
  * **Nome**: um identificador, geralmente Olá URL da solicitação HTTP de saudação.
  * **SyntheticSource**: se não nula ou vazia, uma cadeia de caracteres que indica que essa fonte Olá da solicitação de saudação foi identificada como um teste da web ou robô. Por padrão, ela é excluída dos cálculos no Metrics Explorer.
* **Propriedades**: propriedades que são enviadas com todos os dados de telemetria. Pode ser substituído nas chamadas individuais de Track*.
* **Sessão**: Olá sessão de usuário. Olá ID estiver definido como valor tooa gerado, que é alterado quando o usuário Olá não foi ativo por um tempo.
* **Usuário**: informações do usuário.

## <a name="limits"></a>limites
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

tooavoid atingir o limite de taxa de dados hello, use [amostragem](app-insights-sampling.md).

toodetermine como dados long são mantidos, consulte [privacidade e retenção de dados](app-insights-data-retention-privacy.md).

## <a name="reference-docs"></a>Documentos de Referência
* [Referência do ASP.NET](https://msdn.microsoft.com/library/dn817570.aspx)
* [Referência do Java](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [Referência do JavaScript](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [SDK do Android](https://github.com/Microsoft/ApplicationInsights-Android)
* [SDK do iOS](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a>Código do SDK
* [SDK de Núcleo do ASP.NET](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [Pacotes do Windows Server](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [Java SDK](https://github.com/Microsoft/ApplicationInsights-Java)
* [SDK do JavaScript](https://github.com/Microsoft/ApplicationInsights-JS)
* [Todas as plataformas](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a>Perguntas
* *Que exceções podem ser lançadas por chamadas Track_()?*

    Nenhuma. Você não precisa toowrap-los em cláusulas de try-catch. Se Olá SDK encontrar problemas, ele registrará em log mensagens na saída de console de depuração de saudação e --se hello mensagens conseguir – em busca de diagnóstico.
* *Há dados de tooget uma API REST do portal Olá?*

    Sim, Olá [API de acesso a dados](https://dev.applicationinsights.io/). Incluem outros dados de maneiras tooextract [exportar de análise tooPower BI](app-insights-export-power-bi.md) e [a exportação contínua](app-insights-export-telemetry.md).

## <a name="next"></a>Próximas etapas
* [Pesquisar eventos e logs](app-insights-diagnostic-search.md)

* [Solução de problemas](app-insights-troubleshoot-faq.md)


