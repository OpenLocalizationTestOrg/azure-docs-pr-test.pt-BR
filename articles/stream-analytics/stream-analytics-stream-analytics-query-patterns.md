---
title: "exemplos de aaaQuery para padrões de uso comuns no Stream Analytics | Microsoft Docs"
description: "Padrões de consulta comuns do Azure Stream Analytics"
keywords: exemplos de consulta
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jenniehubbard
editor: cgronlun
ms.assetid: 6b9a7d00-fbcc-42f6-9cbb-8bbf0bbd3d0e
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/08/2017
ms.author: jenniehubbard
ms.openlocfilehash: c8f7a8ac661eaf0281f4140b02c42141b73040fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a>Exemplos de consulta para padrões de uso do Stream Analytics
## <a name="introduction"></a>Introdução
As consultas no Azure Stream Analytics são expressas em uma linguagem de consulta parecida com o SQL. Essas consultas estão documentadas em Olá [referência de linguagem de consulta do Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx) guia. Este artigo descreve soluções tooseveral padrões comuns de consulta, com base em cenários do mundo real. É um trabalho em andamento e continua toobe atualizado com novos padrões de forma contínua.

## <a name="query-example-convert-data-types"></a>Exemplo de consulta: converter tipos de dados
**Descrição**: definir tipos de saudação de propriedades no fluxo de entrada hello.
Por exemplo, Olá carro são as novidades no fluxo de entrada hello como cadeias de caracteres e o peso precisa toobe convertido muito**INT** tooperform **soma** -o.

**Entrada**:

| Faça | Hora | Peso |
| --- | --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |"1000" |
| Honda |2015-01-01T00:00:02.0000000Z |"2000" |

**Saída**:

| Faça | Peso |
| --- | --- |
| Honda |3000 |

**Solução**:

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

**Explicação**: Use um **CAST** instrução Olá **peso** campo toospecify seu tipo de dados. Consulte lista de saudação de tipos de dados com suporte no [tipos de dados (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).

## <a name="query-example-use-likenot-like-toodo-pattern-matching"></a>Exemplo de consulta: Use Like ou não como correspondência de padrão de toodo
**Descrição**: Verifique se o valor de um campo em eventos de saudação corresponde a um determinado padrão.
Por exemplo, verificar o resultado Olá retorna placas que começam com A e terminar com 9.

**Entrada**:

| Faça | PlacaDeCarro | Hora |
| --- | --- | --- |
| Honda |ABC-123 |2015-01-01T00:00:01.0000000Z |
| Toyota |AAA-999 |2015-01-01T00:00:02.0000000Z |
| Nissan |ABC-369 |2015-01-01T00:00:03.0000000Z |

**Saída**:

| Faça | PlacaDeCarro | Hora |
| --- | --- | --- |
| Toyota |AAA-999 |2015-01-01T00:00:02.0000000Z |
| Nissan |ABC-369 |2015-01-01T00:00:03.0000000Z |

**Solução**:

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

**Explicação**: Olá Use **como** saudação do instrução toocheck **LicensePlate** valor do campo. Ele deve começar com um A, ter uma cadeia de caracteres com nenhum ou mais caracteres, e terminar com 9. 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a>Exemplo de consulta: especifique a lógica para casos/valores diferentes (instruções CASE)
**Descrição**: forneça um cálculo diferente para um campo com base em um critério específico.
Por exemplo, forneça uma descrição de cadeia de caracteres para quantos carros de saudação mesmo fazer passado, com um caso especial para 1.

**Entrada**:

| Faça | Hora |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Saída**:

| CarrosPassaram | Hora |
| --- | --- | --- |
| 1 Honda |2015-01-01T00:00:10.0000000Z |
| 2 Toyotas |2015-01-01T00:00:10.0000000Z |

**Solução**:

    SELECT
        CASE
            WHEN COUNT(*) = 1 THEN CONCAT('1 ', Make)
            ELSE CONCAT(CAST(COUNT(*) AS NVARCHAR(MAX)), ' ', Make, 's')
        END AS CarsPassed,
        System.TimeStamp AS Time
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

**Explicação**: Olá **caso** cláusula nos permite tooprovide uma computação diferente, com base em alguns critérios (no nosso caso, a contagem de saudação de carros Olá na janela de agregação de saudação).

## <a name="query-example-send-data-toomultiple-outputs"></a>Exemplo de consulta: enviar dados toomultiple saídas
**Descrição**: enviar dados toomultiple destinos de um único trabalho de saída.
Por exemplo, analisar os dados de um alerta de limite e armazenamento de tooblob todos os eventos de arquivos.

**Entrada**:

| Faça | Hora |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Saída1**:

| Faça | Hora |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Saída2**:

| Faça | Hora | Contagem |
| --- | --- | --- |
| Toyota |2015-01-01T00:00:10.0000000Z |3 |

**Solução**:

    SELECT
        *
    INTO
        ArchiveOutput
    FROM
        Input TIMESTAMP BY Time

    SELECT
        Make,
        System.TimeStamp AS Time,
        COUNT(*) AS [Count]
    INTO
        AlertOutput
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)
    HAVING
        [Count] >= 3

