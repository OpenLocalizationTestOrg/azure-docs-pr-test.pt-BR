---
title: entradas de amostragem AAA no Azure Stream Analytics | Microsoft Docs
description: Identificar problemas ao solucionar problemas em trabalhos do Stream Analytics.
keywords: "entrada de solução de problemas, amostragem de entrada"
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
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 9637a8664de099eebb8f5654036d2957f4c6b7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a>Amostragem do fluxo de entrada do Stream Analytics do Azure

Usando o Azure Stream Analytics, você pode criar amostra eventos de entrada que vêm de um arquivo e testar as consultas no portal de saudação sem a necessidade de toostart ou interromper um trabalho.

## <a name="testing-your-query"></a>Testando sua consulta

No painel de detalhes do trabalho do Stream Analytics hello, abra Olá **editor de consultas** folha clicando no nome de consulta de saudação em **consulta**. (Em nosso cenário de exemplo, porque nenhuma consulta tiver sido criada, clique em Olá **< >** espaço reservado.)

![editor de consultas de análise de fluxo de saudação](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

folha de editor avançado Olá para criar sua consulta é exibida como era na versão anterior do hello. Agora folha Olá foi atualizada com um novo painel esquerdo que mostra Olá entradas e saídas que são usadas pela consulta hello e definidas para este trabalho.

![editor de consultas de análise de fluxo de saudação as entradas e saídas de listas](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

São mostradas também uma entrada adicional e uma saída, que não são definidas. Eles vêm Olá novo modelo de consulta que começam com. Alterar, ou até mesmo desaparecer completamente, como editar consulta hello. Você pode ignorá-las com segurança por ora.

tootest com dados de entrada de exemplo, qualquer uma das suas entradas e, em seguida, selecione **carregar dados de exemplo do arquivo**.

![Olá dados de exemplo do carregamento do Stream Analytics consulta editor de comando de arquivo](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

Após a conclusão do carregamento de saudação, clique em **teste** tootest esta consulta em relação a saudação amostra dos dados que você forneceu.

![botão de teste Olá Stream Analytics query editor](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

Se você quiser saída do teste Olá toosave para uso posterior, a saída de saudação da consulta é exibida no navegador de saudação com resultados do download de toohello um link. Você pode facilmente e iterativamente modificar sua consulta e testá-lo repetidamente toosee como saída de hello é alterado.

![A saída do exemplo do editor de consultas do Stream Analytics](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

Olá anterior a imagem, uma segunda saída foi adicionada, chamado **HighAvgTempOutput**.

Quando você usa várias saídas em uma consulta, você pode ver os resultados de saudação para cada saída separadamente e alternar facilmente entre eles.

Depois que você estiver satisfeito com os resultados de Olá, você pode salvar sua consulta, iniciar o trabalho, sente-se e assista magic Olá da análise de fluxo de.

## <a name="get-help"></a>Obter ajuda

Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
