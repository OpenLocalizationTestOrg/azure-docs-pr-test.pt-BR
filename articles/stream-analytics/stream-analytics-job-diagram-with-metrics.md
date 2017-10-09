---
title: "AAA Azure Stream Analytics controladas por dados depuração usando o diagrama de trabalho Olá | Microsoft Docs"
description: "Solucionar problemas de seu trabalho do Stream Analytics por meio de métricas e diagrama de trabalho hello."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/01/2017
ms.author: jeffstok
ms.openlocfilehash: 1af884d485bebb06b034da01a13f7f8240516571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a>Depurando usando o diagrama de trabalho Olá controlada por dados

diagrama de trabalho Olá Olá **monitoramento** folha em Olá portal do Azure pode ajudá-lo a visualizar seu pipeline de trabalho. Ele mostra entradas, saídas e etapas de consulta. Você pode usar métricas de Olá Olá trabalho diagrama tooexamine para cada etapa, toomore isolar rapidamente a origem de saudação de um problema ao solucionar problemas.

## <a name="using-hello-job-diagram"></a>Usando o diagrama de trabalho Olá

Em Olá portal do Azure, enquanto um trabalho de análise de fluxo, em **suporte + solução de problemas**, selecione **diagrama trabalho**:

![Diagrama de trabalho com métricas - local](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

Selecione cada seção correspondente de consulta etapa toosee Olá em uma painel de edição de consulta. Um gráfico de métrica para a etapa de saudação é exibido em um painel inferior na página de saudação.

![Diagrama de trabalho com métricas - local](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

partições de saudação toosee de entrada de Hubs de eventos do Azure hello, selecione **...** O menu de contexto é exibido. Você também pode ver fusão de entrada hello.

![Diagrama de trabalho com métricas - expandir partição](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

gráfico métrica do hello toosee apenas uma única partição, nó de partição Olá select. métricas de saudação são mostradas na parte inferior da saudação da página de saudação.

![Diagrama de trabalho com métricas - mais métricas](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

gráfico de métricas toosee Olá para uma fusão, nó de fusão Olá select. Olá gráfico a seguir mostra que não há eventos foram descartados ou ajustados.

![Diagrama de trabalho com métricas - grade](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

detalhes de saudação toosee da hora toohello de ponto de gráfico e o valor de métrica hello.

![Diagrama de trabalho com métricas - focalizar](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a>Solucionar problemas usando métricas

Olá **QueryLastProcessedTime** métrica indica quando uma etapa específica recebeu dados. Examinando topologia hello, você pode trabalhar para trás da saudação saída processador toosee qual etapa não está recebendo dados. Se uma etapa não está recebendo dados, vá para etapa de consulta toohello antes dele. Verifique se a etapa de consulta anterior hello tem uma janela de tempo, e se tiver passado tempo suficiente para que ele toooutput dados. (Observe que tempo windows são ajustada toohello horas.)
 
Se hello etapa de consulta anterior é um processador de entrada, use Olá métricas entrada toohelp resposta Olá destino perguntas a seguir. Elas podem ajudar a determinar se um trabalho está recebendo dados de suas fontes de entrada. Se a consulta Olá estiver particionada, examine cada partição.
 
### <a name="how-much-data-is-being-read"></a>Qual o volume de dados que está sendo lindo?

*   **InputEventsSourcesTotal** é Olá número de unidades de dados de leitura. Olá, por exemplo, o número de blobs.
*   **InputEventsTotal** é Olá número de eventos de leitura. Essa métrica está disponível por partição.
*   **InputEventsInBytesTotal** é Olá número de bytes lidos.
*   **InputEventsLastArrivalTime** é atualizado com o tempo na fila de cada evento recebido.
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a>O tempo está avançando? Se eventos reais forem lidos, a pontuação não poderá ser emitida.

*   **InputEventsLastPunctuationTime** indica quando uma pontuação foi emitida tookeep tempo mover para a frente. Se a pontuação não for emitida, o fluxo de dados poderá ser bloqueado.
 
### <a name="are-there-any-errors-in-hello-input"></a>Há erros na entrada Olá?

*   **InputEventsEventDataNullTotal** é uma contagem de eventos que têm dados nulos.
*   **InputEventsSerializerErrorsTotal** é uma contagem de eventos que não puderam ser desserializados corretamente.
*   **InputEventsDegradedTotal** é uma contagem de eventos que tiveram um problema diferente de desserialização.
 
### <a name="are-events-being-dropped-or-adjusted"></a>Os eventos estão sendo removidos ou ajustados?

*   **InputEventsEarlyTotal** é Olá número de eventos que têm um carimbo de hora do aplicativo antes de marca d'água alta de saudação.
*   **InputEventsLateTotal** é Olá número de eventos que têm um carimbo de hora do aplicativo após a marca d'água alta de saudação.
*   **InputEventsDroppedBeforeApplicationStartTimeTotal** está Olá eventos número descartados antes da hora de início do trabalho de saudação.
 
### <a name="are-we-falling-behind-in-reading-data"></a>Estamos ficando para trás na leitura dos dados?

*   **InputEventsSourcesBackloggedTotal** informa quantas mensagens mais precisam toobe ler para entradas de Hubs de eventos e o Azure IoT Hub.


## <a name="get-help"></a>Obter ajuda
Para obter mais ajuda, teste nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooStream análise](stream-analytics-introduction.md)
* [Introdução ao Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics](stream-analytics-scale-jobs.md)
* [Referência da linguagem de consulta do Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST de gerenciamento do Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
