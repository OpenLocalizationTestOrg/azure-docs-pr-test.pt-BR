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
# <a name="debug-your-model-in-azure-machine-learning"></a><span data-ttu-id="c8144-103">Depurar seu modelo no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c8144-103">Debug your Model in Azure Machine Learning</span></span>

<span data-ttu-id="c8144-104">Este artigo explica os possíveis motivos de saudação por qualquer uma das Olá após duas falhas podem ser encontrada durante a execução de um modelo:</span><span class="sxs-lookup"><span data-stu-id="c8144-104">This article explains hello potential reasons why either of hello following two failures might be encountered when running a model:</span></span>

* <span data-ttu-id="c8144-105">Olá [treinar modelo] [ train-model] módulo produz um erro</span><span class="sxs-lookup"><span data-stu-id="c8144-105">hello [Train Model][train-model] module produces an error</span></span> 
* <span data-ttu-id="c8144-106">Olá [modelo de pontuação] [ score-model] módulo produz resultados incorretos</span><span class="sxs-lookup"><span data-stu-id="c8144-106">hello [Score Model][score-model] module produces incorrect results</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a><span data-ttu-id="c8144-107">O módulo Modelo de Treinamento produz um erro</span><span class="sxs-lookup"><span data-stu-id="c8144-107">Train Model Module produces an error</span></span>

![image1](./media/machine-learning-debug-models/train_model-1.png)

<span data-ttu-id="c8144-109">Olá [treinar modelo] [ train-model] módulo espera duas entradas:</span><span class="sxs-lookup"><span data-stu-id="c8144-109">hello [Train Model][train-model] Module expects two inputs:</span></span>

1. <span data-ttu-id="c8144-110">tipo de saudação do modelo de aprendizado de máquina da coleção de saudação dos modelos fornecidos pelo aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8144-110">hello type of machine learning model from hello collection of models provided by Azure Machine Learning.</span></span>
2. <span data-ttu-id="c8144-111">dados de treinamento com uma coluna de rótulo especificado que especifica Olá Olá toopredict variável (hello outras colunas são consideradas toobe recursos).</span><span class="sxs-lookup"><span data-stu-id="c8144-111">hello training data with a specified Label column which specifies hello variable toopredict (hello other columns are assumed toobe Features).</span></span>

<span data-ttu-id="c8144-112">Esse módulo pode produzir um erro no hello casos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8144-112">This module can produce an error in hello following cases:</span></span>

1. <span data-ttu-id="c8144-113">coluna de rótulo Olá foi especificada incorretamente.</span><span class="sxs-lookup"><span data-stu-id="c8144-113">hello Label column is specified incorrectly.</span></span> <span data-ttu-id="c8144-114">Isso pode ocorrer se mais de uma coluna é selecionada como Olá rótulo ou um índice de coluna incorreto é selecionado.</span><span class="sxs-lookup"><span data-stu-id="c8144-114">This can happen if either more than one column is selected as hello Label or an incorrect column index is selected.</span></span> <span data-ttu-id="c8144-115">Por exemplo, caso segundo Olá se aplica quando um índice de coluna de 30 é usado com um conjunto de dados de entrada que tem apenas 25 colunas.</span><span class="sxs-lookup"><span data-stu-id="c8144-115">For example, hello second case would apply if a column index of 30 is used with an input dataset which has only 25 columns.</span></span>

2. <span data-ttu-id="c8144-116">Olá dataset não contém nenhuma coluna de recurso.</span><span class="sxs-lookup"><span data-stu-id="c8144-116">hello dataset does not contain any Feature columns.</span></span> <span data-ttu-id="c8144-117">Por exemplo, se o conjunto de dados de entrada hello tem apenas uma coluna, que é marcada como coluna de rótulo hello, não haveria nenhum recurso com o modelo de saudação toobuild.</span><span class="sxs-lookup"><span data-stu-id="c8144-117">For example, if hello input dataset has only one column, which is marked as hello Label column, there would be no features with which toobuild hello model.</span></span> <span data-ttu-id="c8144-118">Nesse caso, Olá [treinar modelo] [ train-model] módulo produz um erro.</span><span class="sxs-lookup"><span data-stu-id="c8144-118">In this case, hello [Train Model][train-model] module produces an error.</span></span>

3. <span data-ttu-id="c8144-119">dataset de entrada Hello (recursos ou rótulo) contém infinito como um valor.</span><span class="sxs-lookup"><span data-stu-id="c8144-119">hello input dataset (Features or Label) contains Infinity as a value.</span></span>

## <a name="score-model-module-produces-incorrect-results"></a><span data-ttu-id="c8144-120">O Módulo Modelo de Pontuação produz resultados incorretos</span><span class="sxs-lookup"><span data-stu-id="c8144-120">Score Model Module produces incorrect results</span></span>

![image2](./media/machine-learning-debug-models/train_test-2.png)

