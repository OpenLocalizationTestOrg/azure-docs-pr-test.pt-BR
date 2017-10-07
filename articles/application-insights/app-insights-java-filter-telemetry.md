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
# <a name="filter-telemetry-in-your-java-web-app"></a>Filtrar a telemetria no aplicativo Web Java

Filtros fornecem uma telemetria de saudação do modo tooselect seu [aplicativo web Java envia informações de tooApplication](app-insights-java-get-started.md). Existem alguns filtros prontos para uso, mas você também pode escrever seus próprios filtros personalizados.

saudação de caixa filtros incluem:

* Nível de severidade de rastreamento
* URLs específicas, palavras-chave ou códigos de resposta
* Obter respostas rápidas - ou seja, solicitações toowhich seu aplicativo respondeu tooquickly
* Nomes de eventos específicos

> [!NOTE]
> Filtros distorcer as métricas de saudação do seu aplicativo. Por exemplo, você pode decidir que, em ordem toodiagnose lentidão nas respostas, defina tempos de resposta rápidos de toodiscard um filtro. Mas você deve estar ciente de que os tempos de resposta médio Olá relatados pelo Application Insights será mais lentos do que a velocidade de true hello e contagem de saudação de solicitações será menor que a contagem real de saudação.
> Se isso for um problema, use [Amostragem](app-insights-sampling.md).

## <a name="setting-filters"></a>Definindo filtros

Em ApplicationInsights.xml, adicione uma seção `TelemetryProcessors`, como neste exemplo:


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




[Inspecione o conjunto completo de saudação de processadores internas](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).

## <a name="built-in-filters"></a>Filtros internos

### <a name="metric-telemetry-filter"></a>Filtro de telemetria da métrica

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* `NotNeeded` — lista de nomes de métricas personalizadas separados por vírgula.


### <a name="page-view-telemetry-filter"></a>Filtro de telemetria da exibição de página

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* `DurationThresholdInMS`-Duração se refere a tempo toohello página de saudação tooload. Se for definida, as páginas que são carregadas mais rapidamente que o tempo definido não serão apontadas.
* `NotNeededNames` — lista de nomes de página separados por vírgula.
* `NotNeededUrls` — lista de fragmento de URL separados por vírgula. Por exemplo, `"home"` filtra todas as páginas que têm "home" na URL de saudação.


### <a name="request-telemetry-filter"></a>Filtro de telemetria da solicitação


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a>Filtro de fonte sintética

Filtra em toda a telemetria que têm valores na propriedade SyntheticSource de saudação. Isso inclui solicitações de bots, rastreadores e testes de disponibilidade.

Filtre a telemetria para todas as solicitações sintéticas:


```XML

           <Processor type="SyntheticSourceFilter" />
```

Filtre a telemetria para fontes sintéticas específicas:


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* `NotNeeded` — lista de nomes de fonte sintética separados por vírgula.

### <a name="telemetry-event-filter"></a>Filtro de eventos de telemetria

Filtra eventos personalizados (registrados usando [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* `NotNeededNames` — lista de nomes de eventos separados por vírgula.


### <a name="trace-telemetry-filter"></a>Filtro de telemetria de rastreamento

Filtra rastreamentos de log (registrados usando [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) ou um [coletor de estrutura de registros](app-insights-java-trace-logs.md)).

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* Os valores válidos de `FromSeverityLevel`são:
 *  DESATIVADO             — filtrar TODOS os rastreamentos
 *  RASTREAMENTO           — sem filtragem. nível de tooTrace é igual a
 *  INFORMAÇÕES            — filtrar nível de RASTREAMENTO
 *  AVISO            — filtrar RASTREAMENTO e INFORMAÇÕES
 *  ERRO           — filtrar AVISO, INFORMAÇÕES, RASTREAMENTO
 *  CRÍTICO        — filtrar todos, menos CRÍTICO


## <a name="custom-filters"></a>Filtros personalizados

### <a name="1-code-your-filter"></a>1. Codificar seu filtro

No seu código, crie uma classe que implementa `TelemetryProcessor`:

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


### <a name="2-invoke-your-filter-in-hello-configuration-file"></a>2. Chamar o filtro no arquivo de configuração de saudação

Em ApplicationInsights.xml:

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

## <a name="troubleshooting"></a>Solucionar problemas

*Meu filtro não está funcionando.*

* Verifique se você forneceu valores válidos de parâmetro. Por exemplo, durações devem ser números inteiros. Valores inválidos causarão Olá filtro toobe ignorado. Se seu filtro personalizado lançar uma exceção de um construtor ou método set, ele será ignorado.

## <a name="next-steps"></a>Próximas etapas

* [Amostragem](app-insights-sampling.md) — considere a amostragem como uma alternativa que não distorce suas métricas.
