---
title: aaaAzure modelo de dados do Application Insights | Microsoft Docs
description: "Descreve as propriedades exportadas de exportação contínua em JSON e usados como filtros."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: cabad41c-0518-4669-887f-3087aef865ea
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: bwren
ms.openlocfilehash: 5ff3ce7953b91cc69b5d96c0ea9b6d58a6016e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-export-data-model"></a>Modelo de dados de exportação do Application Insights
Esta tabela lista as propriedades de saudação de telemetria enviada do hello [Application Insights](app-insights-overview.md) SDKs toohello portal.
Você verá essas propriedades na saída de dados de [Exportação Contínua](app-insights-export-telemetry.md).
Elas também aparecerão nos filtros da propriedade no [Explorador de Métrica](app-insights-metrics-explorer.md) e na [Pesquisa de Diagnóstico](app-insights-diagnostic-search.md).

Toonote pontos:

* `[0]`nessas tabelas denota um ponto no caminho de saudação onde você tenha tooinsert um índice. mas nem sempre é 0.
* A duração é em décimos de microssegundo, portanto, 10000000 = = 1 segundo.
* Datas e horas são UTC e são fornecidas no formato ISO de saudação`yyyy-MM-DDThh:mm:ss.sssZ`


## <a name="example"></a>Exemplo
    // A server report about an HTTP request
    {
    "request": [
      {
        "urlData": { // derived from 'url'
          "host": "contoso.org",
          "base": "/",
          "hashTag": ""
        },
        "responseCode": 200, // Sent tooclient
        "success": true, // Default == responseCode<400
        // Request id becomes hello operation id of child events
        "id": "fCOhCdCnZ9I=",  
        "name": "GET Home/Index",
        "count": 1, // 100% / sampling rate
        "durationMetric": {
          "value": 1046804.0, // 10000000 == 1 second
          // Currently hello following fields are redundant:
          "count": 1.0,
          "min": 1046804.0,
          "max": 1046804.0,
          "stdDev": 0.0,
          "sampledValue": 1046804.0
        },
        "url": "/"
      }
    ],
    "internal": {
      "data": {
        "id": "7f156650-ef4c-11e5-8453-3f984b167d05",
        "documentVersion": "1.61"
      }
    },
    "context": {
      "device": { // client browser
        "type": "PC",
        "screenResolution": { },
        "roleInstance": "WFWEB14B.fabrikam.net"
      },
      "application": { },
      "location": { // derived from client ip
        "continent": "North America",
        "country": "United States",
        // last octagon is anonymized too0 at portal:
        "clientip": "168.62.177.0",
        "province": "",
        "city": ""
      },
      "data": {
        "isSynthetic": true, // we identified source as a bot
        // percentage of generated data sent tooportal:
        "samplingRate": 100.0,
        "eventTime": "2016-03-21T10:05:45.7334717Z" // UTC
      },
      "user": {
        "isAuthenticated": false,
        "anonId": "us-tx-sn1-azr", // bot agent id
        "anonAcquisitionDate": "0001-01-01T00:00:00Z",
        "authAcquisitionDate": "0001-01-01T00:00:00Z",
        "accountAcquisitionDate": "0001-01-01T00:00:00Z"
      },
      "operation": {
        "id": "fCOhCdCnZ9I=",
        "parentId": "fCOhCdCnZ9I=",
        "name": "GET Home/Index"
      },
      "cloud": { },
      "serverDevice": { },
      "custom": { // set by custom fields of track calls
        "dimensions": [ ],
        "metrics": [ ]
      },
      "session": {
        "id": "65504c10-44a6-489e-b9dc-94184eb00d86",
        "isFirst": true
      }
    }
  }

## <a name="context"></a>Contexto
Todos os tipos de telemetria são acompanhados por uma seção de contexto. Nem todos esses campos são transmitidos com cada ponto de dados.