**Explicação**: Olá **INTO** cláusula informa Stream Analytics que hello gera toowrite Olá dados toofrom essa instrução.
Olá primeira consulta é uma passagem de dados Olá recebemos saída tooan que chamamos **ArchiveOutput**.
consulta de segundo de saudação faz algumas agregação simple e filtragem e envia os resultados de saudação tooa sistema downstream de alertas.

Observe que você também pode reutilizar os resultados de saudação de expressões de tabela comuns Olá (CTEs) (como **WITH** instruções) em várias declarações de saída. Essa opção tem Olá benefício adicional de abertura menos fonte de entrada toohello leitores.
Por exemplo: 

    WITH AllRedCars AS (
        SELECT
            *
        FROM
            Input TIMESTAMP BY Time
        WHERE
            Color = 'red'
    )
    SELECT * INTO HondaOutput FROM AllRedCars WHERE Make = 'Honda'
    SELECT * INTO ToyotaOutput FROM AllRedCars WHERE Make = 'Toyota'

## <a name="query-example-count-unique-values"></a>Exemplo de consulta: contar valores exclusivos
**Descrição**: contar Olá número exclusivo de valores de campo que aparecem no fluxo hello dentro de uma janela de tempo.
Por exemplo, quantas exclusivas faz de carros passados pelo pedágio Olá em uma janela de 2 segundos?

**Entrada**:

| Faça | Hora |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Saída:**

| Contagem | Hora |
| --- | --- |
| 2 |2015-01-01T00:00:02.000Z |
| 1 |2015-01-01T00:00:04.000Z |

**Solução:**

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


**Explicação:**
**COUNT (DISTINCT Verifique)** retorna Olá número de valores distintos em Olá **fazer** coluna dentro de uma janela de tempo.

## <a name="query-example-determine-if-a-value-has-changed"></a>Exemplo de consulta: determinar se um valor foi alterado
**Descrição**: examinar um toodetermine valor anterior, se for diferente do valor atual de saudação.
Por exemplo, está carro anterior Olá Olá Olá de estrada pedágio que mesmo fazer como car atual Olá?

**Entrada**:

| Faça | Hora |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |

**Saída**:

| Faça | Hora |
| --- | --- |
| Toyota |2015-01-01T00:00:02.0000000Z |

**Solução**:

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

**Explicação**: Use **LATÊNCIA** toopeek em Olá fluxo volta um evento de entrada e obter Olá **fazer** valor. Em seguida, comparar toohello **fazer** valor em Olá atual e saída saudação do evento, se eles forem diferentes.

## <a name="query-example-find-hello-first-event-in-a-window"></a>Exemplo de consulta: localizar Olá primeiro evento em uma janela
**Descrição**: localizar Olá primeiro carro em cada intervalo de 10 minutos.

**Entrada**:

| PlacaDeCarro | Faça | Hora |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:02:17.0000000Z |
| RMV 8282 |Honda |2015-07-27T00:05:01.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:06:00.0000000Z |
| VFE 1616 |Toyota |2015-07-27T00:09:31.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Saída**:

| PlacaDeCarro | Faça | Hora |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |

**Solução**:

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

Agora vamos alterar Olá problema e localizar Olá primeiro carro de um determinado fazer em cada intervalo de 10 minutos.

