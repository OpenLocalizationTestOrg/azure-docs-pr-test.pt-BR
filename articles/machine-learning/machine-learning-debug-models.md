---
title: Depurar seu modelo no Machine Learning do Azure | Microsoft Docs
description: "Como depurar erros produzidos pelos módulos Modelo de Treinamento e Modelo de Pontuação no Azure Machine Learning."
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
ms.openlocfilehash: d4cc94a6395ea45bccf65d9a9f3118ec98cb258d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-model-in-azure-machine-learning"></a><span data-ttu-id="6eaaf-103">Depurar seu modelo no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6eaaf-103">Debug your Model in Azure Machine Learning</span></span>

<span data-ttu-id="6eaaf-104">Este artigo explica os motivos possíveis pelos quais uma das seguintes falhas pode ser encontrada durante a execução de um modelo:</span><span class="sxs-lookup"><span data-stu-id="6eaaf-104">This article explains the potential reasons why either of the following two failures might be encountered when running a model:</span></span>

* <span data-ttu-id="6eaaf-105">o módulo [Modelo de Treinamento][train-model] produz um erro</span><span class="sxs-lookup"><span data-stu-id="6eaaf-105">the [Train Model][train-model] module produces an error</span></span> 
* <span data-ttu-id="6eaaf-106">o módulo [Modelo de Pontuação][score-model] produz resultados incorretos</span><span class="sxs-lookup"><span data-stu-id="6eaaf-106">the [Score Model][score-model] module produces incorrect results</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a><span data-ttu-id="6eaaf-107">O módulo Modelo de Treinamento produz um erro</span><span class="sxs-lookup"><span data-stu-id="6eaaf-107">Train Model Module produces an error</span></span>

![image1](./media/machine-learning-debug-models/train_model-1.png)

<span data-ttu-id="6eaaf-109">O módulo [Modelo de Treinamento][train-model] espera duas entradas:</span><span class="sxs-lookup"><span data-stu-id="6eaaf-109">The [Train Model][train-model] Module expects two inputs:</span></span>

1. <span data-ttu-id="6eaaf-110">O tipo de modelo de aprendizado de máquina da coleção de modelos fornecida pelo Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="6eaaf-110">The type of machine learning model from the collection of models provided by Azure Machine Learning.</span></span>
2. <span data-ttu-id="6eaaf-111">Os dados de treinamento com uma coluna Rótulo especificada que especifica a variável a ser prevista (as outras colunas são consideradas Recursos).</span><span class="sxs-lookup"><span data-stu-id="6eaaf-111">The training data with a specified Label column which specifies the variable to predict (the other columns are assumed to be Features).</span></span>

<span data-ttu-id="6eaaf-112">Esse módulo pode produzir um erro nos seguintes casos:</span><span class="sxs-lookup"><span data-stu-id="6eaaf-112">This module can produce an error in the following cases:</span></span>

1. <span data-ttu-id="6eaaf-113">A coluna Rótulo foi especificada incorretamente.</span><span class="sxs-lookup"><span data-stu-id="6eaaf-113">The Label column is specified incorrectly.</span></span> <span data-ttu-id="6eaaf-114">Isso pode ocorrer se mais de uma coluna é selecionada como o Rótulo ou um índice de coluna incorreto está selecionado.</span><span class="sxs-lookup"><span data-stu-id="6eaaf-114">This can happen if either more than one column is selected as the Label or an incorrect column index is selected.</span></span> <span data-ttu-id="6eaaf-115">Por exemplo, o segundo caso será aplicável se um índice de coluna 30 for usado com um conjunto de dados de entrada que tem apenas 25 colunas.</span><span class="sxs-lookup"><span data-stu-id="6eaaf-115">For example, the second case would apply if a column index of 30 is used with an input dataset which has only 25 columns.</span></span>

2. <span data-ttu-id="6eaaf-116">O conjunto de dados não contém nenhuma coluna de Recurso.</span><span class="sxs-lookup"><span data-stu-id="6eaaf-116">The dataset does not contain any Feature columns.</span></span> <span data-ttu-id="6eaaf-117">Por exemplo, se o conjunto de dados de entrada tivesse apenas uma coluna, que é marcada como a coluna Rótulo, não haveria nenhum recurso com o qual compilar o modelo.</span><span class="sxs-lookup"><span data-stu-id="6eaaf-117">For example, if the input dataset has only one column, which is marked as the Label column, there would be no features with which to build the model.</span></span> <span data-ttu-id="6eaaf-118">Nesse caso, o módulo [Modelo de Treinamento][train-model] produz um erro.</span><span class="sxs-lookup"><span data-stu-id="6eaaf-118">In this case, the [Train Model][train-model] module produces an error.</span></span>

3. <span data-ttu-id="6eaaf-119">O conjunto de dados de entrada (Recursos ou Rótulo) contém Infinito como um valor.</span><span class="sxs-lookup"><span data-stu-id="6eaaf-119">The input dataset (Features or Label) contains Infinity as a value.</span></span>

## <a name="score-model-module-produces-incorrect-results"></a><span data-ttu-id="6eaaf-120">O Módulo Modelo de Pontuação produz resultados incorretos</span><span class="sxs-lookup"><span data-stu-id="6eaaf-120">Score Model Module produces incorrect results</span></span>

![image2](./media/machine-learning-debug-models/train_test-2.png)

