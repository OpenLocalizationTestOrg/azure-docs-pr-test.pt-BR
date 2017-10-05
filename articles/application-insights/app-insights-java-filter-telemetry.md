---
title: Filtrar a telemetria do Application Insights do Azure no aplicativo Web Java | Microsoft Docs
description: "Reduza o tráfego da telemetria filtrando os eventos que você não precisa monitorar."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 5f6d6d4ad590b85810c42e9f9520850024c5446a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="filter-telemetry-in-your-java-web-app"></a><span data-ttu-id="2022e-103">Filtrar a telemetria no aplicativo Web Java</span><span class="sxs-lookup"><span data-stu-id="2022e-103">Filter telemetry in your Java web app</span></span>

<span data-ttu-id="2022e-104">Os filtros fornecem uma maneira de selecionar a telemetria que seu [aplicativo Web Java envia ao Application Insights](app-insights-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2022e-104">Filters provide a way to select the telemetry that your [Java web app sends to Application Insights](app-insights-java-get-started.md).</span></span> <span data-ttu-id="2022e-105">Existem alguns filtros prontos para uso, mas você também pode escrever seus próprios filtros personalizados.</span><span class="sxs-lookup"><span data-stu-id="2022e-105">There are some out-of-the-box filters that you can use, and you can also write your own custom filters.</span></span>

<span data-ttu-id="2022e-106">Os filtros prontos para uso incluem:</span><span class="sxs-lookup"><span data-stu-id="2022e-106">The out-of-the-box filters include:</span></span>

* <span data-ttu-id="2022e-107">Nível de severidade de rastreamento</span><span class="sxs-lookup"><span data-stu-id="2022e-107">Trace severity level</span></span>
* <span data-ttu-id="2022e-108">URLs específicas, palavras-chave ou códigos de resposta</span><span class="sxs-lookup"><span data-stu-id="2022e-108">Specific URLs, keywords or response codes</span></span>
* <span data-ttu-id="2022e-109">Respostas rápidas, isto é, solicitações às quais seu aplicativo respondeu rapidamente</span><span class="sxs-lookup"><span data-stu-id="2022e-109">Fast responses - that is, requests to which your app responded to quickly</span></span>
* <span data-ttu-id="2022e-110">Nomes de eventos específicos</span><span class="sxs-lookup"><span data-stu-id="2022e-110">Specific event names</span></span>

> [!NOTE]
> <span data-ttu-id="2022e-111">Os filtros distorcem as métricas do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2022e-111">Filters skew the metrics of your app.</span></span> <span data-ttu-id="2022e-112">Por exemplo, você pode decidir que, para diagnosticar respostas lentas, vai definir um filtro para descartar tempos rápidos de resposta.</span><span class="sxs-lookup"><span data-stu-id="2022e-112">For example, you might decide that, in order to diagnose slow responses, you will set a filter to discard fast response times.</span></span> <span data-ttu-id="2022e-113">Mas você deve estar ciente de que a média dos tempos de resposta relatada pelo Application Insights será mais lenta que a velocidade verdadeira e a contagem de solicitações será menor que a contagem real.</span><span class="sxs-lookup"><span data-stu-id="2022e-113">But you must be aware that the average response times reported by Application Insights will then be slower than the true speed, and the count of requests will be smaller than the real count.</span></span>
> <span data-ttu-id="2022e-114">Se isso for um problema, use [Amostragem](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="2022e-114">If this is a concern, use [Sampling](app-insights-sampling.md) instead.</span></span>

## <a name="setting-filters"></a><span data-ttu-id="2022e-115">Definindo filtros</span><span class="sxs-lookup"><span data-stu-id="2022e-115">Setting filters</span></span>

<span data-ttu-id="2022e-116">Em ApplicationInsights.xml, adicione uma seção `TelemetryProcessors`, como neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="2022e-116">In ApplicationInsights.xml, add a `TelemetryProcessors` section like this example:</span></span>


```XML

    <ApplicationInsights>
      <TelemetryProcessors>

        <BuiltInProcessors>
           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="100"/>
                  <Add name="NotNeededResponseCodes" value="200-400"/>
           </Processor>

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="100"/>
                  <Add name="NotNeededNames" value="home,index"/>
                  <Add name="NotNeededUrls" value=".jpg,.css"/>
           </Processor>

           <Processor type="TelemetryEventFilter">
                  <!-- Names of events we don't want to see -->
                  <Add name="NotNeededNames" value="Start,Stop,Pause"/>
           </Processor>

           <!-- Exclude telemetry from availability tests and bots -->
           <Processor type="SyntheticSourceFilter">
                <!-- Optional: specify which synthetic sources,
                     comma-separated
                     - default is all synthetics -->
                <Add name="NotNeededSources" value="Application Insights Availability Monitoring,BingPreview"
           </Processor>

        </BuiltInProcessors>

        <CustomProcessors>
          <Processor type="com.fabrikam.MyFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>

      </TelemetryProcessors>
    </ApplicationInsights>

```




<span data-ttu-id="2022e-117">[Inspecione o conjunto completo de processadores internos](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span><span class="sxs-lookup"><span data-stu-id="2022e-117">[Inspect the full set of built-in processors](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span></span>

## <a name="built-in-filters"></a><span data-ttu-id="2022e-118">Filtros internos</span><span class="sxs-lookup"><span data-stu-id="2022e-118">Built-in filters</span></span>

### <a name="metric-telemetry-filter"></a><span data-ttu-id="2022e-119">Filtro de telemetria da métrica</span><span class="sxs-lookup"><span data-stu-id="2022e-119">Metric Telemetry filter</span></span>

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* <span data-ttu-id="2022e-120">`NotNeeded` — lista de nomes de métricas personalizadas separados por vírgula.</span><span class="sxs-lookup"><span data-stu-id="2022e-120">`NotNeeded` - Comma-separated list of custom metric names.</span></span>


### <a name="page-view-telemetry-filter"></a><span data-ttu-id="2022e-121">Filtro de telemetria da exibição de página</span><span class="sxs-lookup"><span data-stu-id="2022e-121">Page View Telemetry filter</span></span>

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* <span data-ttu-id="2022e-122">`DurationThresholdInMS` — duração refere-se ao tempo levado para carregar a página.</span><span class="sxs-lookup"><span data-stu-id="2022e-122">`DurationThresholdInMS` - Duration refers to the time taken to load the page.</span></span> <span data-ttu-id="2022e-123">Se for definida, as páginas que são carregadas mais rapidamente que o tempo definido não serão apontadas.</span><span class="sxs-lookup"><span data-stu-id="2022e-123">If this is set, pages that loaded faster than this time are not reported.</span></span>
* <span data-ttu-id="2022e-124">`NotNeededNames` — lista de nomes de página separados por vírgula.</span><span class="sxs-lookup"><span data-stu-id="2022e-124">`NotNeededNames` - Comma-separated list of page names.</span></span>
* <span data-ttu-id="2022e-125">`NotNeededUrls` — lista de fragmento de URL separados por vírgula.</span><span class="sxs-lookup"><span data-stu-id="2022e-125">`NotNeededUrls` - Comma-separated list of URL fragments.</span></span> <span data-ttu-id="2022e-126">Por exemplo, `"home"` filtra todas as páginas que têm "início" na URL.</span><span class="sxs-lookup"><span data-stu-id="2022e-126">For example, `"home"` filters out all pages that have "home" in the URL.</span></span>


### <a name="request-telemetry-filter"></a><span data-ttu-id="2022e-127">Filtro de telemetria da solicitação</span><span class="sxs-lookup"><span data-stu-id="2022e-127">Request Telemetry Filter</span></span>


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a><span data-ttu-id="2022e-128">Filtro de fonte sintética</span><span class="sxs-lookup"><span data-stu-id="2022e-128">Synthetic Source filter</span></span>

<span data-ttu-id="2022e-129">Filtra toda a telemetria que têm valores na propriedade SyntheticSource.</span><span class="sxs-lookup"><span data-stu-id="2022e-129">Filters out all telemetry that have values in the SyntheticSource property.</span></span> <span data-ttu-id="2022e-130">Isso inclui solicitações de bots, rastreadores e testes de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="2022e-130">These include requests from bots, spiders and availability tests.</span></span>

<span data-ttu-id="2022e-131">Filtre a telemetria para todas as solicitações sintéticas:</span><span class="sxs-lookup"><span data-stu-id="2022e-131">Filter out telemetry for all synthetic requests:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" />
```

<span data-ttu-id="2022e-132">Filtre a telemetria para fontes sintéticas específicas:</span><span class="sxs-lookup"><span data-stu-id="2022e-132">Filter out telemetry for specific synthetic sources:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* <span data-ttu-id="2022e-133">`NotNeeded` — lista de nomes de fonte sintética separados por vírgula.</span><span class="sxs-lookup"><span data-stu-id="2022e-133">`NotNeeded` - Comma-separated list of synthetic source names.</span></span>

### <a name="telemetry-event-filter"></a><span data-ttu-id="2022e-134">Filtro de eventos de telemetria</span><span class="sxs-lookup"><span data-stu-id="2022e-134">Telemetry Event filter</span></span>

<span data-ttu-id="2022e-135">Filtra eventos personalizados (registrados usando [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span><span class="sxs-lookup"><span data-stu-id="2022e-135">Filters custom events (logged using [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span></span>


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* <span data-ttu-id="2022e-136">`NotNeededNames` — lista de nomes de eventos separados por vírgula.</span><span class="sxs-lookup"><span data-stu-id="2022e-136">`NotNeededNames` - Comma-separated list of event names.</span></span>


### <a name="trace-telemetry-filter"></a><span data-ttu-id="2022e-137">Filtro de telemetria de rastreamento</span><span class="sxs-lookup"><span data-stu-id="2022e-137">Trace Telemetry filter</span></span>

<span data-ttu-id="2022e-138">Filtra rastreamentos de log (registrados usando [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) ou um [coletor de estrutura de registros](app-insights-java-trace-logs.md)).</span><span class="sxs-lookup"><span data-stu-id="2022e-138">Filters log traces (logged using [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) or a [logging framework collector](app-insights-java-trace-logs.md)).</span></span>

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* <span data-ttu-id="2022e-139">Os valores válidos de `FromSeverityLevel`são:</span><span class="sxs-lookup"><span data-stu-id="2022e-139">`FromSeverityLevel` valid values are:</span></span>
 *  <span data-ttu-id="2022e-140">DESATIVADO             — filtrar TODOS os rastreamentos</span><span class="sxs-lookup"><span data-stu-id="2022e-140">OFF             - Filter out ALL traces</span></span>
 *  <span data-ttu-id="2022e-141">RASTREAMENTO           — sem filtragem.</span><span class="sxs-lookup"><span data-stu-id="2022e-141">TRACE           - No filtering.</span></span> <span data-ttu-id="2022e-142">igual a Nível de rastreamento</span><span class="sxs-lookup"><span data-stu-id="2022e-142">equals to Trace level</span></span>
 *  <span data-ttu-id="2022e-143">INFORMAÇÕES            — filtrar nível de RASTREAMENTO</span><span class="sxs-lookup"><span data-stu-id="2022e-143">INFO            - Filter out TRACE level</span></span>
 *  <span data-ttu-id="2022e-144">AVISO            — filtrar RASTREAMENTO e INFORMAÇÕES</span><span class="sxs-lookup"><span data-stu-id="2022e-144">WARN            - Filter out TRACE and INFO</span></span>
 *  <span data-ttu-id="2022e-145">ERRO           — filtrar AVISO, INFORMAÇÕES, RASTREAMENTO</span><span class="sxs-lookup"><span data-stu-id="2022e-145">ERROR           - Filter out WARN, INFO, TRACE</span></span>
 *  <span data-ttu-id="2022e-146">CRÍTICO        — filtrar todos, menos CRÍTICO</span><span class="sxs-lookup"><span data-stu-id="2022e-146">CRITICAL        - filter out all but CRITICAL</span></span>


## <a name="custom-filters"></a><span data-ttu-id="2022e-147">Filtros personalizados</span><span class="sxs-lookup"><span data-stu-id="2022e-147">Custom filters</span></span>

### <a name="1-code-your-filter"></a><span data-ttu-id="2022e-148">1. Codificar seu filtro</span><span class="sxs-lookup"><span data-stu-id="2022e-148">1. Code your filter</span></span>

<span data-ttu-id="2022e-149">No seu código, crie uma classe que implementa `TelemetryProcessor`:</span><span class="sxs-lookup"><span data-stu-id="2022e-149">In your code, create a class that implements `TelemetryProcessor`:</span></span>

```Java

    package com.fabrikam.MyFilter;
    import com.microsoft.applicationinsights.extensibility.TelemetryProcessor;
    import com.microsoft.applicationinsights.telemetry.Telemetry;

    public class SuccessFilter implements TelemetryProcessor {

       /* Any parameters that are required to support the filter.*/
       private final String successful;

       /* Initializers for the parameters, named "setParameterName" */
       public void setNotNeeded(String successful)
       {
          this.successful = successful;
       }

       /* This method is called for each item of telemetry to be sent.
          Return false to discard it.
          Return true to allow other processors to inspect it. */
       @Override
       public boolean process(Telemetry telemetry) {
        if (telemetry == null) { return true; }
        if (telemetry instanceof RequestTelemetry)
        {
            RequestTelemetry requestTelemetry = (RequestTelemetry)telemetry;
            return request.getSuccess() == successful;
        }
        return true;
       }
    }

```


### <a name="2-invoke-your-filter-in-the-configuration-file"></a><span data-ttu-id="2022e-150">2. Invocar o filtro no arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="2022e-150">2. Invoke your filter in the configuration file</span></span>

<span data-ttu-id="2022e-151">Em ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="2022e-151">In ApplicationInsights.xml:</span></span>

```XML


    <ApplicationInsights>
      <TelemetryProcessors>
        <CustomProcessors>
          <Processor type="com.fabrikam.SuccessFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>
      </TelemetryProcessors>
    </ApplicationInsights>

```

## <a name="troubleshooting"></a><span data-ttu-id="2022e-152">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="2022e-152">Troubleshooting</span></span>

<span data-ttu-id="2022e-153">*Meu filtro não está funcionando.*</span><span class="sxs-lookup"><span data-stu-id="2022e-153">*My filter isn't working.*</span></span>

* <span data-ttu-id="2022e-154">Verifique se você forneceu valores válidos de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="2022e-154">Check that you have provided valid parameter values.</span></span> <span data-ttu-id="2022e-155">Por exemplo, durações devem ser números inteiros.</span><span class="sxs-lookup"><span data-stu-id="2022e-155">For example, durations should be integers.</span></span> <span data-ttu-id="2022e-156">Valores inválidos farão com que o filtro seja ignorado.</span><span class="sxs-lookup"><span data-stu-id="2022e-156">Invalid values will cause the filter to be ignored.</span></span> <span data-ttu-id="2022e-157">Se seu filtro personalizado lançar uma exceção de um construtor ou método set, ele será ignorado.</span><span class="sxs-lookup"><span data-stu-id="2022e-157">If your custom filter throws an exception from a constructor or set method, it will be ignored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2022e-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2022e-158">Next steps</span></span>

* <span data-ttu-id="2022e-159">[Amostragem](app-insights-sampling.md) — considere a amostragem como uma alternativa que não distorce suas métricas.</span><span class="sxs-lookup"><span data-stu-id="2022e-159">[Sampling](app-insights-sampling.md) - Consider sampling as an alternative that does not skew your metrics.</span></span>