| PlacaDeCarro | Faça | Hora |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:02:17.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:06:00.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Solução**:

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-hello-last-event-in-a-window"></a>Exemplo de consulta: localizar Olá último evento em uma janela
**Descrição**: carro de última encontrar hello em cada intervalo de 10 minutos.

**Entrada**:

| PlacaDeCarro | Faça | Hora |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:02:17.0000000Z |
| RMV 8282 |Honda |2015-07-27T00:05:01.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:06:00.0000000Z |
| VFE 1616 |Toyota |2015-07-27T00:09:31.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Saída**:

| PlacaDeCarro | Faça | Hora |
| --- | --- | --- |
| VFE 1616 |Toyota |2015-07-27T00:09:31.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Solução**:

    WITH LastInWindow AS
    (
        SELECT 
            MAX(Time) AS LastEventTime
        FROM 
            Input TIMESTAMP BY Time
        GROUP BY 
            TumblingWindow(minute, 10)
    )
    SELECT 
        Input.LicensePlate,
        Input.Make,
        Input.Time
    FROM
        Input TIMESTAMP BY Time 
        INNER JOIN LastInWindow
        ON DATEDIFF(minute, Input, LastInWindow) BETWEEN 0 AND 10
        AND Input.Time = LastInWindow.LastEventTime

**Explicação**: há duas etapas na consulta de saudação. Olá primeiro localiza uma saudação mais recente carimbo de hora no windows 10 minutos. junções de etapa segundo Olá Olá resultados de consulta de primeira Olá Olá original fluxo toofind Olá eventos que correspondem a última carimbos de hora Olá em cada janela. 

## <a name="query-example-detect-hello-absence-of-events"></a>Exemplo de consulta: detectarem Olá ausência de eventos
**Descrição**: confirme se um fluxo não tem um valor correspondente a determinado critério.
Por exemplo, 2 carros consecutivos de saudação que mesmo fazer inseriu road de pedágio hello dentro Olá últimos 90 segundos?

**Entrada**:

| Faça | PlacaDeCarro | Hora |
| --- | --- | --- |
| Honda |ABC-123 |2015-01-01T00:00:01.0000000Z |
| Honda |AAA-999 |2015-01-01T00:00:02.0000000Z |
| Toyota |DEF-987 |2015-01-01T00:00:03.0000000Z |
| Honda |GHI-345 |2015-01-01T00:00:04.0000000Z |

**Saída**:

| Faça | Hora | PlacaDoCarroAtual | PlacaDoPrimeiroCarro | HoraDoPrimeiroCarro |
| --- | --- | --- | --- | --- |
| Honda |2015-01-01T00:00:02.0000000Z |AAA-999 |ABC-123 |2015-01-01T00:00:01.0000000Z |

