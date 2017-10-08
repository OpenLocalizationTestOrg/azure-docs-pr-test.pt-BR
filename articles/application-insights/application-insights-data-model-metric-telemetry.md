---
title: "aaaAzure modelo de dados de telemetria do Application Insights - telemetria de métrica | Microsoft Docs"
description: "Modelo de dados do Application Insights para telemetria de métricas"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 005e218a8451007458185f1e457a20cee93fa630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a>Telemetria de métricas: modelo de dados do Application Insights

Há dois tipos de telemetria de métricas com suporte do [Application Insights](app-insights-overview.md): medida única e métrica agregada previamente. A medida única é apenas um nome e valor. Métrica agregada previamente Especifica o valor mínimo e máximo da métrica de saudação no intervalo de agregação de saudação e desvio padrão dele.

A telemetria de métrica agregada previamente supõe que esse período de agregação foi de um minuto.

Há vários nomes de métrica conhecidos com suporte do Application Insights. 

Métrica representando os contadores de processo e de sistema:

| **Nome do .NET**             | **Nome independente de plataforma** | **Nome da API REST** | **Descrição**
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | Trabalho em andamento... | [processorCpuPercentage](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | total de CPU do computador
| `\Memory\Available Bytes`                 | Trabalho em andamento... | [memoryAvailableBytes](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | memória disponível em disco
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | Trabalho em andamento... | [processCpuPercentage](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | CPU do processo de saudação hospedando o aplicativo hello
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | Trabalho em andamento... | [processPrivateBytes](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | memória usada pelo processo de saudação hospedando o aplicativo hello
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | Trabalho em andamento... | [processIOBytesPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | taxa de operações de e/s é executado pelo processo que hospeda o aplicativo hello
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | Trabalho em andamento... | [requestsPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | taxa de solicitações processadas por aplicativo 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | Trabalho em andamento... | [exceptionsPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | taxa de exceções geradas por aplicativo
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | Trabalho em andamento... | [requestExecutionTime](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | tempo médio de execução de solicitações
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | Trabalho em andamento... | [requestsInQueue](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | número de solicitações aguardando em uma fila de processamento de saudação

## <a name="name"></a>Nome

Nome da métrica Olá você gostaria que toosee no portal do Application Insights e interface do usuário. 

## <a name="value"></a>Valor

Valor único para medida. Soma de medidas individuais para agregação de saudação.

## <a name="count"></a>Contagem

Peso da métrica de métrica Olá agregado. Não deve ser definido para uma medida.

## <a name="min"></a>Min

Valor mínimo da métrica Olá agregado. Não deve ser definido para uma medida.

## <a name="max"></a>max

Valor máximo da métrica Olá agregado. Não deve ser definido para uma medida.

## <a name="standard-deviation"></a>Desvio padrão

Desvio padrão de métrica Olá agregado. Não deve ser definido para uma medida.

## <a name="custom-properties"></a>Propriedades personalizadas

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a>Próximas etapas

- Saiba como toouse [API do Application Insights para métricas e eventos personalizados](app-insights-api-custom-events-metrics.md#trackmetric).
- Consulte [modelo de dados](application-insights-data-model.md) para modelo de dados e tipos do Application Insights.
- Confira as [plataformas](app-insights-platforms.md) com suporte do Application Insights.
