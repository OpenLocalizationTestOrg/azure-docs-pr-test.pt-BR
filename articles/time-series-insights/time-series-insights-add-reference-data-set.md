---
title: "ambiente do Azure Insights de série de tempo do aaaAdd Referência conjunto de dados tooyour | Microsoft Docs"
description: "Neste tutorial, você adiciona o ambiente de informações da série de tempo de tooyour de conjunto de dados de referência"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 05e626ed81a22f2a8710b23a931ccd17c0f38ca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a>Criar um conjunto de dados de referência para o seu ambiente de informações da série de tempo usando o portal do Ibiza Olá

Um conjunto de dados de referência é uma coleção de itens que são aumentados com eventos de saudação da fonte de evento. O mecanismo de entrada da Análise de Séries Temporais une um evento da fonte de evento a um item em seu conjunto de dados de referência. Esse evento aumentado é disponibilizado para consulta. Essa junção for baseada em chaves de saudação definidas em seu conjunto de dados de referência.

## <a name="steps-tooadd-a-reference-data-set-tooyour-environment"></a>Etapas tooadd um ambiente de tooyour do conjunto de dados de referência

1. Entrar toohello [portal do Ibiza](https://portal.azure.com).
2. Clique em "Todos os recursos" no menu de saudação no lado esquerdo de saudação do portal do Ibiza hello.
3. Selecione o seu ambiente de Análise de Séries Temporais.

    ![Criar conjunto de dados de referência de informações da série de tempo de saudação](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. Selecione "Conjuntos de dados de referência" e clique em "+ Adicionar".

    ![Criar conjunto de dados de referência de informações da série de tempo de saudação - detalhes](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. Especifique o nome de Olá Olá referência do conjunto de dados.
6. Especifique o nome da chave hello e seu tipo. Este nome e o tipo é toopick usado Olá correto da propriedade de evento Olá na fonte de evento. Por exemplo, se você fornecer o nome da chave como "DeviceId" e digite como "String", em seguida, Olá Insights de série de tempo mecanismo de entrada procura uma propriedade com nome hello "DeviceId" do tipo "Cadeia de caracteres" no evento de entrada hello. Você pode fornecer mais de um toojoin chave evento hello. correspondência de nome de propriedade Olá diferencia maiusculas de minúsculas.

     ![Criar conjunto de dados de referência de informações da série de tempo de saudação - detalhes](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. Clique em “Criar”.

## <a name="next-steps"></a>Próximas etapas

* [Gerenciar dados de referência](time-series-insights-manage-reference-data-csharp.md) programaticamente.
* Para obter referência de API completa hello, consulte [API de dados de referência](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) documento.
