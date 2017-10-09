---
title: "testes de consulta de análise de fluxo de aaaAzure | Microsoft Docs"
description: Como tootest suas consultas em trabalhos do Stream Analytics.
keywords: testar consulta, solucionar problemas da consulta
documentation center: 
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
ms.openlocfilehash: 3b141d98332fdc170e696e181c8446796a86f78e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-stream-analytics-queries-in-hello-azure-portal"></a>Testar as consultas de análise de fluxo do Azure em Olá portal do Azure

Com o Azure Stream Analytics, você pode testar as consultas em Olá portal do Azure sem a necessidade de toostart ou interromper um trabalho.

## <a name="test-hello-input"></a>Entrada de saudação do teste

1. tootest com dados de entrada de exemplo, qualquer uma das suas entradas e, em seguida, selecione **carregar dados de exemplo do arquivo**.

    ![consulta de teste do editor de consultas do stream analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. Após a conclusão do carregamento de saudação, clique em **teste** tootest esta consulta em relação a saudação amostra dos dados que você forneceu.

    ![dados de exemplo de teste do editor de consultas do stream analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

saída de Hello da consulta é exibida no navegador hello, com um link para Download resultados você deseja saída do teste Olá toosave para uso posterior. Você pode facilmente e iterativamente modificar sua consulta e testá-lo repetidamente toosee como saída de hello é alterado.

![A saída do exemplo do editor de consultas do Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

Com várias saídas usadas em uma consulta, você pode ver os resultados de saudação para ambas as saídas separadamente e alternar facilmente entre eles.

Quando estiver satisfeito com os resultados de Olá mostrados no navegador hello, salvar sua consulta, iniciar o trabalho e permitem que ele processa os eventos sem erro.

## <a name="get-help"></a>Obter ajuda

Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas

* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