<span data-ttu-id="6eaaf-122">Em um experimento típico de treinamento/teste de aprendizado supervisionado, o módulo [Dividir Dados][split] divide o conjunto de dados original em duas partes: uma parte é usada para treinar o modelo e a outra é usada para pontuar o desempenho do modelo treinado.</span><span class="sxs-lookup"><span data-stu-id="6eaaf-122">In a typical training/testing experiment for supervised learning, the [Split Data][split] module divides the original dataset into two parts: one part is used to train the model and one part is used to score how well the trained model performs.</span></span> <span data-ttu-id="6eaaf-123">O modelo treinado, em seguida, é usado para pontuar os dados de teste e, depois, os resultados são avaliados para determinar a precisão do modelo.</span><span class="sxs-lookup"><span data-stu-id="6eaaf-123">The trained model is then used to score the test data, after which the results are evaluated to determine the accuracy of the model.</span></span>

<span data-ttu-id="6eaaf-124">O módulo [Modelo de Pontuação][score-model] requer duas entradas:</span><span class="sxs-lookup"><span data-stu-id="6eaaf-124">The [Score Model][score-model] module requires two inputs:</span></span>

1. <span data-ttu-id="6eaaf-125">Uma saída do modelo treinado do módulo [Modelo de Treinamento][train-model].</span><span class="sxs-lookup"><span data-stu-id="6eaaf-125">A trained model output from the [Train Model][train-model] module.</span></span>
2. <span data-ttu-id="6eaaf-126">Um conjunto de dados de pontuação diferente do conjunto de dados usado para treinar o modelo.</span><span class="sxs-lookup"><span data-stu-id="6eaaf-126">A scoring dataset that is different from the dataset used to train the model.</span></span>

<span data-ttu-id="6eaaf-127">É possível que, mesmo que o experimento tenha sido bem-sucedido, o módulo [Modelo de Pontuação][score-model] produza resultados incorretos.</span><span class="sxs-lookup"><span data-stu-id="6eaaf-127">It's possible that even though the experiment succeeds, the [Score Model][score-model] module produces incorrect results.</span></span> <span data-ttu-id="6eaaf-128">Vários cenários podem causar isso:</span><span class="sxs-lookup"><span data-stu-id="6eaaf-128">Several scenarios may cause this to happen:</span></span>

1. <span data-ttu-id="6eaaf-129">Se o Rótulo especificado for categórico e um modelo de regressão for treinado nos dados, uma saída incorreta será produzida pelo módulo [Modelo de Pontuação][score-model].</span><span class="sxs-lookup"><span data-stu-id="6eaaf-129">If the specified Label is categorical and a regression model is trained on the data, an incorrect output would be produced by the [Score Model][score-model] module.</span></span> <span data-ttu-id="6eaaf-130">Isso ocorre porque a regressão requer uma variável de resposta contínua.</span><span class="sxs-lookup"><span data-stu-id="6eaaf-130">This is because regression requires a continuous response variable.</span></span> <span data-ttu-id="6eaaf-131">Nesse caso, deve ser mais adequado usar um modelo de classificação.</span><span class="sxs-lookup"><span data-stu-id="6eaaf-131">In this case, it would be more suitable to use a classification model.</span></span> 

2. <span data-ttu-id="6eaaf-132">Da mesma forma, se um modelo de classificação for treinado em um conjunto de dados com números de ponto flutuante na coluna Rótulo, ele pode produzir resultados indesejáveis.</span><span class="sxs-lookup"><span data-stu-id="6eaaf-132">Similarly, if a classification model is trained on a dataset having floating point numbers in the Label column, it may produce undesirable results.</span></span> <span data-ttu-id="6eaaf-133">Isso ocorre porque a classificação exige uma variável de resposta discreta que permite somente valores que variam em um conjunto finito e, normalmente, um conjunto pequeno de classes.</span><span class="sxs-lookup"><span data-stu-id="6eaaf-133">This is because classification requires a discrete response variable that only allows values that range over a finite, and usually somewhat small, set of classes.</span></span>

3. <span data-ttu-id="6eaaf-134">Se o conjunto de dados de pontuação não contiver todos os recursos usados para treinar o modelo, o [Modelo de Pontuação][score-model] produzirá um erro.</span><span class="sxs-lookup"><span data-stu-id="6eaaf-134">If the scoring dataset does not contain all the features used to train the model, the [Score Model][score-model] produces an error.</span></span>

4. <span data-ttu-id="6eaaf-135">Se uma linha no conjunto de dados de pontuação tiver um valor ausente ou um valor infinito para qualquer um de seus recursos, o [Modelo de Pontuação][score-model] não produzirá nenhuma saída correspondente a essa linha.</span><span class="sxs-lookup"><span data-stu-id="6eaaf-135">If a row in the scoring dataset contains a missing value or an infinite value for any of its features, the [Score Model][score-model] will not produce any output corresponding to that row.</span></span>

5. <span data-ttu-id="6eaaf-136">O [Modelo de Pontuação][score-model] pode produzir saídas idênticas para todas as linhas no conjunto de dados de pontuação.</span><span class="sxs-lookup"><span data-stu-id="6eaaf-136">The [Score Model][score-model] may produce identical outputs for all rows in the scoring dataset.</span></span> <span data-ttu-id="6eaaf-137">Isso pode ocorrer, por exemplo, ao tentar fazer a classificação usando Florestas de Decisão se o número mínimo de amostras por nó folha for escolhido como sendo maior que o número de exemplos de treinamento disponível.</span><span class="sxs-lookup"><span data-stu-id="6eaaf-137">This could occur, for example, when attempting classification using Decision Forests if the minimum number of samples per leaf node is chosen to be more than the number of training examples available.</span></span>

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

