---
title: "aaaAdvanced a exploração de dados e modelagem com Spark | Microsoft Docs"
description: "Use a exploração de dados do HDInsight Spark toodo e treinar modelos de classificação e regressão binários usando a otimização de validação cruzada e hyperparameter."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f90d9a80-4eaf-437b-a914-23514390cd60
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 055c342857fd732633cec9810de69cee61db973d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a><span data-ttu-id="66214-103">Modelagem e exploração de dados avançados com o Spark</span><span class="sxs-lookup"><span data-stu-id="66214-103">Advanced data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="66214-104">Este passo a passo usa HDInsight Spark toodo exploração e treinar binária e classificação de dados usando a validação cruzada de modelos de regressão e otimização de hyperparameter em uma amostra de saudação NYC táxi viagem e passagens de conjunto de dados de 2013.</span><span class="sxs-lookup"><span data-stu-id="66214-104">This walkthrough uses HDInsight Spark toodo data exploration and train binary classification and regression models using cross-validation and hyperparameter optimization on a sample of hello NYC taxi trip and fare 2013 dataset.</span></span> <span data-ttu-id="66214-105">Lhe orienta pelas etapas de saudação do hello [processo de ciência de dados](http://aka.ms/datascienceprocess), cluster de ponta a ponta, usando um HDInsight Spark para processamento e modelos de dados e Olá Olá toostore de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="66214-105">It walks you through hello steps of hello [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs toostore hello data and hello models.</span></span> <span data-ttu-id="66214-106">processo de saudação explora e visualiza os dados transferidos de um Blob de armazenamento do Azure e, em seguida, prepara Olá dados toobuild modelos de previsão.</span><span class="sxs-lookup"><span data-stu-id="66214-106">hello process explores and visualizes data brought in from an Azure Storage Blob and then prepares hello data toobuild predictive models.</span></span> <span data-ttu-id="66214-107">Python foi usado toocode Olá solução e tooshow Olá relevantes gráficos.</span><span class="sxs-lookup"><span data-stu-id="66214-107">Python has been used toocode hello solution and tooshow hello relevant plots.</span></span> <span data-ttu-id="66214-108">Esses modelos são compilados usando classificação binária do toodo Olá Spark MLlib Kit de ferramentas e tarefas de modelagem de regressão.</span><span class="sxs-lookup"><span data-stu-id="66214-108">These models are build using hello Spark MLlib toolkit toodo binary classification and regression modeling tasks.</span></span> 

* <span data-ttu-id="66214-109">Olá **classificação binária** tarefa é toopredict ou não uma dica é pago para viagem hello.</span><span class="sxs-lookup"><span data-stu-id="66214-109">hello **binary classification** task is toopredict whether or not a tip is paid for hello trip.</span></span> 
* <span data-ttu-id="66214-110">Olá **regressão** tarefa é toopredict Olá Olá dica com base em outros recursos de dica.</span><span class="sxs-lookup"><span data-stu-id="66214-110">hello **regression** task is toopredict hello amount of hello tip based on other tip features.</span></span> 

<span data-ttu-id="66214-111">etapas de modelagem Olá também contêm código que mostra como tootrain, avaliar e salvar cada tipo de modelo.</span><span class="sxs-lookup"><span data-stu-id="66214-111">hello modeling steps also contain code showing how tootrain, evaluate, and save each type of model.</span></span> <span data-ttu-id="66214-112">Olá tópico aborda algumas das Olá mesmo Terra como Olá [exploração de dados e modelagem com Spark](machine-learning-data-science-spark-data-exploration-modeling.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="66214-112">hello topic covers some of hello same ground as hello [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic.</span></span> <span data-ttu-id="66214-113">Mas ele é mais "Avançado" que também utiliza a validação cruzada com hyperparameter varredura tootrain modelos de classificação e regressão de maneira ideal precisos.</span><span class="sxs-lookup"><span data-stu-id="66214-113">But it is more "advanced" in that it also uses cross-validation with hyperparameter sweeping tootrain optimally accurate classification and regression models.</span></span> 

<span data-ttu-id="66214-114">**Validação cruzada (VC)** é uma técnica que avalia como um modelo treinado em um conjunto conhecido de dados generaliza toopredicting Olá recursos de conjuntos de dados no qual ele não foi treinado.</span><span class="sxs-lookup"><span data-stu-id="66214-114">**Cross-validation (CV)** is a technique that assesses how well a model trained on a known set of data generalizes toopredicting hello features of datasets on which it has not been trained.</span></span>  <span data-ttu-id="66214-115">Uma implementação comum usada aqui é toodivide um conjunto de dados em K dobras e, em seguida, treinar o modelo de saudação de forma round robin em apenas uma das partições de saudação.</span><span class="sxs-lookup"><span data-stu-id="66214-115">A common implementation used here is toodivide a dataset into K folds and then train hello model in a round-robin fashion on all but one of hello folds.</span></span> <span data-ttu-id="66214-116">capacidade de saudação do hello modelo tooprediction com precisão quando testados no conjunto de dados independentes no modelo dobra não usado tootrain Olá Olá será avaliada.</span><span class="sxs-lookup"><span data-stu-id="66214-116">hello ability of hello model tooprediction accurately when tested against hello independent dataset in this fold not used tootrain hello model is assessed.</span></span>

<span data-ttu-id="66214-117">**Otimização de Hyperparameter** Olá problema de escolher um conjunto de hiperparâmetros para um algoritmo de aprendizado, geralmente com a meta de saudação de otimizar uma medida de desempenho do algoritmo Olá em um conjunto de dados independente.</span><span class="sxs-lookup"><span data-stu-id="66214-117">**Hyperparameter optimization** is hello problem of choosing a set of hyperparameters for a learning algorithm, usually with hello goal of optimizing a measure of hello algorithm's performance on an independent data set.</span></span> <span data-ttu-id="66214-118">**Hiperparâmetros** são valores que devem ser especificados fora do procedimento de treinamento de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="66214-118">**Hyperparameters** are values that must be specified outside of hello model training procedure.</span></span> <span data-ttu-id="66214-119">Suposições sobre esses valores podem afetar a flexibilidade de saudação e precisão dos modelos de saudação.</span><span class="sxs-lookup"><span data-stu-id="66214-119">Assumptions about these values can impact hello flexibility and accuracy of hello models.</span></span> <span data-ttu-id="66214-120">Árvores de decisão têm hiperparâmetros, por exemplo, como Olá desejado profundidade e número de folhas na árvore de saudação.</span><span class="sxs-lookup"><span data-stu-id="66214-120">Decision trees have hyperparameters, for example, such as hello desired depth and number of leaves in hello tree.</span></span> <span data-ttu-id="66214-121">As SVMs (Máquinas de Vetor de Suporte) exigem a configuração de um termo de penalidade de classificação incorreta.</span><span class="sxs-lookup"><span data-stu-id="66214-121">Support Vector Machines (SVMs) require setting a misclassification penalty term.</span></span> 

<span data-ttu-id="66214-122">Uma otimização de hyperparameter de tooperform forma comum usada aqui é uma pesquisa de grade, ou um **varredura de parâmetro**.</span><span class="sxs-lookup"><span data-stu-id="66214-122">A common way tooperform hyperparameter optimization used here is a grid search, or a **parameter sweep**.</span></span> <span data-ttu-id="66214-123">Isso consiste em executar uma pesquisa detalhada por meio de valores de saudação um subconjunto especificado de espaço de hyperparameter Olá para um algoritmo de aprendizado.</span><span class="sxs-lookup"><span data-stu-id="66214-123">This consists of performing an exhaustive search through hello values a specified subset of hello hyperparameter space for a learning algorithm.</span></span> <span data-ttu-id="66214-124">Validação cruzada pode fornecer um toosort de métrica de desempenho os resultados ideais de Olá produzido pelo algoritmo de pesquisa de grade hello.</span><span class="sxs-lookup"><span data-stu-id="66214-124">Cross validation can supply a performance metric toosort out hello optimal results produced by hello grid search algorithm.</span></span> <span data-ttu-id="66214-125">VC usado com ajuda a varredura de hyperparameter problemas de limite como sobreajuste um tootraining de dados de modelo para que o modelo hello mantém Olá capacidade tooapply toohello conjunto geral de dados do qual Olá dados de treinamento foi extraídos.</span><span class="sxs-lookup"><span data-stu-id="66214-125">CV used with hyperparameter sweeping helps limit problems like overfitting a model tootraining data so that hello model retains hello capacity tooapply toohello general set of data from which hello training data was extracted.</span></span>

<span data-ttu-id="66214-126">os modelos de saudação que usamos incluem gradientes árvores aumentadas, florestas aleatórias e regressão logística e linear:</span><span class="sxs-lookup"><span data-stu-id="66214-126">hello models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="66214-127">[Regressão linear com SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) é um modelo de regressão linear que usa um método descendente gradiente Estocástico (SGD) e para a otimização e recurso de dimensionamento quantidades de dica de saudação toopredict pago.</span><span class="sxs-lookup"><span data-stu-id="66214-127">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling toopredict hello tip amounts paid.</span></span> 
* <span data-ttu-id="66214-128">[Regressão logística com LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) ou regressão "logit", é um modelo de regressão que pode ser usado quando a variável dependente de saudação é categórica toodo a classificação de dados.</span><span class="sxs-lookup"><span data-stu-id="66214-128">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when hello dependent variable is categorical toodo data classification.</span></span> <span data-ttu-id="66214-129">LBFGS é um algoritmo de otimização de quase-Newton que aproxima o algoritmo Broyden – Fletcher – Goldfarb – Shanno (BFGS) de saudação usando uma quantidade limitada de memória do computador e que é amplamente usada no aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="66214-129">LBFGS is a quasi-Newton optimization algorithm that approximates hello Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="66214-130">[Florestas aleatórias](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) são conjuntos de árvores de decisão.</span><span class="sxs-lookup"><span data-stu-id="66214-130">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="66214-131">Elas combinam muitas decisões árvores tooreduce Olá risco de superajuste.</span><span class="sxs-lookup"><span data-stu-id="66214-131">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="66214-132">Florestas aleatórias são usadas para classificação e regressão e podem lidar com recursos categóricos e configuração de classificação multiclasse toohello podem ser estendidas.</span><span class="sxs-lookup"><span data-stu-id="66214-132">Random forests are used for regression and classification and can handle categorical features and can be extended toohello multiclass classification setting.</span></span> <span data-ttu-id="66214-133">Eles não exigem recurso escala e são capazes de toocapture não linearidades e interações de recurso.</span><span class="sxs-lookup"><span data-stu-id="66214-133">They do not require feature scaling and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="66214-134">Florestas aleatórias são um dos modelos de classificação e regressão de aprendizado de máquina mais bem-sucedida de saudação.</span><span class="sxs-lookup"><span data-stu-id="66214-134">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="66214-135">[GBTs (árvores com aumento gradiente)](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) são conjuntos de árvores de decisão.</span><span class="sxs-lookup"><span data-stu-id="66214-135">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="66214-136">Árvores de decisão de treinar GBTs iterativamente toominimize uma função de perda.</span><span class="sxs-lookup"><span data-stu-id="66214-136">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="66214-137">GBTs são usados para classificação e regressão pode lidar com recursos categóricos, não requerem o dimensionamento de recurso e são capazes de toocapture não linearidades e interações de recursos.</span><span class="sxs-lookup"><span data-stu-id="66214-137">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="66214-138">Elas também podem ser usadas em uma configuração de classificação multiclasse.</span><span class="sxs-lookup"><span data-stu-id="66214-138">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="66214-139">Varredura de exemplos do uso de VC e Hyperparameter de modelagem são mostradas para problema de classificação binária hello.</span><span class="sxs-lookup"><span data-stu-id="66214-139">Modeling examples using CV and Hyperparameter sweep are shown for hello binary classification problem.</span></span> <span data-ttu-id="66214-140">Os exemplos mais simples (sem varredura de parâmetro) são apresentados no tópico principal de Olá para tarefas de regressão.</span><span class="sxs-lookup"><span data-stu-id="66214-140">Simpler examples (without parameter sweeps) are presented in hello main topic for regression tasks.</span></span> <span data-ttu-id="66214-141">Mas, no Apêndice hello, validação usando net Elástico para regressão linear e VC com o uso de varredura de parâmetro de regressão de floresta aleatório também é apresentada.</span><span class="sxs-lookup"><span data-stu-id="66214-141">But in hello appendix, validation using elastic net for linear regression and CV with parameter sweep using for random forest regression are also presented.</span></span> <span data-ttu-id="66214-142">Olá **elástica net** é um método de regressão regularizada para ajuste de regressão linear que modelos linearmente combina as métricas de L1 e L2 hello como penalidades de saudação [Laço](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) e [Montanhas](https://en.wikipedia.org/wiki/Tikhonov_regularization) métodos.</span><span class="sxs-lookup"><span data-stu-id="66214-142">hello **elastic net** is a regularized regression method for fitting linear regression models that linearly combines hello L1 and L2 metrics as penalties of hello [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) and [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) methods.</span></span>   

> [!NOTE]
> <span data-ttu-id="66214-143">Embora o Kit de ferramentas do hello Spark MLlib toowork projetado em grandes conjuntos de dados, um exemplo relativamente pequeno (aproximadamente 30 Mb usando 170 mil linhas, cerca de 0,1% de saudação original NYC dataset) é usado aqui para sua conveniência.</span><span class="sxs-lookup"><span data-stu-id="66214-143">Although hello Spark MLlib toolkit is designed toowork on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of hello original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="66214-144">Exercício Olá fornecido aqui é executado com eficiência (em cerca de 10 minutos) em um cluster de HDInsight com 2 nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="66214-144">hello exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="66214-145">Olá mesmo código, com pequenas modificações, pode ser usado tooprocess-conjuntos de dados maiores, com as modificações apropriadas para o cache de dados na memória e alterar o tamanho do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="66214-145">hello same code, with minor modifications, can be used tooprocess larger data-sets, with appropriate modifications for caching data in memory and changing hello cluster size.</span></span>
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a><span data-ttu-id="66214-146">Instalação: blocos de notas e clusters do Spark</span><span class="sxs-lookup"><span data-stu-id="66214-146">Setup: Spark clusters and notebooks</span></span>
<span data-ttu-id="66214-147">As etapas de configuração e o código são fornecidos neste passo a passo para usar um HDInsight Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="66214-147">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="66214-148">Porém, notebooks Jupyter são fornecidos tanto para o HDInsight Spark 1.6 quanto para os clusters Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="66214-148">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="66214-149">Uma descrição da saudação toothem de anotações e links são fornecidos no hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) para o repositório do GitHub Olá que os contém.</span><span class="sxs-lookup"><span data-stu-id="66214-149">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="66214-150">Além disso, Olá código aqui e em blocos de anotações Olá vinculado é genérico e deve funcionar em qualquer cluster do Spark.</span><span class="sxs-lookup"><span data-stu-id="66214-150">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="66214-151">Se você não estiver usando o HDInsight Spark, as etapas de configuração e gerenciamento de cluster Olá podem ser ligeiramente diferentes da que é mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="66214-151">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="66214-152">Para sua conveniência, aqui estão Olá links toohello Jupyter blocos de anotações para Spark 1.6 e 2.0 toobe executar no kernel do pyspark de saudação do servidor de Jupyter Notebook de saudação:</span><span class="sxs-lookup"><span data-stu-id="66214-152">For convenience, here are hello links toohello Jupyter notebooks for Spark 1.6 and 2.0 toobe run in hello pyspark kernel of hello Jupyter Notebook server:</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="66214-153">Blocos de notas Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="66214-153">Spark 1.6 notebooks</span></span>

<span data-ttu-id="66214-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): inclui tópicos no blocos de notas nº. 1 e o desenvolvimento de modelos usando validação cruzada e ajuste de hiperparâmetro.</span><span class="sxs-lookup"><span data-stu-id="66214-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Includes topics in notebook #1, and model development using hyperparameter tuning and cross-validation.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="66214-155">Blocos de notas Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="66214-155">Spark 2.0 notebooks</span></span>

<span data-ttu-id="66214-156">[Spark2.0-pySpark3-Machine-Learning-data-Science-Spark-Advanced-data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): este arquivo fornece informações sobre como a exploração de dados tooperform, modelagem e pontuação no Spark 2.0 clusters.</span><span class="sxs-lookup"><span data-stu-id="66214-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how tooperform data exploration, modeling, and scoring in Spark 2.0 clusters.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="66214-157">Programa de instalação: Olá, bibliotecas e locais de armazenamento predefinição contexto Spark</span><span class="sxs-lookup"><span data-stu-id="66214-157">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="66214-158">Spark é capaz de tooAzure tooread e gravar o Blob de armazenamento (também conhecido como WASB).</span><span class="sxs-lookup"><span data-stu-id="66214-158">Spark is able tooread and write tooAzure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="66214-159">Para qualquer um dos seus dados existentes armazenados podem ser processadas usando Spark e Olá resultados armazenados em WASB.</span><span class="sxs-lookup"><span data-stu-id="66214-159">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="66214-160">toosave modelos ou os arquivos em WASB, o caminho Olá precisa toobe especificado corretamente.</span><span class="sxs-lookup"><span data-stu-id="66214-160">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="66214-161">Olá padrão contêiner anexado toohello Spark cluster pode ser referenciado usando um caminho começando com: "wasb: / / /".</span><span class="sxs-lookup"><span data-stu-id="66214-161">hello default container attached toohello Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="66214-162">Outros locais são referenciados por "wasb://".</span><span class="sxs-lookup"><span data-stu-id="66214-162">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="66214-163">Definir caminhos de diretório para locais de armazenamento no WASB</span><span class="sxs-lookup"><span data-stu-id="66214-163">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="66214-164">Olá, exemplo de código a seguir especifica o local de saudação de Olá toobe de dados de leitura e Olá caminho para a saída do modelo Olá modelo armazenamento diretório toowhich Olá é salvo:</span><span class="sxs-lookup"><span data-stu-id="66214-164">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved:</span></span>

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="66214-165">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-165">**OUTPUT**</span></span>

<span data-ttu-id="66214-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span><span class="sxs-lookup"><span data-stu-id="66214-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="66214-167">Importar bibliotecas</span><span class="sxs-lookup"><span data-stu-id="66214-167">Import libraries</span></span>
<span data-ttu-id="66214-168">Importe bibliotecas necessárias com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="66214-168">Import necessary libraries with hello following code:</span></span>

    # LOAD PYSPARK LIBRARIES
    import pyspark
    from pyspark import SparkConf
    from pyspark import SparkContext
    from pyspark.sql import SQLContext
    import matplotlib
    import matplotlib.pyplot as plt
    from pyspark.sql import Row
    from pyspark.sql.functions import UserDefinedFunction
    from pyspark.sql.types import *
    import atexit
    from numpy import array
    import numpy as np
    import datetime


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="66214-169">Contexto predefinido do Spark e palavras mágicas do PySpark</span><span class="sxs-lookup"><span data-stu-id="66214-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="66214-170">kernels PySpark de saudação que são fornecidos com blocos de anotações do Jupyter tem um contexto de predefinição.</span><span class="sxs-lookup"><span data-stu-id="66214-170">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="66214-171">Portanto não é necessário tooset Olá Spark ou Hive contextos explicitamente antes de começar a trabalhar com o aplicativo hello que você está desenvolvendo.</span><span class="sxs-lookup"><span data-stu-id="66214-171">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="66214-172">Esses contextos estão disponíveis para você por padrão.</span><span class="sxs-lookup"><span data-stu-id="66214-172">These contexts are available for you by default.</span></span> <span data-ttu-id="66214-173">Esses contextos são:</span><span class="sxs-lookup"><span data-stu-id="66214-173">These contexts are:</span></span>

* <span data-ttu-id="66214-174">sc - para o Spark</span><span class="sxs-lookup"><span data-stu-id="66214-174">sc - for Spark</span></span> 
* <span data-ttu-id="66214-175">sqlContext - para o Hive</span><span class="sxs-lookup"><span data-stu-id="66214-175">sqlContext - for Hive</span></span>

<span data-ttu-id="66214-176">Olá PySpark kernel fornece algumas predefinidas "magics", que são comandos especiais que podem ser chamados com % %.</span><span class="sxs-lookup"><span data-stu-id="66214-176">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="66214-177">Há dois comandos que são usados nesses exemplos de código.</span><span class="sxs-lookup"><span data-stu-id="66214-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="66214-178">**% % local** Especifica que o código de saudação em linhas subsequentes é toobe executado localmente.</span><span class="sxs-lookup"><span data-stu-id="66214-178">**%%local** Specifies that hello code in subsequent lines is toobe executed locally.</span></span> <span data-ttu-id="66214-179">O código deve ser um código Python válido.</span><span class="sxs-lookup"><span data-stu-id="66214-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="66214-180">**% % -o do sql <variable name>**  executa uma consulta de Hive em Olá sqlContext.</span><span class="sxs-lookup"><span data-stu-id="66214-180">**%%sql -o <variable name>** Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="66214-181">Se Olá -o parâmetro for passado, resultado de saudação de consulta de saudação é mantido no Olá % % contexto Python local como um DataFrame Pandas.</span><span class="sxs-lookup"><span data-stu-id="66214-181">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="66214-182">Para obter mais informações sobre kernels Olá para blocos de anotações do Jupyter e hello predefinidas "magics" que eles fornecem, consulte [clusters Kernels disponíveis para blocos de anotações do Jupyter com Linux do HDInsight Spark no HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="66214-182">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="66214-183">Ingestão de dados do blob público:</span><span class="sxs-lookup"><span data-stu-id="66214-183">Data ingestion from public blob:</span></span>
<span data-ttu-id="66214-184">Olá, primeira etapa no processo de ciência de dados Olá é tooingest Olá dados toobe analisado de fontes de onde ele reside em seu ambiente de modelagem e exploração de dados.</span><span class="sxs-lookup"><span data-stu-id="66214-184">hello first step in hello data science process is tooingest hello data toobe analyzed from sources where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="66214-185">Esse ambiente é o Spark neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="66214-185">This environment is Spark in this walkthrough.</span></span> <span data-ttu-id="66214-186">Esta seção contém Olá código toocomplete uma série de tarefas:</span><span class="sxs-lookup"><span data-stu-id="66214-186">This section contains hello code toocomplete a series of tasks:</span></span>

* <span data-ttu-id="66214-187">Olá toobe de exemplo de dados modelado de ingestão</span><span class="sxs-lookup"><span data-stu-id="66214-187">ingest hello data sample toobe modeled</span></span>
* <span data-ttu-id="66214-188">ler no conjunto de dados entrada hello (armazenado como um arquivo. tsv)</span><span class="sxs-lookup"><span data-stu-id="66214-188">read in hello input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="66214-189">formato e dados saudação normal</span><span class="sxs-lookup"><span data-stu-id="66214-189">format and clean hello data</span></span>
* <span data-ttu-id="66214-190">criar e armazenar objetos em cache (RDDs ou quadros de dados) na memória</span><span class="sxs-lookup"><span data-stu-id="66214-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="66214-191">registrá-lo como uma tabela temporária no contexto do SQL.</span><span class="sxs-lookup"><span data-stu-id="66214-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="66214-192">Este é o código de saudação para ingestão de dados.</span><span class="sxs-lookup"><span data-stu-id="66214-192">Here is hello code for data ingestion.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    schema_string = taxi_train_file.first()
    fields = [StructField(field_name, StringType(), True) for field_name in schema_string.split('\t')]
    fields[7].dataType = IntegerType() #Pickup hour
    fields[8].dataType = IntegerType() # Pickup week
    fields[9].dataType = IntegerType() # Weekday
    fields[10].dataType = IntegerType() # Passenger count
    fields[11].dataType = FloatType() # Trip time in secs
    fields[12].dataType = FloatType() # Trip distance
    fields[19].dataType = FloatType() # Fare amount
    fields[20].dataType = FloatType() # Surcharge
    fields[21].dataType = FloatType() # Mta_tax
    fields[22].dataType = FloatType() # Tip amount
    fields[23].dataType = FloatType() # Tolls amount
    fields[24].dataType = FloatType() # Total amount
    fields[25].dataType = IntegerType() # Tipped or not
    fields[26].dataType = IntegerType() # Tip class
    taxi_schema = StructType(fields)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_header = taxi_train_file.filter(lambda l: "medallion" in l)
    taxi_temp = taxi_train_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))


    # CREATE DATA FRAME
    taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_train_cleaned = taxi_train_df.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES hello DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="66214-193">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-193">**OUTPUT**</span></span>

<span data-ttu-id="66214-194">Tempo gasto tooexecute acima célula: 276.62 segundos</span><span class="sxs-lookup"><span data-stu-id="66214-194">Time taken tooexecute above cell: 276.62 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="66214-195">Visualização e exploração de dados</span><span class="sxs-lookup"><span data-stu-id="66214-195">Data exploration & visualization</span></span>
<span data-ttu-id="66214-196">Quando dados saudação foi colocados no Spark, hello próxima etapa no processo de ciência de dados Olá é toogain de compreensão mais profunda dos dados Olá por meio de exploração e visualização.</span><span class="sxs-lookup"><span data-stu-id="66214-196">Once hello data has been brought into Spark, hello next step in hello data science process is toogain deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="66214-197">Nesta seção, podemos examinar dados de táxi hello usando consultas SQL e recursos em potencial e variáveis de destino de saudação de plotagem para inspeção visual.</span><span class="sxs-lookup"><span data-stu-id="66214-197">In this section, we examine hello taxi data using SQL queries and plot hello target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="66214-198">Especificamente, podemos plotar frequência Olá passageiro de contagens de em viagens táxi, a frequência de saudação de quantidades de ponta e como dicas variam de acordo com o tipo e a quantidade de pagamento.</span><span class="sxs-lookup"><span data-stu-id="66214-198">Specifically, we plot hello frequency of passenger counts in taxi trips, hello frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a><span data-ttu-id="66214-199">Plotar um histograma de frequências de contagem de passageiro no exemplo hello de viagens táxi</span><span class="sxs-lookup"><span data-stu-id="66214-199">Plot a histogram of passenger count frequencies in hello sample of taxi trips</span></span>
<span data-ttu-id="66214-200">Esse código e trechos de código subsequentes usam exemplo do SQL tooquery magic hello e os dados de saudação do tooplot magic local.</span><span class="sxs-lookup"><span data-stu-id="66214-200">This code and subsequent snippets use SQL magic tooquery hello sample and local magic tooplot hello data.</span></span>

* <span data-ttu-id="66214-201">**Magic SQL (`%%sql`)** hello HDInsight PySpark kernel dá suporte a fácil embutido HiveQL consultas em relação a saudação sqlContext.</span><span class="sxs-lookup"><span data-stu-id="66214-201">**SQL magic (`%%sql`)** hello HDInsight PySpark kernel supports easy inline HiveQL queries against hello sqlContext.</span></span> <span data-ttu-id="66214-202">saudação (-o VARIABLE_NAME) argumento persiste saída Olá de consulta do SQL hello como um DataFrame Pandas no servidor do Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="66214-202">hello (-o VARIABLE_NAME) argument persists hello output of hello SQL query as a Pandas DataFrame on hello Jupyter server.</span></span> <span data-ttu-id="66214-203">Isso significa que ele está disponível no modo local hello.</span><span class="sxs-lookup"><span data-stu-id="66214-203">This means it is available in hello local mode.</span></span>
* <span data-ttu-id="66214-204">Olá  **`%%local` mágico** é usado toorun código localmente no servidor de Jupyter hello, que é Olá um nó principal do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="66214-204">hello **`%%local` magic** is used toorun code locally on hello Jupyter server, which is hello headnode of hello HDInsight cluster.</span></span> <span data-ttu-id="66214-205">Normalmente, você usa `%%local` magic após Olá `%%sql -o` magic é usado toorun uma consulta.</span><span class="sxs-lookup"><span data-stu-id="66214-205">Typically, you use `%%local` magic after hello `%%sql -o` magic is used toorun a query.</span></span> <span data-ttu-id="66214-206">parâmetro -o de Hello persistir Olá saída de hello SQL consulta localmente.</span><span class="sxs-lookup"><span data-stu-id="66214-206">hello -o parameter would persist hello output of hello SQL query locally.</span></span> <span data-ttu-id="66214-207">Em seguida, Olá `%%local` gatilhos magic Olá próximo conjunto de toorun de trechos de código localmente em relação a saída de hello de consultas SQL Olá persistiu localmente.</span><span class="sxs-lookup"><span data-stu-id="66214-207">Then hello `%%local` magic triggers hello next set of code snippets toorun locally against hello output of hello SQL queries that has been persisted locally.</span></span> <span data-ttu-id="66214-208">saída de Hello é visualizada automaticamente depois de executar código hello.</span><span class="sxs-lookup"><span data-stu-id="66214-208">hello output is automatically visualized after you run hello code.</span></span>

<span data-ttu-id="66214-209">Essa consulta recupera viagens Olá por contagem de passageiro.</span><span class="sxs-lookup"><span data-stu-id="66214-209">This query retrieves hello trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


<span data-ttu-id="66214-210">Esse código cria um quadro de dados local de saída da consulta hello e plota dados saudação.</span><span class="sxs-lookup"><span data-stu-id="66214-210">This code creates a local data-frame from hello query output and plots hello data.</span></span> <span data-ttu-id="66214-211">Olá `%%local` mágico cria um local-quadro de dados, `sqlResults`, que pode ser usado para plotar com matplotlib.</span><span class="sxs-lookup"><span data-stu-id="66214-211">hello `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="66214-212">Essas palavras mágicas do PySpark são usadas várias vezes neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="66214-212">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="66214-213">Se a quantidade de saudação de dados for grande, você deve exemplo toocreate um quadro de dados que pode caber na memória local.</span><span class="sxs-lookup"><span data-stu-id="66214-213">If hello amount of data is large, you should sample toocreate a data-frame that can fit in local memory.</span></span>
> 
> 

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="66214-214">Aqui está viagens de Olá Olá código tooplot por passageiro contagens</span><span class="sxs-lookup"><span data-stu-id="66214-214">Here is hello code tooplot hello trips by passenger counts</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT PASSENGER NUMBER VS TRIP COUNTS
    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

<span data-ttu-id="66214-215">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-215">**OUTPUT**</span></span>

![Frequência de corridas por contagem de passageiros](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

<span data-ttu-id="66214-217">Você pode selecionar entre vários tipos diferentes de visualizações (tabela, pizza, linha, área ou barra) usando Olá **tipo** botões de menu no bloco de anotações de saudação.</span><span class="sxs-lookup"><span data-stu-id="66214-217">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using hello **Type** menu buttons in hello notebook.</span></span> <span data-ttu-id="66214-218">gráfico de barras Olá é mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="66214-218">hello Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="66214-219">Plote um histograma de valores de gorjetas e como o valor das gorjetas varia pelas tarifas e contagens de passageiros.</span><span class="sxs-lookup"><span data-stu-id="66214-219">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="66214-220">Usar um banco de dados consulta toosample do SQL.</span><span class="sxs-lookup"><span data-stu-id="66214-220">Use a SQL query toosample data..</span></span>

    # SQL SQUERY
    %%sql -q -o sqlResults
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train 
        WHERE passenger_count > 0 
        AND passenger_count < 7
        AND fare_amount > 0 
        AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 
        AND tip_amount < 25


<span data-ttu-id="66214-221">Esta célula código usa Olá consulta toocreate três gráficos Olá de dados do SQL.</span><span class="sxs-lookup"><span data-stu-id="66214-221">This code cell uses hello SQL query toocreate three plots hello data.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline

    # TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = resultsPDDF[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = resultsPDDF.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount ($) by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = resultsPDDF.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(resultsPDDF.passenger_count))
    ax.set_title('Tip amount by Fare amount ($)')
    ax.set_xlabel('Fare Amount')
    ax.set_ylabel('Tip Amount')
    plt.axis([-2, 120, -2, 30])
    plt.show()


<span data-ttu-id="66214-222">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="66214-222">**OUTPUT:**</span></span> 

![Distribuição de valores de gorjetas](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![Valor de gorjeta por contagem de passageiros](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Valor de gorjeta por valor de tarifa](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="66214-226">Engenharia de recursos, transformação e preparação de dados para a modelagem</span><span class="sxs-lookup"><span data-stu-id="66214-226">Feature engineering, transformation, and data preparation for modeling</span></span>
<span data-ttu-id="66214-227">Esta seção descreve e fornece código Olá para procedimentos usados tooprepare dados para uso em modelagem ML.</span><span class="sxs-lookup"><span data-stu-id="66214-227">This section describes and provides hello code for procedures used tooprepare data for use in ML modeling.</span></span> <span data-ttu-id="66214-228">Ele mostra como as tarefas de saudação toodo a seguir:</span><span class="sxs-lookup"><span data-stu-id="66214-228">It shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="66214-229">Criar um novo recurso por meio do particionamento de horários em compartimentos de tempo de tráfego</span><span class="sxs-lookup"><span data-stu-id="66214-229">Create a new feature by partitioning hours into traffic time bins</span></span>
* <span data-ttu-id="66214-230">Indexar e fazer a codificação one-hot dos recursos categóricos</span><span class="sxs-lookup"><span data-stu-id="66214-230">Index and on-hot encode categorical features</span></span>
* <span data-ttu-id="66214-231">Criar objetos de ponto rotulado para entrada em funções de ML</span><span class="sxs-lookup"><span data-stu-id="66214-231">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="66214-232">Cria uma amostragem aleatória de subgrupos de dados hello e dividi-lo em treinamento e conjuntos de teste</span><span class="sxs-lookup"><span data-stu-id="66214-232">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
* <span data-ttu-id="66214-233">Dimensionamento de recursos</span><span class="sxs-lookup"><span data-stu-id="66214-233">Feature scaling</span></span>
* <span data-ttu-id="66214-234">Armazenar objetos em cache na memória</span><span class="sxs-lookup"><span data-stu-id="66214-234">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a><span data-ttu-id="66214-235">Criar um novo recurso por meio do particionamento de horários de tráfego em compartimentos</span><span class="sxs-lookup"><span data-stu-id="66214-235">Create a new feature by partitioning traffic times into bins</span></span>
<span data-ttu-id="66214-236">Esse código mostra como toocreate um novo recurso por meio do particionamento tráfego vezes em compartimentos e como toocache Olá resultante quadro de dados na memória.</span><span class="sxs-lookup"><span data-stu-id="66214-236">This code shows how toocreate a new feature by partitioning traffic times into bins and then how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="66214-237">Cache leva tempo de execução tooimproved onde resiliente distribuídas conjuntos de dados (RDDs) e quadros de dados são usados repetidamente.</span><span class="sxs-lookup"><span data-stu-id="66214-237">Caching leads tooimproved execution time where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly.</span></span> <span data-ttu-id="66214-238">Portanto, armazenamos em cache RDDs e quadros de dados em vários estágios no passo a passo.</span><span class="sxs-lookup"><span data-stu-id="66214-238">So, we cache RDDs and data-frames at several stages in this walkthrough.</span></span>

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train 
    """
    taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    # hello .COUNT() GOES THROUGH hello ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES hello COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

<span data-ttu-id="66214-239">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-239">**OUTPUT**</span></span>

<span data-ttu-id="66214-240">126050</span><span class="sxs-lookup"><span data-stu-id="66214-240">126050</span></span>

### <a name="index-and-one-hot-encode-categorical-features"></a><span data-ttu-id="66214-241">Indexar e fazer a codificação one-hot dos recursos categóricos</span><span class="sxs-lookup"><span data-stu-id="66214-241">Index and one-hot encode categorical features</span></span>
<span data-ttu-id="66214-242">Esta seção mostra como tooindex ou codificar recursos categóricos para entrada em Olá funções da modelagem.</span><span class="sxs-lookup"><span data-stu-id="66214-242">This section shows how tooindex or encode categorical features for input into hello modeling functions.</span></span> <span data-ttu-id="66214-243">Olá modelagem e prever a funções de MLlib exigem que os recursos com dados categóricos de entrada ser indexados ou codificados toouse anterior.</span><span class="sxs-lookup"><span data-stu-id="66214-243">hello modeling and predict functions of MLlib require that features with categorical input data be indexed or encoded prior toouse.</span></span> 

<span data-ttu-id="66214-244">Dependendo do modelo de hello, você precisa tooindex ou codificá-los de maneiras diferentes.</span><span class="sxs-lookup"><span data-stu-id="66214-244">Depending on hello model, you need tooindex or encode them in different ways.</span></span> <span data-ttu-id="66214-245">Por exemplo, modelos de regressão Linear e logística exigem hot uma codificação, onde, por exemplo, um recurso com três categorias pode ser expandido em três colunas de recurso, com cada contendo 0 ou 1 dependendo da categoria de saudação de uma observação.</span><span class="sxs-lookup"><span data-stu-id="66214-245">For example, Logistic and Linear Regression models require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="66214-246">Fornece MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) toodo hot uma codificação de função.</span><span class="sxs-lookup"><span data-stu-id="66214-246">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function toodo one-hot encoding.</span></span> <span data-ttu-id="66214-247">Este codificador mapeia uma coluna da coluna de tooa de índices de rótulo de vetores de binários, no máximo um único um valor.</span><span class="sxs-lookup"><span data-stu-id="66214-247">This encoder maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="66214-248">Essa codificação permite que os algoritmos que esperam recursos com valores numéricos, como a regressão logística, recursos de toocategorical toobe aplicado.</span><span class="sxs-lookup"><span data-stu-id="66214-248">This encoding allows algorithms that expect numerical valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

<span data-ttu-id="66214-249">Aqui está o hello tooindex de código e codificar recursos categóricos:</span><span class="sxs-lookup"><span data-stu-id="66214-249">Here is hello code tooindex and encode categorical features:</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is hello cleaned one from above
    indexed = model.transform(taxi_df_train_with_newFeatures)
    encoder = OneHotEncoder(dropLast=False, inputCol="vendorIndex", outputCol="vendorVec")
    encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    stringIndexer = StringIndexer(inputCol="rate_code", outputCol="rateIndex")
    model = stringIndexer.fit(encoded1)
    indexed = model.transform(encoded1)
    encoder = OneHotEncoder(dropLast=False, inputCol="rateIndex", outputCol="rateVec")
    encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    stringIndexer = StringIndexer(inputCol="payment_type", outputCol="paymentIndex")
    model = stringIndexer.fit(encoded2)
    indexed = model.transform(encoded2)
    encoder = OneHotEncoder(dropLast=False, inputCol="paymentIndex", outputCol="paymentVec")
    encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="66214-250">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-250">**OUTPUT**</span></span>

<span data-ttu-id="66214-251">Tempo gasto tooexecute acima célula: segundos 3.14</span><span class="sxs-lookup"><span data-stu-id="66214-251">Time taken tooexecute above cell: 3.14 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="66214-252">Criar objetos de ponto rotulado para entrada em funções de ML</span><span class="sxs-lookup"><span data-stu-id="66214-252">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="66214-253">Esta seção contém o código que mostra como o tipo de dados de texto categóricos tooindex como um rótulo de ponto de dados e como tooencode-lo.</span><span class="sxs-lookup"><span data-stu-id="66214-253">This section contains code that shows how tooindex categorical text data as a labeled point data type and how tooencode it.</span></span> <span data-ttu-id="66214-254">Isso prepara toobe usado tootrain e teste MLlib Regressão logística e outros modelos de classificação.</span><span class="sxs-lookup"><span data-stu-id="66214-254">This prepares it toobe used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="66214-255">Objetos de ponto rotulados são RDDs (Conjuntos de Dados Resilientes Distribuídos) formatados de uma maneira que é necessária como dados de entrada pela maioria dos algoritmos de ML no MLlib.</span><span class="sxs-lookup"><span data-stu-id="66214-255">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="66214-256">Um [ponto rotulado](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) é um vetor local, denso ou esparso, associado a um rótulo/resposta.</span><span class="sxs-lookup"><span data-stu-id="66214-256">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="66214-257">Aqui está o hello tooindex de código e codificar os recursos de texto para classificação binária.</span><span class="sxs-lookup"><span data-stu-id="66214-257">Here is hello code tooindex and encode text features for binary classification.</span></span>

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.pickup_hour, line.weekday,
                             line.passenger_count, line.trip_time_in_secs, line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                   line.vendorVec.toArray(), line.rateVec.toArray(), line.paymentVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


<span data-ttu-id="66214-258">Aqui está o código de saudação tooencode e o índice de recursos categóricos texto para análise de regressão linear.</span><span class="sxs-lookup"><span data-stu-id="66214-258">Here is hello code tooencode and index categorical text features for linear regression analysis.</span></span>

    # FUNCTIONS FOR REGRESSION WITH TIP AMOUNT AS TARGET VARIABLE

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="66214-259">Cria uma amostragem aleatória de subgrupos de dados hello e dividi-lo em treinamento e conjuntos de teste</span><span class="sxs-lookup"><span data-stu-id="66214-259">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
<span data-ttu-id="66214-260">Esse código cria uma amostragem aleatória de dados de saudação (25% é usado aqui).</span><span class="sxs-lookup"><span data-stu-id="66214-260">This code creates a random sampling of hello data (25% is used here).</span></span> <span data-ttu-id="66214-261">Embora não seja necessário para este exemplo devido toohello tamanho do conjunto de dados hello, demonstraremos como de exemplo dados Olá aqui.</span><span class="sxs-lookup"><span data-stu-id="66214-261">Although it is not required for this example due toohello size of hello dataset, we demonstrate how you can sample hello data here.</span></span> <span data-ttu-id="66214-262">Você sabe como toouse-lo para seus próprios problemas se necessário.</span><span class="sxs-lookup"><span data-stu-id="66214-262">Then you know how toouse it for your own problem if needed.</span></span> <span data-ttu-id="66214-263">Quando as amostras são grandes, isso pode economizar um tempo significativo durante o treinamento de modelos.</span><span class="sxs-lookup"><span data-stu-id="66214-263">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="66214-264">Em seguida, dividiremos exemplo hello em uma parte de treinamento (75% aqui) e um teste toouse de parte (25% aqui) de classificação e modelagem de regressão.</span><span class="sxs-lookup"><span data-stu-id="66214-264">Next we split hello sample into a training part (75% here) and a testing part (25% here) toouse in classification and regression modeling.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    from pyspark.sql.functions import rand

    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST, WITH A RANDOM COLUMN ADDED FOR DOING CV (SHOWN LATER)
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # CACHE TRAIN AND TEST DATA
    trainData.cache()
    testData.cache()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary = trainData.map(parseRowIndexingBinary)
    indexedTESTbinary = testData.map(parseRowIndexingBinary)
    oneHotTRAINbinary = trainData.map(parseRowOneHotBinary)
    oneHotTESTbinary = testData.map(parseRowOneHotBinary)

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg = trainData.map(parseRowIndexingRegression)
    indexedTESTreg = testData.map(parseRowIndexingRegression)
    oneHotTRAINreg = trainData.map(parseRowOneHotRegression)
    oneHotTESTreg = testData.map(parseRowOneHotRegression)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="66214-265">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-265">**OUTPUT**</span></span>

<span data-ttu-id="66214-266">Tempo gasto tooexecute acima célula: 0.31 segundos</span><span class="sxs-lookup"><span data-stu-id="66214-266">Time taken tooexecute above cell: 0.31 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="66214-267">Dimensionamento de recursos</span><span class="sxs-lookup"><span data-stu-id="66214-267">Feature scaling</span></span>
<span data-ttu-id="66214-268">Dimensionamento de recurso, também conhecido como normalização de dados assegura que os recursos com valores amplamente distribuídos são não fornecido excessiva pesar na função objetivo hello.</span><span class="sxs-lookup"><span data-stu-id="66214-268">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> <span data-ttu-id="66214-269">código para o recurso de dimensionamento Hello usa Olá [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) variação de toounit tooscale Olá recursos.</span><span class="sxs-lookup"><span data-stu-id="66214-269">hello code for feature scaling uses hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello features toounit variance.</span></span> <span data-ttu-id="66214-270">Ele é fornecido pela MLlib para uso na regressão linear com SGD (Stochastic Gradient Descent).</span><span class="sxs-lookup"><span data-stu-id="66214-270">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD).</span></span> <span data-ttu-id="66214-271">O SGD é um algoritmo popular de treinamento de uma grande variedade de outros modelos de aprendizado de máquina, como regressões regularizadas ou SVM (máquinas de vetor de suporte).</span><span class="sxs-lookup"><span data-stu-id="66214-271">SGD is a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>   

> [!TIP]
> <span data-ttu-id="66214-272">Encontramos Olá LinearRegressionWithSGD algoritmo toobe toofeature confidencial dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="66214-272">We have found hello LinearRegressionWithSGD algorithm toobe sensitive toofeature scaling.</span></span>   
> 
> 

<span data-ttu-id="66214-273">Aqui está a variáveis de tooscale Olá código para uso com o algoritmo SGD linear Olá regularizada.</span><span class="sxs-lookup"><span data-stu-id="66214-273">Here is hello code tooscale variables for use with hello regularized linear SGD algorithm.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils

    # SCALE VARIABLES FOR REGULARIZED LINEAR SGD ALGORITHM
    label = oneHotTRAINreg.map(lambda x: x.label)
    features = oneHotTRAINreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTRAINregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    label = oneHotTESTreg.map(lambda x: x.label)
    features = oneHotTESTreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTESTregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="66214-274">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-274">**OUTPUT**</span></span>

<span data-ttu-id="66214-275">Tempo gasto tooexecute acima célula: 11.67 segundos</span><span class="sxs-lookup"><span data-stu-id="66214-275">Time taken tooexecute above cell: 11.67 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="66214-276">Armazenar objetos em cache na memória</span><span class="sxs-lookup"><span data-stu-id="66214-276">Cache objects in memory</span></span>
<span data-ttu-id="66214-277">tempo Olá para treinamento e teste de algoritmos ML pode ser reduzido ao armazenar em cache o quadro de dados de entrada hello objetos usados para classificação, regressão e recursos de escala.</span><span class="sxs-lookup"><span data-stu-id="66214-277">hello time taken for training and testing of ML algorithms can be reduced by caching hello input data frame objects used for classification, regression and, scaled features.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.cache()
    indexedTESTbinary.cache()
    oneHotTRAINbinary.cache()
    oneHotTESTbinary.cache()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.cache()
    indexedTESTreg.cache()
    oneHotTRAINreg.cache()
    oneHotTESTreg.cache()

    # SCALED FEATURES
    oneHotTRAINregScaled.cache()
    oneHotTESTregScaled.cache()

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="66214-278">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-278">**OUTPUT**</span></span> 

<span data-ttu-id="66214-279">Tempo gasto tooexecute acima célula: 0,13 segundos</span><span class="sxs-lookup"><span data-stu-id="66214-279">Time taken tooexecute above cell: 0.13 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="66214-280">Prever se uma gorjeta é paga ou não com modelos de classificação binária</span><span class="sxs-lookup"><span data-stu-id="66214-280">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="66214-281">Esta seção mostra como usar três modelos para tarefa de classificação binária Olá de prever se uma dica é pago por uma viagem táxi ou não.</span><span class="sxs-lookup"><span data-stu-id="66214-281">This section shows how use three models for hello binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="66214-282">modelos de saudação apresentados são:</span><span class="sxs-lookup"><span data-stu-id="66214-282">hello models presented are:</span></span>

* <span data-ttu-id="66214-283">Regressão logística</span><span class="sxs-lookup"><span data-stu-id="66214-283">Logistic regression</span></span> 
* <span data-ttu-id="66214-284">Floresta aleatória</span><span class="sxs-lookup"><span data-stu-id="66214-284">Random forest</span></span>
* <span data-ttu-id="66214-285">Árvores de Ampliação de Gradiente</span><span class="sxs-lookup"><span data-stu-id="66214-285">Gradient Boosting Trees</span></span>

<span data-ttu-id="66214-286">Cada seção de código de compilação de modelo é dividida em etapas:</span><span class="sxs-lookup"><span data-stu-id="66214-286">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="66214-287">**Modelar os dados de treinamento** com um conjunto de parâmetros</span><span class="sxs-lookup"><span data-stu-id="66214-287">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="66214-288">**Modelar a avaliação** em um conjunto de dados de teste com métricas</span><span class="sxs-lookup"><span data-stu-id="66214-288">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="66214-289">**Salvar modelo** no blob para consumo futuro</span><span class="sxs-lookup"><span data-stu-id="66214-289">**Saving model** in blob for future consumption</span></span>

<span data-ttu-id="66214-290">Vamos mostrar como toodo validação cruzada (VC) com o parâmetro de varredura de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="66214-290">We show how toodo cross-validation (CV) with parameter sweeping in two ways:</span></span>

1. <span data-ttu-id="66214-291">Usando **genérico** código personalizado que pode ser aplicado tooany algoritmo no parâmetro MLlib e tooany define em um algoritmo.</span><span class="sxs-lookup"><span data-stu-id="66214-291">Using **generic** custom code which can be applied tooany algorithm in MLlib and tooany parameter sets in an algorithm.</span></span> 
2. <span data-ttu-id="66214-292">Usando Olá **pySpark função do pipeline de CrossValidator**.</span><span class="sxs-lookup"><span data-stu-id="66214-292">Using hello **pySpark CrossValidator pipeline function**.</span></span> <span data-ttu-id="66214-293">Observe que o CrossValidator tem algumas limitações para o Spark 1.5.0:</span><span class="sxs-lookup"><span data-stu-id="66214-293">Note that CrossValidator has a few limitations for Spark 1.5.0:</span></span> 
   
   * <span data-ttu-id="66214-294">Os modelos de pipeline não podem ser salvos/persistidos para consumo futuro.</span><span class="sxs-lookup"><span data-stu-id="66214-294">Pipeline models cannot be saved/persisted for future consumption.</span></span>
   * <span data-ttu-id="66214-295">Não pode ser usado para todos os parâmetros em um modelo.</span><span class="sxs-lookup"><span data-stu-id="66214-295">Cannot be used for every parameter in a model.</span></span>
   * <span data-ttu-id="66214-296">Não pode ser usado para todos os algoritmos MLlib.</span><span class="sxs-lookup"><span data-stu-id="66214-296">Cannot be used for every MLlib algorithm.</span></span>

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-hello-logistic-regression-algorithm-for-binary-classification"></a><span data-ttu-id="66214-297">Genérico cruzado validação e limpeza hyperparameter usado com o algoritmo de regressão logística Olá para classificação binária</span><span class="sxs-lookup"><span data-stu-id="66214-297">Generic cross validation and hyperparameter sweeping used with hello logistic regression algorithm for binary classification</span></span>
<span data-ttu-id="66214-298">código de saudação nesta seção mostra como tootrain, avaliar e salvar um modelo de regressão logística com [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) que prevê se ou não uma dica é pago por uma viagem Olá NYC táxi o conjunto de dados de processamento e passagens.</span><span class="sxs-lookup"><span data-stu-id="66214-298">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="66214-299">modelo de saudação é treinado usando cruzada limpeza hyperparameter implementado com código personalizado que pode ser aplicado tooany de saudação MLlib algoritmos de aprendizado e validação (CV).</span><span class="sxs-lookup"><span data-stu-id="66214-299">hello model is trained using cross validation (CV) and hyperparameter sweeping implemented with custom code that can be applied tooany of hello learning algorithms in MLlib.</span></span>   

> [!NOTE]
> <span data-ttu-id="66214-300">execução de saudação desse código personalizado do VC pode levar vários minutos.</span><span class="sxs-lookup"><span data-stu-id="66214-300">hello execution of this custom CV code can take several minutes.</span></span>
> 
> 

<span data-ttu-id="66214-301">**Treinar o modelo de regressão logística hello usando VC e limpeza de hyperparameter**</span><span class="sxs-lookup"><span data-stu-id="66214-301">**Train hello logistic regression model using CV and hyperparameter sweeping**</span></span>

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from pyspark.mllib.evaluation import BinaryClassificationMetrics

    # CREATE PARAMETER GRID FOR LOGISTIC REGRESSION PARAMETER SWEEP
    from sklearn.grid_search import ParameterGrid
    grid = [{'regParam': [0.01, 0.1], 'iterations': [5, 10], 'regType': ["l1", "l2"], 'tolerance': [1e-3, 1e-4]}]
    paramGrid = list(ParameterGrid(grid))
    numModels = len(paramGrid)

    # SET NUM FOLDS AND NUM PARAMETER SETS tooSWEEP ON
    nFolds = 3;
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    # BEGIN CV WITH PARAMETER SWEEP
    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create LabeledPoints from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowOneHotBinary)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowOneHotBinary)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            regt = paramGrid[j]['regType']
            regp = paramGrid[j]['regParam']
            iters = paramGrid[j]['iterations']
            tol = paramGrid[j]['tolerance']
            # Train logistic regression model with hypermarameter set
            model = LogisticRegressionWithLBFGS.train(trainCVLabPt, regType=regt, iterations=iters,  
                                                      regParam=regp, tolerance = tol, intercept=True)
            predictionAndLabels = validationLabPt.map(lambda lp: (float(model.predict(lp.features)), lp.label))
            # Use ROC-AUC as accuracy metrics
            validMetrics = BinaryClassificationMetrics(predictionAndLabels)
            metric = validMetrics.areaUnderROC
            metricSum[j] += metric

    avgAcc = metricSum / nFolds;
    bestParam = paramGrid[np.argmax(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    # TRAIN ON FULL TRAIING SET USING BEST PARAMETERS FROM CV/PARAMETER SWEEP
    logitBest = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, regType=bestParam['regType'], 
                                                  iterations=bestParam['iterations'], 
                                                  regParam=bestParam['regParam'], tolerance = bestParam['tolerance'], 
                                                  intercept=True)


    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="66214-302">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-302">**OUTPUT**</span></span>

<span data-ttu-id="66214-303">Coeficientes: [0,0082065285375, -0,0223675576104, -0,0183812028036, -3,48124578069e-05, -0,00247646947233, -0,00165897881503, 0,0675394837328, -0,111823113101, -0,324609912762, -0,204549780032, -1,36499216354, 0,591088507921, -0,664263411392, -1,00439726852, 3,46567827545, -3,51025855172, -0,0471341112232, -0,043521833294, 0,000243375810385, 0,054518719222]</span><span class="sxs-lookup"><span data-stu-id="66214-303">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="66214-304">Interceptação: -0,0111216486893</span><span class="sxs-lookup"><span data-stu-id="66214-304">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="66214-305">Tempo gasto tooexecute acima célula: 14.43 segundos</span><span class="sxs-lookup"><span data-stu-id="66214-305">Time taken tooexecute above cell: 14.43 seconds</span></span>

<span data-ttu-id="66214-306">**Avaliar o modelo de classificação binária Olá com métricas padrão**</span><span class="sxs-lookup"><span data-stu-id="66214-306">**Evaluate hello binary classification model with standard metrics**</span></span>

<span data-ttu-id="66214-307">código Olá nesta seção mostra como tooevaluate uma regressão logística de modelo em um teste-conjunto de dados, incluindo um gráfico de saudação curva ROC.</span><span class="sxs-lookup"><span data-stu-id="66214-307">hello code in this section shows how tooevaluate a logistic regression model against a test data-set, including a plot of hello ROC curve.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT LIBRARIES
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # PREDICT ON TEST DATA WITH BEST/FINAL MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitBest.predict(lp.features)), lp.label))

    # INSTANTIATE METRICS OBJECT
    metrics = BinaryClassificationMetrics(predictionAndLabels)

    # AREA UNDER PRECISION-RECALL CURVE
    print("Area under PR = %s" % metrics.areaUnderPR)

    # AREA UNDER ROC CURVE
    print("Area under ROC = %s" % metrics.areaUnderROC)
    metrics = MulticlassMetrics(predictionAndLabels)

    # OVERALL STATISTICS
    precision = metrics.precision()
    recall = metrics.recall()
    f1Score = metrics.fMeasure()
    print("Summary Stats")
    print("Precision = %s" % precision)
    print("Recall = %s" % recall)
    print("F1 Score = %s" % f1Score)

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitBest.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="66214-308">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-308">**OUTPUT**</span></span>

<span data-ttu-id="66214-309">Área sob PR = 0,985336538462</span><span class="sxs-lookup"><span data-stu-id="66214-309">Area under PR = 0.985336538462</span></span>

<span data-ttu-id="66214-310">Área sob ROC = 0,983383274312</span><span class="sxs-lookup"><span data-stu-id="66214-310">Area under ROC = 0.983383274312</span></span>

<span data-ttu-id="66214-311">Estatísticas de resumo</span><span class="sxs-lookup"><span data-stu-id="66214-311">Summary Stats</span></span>

<span data-ttu-id="66214-312">Precisão = 0,984174341679</span><span class="sxs-lookup"><span data-stu-id="66214-312">Precision = 0.984174341679</span></span>

<span data-ttu-id="66214-313">Cancelamento = 0,984174341679</span><span class="sxs-lookup"><span data-stu-id="66214-313">Recall = 0.984174341679</span></span>

<span data-ttu-id="66214-314">Pontuação F1 = 0,984174341679</span><span class="sxs-lookup"><span data-stu-id="66214-314">F1 Score = 0.984174341679</span></span>

<span data-ttu-id="66214-315">Tempo gasto tooexecute acima célula: 2,67 segundos</span><span class="sxs-lookup"><span data-stu-id="66214-315">Time taken tooexecute above cell: 2.67 seconds</span></span>

<span data-ttu-id="66214-316">**Plote curva ROC hello.**</span><span class="sxs-lookup"><span data-stu-id="66214-316">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="66214-317">Olá *predictionAndLabelsDF* é registrado como uma tabela, *tmp_results*, na célula de saudação anterior.</span><span class="sxs-lookup"><span data-stu-id="66214-317">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="66214-318">*tmp_results* pode ser usado toodo consultas e resultados de saída em Olá sqlResults-quadro de dados para plotar.</span><span class="sxs-lookup"><span data-stu-id="66214-318">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="66214-319">Aqui está o código de saudação.</span><span class="sxs-lookup"><span data-stu-id="66214-319">Here is hello code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="66214-320">Aqui está o previsões de toomake código hello e Olá plotagem ROC curva.</span><span class="sxs-lookup"><span data-stu-id="66214-320">Here is hello code toomake predictions and plot hello ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES                              
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    #PREDICTIONS
    predictions_pddf = sqlResults.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVES
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


<span data-ttu-id="66214-321">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-321">**OUTPUT**</span></span>

![Curva ROC de regressão logística de abordagem genérica](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

<span data-ttu-id="66214-323">**Persistir o modelo em um blob para consumo futuro**</span><span class="sxs-lookup"><span data-stu-id="66214-323">**Persist model in a blob for future consumption**</span></span>

<span data-ttu-id="66214-324">código Olá nesta seção mostra como modelo de regressão logística de saudação toosave para consumo.</span><span class="sxs-lookup"><span data-stu-id="66214-324">hello code in this section shows how toosave hello logistic regression model for consumption.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    # PERSIST MODEL
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;

    logitBest.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";


<span data-ttu-id="66214-325">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-325">**OUTPUT**</span></span>

<span data-ttu-id="66214-326">Tempo gasto tooexecute acima célula: 34.57 segundos</span><span class="sxs-lookup"><span data-stu-id="66214-326">Time taken tooexecute above cell: 34.57 seconds</span></span>

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a><span data-ttu-id="66214-327">Usar a função de pipeline CrossValidator da MLlib com o modelo de regressão logística (Regressão elástica)</span><span class="sxs-lookup"><span data-stu-id="66214-327">Use MLlib's CrossValidator pipeline function with logistic regression (Elastic regression) model</span></span>
<span data-ttu-id="66214-328">código de saudação nesta seção mostra como tootrain, avaliar e salvar um modelo de regressão logística com [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) que prevê se ou não uma dica é pago por uma viagem Olá NYC táxi o conjunto de dados de processamento e passagens.</span><span class="sxs-lookup"><span data-stu-id="66214-328">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="66214-329">modelo de saudação é treinado usando validação cruzada (VC) e limpeza hyperparameter implementados com hello MLlib CrossValidator função de pipeline para VC com varredura de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="66214-329">hello model is trained using cross validation (CV) and hyperparameter sweeping implemented with hello MLlib CrossValidator pipeline function for CV with parameter sweep.</span></span>   

> [!NOTE]
> <span data-ttu-id="66214-330">execução de saudação do código MLlib VC pode levar vários minutos.</span><span class="sxs-lookup"><span data-stu-id="66214-330">hello execution of this MLlib CV code can take several minutes.</span></span>
> 
> 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.classification import LogisticRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import BinaryClassificationEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder
    from sklearn.metrics import roc_curve,auc

    # DEFINE ALGORITHM / MODEL
    lr = LogisticRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build()

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=BinaryClassificationEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA-FRAME: THIS DOES NOT RUN ON RDDs
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINbinary, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    ## PREDICT AND EVALUATE ON TEST DATA-SET

    # USE TEST DATASET FOR PREDICTION
    testDataFrame = sqlContext.createDataFrame(oneHotTESTbinary, ["features", "label"])
    test_predictions = cv_model.transform(testDataFrame)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="66214-331">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-331">**OUTPUT**</span></span>

<span data-ttu-id="66214-332">Tempo gasto tooexecute acima célula: 107.98 segundos</span><span class="sxs-lookup"><span data-stu-id="66214-332">Time taken tooexecute above cell: 107.98 seconds</span></span>

<span data-ttu-id="66214-333">**Plote curva ROC hello.**</span><span class="sxs-lookup"><span data-stu-id="66214-333">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="66214-334">Olá *predictionAndLabelsDF* é registrado como uma tabela, *tmp_results*, na célula de saudação anterior.</span><span class="sxs-lookup"><span data-stu-id="66214-334">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="66214-335">*tmp_results* pode ser usado toodo consultas e resultados de saída em Olá sqlResults-quadro de dados para plotar.</span><span class="sxs-lookup"><span data-stu-id="66214-335">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="66214-336">Aqui está o código de saudação.</span><span class="sxs-lookup"><span data-stu-id="66214-336">Here is hello code.</span></span>

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

<span data-ttu-id="66214-337">Aqui está a curva ROC Olá código tooplot hello.</span><span class="sxs-lookup"><span data-stu-id="66214-337">Here is hello code tooplot hello ROC curve.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES 
    %%local
    from sklearn.metrics import roc_curve,auc

    # ROC CURVE
    prob = [x["values"][1] for x in sqlResults["probability"]]
    fpr, tpr, thresholds = roc_curve(sqlResults['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    #PLOT
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


<span data-ttu-id="66214-338">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-338">**OUTPUT**</span></span>

![Curva ROC de regressão logística usando CrossValidator da MLlib](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="66214-340">Classificação de floresta aleatória</span><span class="sxs-lookup"><span data-stu-id="66214-340">Random forest classification</span></span>
<span data-ttu-id="66214-341">código Olá nesta seção mostra como tootrain, avaliar e salvar uma regressão de floresta aleatório que prevê se ou não uma dica é pago por uma viagem Olá NYC táxi viagem e passagens conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="66214-341">hello code in this section shows how tootrain, evaluate, and save a random forest regression that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # TRAIN RANDOMFOREST MODEL
    rfModel = RandomForest.trainClassifier(indexedTRAINbinary, numClasses=2, 
                                           categoricalFeaturesInfo=categoricalFeaturesInfo,
                                           numTrees=25, featureSubsetStrategy="auto",
                                           impurity='gini', maxDepth=5, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = rfModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp;
    dirfilename = modelDir + rfclassificationfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="66214-342">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-342">**OUTPUT**</span></span>

<span data-ttu-id="66214-343">Área sob ROC = 0,985336538462</span><span class="sxs-lookup"><span data-stu-id="66214-343">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="66214-344">Tempo gasto tooexecute acima célula: 26.72 segundos</span><span class="sxs-lookup"><span data-stu-id="66214-344">Time taken tooexecute above cell: 26.72 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="66214-345">Classificação de árvores de ampliação de gradiente</span><span class="sxs-lookup"><span data-stu-id="66214-345">Gradient boosting trees classification</span></span>
<span data-ttu-id="66214-346">código Olá nesta seção mostra como tootrain, avaliar e salvar um modelo de árvores de ampliação gradiente que prevê se ou não uma dica é pago por uma viagem Olá NYC táxi viagem e passagens conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="66214-346">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # Area under ROC curve
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN A BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp;
    dirfilename = modelDir + btclassificationfilename;

    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="66214-347">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-347">**OUTPUT**</span></span>

<span data-ttu-id="66214-348">Área sob ROC = 0,985336538462</span><span class="sxs-lookup"><span data-stu-id="66214-348">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="66214-349">Tempo gasto tooexecute acima célula: 28.13 segundos</span><span class="sxs-lookup"><span data-stu-id="66214-349">Time taken tooexecute above cell: 28.13 seconds</span></span>

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a><span data-ttu-id="66214-350">Prever valores de gorjetas com modelos de regressão (não usando CV)</span><span class="sxs-lookup"><span data-stu-id="66214-350">Predict tip amount with regression models (not using CV)</span></span>
<span data-ttu-id="66214-351">Esta seção mostra como usar três modelos para tarefa de regressão Olá: prever Olá dica quantidade pagada para uma viagem de táxi com base em outros recursos de dica.</span><span class="sxs-lookup"><span data-stu-id="66214-351">This section shows how use three models for hello regression task: predict hello tip amount paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="66214-352">modelos de saudação apresentados são:</span><span class="sxs-lookup"><span data-stu-id="66214-352">hello models presented are:</span></span>

* <span data-ttu-id="66214-353">Regressão linear regularizada</span><span class="sxs-lookup"><span data-stu-id="66214-353">Regularized linear regression</span></span>
* <span data-ttu-id="66214-354">Floresta aleatória</span><span class="sxs-lookup"><span data-stu-id="66214-354">Random forest</span></span>
* <span data-ttu-id="66214-355">Árvores de Ampliação de Gradiente</span><span class="sxs-lookup"><span data-stu-id="66214-355">Gradient Boosting Trees</span></span>

<span data-ttu-id="66214-356">Esses modelos foram descritos na introdução de saudação.</span><span class="sxs-lookup"><span data-stu-id="66214-356">These models were described in hello introduction.</span></span> <span data-ttu-id="66214-357">Cada seção de código de compilação de modelo é dividida em etapas:</span><span class="sxs-lookup"><span data-stu-id="66214-357">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="66214-358">**Modelar os dados de treinamento** com um conjunto de parâmetros</span><span class="sxs-lookup"><span data-stu-id="66214-358">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="66214-359">**Modelar a avaliação** em um conjunto de dados de teste com métricas</span><span class="sxs-lookup"><span data-stu-id="66214-359">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="66214-360">**Salvar modelo** no blob para consumo futuro</span><span class="sxs-lookup"><span data-stu-id="66214-360">**Saving model** in blob for future consumption</span></span>   

> <span data-ttu-id="66214-361">Observação do AZURE: As validação cruzada não é usada com três modelos de regressão Olá nesta seção, pois isso foi mostrado em detalhes para modelos de regressão logística hello.</span><span class="sxs-lookup"><span data-stu-id="66214-361">AZURE NOTE: Cross-validation is not used with hello three regression models in this section, since this was shown in detail for hello logistic regression models.</span></span> <span data-ttu-id="66214-362">Um exemplo que mostra como toouse VC com Elástico Net para regressão linear é fornecida no hello Apêndice deste tópico.</span><span class="sxs-lookup"><span data-stu-id="66214-362">An example showing how toouse CV with Elastic Net for linear regression is provided in hello Appendix of this topic.</span></span>
> 
> <span data-ttu-id="66214-363">Observação do AZURE: Em nossa experiência, pode haver problemas com convergência de LinearRegressionWithSGD modelos e parâmetros necessário toobe alterado/otimizado cuidadosamente para obter um modelo válido.</span><span class="sxs-lookup"><span data-stu-id="66214-363">AZURE NOTE: In our experience, there can be issues with convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="66214-364">O dimensionamento de variáveis ajuda significativamente com a convergência.</span><span class="sxs-lookup"><span data-stu-id="66214-364">Scaling of variables significantly helps with convergence.</span></span> <span data-ttu-id="66214-365">Elástico regressão net, mostrado Olá apêndice toothis tópico, também pode ser usado em vez de LinearRegressionWithSGD.</span><span class="sxs-lookup"><span data-stu-id="66214-365">Elastic net regression, shown in hello Appendix toothis topic, can also be used instead of LinearRegressionWithSGD.</span></span>
> 
> 

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="66214-366">Regressão linear com SGD</span><span class="sxs-lookup"><span data-stu-id="66214-366">Linear regression with SGD</span></span>
<span data-ttu-id="66214-367">Olá código nesta seção mostra como toouse dimensionado recursos tootrain uma regressão linear usa descendente do gradiente estocástico (SGD) para a otimização, e como tooscore, avaliar e Salvar modelo Olá no armazenamento de Blob do Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="66214-367">hello code in this section shows how toouse scaled features tootrain a linear regression that uses stochastic gradient descent (SGD) for optimization, and how tooscore, evaluate, and save hello model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="66214-368">Em nossa experiência, pode haver problemas com convergência de saudação de LinearRegressionWithSGD modelos e parâmetros necessário toobe alterado/otimizado cuidadosamente para obter um modelo válido.</span><span class="sxs-lookup"><span data-stu-id="66214-368">In our experience, there can be issues with hello convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="66214-369">O dimensionamento de variáveis ajuda significativamente com a convergência.</span><span class="sxs-lookup"><span data-stu-id="66214-369">Scaling of variables significantly helps with convergence.</span></span>
> 
> 

    # LINEAR REGRESSION WITH SGD 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES tooTRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="66214-370">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-370">**OUTPUT**</span></span>

<span data-ttu-id="66214-371">Coeficientes: [0,0141707753435, -0,0252930927087, -0,0231442517137, 0,247070902996, 0,312544147152, 0,360296120645, 0,0122079566092, -0,00456498588241, -0,0898228505177, 0,0714046248793, 0,102171263868, 0,100022455632, -0,00289545676449, -0,00791124681938, 0,54396316518, -0,536293513569, 0,0119076553369, -0,0173039244582, 0,0119632796147, 0,00146764882502]</span><span class="sxs-lookup"><span data-stu-id="66214-371">Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span></span>

<span data-ttu-id="66214-372">Interceptação: 0,854507624459</span><span class="sxs-lookup"><span data-stu-id="66214-372">Intercept: 0.854507624459</span></span>

<span data-ttu-id="66214-373">RMSE = 1,23485131376</span><span class="sxs-lookup"><span data-stu-id="66214-373">RMSE = 1.23485131376</span></span>

<span data-ttu-id="66214-374">R-sqr = 0,597963951127</span><span class="sxs-lookup"><span data-stu-id="66214-374">R-sqr = 0.597963951127</span></span>

<span data-ttu-id="66214-375">Tempo gasto tooexecute acima célula: 38.62 segundos</span><span class="sxs-lookup"><span data-stu-id="66214-375">Time taken tooexecute above cell: 38.62 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="66214-376">Regressão de Floresta Aleatória</span><span class="sxs-lookup"><span data-stu-id="66214-376">Random Forest regression</span></span>
<span data-ttu-id="66214-377">código Olá nesta seção mostra como tootrain, avaliar e salvar um modelo de floresta aleatório que prevê a quantidade de dica de saudação dados de viagem táxi NYC.</span><span class="sxs-lookup"><span data-stu-id="66214-377">hello code in this section shows how tootrain, evaluate, and save a random forest model that predicts tip amount for hello NYC taxi trip data.</span></span>   

> [!NOTE]
> <span data-ttu-id="66214-378">A validação cruzada com o parâmetro de varredura usando código personalizado é fornecida no Apêndice hello.</span><span class="sxs-lookup"><span data-stu-id="66214-378">Cross-validation with parameter sweeping using custom code is provided in hello appendix.</span></span>
> 
> 

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    # UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp;
    dirfilename = modelDir + rfregressionfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="66214-379">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-379">**OUTPUT**</span></span>

<span data-ttu-id="66214-380">RMSE = 0,931981967875</span><span class="sxs-lookup"><span data-stu-id="66214-380">RMSE = 0.931981967875</span></span>

<span data-ttu-id="66214-381">R-sqr = 0,733445485802</span><span class="sxs-lookup"><span data-stu-id="66214-381">R-sqr = 0.733445485802</span></span>

<span data-ttu-id="66214-382">Tempo gasto tooexecute acima célula: 25.98 segundos</span><span class="sxs-lookup"><span data-stu-id="66214-382">Time taken tooexecute above cell: 25.98 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="66214-383">Regressão de árvores de ampliação de gradiente</span><span class="sxs-lookup"><span data-stu-id="66214-383">Gradient boosting trees regression</span></span>
<span data-ttu-id="66214-384">código Olá nesta seção mostra como tootrain, avaliar e salvar um modelo de árvores de ampliação gradiente que prevê a quantidade de dica de saudação dados de viagem táxi NYC.</span><span class="sxs-lookup"><span data-stu-id="66214-384">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts tip amount for hello NYC taxi trip data.</span></span>

<span data-ttu-id="66214-385">**Treinar e avaliar**</span><span class="sxs-lookup"><span data-stu-id="66214-385">**Train and evaluate **</span></span>

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    # EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES
    test_predictions= sqlContext.createDataFrame(predictionAndLabels)
    test_predictions_pddf = test_predictions.toPandas()

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="66214-386">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-386">**OUTPUT**</span></span>

<span data-ttu-id="66214-387">RMSE = 0,928172197114</span><span class="sxs-lookup"><span data-stu-id="66214-387">RMSE = 0.928172197114</span></span>

<span data-ttu-id="66214-388">R-sqr = 0,732680354389</span><span class="sxs-lookup"><span data-stu-id="66214-388">R-sqr = 0.732680354389</span></span>

<span data-ttu-id="66214-389">Tempo gasto tooexecute acima célula: 20.9 segundos</span><span class="sxs-lookup"><span data-stu-id="66214-389">Time taken tooexecute above cell: 20.9 seconds</span></span>

<span data-ttu-id="66214-390">**Plotar**</span><span class="sxs-lookup"><span data-stu-id="66214-390">**Plot**</span></span>

<span data-ttu-id="66214-391">*tmp_results* é registrado como uma tabela Hive na célula anterior hello.</span><span class="sxs-lookup"><span data-stu-id="66214-391">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="66214-392">Resultados da tabela de saudação são saída Olá *sqlResults* quadro de dados para plotar.</span><span class="sxs-lookup"><span data-stu-id="66214-392">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="66214-393">Aqui está o código de saudação</span><span class="sxs-lookup"><span data-stu-id="66214-393">Here is hello code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="66214-394">Aqui está a dados Olá código tooplot hello usando Olá Jupyter server.</span><span class="sxs-lookup"><span data-stu-id="66214-394">Here is hello code tooplot hello data using hello Jupyter server.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import numpy as np

    # PLOT
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['_1'], sqlResults['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(sqlResults['_1'], fit[0] * sqlResults['_1'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 15])
    plt.show(ax)

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a><span data-ttu-id="66214-396">Apêndice: Tarefas de regressão adicionais usando a validação cruzada com limpezas de parâmetro</span><span class="sxs-lookup"><span data-stu-id="66214-396">Appendix: Additional regression tasks using cross validation with parameter sweeps</span></span>
<span data-ttu-id="66214-397">Este apêndice contém mostrando código como toodo VC usando net Elástico para regressão linear e como toodo VC com parâmetro de varredura usando código personalizado para regressão de floresta aleatório.</span><span class="sxs-lookup"><span data-stu-id="66214-397">This appendix contains code showing how toodo CV using Elastic net for linear regression and how toodo CV with parameter sweep using custom code for random forest regression.</span></span>

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a><span data-ttu-id="66214-398">Validação cruzada usando a rede elástica para a regressão linear</span><span class="sxs-lookup"><span data-stu-id="66214-398">Cross validation using Elastic net for linear regression</span></span>
<span data-ttu-id="66214-399">código Olá nesta seção mostra como toodo cruzada validação usando elástica net para regressão linear e como tooevaluate Olá modelo com base em dados de teste.</span><span class="sxs-lookup"><span data-stu-id="66214-399">hello code in this section shows how toodo cross validation using Elastic net for linear regression and how tooevaluate hello model against test data.</span></span>

    ###  CV USING ELASTIC NET FOR LINEAR REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.regression import LinearRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import RegressionEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder

    # DEFINE ALGORITHM/MODEL
    lr = LinearRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build() 

    # DEFINE PIPELINE 
    # SIMPLY hello MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses hello best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT tooDF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="66214-400">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-400">**OUTPUT**</span></span>

<span data-ttu-id="66214-401">Tempo gasto tooexecute acima célula: 161.21 segundos</span><span class="sxs-lookup"><span data-stu-id="66214-401">Time taken tooexecute above cell: 161.21  seconds</span></span>

<span data-ttu-id="66214-402">**Avaliar com a métrica R-SQR**</span><span class="sxs-lookup"><span data-stu-id="66214-402">**Evaluate with R-SQR metric**</span></span>

<span data-ttu-id="66214-403">*tmp_results* é registrado como uma tabela Hive na célula anterior hello.</span><span class="sxs-lookup"><span data-stu-id="66214-403">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="66214-404">Resultados da tabela de saudação são saída Olá *sqlResults* quadro de dados para plotar.</span><span class="sxs-lookup"><span data-stu-id="66214-404">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="66214-405">Aqui está o código de saudação</span><span class="sxs-lookup"><span data-stu-id="66214-405">Here is hello code</span></span>

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


<span data-ttu-id="66214-406">Aqui está a saudação código toocalculate sqr R.</span><span class="sxs-lookup"><span data-stu-id="66214-406">Here is hello code toocalculate R-sqr.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


<span data-ttu-id="66214-407">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-407">**OUTPUT**</span></span>

<span data-ttu-id="66214-408">R-sqr = 0,619184907088</span><span class="sxs-lookup"><span data-stu-id="66214-408">R-sqr = 0.619184907088</span></span>

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a><span data-ttu-id="66214-409">Validação cruzada com limpeza de parâmetro usando o código personalizado para a regressão de floresta aleatória</span><span class="sxs-lookup"><span data-stu-id="66214-409">Cross validation with parameter sweep using custom code for random forest regression</span></span>
<span data-ttu-id="66214-410">código Olá nesta seção mostra como toodo validação cruzada com varredura de parâmetro usando código personalizado para regressão de floresta aleatório e como tooevaluate Olá modelo com base em dados de teste.</span><span class="sxs-lookup"><span data-stu-id="66214-410">hello code in this section shows how toodo cross validation with parameter sweep using custom code for random forest regression and how tooevaluate hello model against test data.</span></span>

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    # GET ACCURARY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics
    from sklearn.grid_search import ParameterGrid

    ## CREATE PARAMETER GRID
    grid = [{'maxDepth': [5,10], 'numTrees': [25,50]}]
    paramGrid = list(ParameterGrid(grid))

    ## SPECIFY LEVELS OF CATEGORICAL VARIBLES
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # SPECIFY NUMFOLDS AND ARRAY tooHOLD METRICS
    nFolds = 3;
    numModels = len(paramGrid)
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create labeled points from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowIndexingRegression)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowIndexingRegression)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            maxD = paramGrid[j]['maxDepth']
            numT = paramGrid[j]['numTrees']
            # Train logistic regression model with hypermarameter set
            rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=numT, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=maxD, maxBins=32)
            predictions = rfModel.predict(validationLabPt.map(lambda x: x.features))
            predictionAndLabels = validationLabPt.map(lambda lp: lp.label).zip(predictions)
            # Use ROC-AUC as accuracy metrics
            validMetrics = RegressionMetrics(predictionAndLabels)
            metric = validMetrics.rootMeanSquaredError
            metricSum[j] += metric

    avgAcc = metricSum/nFolds;
    bestParam = paramGrid[np.argmin(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    ## TRAIN FINAL MODL WIHT BEST PARAMETERS
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=bestParam['numTrees'], featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=bestParam['maxDepth'], maxBins=32)

    # EVALUATE MODEL ON TEST DATA
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    #PRINT TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="66214-411">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-411">**OUTPUT**</span></span>

<span data-ttu-id="66214-412">RMSE = 0,906972198262</span><span class="sxs-lookup"><span data-stu-id="66214-412">RMSE = 0.906972198262</span></span>

<span data-ttu-id="66214-413">R-sqr = 0,740751197012</span><span class="sxs-lookup"><span data-stu-id="66214-413">R-sqr = 0.740751197012</span></span>

<span data-ttu-id="66214-414">Tempo gasto tooexecute acima célula: 69.17 segundos</span><span class="sxs-lookup"><span data-stu-id="66214-414">Time taken tooexecute above cell: 69.17 seconds</span></span>

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a><span data-ttu-id="66214-415">Limpar objetos da memória e imprimir os locais de modelo</span><span class="sxs-lookup"><span data-stu-id="66214-415">Clean up objects from memory and print model locations</span></span>
<span data-ttu-id="66214-416">Use `unpersist()` toodelete objetos armazenados em cache na memória.</span><span class="sxs-lookup"><span data-stu-id="66214-416">Use `unpersist()` toodelete objects cached in memory.</span></span>

    # UNPERSIST OBJECTS CACHED IN MEMORY

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()
    trainData.unpersist()
    trainData.unpersist()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.unpersist()
    indexedTESTbinary.unpersist()
    oneHotTRAINbinary.unpersist()
    oneHotTESTbinary.unpersist()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.unpersist()
    indexedTESTreg.unpersist()
    oneHotTRAINreg.unpersist()
    oneHotTESTreg.unpersist()

    # SCALED FEATURES
    oneHotTRAINregScaled.unpersist()
    oneHotTESTregScaled.unpersist()


<span data-ttu-id="66214-417">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-417">**OUTPUT**</span></span>

<span data-ttu-id="66214-418">PythonRDD[122] em RDD em PythonRDD.scala:43</span><span class="sxs-lookup"><span data-stu-id="66214-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span></span>

<span data-ttu-id="66214-419">* * Impressão caminho toomodel arquivos toobe usado no bloco de anotações de consumo de saudação.</span><span class="sxs-lookup"><span data-stu-id="66214-419">**Printout path toomodel files toobe used in hello consumption notebook.</span></span> <span data-ttu-id="66214-420">* * tooconsume e pontuação um independente de-conjunto de dados, você precisa toocopy e cole esses nomes de arquivo hello "Bloco de anotações de consumo".</span><span class="sxs-lookup"><span data-stu-id="66214-420">** tooconsume and score an independent data-set, you need toocopy and paste these file names in hello "Consumption notebook".</span></span>

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="66214-421">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="66214-421">**OUTPUT**</span></span>

<span data-ttu-id="66214-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span><span class="sxs-lookup"><span data-stu-id="66214-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span></span>

<span data-ttu-id="66214-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span><span class="sxs-lookup"><span data-stu-id="66214-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span></span>

<span data-ttu-id="66214-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span><span class="sxs-lookup"><span data-stu-id="66214-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span></span>

<span data-ttu-id="66214-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span><span class="sxs-lookup"><span data-stu-id="66214-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span></span>

<span data-ttu-id="66214-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span><span class="sxs-lookup"><span data-stu-id="66214-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span></span>

<span data-ttu-id="66214-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span><span class="sxs-lookup"><span data-stu-id="66214-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span></span>

## <a name="whats-next"></a><span data-ttu-id="66214-428">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="66214-428">What's next?</span></span>
<span data-ttu-id="66214-429">Agora que você criou modelos de classificação e regressão com hello Spark MlLib, você está pronto toolearn como tooscore e avaliar esses modelos.</span><span class="sxs-lookup"><span data-stu-id="66214-429">Now that you have created regression and classification models with hello Spark MlLib, you are ready toolearn how tooscore and evaluate these models.</span></span>

<span data-ttu-id="66214-430">**Consumo de modelo:** toolearn como tooscore e avaliar modelos de classificação e regressão de saudação criados neste tópico, consulte [pontuação e avaliar modelos de aprendizado de máquina criados Spark](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="66214-430">**Model consumption:** toolearn how tooscore and evaluate hello classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

