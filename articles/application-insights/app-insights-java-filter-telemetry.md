---
title: aaaFilter telemetria do Application Insights do Azure em seu aplicativo da web de Java | Microsoft Docs
description: "Reduzir o tráfego de telemetria filtrando eventos Olá toomonitor não é necessário."
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
ms.openlocfilehash: 95713e11d5f86472777c67e4e7f3177fbf2cd0b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="filter-telemetry-in-your-java-web-app"></a><span data-ttu-id="2364a-103">Filtrar a telemetria no aplicativo Web Java</span><span class="sxs-lookup"><span data-stu-id="2364a-103">Filter telemetry in your Java web app</span></span>

<span data-ttu-id="2364a-104">Filtros fornecem uma telemetria de saudação do modo tooselect seu [aplicativo web Java envia informações de tooApplication](app-insights-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2364a-104">Filters provide a way tooselect hello telemetry that your [Java web app sends tooApplication Insights](app-insights-java-get-started.md).</span></span> <span data-ttu-id="2364a-105">Existem alguns filtros prontos para uso, mas você também pode escrever seus próprios filtros personalizados.</span><span class="sxs-lookup"><span data-stu-id="2364a-105">There are some out-of-the-box filters that you can use, and you can also write your own custom filters.</span></span>

<span data-ttu-id="2364a-106">saudação de caixa filtros incluem:</span><span class="sxs-lookup"><span data-stu-id="2364a-106">hello out-of-the-box filters include:</span></span>

* <span data-ttu-id="2364a-107">Nível de severidade de rastreamento</span><span class="sxs-lookup"><span data-stu-id="2364a-107">Trace severity level</span></span>
* <span data-ttu-id="2364a-108">URLs específicas, palavras-chave ou códigos de resposta</span><span class="sxs-lookup"><span data-stu-id="2364a-108">Specific URLs, keywords or response codes</span></span>
* <span data-ttu-id="2364a-109">Obter respostas rápidas - ou seja, solicitações toowhich seu aplicativo respondeu tooquickly</span><span class="sxs-lookup"><span data-stu-id="2364a-109">Fast responses - that is, requests toowhich your app responded tooquickly</span></span>
* <span data-ttu-id="2364a-110">Nomes de eventos específicos</span><span class="sxs-lookup"><span data-stu-id="2364a-110">Specific event names</span></span>

> [!NOTE]
> <span data-ttu-id="2364a-111">Filtros distorcer as métricas de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2364a-111">Filters skew hello metrics of your app.</span></span> <span data-ttu-id="2364a-112">Por exemplo, você pode decidir que, em ordem toodiagnose lentidão nas respostas, defina tempos de resposta rápidos de toodiscard um filtro.</span><span class="sxs-lookup"><span data-stu-id="2364a-112">For example, you might decide that, in order toodiagnose slow responses, you will set a filter toodiscard fast response times.</span></span> <span data-ttu-id="2364a-113">Mas você deve estar ciente de que os tempos de resposta médio Olá relatados pelo Application Insights será mais lentos do que a velocidade de true hello e contagem de saudação de solicitações será menor que a contagem real de saudação.</span><span class="sxs-lookup"><span data-stu-id="2364a-113">But you must be aware that hello average response times reported by Application Insights will then be slower than hello true speed, and hello count of requests will be smaller than hello real count.</span></span>
> <span data-ttu-id="2364a-114">Se isso for um problema, use [Amostragem](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="2364a-114">If this is a concern, use [Sampling](app-insights-sampling.md) instead.</span></span>

## <a name="setting-filters"></a><span data-ttu-id="2364a-115">Definindo filtros</span><span class="sxs-lookup"><span data-stu-id="2364a-115">Setting filters</span></span>

<span data-ttu-id="2364a-116">Em ApplicationInsights.xml, adicione uma seção `TelemetryProcessors`, como neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="2364a-116">In ApplicationInsights.xml, add a `TelemetryProcessors` section like this example:</span></span>


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
                  <!-- Names of events we don't want toosee -->
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




<span data-ttu-id="2364a-117">[Inspecione o conjunto completo de saudação de processadores internas](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span><span class="sxs-lookup"><span data-stu-id="2364a-117">[Inspect hello full set of built-in processors](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span></span>

## <a name="built-in-filters"></a><span data-ttu-id="2364a-118">Filtros internos</span><span class="sxs-lookup"><span data-stu-id="2364a-118">Built-in filters</span></span>

### <a name="metric-telemetry-filter"></a><span data-ttu-id="2364a-119">Filtro de telemetria da métrica</span><span class="sxs-lookup"><span data-stu-id="2364a-119">Metric Telemetry filter</span></span>

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* <span data-ttu-id="2364a-120">`NotNeeded` — lista de nomes de métricas personalizadas separados por vírgula.</span><span class="sxs-lookup"><span data-stu-id="2364a-120">`NotNeeded` - Comma-separated list of custom metric names.</span></span>


### <a name="page-view-telemetry-filter"></a><span data-ttu-id="2364a-121">Filtro de telemetria da exibição de página</span><span class="sxs-lookup"><span data-stu-id="2364a-121">Page View Telemetry filter</span></span>

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* <span data-ttu-id="2364a-122">`DurationThresholdInMS`-Duração se refere a tempo toohello página de saudação tooload.</span><span class="sxs-lookup"><span data-stu-id="2364a-122">`DurationThresholdInMS` - Duration refers toohello time taken tooload hello page.</span></span> <span data-ttu-id="2364a-123">Se for definida, as páginas que são carregadas mais rapidamente que o tempo definido não serão apontadas.</span><span class="sxs-lookup"><span data-stu-id="2364a-123">If this is set, pages that loaded faster than this time are not reported.</span></span>
* <span data-ttu-id="2364a-124">`NotNeededNames` — lista de nomes de página separados por vírgula.</span><span class="sxs-lookup"><span data-stu-id="2364a-124">`NotNeededNames` - Comma-separated list of page names.</span></span>
* <span data-ttu-id="2364a-125">`NotNeededUrls` — lista de fragmento de URL separados por vírgula.</span><span class="sxs-lookup"><span data-stu-id="2364a-125">`NotNeededUrls` - Comma-separated list of URL fragments.</span></span> <span data-ttu-id="2364a-126">Por exemplo, `"home"` filtra todas as páginas que têm "home" na URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="2364a-126">For example, `"home"` filters out all pages that have "home" in hello URL.</span></span>


### <a name="request-telemetry-filter"></a><span data-ttu-id="2364a-127">Filtro de telemetria da solicitação</span><span class="sxs-lookup"><span data-stu-id="2364a-127">Request Telemetry Filter</span></span>


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a><span data-ttu-id="2364a-128">Filtro de fonte sintética</span><span class="sxs-lookup"><span data-stu-id="2364a-128">Synthetic Source filter</span></span>

<span data-ttu-id="2364a-129">Filtra em toda a telemetria que têm valores na propriedade SyntheticSource de saudação.</span><span class="sxs-lookup"><span data-stu-id="2364a-129">Filters out all telemetry that have values in hello SyntheticSource property.</span></span> <span data-ttu-id="2364a-130">Isso inclui solicitações de bots, rastreadores e testes de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="2364a-130">These include requests from bots, spiders and availability tests.</span></span>

<span data-ttu-id="2364a-131">Filtre a telemetria para todas as solicitações sintéticas:</span><span class="sxs-lookup"><span data-stu-id="2364a-131">Filter out telemetry for all synthetic requests:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" />
```

<span data-ttu-id="2364a-132">Filtre a telemetria para fontes sintéticas específicas:</span><span class="sxs-lookup"><span data-stu-id="2364a-132">Filter out telemetry for specific synthetic sources:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* <span data-ttu-id="2364a-133">`NotNeeded` — lista de nomes de fonte sintética separados por vírgula.</span><span class="sxs-lookup"><span data-stu-id="2364a-133">`NotNeeded` - Comma-separated list of synthetic source names.</span></span>

### <a name="telemetry-event-filter"></a><span data-ttu-id="2364a-134">Filtro de eventos de telemetria</span><span class="sxs-lookup"><span data-stu-id="2364a-134">Telemetry Event filter</span></span>

<span data-ttu-id="2364a-135">Filtra eventos personalizados (registrados usando [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span><span class="sxs-lookup"><span data-stu-id="2364a-135">Filters custom events (logged using [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span></span>


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* <span data-ttu-id="2364a-136">`NotNeededNames` — lista de nomes de eventos separados por vírgula.</span><span class="sxs-lookup"><span data-stu-id="2364a-136">`NotNeededNames` - Comma-separated list of event names.</span></span>


### <a name="trace-telemetry-filter"></a><span data-ttu-id="2364a-137">Filtro de telemetria de rastreamento</span><span class="sxs-lookup"><span data-stu-id="2364a-137">Trace Telemetry filter</span></span>

<span data-ttu-id="2364a-138">Filtra rastreamentos de log (registrados usando [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) ou um [coletor de estrutura de registros](app-insights-java-trace-logs.md)).</span><span class="sxs-lookup"><span data-stu-id="2364a-138">Filters log traces (logged using [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) or a [logging framework collector](app-insights-java-trace-logs.md)).</span></span>

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* <span data-ttu-id="2364a-139">Os valores válidos de `FromSeverityLevel`são:</span><span class="sxs-lookup"><span data-stu-id="2364a-139">`FromSeverityLevel` valid values are:</span></span>
 *  <span data-ttu-id="2364a-140">DESATIVADO             — filtrar TODOS os rastreamentos</span><span class="sxs-lookup"><span data-stu-id="2364a-140">OFF             - Filter out ALL traces</span></span>
 *  <span data-ttu-id="2364a-141">RASTREAMENTO           — sem filtragem.</span><span class="sxs-lookup"><span data-stu-id="2364a-141">TRACE           - No filtering.</span></span> <span data-ttu-id="2364a-142">nível de tooTrace é igual a</span><span class="sxs-lookup"><span data-stu-id="2364a-142">equals tooTrace level</span></span>
 *  <span data-ttu-id="2364a-143">INFORMAÇÕES            — filtrar nível de RASTREAMENTO</span><span class="sxs-lookup"><span data-stu-id="2364a-143">INFO            - Filter out TRACE level</span></span>
 *  <span data-ttu-id="2364a-144">AVISO            — filtrar RASTREAMENTO e INFORMAÇÕES</span><span class="sxs-lookup"><span data-stu-id="2364a-144">WARN            - Filter out TRACE and INFO</span></span>
 *  <span data-ttu-id="2364a-145">ERRO           — filtrar AVISO, INFORMAÇÕES, RASTREAMENTO</span><span class="sxs-lookup"><span data-stu-id="2364a-145">ERROR           - Filter out WARN, INFO, TRACE</span></span>
 *  <span data-ttu-id="2364a-146">CRÍTICO        — filtrar todos, menos CRÍTICO</span><span class="sxs-lookup"><span data-stu-id="2364a-146">CRITICAL        - filter out all but CRITICAL</span></span>


## <a name="custom-filters"></a><span data-ttu-id="2364a-147">Filtros personalizados</span><span class="sxs-lookup"><span data-stu-id="2364a-147">Custom filters</span></span>

### <a name="1-code-your-filter"></a><span data-ttu-id="2364a-148">1. Codificar seu filtro</span><span class="sxs-lookup"><span data-stu-id="2364a-148">1. Code your filter</span></span>

<span data-ttu-id="2364a-149">No seu código, crie uma classe que implementa `TelemetryProcessor`:</span><span class="sxs-lookup"><span data-stu-id="2364a-149">In your code, create a class that implements `TelemetryProcessor`:</span></span>

```Java

    package com.fabrikam.MyFilter;
    import com.microsoft.applicationinsights.extensibility.TelemetryProcessor;
    import com.microsoft.applicationinsights.telemetry.Telemetry;

    public class SuccessFilter implements TelemetryProcessor {

       /* Any parameters that are required toosupport hello filter.*/
       private final String successful;

       /* Initializers for hello parameters, named "setParameterName" */
       public void setNotNeeded(String successful)
       {
          this.successful = successful;
       }

       /* This method is called for each item of telemetry toobe sent.
          Return false toodiscard it.
          Return true tooallow other processors tooinspect it. */
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


### <a name="2-invoke-your-filter-in-hello-configuration-file"></a><span data-ttu-id="2364a-150">2. Chamar o filtro no arquivo de configuração de saudação</span><span class="sxs-lookup"><span data-stu-id="2364a-150">2. Invoke your filter in hello configuration file</span></span>

<span data-ttu-id="2364a-151">Em ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="2364a-151">In ApplicationInsights.xml:</span></span>

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

## <a name="troubleshooting"></a><span data-ttu-id="2364a-152">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="2364a-152">Troubleshooting</span></span>

<span data-ttu-id="2364a-153">*Meu filtro não está funcionando.*</span><span class="sxs-lookup"><span data-stu-id="2364a-153">*My filter isn't working.*</span></span>

* <span data-ttu-id="2364a-154">Verifique se você forneceu valores válidos de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="2364a-154">Check that you have provided valid parameter values.</span></span> <span data-ttu-id="2364a-155">Por exemplo, durações devem ser números inteiros.</span><span class="sxs-lookup"><span data-stu-id="2364a-155">For example, durations should be integers.</span></span> <span data-ttu-id="2364a-156">Valores inválidos causarão Olá filtro toobe ignorado.</span><span class="sxs-lookup"><span data-stu-id="2364a-156">Invalid values will cause hello filter toobe ignored.</span></span> <span data-ttu-id="2364a-157">Se seu filtro personalizado lançar uma exceção de um construtor ou método set, ele será ignorado.</span><span class="sxs-lookup"><span data-stu-id="2364a-157">If your custom filter throws an exception from a constructor or set method, it will be ignored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2364a-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2364a-158">Next steps</span></span>

* <span data-ttu-id="2364a-159">[Amostragem](app-insights-sampling.md) — considere a amostragem como uma alternativa que não distorce suas métricas.</span><span class="sxs-lookup"><span data-stu-id="2364a-159">[Sampling](app-insights-sampling.md) - Consider sampling as an alternative that does not skew your metrics.</span></span>