**Solução**:

    SELECT
        Make,
        Time,
        LicensePlate AS CurrentCarLicensePlate,
        LAG(LicensePlate, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarLicensePlate,
        LAG(Time, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarTime
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(second, 90)) = Make

**Explicação**: Use **LATÊNCIA** toopeek em Olá fluxo volta um evento de entrada e obter Olá **fazer** valor. Compare-toohello **fazer** valor no evento atual hello e eventos de saudação de saída se eles são Olá mesmo. Você também pode usar **LATÊNCIA** tooget dados sobre o carro anterior hello.

## <a name="query-example-detect-hello-duration-between-events"></a>Exemplo de consulta: detectar duração Olá entre eventos
**Descrição**: localizar duração de saudação de um determinado evento. Por exemplo, dada uma sequência de cliques da web, determine gasto em um recurso de tempo de saudação.

**Entrada**:  

| Usuário | Recurso | Evento | Hora |
| --- | --- | --- | --- |
| user@location.com |RightMenu |Iniciar |2015-01-01T00:00:01.0000000Z |
| user@location.com |RightMenu |End |2015-01-01T00:00:08.0000000Z |

**Saída**:  

| Usuário | Recurso | Duração |
| --- | --- | --- |
| user@location.com |RightMenu |7 |

**Solução**:

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

**Explicação**: Olá Use **último** função tooretrieve Olá última **tempo** valor quando o tipo de evento Olá foi **iniciar**. Olá **último** função usa **PARTITION BY [usuário]** tooindicate que Olá resultado é calculado por usuário exclusivo. consulta de saudação tem um limite máximo de 1 hora de diferença de tempo de saudação entre **iniciar** e **parar** eventos, mas pode ser configurado conforme necessário **(limite DURATION(hour, 1)**.

## <a name="query-example-detect-hello-duration-of-a-condition"></a>Exemplo de consulta: detectar duração de saudação de uma condição
**Descrição**: descubra por quanto tempo uma condição durou.
Por exemplo, suponha que um bug resultou no peso incorreto de todos os carros (acima de 9.000 quilos). Queremos toocompute duração de saudação do bug hello.

**Entrada**:

| Faça | Hora | Peso |
| --- | --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |2000 |
| Toyota |2015-01-01T00:00:02.0000000Z |25000 |
| Honda |2015-01-01T00:00:03.0000000Z |26000 |
| Toyota |2015-01-01T00:00:04.0000000Z |25000 |
| Honda |2015-01-01T00:00:05.0000000Z |26000 |
| Toyota |2015-01-01T00:00:06.0000000Z |25000 |
| Honda |2015-01-01T00:00:07.0000000Z |26000 |
| Toyota |2015-01-01T00:00:08.0000000Z |2000 |

**Saída**:

| FalhaInicial | FalhaFinal |
| --- | --- |
| 2015-01-01T00:00:02.000Z |2015-01-01T00:00:07.000Z |

**Solução**:

````
    WITH SelectPreviousEvent AS
    (
    SELECT
    *,
        LAG([time]) OVER (LIMIT DURATION(hour, 24)) as previousTime,
        LAG([weight]) OVER (LIMIT DURATION(hour, 24)) as previousWeight
    FROM input TIMESTAMP BY [time]
    )

    SELECT 
        LAG(time) OVER (LIMIT DURATION(hour, 24) WHEN previousWeight < 20000 ) [StartFault],
        previousTime [EndFault]
    FROM SelectPreviousEvent
    WHERE
        [weight] < 20000
        AND previousWeight > 20000
````

**Explicação**: Use **LATÊNCIA** tooview fluxo de entrada hello por 24 horas e procurar instâncias onde **StartFault** e **StopFault** são incluídas por Olá Peso < 20000.

## <a name="query-example-fill-missing-values"></a>Exemplo de consulta: preencher valores ausentes
**Descrição**: para o fluxo de saudação de eventos que têm valores ausentes, produzir um fluxo de eventos com intervalos regulares.
Por exemplo, gera um evento a cada 5 segundos que informa o ponto de dados Olá visto mais recentemente.

**Entrada**:

| t | value |
| --- | --- |
| "2014-01-01T06:01:00" |1 |
| "2014-01-01T06:01:05" |2 |
| "2014-01-01T06:01:10" |3 |
| "2014-01-01T06:01:15" |4 |
| "2014-01-01T06:01:30" |5 |
| "2014-01-01T06:01:35" |6 |

**(10 primeiras linhas) de saída**:

| windowend | lastevent.t | lastevent.value |
| --- | --- | --- |
| 2014-01-01T14:01:00.000Z |2014-01-01T14:01:00.000Z |1 |
| 2014-01-01T14:01:05.000Z |2014-01-01T14:01:05.000Z |2 |
| 2014-01-01T14:01:10.000Z |2014-01-01T14:01:10.000Z |3 |
| 2014-01-01T14:01:15.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:20.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:25.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:30.000Z |2014-01-01T14:01:30.000Z |5 |
| 2014-01-01T14:01:35.000Z |2014-01-01T14:01:35.000Z |6 |
| 2014-01-01T14:01:40.000Z |2014-01-01T14:01:35.000Z |6 |
| 2014-01-01T14:01:45.000Z |2014-01-01T14:01:35.000Z |6 |

**Solução**:

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


**Explicação**: esta consulta gera eventos de 5 segundos e saídas Olá último evento recebido anteriormente. Olá [janela Hopping](https://msdn.microsoft.com/library/dn835041.aspx "Hopping janela — Azure Stream Analytics") duração determina quanto consulta Olá back parece evento mais recente do toofind hello (300 segundos, neste exemplo).

## <a name="get-help"></a>Obter ajuda
Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

