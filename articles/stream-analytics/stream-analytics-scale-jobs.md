---
title: "taxa de transferência tooincrease trabalhos de análise de fluxo de aaaScale | Microsoft Docs"
description: "Saiba como os trabalhos de análise de fluxo de tooscale configurar partições de entrada, ajustando a definição de consulta hello e definindo unidades de streaming de trabalhos."
keywords: "streaming de dados, processamento de dados de streaming, ajuste de análise"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/22/2017
ms.author: jeffstok
ms.openlocfilehash: 4ba8f6b2f8bfebd52cfa07696b501b42cda21f75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-stream-analytics-jobs-tooincrease-stream-data-processing-throughput"></a>Escala do Azure Stream Analytics trabalhos tooincrease fluxo processamento de dados de taxa de transferência
Este artigo mostra como tootune um Stream Analytics consultar tooincrease a taxa de transferência para trabalhos de análise de fluxo contínuo. Você aprenderá como tooscale do Stream Analytics trabalhos configurando partições de entrada, definição de consulta de análise de ajuste hello e calcular e configuração de trabalho *unidades de streaming* (SUs). 

## <a name="what-are-hello-parts-of-a-stream-analytics-job"></a>Quais são Olá partes de um trabalho do Stream Analytics?
Uma definição de trabalho de Stream Analytics inclui entradas, consulta e saída. As entradas são onde o trabalho Olá lê o fluxo de dados de saudação do. consulta Hello é fluxo de entrada hello dados tootransform usado e saída de hello é onde o trabalho Olá envia os resultados do trabalho Olá para.  

Um trabalho requer pelo menos uma fonte de entrada para streaming de dados. Olá fonte de entrada de fluxo de dados pode ser armazenado em um hub de eventos do Azure ou no armazenamento de BLOBs do Azure. Para obter mais informações, consulte [tooAzure de Introdução do Stream Analytics](stream-analytics-introduction.md) e [começar a usar o Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).

## <a name="partitions-in-event-hubs-and-azure-storage"></a>Partições em Hubs de evento ou armazenamento do Azure
Dimensionamento de um trabalho do Stream Analytics aproveita partições Olá entrada ou saída. Particionamento permite que você divida dados em subconjuntos com base em uma chave de partição. Um processo que consome dados hello (como um trabalho de análise de fluxo) pode consumir e gravar diferentes partições em paralelo, o que aumenta a taxa de transferência. Quando você trabalha com Streaming Analytics, você pode tirar proveito do particionamento em Hubs de eventos e em armazenamento de Blobs. 

Para obter mais informações sobre partições, consulte Olá artigos a seguir:

