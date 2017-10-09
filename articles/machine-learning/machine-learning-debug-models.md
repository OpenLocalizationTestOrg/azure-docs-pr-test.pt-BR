---
title: "aaaDebug seu modelo no aprendizado de máquina do Azure | Microsoft Docs"
description: "Como erros toodebug produzido pelo modelo de treinamento e o modelo de pontuação módulos no aprendizado de máquina do Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 629dc45e-ac1e-4b7d-b120-08813dc448be
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bradsev;garye
ms.openlocfilehash: ee38ca8ce38d4fc7add5ba70c80ab9bb2ceaf1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-model-in-azure-machine-learning"></a>Depurar seu modelo no Azure Machine Learning

Este artigo explica os possíveis motivos de saudação por qualquer uma das Olá após duas falhas podem ser encontrada durante a execução de um modelo:

* Olá [treinar modelo] [ train-model] módulo produz um erro 
* Olá [modelo de pontuação] [ score-model] módulo produz resultados incorretos 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a>O módulo Modelo de Treinamento produz um erro

![image1](./media/machine-learning-debug-models/train_model-1.png)

Olá [treinar modelo] [ train-model] módulo espera duas entradas:

1. tipo de saudação do modelo de aprendizado de máquina da coleção de saudação dos modelos fornecidos pelo aprendizado de máquina do Azure.
2. dados de treinamento com uma coluna de rótulo especificado que especifica Olá Olá toopredict variável (hello outras colunas são consideradas toobe recursos).

Esse módulo pode produzir um erro no hello casos a seguir:

1. coluna de rótulo Olá foi especificada incorretamente. Isso pode ocorrer se mais de uma coluna é selecionada como Olá rótulo ou um índice de coluna incorreto é selecionado. Por exemplo, caso segundo Olá se aplica quando um índice de coluna de 30 é usado com um conjunto de dados de entrada que tem apenas 25 colunas.

2. Olá dataset não contém nenhuma coluna de recurso. Por exemplo, se o conjunto de dados de entrada hello tem apenas uma coluna, que é marcada como coluna de rótulo hello, não haveria nenhum recurso com o modelo de saudação toobuild. Nesse caso, Olá [treinar modelo] [ train-model] módulo produz um erro.

3. dataset de entrada Hello (recursos ou rótulo) contém infinito como um valor.

## <a name="score-model-module-produces-incorrect-results"></a>O Módulo Modelo de Pontuação produz resultados incorretos

![image2](./media/machine-learning-debug-models/train_test-2.png)

Em uma experiência típica do treinamento/teste de aprendizado supervisionado, Olá [dividir dados] [ split] módulo divide o conjunto de dados original Olá em duas partes: uma parte é o modelo de saudação do tootrain usados e uma parte é usada tooscore como modelo treinado Olá executa. modelo treinado Olá for usado tooscore Olá dados de teste, após o qual resultados Olá são toodetermine avaliado Olá precisão do modelo de saudação.

Olá [modelo de pontuação] [ score-model] módulo requer duas entradas:

1. Uma saída de modelo treinado de saudação [treinar modelo] [ train-model] módulo.
2. Um conjunto de dados de pontuação que é diferente do conjunto de dados Olá usado tootrain modelo de saudação.

Ele do possível, embora a experiência de saudação for bem-sucedida, Olá [modelo de pontuação] [ score-model] módulo produz resultados incorretos. Vários cenários podem causar esse toohappen:

1. Se Olá especificado rótulo for categórico e a um modelo de regressão é treinado nos dados hello, uma saída incorreta seria produzida por Olá [modelo de pontuação] [ score-model] módulo. Isso ocorre porque a regressão requer uma variável de resposta contínua. Nesse caso, seria mais adequado toouse um modelo de classificação. 

2. Da mesma forma, se um modelo de classificação é treinado em um conjunto de dados com números de ponto flutuante na coluna de rótulo hello, ele pode produzir resultados indesejáveis. Isso ocorre porque a classificação exige uma variável de resposta discreta que permite somente valores que variam em um conjunto finito e, normalmente, um conjunto pequeno de classes.

3. Se Olá pontuação dataset não contém todos os modelos de Olá Olá recursos usados tootrain, Olá [modelo de pontuação] [ score-model] produz um erro.

4. Se uma linha hello pontuação de conjunto de dados contiver um valor ausente ou um valor infinito para qualquer um dos seus recursos, Olá [modelo de pontuação] [ score-model] não produzirá nenhuma saída correspondente toothat linha.

5. Olá [modelo de pontuação] [ score-model] pode produzir resultados idênticos para todas as linhas da saudação pontuação de conjunto de dados. Isso pode ocorrer, por exemplo, durante a tentativa de classificação usando florestas de decisão se o número mínimo de saudação de amostras por nó folha é escolhido toobe mais de saudação número de exemplos de treinamento disponíveis.

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

