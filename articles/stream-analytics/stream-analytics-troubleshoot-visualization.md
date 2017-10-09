---
title: aaaVisualize e solucionar problemas de trabalhos do Stream Analytics | Microsoft Docs
description: "Saiba como toovisualize um trabalho de análise de fluxo de pipeline para solução de problemas usando o recurso de diagrama de diagnóstico de saudação de autoatendimento."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: d87841cd-c59f-4a46-b46e-8b904fdc12e9
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 8a6715be601fdc47b8d9caf4112da161dad22618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a>Visualizar e solucionar problemas com trabalhos do Stream Analytics
No Stream Analytics, assim como acontece com outras tecnologias baseadas em nuvem, solução de problemas às vezes, é necessário toolook em por que um trabalho não produz saída de hello esperado (ou qualquer saída para essa finalidade). Com isso em mente, o Stream Analytics fornece a capacidade de saudação para a visualização de um trabalho de streaming. Isso também é útil como uma ferramenta de modelagem e tem Olá benefício adicional para aqueles que exigem a documentação de seu trabalho.

Na visualização de saudação entradas de saudação do painel são visíveis, bem como a consulta hello está sendo executada e, em seguida, todas as saídas de saudação configurado. Problemas de conectividade ou a configuração se tornam mais aparentes e também pode ser útil toosee uma representação visual da sua configuração.

## <a name="using-hello-diagnosis-diagram-tool"></a>Usando a ferramenta de diagrama de diagnóstico Olá
tooaccess esse visualizador, basta clicar na Olá botão "Diagrama de diagnóstico" hello folha "Configurações" da saudação do trabalho de análise de fluxo de saudação.

![stream-analytics-troubleshoot-visualization-diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

Cada entrada e saída é codificado por cores tooindicate Olá estado atual desse componente, conforme mostrado abaixo.

![stream-analytics-troubleshoot-visualization-input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

Quando o usuário de saudação quiser toolook consulta intermediário etapas toounderstand Olá dados fluxo padrões dentro de um trabalho, ferramenta de visualização Olá fornece uma exibição de análise de saudação da consulta Olá em suas etapas de componentes e a sequência de fluxo de saudação. Clicando em cada etapa de consulta mostrará a seção correspondente de saudação em uma consulta de editar o painel conforme ilustrado. 

![stream-analytics-troubleshoot-visualization-intermediate-steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

