---
title: Testes de consulta do Stream Analytics do Azure | Microsoft Docs
description: Como testar as consultas em trabalhos do Stream Analytics.
keywords: testar consulta, solucionar problemas da consulta
documentation center: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: samacha
ms.openlocfilehash: 2898e3404dcfa3d75e3920f9c83e4efa7201998e
ms.sourcegitcommit: 3cdc82a5561abe564c318bd12986df63fc980a5a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="test-azure-stream-analytics-queries-in-the-azure-portal"></a>Testar as consultas do Stream Analytics do Azure no portal do Azure

Com o Stream Analytics do Azure, você pode testar consultas no portal do Azure sem a necessidade de iniciar ou interromper um trabalho.

## <a name="test-the-input"></a>Testar a entrada

1. Para testar com dados de entrada de exemplo, clique com o botão direito do mouse em qualquer uma de suas entradas e, em seguida, selecione **Carregar dados de exemplo do arquivo**. No momento, você pode carregar apenas os dados formatados em JSON. Se os dados estiverem em um formato diferente, como CSV, você deverá convertê-los em JSON antes de carregar. Você pode usar qualquer ferramenta de conversão de código-fonte aberto, como [conversor de CSV para JSON](http://www.convertcsv.com/csv-to-json.htm), para converter seus dados em JSON.

    ![consulta de teste do editor de consultas do stream analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. Depois que o upload for concluído, clique em **Teste** para testar essa consulta em relação aos dados de exemplo que você forneceu.

    ![dados de exemplo de teste do editor de consultas do stream analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

A saída da consulta é exibida no navegador com um link Baixar resultados, caso você queira salvar a saída do teste para uso posterior. Agora você pode modificar fácil e iterativamente sua consulta e testá-la repetidamente para ver como a saída muda.

![A saída do exemplo do editor de consultas do Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

Com várias saídas usadas em uma consulta, você pode ver os resultados de ambas as saídas separadamente e alterná-los facilmente.

Quando estiver satisfeito com os resultados mostrados no navegador, você poderá salvar sua consulta, iniciar seu trabalho e deixá-lo processar os eventos sem erro.

## <a name="get-help"></a>Obter ajuda

Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas

* [Introdução ao Stream Analytics do Azure](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
