---
title: "aaaOptimize seus algoritmos de aprendizado de máquina do Azure | Microsoft Docs"
description: "Explica como o parâmetro de ideal de saudação do toochoose definido por um algoritmo no aprendizado de máquina do Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6717e30e-b8d8-4cc1-ad0b-1d4727928d32
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: fbf2f71abdbce19483fb048d67a39cbb368a928e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-parameters-toooptimize-your-algorithms-in-azure-machine-learning"></a>Escolher parâmetros toooptimize seus algoritmos de aprendizado de máquina do Azure
Este tópico descreve como toochoose Olá direito hyperparameter definido por um algoritmo no aprendizado de máquina do Azure. A maioria dos algoritmos de aprendizagem de máquina tem tooset de parâmetros. Quando você treina um modelo, você precisa tooprovide valores para esses parâmetros. eficácia de saudação do modelo treinado Olá depende de parâmetros de modelo de saudação que você escolher. Olá processo de localização de conjunto de parâmetros de saudação ideal é conhecido como *seleção de modelo*.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Não há seleção do modelo de toodo de várias maneiras. No aprendizado de máquina, a validação cruzada é um dos métodos de hello mais amplamente usado para seleção de modelo e é o mecanismo de seleção de modelo saudação padrão no aprendizado de máquina do Azure. Como o Azure Machine Learning dá suporte a R e Python, você sempre pode implementar seus próprios mecanismos de seleção de modelo usando R ou Python.

Há quatro etapas no processo de saudação de localização Olá melhor conjunto de parâmetros:

1. **Definir o espaço de parâmetro hello**: algoritmo hello, primeiro decida valores de parâmetro exata Olá desejados tooconsider.
2. **Definir configurações de validação cruzada Olá**: decidir como validação cruzada toochoose dobra de saudação de conjunto de dados.
3. **Definir a métrica de saudação**: decidir quais toouse métrica para determinar melhor o conjunto de parâmetros, como precisão hello, pontuação f, precisão, lembre-se ou erro ao quadrado da média de raiz.
4. **Treinar, avaliar e comparar**: para cada combinação exclusiva de valores de parâmetro hello, validação cruzada é realizada pela e com base na métrica de erro Olá você definir. Depois de avaliação e comparação, você pode escolher o modelo de melhor desempenho de saudação.

Olá a imagem a seguir ilustra mostra como isso pode ser obtido no aprendizado de máquina do Azure.

![Localizar o melhor conjunto de parâmetro hello](./media/machine-learning-algorithm-parameters-optimize/fig1.png)

## <a name="define-hello-parameter-space"></a>Definir o espaço de parâmetro hello
Você pode definir o parâmetro hello definido na etapa de inicialização do modelo de saudação. Painel de parâmetro de todos os algoritmos de aprendizado de máquina Hello tem dois modos de aprendizagem: *único parâmetro* e *intervalo de parâmetro*. Escolha o modo de Intervalo de Parâmetros. No modo de intervalo de parâmetros, você pode inserir vários valores para cada parâmetro. Você pode inserir valores separados por vírgula na caixa de texto de saudação.

![Árvore de decisão aumentada de duas classes, parâmetro único](./media/machine-learning-algorithm-parameters-optimize/fig2.png)

 Como alternativa, você pode definir pontos de mínimo e máximo de saudação da grade de saudação e o número total de saudação de pontos toobe gerado com **Use intervalo construtor**. Por padrão, os valores de parâmetro hello são gerados em uma escala linear. Mas se **escala logarítmica** estiver marcada, Olá valores são gerados na escala de log hello (ou seja, Olá taxa de pontos adjacentes Olá é constante em vez de seu diferença). Para parâmetros de inteiros, você pode definir um intervalo usando um hífen. Por exemplo, "1-10" significa que todos os números inteiros entre 1 e 10 (ambos incluídos) formam o conjunto de parâmetros de saudação. Um modo misto também tem suporte. Olá, por exemplo, o conjunto de parâmetros "1-10, 20, 50" incluiria inteiros de 1 a 10, 20 e 50.

![Árvore de decisão aumentada de duas classes, intervalo de parâmetros](./media/machine-learning-algorithm-parameters-optimize/fig3.png)

## <a name="define-cross-validation-folds"></a>Definir dobras de validação cruzada
Olá [partição e exemplo] [ partition-and-sample] módulo pode ser usado toorandomly atribuir dobras toohello dados. Em Olá a seguinte configuração de exemplo para o módulo hello, definimos cinco dobras e atribuir aleatoriamente uma partição número toohello de instâncias de exemplo.

![Partição e exemplo](./media/machine-learning-algorithm-parameters-optimize/fig4.png)

## <a name="define-hello-metric"></a>Definir a métrica de saudação
Olá [ajustar o modelo de Hiperparâmetros] [ tune-model-hyperparameters] módulo fornece suporte para a escolha empiricamente Olá melhor conjunto de parâmetros para um determinado algoritmo e um conjunto de dados. Além disso tooother informações sobre Olá de treinamento de modelo, hello **propriedades** painel deste módulo inclui métrica Olá para determinar o melhor conjunto de parâmetro hello. Ele tem duas caixas de listagem suspensas diferentes para algoritmos de classificação e regressão, respectivamente. Se Olá em questão é um algoritmo de classificação, métrica de regressão Olá será ignorada e vice-versa. Nesse exemplo específico, a métrica de saudação é **precisão**.   

![Parâmetros de limpeza](./media/machine-learning-algorithm-parameters-optimize/fig5.png)

## <a name="train-evaluate-and-compare"></a>Treinar, avaliar e comparar
Olá mesmo [ajustar o modelo de Hiperparâmetros] [ tune-model-hyperparameters] módulo treina todos os modelos de saudação que correspondem a toohello conjunto de parâmetros, avalia várias métricas e cria Olá melhor treinado com base em Olá métrica que você escolher. Este módulo tem duas entradas obrigatórias:

* aprendiz não treinado Olá
* saudação de conjunto de dados

o módulo de saudação também tem um conjunto de dados de entrada. Conecte o conjunto de dados de saudação com dobra informações toohello obrigatório do conjunto de dados de entrada. Se a saudação de conjunto de dados não está atribuído a qualquer informação de dobra, uma 10 vezes a validação cruzada é executada automaticamente por padrão. Se não for feita a atribuição de dobra hello e um conjunto de dados de validação é fornecido na porta de conjunto de dados opcional hello, em seguida, um modo de teste de treinamento é escolhido e Olá primeiro conjunto de dados é o modelo de saudação do tootrain usada para cada combinação de parâmetros.

![Classificador de árvore de decisão aumentada](./media/machine-learning-algorithm-parameters-optimize/fig6a.png)

modelo de Hello, em seguida, é avaliado no conjunto de dados de validação de saudação. Olá deixado porta de saída de hello módulo mostra diferentes métricas como funções de valores de parâmetro. Olá correto de porta de saída fornece treinado Olá correspondente toohello modelo melhor desempenho de acordo com o toohello escolhido métrica (**precisão** nesse caso).  

![Conjunto de dados de validação](./media/machine-learning-algorithm-parameters-optimize/fig6b.png)

Você pode ver os parâmetros exatos a saudação escolhidos visualizando Olá porta de saída à direita. Esse modelo pode ser usado na pontuação de um conjunto de teste ou em um serviço Web operacionalizado depois de salvá-lo como um modelo treinado.

<!-- Module References -->
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[tune-model-hyperparameters]: https://msdn.microsoft.com/library/azure/038d91b6-c2f2-42a1-9215-1f2c20ed1b40/
