---
title: aaaDebug Stream Analytics do Azure com receptores de evento de hub | Microsoft Docs
description: "Práticas recomendadas de consulta para consideração de grupos de consumidores dos Hubs de Eventos em trabalhos do Stream Analytics."
keywords: limite do hub de eventos, grupo de consumidores
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
ms.openlocfilehash: 89821e6273151de43b5e42d907e547c939e24824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a>Depurar o Stream Analytics do Azure com receptores do hub de eventos

Você pode usar os Hubs de eventos do Azure no Azure Stream Analytics tooingest ou saída de dados de um trabalho. Uma prática recomendada para usar Hubs de eventos é toouse vários grupos de consumidores, tooensure escalabilidade de trabalho. Uma razão é que o número de Olá de leitores em trabalho do Stream Analytics Olá para uma entrada específica afeta número Olá de leitores em um grupo único consumidor. número preciso de saudação de destinatários baseia-se nos detalhes de implementação interna Olá expansão topologia lógica. número de saudação de destinatários não está exposto externamente. número de saudação de leitores de pode ser alterado na hora de início do trabalho de saudação ou durante as atualizações do trabalho.

> [!NOTE]
> Quando o número de saudação de leitores alterado durante uma atualização de trabalho, transitórios avisos são gravados tooaudit logs. Os trabalhos do Stream Analytics são recuperados automaticamente desses problemas transitórios.

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a>Número de leitores por partição excede o limite de cinco dos Hubs de Eventos

Cenários no qual Olá número de leitores por partição excede o limite de Hubs de eventos de saudação de cinco incluem o seguinte hello:

* Várias instruções SELECT: se você usar várias instruções SELECT que fazem referência muito**mesmo** hub de eventos de entrada, cada instrução SELECT faz com que um novo toobe de destinatário criado.
* UNIÃO: Quando você usa uma união, é possível toohave várias entradas que fazem referência toohello **mesmo** grupo de consumidor e hub de eventos.
* AUTOJUNÇÃO: Quando você usa uma operação JOIN de AUTOATENDIMENTO, é possível toorefer toohello **mesmo** hub de eventos várias vezes.

## <a name="solution"></a>Solução

Olá práticas recomendadas a seguir podem ajudar a reduzir os cenários no qual Olá número de leitores por partição excede o limite de Hubs de eventos de saudação de cinco.

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a>Dividir a consulta em várias etapas usando uma cláusula WITH

cláusula WITH de saudação especifica um conjunto de resultados nomeado temporário que pode ser referenciado por uma cláusula FROM da consulta de saudação. Você define a cláusula WITH de saudação em escopo de execução de saudação de uma única instrução SELECT.

Por exemplo, em vez desta consulta:

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

Use esta consulta:

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-toodifferent-consumer-groups"></a>Certifique-se de que entradas vinculam grupos de consumidores toodifferent

Para consultas de três ou mais entradas são conectado toohello mesmo consumidor de Hubs de eventos de grupo, criar grupos de consumidores separado. Isso exige a criação de saudação de entradas adicionais de análise de fluxo.


## <a name="get-help"></a>Obter ajuda
Para obter mais ajuda, teste nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooStream análise](stream-analytics-introduction.md)
* [Introdução ao Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics](stream-analytics-scale-jobs.md)
* [Referência da linguagem de consulta do Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST de gerenciamento do Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
