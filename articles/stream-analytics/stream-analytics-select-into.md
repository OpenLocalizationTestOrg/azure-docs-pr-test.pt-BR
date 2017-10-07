---
title: consultas aaaDebug Stream Analytics do Azure usando SELECT INTO | Microsoft Docs
description: "Consulta intermediária com dados de exemplo usando instruções SELECT INTO no Stream Analytics"
keywords: 
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 27e41af1a6ea06b4509d07a3a67087490d0ec1fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a>Depurar consultas usando instruções SELECT INTO

No processamento de dados em tempo real, saber quais dados Olá parece no meio de saudação do hello consulta pode ser úteis. Como as entradas ou etapas de um trabalho do Stream Analytics do Azure podem ser lidas várias vezes, você pode escrever instruções SELECT INTO extras. Isso gera dados intermediários para armazenamento e permite que você inspecione a exatidão de saudação do dados hello, assim como *Assista variáveis* quando você depura um programa.

## <a name="use-select-into-toocheck-hello-data-stream"></a>Use SELECT INTO toocheck Olá fluxo de dados

Olá seguinte exemplo de consulta em um trabalho do Stream Analytics do Azure tem um fluxo de entrada, duas entradas de dados de referência e uma saída tooAzure armazenamento de tabela. consulta de saudação associa dados de hub de eventos hello e dois blobs tooget Olá nome e categoria de informações de referência:

![Exemplo de consulta SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

Observe que Olá trabalho está em execução, mas nenhum evento sendo produzido na saída de hello. Em Olá **monitoramento** lado a lado, mostrada aqui, você pode ver que a entrada hello está produzindo dados, mas você não souber qual etapa da saudação **INGRESSAR** causado todos Olá toobe eventos descartado.

![bloco de monitoramento de saudação](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
Nessa situação, você pode adicionar alguns extras instruções SELECT INTO muito "" resultados intermediários de junção hello e dados de saudação que será lido da entrada hello.

Neste exemplo, adicionamos duas novas "saídas temporárias". Elas podem ser qualquer coletor desejado. Aqui, usamos o Armazenamento do Azure como um exemplo:

![Adicionando instruções SELECT INTO extras](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

Em seguida, você pode reescrever consulta hello como esta:

![Consulta SELECT INTO reescrita](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

Agora, iniciar o trabalho de saudação e permitir sua execução por alguns minutos. Em seguida, consulta temp1 e temp2 com saudação do Visual Studio Cloud Explorer tooproduce tabelas a seguir:

**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)

**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)

Como você pode ver, temp1 e temp2 tem dados e coluna de nome de saudação é populada corretamente em temp2. No entanto, como ainda não há dados na saída, algo está errado:

![SELECT INTO output1 table with no data](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

Por Olá dados de amostra, você pode ser quase certo de que o problema de saudação é com hello segundo junção. Você pode baixar dados de referência de saudação do blob hello e dar uma olhada:

![SELECT INTO ref table](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

Como você pode ver, o formato de saudação do hello GUID nesses dados de referência é diferente do formato de saudação do hello [] na coluna temp2. É por isso que dados saudação não chegarem na output1 conforme o esperado.

Você pode corrigir o formato de dados hello, carregá-lo tooreference blob e tente novamente:

![SELECT INTO temp table](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

Neste momento, dados de saudação na saída de hello são formatados e preenchidos conforme o esperado.

![SELECT INTO final table](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a>Obter ajuda

Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas

* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

