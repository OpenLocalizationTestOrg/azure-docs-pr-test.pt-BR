---
title: "funções de janela de análise de tooStream aaaIntroduction | Microsoft Docs"
description: "Saiba mais sobre as três funções de janela Olá no Stream Analytics (em cascata, de salto, deslizante)."
keywords: janela em cascata, janela deslizante, janela de salto
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 7fc36eb9afb2b28e2791d925d26923145eb38074
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toostream-analytics-window-functions"></a>Funções de janela de análise de tooStream de Introdução
Em cenários de streaming em tempo real muitos, é operações de tooperform necessário apenas em dados de saudação contidos no windows temporal. O suporte nativo para funções de janelamento é um recurso principal do Azure Stream Analytics que move agulha Olá na produtividade do desenvolvedor na criação de trabalhos de processamento de fluxo complexas. Análise de fluxo permite que os desenvolvedores toouse [ **em cascata**](https://msdn.microsoft.com/library/dn835055.aspx), [ **Hopping** ](https://msdn.microsoft.com/library/dn835041.aspx) e [ **deslizante** ](https://msdn.microsoft.com/library/dn835051.aspx) operações temporais do windows tooperform no fluxo de dados. Vale a pena observar que todos os [janela](https://msdn.microsoft.com/library/dn835019.aspx) operações enviar os resultados em Olá **final** da janela de saudação. saída de saudação da janela Olá será evento único com base na função de agregação Olá usada. evento Olá terá o carimbo de hora de saudação do final de saudação da janela de saudação e todas as funções de janela são definidas com um comprimento fixo. Por último é toonote importante que todas as funções de janela devem ser usadas em uma [ **GROUP BY** ](https://msdn.microsoft.com/library/dn835023.aspx) cláusula.

![Conceitos de funções de Janela do Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a>Janela em Cascata
Funções de janela em cascata são usado toosegment um fluxo de dados em segmentos distintos de tempo e executam uma função em relação a elas, como o exemplo hello abaixo. principais diferenciais saudação de uma janela em cascata são que eles se repetir, não se sobrepõem e um evento não pode pertencer toomore que uma janela em cascata.

![Introdução às funções de Janela em cascata do Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a>Janela de Salto
As funções da Janela de Salto pulam para frente um período fixo no tempo. Pode ser fácil toothink-los como janelas em cascata que podem se sobrepor, portanto eventos podem pertencer a toomore de um conjunto de resultados de janela Hopping. toomake uma janela Hopping Olá mesmo como uma janela em cascata um especificaria simplesmente toobe de tamanho de salto Olá Olá mesmo como o tamanho da janela hello. 

![Introdução às funções de Janela de salto do Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a>Janela Deslizante
As funções da Janela Deslizante, diferentemente das Janelas em Cascata e de Salto, produzem uma saída **apenas** quando um evento ocorre. Cada janela terá pelo menos um evento e Olá continuamente avança por um € (épsilon). Como as janelas de salto, eventos podem pertencer toomore que uma janela deslizante.

![Introdução às funções de Janela deslizante do Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a>Obtendo ajuda com funções de janela
Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

