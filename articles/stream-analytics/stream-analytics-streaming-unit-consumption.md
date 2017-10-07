---
title: "O Azure Stream Analytics: Otimizar seu toouse trabalho unidades de Streaming com eficiência | Microsoft Docs"
description: "Práticas recomendadas de consulta para dimensionamento e desempenho no Stream Analytics do Azure."
keywords: unidade de streaming, desempenho de consulta
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 5ad98b34d625190a879260f54c9eff0294e230cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-job-toouse-streaming-units-efficiently"></a>Otimizar seu toouse trabalho unidades de Streaming com eficiência

O Azure Stream Analytics agrega desempenho hello "peso" da execução de um trabalho em unidades de Streaming (SUs). SUs representam os recursos de computação Olá que são consumido tooexecute um trabalho. SUs fornecem um maneira toodescribe Olá relativo de processamento de eventos capacidade com base em uma medida combinada de CPU, memória e leitura e gravação taxas. Esse permite capacidade que você se concentre na lógica de consulta hello e remove você da necessidade de considerações de desempenho da camada de armazenamento tooknow, alocar memória para o trabalho manualmente e aproximado Olá CPU core-contagem necessário toorun seu trabalho de maneira oportuna.

## <a name="how-many-sus-are-required-for-a-job"></a>Quantas SUs são necessárias para um trabalho?

Escolher número de saudação do SUs necessário para um determinado trabalho depende da configuração de partição de saudação para entradas de saudação e consulta Olá que esteja definida no trabalho de saudação. Olá **escala** folha permite tooset Olá número à direita do SUs. É uma prática recomendada tooallocate SUs mais que o necessário. otimiza o mecanismo de processamento de análise de fluxo de saudação de latência e taxa de transferência no custo de saudação da alocação de memória adicional.

Em geral, a prática recomendada de saudação é toostart com 6 SUs para consultas que não usam *PARTITION BY*. Em seguida, determine o ponto central de saudação usando um método de tentativa e erro no qual você modifica número de saudação do SUs após passar representativas quantidades de dados e examinar a métrica de utilização do hello SU %.

A análise de fluxo do Azure mantém os eventos em uma janela chamada hello "reordenar buffer" antes de iniciar qualquer processamento. Eventos são classificados na janela de reordenar Olá por hora e operações subsequentes são executadas em eventos Olá temporariamente classificado. Reordenar eventos por hora garante que esse operador Olá tem visibilidade de todos os eventos Olá Olá estipulado período de tempo. Ele também permite operador Olá executar processamento requisito hello e produzir uma saída. Um efeito colateral esse mecanismo é que o processamento está atrasado por duração de saudação da janela de reordenar hello. espaço de memória de saudação do trabalho de saudação (que afeta o consumo SU) é uma função do tamanho de saudação desse número de janela e hello reordenar de eventos contidos nele.

> [!NOTE]
> Quando o número de saudação de leitores de alterado durante as atualizações do trabalho, transitórios avisos são gravados tooaudit logs. Os trabalhos do Stream Analytics são recuperados automaticamente desses problemas transitórios.

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a>Causas comuns de memória alta para alto uso de SU na execução de trabalhos

### <a name="high-cardinality-for-group-by"></a>Alta cardinalidade para GROUP BY

cardinalidade Olá de eventos de entrada determina o uso de memória para o trabalho de saudação.

Por exemplo, em `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, Olá número associado **clusterizado** é cardinalidade Olá de consulta de saudação.

toomitigate problemas causados por alta cardinalidade, expansão consulta Olá aumentando partições usando **PARTITION BY**.

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

Olá inúmeros *clusterizado* é Olá cardinalidade de GROUP BY aqui.

Após a consulta Olá for particionada, ele distribuída por vários nós. Como resultado, Olá número de eventos que entram em cada nó é reduzido, que por sua vez reduz o tamanho de saudação do buffer de reordenar hello. Você também deve dividir partições do hub de eventos por id de partição.

### <a name="high-unmatched-event-count-for-join"></a>Alta contagem de eventos sem correspondência para JOIN

número de saudação de eventos não correspondentes em uma junção afeta utilização de memória de saudação de consulta de saudação. Por exemplo, execute uma consulta que está procurando toofind Olá inúmeros impressões de anúncio que gera cliques:

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

Nesse cenário, é possível que vários anúncios sejam mostrados e poucos cliques sejam gerados. Esse é um resultado exigiria Olá trabalho tookeep todos os eventos de saudação na janela de tempo de saudação. quantidade de saudação de memória consumida é a taxa de evento e o tamanho de janela toohello proporcional. 

toomitigate nessa situação, a expansão de consulta Olá aumentando partições usando PARTITION BY. 

Após a consulta Olá for particionada, ele distribuída por vários nós de processamento. Como resultado, Olá número de eventos que entram em cada nó é reduzido, que por sua vez reduz o tamanho de saudação do buffer de reordenar hello.

### <a name="large-number-of-out-of-order-events"></a>Grande número de eventos fora de ordem 

Um grande número de eventos fora de ordem dentro de uma janela de tempo grande faz com que o tamanho de saudação do hello "reordenar buffer" toobe maior. toomitigate nessa situação, a consulta de saudação escala aumentando partições usando PARTITION BY. Após a consulta Olá for particionada, ele distribuída por vários nós. Como resultado, Olá número de eventos que entram em cada nó é reduzido, que por sua vez reduz o tamanho de saudação do buffer de reordenar hello. 


## <a name="get-help"></a>Obter ajuda
Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de linguagem de consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)
