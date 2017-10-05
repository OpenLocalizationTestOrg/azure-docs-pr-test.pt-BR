---
title: "Modelagem e exploração de dados avançados com o Spark | Microsoft Docs"
description: "Use o HDInsight Spark para fazer a exploração de dados e treinar modelos de classificação e regressão binários usando a validação cruzada e a otimização de hiperparâmetro."
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
ms.openlocfilehash: e6bf6bd3c905f077841ef166540337a251b91ad1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a><span data-ttu-id="65398-103">Modelagem e exploração de dados avançados com o Spark</span><span class="sxs-lookup"><span data-stu-id="65398-103">Advanced data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="65398-104">Este passo a passo usa o HDInsight Spark para executar a exploração de dados e treinar a classificação binária e os modelos de regressão usando validação cruzada e otimização de hiperparâmetro em uma amostra do conjunto de dados de corridas e tarifas de táxi em Nova York de 2013.</span><span class="sxs-lookup"><span data-stu-id="65398-104">This walkthrough uses HDInsight Spark to do data exploration and train binary classification and regression models using cross-validation and hyperparameter optimization on a sample of the NYC taxi trip and fare 2013 dataset.</span></span> <span data-ttu-id="65398-105">Ele o orienta ao longo das etapas do [Processo de Ciência de Dados](http://aka.ms/datascienceprocess), de ponta a ponta, usando um cluster HDInsight Spark para processamento e blobs do Azure para armazenar os dados e os modelos.</span><span class="sxs-lookup"><span data-stu-id="65398-105">It walks you through the steps of the [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs to store the data and the models.</span></span> <span data-ttu-id="65398-106">O processo explora e visualiza os dados transferidos de um Blob de Armazenamento do Azure e prepara os dados para criar modelos preditivos.</span><span class="sxs-lookup"><span data-stu-id="65398-106">The process explores and visualizes data brought in from an Azure Storage Blob and then prepares the data to build predictive models.</span></span> <span data-ttu-id="65398-107">Python foi usado para codificar a solução e mostrar os gráficos relevantes.</span><span class="sxs-lookup"><span data-stu-id="65398-107">Python has been used to code the solution and to show the relevant plots.</span></span> <span data-ttu-id="65398-108">Esses modelos são compilados usando o kit de ferramentas Spark MLlib para executar tarefas de classificação binária e modelagem de regressão.</span><span class="sxs-lookup"><span data-stu-id="65398-108">These models are build using the Spark MLlib toolkit to do binary classification and regression modeling tasks.</span></span> 

* <span data-ttu-id="65398-109">A tarefa de **classificação binária** consiste em prever se uma gorjeta é paga ou não pela corrida.</span><span class="sxs-lookup"><span data-stu-id="65398-109">The **binary classification** task is to predict whether or not a tip is paid for the trip.</span></span> 
* <span data-ttu-id="65398-110">A tarefa de **regressão** consiste em prever o valor da gorjeta com base em outros recursos de gorjeta.</span><span class="sxs-lookup"><span data-stu-id="65398-110">The **regression** task is to predict the amount of the tip based on other tip features.</span></span> 

<span data-ttu-id="65398-111">As etapas de modelagem também contêm código que mostra como treinar, avaliar e salvar cada tipo de modelo.</span><span class="sxs-lookup"><span data-stu-id="65398-111">The modeling steps also contain code showing how to train, evaluate, and save each type of model.</span></span> <span data-ttu-id="65398-112">O tópico aborda alguns dos mesmos assuntos como o tópico [Modelagem e exploração de dados com Spark](machine-learning-data-science-spark-data-exploration-modeling.md).</span><span class="sxs-lookup"><span data-stu-id="65398-112">The topic covers some of the same ground as the [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic.</span></span> <span data-ttu-id="65398-113">Porém, ele é mais "avançado", já que também utiliza a validação cruzada com a varredura de hiperparâmetro para treinar modelos de classificação e regressão ideal precisos.</span><span class="sxs-lookup"><span data-stu-id="65398-113">But it is more "advanced" in that it also uses cross-validation with hyperparameter sweeping to train optimally accurate classification and regression models.</span></span> 

<span data-ttu-id="65398-114">**CV (Validação cruzada)** é uma técnica que avalia quão bem um modelo treinado em um conjunto de dados conhecido é generalizado para prever os recursos dos conjuntos de dados nos quais ele não foi treinado.</span><span class="sxs-lookup"><span data-stu-id="65398-114">**Cross-validation (CV)** is a technique that assesses how well a model trained on a known set of data generalizes to predicting the features of datasets on which it has not been trained.</span></span>  <span data-ttu-id="65398-115">Uma implementação comum usada aqui é dividir um conjunto de dados em partições K e, em seguida, treinar o modelo em um estilo round-robin em todas, exceto uma das partições.</span><span class="sxs-lookup"><span data-stu-id="65398-115">A common implementation used here is to divide a dataset into K folds and then train the model in a round-robin fashion on all but one of the folds.</span></span> <span data-ttu-id="65398-116">Avaliamos a capacidade do modelo de prever com precisão quando testado em relação ao conjunto de dados independente na partição que não foi usada para treinar o modelo.</span><span class="sxs-lookup"><span data-stu-id="65398-116">The ability of the model to prediction accurately when tested against the independent dataset in this fold not used to train the model is assessed.</span></span>

<span data-ttu-id="65398-117">**Otimização do hiperparâmetro** é o problema de escolher um conjunto de hiperparâmetros para um algoritmo de aprendizado, normalmente com o objetivo de otimizar uma medida de desempenho do algoritmo em um conjunto de dados independente.</span><span class="sxs-lookup"><span data-stu-id="65398-117">**Hyperparameter optimization** is the problem of choosing a set of hyperparameters for a learning algorithm, usually with the goal of optimizing a measure of the algorithm's performance on an independent data set.</span></span> <span data-ttu-id="65398-118">**Hiperparâmetros** são valores que devem ser especificados fora do procedimento de treinamento do modelo.</span><span class="sxs-lookup"><span data-stu-id="65398-118">**Hyperparameters** are values that must be specified outside of the model training procedure.</span></span> <span data-ttu-id="65398-119">As suposições sobre esses valores podem afetar a flexibilidade e a precisão dos modelos.</span><span class="sxs-lookup"><span data-stu-id="65398-119">Assumptions about these values can impact the flexibility and accuracy of the models.</span></span> <span data-ttu-id="65398-120">As árvores de decisão têm hiperparâmetros, por exemplo, como a profundidade desejada e o número de folhas na árvore.</span><span class="sxs-lookup"><span data-stu-id="65398-120">Decision trees have hyperparameters, for example, such as the desired depth and number of leaves in the tree.</span></span> <span data-ttu-id="65398-121">As SVMs (Máquinas de Vetor de Suporte) exigem a configuração de um termo de penalidade de classificação incorreta.</span><span class="sxs-lookup"><span data-stu-id="65398-121">Support Vector Machines (SVMs) require setting a misclassification penalty term.</span></span> 

<span data-ttu-id="65398-122">Uma maneira comum de executar a otimização de hiperparâmetro usada aqui é uma pesquisa de grade ou um **limpeza de parâmetro**.</span><span class="sxs-lookup"><span data-stu-id="65398-122">A common way to perform hyperparameter optimization used here is a grid search, or a **parameter sweep**.</span></span> <span data-ttu-id="65398-123">Isso consiste em realizar uma pesquisa detalhada pelos valores de um subconjunto especificado do espaço do hiperparâmetro para um algoritmo de aprendizado.</span><span class="sxs-lookup"><span data-stu-id="65398-123">This consists of performing an exhaustive search through the values a specified subset of the hyperparameter space for a learning algorithm.</span></span> <span data-ttu-id="65398-124">A validação cruzada pode fornecer uma métrica de desempenho para classificar os resultados ideais produzidos pelo algoritmo de pesquisa de grade.</span><span class="sxs-lookup"><span data-stu-id="65398-124">Cross validation can supply a performance metric to sort out the optimal results produced by the grid search algorithm.</span></span> <span data-ttu-id="65398-125">A CV usada com a limpeza do hiperparâmetro limita os problemas como sobreajuste de um modelo de dados de treinamento para que o modelo mantenha a capacidade de se aplicar ao conjunto de dados geral do qual os dados de treinamento foram extraídos.</span><span class="sxs-lookup"><span data-stu-id="65398-125">CV used with hyperparameter sweeping helps limit problems like overfitting a model to training data so that the model retains the capacity to apply to the general set of data from which the training data was extracted.</span></span>

<span data-ttu-id="65398-126">Os modelos que usamos incluem regressão logística e linear, florestas aleatórias e árvores aumentadas gradientes:</span><span class="sxs-lookup"><span data-stu-id="65398-126">The models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="65398-127">[Regressão linear com SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) é um modelo de regressão linear que usa um método SGD (Stochastic Gradient Descent) para otimização e dimensionamento de recursos para prever os valores das gorjetas pagas.</span><span class="sxs-lookup"><span data-stu-id="65398-127">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling to predict the tip amounts paid.</span></span> 
* <span data-ttu-id="65398-128">[Regressão logística com LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) ou regressão "logit" é um modelo de regressão que pode ser usado quando a variável dependente é categórica para fazer a classificação de dados.</span><span class="sxs-lookup"><span data-stu-id="65398-128">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when the dependent variable is categorical to do data classification.</span></span> <span data-ttu-id="65398-129">LBFGS é um algoritmo de otimização quase Newton que aproxima o algoritmo BFGS (Broyden–Fletcher–Goldfarb–Shanno) usando uma quantidade limitada de memória do computador e que é amplamente usado no aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="65398-129">LBFGS is a quasi-Newton optimization algorithm that approximates the Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="65398-130">[Florestas aleatórias](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) são conjuntos de árvores de decisão.</span><span class="sxs-lookup"><span data-stu-id="65398-130">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="65398-131">Elas combinam várias árvores de decisão para reduzir o risco de superajuste.</span><span class="sxs-lookup"><span data-stu-id="65398-131">They combine many decision trees to reduce the risk of overfitting.</span></span> <span data-ttu-id="65398-132">Florestas aleatórias são usadas para classificação e regressão e podem manipular recursos categóricos e podem ser estendidas para a configuração de classificação multiclasse.</span><span class="sxs-lookup"><span data-stu-id="65398-132">Random forests are used for regression and classification and can handle categorical features and can be extended to the multiclass classification setting.</span></span> <span data-ttu-id="65398-133">Elas não exigem o dimensionamento de recursos e são capazes de capturar não linearidades e interações de recursos.</span><span class="sxs-lookup"><span data-stu-id="65398-133">They do not require feature scaling and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="65398-134">As florestas aleatórias são um dos modelos de aprendizado de máquina com maior taxa de sucesso para classificação e regressão.</span><span class="sxs-lookup"><span data-stu-id="65398-134">Random forests are one of the most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="65398-135">[GBTs (árvores com aumento gradiente)](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) são conjuntos de árvores de decisão.</span><span class="sxs-lookup"><span data-stu-id="65398-135">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="65398-136">As GBTs treinam árvores de decisão iterativamente para minimizar uma função de perda.</span><span class="sxs-lookup"><span data-stu-id="65398-136">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="65398-137">As GBTs são usadas para regressão e classificação e podem lidar com recursos categóricos, não exigem o dimensionamento de recursos e podem capturar não linearidades e interações de recursos.</span><span class="sxs-lookup"><span data-stu-id="65398-137">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="65398-138">Elas também podem ser usadas em uma configuração de classificação multiclasse.</span><span class="sxs-lookup"><span data-stu-id="65398-138">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="65398-139">Os exemplos de modelagem usando CV e limpeza de hiperparâmetro são mostrados para o problema de classificação binária.</span><span class="sxs-lookup"><span data-stu-id="65398-139">Modeling examples using CV and Hyperparameter sweep are shown for the binary classification problem.</span></span> <span data-ttu-id="65398-140">Exemplos mais simples (sem limpezas de parâmetro) são apresentados no tópico principal para tarefas de regressão.</span><span class="sxs-lookup"><span data-stu-id="65398-140">Simpler examples (without parameter sweeps) are presented in the main topic for regression tasks.</span></span> <span data-ttu-id="65398-141">Mas no apêndice, a validação usando a rede elástica para regressão linear e a CV com a limpeza de parâmetros usando a regressão de floresta aleatória também são apresentadas.</span><span class="sxs-lookup"><span data-stu-id="65398-141">But in the appendix, validation using elastic net for linear regression and CV with parameter sweep using for random forest regression are also presented.</span></span> <span data-ttu-id="65398-142">A **rede elástica** é um método de regressão regularizado para ajustar os modelos de regressão linear que combina linearmente as métricas L1 e L2 como penalidades dos métodos [laço](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) e [ressalto](https://en.wikipedia.org/wiki/Tikhonov_regularization).</span><span class="sxs-lookup"><span data-stu-id="65398-142">The **elastic net** is a regularized regression method for fitting linear regression models that linearly combines the L1 and L2 metrics as penalties of the [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) and [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) methods.</span></span>   

> [!NOTE]
> <span data-ttu-id="65398-143">Embora o kit de ferramentas Spark MLlib tenha sido projetado para trabalhar com grandes conjuntos de dados, uma amostra relativamente pequena (cerca de 30 Mb usando 170 mil linhas, cerca de 0,1% do conjunto de dados original NYC) foi usada por conveniência.</span><span class="sxs-lookup"><span data-stu-id="65398-143">Although the Spark MLlib toolkit is designed to work on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of the original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="65398-144">O exercício fornecido aqui é executado com eficiência (em cerca de 10 minutos) em um cluster HDInsight com dois nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="65398-144">The exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="65398-145">O mesmo código, com pequenas modificações, pode ser usado para processar conjuntos de dados maiores, com as modificações apropriadas para armazenar dados na memória em cache e alterar o tamanho do cluster.</span><span class="sxs-lookup"><span data-stu-id="65398-145">The same code, with minor modifications, can be used to process larger data-sets, with appropriate modifications for caching data in memory and changing the cluster size.</span></span>
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a><span data-ttu-id="65398-146">Instalação: blocos de notas e clusters do Spark</span><span class="sxs-lookup"><span data-stu-id="65398-146">Setup: Spark clusters and notebooks</span></span>
<span data-ttu-id="65398-147">As etapas de configuração e o código são fornecidos neste passo a passo para usar um HDInsight Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="65398-147">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="65398-148">Porém, notebooks Jupyter são fornecidos tanto para o HDInsight Spark 1.6 quanto para os clusters Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="65398-148">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="65398-149">Uma descrição de notebooks e links são fornecidos em [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) para o repositório do GitHub que os contém.</span><span class="sxs-lookup"><span data-stu-id="65398-149">A description of the notebooks and links to them are provided in the [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for the GitHub repository containing them.</span></span> <span data-ttu-id="65398-150">No entanto, o código mostrado aqui e nos notebooks vinculados é genérico e funcionarão em qualquer cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="65398-150">Moreover, the code here and in the linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="65398-151">Se você não estiver usando o HDInsight Spark, as etapas de configuração e gerenciamento do cluster poderão ser ligeiramente diferentes do que é mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="65398-151">If you are not using HDInsight Spark, the cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="65398-152">Para sua conveniência, aqui estão os links para os blocos de notas Jupyter para Spark 1.6 e 2.0 para execução no kernel pyspark do servidor de bloco de notas Jupyter:</span><span class="sxs-lookup"><span data-stu-id="65398-152">For convenience, here are the links to the Jupyter notebooks for Spark 1.6 and 2.0 to be run in the pyspark kernel of the Jupyter Notebook server:</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="65398-153">Blocos de notas Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="65398-153">Spark 1.6 notebooks</span></span>

<span data-ttu-id="65398-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): inclui tópicos no blocos de notas nº. 1 e o desenvolvimento de modelos usando validação cruzada e ajuste de hiperparâmetro.</span><span class="sxs-lookup"><span data-stu-id="65398-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Includes topics in notebook #1, and model development using hyperparameter tuning and cross-validation.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="65398-155">Blocos de notas Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="65398-155">Spark 2.0 notebooks</span></span>

<span data-ttu-id="65398-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): este arquivo fornece informações sobre como executar exploração, modelagem e pontuação de dados em clusters Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="65398-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how to perform data exploration, modeling, and scoring in Spark 2.0 clusters.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-the-preset-spark-context"></a><span data-ttu-id="65398-157">Instalação: locais de armazenamento, bibliotecas e o contexto predefinido do Spark</span><span class="sxs-lookup"><span data-stu-id="65398-157">Setup: storage locations, libraries, and the preset Spark context</span></span>
<span data-ttu-id="65398-158">O Spark pode ler e gravar em um Blob de Armazenamento do Azure (também conhecido como WASB).</span><span class="sxs-lookup"><span data-stu-id="65398-158">Spark is able to read and write to Azure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="65398-159">Portanto, qualquer dado existente armazenado lá pode ser processado usando o Spark, e os resultados podem ser armazenados novamente no WASB.</span><span class="sxs-lookup"><span data-stu-id="65398-159">So any of your existing data stored there can be processed using Spark and the results stored again in WASB.</span></span>

<span data-ttu-id="65398-160">Para salvar arquivos ou modelos no WASB, o caminho deve ser especificado corretamente.</span><span class="sxs-lookup"><span data-stu-id="65398-160">To save models or files in WASB, the path needs to be specified properly.</span></span> <span data-ttu-id="65398-161">O contêiner padrão anexado ao cluster Spark pode ser referenciado usando um caminho que começa com: “wasb:///”.</span><span class="sxs-lookup"><span data-stu-id="65398-161">The default container attached to the Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="65398-162">Outros locais são referenciados por "wasb://".</span><span class="sxs-lookup"><span data-stu-id="65398-162">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="65398-163">Definir caminhos de diretório para locais de armazenamento no WASB</span><span class="sxs-lookup"><span data-stu-id="65398-163">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="65398-164">O exemplo de código a seguir especifica o local dos dados a serem lidos e o caminho do diretório de armazenamento de modelo em que a saída do modelo será salva:</span><span class="sxs-lookup"><span data-stu-id="65398-164">The following code sample specifies the location of the data to be read and the path for the model storage directory to which the model output is saved:</span></span>

    # SET PATHS TO FILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET THE MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT THE FINAL BACKSLASH IN THE PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="65398-165">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-165">**OUTPUT**</span></span>

<span data-ttu-id="65398-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span><span class="sxs-lookup"><span data-stu-id="65398-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="65398-167">Importar bibliotecas</span><span class="sxs-lookup"><span data-stu-id="65398-167">Import libraries</span></span>
<span data-ttu-id="65398-168">Importe as bibliotecas necessárias com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="65398-168">Import necessary libraries with the following code:</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="65398-169">Contexto predefinido do Spark e palavras mágicas do PySpark</span><span class="sxs-lookup"><span data-stu-id="65398-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="65398-170">Os kernels PySpark fornecidos com os notebooks Jupyter têm contextos predefinidos.</span><span class="sxs-lookup"><span data-stu-id="65398-170">The PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="65398-171">Portanto, não é necessário definir explicitamente os contextos Spark ou Hive antes de começar a trabalhar com o aplicativo que você está desenvolvendo.</span><span class="sxs-lookup"><span data-stu-id="65398-171">So you do not need to set the Spark or Hive contexts explicitly before you start working with the application you are developing.</span></span> <span data-ttu-id="65398-172">Esses contextos estão disponíveis para você por padrão.</span><span class="sxs-lookup"><span data-stu-id="65398-172">These contexts are available for you by default.</span></span> <span data-ttu-id="65398-173">Esses contextos são:</span><span class="sxs-lookup"><span data-stu-id="65398-173">These contexts are:</span></span>

* <span data-ttu-id="65398-174">sc - para o Spark</span><span class="sxs-lookup"><span data-stu-id="65398-174">sc - for Spark</span></span> 
* <span data-ttu-id="65398-175">sqlContext - para o Hive</span><span class="sxs-lookup"><span data-stu-id="65398-175">sqlContext - for Hive</span></span>

<span data-ttu-id="65398-176">O kernel PySpark fornece algumas “palavras mágicas” predefinidas, que são comandos especiais que podem ser chamados com %%.</span><span class="sxs-lookup"><span data-stu-id="65398-176">The PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="65398-177">Há dois comandos que são usados nesses exemplos de código.</span><span class="sxs-lookup"><span data-stu-id="65398-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="65398-178">**%%local** Especifica que o código nas linhas posteriores é executado localmente.</span><span class="sxs-lookup"><span data-stu-id="65398-178">**%%local** Specifies that the code in subsequent lines is to be executed locally.</span></span> <span data-ttu-id="65398-179">O código deve ser um código Python válido.</span><span class="sxs-lookup"><span data-stu-id="65398-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="65398-180">**%%sql -o <variable name>** Executa uma consulta do Hive no sqlContext.</span><span class="sxs-lookup"><span data-stu-id="65398-180">**%%sql -o <variable name>** Executes a Hive query against the sqlContext.</span></span> <span data-ttu-id="65398-181">Se o parâmetro -o for transmitido, o resultado da consulta será persistido no contexto %%local do Python como um quadro de dados do Pandas.</span><span class="sxs-lookup"><span data-stu-id="65398-181">If the -o parameter is passed, the result of the query is persisted in the %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="65398-182">Para saber mais sobre os kernels para notebooks Jupyter e as "palavras mágicas" predefinidas que eles fornecem, confira [Kernels disponíveis para notebooks Jupyter com clusters Linux do HDInsight Spark no HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="65398-182">For more information on the kernels for Jupyter notebooks and the predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="65398-183">Ingestão de dados do blob público:</span><span class="sxs-lookup"><span data-stu-id="65398-183">Data ingestion from public blob:</span></span>
<span data-ttu-id="65398-184">A primeira etapa no processo de ciência de dados é ingerir os dados a serem analisados de fontes nas quais eles residem para seu ambiente de modelagem e exploração de dados.</span><span class="sxs-lookup"><span data-stu-id="65398-184">The first step in the data science process is to ingest the data to be analyzed from sources where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="65398-185">Esse ambiente é o Spark neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="65398-185">This environment is Spark in this walkthrough.</span></span> <span data-ttu-id="65398-186">Esta seção contém o código para concluir uma série de tarefas:</span><span class="sxs-lookup"><span data-stu-id="65398-186">This section contains the code to complete a series of tasks:</span></span>

* <span data-ttu-id="65398-187">ingerir a amostra de dados a ser modelada</span><span class="sxs-lookup"><span data-stu-id="65398-187">ingest the data sample to be modeled</span></span>
* <span data-ttu-id="65398-188">ler o conjunto de dados (armazenado como um arquivo .tsv)</span><span class="sxs-lookup"><span data-stu-id="65398-188">read in the input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="65398-189">formatar e limpar os dados</span><span class="sxs-lookup"><span data-stu-id="65398-189">format and clean the data</span></span>
* <span data-ttu-id="65398-190">criar e armazenar objetos em cache (RDDs ou quadros de dados) na memória</span><span class="sxs-lookup"><span data-stu-id="65398-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="65398-191">registrá-lo como uma tabela temporária no contexto do SQL.</span><span class="sxs-lookup"><span data-stu-id="65398-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="65398-192">Aqui está o código para ingestão de dados.</span><span class="sxs-lookup"><span data-stu-id="65398-192">Here is the code for data ingestion.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF THE FILE FROM HEADER
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

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES THE DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="65398-193">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-193">**OUTPUT**</span></span>

<span data-ttu-id="65398-194">Tempo necessário para executar a célula acima: 276,62 segundos</span><span class="sxs-lookup"><span data-stu-id="65398-194">Time taken to execute above cell: 276.62 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="65398-195">Visualização e exploração de dados</span><span class="sxs-lookup"><span data-stu-id="65398-195">Data exploration & visualization</span></span>
<span data-ttu-id="65398-196">Depois que os dados forem incluídos no Spark, a próxima etapa no processo de ciência de dados será obter uma compreensão mais profunda dos dados por meio de exploração e visualização.</span><span class="sxs-lookup"><span data-stu-id="65398-196">Once the data has been brought into Spark, the next step in the data science process is to gain deeper understanding of the data through exploration and visualization.</span></span> <span data-ttu-id="65398-197">Nesta seção, podemos examinar os dados de táxi usando consultas SQL e plotar as variáveis de destino e os recursos em potencial para inspeção visual.</span><span class="sxs-lookup"><span data-stu-id="65398-197">In this section, we examine the taxi data using SQL queries and plot the target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="65398-198">Especificamente, plotamos a frequência das contagens de passageiros em corridas de táxi, a frequência de gorjetas e como as gorjetas variam de acordo com o valor e o tipo de pagamento.</span><span class="sxs-lookup"><span data-stu-id="65398-198">Specifically, we plot the frequency of passenger counts in taxi trips, the frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-the-sample-of-taxi-trips"></a><span data-ttu-id="65398-199">Plotar um histograma de frequências de contagens de passageiros na amostra de corridas de táxi</span><span class="sxs-lookup"><span data-stu-id="65398-199">Plot a histogram of passenger count frequencies in the sample of taxi trips</span></span>
<span data-ttu-id="65398-200">Este código e os trechos de código posteriores usam as palavras mágicas do SQL para consultar a amostra e as palavras mágicas locais para plotar os dados.</span><span class="sxs-lookup"><span data-stu-id="65398-200">This code and subsequent snippets use SQL magic to query the sample and local magic to plot the data.</span></span>

* <span data-ttu-id="65398-201">A **mágica do SQL (`%%sql`)** O kernel HDInsight PySpark dá suporte a consultas do HiveQL fáceis e embutidas no sqlContext.</span><span class="sxs-lookup"><span data-stu-id="65398-201">**SQL magic (`%%sql`)** The HDInsight PySpark kernel supports easy inline HiveQL queries against the sqlContext.</span></span> <span data-ttu-id="65398-202">O argumento (-o VARIABLE_NAME) persiste a saída da consulta SQL como um quadro de dados do Pandas no servidor do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="65398-202">The (-o VARIABLE_NAME) argument persists the output of the SQL query as a Pandas DataFrame on the Jupyter server.</span></span> <span data-ttu-id="65398-203">Isso significa que ele está disponível no modo local.</span><span class="sxs-lookup"><span data-stu-id="65398-203">This means it is available in the local mode.</span></span>
* <span data-ttu-id="65398-204">A **`%%local`** é usada para executar o código localmente no servidor do Jupyter, que é o nó de cabeçalho do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65398-204">The **`%%local` magic** is used to run code locally on the Jupyter server, which is the headnode of the HDInsight cluster.</span></span> <span data-ttu-id="65398-205">Normalmente, você usa a mágica `%%local` após a mágica `%%sql -o` ser usada para executar uma consulta.</span><span class="sxs-lookup"><span data-stu-id="65398-205">Typically, you use `%%local` magic after the `%%sql -o` magic is used to run a query.</span></span> <span data-ttu-id="65398-206">O parâmetro -o persistiria a saída da consulta SQL localmente.</span><span class="sxs-lookup"><span data-stu-id="65398-206">The -o parameter would persist the output of the SQL query locally.</span></span> <span data-ttu-id="65398-207">Em seguida, a mágica `%%local` dispara o próximo conjunto de trechos de código para ser executado localmente em relação à saída de consultas SQL persistida localmente.</span><span class="sxs-lookup"><span data-stu-id="65398-207">Then the `%%local` magic triggers the next set of code snippets to run locally against the output of the SQL queries that has been persisted locally.</span></span> <span data-ttu-id="65398-208">A saída é visualizada automaticamente após a execução do código.</span><span class="sxs-lookup"><span data-stu-id="65398-208">The output is automatically visualized after you run the code.</span></span>

<span data-ttu-id="65398-209">Essa consulta recupera as corridas por contagem de passageiros.</span><span class="sxs-lookup"><span data-stu-id="65398-209">This query retrieves the trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


<span data-ttu-id="65398-210">Esse código cria um quadro de dados local da saída da consulta e plota os dados.</span><span class="sxs-lookup"><span data-stu-id="65398-210">This code creates a local data-frame from the query output and plots the data.</span></span> <span data-ttu-id="65398-211">A palavra mágica `%%local` cria um quadro de dados local, `sqlResults`, que pode ser usado para plotar com matplotlib.</span><span class="sxs-lookup"><span data-stu-id="65398-211">The `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="65398-212">Essas palavras mágicas do PySpark são usadas várias vezes neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="65398-212">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="65398-213">Se a quantidade de dados for grande, você deverá obter uma amostra para criar um quadro de dados que se ajusta na memória local.</span><span class="sxs-lookup"><span data-stu-id="65398-213">If the amount of data is large, you should sample to create a data-frame that can fit in local memory.</span></span>
> 
> 

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES. 
    # CLICK ON THE TYPE OF PLOT TO BE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="65398-214">Este é o código para plotar as corridas por contagens de passageiros</span><span class="sxs-lookup"><span data-stu-id="65398-214">Here is the code to plot the trips by passenger counts</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
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

<span data-ttu-id="65398-215">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-215">**OUTPUT**</span></span>

![Frequência de corridas por contagem de passageiros](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

<span data-ttu-id="65398-217">É possível selecionar entre vários tipos diferentes de visualizações (Tabela, Pizza, Linha, Área ou Barra) usando os botões de menu **Tipo** no notebook.</span><span class="sxs-lookup"><span data-stu-id="65398-217">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using the **Type** menu buttons in the notebook.</span></span> <span data-ttu-id="65398-218">A plotagem de Barras é mostrada aqui.</span><span class="sxs-lookup"><span data-stu-id="65398-218">The Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="65398-219">Plote um histograma de valores de gorjetas e como o valor das gorjetas varia pelas tarifas e contagens de passageiros.</span><span class="sxs-lookup"><span data-stu-id="65398-219">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="65398-220">Use uma consulta SQL para obter amostra de dados.</span><span class="sxs-lookup"><span data-stu-id="65398-220">Use a SQL query to sample data..</span></span>

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


<span data-ttu-id="65398-221">Esta célula de código usa a consulta SQL para criar três plotagens dos dados.</span><span class="sxs-lookup"><span data-stu-id="65398-221">This code cell uses the SQL query to create three plots the data.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="65398-222">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="65398-222">**OUTPUT:**</span></span> 

![Distribuição de valores de gorjetas](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![Valor de gorjeta por contagem de passageiros](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Valor de gorjeta por valor de tarifa](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="65398-226">Engenharia de recursos, transformação e preparação de dados para a modelagem</span><span class="sxs-lookup"><span data-stu-id="65398-226">Feature engineering, transformation, and data preparation for modeling</span></span>
<span data-ttu-id="65398-227">Esta seção descreve e fornece o código para os procedimentos usados para preparar dados para uso na modelagem ML.</span><span class="sxs-lookup"><span data-stu-id="65398-227">This section describes and provides the code for procedures used to prepare data for use in ML modeling.</span></span> <span data-ttu-id="65398-228">Ela mostra como realizar as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="65398-228">It shows how to do the following tasks:</span></span>

* <span data-ttu-id="65398-229">Criar um novo recurso por meio do particionamento de horários em compartimentos de tempo de tráfego</span><span class="sxs-lookup"><span data-stu-id="65398-229">Create a new feature by partitioning hours into traffic time bins</span></span>
* <span data-ttu-id="65398-230">Indexar e fazer a codificação one-hot dos recursos categóricos</span><span class="sxs-lookup"><span data-stu-id="65398-230">Index and on-hot encode categorical features</span></span>
* <span data-ttu-id="65398-231">Criar objetos de ponto rotulado para entrada em funções de ML</span><span class="sxs-lookup"><span data-stu-id="65398-231">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="65398-232">Criar uma subamostragem aleatória dos dados e dividi-la em conjuntos de treinamento e teste</span><span class="sxs-lookup"><span data-stu-id="65398-232">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
* <span data-ttu-id="65398-233">Dimensionamento de recursos</span><span class="sxs-lookup"><span data-stu-id="65398-233">Feature scaling</span></span>
* <span data-ttu-id="65398-234">Armazenar objetos em cache na memória</span><span class="sxs-lookup"><span data-stu-id="65398-234">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a><span data-ttu-id="65398-235">Criar um novo recurso por meio do particionamento de horários de tráfego em compartimentos</span><span class="sxs-lookup"><span data-stu-id="65398-235">Create a new feature by partitioning traffic times into bins</span></span>
<span data-ttu-id="65398-236">Este código mostra como criar um novo recurso particionando horários de tráfego em compartimentos e como armazenar em cache o quadro de dados resultante na memória.</span><span class="sxs-lookup"><span data-stu-id="65398-236">This code shows how to create a new feature by partitioning traffic times into bins and then how to cache the resulting data frame in memory.</span></span> <span data-ttu-id="65398-237">O armazenamento em cache proporciona um tempo de execução melhor, em que os RDDs (Conjuntos de Dados Resilientes Distribuídos) e quadros de dados são usados repetidamente.</span><span class="sxs-lookup"><span data-stu-id="65398-237">Caching leads to improved execution time where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly.</span></span> <span data-ttu-id="65398-238">Portanto, armazenamos em cache RDDs e quadros de dados em vários estágios no passo a passo.</span><span class="sxs-lookup"><span data-stu-id="65398-238">So, we cache RDDs and data-frames at several stages in this walkthrough.</span></span>

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
    # THE .COUNT() GOES THROUGH THE ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES THE COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

<span data-ttu-id="65398-239">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-239">**OUTPUT**</span></span>

<span data-ttu-id="65398-240">126050</span><span class="sxs-lookup"><span data-stu-id="65398-240">126050</span></span>

### <a name="index-and-one-hot-encode-categorical-features"></a><span data-ttu-id="65398-241">Indexar e fazer a codificação one-hot dos recursos categóricos</span><span class="sxs-lookup"><span data-stu-id="65398-241">Index and one-hot encode categorical features</span></span>
<span data-ttu-id="65398-242">Esta seção mostra como indexar ou codificar recursos categóricos para entrada nas funções de modelagem.</span><span class="sxs-lookup"><span data-stu-id="65398-242">This section shows how to index or encode categorical features for input into the modeling functions.</span></span> <span data-ttu-id="65398-243">As funções de modelagem e previsão de MLlib exigem que recursos que tenham dados de entrada categóricos sejam indexados ou codificados antes do uso.</span><span class="sxs-lookup"><span data-stu-id="65398-243">The modeling and predict functions of MLlib require that features with categorical input data be indexed or encoded prior to use.</span></span> 

<span data-ttu-id="65398-244">Dependendo do modelo, você precisa indexá-lo ou codificá-lo de maneiras diferentes.</span><span class="sxs-lookup"><span data-stu-id="65398-244">Depending on the model, you need to index or encode them in different ways.</span></span> <span data-ttu-id="65398-245">Por exemplo, modelos de regressão linear e logística exigem codificação one-hot, em que, por exemplo, um recurso com três categorias pode ser expandido em três colunas de recursos, em que cada uma contém 0 ou 1, dependendo da categoria de uma observação.</span><span class="sxs-lookup"><span data-stu-id="65398-245">For example, Logistic and Linear Regression models require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on the category of an observation.</span></span> <span data-ttu-id="65398-246">A MLlib fornece a função [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) para executar a codificação one-hot.</span><span class="sxs-lookup"><span data-stu-id="65398-246">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function to do one-hot encoding.</span></span> <span data-ttu-id="65398-247">Esse codificador mapeia uma coluna de índices de rótulo para uma coluna de vetores binários com, no máximo, um valor único.</span><span class="sxs-lookup"><span data-stu-id="65398-247">This encoder maps a column of label indices to a column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="65398-248">Essa codificação permite que os algoritmos que esperam recursos valiosos numéricos, por exemplo a regressão logística, sejam aplicados em recursos categóricos.</span><span class="sxs-lookup"><span data-stu-id="65398-248">This encoding allows algorithms that expect numerical valued features, such as logistic regression, to be applied to categorical features.</span></span>

<span data-ttu-id="65398-249">Aqui está o código para indexar e codificar recursos categóricos:</span><span class="sxs-lookup"><span data-stu-id="65398-249">Here is the code to index and encode categorical features:</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is the cleaned one from above
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="65398-250">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-250">**OUTPUT**</span></span>

<span data-ttu-id="65398-251">Tempo necessário para executar a célula acima: 3,14 segundos</span><span class="sxs-lookup"><span data-stu-id="65398-251">Time taken to execute above cell: 3.14 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="65398-252">Criar objetos de ponto rotulado para entrada em funções de ML</span><span class="sxs-lookup"><span data-stu-id="65398-252">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="65398-253">Esta seção contém códigos que mostram como indexar dados categóricos de texto como tipos de dados de ponto rotulado e como codificá-los.</span><span class="sxs-lookup"><span data-stu-id="65398-253">This section contains code that shows how to index categorical text data as a labeled point data type and how to encode it.</span></span> <span data-ttu-id="65398-254">Essa ação os prepara para serem usados em treinamentos e testes de regressão logística de MLlib e outros modelos de classificação.</span><span class="sxs-lookup"><span data-stu-id="65398-254">This prepares it to be used to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="65398-255">Objetos de ponto rotulados são RDDs (Conjuntos de Dados Resilientes Distribuídos) formatados de uma maneira que é necessária como dados de entrada pela maioria dos algoritmos de ML no MLlib.</span><span class="sxs-lookup"><span data-stu-id="65398-255">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="65398-256">Um [ponto rotulado](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) é um vetor local, denso ou esparso, associado a um rótulo/resposta.</span><span class="sxs-lookup"><span data-stu-id="65398-256">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="65398-257">Este é o código para indexar e codificar recursos de texto para a classificação binária.</span><span class="sxs-lookup"><span data-stu-id="65398-257">Here is the code to index and encode text features for binary classification.</span></span>

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


<span data-ttu-id="65398-258">Este é o código para codificar e indexar recursos de texto categórico para a análise de regressão linear.</span><span class="sxs-lookup"><span data-stu-id="65398-258">Here is the code to encode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-the-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="65398-259">Criar uma subamostragem aleatória dos dados e dividi-la em conjuntos de treinamento e teste</span><span class="sxs-lookup"><span data-stu-id="65398-259">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
<span data-ttu-id="65398-260">Esse código cria uma amostragem aleatória dos dados (o valor de 25% é usado aqui).</span><span class="sxs-lookup"><span data-stu-id="65398-260">This code creates a random sampling of the data (25% is used here).</span></span> <span data-ttu-id="65398-261">Embora não seja necessário para este exemplo, devido ao tamanho do conjunto de dados, demonstramos como é possível obter amostras de dados.</span><span class="sxs-lookup"><span data-stu-id="65398-261">Although it is not required for this example due to the size of the dataset, we demonstrate how you can sample the data here.</span></span> <span data-ttu-id="65398-262">Em seguida, você saberá como usá-lo para resolver seus próprios problemas, se necessário.</span><span class="sxs-lookup"><span data-stu-id="65398-262">Then you know how to use it for your own problem if needed.</span></span> <span data-ttu-id="65398-263">Quando as amostras são grandes, isso pode economizar um tempo significativo durante o treinamento de modelos.</span><span class="sxs-lookup"><span data-stu-id="65398-263">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="65398-264">Em seguida, dividimos o exemplo em uma parte de treinamento (75% aqui) e uma parte de teste (25% aqui) para usar na classificação e na modelagem de regressão.</span><span class="sxs-lookup"><span data-stu-id="65398-264">Next we split the sample into a training part (75% here) and a testing part (25% here) to use in classification and regression modeling.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="65398-265">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-265">**OUTPUT**</span></span>

<span data-ttu-id="65398-266">Tempo necessário para executar a célula acima: 0,31 segundo</span><span class="sxs-lookup"><span data-stu-id="65398-266">Time taken to execute above cell: 0.31 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="65398-267">Dimensionamento de recursos</span><span class="sxs-lookup"><span data-stu-id="65398-267">Feature scaling</span></span>
<span data-ttu-id="65398-268">O dimensionamento de recursos, também conhecido como normalização de dados, faz com que recursos com valores amplamente distribuídos não tenham peso excessivo na função objetiva.</span><span class="sxs-lookup"><span data-stu-id="65398-268">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in the objective function.</span></span> <span data-ttu-id="65398-269">O código para o dimensionamento de recursos usa [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) para dimensionar os recursos para variância de unidade.</span><span class="sxs-lookup"><span data-stu-id="65398-269">The code for feature scaling uses the [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) to scale the features to unit variance.</span></span> <span data-ttu-id="65398-270">Ele é fornecido pela MLlib para uso na regressão linear com SGD (Stochastic Gradient Descent).</span><span class="sxs-lookup"><span data-stu-id="65398-270">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD).</span></span> <span data-ttu-id="65398-271">O SGD é um algoritmo popular de treinamento de uma grande variedade de outros modelos de aprendizado de máquina, como regressões regularizadas ou SVM (máquinas de vetor de suporte).</span><span class="sxs-lookup"><span data-stu-id="65398-271">SGD is a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>   

> [!TIP]
> <span data-ttu-id="65398-272">Observamos que o algoritmo LinearRegressionWithSGD é sensível ao dimensionamento de recursos.</span><span class="sxs-lookup"><span data-stu-id="65398-272">We have found the LinearRegressionWithSGD algorithm to be sensitive to feature scaling.</span></span>   
> 
> 

<span data-ttu-id="65398-273">Veja o código para escalar as variáveis para uso com o algoritmo SGD linear regularizado.</span><span class="sxs-lookup"><span data-stu-id="65398-273">Here is the code to scale variables for use with the regularized linear SGD algorithm.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="65398-274">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-274">**OUTPUT**</span></span>

<span data-ttu-id="65398-275">Tempo necessário para executar a célula acima: 11,67 segundos</span><span class="sxs-lookup"><span data-stu-id="65398-275">Time taken to execute above cell: 11.67 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="65398-276">Armazenar objetos em cache na memória</span><span class="sxs-lookup"><span data-stu-id="65398-276">Cache objects in memory</span></span>
<span data-ttu-id="65398-277">O tempo necessário para treinamento e teste dos algoritmos de ML pode ser reduzido armazenando-se em cache os objetos de quadro de dados de entrada usados para classificação, regressão e recursos dimensionados.</span><span class="sxs-lookup"><span data-stu-id="65398-277">The time taken for training and testing of ML algorithms can be reduced by caching the input data frame objects used for classification, regression and, scaled features.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="65398-278">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-278">**OUTPUT**</span></span> 

<span data-ttu-id="65398-279">Tempo necessário para executar a célula acima: 0,13 segundo</span><span class="sxs-lookup"><span data-stu-id="65398-279">Time taken to execute above cell: 0.13 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="65398-280">Prever se uma gorjeta é paga ou não com modelos de classificação binária</span><span class="sxs-lookup"><span data-stu-id="65398-280">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="65398-281">Esta seção mostra como usar três modelos para a tarefa de classificação binária de prever se uma gorjeta é paga ou não por uma corrida de táxi.</span><span class="sxs-lookup"><span data-stu-id="65398-281">This section shows how use three models for the binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="65398-282">Os modelos apresentados são:</span><span class="sxs-lookup"><span data-stu-id="65398-282">The models presented are:</span></span>

* <span data-ttu-id="65398-283">Regressão logística</span><span class="sxs-lookup"><span data-stu-id="65398-283">Logistic regression</span></span> 
* <span data-ttu-id="65398-284">Floresta aleatória</span><span class="sxs-lookup"><span data-stu-id="65398-284">Random forest</span></span>
* <span data-ttu-id="65398-285">Árvores de Ampliação de Gradiente</span><span class="sxs-lookup"><span data-stu-id="65398-285">Gradient Boosting Trees</span></span>

<span data-ttu-id="65398-286">Cada seção de código de compilação de modelo é dividida em etapas:</span><span class="sxs-lookup"><span data-stu-id="65398-286">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="65398-287">**Modelar os dados de treinamento** com um conjunto de parâmetros</span><span class="sxs-lookup"><span data-stu-id="65398-287">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="65398-288">**Modelar a avaliação** em um conjunto de dados de teste com métricas</span><span class="sxs-lookup"><span data-stu-id="65398-288">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="65398-289">**Salvar modelo** no blob para consumo futuro</span><span class="sxs-lookup"><span data-stu-id="65398-289">**Saving model** in blob for future consumption</span></span>

<span data-ttu-id="65398-290">Mostraremos como fazer a CV (validação cruzada) com a limpeza de parâmetro de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="65398-290">We show how to do cross-validation (CV) with parameter sweeping in two ways:</span></span>

1. <span data-ttu-id="65398-291">Usando o código personalizado **genérico** que pode ser aplicado a qualquer algoritmo na MLlib e a quaisquer conjuntos de parâmetros em um algoritmo.</span><span class="sxs-lookup"><span data-stu-id="65398-291">Using **generic** custom code which can be applied to any algorithm in MLlib and to any parameter sets in an algorithm.</span></span> 
2. <span data-ttu-id="65398-292">Usando a **função de pipeline CrossValidator do pySpark**.</span><span class="sxs-lookup"><span data-stu-id="65398-292">Using the **pySpark CrossValidator pipeline function**.</span></span> <span data-ttu-id="65398-293">Observe que o CrossValidator tem algumas limitações para o Spark 1.5.0:</span><span class="sxs-lookup"><span data-stu-id="65398-293">Note that CrossValidator has a few limitations for Spark 1.5.0:</span></span> 
   
   * <span data-ttu-id="65398-294">Os modelos de pipeline não podem ser salvos/persistidos para consumo futuro.</span><span class="sxs-lookup"><span data-stu-id="65398-294">Pipeline models cannot be saved/persisted for future consumption.</span></span>
   * <span data-ttu-id="65398-295">Não pode ser usado para todos os parâmetros em um modelo.</span><span class="sxs-lookup"><span data-stu-id="65398-295">Cannot be used for every parameter in a model.</span></span>
   * <span data-ttu-id="65398-296">Não pode ser usado para todos os algoritmos MLlib.</span><span class="sxs-lookup"><span data-stu-id="65398-296">Cannot be used for every MLlib algorithm.</span></span>

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-the-logistic-regression-algorithm-for-binary-classification"></a><span data-ttu-id="65398-297">Limpeza de hiperparâmetro e validação cruzada genérica usadas com o algoritmo de regressão logística para classificação binária</span><span class="sxs-lookup"><span data-stu-id="65398-297">Generic cross validation and hyperparameter sweeping used with the logistic regression algorithm for binary classification</span></span>
<span data-ttu-id="65398-298">O código nesta seção mostra como treinar, avaliar e salvar um modelo de regressão logística com [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) que prevê se uma gorjeta será paga ou não por uma corrida no conjunto de dados de corridas e tarifas de táxi de Nova York.</span><span class="sxs-lookup"><span data-stu-id="65398-298">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="65398-299">O modelo é treinado usando a CV (validação cruzada) e a limpeza de hiperparâmetro implementada com o código personalizado que pode ser aplicado a qualquer um dos algoritmos de aprendizado na MLlib.</span><span class="sxs-lookup"><span data-stu-id="65398-299">The model is trained using cross validation (CV) and hyperparameter sweeping implemented with custom code that can be applied to any of the learning algorithms in MLlib.</span></span>   

> [!NOTE]
> <span data-ttu-id="65398-300">A execução desse código personalizado de CV pode levar vários minutos.</span><span class="sxs-lookup"><span data-stu-id="65398-300">The execution of this custom CV code can take several minutes.</span></span>
> 
> 

<span data-ttu-id="65398-301">**Treinar o modelo de regressão logística usando a CV e a limpeza de hiperparâmetro**</span><span class="sxs-lookup"><span data-stu-id="65398-301">**Train the logistic regression model using CV and hyperparameter sweeping**</span></span>

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

    # SET NUM FOLDS AND NUM PARAMETER SETS TO SWEEP ON
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


    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="65398-302">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-302">**OUTPUT**</span></span>

<span data-ttu-id="65398-303">Coeficientes: [0,0082065285375, -0,0223675576104, -0,0183812028036, -3,48124578069e-05, -0,00247646947233, -0,00165897881503, 0,0675394837328, -0,111823113101, -0,324609912762, -0,204549780032, -1,36499216354, 0,591088507921, -0,664263411392, -1,00439726852, 3,46567827545, -3,51025855172, -0,0471341112232, -0,043521833294, 0,000243375810385, 0,054518719222]</span><span class="sxs-lookup"><span data-stu-id="65398-303">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="65398-304">Interceptação: -0,0111216486893</span><span class="sxs-lookup"><span data-stu-id="65398-304">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="65398-305">Tempo necessário para executar a célula acima: 14,43 segundos</span><span class="sxs-lookup"><span data-stu-id="65398-305">Time taken to execute above cell: 14.43 seconds</span></span>

<span data-ttu-id="65398-306">**Avaliar o modelo de classificação binária com métricas padrão**</span><span class="sxs-lookup"><span data-stu-id="65398-306">**Evaluate the binary classification model with standard metrics**</span></span>

<span data-ttu-id="65398-307">O código nesta seção mostra como avaliar um modelo de regressão logística em um conjunto dados de teste, incluindo uma plotagem da curva ROC.</span><span class="sxs-lookup"><span data-stu-id="65398-307">The code in this section shows how to evaluate a logistic regression model against a test data-set, including a plot of the ROC curve.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="65398-308">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-308">**OUTPUT**</span></span>

<span data-ttu-id="65398-309">Área sob PR = 0,985336538462</span><span class="sxs-lookup"><span data-stu-id="65398-309">Area under PR = 0.985336538462</span></span>

<span data-ttu-id="65398-310">Área sob ROC = 0,983383274312</span><span class="sxs-lookup"><span data-stu-id="65398-310">Area under ROC = 0.983383274312</span></span>

<span data-ttu-id="65398-311">Estatísticas de resumo</span><span class="sxs-lookup"><span data-stu-id="65398-311">Summary Stats</span></span>

<span data-ttu-id="65398-312">Precisão = 0,984174341679</span><span class="sxs-lookup"><span data-stu-id="65398-312">Precision = 0.984174341679</span></span>

<span data-ttu-id="65398-313">Cancelamento = 0,984174341679</span><span class="sxs-lookup"><span data-stu-id="65398-313">Recall = 0.984174341679</span></span>

<span data-ttu-id="65398-314">Pontuação F1 = 0,984174341679</span><span class="sxs-lookup"><span data-stu-id="65398-314">F1 Score = 0.984174341679</span></span>

<span data-ttu-id="65398-315">Tempo necessário para executar a célula acima: 2,67 segundos</span><span class="sxs-lookup"><span data-stu-id="65398-315">Time taken to execute above cell: 2.67 seconds</span></span>

<span data-ttu-id="65398-316">**Plote a curva ROC.**</span><span class="sxs-lookup"><span data-stu-id="65398-316">**Plot the ROC curve.**</span></span>

<span data-ttu-id="65398-317">O *predictionAndLabelsDF* é registrado como uma tabela, *tmp_results*, na célula anterior.</span><span class="sxs-lookup"><span data-stu-id="65398-317">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span></span> <span data-ttu-id="65398-318">A tabela *tmp_results* pode ser usada para fazer consultas e resultados de saída para o quadro de dados sqlResults para plotagem.</span><span class="sxs-lookup"><span data-stu-id="65398-318">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span></span> <span data-ttu-id="65398-319">Veja o código.</span><span class="sxs-lookup"><span data-stu-id="65398-319">Here is the code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="65398-320">Este é o código para fazer previsões e plotar a curva ROC.</span><span class="sxs-lookup"><span data-stu-id="65398-320">Here is the code to make predictions and plot the ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES                              
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


<span data-ttu-id="65398-321">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-321">**OUTPUT**</span></span>

![Curva ROC de regressão logística de abordagem genérica](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

<span data-ttu-id="65398-323">**Persistir o modelo em um blob para consumo futuro**</span><span class="sxs-lookup"><span data-stu-id="65398-323">**Persist model in a blob for future consumption**</span></span>

<span data-ttu-id="65398-324">O código nesta seção mostra como salvar o modelo de regressão logística para consumo.</span><span class="sxs-lookup"><span data-stu-id="65398-324">The code in this section shows how to save the logistic regression model for consumption.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";


<span data-ttu-id="65398-325">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-325">**OUTPUT**</span></span>

<span data-ttu-id="65398-326">Tempo necessário para executar a célula acima: 34,57 segundos</span><span class="sxs-lookup"><span data-stu-id="65398-326">Time taken to execute above cell: 34.57 seconds</span></span>

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a><span data-ttu-id="65398-327">Usar a função de pipeline CrossValidator da MLlib com o modelo de regressão logística (Regressão elástica)</span><span class="sxs-lookup"><span data-stu-id="65398-327">Use MLlib's CrossValidator pipeline function with logistic regression (Elastic regression) model</span></span>
<span data-ttu-id="65398-328">O código nesta seção mostra como treinar, avaliar e salvar um modelo de regressão logística com [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) que prevê se uma gorjeta será paga ou não por uma corrida no conjunto de dados de corridas e tarifas de táxi de Nova York.</span><span class="sxs-lookup"><span data-stu-id="65398-328">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="65398-329">O modelo é treinado usando a CV (validação cruzada) e a limpeza de hiperparâmetro implementada com a função de pipeline CrossValidator da MLlib para CV com limpeza de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="65398-329">The model is trained using cross validation (CV) and hyperparameter sweeping implemented with the MLlib CrossValidator pipeline function for CV with parameter sweep.</span></span>   

> [!NOTE]
> <span data-ttu-id="65398-330">A execução desse código de CV da MLlib pode levar vários minutos.</span><span class="sxs-lookup"><span data-stu-id="65398-330">The execution of this MLlib CV code can take several minutes.</span></span>
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

    # CONVERT TO DATA-FRAME: THIS DOES NOT RUN ON RDDs
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="65398-331">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-331">**OUTPUT**</span></span>

<span data-ttu-id="65398-332">Tempo necessário para executar a célula acima: 107,98 segundos</span><span class="sxs-lookup"><span data-stu-id="65398-332">Time taken to execute above cell: 107.98 seconds</span></span>

<span data-ttu-id="65398-333">**Plote a curva ROC.**</span><span class="sxs-lookup"><span data-stu-id="65398-333">**Plot the ROC curve.**</span></span>

<span data-ttu-id="65398-334">O *predictionAndLabelsDF* é registrado como uma tabela, *tmp_results*, na célula anterior.</span><span class="sxs-lookup"><span data-stu-id="65398-334">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span></span> <span data-ttu-id="65398-335">A tabela *tmp_results* pode ser usada para fazer consultas e resultados de saída para o quadro de dados sqlResults para plotagem.</span><span class="sxs-lookup"><span data-stu-id="65398-335">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span></span> <span data-ttu-id="65398-336">Veja o código.</span><span class="sxs-lookup"><span data-stu-id="65398-336">Here is the code.</span></span>

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

<span data-ttu-id="65398-337">Este é o código para plotar a curva ROC.</span><span class="sxs-lookup"><span data-stu-id="65398-337">Here is the code to plot the ROC curve.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES 
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


<span data-ttu-id="65398-338">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-338">**OUTPUT**</span></span>

![Curva ROC de regressão logística usando CrossValidator da MLlib](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="65398-340">Classificação de floresta aleatória</span><span class="sxs-lookup"><span data-stu-id="65398-340">Random forest classification</span></span>
<span data-ttu-id="65398-341">O código nesta seção mostra como treinar, avaliar e salvar uma regressão de floresta aleatória que prevê se uma gorjeta é paga ou não por uma corrida no conjunto de dados de corridas e tarifas de táxi de Nova York.</span><span class="sxs-lookup"><span data-stu-id="65398-341">The code in this section shows how to train, evaluate, and save a random forest regression that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

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
    ## UN-COMMENT IF YOU WANT TO PRING TREES
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="65398-342">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-342">**OUTPUT**</span></span>

<span data-ttu-id="65398-343">Área sob ROC = 0,985336538462</span><span class="sxs-lookup"><span data-stu-id="65398-343">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="65398-344">Tempo necessário para executar a célula acima: 26,72 segundos</span><span class="sxs-lookup"><span data-stu-id="65398-344">Time taken to execute above cell: 26.72 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="65398-345">Classificação de árvores de ampliação de gradiente</span><span class="sxs-lookup"><span data-stu-id="65398-345">Gradient boosting trees classification</span></span>
<span data-ttu-id="65398-346">O código nesta seção mostra como treinar, avaliar e salvar um modelo de árvores de ampliação de gradiente que prevê se uma gorjeta é paga ou não por uma corrida no conjunto de dados de corridas e tarifas de táxi de Nova York.</span><span class="sxs-lookup"><span data-stu-id="65398-346">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT TO PRINT TREE DETAILS
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="65398-347">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-347">**OUTPUT**</span></span>

<span data-ttu-id="65398-348">Área sob ROC = 0,985336538462</span><span class="sxs-lookup"><span data-stu-id="65398-348">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="65398-349">Tempo necessário para executar a célula acima: 28,13 segundos</span><span class="sxs-lookup"><span data-stu-id="65398-349">Time taken to execute above cell: 28.13 seconds</span></span>

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a><span data-ttu-id="65398-350">Prever valores de gorjetas com modelos de regressão (não usando CV)</span><span class="sxs-lookup"><span data-stu-id="65398-350">Predict tip amount with regression models (not using CV)</span></span>
<span data-ttu-id="65398-351">Esta seção mostra como usar três modelos para a tarefa de regressão de prever o valor da gorjeta paga por uma corrida de táxi com base em outros recursos de gorjeta.</span><span class="sxs-lookup"><span data-stu-id="65398-351">This section shows how use three models for the regression task: predict the tip amount paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="65398-352">Os modelos apresentados são:</span><span class="sxs-lookup"><span data-stu-id="65398-352">The models presented are:</span></span>

* <span data-ttu-id="65398-353">Regressão linear regularizada</span><span class="sxs-lookup"><span data-stu-id="65398-353">Regularized linear regression</span></span>
* <span data-ttu-id="65398-354">Floresta aleatória</span><span class="sxs-lookup"><span data-stu-id="65398-354">Random forest</span></span>
* <span data-ttu-id="65398-355">Árvores de Ampliação de Gradiente</span><span class="sxs-lookup"><span data-stu-id="65398-355">Gradient Boosting Trees</span></span>

<span data-ttu-id="65398-356">Esses modelos foram descritos na introdução.</span><span class="sxs-lookup"><span data-stu-id="65398-356">These models were described in the introduction.</span></span> <span data-ttu-id="65398-357">Cada seção de código de compilação de modelo é dividida em etapas:</span><span class="sxs-lookup"><span data-stu-id="65398-357">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="65398-358">**Modelar os dados de treinamento** com um conjunto de parâmetros</span><span class="sxs-lookup"><span data-stu-id="65398-358">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="65398-359">**Modelar a avaliação** em um conjunto de dados de teste com métricas</span><span class="sxs-lookup"><span data-stu-id="65398-359">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="65398-360">**Salvar modelo** no blob para consumo futuro</span><span class="sxs-lookup"><span data-stu-id="65398-360">**Saving model** in blob for future consumption</span></span>   

> <span data-ttu-id="65398-361">OBSERVAÇÃO DO AZURE: a validação cruzada não é usada com os três modelos de regressão nesta seção, já que isso foi mostrado em detalhes para os modelos de regressão logística.</span><span class="sxs-lookup"><span data-stu-id="65398-361">AZURE NOTE: Cross-validation is not used with the three regression models in this section, since this was shown in detail for the logistic regression models.</span></span> <span data-ttu-id="65398-362">Um exemplo que mostra como usar a CV com a Rede Elástica para a regressão linear é fornecido no Apêndice desse tópico.</span><span class="sxs-lookup"><span data-stu-id="65398-362">An example showing how to use CV with Elastic Net for linear regression is provided in the Appendix of this topic.</span></span>
> 
> <span data-ttu-id="65398-363">OBSERVAÇÃO DO AZURE: em nossa experiência, pode haver problemas com convergência de modelos LinearRegressionWithSGD, e os parâmetros precisam ser alterados/otimizados cuidadosamente para a obtenção de um modelo válido.</span><span class="sxs-lookup"><span data-stu-id="65398-363">AZURE NOTE: In our experience, there can be issues with convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="65398-364">O dimensionamento de variáveis ajuda significativamente com a convergência.</span><span class="sxs-lookup"><span data-stu-id="65398-364">Scaling of variables significantly helps with convergence.</span></span> <span data-ttu-id="65398-365">A regressão da rede elástica, mostrada no Apêndice deste tópico, também pode ser usada em vez de LinearRegressionWithSGD.</span><span class="sxs-lookup"><span data-stu-id="65398-365">Elastic net regression, shown in the Appendix to this topic, can also be used instead of LinearRegressionWithSGD.</span></span>
> 
> 

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="65398-366">Regressão linear com SGD</span><span class="sxs-lookup"><span data-stu-id="65398-366">Linear regression with SGD</span></span>
<span data-ttu-id="65398-367">O código nesta seção mostra como usar recursos dimensionados para treinar uma regressão linear que usa SGD (Stochastic Gradient Descent) para otimização e como pontuar, avaliar e salvar o modelo no WASB (Armazenamento de Blobs do Azure).</span><span class="sxs-lookup"><span data-stu-id="65398-367">The code in this section shows how to use scaled features to train a linear regression that uses stochastic gradient descent (SGD) for optimization, and how to score, evaluate, and save the model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="65398-368">Em nossa experiência, pode haver problemas com a convergência de modelos LinearRegressionWithSGD, e os parâmetros precisam ser alterados/otimizados cuidadosamente para a obtenção de um modelo válido.</span><span class="sxs-lookup"><span data-stu-id="65398-368">In our experience, there can be issues with the convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="65398-369">O dimensionamento de variáveis ajuda significativamente com a convergência.</span><span class="sxs-lookup"><span data-stu-id="65398-369">Scaling of variables significantly helps with convergence.</span></span>
> 
> 

    # LINEAR REGRESSION WITH SGD 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES TO TRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="65398-370">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-370">**OUTPUT**</span></span>

<span data-ttu-id="65398-371">Coeficientes: [0,0141707753435, -0,0252930927087, -0,0231442517137, 0,247070902996, 0,312544147152, 0,360296120645, 0,0122079566092, -0,00456498588241, -0,0898228505177, 0,0714046248793, 0,102171263868, 0,100022455632, -0,00289545676449, -0,00791124681938, 0,54396316518, -0,536293513569, 0,0119076553369, -0,0173039244582, 0,0119632796147, 0,00146764882502]</span><span class="sxs-lookup"><span data-stu-id="65398-371">Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span></span>

<span data-ttu-id="65398-372">Interceptação: 0,854507624459</span><span class="sxs-lookup"><span data-stu-id="65398-372">Intercept: 0.854507624459</span></span>

<span data-ttu-id="65398-373">RMSE = 1,23485131376</span><span class="sxs-lookup"><span data-stu-id="65398-373">RMSE = 1.23485131376</span></span>

<span data-ttu-id="65398-374">R-sqr = 0,597963951127</span><span class="sxs-lookup"><span data-stu-id="65398-374">R-sqr = 0.597963951127</span></span>

<span data-ttu-id="65398-375">Tempo necessário para executar a célula acima: 38,62 segundos</span><span class="sxs-lookup"><span data-stu-id="65398-375">Time taken to execute above cell: 38.62 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="65398-376">Regressão de Floresta Aleatória</span><span class="sxs-lookup"><span data-stu-id="65398-376">Random Forest regression</span></span>
<span data-ttu-id="65398-377">O código nesta seção mostra como treinar, avaliar e salvar um modelo de floresta aleatória que prevê o valor da gorjeta para os dados de corridas de táxi de Nova York.</span><span class="sxs-lookup"><span data-stu-id="65398-377">The code in this section shows how to train, evaluate, and save a random forest model that predicts tip amount for the NYC taxi trip data.</span></span>   

> [!NOTE]
> <span data-ttu-id="65398-378">A validação cruzada com a limpeza de parâmetro usando código personalizado é fornecida no apêndice.</span><span class="sxs-lookup"><span data-stu-id="65398-378">Cross-validation with parameter sweeping using custom code is provided in the appendix.</span></span>
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
    # UN-COMMENT IF YOU WANT TO PRING TREES
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="65398-379">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-379">**OUTPUT**</span></span>

<span data-ttu-id="65398-380">RMSE = 0,931981967875</span><span class="sxs-lookup"><span data-stu-id="65398-380">RMSE = 0.931981967875</span></span>

<span data-ttu-id="65398-381">R-sqr = 0,733445485802</span><span class="sxs-lookup"><span data-stu-id="65398-381">R-sqr = 0.733445485802</span></span>

<span data-ttu-id="65398-382">Tempo necessário para executar a célula acima: 25,98 segundos</span><span class="sxs-lookup"><span data-stu-id="65398-382">Time taken to execute above cell: 25.98 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="65398-383">Regressão de árvores de ampliação de gradiente</span><span class="sxs-lookup"><span data-stu-id="65398-383">Gradient boosting trees regression</span></span>
<span data-ttu-id="65398-384">O código nesta seção mostra como treinar, avaliar e salvar um modelo de árvores de ampliação de gradiente que prevê o valor da gorjeta para os dados de corridas de táxi de Nova York.</span><span class="sxs-lookup"><span data-stu-id="65398-384">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts tip amount for the NYC taxi trip data.</span></span>

<span data-ttu-id="65398-385">* * Treinar e avaliar * *</span><span class="sxs-lookup"><span data-stu-id="65398-385">**Train and evaluate **</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="65398-386">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-386">**OUTPUT**</span></span>

<span data-ttu-id="65398-387">RMSE = 0,928172197114</span><span class="sxs-lookup"><span data-stu-id="65398-387">RMSE = 0.928172197114</span></span>

<span data-ttu-id="65398-388">R-sqr = 0,732680354389</span><span class="sxs-lookup"><span data-stu-id="65398-388">R-sqr = 0.732680354389</span></span>

<span data-ttu-id="65398-389">Tempo necessário para executar a célula acima: 20,9 segundos</span><span class="sxs-lookup"><span data-stu-id="65398-389">Time taken to execute above cell: 20.9 seconds</span></span>

<span data-ttu-id="65398-390">**Plotar**</span><span class="sxs-lookup"><span data-stu-id="65398-390">**Plot**</span></span>

<span data-ttu-id="65398-391">*tmp_results* é registrado como uma tabela do Hive na célula anterior.</span><span class="sxs-lookup"><span data-stu-id="65398-391">*tmp_results* is registered as a Hive table in the previous cell.</span></span> <span data-ttu-id="65398-392">Os resultados da tabela são gerados no quadro de dados *sqlResults* para plotagem.</span><span class="sxs-lookup"><span data-stu-id="65398-392">Results from the table are output into the *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="65398-393">Veja o código</span><span class="sxs-lookup"><span data-stu-id="65398-393">Here is the code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="65398-394">Este é o código para plotar os dados usando o servidor do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="65398-394">Here is the code to plot the data using the Jupyter server.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
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

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a><span data-ttu-id="65398-396">Apêndice: Tarefas de regressão adicionais usando a validação cruzada com limpezas de parâmetro</span><span class="sxs-lookup"><span data-stu-id="65398-396">Appendix: Additional regression tasks using cross validation with parameter sweeps</span></span>
<span data-ttu-id="65398-397">Este apêndice contém o código que mostra como fazer a CV usando rede elástica para regressão linear e como fazer a CV com a limpeza de parâmetro usando o código personalizado para a regressão de floresta aleatória.</span><span class="sxs-lookup"><span data-stu-id="65398-397">This appendix contains code showing how to do CV using Elastic net for linear regression and how to do CV with parameter sweep using custom code for random forest regression.</span></span>

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a><span data-ttu-id="65398-398">Validação cruzada usando a rede elástica para a regressão linear</span><span class="sxs-lookup"><span data-stu-id="65398-398">Cross validation using Elastic net for linear regression</span></span>
<span data-ttu-id="65398-399">O código nesta seção mostra como fazer a validação cruzada usando a rede elástica para a regressão linear e como avaliar o modelo em relação aos dados de teste.</span><span class="sxs-lookup"><span data-stu-id="65398-399">The code in this section shows how to do cross validation using Elastic net for linear regression and how to evaluate the model against test data.</span></span>

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
    # SIMPLY THE MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT TO DATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses the best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT TO DF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="65398-400">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-400">**OUTPUT**</span></span>

<span data-ttu-id="65398-401">Tempo necessário para executar a célula acima: 161,21 segundos</span><span class="sxs-lookup"><span data-stu-id="65398-401">Time taken to execute above cell: 161.21  seconds</span></span>

<span data-ttu-id="65398-402">**Avaliar com a métrica R-SQR**</span><span class="sxs-lookup"><span data-stu-id="65398-402">**Evaluate with R-SQR metric**</span></span>

<span data-ttu-id="65398-403">*tmp_results* é registrado como uma tabela do Hive na célula anterior.</span><span class="sxs-lookup"><span data-stu-id="65398-403">*tmp_results* is registered as a Hive table in the previous cell.</span></span> <span data-ttu-id="65398-404">Os resultados da tabela são gerados no quadro de dados *sqlResults* para plotagem.</span><span class="sxs-lookup"><span data-stu-id="65398-404">Results from the table are output into the *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="65398-405">Veja o código</span><span class="sxs-lookup"><span data-stu-id="65398-405">Here is the code</span></span>

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


<span data-ttu-id="65398-406">Este é o código para calcular o R-sqr.</span><span class="sxs-lookup"><span data-stu-id="65398-406">Here is the code to calculate R-sqr.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


<span data-ttu-id="65398-407">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-407">**OUTPUT**</span></span>

<span data-ttu-id="65398-408">R-sqr = 0,619184907088</span><span class="sxs-lookup"><span data-stu-id="65398-408">R-sqr = 0.619184907088</span></span>

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a><span data-ttu-id="65398-409">Validação cruzada com limpeza de parâmetro usando o código personalizado para a regressão de floresta aleatória</span><span class="sxs-lookup"><span data-stu-id="65398-409">Cross validation with parameter sweep using custom code for random forest regression</span></span>
<span data-ttu-id="65398-410">O código nesta seção mostra como fazer a validação cruzada com a limpeza de parâmetro usando o código personalizado para a regressão de floresta aleatória e como avaliar o modelo em relação aos dados de teste.</span><span class="sxs-lookup"><span data-stu-id="65398-410">The code in this section shows how to do cross validation with parameter sweep using custom code for random forest regression and how to evaluate the model against test data.</span></span>

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

    # SPECIFY NUMFOLDS AND ARRAY TO HOLD METRICS
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="65398-411">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-411">**OUTPUT**</span></span>

<span data-ttu-id="65398-412">RMSE = 0,906972198262</span><span class="sxs-lookup"><span data-stu-id="65398-412">RMSE = 0.906972198262</span></span>

<span data-ttu-id="65398-413">R-sqr = 0,740751197012</span><span class="sxs-lookup"><span data-stu-id="65398-413">R-sqr = 0.740751197012</span></span>

<span data-ttu-id="65398-414">Tempo necessário para executar a célula acima: 69,17 segundos</span><span class="sxs-lookup"><span data-stu-id="65398-414">Time taken to execute above cell: 69.17 seconds</span></span>

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a><span data-ttu-id="65398-415">Limpar objetos da memória e imprimir os locais de modelo</span><span class="sxs-lookup"><span data-stu-id="65398-415">Clean up objects from memory and print model locations</span></span>
<span data-ttu-id="65398-416">Use `unpersist()` para excluir objetos armazenados em cache na memória.</span><span class="sxs-lookup"><span data-stu-id="65398-416">Use `unpersist()` to delete objects cached in memory.</span></span>

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


<span data-ttu-id="65398-417">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-417">**OUTPUT**</span></span>

<span data-ttu-id="65398-418">PythonRDD[122] em RDD em PythonRDD.scala:43</span><span class="sxs-lookup"><span data-stu-id="65398-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span></span>

<span data-ttu-id="65398-419">* * Caminho de impressão para arquivos de modelo a ser usado no bloco de anotações de consumo.</span><span class="sxs-lookup"><span data-stu-id="65398-419">**Printout path to model files to be used in the consumption notebook.</span></span> <span data-ttu-id="65398-420">* * Para consumir e classificar um conjunto de dados independente, você precisa copiar e colar esses nomes de arquivo em "notebook de consumo".</span><span class="sxs-lookup"><span data-stu-id="65398-420">** To consume and score an independent data-set, you need to copy and paste these file names in the "Consumption notebook".</span></span>

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="65398-421">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="65398-421">**OUTPUT**</span></span>

<span data-ttu-id="65398-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span><span class="sxs-lookup"><span data-stu-id="65398-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span></span>

<span data-ttu-id="65398-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span><span class="sxs-lookup"><span data-stu-id="65398-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span></span>

<span data-ttu-id="65398-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span><span class="sxs-lookup"><span data-stu-id="65398-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span></span>

<span data-ttu-id="65398-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span><span class="sxs-lookup"><span data-stu-id="65398-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span></span>

<span data-ttu-id="65398-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span><span class="sxs-lookup"><span data-stu-id="65398-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span></span>

<span data-ttu-id="65398-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span><span class="sxs-lookup"><span data-stu-id="65398-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span></span>

## <a name="whats-next"></a><span data-ttu-id="65398-428">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="65398-428">What's next?</span></span>
<span data-ttu-id="65398-429">Agora que criou modelos de regressão e classificação com o Spark MlLib, você está pronto para aprender a classificar e avaliar os modelos.</span><span class="sxs-lookup"><span data-stu-id="65398-429">Now that you have created regression and classification models with the Spark MlLib, you are ready to learn how to score and evaluate these models.</span></span>

<span data-ttu-id="65398-430">**Consumo de modelos:** para aprender a pontuar e avaliar os modelos de classificação e regressão criados neste tópico, confira [Pontuar modelos de aprendizado de máquina criados no Spark](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="65398-430">**Model consumption:** To learn how to score and evaluate the classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