| Caminho | Tipo | Observações |
| --- | --- | --- |
| context.custom.dimensions [0] |object [ ] |Pares de cadeira de caractere chave-valor definidos pelo parâmetro das propriedades personalizadas. Comprimento máximo da chave 100, comprimento máximo dos valores 1024. Mais de 100 valores exclusivos, propriedade Olá pode ser pesquisada, mas não pode ser usada para a segmentação. Máximo de 200 chaves por ikey. |
| context.custom.metrics [0] |object [ ] |Pares de chave-valor definidos pelo parâmetro de medidas personalizadas e por TrackMetrics. Comprimento máximo da chave 100, os valores podem ser numéricos. |
| context.data.eventTime |string |UTC |
| context.data.isSynthetic |Booliano |Solicitação aparece toocome de um teste da web ou de bot. |
| context.data.samplingRate |número |Porcentagem de telemetria gerada por Olá SDK enviada tooportal. Intervalo 0.0-100.0. |
| context.device |objeto |Dispositivo de cliente |
| context.device.browser |string |IE, Chrome, ... |
| context.device.browserVersion |string |Chrome 48.0, ... |
| context.device.deviceModel |string | |
| context.device.deviceName |string | |
| context.device.id |string | |
| context.device.locale |string |en-GB, de-DE, ... |
| context.device.network |string | |
| context.device.oemName |string | |
| context.device.osVersion |string |SO host |
| context.device.roleInstance |string |ID do host do servidor |
| context.device.roleName |string | |
| context.device.type |string |PC, navegador,... |
| context.location |objeto |Derivado de clientip. |
| context.location.city |string |Derivado de clientip, se conhecido |
| context.location.clientip |string |Última octógono é too0 anônimos. |
| context.location.continent |string | |
| context.location.country |string | |
| context.location.province |string |Estado ou província |
| context.operation.id |string |Itens que têm Olá a mesma id de operação são mostrados como itens relacionados no portal de saudação. Geralmente Olá id da solicitação. |
| context.operation.name |string |nome solicitação ou url |
| context.operation.parentId |string |Permite itens relacionados aninhados. |
| context.session.id |string |ID de um grupo de operações de saudação de mesma origem. Um período de 30 minutos sem uma operação sinaliza o término de saudação de uma sessão. |
| context.session.isFirst |booleano | |
| context.user.accountAcquisitionDate |string | |
| context.user.anonAcquisitionDate |string | |
| context.user.anonId |string | |
| context.user.authAcquisitionDate |string |[Usuário autenticado](app-insights-api-custom-events-metrics.md#authenticated-users) |
| context.user.isAuthenticated |booleano | |
| internal.data.documentVersion |string | |
| internal.data.id |string | |

## <a name="events"></a>Eventos
Eventos personalizados gerados por [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).

| Caminho | Tipo | Observações |
| --- | --- | --- |
| event [0] count |inteiro |100/(taxa de[amostragem](app-insights-sampling.md) ). Por exemplo, 4 =&gt; 25%. |
| event [0] name |string |Nome do evento.  Comprimento máximo 250. |
| event [0] url |string | |
| event [0] urlData.base |string | |
| event [0] urlData.host |string | |

## <a name="exceptions"></a>Exceções
Relatórios [exceções](app-insights-asp-net-exceptions.md) no servidor de saudação e no navegador de saudação.

| Caminho | Tipo | Observações |
| --- | --- | --- |
| basicException [0] assembly |string | |
| basicException [0] count |inteiro |100/(taxa de[amostragem](app-insights-sampling.md) ). Por exemplo, 4 =&gt; 25%. |
| basicException [0] exceptionGroup |string | |
| basicException [0] exceptionType |string | |
| basicException [0] failedUserCodeMethod |string | |
| basicException [0] failedUserCodeAssembly |string | |
| basicException [0] handledAt |string | |
| basicException [0] hasFullStack |booleano | |
| basicException [0] id |string | |
| basicException [0] method |string | |
| basicException [0] message |string |Mensagem de exceção. Comprimento máximo 10k. |
| basicException [0] outerExceptionMessage |string | |
| basicException [0] outerExceptionThrownAtAssembly |string | |
| basicException [0] outerExceptionThrownAtMethod |string | |
| basicException [0] outerExceptionType |string | |
| basicException [0] outerId |string | |
| basicException [0] parsedStack [0] assembly |string | |
| basicException [0] parsedStack [0] fileName |string | |
| basicException [0] parsedStack [0] level |inteiro | |
| basicException [0] parsedStack [0] line |inteiro | |
| basicException [0] parsedStack [0] method |string | |
| basicException [0] stack |string |Comprimento máximo 10k |
| basicException [0] typeName |string | |

## <a name="trace-messages"></a>Mensagens de rastreamento
Enviado por [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace)e por Olá [log adaptadores](app-insights-asp-net-trace-logs.md).

| Caminho | Tipo | Observações |
| --- | --- | --- |
| message [0] loggerName |string | |
| message [0] parameters |string | |
| message [0] raw |string |mensagem de log Hello, comprimento máximo 10k. |
| message [0] severityLevel |string | |

## <a name="remote-dependency"></a>Dependência remota
Enviado por TrackDependency. Usado tooreport desempenho e o uso de [chama toodependencies](app-insights-asp-net-dependencies.md) no servidor de saudação e chamadas AJAX no navegador de saudação.

| Caminho | Tipo | Observações |
| --- | --- | --- |
| remoteDependency [0] async |booleano | |
| remoteDependency [0] baseName |string | |
| remoteDependency [0] commandName |string |Por exemplo, "home/index" |
| remoteDependency [0] count |inteiro |100/(taxa de[amostragem](app-insights-sampling.md) ). Por exemplo, 4 =&gt; 25%. |
| remoteDependency [0] dependencyTypeName |string |HTTP, SQL, ... |
| remoteDependency [0] durationMetric.value |número |Hora da chamada toocompletion de resposta de dependência |
| remoteDependency [0] id |string | |
| remoteDependency [0] name |string |Url. Comprimento máximo 250. |
| remoteDependency [0] resultCode |string |da dependência de HTTP |
| remoteDependency [0] success |booleano | |
| remoteDependency [0] type |string |Http, Sql,... |
| remoteDependency [0] url |string |Comprimento máximo 2000 |
| remoteDependency [0] urlData.base |string |Comprimento máximo 2000 |
| remoteDependency [0] urlData.hashTag |string | |
| remoteDependency [0] urlData.host |string |Comprimento máximo 200 |

## <a name="requests"></a>Solicitações
Enviado por [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest). módulos padrão Olá usam esse tempo de resposta do servidor tooreports, medido no servidor de saudação.

| Caminho | Tipo | Observações |
| --- | --- | --- |
| request [0] count |inteiro |100/(taxa de[amostragem](app-insights-sampling.md) ). Por exemplo: 4 =&gt; 25%. |
| request [0] durationMetric.value |número |Tempo de tooresponse que chegam de solicitação. 1e7 == 1s |
| request [0] id |string |ID da operação |
| request [0] name |string |GET/POST + url base.  Comprimento máximo 250 |
| request [0] responseCode |inteiro |Tooclient de resposta enviada de HTTP |
| request [0] success |booleano |Padrão == (responseCode &lt; 400) |
| request [0] url |string |Não incluindo o host |
| request [0] urlData.base |string | |
| request [0] urlData.hashTag |string | |
| request [0] urlData.host |string | |

## <a name="page-view-performance"></a>Desempenho de exibição da página
Enviado pelo navegador hello. Medidas Olá tempo tooprocess uma página, de usuário iniciante Olá solicitação toodisplay concluída (excluindo as chamadas de AJAX assíncronas).

Os valores de contexto mostram a versão do navegador e do sistema operacional cliente.

| Caminho | Tipo | Observações |
| --- | --- | --- |
| clientPerformance [0] clientProcess.value |inteiro |Hora de término da página de Olá Olá HTML toodisplaying de recebimento. |
| clientPerformance [0] name |string | |
| clientPerformance [0] networkConnection.value |inteiro |Tempo gasto tooestablish uma conexão de rede. |
| clientPerformance [0] receiveRequest.value |inteiro |Hora de término de envio Olá tooreceiving da solicitação Olá HTML na resposta. |
| clientPerformance [0] sendRequest.value |inteiro |Hora da solicitação HTTP de saudação toosend obtido. |
| clientPerformance [0] total.value |inteiro |Tempo de toosend Olá solicitação toodisplaying Olá página inicial. |
| clientPerformance [0] url |string |URL dessa solicitação |
| clientPerformance [0] urlData.base |string | |
| clientPerformance [0] urlData.hashTag |string | |
| clientPerformance [0] urlData.host |string | |
| clientPerformance [0] urlData.protocol |string | |

## <a name="page-views"></a>Visualizações de página
Enviado por trackPageView() ou [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)

| Caminho | Tipo | Observações |
| --- | --- | --- |
| view [0] count |inteiro |100/(taxa de[amostragem](app-insights-sampling.md) ). Por exemplo, 4 =&gt; 25%. |
| view [0] durationMetric.value |inteiro |Valor definido opcionalmente em trackPageView() ou por startTrackPage() - stopTrackPage(). Olá mesmo não como valores de nodesempenho do cliente. |
| view [0] name |string |Título da página.  Comprimento máximo 250 |
| view [0] url |string | |
| view [0] urlData.base |string | |
| view [0] urlData.hashTag |string | |
| view [0] urlData.host |string | |

## <a name="availability"></a>Disponibilidade
Relata os [testes de disponibilidade na Web](app-insights-monitor-web-app-availability.md).

| Caminho | Tipo | Observações |
| --- | --- | --- |
| availability [0] availabilityMetric.name |string |Disponibilidade |
| availability [0] availabilityMetric.value |número |1.0 ou 0.0 |
| availability [0] count |inteiro |100/(taxa de[amostragem](app-insights-sampling.md) ). Por exemplo, 4 =&gt; 25%. |
| availability [0] dataSizeMetric.name |string | |
| availability [0] dataSizeMetric.value |inteiro | |
| availability [0] durationMetric.name |string | |
| availability [0] durationMetric.value |número |Duração do teste. 1e7==1s |
| availability [0] message |string |Diagnóstico de falha |
| availability [0] result |string |Aprovado/Reprovado |
| availability [0] runLocation |string |Fonte geográfica de solicitações http |
| availability [0] testName |string | |
| availability [0] testRunId |string | |
| availability [0] testTimestamp |string | |

## <a name="metrics"></a>Métricas
Gerado por TrackMetric().

o valor de métrica Olá é encontrado no context.custom.metrics[0]

Por exemplo:

    {
     "metric": [ ],
     "context": {
     ...
     "custom": {
        "dimensions": [
          { "ProcessId": "4068" }
        ],
        "metrics": [
          {
            "dispatchRate": {
              "value": 0.001295,
              "count": 1.0,
              "min": 0.001295,
              "max": 0.001295,
              "stdDev": 0.0,
              "sampledValue": 0.001295,
              "sum": 0.001295
            }
          }
         } ] }
    }

## <a name="about-metric-values"></a>Sobre valores de métricas
Valores de métricas, tanto em relatórios de métrica quanto em outros locais, são relatados com uma estrutura de objeto padrão. Por exemplo:

      "durationMetric": {
        "name": "contoso.org",
        "type": "Aggregation",
        "value": 468.71603053650279,
        "count": 1.0,
        "min": 468.71603053650279,
        "max": 468.71603053650279,
        "stdDev": 0.0,
        "sampledValue": 468.71603053650279
      }

No momento - Embora isso pode ser alterado em Olá futura - em todos os valores relatados de módulos SDK padrão hello, `count==1` e apenas Olá `name` e `value` os campos são úteis. Olá único caso em que eles seriam diferentes seria se você escrever seus próprio chamadas TrackMetric na qual você define Olá outros parâmetros.

Olá finalidade da saudação outros campos é tooallow métricas toobe Olá SDK, portal de toohello tooreduce tráfego agregado. Por exemplo, você pode realizar várias leituras sucessivas antes de enviar cada relatório de métricas. Você deve calcular Olá min, max, desvio padrão e valor de agregação (soma ou média) e definir contagem toohello número de leituras representado pelo relatório de saudação.

Nas tabelas de saudação acima, podemos ter omitido Olá campos usados raramente count, min, max, stdDev e sampledValue.

Em vez de pré-agregar métricas, você pode usar [amostragem](app-insights-sampling.md) se precisar de volume de saudação tooreduce de telemetria.

### <a name="durations"></a>Durações
Exceto quando indicado o contrário, as durações são representadas em décimos de microssegundo, de modo que 10000000.0 significa 1 segundo.

## <a name="see-also"></a>Consulte também
* [Application Insights](app-insights-overview.md)
* [Exportação Contínua](app-insights-export-telemetry.md)
* [Exemplos de código](app-insights-export-telemetry.md#code-samples)