* [Visão geral dos recursos de Hubs de Eventos](../event-hubs/event-hubs-features.md#partitions)
* [Particionamento de dados](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a>Unidades de streaming (SUs)
Unidades (SUs) representam Olá recursos de streaming e computação de energia que são necessários na ordem tooexecute um trabalho do Stream Analytics do Azure. SUs fornecem um maneira toodescribe Olá relativo de processamento de eventos capacidade com base em uma medida combinada de CPU, memória e leitura e gravação taxas. Cada SU corresponde tooroughly 1 MB/segundo de taxa de transferência. 

Escolhendo o SUs quantos são necessários para um determinado trabalho depende na configuração de partição Olá para entradas de saudação e consulta Olá definidas para o trabalho de saudação. Você pode selecionar a cota de tooyour em SUs para um trabalho. Por padrão, cada assinatura do Azure tem uma cota de backup too50 SUs para todos os trabalhos de análise de saudação em uma região específica. tooincrease SUs para suas assinaturas além essa cota, entre em contato com [Microsoft Support](http://support.microsoft.com). Os valores válidos para o SUs por trabalho são 1, 3, 6 e em incrementos de 6.

## <a name="embarrassingly-parallel-jobs"></a>Trabalhos embaraçosamente paralelos
Um *paralelo* trabalho é cenário mais escalonável hello, temos no Azure Stream Analytics. Ele se conecta a uma partição da instância de entrada tooone Olá da partição de tooone Olá consulta de saída de hello. Esse paralelismo tem Olá requisitos a seguir:

1. Se sua lógica de consulta depende Olá a mesma chave que está sendo processado por Olá mesma instância de consulta, você deve assegurar-se de que eventos Olá vão toohello mesma partição de sua entrada. Para hubs de eventos, isso significa que os dados de evento de saudação devem ter Olá **PartitionKey** conjunto de valor. Como alternativa, você pode usar os remetentes particionados. Para o armazenamento de blob, isso significa que os eventos de saudação são enviados toohello mesma pasta de partição. Se sua lógica de consulta não requer Olá a mesma chave toobe processada por Olá mesma instância de consulta, você pode ignorar esse requisito. Um exemplo disso seria uma consulta simples de seleção/projeto/filtro.  

2. Depois de saudação dados são dispostos no lado de entrada hello, assegure-se de que sua consulta está particionada. Isso exige que você toouse **Partition By** em todas as etapas de saudação. Várias etapas são permitidas, mas todos eles devem ser particionados por Olá mesma chave. Atualmente, Olá chave de particionamento deve ser definido muito**PartitionId** em ordem para Olá trabalho toobe totalmente paralelo.  

3. Atualmente, somente Hubs de eventos e armazenamento de Blobs permitem a saída particionada. Saída do hub de eventos, você deve configurar Olá partição chave toobe **PartitionId**. Saída do armazenamento de blob, você não tem toodo, nada.  

4. número de saudação de partições de entrada deve ser igual Olá número de partições de saída. Atualmente, o armazenamento de Blobs de saída não suporta partições. Mas isso é okey, porque ele herda Olá esquema da consulta upstream Olá de particionamento. Exemplos de valores de partição que permitem um trabalho totalmente paralelo:  

   * 8 partições de entrada de Hubs de Eventos e 8 partições de saída de Hubs de Eventos
   * 8 partições de entrada de Hubs de Eventos e Saída de armazenamento de Blobs  
   * 8 partições de entrada de armazenamento de Blobs e Saída de armazenamento de Blobs  
   * 8 partições de entrada de armazenamento de Blobs e 8 partições de saída de Hubs de Eventos  

Olá seções a seguir discutem alguns cenários de exemplo que são excessivamente paralelos.

### <a name="simple-query"></a>Consulta simples

* Entrada: Hub de eventos com 8 partições
* Saída: Hub de eventos com 8 partições

Consulta:

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

Essa consulta é um filtro simples. Portanto, não precisamos tooworry sobre o particionamento de entrada hello que está sendo enviada toohello hub de eventos. Observe que essa consulta Olá inclui **partição por PartitionId**, portanto, ela preenche o requisito #2 anteriores. Saída de hello, precisamos de saída do hub de eventos do tooconfigure Olá no conjunto de chaves de partição Olá trabalho toohave Olá muito**PartitionId**. Uma última verificação está toomake se Olá número de partições de entrada é igual toohello número de partições de saída.

### <a name="query-with-a-grouping-key"></a>Consulta com chave de agrupamento

* Entrada: Hub de eventos com 8 partições
* Saída: Armazenamento de Blobs

Consulta:

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Esta consulta tem uma chave de agrupamento. Portanto, Olá mesmo toobe principais necessidades processada pelo Olá mesmo consultar instâncias, o que significa que eventos devem ser enviados toohello hub de eventos de modo particionado. Mas qual chave deve ser usada? **PartitionId** é um conceito de lógica de trabalho. Olá chave nos preocupamos realmente é **TollBoothId**, portanto Olá **PartitionKey** valor dos dados de evento Olá deve ser **TollBoothId**. Podemos fazer isso na consulta Olá definindo **Partition By** muito**PartitionId**. Como saída de hello é o armazenamento de blob, não precisamos tooworry sobre como configurar um valor de chave de partição, de acordo com o requisito #4.

### <a name="multi-step-query-with-a-grouping-key"></a>Consulta de várias etapas com chave de agrupamento
* Entrada: Hub de eventos com 8 partições
* Saída: Instância de Hub de eventos com 8 partições

Consulta:

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Esta consulta tem uma chave de agrupamento, Olá assim mesmo toobe principais necessidades processada pelo Olá mesma instância de consulta. Podemos usar Olá a mesma estratégia como no exemplo anterior de saudação. Nesse caso, a consulta de saudação tem várias etapas. Cada etapa tem **Partition By PartitionId**? Sim, então consulta Olá preenche o requisito #3. Saída de hello, precisamos chave de partição Olá tooset muito**PartitionId**, conforme discutido anteriormente. Também é possível observar que ele tem Olá mesmo número de partições como entrada hello.

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a>Cenários de exemplo que *não* são embaraçosamente paralelos

Na seção anterior do hello, mostramos alguns cenários em paralelos. Nesta seção, vamos discutir os cenários que não atendem a todos os Olá requisitos toobe paralelo. 

### <a name="mismatched-partition-count"></a>Contagem de partições incompatível
* Entrada: Hub de eventos com 8 partições
* Saída: Hub de eventos com 32 partições

Nesse caso, não importa qual consulta Olá é. Se a contagem de partição de entrada hello não coincidir com a contagem de partições de saída de hello, topologia de saudação não é paralela.

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a>Não usando Hubs de Eventos ou armazenamento de Blobs como saída
* Entrada: Hub de eventos com 8 partições
* Saída: PowerBI

Atualmente, a saída do PowerBI não suporta particionamento. Portanto, esse cenário não é embaraçosamente paralelo.

### <a name="multi-step-query-with-different-partition-by-values"></a>Consulta de várias etapas com diferentes valores por partição
* Entrada: Hub de eventos com 8 partições
* Saída: Hub de eventos com 8 partições

Consulta:

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

Como você pode ver, Olá segunda etapa usa **TollBoothId** como Olá chave de particionamento. Esta etapa não é Olá mesmo como primeira etapa do hello e, portanto, requer nos toodo uma ordem aleatória. 

Olá exemplos anteriores mostram alguns trabalhos do Stream Analytics que está de acordo com muito (ou não) em uma topologia em paralela. Se eles estão em conformidade, eles têm o potencial de saudação para expansão máxima. Para trabalhos que não se encaixam em nenhum desses perfis, as diretrizes de expansão estarão disponíveis em atualizações futuras. Por enquanto, use diretrizes gerais de saudação em Olá seções a seguir.

## <a name="calculate-hello-maximum-streaming-units-of-a-job"></a>Calcular a saudação unidades de streaming de máximo de um trabalho
número total de saudação de unidades de streaming que pode ser usado por um trabalho do Stream Analytics depende do número Olá das etapas de consulta Olá definidos para trabalho hello e número de saudação de partições para cada etapa.

### <a name="steps-in-a-query"></a>Etapas de uma consulta
Uma consulta pode ter uma ou mais etapas. Cada etapa é uma subconsulta definida por Olá **WITH** palavra-chave. consulta Olá fora Olá **WITH** palavra-chave (apenas uma consulta) também é contado como uma etapa, como Olá **selecione** instrução Olá consulta a seguir:

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

Esta consulta tem duas etapas.

> [!NOTE]
> Essa consulta é abordada em mais detalhes posteriormente neste artigo hello.
>  

### <a name="partition-a-step"></a>Uma etapa de partição
Particionamento de uma etapa requer Olá condições a seguir:

* fonte de entrada Hello deve ser particionado. 
* Olá **selecione** instrução de consulta Olá deve ler de uma fonte de entrada particionada.
* consulta de saudação na etapa Olá deve ter Olá **Partition By** palavra-chave.

Quando uma consulta for particionada, eventos de entrada hello são processados e agregados na partição separada grupos e saídas de eventos são geradas para cada um dos grupos de saudação. Se você quiser uma agregação combinada, você deve criar um segundo tooaggregate de etapa não particionado.

### <a name="calculate-hello-max-streaming-units-for-a-job"></a>Calcule o máximo de saudação unidades para um trabalho de streaming
Juntas, todas as etapas não particionado podem escalar verticalmente toosix unidades (SUs) para um trabalho de análise de fluxo de streaming. SUs tooadd, uma etapa devem ser particionado. Cada partição pode ter seis unidades de streaming.

<table border="1">
<tr><th>Consultar</th><th>SUs máxima para o trabalho de saudação</th></td>

<tr><td>
<ul>
<li>consulta de saudação contém uma etapa.</li>
<li>etapa Olá não está particionada.</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>fluxo de dados de entrada Hello é particionado por 3.</li>
<li>consulta de saudação contém uma etapa.</li>
<li>etapa Hello está particionada.</li>
</ul>
</td>
<td>18</td></tr>

<tr><td>
<ul>
<li>consulta de saudação contém duas etapas.</li>
<li>Nenhuma das etapas de saudação é particionada.</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>fluxo de dados de entrada Hello é particionado por 3.</li>
<li>consulta de saudação contém duas etapas. etapa de entrada Hello está particionada e Olá segunda etapa não é.</li>
<li>Olá <strong>selecione</strong> lê de declaração de entrada hello particionada.</li>
</ul>
</td>
<td>24 (18 para as etapas particionadas + 6 para as etapas não particionadas)</td></tr>
</table>

### <a name="examples-of-scaling"></a>Exemplos de escala

Olá, consulta a seguir calcula Olá número de carros dentro de uma janela de três minutos passando por uma estação de pedágio que tem três tollbooths. Essa consulta pode ser dimensionada toosix SUs.

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

toouse mais SUs para Olá consulta, ambos Olá fluxo de dados de entrada e consulta Olá deve ser particionada. Como partição de fluxo de dados hello está definida too3, hello seguinte consulta modificada pode ser dimensionada too18 SUs:

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Quando uma consulta for particionada, eventos de entrada hello são processados e agregados em grupos de partição separada. Eventos de saída também são gerados para cada um dos grupos de saudação. O particionamento pode fazer com que alguns resultados inesperados quando hello **GROUP BY** campo não é uma chave de partição Olá no fluxo de dados de entrada hello. Por exemplo, Olá **TollBoothId** campo na consulta anterior Olá não é chave de partição de saudação do **Entrada1**. resultado de saudação é que hello dados de pedágio #1 possam ser distribuídos em várias partições.

Cada Olá **Entrada1** partições serão processadas separadamente pela análise de fluxo. Como resultado, vários registros de contagem de carro Olá para Olá mesmo pedágio em Olá mesma janela em cascata será criada. Se a chave de partição de entrada hello não pode ser alterado, esse problema pode ser corrigido adicionando uma etapa de partição não, como no exemplo a seguir de saudação:

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

Essa consulta pode ser dimensionado too24 SUs.

> [!NOTE]
> Se você estiver unindo os dois fluxos, certifique-se de que fluxos Olá são particionados por chave de partição de saudação da coluna de saudação que você use toocreate Olá junções. Também, certifique-se de que você tenha Olá mesmo número de partições em ambos os fluxos.
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a>Configurar as unidades de streaming do Stream Analytics

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Na lista de saudação de recursos, localize o trabalho de análise de fluxo de saudação que você deseja tooscale e abra-o.
3. Em Olá trabalho folha, em **configurar**, clique em **escala**.

    ![Configuração de trabalho do Stream Analytics no Portal do Azure][img.stream.analytics.preview.portal.settings.scale]

4. Use Olá controle deslizante tooset hello SUs para trabalho hello. Observe que você está limitado toospecific configurações de SU.


## <a name="monitor-job-performance"></a>Monitorar o desempenho do trabalho
Usando Olá portal do Azure, você pode controlar taxa de transferência de saudação de um trabalho:

![Análise de fluxo do Azure, monitorar trabalhos][img.stream.analytics.monitor.job]

Calcule taxa de transferência de saudação esperada de carga de trabalho de saudação. Se a taxa de transferência de saudação é menor do que o esperado, ajustar a partição de entrada hello, ajustar a consulta hello e adicionar SUs tooyour trabalho.


## <a name="visualize-stream-analytics-throughput-at-scale-hello-raspberry-pi-scenario"></a>Visualizar a taxa de transferência do Stream Analytics em escala: cenário de Pi framboesa Olá
toohelp que você entender como os trabalhos do Stream Analytics escala, realizamos uma experiência com base na entrada de um dispositivo de framboesa Pi. Esse teste vamos ver o efeito de saudação na taxa de transferência de várias partições e unidades de streaming.

Nesse cenário, o dispositivo de saudação envia hub de eventos de tooan sensor dados (clientes). Análise de fluxo contínuo processa dados saudação e envia um alerta ou estatísticas como um hub de eventos de tooanother de saída. 

cliente Olá envia dados de sensor no formato JSON. a saída de dados Olá também está no formato JSON. dados de saudação tem esta aparência:

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

Olá consulta a seguir é usado toosend um alerta quando uma luz é desligada:

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a>Medida de taxa de transferência

Nesse contexto, a taxa de transferência é a quantidade Olá de dados de entrada processados pela análise de fluxo em um determinado período de tempo. (É medido por 10 minutos). dados de entrada tooachieve Olá melhor throughput de processamento para hello, entrada de fluxo de dados hello e consulta Olá foram particionadas. Incluímos **Count ()** em Olá consulta toomeasure quantos eventos de entrada foram processados. toomake se Olá trabalho foi não simplesmente aguardando toocome eventos de entrada, cada partição do hub de evento de entrada hello foi pré-carregado com cerca de 300 MB de dados de entrada.

Olá tabela a seguir mostra os resultados de saudação que vimos quando a partição correspondente Olá contagens hubs de eventos e aumentamos o número de saudação de unidades de streaming.  

<table border="1">
<tr><th>Partições de entrada</th><th>Partições de saída</th><th>Unidades de streaming</th><th>Taxa de transferência mantida
</th></td>

<tr><td>12</td>
<td>12</td>
<td>6</td>
<td>4,06 MB/s</td>
</tr>

<tr><td>12</td>
<td>12</td>
<td>12</td>
<td>8,06 MB/s</td>
</tr>

<tr><td>48</td>
<td>48</td>
<td>48</td>
<td>38,32 MB/s</td>
</tr>

<tr><td>192</td>
<td>192</td>
<td>192</td>
<td>172,67 MB/s</td>
</tr>

<tr><td>480</td>
<td>480</td>
<td>480</td>
<td>454,27 MB/s</td>
</tr>

<tr><td>720</td>
<td>720</td>
<td>720</td>
<td>609,69 MB/s</td>
</tr>
</table>

E hello, gráfico a seguir mostra uma visualização de relação de saudação entre SUs e taxa de transferência.

![img.stream.analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a>Obter ajuda
Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->

[img.stream.analytics.monitor.job]: ./media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor-NewPortal.png
[img.stream.analytics.configure.scale]: ./media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: ./media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings-NewPortal.png   

<!--Link references-->

[microsoft.support]: http://support.microsoft.com
[azure.management.portal]: http://manage.windowsazure.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

