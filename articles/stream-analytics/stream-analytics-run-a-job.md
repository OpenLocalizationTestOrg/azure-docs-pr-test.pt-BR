---
title: toostart aaaHow streaming trabalhos no Stream Analytics | Microsoft Docs
description: Como executar um trabalho de streaming no Stream Analytics do Azure | segmento do roteiro de aprendizagem.
keywords: trabalhos de streaming
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9d46950f-2b69-49ce-a567-df558c5dd820
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 67aa14860c38cbd0535d0ec4f23729445d0185c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-streaming-job-in-azure-stream-analytics"></a>Como toorun um fluxo de trabalho no Azure Stream Analytics
Quando um trabalho de entrada, saída e consulta todos os foram especificados que você pode iniciar o trabalho de análise de fluxo de saudação.

toostart seu trabalho:

1. No portal clássico do Azure hello, no painel de trabalho hello, clique em **iniciar** final Olá Olá página.
   
   ![Botão Iniciar trabalho](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   No portal do Azure de Olá, clique em **iniciar** na parte superior de saudação da sua página de trabalho.
   
   ![Botão Iniciar trabalho no Portal do Azure](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. Especifique um **iniciar saída** toodetermine valor quando esse trabalho iniciará a produzir a saída. Olá configuração padrão para trabalhos que não foram iniciados anteriormente é **hora de início do trabalho**, que significa que o trabalho Olá imediatamente Iniciar processamento de dados. Você também pode especificar um **personalizado** tempo no hello passado (para consumir dados históricos) ou Olá futura (toodelay processamento até que um tempo futuro). Para casos em que um trabalho foi anteriormente iniciado e interrompido, Olá opção **hora da última interrupção** está disponível no trabalho de saudação tooresume ordem de saudação última hora de saída e evitar a perda de dados.  
   
   ![Hora de início do trabalho de streaming](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Hora de início do trabalho de transmissão no Portal do Azure](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. Confirme sua seleção. status do trabalho Olá alterará muito*iniciando* e em breve moverá muito*executando* depois que o trabalho Olá foi iniciado. Você pode monitorar o progresso de saudação da saudação **iniciar** operação em Olá **Hub de notificação**:
   
   ![andamento do trabalho de streaming](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Andamento do trabalho de transmissão no Portal do Azure](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a>Obter ajuda
Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

