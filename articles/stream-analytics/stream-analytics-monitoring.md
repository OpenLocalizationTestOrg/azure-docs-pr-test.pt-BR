---
title: "Monitoramento de trabalho de análise de fluxo de aaaUnderstanding | Microsoft Docs"
description: "Noções básicas sobre monitoramento de trabalho do Stream Analytics"
keywords: monitor de consultas
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 36819025c7b2ddbf4b9694522f1b4820407ca5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a>Entender o monitoramento de trabalho do Stream Analytics e como consultas toomonitor

## <a name="introduction-hello-monitor-page"></a>Introdução: página de monitor de saudação
Olá portal do Azure, as principais métricas de desempenho que podem ser usado toomonitor e solucionar problemas de desempenho de sua consulta e o trabalho de superfície. toosee essas métricas, procurar o trabalho de análise de fluxo de toohello você está interessado em ver saudação do modo de exibição e métricas para **monitoramento** seção na página de visão geral de saudação.  

![Link de monitoramento](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

janela Hello serão exibidos conforme mostrado:

![Painel de Trabalho de monitoramento](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a>Métricas disponíveis para o Stream Analytics
| Métrica                 | Definição                               |
| ---------------------- | ---------------------------------------- |
| % de utilização do SU       | utilização de saudação do hello unidades de Streaming atribuído tooa trabalho na guia de escala de saudação do trabalho hello. Se esse indicador alcançar 80% ou acima, há grande probabilidade de que o processamento de eventos se atrase ou pare. |
| Eventos de entrada           | Quantidade de dados recebidos pelo trabalho do Stream Analytics hello, no número de eventos. Isso pode ser usado toovalidate que os eventos estão sendo enviados toohello fonte de entrada. |
| Eventos de saída          | Quantidade de dados enviados pelo Olá Stream Analytics trabalho toohello destino de saída, no número de eventos. |
| Eventos fora de ordem    | Número de eventos recebidos fora de ordem que foram descartados ou que receberam um carimbo de hora ajustado com base em Olá diretiva de ordenação de eventos. Isso pode ser afetado pela configuração de saudação da configuração da janela de tolerância de fora de ordem de saudação. |
| Erros de conversão de dados | Número de erros de conversão de dados gerado por um trabalho do Stream Analytics. |
| Erros de tempo de execução         | Olá total de erros que ocorrem durante a execução de um trabalho do Stream Analytics. |
| Eventos de entrada atrasados      | Número de eventos que chegam tarde de origem Olá que pode ter sido descartado ou seu carimbo de data foi ajustado, com base na configuração de diretiva de ordenação de eventos de saudação da configuração de janela de tolerância da chegada tardia hello. |
| Solicitações de função      | Número de chamadas toohello função de aprendizado de máquina do Azure (se houver). |
| Solicitações de função com falha | Número de chamadas à função Azure Machine Learning com falha (se presente). |
| Eventos de função        | Número de eventos enviados toohello função de aprendizado de máquina do Azure (se houver). |
| Bytes de evento de entrada      | Quantidade de dados recebidos pelo trabalho do Stream Analytics hello, em bytes. Isso pode ser usado toovalidate que os eventos estão sendo enviados toohello fonte de entrada. |


## <a name="customizing-monitoring-in-hello-azure-portal"></a>Personalizando o monitoramento no hello portal do Azure
Você pode ajustar o tipo de gráfico, as métricas mostrados, hello e intervalo nas configurações do hello Editar gráfico de tempo. Para obter detalhes, consulte [como tooCustomize monitoramento](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).

  ![Gráfico do Tempo do Monitor de Consultas](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a>Obter ajuda
Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