<span data-ttu-id="c8144-122">Em uma experiência típica do treinamento/teste de aprendizado supervisionado, Olá [dividir dados] [ split] módulo divide o conjunto de dados original Olá em duas partes: uma parte é o modelo de saudação do tootrain usados e uma parte é usada tooscore como modelo treinado Olá executa.</span><span class="sxs-lookup"><span data-stu-id="c8144-122">In a typical training/testing experiment for supervised learning, hello [Split Data][split] module divides hello original dataset into two parts: one part is used tootrain hello model and one part is used tooscore how well hello trained model performs.</span></span> <span data-ttu-id="c8144-123">modelo treinado Olá for usado tooscore Olá dados de teste, após o qual resultados Olá são toodetermine avaliado Olá precisão do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c8144-123">hello trained model is then used tooscore hello test data, after which hello results are evaluated toodetermine hello accuracy of hello model.</span></span>

<span data-ttu-id="c8144-124">Olá [modelo de pontuação] [ score-model] módulo requer duas entradas:</span><span class="sxs-lookup"><span data-stu-id="c8144-124">hello [Score Model][score-model] module requires two inputs:</span></span>

1. <span data-ttu-id="c8144-125">Uma saída de modelo treinado de saudação [treinar modelo] [ train-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="c8144-125">A trained model output from hello [Train Model][train-model] module.</span></span>
2. <span data-ttu-id="c8144-126">Um conjunto de dados de pontuação que é diferente do conjunto de dados Olá usado tootrain modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c8144-126">A scoring dataset that is different from hello dataset used tootrain hello model.</span></span>

<span data-ttu-id="c8144-127">Ele do possível, embora a experiência de saudação for bem-sucedida, Olá [modelo de pontuação] [ score-model] módulo produz resultados incorretos.</span><span class="sxs-lookup"><span data-stu-id="c8144-127">It's possible that even though hello experiment succeeds, hello [Score Model][score-model] module produces incorrect results.</span></span> <span data-ttu-id="c8144-128">Vários cenários podem causar esse toohappen:</span><span class="sxs-lookup"><span data-stu-id="c8144-128">Several scenarios may cause this toohappen:</span></span>

1. <span data-ttu-id="c8144-129">Se Olá especificado rótulo for categórico e a um modelo de regressão é treinado nos dados hello, uma saída incorreta seria produzida por Olá [modelo de pontuação] [ score-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="c8144-129">If hello specified Label is categorical and a regression model is trained on hello data, an incorrect output would be produced by hello [Score Model][score-model] module.</span></span> <span data-ttu-id="c8144-130">Isso ocorre porque a regressão requer uma variável de resposta contínua.</span><span class="sxs-lookup"><span data-stu-id="c8144-130">This is because regression requires a continuous response variable.</span></span> <span data-ttu-id="c8144-131">Nesse caso, seria mais adequado toouse um modelo de classificação.</span><span class="sxs-lookup"><span data-stu-id="c8144-131">In this case, it would be more suitable toouse a classification model.</span></span> 

2. <span data-ttu-id="c8144-132">Da mesma forma, se um modelo de classificação é treinado em um conjunto de dados com números de ponto flutuante na coluna de rótulo hello, ele pode produzir resultados indesejáveis.</span><span class="sxs-lookup"><span data-stu-id="c8144-132">Similarly, if a classification model is trained on a dataset having floating point numbers in hello Label column, it may produce undesirable results.</span></span> <span data-ttu-id="c8144-133">Isso ocorre porque a classificação exige uma variável de resposta discreta que permite somente valores que variam em um conjunto finito e, normalmente, um conjunto pequeno de classes.</span><span class="sxs-lookup"><span data-stu-id="c8144-133">This is because classification requires a discrete response variable that only allows values that range over a finite, and usually somewhat small, set of classes.</span></span>

3. <span data-ttu-id="c8144-134">Se Olá pontuação dataset não contém todos os modelos de Olá Olá recursos usados tootrain, Olá [modelo de pontuação] [ score-model] produz um erro.</span><span class="sxs-lookup"><span data-stu-id="c8144-134">If hello scoring dataset does not contain all hello features used tootrain hello model, hello [Score Model][score-model] produces an error.</span></span>

4. <span data-ttu-id="c8144-135">Se uma linha hello pontuação de conjunto de dados contiver um valor ausente ou um valor infinito para qualquer um dos seus recursos, Olá [modelo de pontuação] [ score-model] não produzirá nenhuma saída correspondente toothat linha.</span><span class="sxs-lookup"><span data-stu-id="c8144-135">If a row in hello scoring dataset contains a missing value or an infinite value for any of its features, hello [Score Model][score-model] will not produce any output corresponding toothat row.</span></span>

5. <span data-ttu-id="c8144-136">Olá [modelo de pontuação] [ score-model] pode produzir resultados idênticos para todas as linhas da saudação pontuação de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="c8144-136">hello [Score Model][score-model] may produce identical outputs for all rows in hello scoring dataset.</span></span> <span data-ttu-id="c8144-137">Isso pode ocorrer, por exemplo, durante a tentativa de classificação usando florestas de decisão se o número mínimo de saudação de amostras por nó folha é escolhido toobe mais de saudação número de exemplos de treinamento disponíveis.</span><span class="sxs-lookup"><span data-stu-id="c8144-137">This could occur, for example, when attempting classification using Decision Forests if hello minimum number of samples per leaf node is chosen toobe more than hello number of training examples available.</span></span>

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

