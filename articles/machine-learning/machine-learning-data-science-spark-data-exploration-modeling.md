---
title: "Modelagem e exploração de dados com Spark | Microsoft Docs"
description: "Demonstra os recursos de exploração e modelagem de dados do kit de ferramentas do Spark MLlib no Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b989b918-5ba5-4696-b8d0-76ae510a23f4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 711407f7dd9e6d442e3f04a23962487f4808e8e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="data-exploration-and-modeling-with-spark"></a><span data-ttu-id="4dc6c-103">Modelagem e exploração de dados com Spark</span><span class="sxs-lookup"><span data-stu-id="4dc6c-103">Data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="4dc6c-104">Este passo a passo usa o HDInsight Spark para executar tarefas de exploração de dados e modelagem em um exemplo do conjunto de dados de corridas e tarifas de táxi de Nova York de 2013.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-104">This walkthrough uses HDInsight Spark to do data exploration and binary classification and regression modeling tasks on a sample of the NYC taxi trip and fare 2013 dataset.</span></span>  <span data-ttu-id="4dc6c-105">Ele o orienta ao longo das etapas do [Processo de Ciência de Dados](http://aka.ms/datascienceprocess), de ponta a ponta, usando um cluster HDInsight Spark para processamento e blobs do Azure para armazenar os dados e os modelos.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-105">It walks you through the steps of the [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs to store the data and the models.</span></span> <span data-ttu-id="4dc6c-106">O processo explora e visualiza os dados transferidos de um Blob de Armazenamento do Azure e prepara os dados para criar modelos preditivos.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-106">The process explores and visualizes data brought in from an Azure Storage Blob and then prepares the data to build predictive models.</span></span> <span data-ttu-id="4dc6c-107">Esses modelos são compilados usando o kit de ferramentas Spark MLlib para executar tarefas de classificação binária e modelagem de regressão.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-107">These models are build using the Spark MLlib toolkit to do binary classification and regression modeling tasks.</span></span>

* <span data-ttu-id="4dc6c-108">A tarefa de **classificação binária** consiste em prever se uma gorjeta é paga ou não pela corrida.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-108">The **binary classification** task is to predict whether or not a tip is paid for the trip.</span></span> 
* <span data-ttu-id="4dc6c-109">A tarefa de **regressão** consiste em prever o valor da gorjeta com base em outros recursos de gorjeta.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-109">The **regression** task is to predict the amount of the tip based on other tip features.</span></span> 

<span data-ttu-id="4dc6c-110">Os modelos que usamos incluem regressão logística e linear, florestas aleatórias e árvores aumentadas gradientes:</span><span class="sxs-lookup"><span data-stu-id="4dc6c-110">The models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="4dc6c-111">[Regressão linear com SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) é um modelo de regressão linear que usa um método SGD (Stochastic Gradient Descent) para otimização e dimensionamento de recursos para prever os valores das gorjetas pagas.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-111">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling to predict the tip amounts paid.</span></span> 
* <span data-ttu-id="4dc6c-112">[Regressão logística com LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) ou regressão "logit" é um modelo de regressão que pode ser usado quando a variável dependente é categórica para fazer a classificação de dados.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-112">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when the dependent variable is categorical to do data classification.</span></span> <span data-ttu-id="4dc6c-113">LBFGS é um algoritmo de otimização quase Newton que aproxima o algoritmo BFGS (Broyden–Fletcher–Goldfarb–Shanno) usando uma quantidade limitada de memória do computador e que é amplamente usado no aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-113">LBFGS is a quasi-Newton optimization algorithm that approximates the Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="4dc6c-114">[Florestas aleatórias](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) são conjuntos de árvores de decisão.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-114">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="4dc6c-115">Elas combinam várias árvores de decisão para reduzir o risco de superajuste.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-115">They combine many decision trees to reduce the risk of overfitting.</span></span> <span data-ttu-id="4dc6c-116">Florestas aleatórias são usadas para classificação e regressão e podem manipular recursos categóricos e podem ser estendidas para a configuração de classificação multiclasse.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-116">Random forests are used for regression and classification and can handle categorical features and can be extended to the multiclass classification setting.</span></span> <span data-ttu-id="4dc6c-117">Elas não exigem o dimensionamento de recursos e são capazes de capturar não linearidades e interações de recursos.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-117">They do not require feature scaling and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="4dc6c-118">As florestas aleatórias são um dos modelos de aprendizado de máquina com maior taxa de sucesso para classificação e regressão.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-118">Random forests are one of the most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="4dc6c-119">[GBTs (árvores com aumento gradiente)](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) são conjuntos de árvores de decisão.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-119">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="4dc6c-120">As GBTs treinam árvores de decisão iterativamente para minimizar uma função de perda.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-120">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="4dc6c-121">As GBTs são usadas para regressão e classificação e podem lidar com recursos categóricos, não exigem o dimensionamento de recursos e podem capturar não linearidades e interações de recursos.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-121">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="4dc6c-122">Elas também podem ser usadas em uma configuração de classificação multiclasse.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-122">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="4dc6c-123">As etapas de modelagem também contêm código que mostra como treinar, avaliar e salvar cada tipo de modelo.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-123">The modeling steps also contain code showing how to train, evaluate, and save each type of model.</span></span> <span data-ttu-id="4dc6c-124">Python foi usado para codificar a solução e mostrar os gráficos relevantes.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-124">Python has been used to code the solution and to show the relevant plots.</span></span>   

> [!NOTE]
> <span data-ttu-id="4dc6c-125">Embora o kit de ferramentas Spark MLlib tenha sido projetado para trabalhar com grandes conjuntos de dados, uma amostra relativamente pequena (cerca de 30 Mb usando 170 mil linhas, cerca de 0,1% do conjunto de dados original NYC) foi usada por conveniência.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-125">Although the Spark MLlib toolkit is designed to work on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of the original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="4dc6c-126">O exercício fornecido aqui é executado com eficiência (em cerca de 10 minutos) em um cluster HDInsight com dois nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-126">The exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="4dc6c-127">O mesmo código, com pequenas modificações, pode ser usado para processar conjuntos de dados maiores, com as modificações apropriadas para armazenar dados na memória em cache e alterar o tamanho do cluster.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-127">The same code, with minor modifications, can be used to process larger data-sets, with appropriate modifications for caching data in memory and changing the cluster size.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="4dc6c-128">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4dc6c-128">Prerequisites</span></span>
<span data-ttu-id="4dc6c-129">Você precisara de uma conta do Azure e de um cluster HDInsight do Spark 1.6 (ou Spark 2.0) para concluir este passo a passo.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-129">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster to complete this walkthrough.</span></span> <span data-ttu-id="4dc6c-130">Confira o [Visão geral de Ciência de dados usando o Spark no Azure HDInsight](machine-learning-data-science-spark-overview.md) para obter instruções sobre como atender a esses requisitos.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-130">See the [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how to satisfy these requirements.</span></span> <span data-ttu-id="4dc6c-131">Esse tópico também contém uma descrição dos dados de Táxi NYC 2013 usados aqui e instruções sobre como executar código a partir de um notebook Jupyter no cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-131">That topic also contains a description of the NYC 2013 Taxi data used here and instructions on how to execute code from a Jupyter notebook on the Spark cluster.</span></span> 

## <a name="spark-clusters-and-notebooks"></a><span data-ttu-id="4dc6c-132">Blocos de notas e clusters do Spark</span><span class="sxs-lookup"><span data-stu-id="4dc6c-132">Spark clusters and notebooks</span></span>
<span data-ttu-id="4dc6c-133">As etapas de configuração e o código são fornecidos neste passo a passo para usar um HDInsight Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-133">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="4dc6c-134">Porém, notebooks Jupyter são fornecidos tanto para o HDInsight Spark 1.6 quanto para os clusters Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-134">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="4dc6c-135">Uma descrição de notebooks e links são fornecidos em [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) para o repositório do GitHub que os contém.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-135">A description of the notebooks and links to them are provided in the [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for the GitHub repository containing them.</span></span> <span data-ttu-id="4dc6c-136">No entanto, o código mostrado aqui e nos notebooks vinculados é genérico e funcionarão em qualquer cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-136">Moreover, the code here and in the linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="4dc6c-137">Se você não estiver usando o HDInsight Spark, as etapas de configuração e gerenciamento do cluster poderão ser ligeiramente diferentes do que é mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-137">If you are not using HDInsight Spark, the cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="4dc6c-138">Para sua conveniência, aqui estão os links para os notebooks Jupyter para Spark 1.6 (para execução no kernel do pySpark do servidor Jupyter Notebook) e Spark 2.0 (para execução no kernel pySpark3 do servidor Jupyter Notebook):</span><span class="sxs-lookup"><span data-stu-id="4dc6c-138">For convenience, here are the links to the Jupyter notebooks for Spark 1.6 (to be run in the pySpark kernel of the Jupyter Notebook server) and  Spark 2.0 (to be run in the pySpark3 kernel of the Jupyter Notebook server):</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="4dc6c-139">Blocos de notas Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="4dc6c-139">Spark 1.6 notebooks</span></span>

<span data-ttu-id="4dc6c-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): fornece informações sobre como executar a exploração, a modelagem e a pontuação de dados com vários algoritmos diferentes.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): Provides information on how to perform data exploration, modeling, and scoring with several different algorithms.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="4dc6c-141">Blocos de notas Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="4dc6c-141">Spark 2.0 notebooks</span></span>
<span data-ttu-id="4dc6c-142">As tarefas de regressão e classificação que são implementadas usando um cluster Spark 2.0 estão em notebooks separados e o notebook de classificação usa um conjunto de dados diferente:</span><span class="sxs-lookup"><span data-stu-id="4dc6c-142">The regression and classification tasks that are implemented using a Spark 2.0 cluster are in separate notebooks and the classification notebook uses a different data set:</span></span>

- <span data-ttu-id="4dc6c-143">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): este arquivo fornece informações sobre como realizar a exploração, modelagem e classificação de dados nos clusters do Spark 2.0 usando o conjunto de dados de tarifas e viagens de Táxi de Nova York descrito [aqui](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="4dc6c-143">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how to perform data exploration, modeling, and scoring in Spark 2.0 clusters using the NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span> <span data-ttu-id="4dc6c-144">Este notebook pode ser um bom ponto de partida para explorar rapidamente o código que fornecemos para o Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-144">This notebook may be a good starting point for quickly exploring the code we have provided for Spark 2.0.</span></span> <span data-ttu-id="4dc6c-145">Para uma análise mais detalhada do notebook dos dados de Táxi de Nova York, veja o próximo notebook nesta lista.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-145">For a more detailed notebook analyzes the NYC Taxi data, see the next notebook in this list.</span></span> <span data-ttu-id="4dc6c-146">Veja as anotações após esta lista que comparam esses notebooks.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-146">See the notes following this list that compare these notebooks.</span></span> 
- <span data-ttu-id="4dc6c-147">[Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): esse arquivo mostra como executar disputa de dados (operações SQL Spark e dataframe), exploração, modelagem e pontuação, utilizando as viagens de táxi de NYC e conjunto de dados de tarifas descritas [aqui](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="4dc6c-147">[Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): This file shows how to perform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using the NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span>
- <span data-ttu-id="4dc6c-148">[Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): esse arquivo mostra como executar disputa de dados (operações SQL Spark e dataframe), exploração, modelagem e pontuação, utilizando um conjunto de dados de partidas no horário de uma companhia aérea conhecida de 2011 e 2012.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-148">[Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): This file shows how to perform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using the well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="4dc6c-149">Integramos o conjunto de dados da companhia aérea com os dados de clima do aeroporto (por exemplo, velocidade do vento, temperatura, altitude etc.) antes da modelagem, para que esses recursos de tempo pudessem ser incluídos no modelo.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-149">We integrated the airline dataset with the airport weather data (e.g. windspeed, temperature, altitude etc.) prior to modeling, so these weather features can be included in the model.</span></span>

<!-- -->

> [!NOTE]
> <span data-ttu-id="4dc6c-150">O conjunto de dados da companhia aérea foi adicionado ao notebook Spark 2.0 para melhor ilustrar os algoritmos de classificação.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-150">The airline dataset was added to the Spark 2.0 notebooks to better illustrate the use of classification algorithms.</span></span> <span data-ttu-id="4dc6c-151">Consulte os links a seguir para obter informações sobre um conjunto de dados de partidas no horário e de clima:</span><span class="sxs-lookup"><span data-stu-id="4dc6c-151">See the following links for information about airline on-time departure dataset and weather dataset:</span></span>

>- <span data-ttu-id="4dc6c-152">Dados de partidas no horário em aeroportos: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span><span class="sxs-lookup"><span data-stu-id="4dc6c-152">Airline on-time departure data: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span></span>

>- <span data-ttu-id="4dc6c-153">Dados de clima aeroporto: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span><span class="sxs-lookup"><span data-stu-id="4dc6c-153">Airport weather data: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span></span> 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
<span data-ttu-id="4dc6c-154">Os notebooks do Spark 2.0 dos conjuntos de dados de atrasos de voo e táxi de Nova York podem levar 10 minutos ou mais para serem executados (dependendo do tamanho do seu cluster de HDI).</span><span class="sxs-lookup"><span data-stu-id="4dc6c-154">The Spark 2.0 notebooks on the NYC taxi and airline flight delay data-sets can take 10 mins or more to run (depending on the size of your HDI cluster).</span></span> <span data-ttu-id="4dc6c-155">O primeiro notebook da lista acima mostra muitos aspectos da exploração, visualização e treinamento de modelo AM de dados em um notebook que leva menos tempo para ser executado com um conjunto de dados de Nova York do exemplo abaixo, em que os arquivos de tarifas e táxi foram previamente integrados: [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) Este notebook leva menos tempo para concluir (2 a 3 minutos) e pode ser um bom ponto de partida para a exploração rápida do código que fornecemos para o Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-155">The first notebook in the above list shows many aspects of the data exploration, visualization and ML model training in a notebook that takes less time to run with down-sampled NYC data set, in which the taxi and fare files have been pre-joined: [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) This notebook takes a much shorter time to finish (2-3 mins) and may be a good starting point for quickly exploring the code we have provided for Spark 2.0.</span></span> 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
<span data-ttu-id="4dc6c-156">As descrições a seguir estão relacionadas ao uso do Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-156">The descriptions below are related to using Spark 1.6.</span></span> <span data-ttu-id="4dc6c-157">Para as versões do Spark 2.0, use os notebooks descritos e vinculados acima.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-157">For Spark 2.0 versions, please use the notebooks described and linked above.</span></span> 

<!-- -->

## <a name="setup-storage-locations-libraries-and-the-preset-spark-context"></a><span data-ttu-id="4dc6c-158">Instalação: locais de armazenamento, bibliotecas e o contexto predefinido do Spark</span><span class="sxs-lookup"><span data-stu-id="4dc6c-158">Setup: storage locations, libraries, and the preset Spark context</span></span>
<span data-ttu-id="4dc6c-159">O Spark pode ler e gravar em um Blob de Armazenamento do Azure (também conhecido como WASB).</span><span class="sxs-lookup"><span data-stu-id="4dc6c-159">Spark is able to read and write to Azure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="4dc6c-160">Portanto, qualquer dado existente armazenado lá pode ser processado usando o Spark, e os resultados podem ser armazenados novamente no WASB.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-160">So any of your existing data stored there can be processed using Spark and the results stored again in WASB.</span></span>

<span data-ttu-id="4dc6c-161">Para salvar arquivos ou modelos no WASB, o caminho deve ser especificado corretamente.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-161">To save models or files in WASB, the path needs to be specified properly.</span></span> <span data-ttu-id="4dc6c-162">O contêiner padrão anexado ao cluster Spark pode ser referenciado usando um caminho que começa com: “wasb:///”.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-162">The default container attached to the Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="4dc6c-163">Outros locais são referenciados por "wasb://".</span><span class="sxs-lookup"><span data-stu-id="4dc6c-163">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="4dc6c-164">Definir caminhos de diretório para locais de armazenamento no WASB</span><span class="sxs-lookup"><span data-stu-id="4dc6c-164">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="4dc6c-165">O exemplo de código a seguir especifica o local dos dados a serem lidos e o caminho do diretório de armazenamento de modelo em que a saída do modelo será salva:</span><span class="sxs-lookup"><span data-stu-id="4dc6c-165">The following code sample specifies the location of the data to be read and the path for the model storage directory to which the model output is saved:</span></span>

    # SET PATHS TO FILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";

    # SET THE MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT THE FINAL BACKSLASH IN THE PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a><span data-ttu-id="4dc6c-166">Importar bibliotecas</span><span class="sxs-lookup"><span data-stu-id="4dc6c-166">Import libraries</span></span>
<span data-ttu-id="4dc6c-167">A instalação também requer a importação das bibliotecas necessárias.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-167">Set up also requires importing necessary libraries.</span></span> <span data-ttu-id="4dc6c-168">Defina o contexto do Spark e importe as bibliotecas necessárias com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="4dc6c-168">Set spark context and import necessary libraries with the following code:</span></span>

    # IMPORT LIBRARIES
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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="4dc6c-169">Contexto predefinido do Spark e palavras mágicas do PySpark</span><span class="sxs-lookup"><span data-stu-id="4dc6c-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="4dc6c-170">Os kernels PySpark fornecidos com os notebooks Jupyter têm contextos predefinidos.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-170">The PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="4dc6c-171">Portanto, não é necessário definir explicitamente os contextos Spark ou Hive antes de começar a trabalhar com o aplicativo que você está desenvolvendo.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-171">So you do not need to set the Spark or Hive contexts explicitly before you start working with the application you are developing.</span></span> <span data-ttu-id="4dc6c-172">Esses contextos estão disponíveis para você por padrão.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-172">These contexts are available for you by default.</span></span> <span data-ttu-id="4dc6c-173">Esses contextos são:</span><span class="sxs-lookup"><span data-stu-id="4dc6c-173">These contexts are:</span></span>

* <span data-ttu-id="4dc6c-174">sc - para o Spark</span><span class="sxs-lookup"><span data-stu-id="4dc6c-174">sc - for Spark</span></span> 
* <span data-ttu-id="4dc6c-175">sqlContext - para o Hive</span><span class="sxs-lookup"><span data-stu-id="4dc6c-175">sqlContext - for Hive</span></span>

<span data-ttu-id="4dc6c-176">O kernel PySpark fornece algumas “palavras mágicas” predefinidas, que são comandos especiais que podem ser chamados com %%.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-176">The PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="4dc6c-177">Há dois comandos que são usados nesses exemplos de código.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="4dc6c-178">**%%local** Especifica que o código nas linhas posteriores é executado localmente.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-178">**%%local** Specifies that the code in subsequent lines is to be executed locally.</span></span> <span data-ttu-id="4dc6c-179">O código deve ser um código Python válido.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="4dc6c-180">**%%sql -o <variable name>** Executa uma consulta do Hive no sqlContext.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-180">**%%sql -o <variable name>** Executes a Hive query against the sqlContext.</span></span> <span data-ttu-id="4dc6c-181">Se o parâmetro -o for transmitido, o resultado da consulta será persistido no contexto %%local do Python como um quadro de dados do Pandas.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-181">If the -o parameter is passed, the result of the query is persisted in the %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="4dc6c-182">Para saber mais sobre os kernels para notebooks Jupyter e as "palavras mágicas" predefinidas que eles fornecem, confira [Kernels disponíveis para notebooks Jupyter com clusters Linux do HDInsight Spark no HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="4dc6c-182">For more information on the kernels for Jupyter notebooks and the predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="4dc6c-183">Ingestão de dados de blob público</span><span class="sxs-lookup"><span data-stu-id="4dc6c-183">Data ingestion from public blob</span></span>
<span data-ttu-id="4dc6c-184">A primeira etapa no processo de ciência de dados é ingerir os dados a serem analisados de fontes nas quais eles residem para seu ambiente de modelagem e exploração de dados.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-184">The first step in the data science process is to ingest the data to be analyzed from sources where is resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="4dc6c-185">Neste passo a passo, o ambiente é o Spark.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-185">The environment is Spark in this walkthrough.</span></span> <span data-ttu-id="4dc6c-186">Esta seção contém o código para concluir uma série de tarefas:</span><span class="sxs-lookup"><span data-stu-id="4dc6c-186">This section contains the code to complete a series of tasks:</span></span>

* <span data-ttu-id="4dc6c-187">ingerir a amostra de dados a ser modelada</span><span class="sxs-lookup"><span data-stu-id="4dc6c-187">ingest the data sample to be modeled</span></span>
* <span data-ttu-id="4dc6c-188">ler o conjunto de dados (armazenado como um arquivo .tsv)</span><span class="sxs-lookup"><span data-stu-id="4dc6c-188">read in the input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="4dc6c-189">formatar e limpar os dados</span><span class="sxs-lookup"><span data-stu-id="4dc6c-189">format and clean the data</span></span>
* <span data-ttu-id="4dc6c-190">criar e armazenar objetos em cache (RDDs ou quadros de dados) na memória</span><span class="sxs-lookup"><span data-stu-id="4dc6c-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="4dc6c-191">registrá-lo como uma tabela temporária no contexto do SQL.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="4dc6c-192">Aqui está o código para ingestão de dados.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-192">Here is the code for data ingestion.</span></span>

    # INGEST DATA

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


    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="4dc6c-193">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-193">**OUTPUT:**</span></span>

<span data-ttu-id="4dc6c-194">Tempo necessário para executar a célula acima: 51,72 segundos</span><span class="sxs-lookup"><span data-stu-id="4dc6c-194">Time taken to execute above cell: 51.72 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="4dc6c-195">Visualização e exploração de dados</span><span class="sxs-lookup"><span data-stu-id="4dc6c-195">Data exploration & visualization</span></span>
<span data-ttu-id="4dc6c-196">Depois que os dados forem incluídos no Spark, a próxima etapa no processo de ciência de dados será obter uma compreensão mais profunda dos dados por meio de exploração e visualização.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-196">Once the data has been brought into Spark, the next step in the data science process is to gain deeper understanding of the data through exploration and visualization.</span></span> <span data-ttu-id="4dc6c-197">Nesta seção, podemos examinar os dados de táxi usando consultas SQL e plotar as variáveis de destino e os recursos em potencial para inspeção visual.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-197">In this section, we examine the taxi data using SQL queries and plot the target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="4dc6c-198">Especificamente, plotamos a frequência das contagens de passageiros em corridas de táxi, a frequência de gorjetas e como as gorjetas variam de acordo com o valor e o tipo de pagamento.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-198">Specifically, we plot the frequency of passenger counts in taxi trips, the frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-the-sample-of-taxi-trips"></a><span data-ttu-id="4dc6c-199">Plotar um histograma de frequências de contagens de passageiros na amostra de corridas de táxi</span><span class="sxs-lookup"><span data-stu-id="4dc6c-199">Plot a histogram of passenger count frequencies in the sample of taxi trips</span></span>
<span data-ttu-id="4dc6c-200">Este código e os trechos de código posteriores usam as palavras mágicas do SQL para consultar a amostra e as palavras mágicas locais para plotar os dados.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-200">This code and subsequent snippets use SQL magic to query the sample and local magic to plot the data.</span></span>

* <span data-ttu-id="4dc6c-201">A **mágica do SQL (`%%sql`)** O kernel HDInsight PySpark dá suporte a consultas do HiveQL fáceis e embutidas no sqlContext.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-201">**SQL magic (`%%sql`)** The HDInsight PySpark kernel supports easy inline HiveQL queries against the sqlContext.</span></span> <span data-ttu-id="4dc6c-202">O argumento (-o VARIABLE_NAME) persiste a saída da consulta SQL como um quadro de dados do Pandas no servidor do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-202">The (-o VARIABLE_NAME) argument persists the output of the SQL query as a Pandas DataFrame on the Jupyter server.</span></span> <span data-ttu-id="4dc6c-203">Isso significa que ele está disponível no modo local.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-203">This means it is available in the local mode.</span></span>
* <span data-ttu-id="4dc6c-204">A **`%%local`** é usada para executar o código localmente no servidor do Jupyter, que é o nó de cabeçalho do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-204">The **`%%local` magic** is used to run code locally on the Jupyter server, which is the headnode of the HDInsight cluster.</span></span> <span data-ttu-id="4dc6c-205">Normalmente, você usa a palavra mágica `%%local` em conjunto com a palavra mágica `%%sql` com o parâmetro -o.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-205">Typically, you use `%%local` magic in conjunction with the `%%sql` magic with -o parameter.</span></span> <span data-ttu-id="4dc6c-206">O parâmetro -o persistiria a saída da consulta SQL localmente e, em seguida, as palavras mágicas de %%local disparariam o próximo conjunto de trechos de código para serem executados localmente na saída das consultas SQL que é persistida localmente</span><span class="sxs-lookup"><span data-stu-id="4dc6c-206">The -o parameter would persist the output of the SQL query locally and then %%local magic would trigger the next set of code snippet to run locally against the output of the SQL queries that is persisted locally</span></span>

<span data-ttu-id="4dc6c-207">A saída é visualizada automaticamente após a execução do código.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-207">The output is automatically visualized after you run the code.</span></span>

<span data-ttu-id="4dc6c-208">Essa consulta recupera as corridas por contagem de passageiros.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-208">This query retrieves the trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST THE sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

<span data-ttu-id="4dc6c-209">Esse código cria um quadro de dados local da saída da consulta e plota os dados.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-209">This code creates a local data-frame from the query output and plots the data.</span></span> <span data-ttu-id="4dc6c-210">A palavra mágica `%%local` cria um quadro de dados local, `sqlResults`, que pode ser usado para plotar com matplotlib.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-210">The `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="4dc6c-211">Essas palavras mágicas do PySpark são usadas várias vezes neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-211">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="4dc6c-212">Se a quantidade de dados for grande, você deverá obter uma amostra para criar um quadro de dados que se ajusta na memória local.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-212">If the amount of data is large, you should sample to create a data-frame that can fit in local memory.</span></span>
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES. 
    # CLICK ON THE TYPE OF PLOT TO BE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="4dc6c-213">Este é o código para plotar as corridas por contagens de passageiros</span><span class="sxs-lookup"><span data-stu-id="4dc6c-213">Here is the code to plot the trips by passenger counts</span></span>

    # PLOT PASSENGER NUMBER VS. TRIP COUNTS
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

<span data-ttu-id="4dc6c-214">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-214">**OUTPUT:**</span></span>

![Frequência de corridas por contagem de passageiros](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

<span data-ttu-id="4dc6c-216">É possível selecionar entre vários tipos diferentes de visualizações (Tabela, Pizza, Linha, Área ou Barra) usando os botões de menu **Tipo** no notebook.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-216">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using the **Type** menu buttons in the notebook.</span></span> <span data-ttu-id="4dc6c-217">A plotagem de Barras é mostrada aqui.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-217">The Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="4dc6c-218">Plote um histograma de valores de gorjetas e como o valor das gorjetas varia pelas tarifas e contagens de passageiros.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-218">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="4dc6c-219">Use uma consulta SQL para obter amostra de dados.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-219">Use a SQL query to sample data.</span></span>

    #PLOT HISTOGRAM OF TIP AMOUNTS AND VARIATION BY PASSENGER COUNT AND PAYMENT TYPE

    # HIVEQL QUERY AGAINST THE sqlContext
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


<span data-ttu-id="4dc6c-220">Esta célula de código usa a consulta SQL para criar três plotagens dos dados.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-220">This code cell uses the SQL query to create three plots the data.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # HISTOGRAM OF TIP AMOUNTS AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 100, -2, 20])
    plt.show()


<span data-ttu-id="4dc6c-221">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-221">**OUTPUT:**</span></span> 

![Distribuição de valores de gorjetas](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![Valor de gorjeta por contagem de passageiros](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Valor de gorjeta por valor de tarifa](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="4dc6c-225">Engenharia de recursos, transformação e preparação de dados para a modelagem</span><span class="sxs-lookup"><span data-stu-id="4dc6c-225">Feature engineering, transformation and data preparation for modeling</span></span>
<span data-ttu-id="4dc6c-226">Esta seção descreve e fornece o código para os procedimentos usados para preparar dados para uso na modelagem ML.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-226">This section describes and provides the code for procedures used to prepare data for use in ML modeling.</span></span> <span data-ttu-id="4dc6c-227">Ela mostra como realizar as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="4dc6c-227">It shows how to do the following tasks:</span></span>

* <span data-ttu-id="4dc6c-228">Criar um novo recurso reunindo horários em blocos de tempo de tráfego</span><span class="sxs-lookup"><span data-stu-id="4dc6c-228">Create a new feature by binning hours into traffic time buckets</span></span>
* <span data-ttu-id="4dc6c-229">Indexar e codificar recursos categóricos</span><span class="sxs-lookup"><span data-stu-id="4dc6c-229">Index and encode categorical features</span></span>
* <span data-ttu-id="4dc6c-230">Criar objetos de ponto rotulado para entrada em funções de ML</span><span class="sxs-lookup"><span data-stu-id="4dc6c-230">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="4dc6c-231">Criar uma subamostragem aleatória dos dados e dividi-la em conjuntos de treinamento e teste</span><span class="sxs-lookup"><span data-stu-id="4dc6c-231">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
* <span data-ttu-id="4dc6c-232">Dimensionamento de recursos</span><span class="sxs-lookup"><span data-stu-id="4dc6c-232">Feature scaling</span></span>
* <span data-ttu-id="4dc6c-233">Armazenar objetos em cache na memória</span><span class="sxs-lookup"><span data-stu-id="4dc6c-233">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="4dc6c-234">Criar um novo recurso reunindo horários em blocos de tempo de tráfego</span><span class="sxs-lookup"><span data-stu-id="4dc6c-234">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="4dc6c-235">Este código mostra como criar um novo recurso reunindo horários em blocos de tempo de tráfego e como armazenar em cache o quadro de dados resultante na memória.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-235">This code shows how to create a new feature by binning hours into traffic time buckets and then how to cache the resulting data frame in memory.</span></span> <span data-ttu-id="4dc6c-236">Quando RDDs (Conjuntos de Dados Resilientes Distribuídos) e quadros de dados são usados repetidamente, o armazenamento em cache leva a tempos de execução melhores.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-236">Where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly, caching leads to improved execution times.</span></span> <span data-ttu-id="4dc6c-237">Da mesma forma, armazenamos em cache RDDs e quadros de dados em vários estágios no passo a passo.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-237">Accordingly, we cache RDDs and data-frames at several stages in the walkthrough.</span></span> 

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

<span data-ttu-id="4dc6c-238">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-238">**OUTPUT:**</span></span> 

<span data-ttu-id="4dc6c-239">126050</span><span class="sxs-lookup"><span data-stu-id="4dc6c-239">126050</span></span>

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a><span data-ttu-id="4dc6c-240">Indexar e codificar recursos categóricos para entrada em funções de modelagem</span><span class="sxs-lookup"><span data-stu-id="4dc6c-240">Index and encode categorical features for input into modeling functions</span></span>
<span data-ttu-id="4dc6c-241">Esta seção mostra como indexar ou codificar recursos categóricos para entrada nas funções de modelagem.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-241">This section shows how to index or encode categorical features for input into the modeling functions.</span></span> <span data-ttu-id="4dc6c-242">As funções de modelagem e previsão de MLlib exigem que recursos com dados de entrada categóricos sejam indexados ou codificados antes do uso.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-242">The modeling and predict functions of MLlib require features with categorical input data to be indexed or encoded prior to use.</span></span> <span data-ttu-id="4dc6c-243">Dependendo do modelo, você precisa indexá-los ou codificá-los de maneiras diferentes:</span><span class="sxs-lookup"><span data-stu-id="4dc6c-243">Depending on the model, you need to index or encode them in different ways:</span></span>  

* <span data-ttu-id="4dc6c-244">**Modelagem em forma de árvore** requer que as categorias sejam codificadas como valores numéricos (por exemplo, um recurso com três categorias pode ser codificado com 0, 1, 2).</span><span class="sxs-lookup"><span data-stu-id="4dc6c-244">**Tree-based modeling** requires categories to be encoded as numerical values (for example, a feature with three categories may be encoded with 0, 1, 2).</span></span> <span data-ttu-id="4dc6c-245">Isso é fornecido pela função [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) do MLlib.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-245">This is provided by MLlib’s [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) function.</span></span> <span data-ttu-id="4dc6c-246">Essa função codifica uma coluna de cadeia de caracteres de rótulos para uma coluna de índices de rótulo que são ordenados por frequências de rótulos.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-246">This function encodes a string column of labels to a column of label indices that are ordered by label frequencies.</span></span> <span data-ttu-id="4dc6c-247">Embora indexados com valores numéricos para entrada e manipulação de dados, os algoritmos baseados em árvore podem ser especificados para tratá-los adequadamente como categorias.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-247">Although indexed with numerical values for input and data handling, the tree-based algorithms can be specified to treat them appropriately as categories.</span></span> 
* <span data-ttu-id="4dc6c-248">**Modelos de regressão linear e logística** exigem codificação one-hot, em que, por exemplo, um recurso com três categorias pode ser expandido em três colunas de recursos, em que cada uma contém 0 ou 1, dependendo da categoria de uma observação.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-248">**Logistic and Linear Regression models** require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on the category of an observation.</span></span> <span data-ttu-id="4dc6c-249">A MLlib fornece a função [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) para executar a codificação one-hot.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-249">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function to do one-hot encoding.</span></span> <span data-ttu-id="4dc6c-250">Esse codificador mapeia uma coluna de índices de rótulo para uma coluna de vetores binários com, no máximo, um valor único.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-250">This encoder maps a column of label indices to a column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="4dc6c-251">Essa codificação permite que os algoritmos que esperam recursos valiosos numéricos, por exemplo a regressão logística, sejam aplicados em recursos categóricos.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-251">This encoding allows algorithms that expect numerical valued features, such as logistic regression, to be applied to categorical features.</span></span>

<span data-ttu-id="4dc6c-252">Aqui está o código para indexar e codificar recursos categóricos:</span><span class="sxs-lookup"><span data-stu-id="4dc6c-252">Here is the code to index and encode categorical features:</span></span>

    # INDEX AND ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES    
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

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

<span data-ttu-id="4dc6c-253">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-253">**OUTPUT:**</span></span>

<span data-ttu-id="4dc6c-254">Tempo necessário para executar a célula acima: 1,28 segundos</span><span class="sxs-lookup"><span data-stu-id="4dc6c-254">Time taken to execute above cell: 1.28 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="4dc6c-255">Criar objetos de ponto rotulado para entrada em funções de ML</span><span class="sxs-lookup"><span data-stu-id="4dc6c-255">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="4dc6c-256">Esta seção contém código que mostra como indexar dados de texto categóricos como um tipo de dados de ponto rotulado e codificá-lo para que ele possa ser usado para treinar e testar a regressão logística de MLlib e outros modelos de classificação.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-256">This section contains code that shows how to index categorical text data as a labeled point data type and encode it so that it can be used to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="4dc6c-257">Objetos de ponto rotulados são RDDs (Conjuntos de Dados Resilientes Distribuídos) formatados de uma maneira que é necessária como dados de entrada pela maioria dos algoritmos de ML no MLlib.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-257">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="4dc6c-258">Um [ponto rotulado](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) é um vetor local, denso ou esparso, associado a um rótulo/resposta.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-258">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>  

<span data-ttu-id="4dc6c-259">Esta seção contém código que mostra como indexar dados de texto categóricos como um tipo de dados de [ponto rotulado](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) e codificá-lo para que ele possa ser usado para treinar e testar a regressão logística de MLlib e outros modelos de classificação.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-259">This section contains code that shows how to index categorical text data as a [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) data type and encode it so that it can be used to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="4dc6c-260">Objetos de ponto de rotulado são RDDs (Conjuntos de Dados Resilientes Distribuídos) que consistem em um rótulo (variável de destino/resposta) e um vetor de recurso.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-260">Labeled point objects are Resilient Distributed Datasets (RDD) consisting of a label (target/response variable) and feature vector.</span></span> <span data-ttu-id="4dc6c-261">Esse formato é necessário como entrada para muitos algoritmos de ML no MLlib.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-261">This format is needed as input by many ML algorithms in MLlib.</span></span>

<span data-ttu-id="4dc6c-262">Este é o código para indexar e codificar recursos de texto para a classificação binária.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-262">Here is the code to index and encode text features for binary classification.</span></span>

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


<span data-ttu-id="4dc6c-263">Este é o código para codificar e indexar recursos de texto categórico para a análise de regressão linear.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-263">Here is the code to encode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-the-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="4dc6c-264">Criar uma subamostragem aleatória dos dados e dividi-la em conjuntos de treinamento e teste</span><span class="sxs-lookup"><span data-stu-id="4dc6c-264">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
<span data-ttu-id="4dc6c-265">Esse código cria uma amostragem aleatória dos dados (o valor de 25% é usado aqui).</span><span class="sxs-lookup"><span data-stu-id="4dc6c-265">This code creates a random sampling of the data (25% is used here).</span></span> <span data-ttu-id="4dc6c-266">Embora não seja necessário para este exemplo, devido ao tamanho do conjunto de dados, demonstramos como é possível obter amostras aqui, para que você saiba como usá-lo para seu próprio problema, quando necessário.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-266">Although it is not required for this example due to the size of the dataset, we demonstrate how you can sample here so you know how to use it for your own problem when needed.</span></span> <span data-ttu-id="4dc6c-267">Quando as amostras são grandes, isso pode economizar um tempo significativo durante o treinamento de modelos.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-267">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="4dc6c-268">Em seguida, dividimos o exemplo em uma parte de treinamento (75% aqui) e uma parte de teste (25% aqui) para usar na classificação e na modelagem de regressão.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-268">Next we split the sample into a training part (75% here) and a testing part (25% here) to use in classification and regression modeling.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.sql.functions import rand

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS (FOR USE LATER IN AN ADVANCED TOPIC)
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

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

<span data-ttu-id="4dc6c-269">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-269">**OUTPUT:**</span></span>

<span data-ttu-id="4dc6c-270">Tempo necessário para executar a célula acima: 0,24 segundos</span><span class="sxs-lookup"><span data-stu-id="4dc6c-270">Time taken to execute above cell: 0.24 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="4dc6c-271">Dimensionamento de recursos</span><span class="sxs-lookup"><span data-stu-id="4dc6c-271">Feature scaling</span></span>
<span data-ttu-id="4dc6c-272">O dimensionamento de recursos, também conhecido como normalização de dados, faz com que recursos com valores amplamente distribuídos não tenham peso excessivo na função objetiva.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-272">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in the objective function.</span></span> <span data-ttu-id="4dc6c-273">O código para o dimensionamento de recursos usa [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) para dimensionar os recursos para variância de unidade.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-273">The code for feature scaling uses the [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) to scale the features to unit variance.</span></span> <span data-ttu-id="4dc6c-274">Ele é fornecido por MLlib para uso na regressão linear com SGD (Stochastic Gradient Descent), um algoritmo popular de treinamento de uma grande variedade de outros modelos de aprendizado de máquina, como regressões regularizadas ou SVM (máquinas de vetor de suporte).</span><span class="sxs-lookup"><span data-stu-id="4dc6c-274">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>

> [!NOTE]
> <span data-ttu-id="4dc6c-275">Observamos que o algoritmo LinearRegressionWithSGD é sensível ao dimensionamento de recursos.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-275">We have found the LinearRegressionWithSGD algorithm to be sensitive to feature scaling.</span></span>
> 
> 

<span data-ttu-id="4dc6c-276">Veja o código para escalar as variáveis para uso com o algoritmo SGD linear regularizado.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-276">Here is the code to scale variables for use with the regularized linear SGD algorithm.</span></span>

    # FEATURE SCALING

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

<span data-ttu-id="4dc6c-277">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-277">**OUTPUT:**</span></span>

<span data-ttu-id="4dc6c-278">Tempo necessário para executar a célula acima: 13,17 segundos</span><span class="sxs-lookup"><span data-stu-id="4dc6c-278">Time taken to execute above cell: 13.17 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="4dc6c-279">Armazenar objetos em cache na memória</span><span class="sxs-lookup"><span data-stu-id="4dc6c-279">Cache objects in memory</span></span>
<span data-ttu-id="4dc6c-280">O tempo necessário para treinamento e teste dos algoritmos de ML pode ser reduzido armazenando-se em cache os objetos de quadro de dados de entrada usados para classificação, regressão e recursos dimensionados.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-280">The time taken for training and testing of ML algorithms can be reduced by caching the input data frame objects used for classification, regression, and scaled features.</span></span>

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

<span data-ttu-id="4dc6c-281">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-281">**OUTPUT:**</span></span> 

<span data-ttu-id="4dc6c-282">Tempo necessário para executar a célula acima: 0,15 segundos</span><span class="sxs-lookup"><span data-stu-id="4dc6c-282">Time taken to execute above cell: 0.15 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="4dc6c-283">Prever se uma gorjeta é paga ou não com modelos de classificação binária</span><span class="sxs-lookup"><span data-stu-id="4dc6c-283">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="4dc6c-284">Esta seção mostra como usar três modelos para a tarefa de classificação binária de prever se uma gorjeta é paga ou não por uma corrida de táxi.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-284">This section shows how use three models for the binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="4dc6c-285">Os modelos apresentados são:</span><span class="sxs-lookup"><span data-stu-id="4dc6c-285">The models presented are:</span></span>

* <span data-ttu-id="4dc6c-286">Regressão logística regularizada</span><span class="sxs-lookup"><span data-stu-id="4dc6c-286">Regularized logistic regression</span></span> 
* <span data-ttu-id="4dc6c-287">Modelo de floresta aleatória</span><span class="sxs-lookup"><span data-stu-id="4dc6c-287">Random forest model</span></span>
* <span data-ttu-id="4dc6c-288">Árvores de Ampliação de Gradiente</span><span class="sxs-lookup"><span data-stu-id="4dc6c-288">Gradient Boosting Trees</span></span>

<span data-ttu-id="4dc6c-289">Cada seção de código de compilação de modelo é dividida em etapas:</span><span class="sxs-lookup"><span data-stu-id="4dc6c-289">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="4dc6c-290">**Modelar os dados de treinamento** com um conjunto de parâmetros</span><span class="sxs-lookup"><span data-stu-id="4dc6c-290">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="4dc6c-291">**Modelar a avaliação** em um conjunto de dados de teste com métricas</span><span class="sxs-lookup"><span data-stu-id="4dc6c-291">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="4dc6c-292">**Salvar modelo** no blob para consumo futuro</span><span class="sxs-lookup"><span data-stu-id="4dc6c-292">**Saving model** in blob for future consumption</span></span>

### <a name="classification-using-logistic-regression"></a><span data-ttu-id="4dc6c-293">Classificação usando regressão logística</span><span class="sxs-lookup"><span data-stu-id="4dc6c-293">Classification using logistic regression</span></span>
<span data-ttu-id="4dc6c-294">O código nesta seção mostra como treinar, avaliar e salvar um modelo de regressão logística com [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) que prevê se uma gorjeta será paga ou não por uma corrida no conjunto de dados de corridas e tarifas de táxi de Nova York.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-294">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

<span data-ttu-id="4dc6c-295">**Treinar o modelo de regressão logística usando a CV e a limpeza de hiperparâmetro**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-295">**Train the logistic regression model using CV and hyperparameter sweeping**</span></span>

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics


    # CREATE MODEL WITH ONE SET OF PARAMETERS
    logitModel = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, iterations=20, initialWeights=None, 
                                                   regParam=0.01, regType='l2', intercept=True, corrections=10, 
                                                   tolerance=0.0001, validateData=True, numClasses=2)

    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitModel.weights))
    print("Intercept: " + str(logitModel.intercept))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="4dc6c-296">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-296">**OUTPUT:**</span></span> 

<span data-ttu-id="4dc6c-297">Coeficientes: [0,0082065285375, -0,0223675576104, -0,0183812028036, -3,48124578069e-05, -0,00247646947233, -0,00165897881503, 0,0675394837328, -0,111823113101, -0,324609912762, -0,204549780032, -1,36499216354, 0,591088507921, -0,664263411392, -1,00439726852, 3,46567827545, -3,51025855172, -0,0471341112232, -0,043521833294, 0,000243375810385, 0,054518719222]</span><span class="sxs-lookup"><span data-stu-id="4dc6c-297">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="4dc6c-298">Interceptação: -0,0111216486893</span><span class="sxs-lookup"><span data-stu-id="4dc6c-298">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="4dc6c-299">Tempo necessário para executar a célula acima: 14,43 segundos</span><span class="sxs-lookup"><span data-stu-id="4dc6c-299">Time taken to execute above cell: 14.43 seconds</span></span>

<span data-ttu-id="4dc6c-300">**Avaliar o modelo de classificação binária com métricas padrão**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-300">**Evaluate the binary classification model with standard metrics**</span></span>

    #EVALUATE LOGISTIC REGRESSION MODEL WITH LBFGS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # PREDICT ON TEST DATA WITH MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitModel.predict(lp.features)), lp.label))

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


    ## SAVE MODEL WITH DATE-STAMP
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;
    logitModel.save(sc, dirfilename);

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitModel.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="4dc6c-301">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-301">**OUTPUT:**</span></span> 

<span data-ttu-id="4dc6c-302">Área sob PR = 0,985297691373</span><span class="sxs-lookup"><span data-stu-id="4dc6c-302">Area under PR = 0.985297691373</span></span>

<span data-ttu-id="4dc6c-303">Área sob ROC = 0,983714670256</span><span class="sxs-lookup"><span data-stu-id="4dc6c-303">Area under ROC = 0.983714670256</span></span>

<span data-ttu-id="4dc6c-304">Estatísticas de resumo</span><span class="sxs-lookup"><span data-stu-id="4dc6c-304">Summary Stats</span></span>

<span data-ttu-id="4dc6c-305">Precisão = 0,984304060189</span><span class="sxs-lookup"><span data-stu-id="4dc6c-305">Precision = 0.984304060189</span></span>

<span data-ttu-id="4dc6c-306">Recuperação = 0,984304060189</span><span class="sxs-lookup"><span data-stu-id="4dc6c-306">Recall = 0.984304060189</span></span>

<span data-ttu-id="4dc6c-307">Pontuação F1 = 0,984304060189</span><span class="sxs-lookup"><span data-stu-id="4dc6c-307">F1 Score = 0.984304060189</span></span>

<span data-ttu-id="4dc6c-308">Tempo necessário para executar a célula acima: 57,61 segundos</span><span class="sxs-lookup"><span data-stu-id="4dc6c-308">Time taken to execute above cell: 57.61 seconds</span></span>

<span data-ttu-id="4dc6c-309">**Plote a curva ROC.**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-309">**Plot the ROC curve.**</span></span>

<span data-ttu-id="4dc6c-310">O *predictionAndLabelsDF* é registrado como uma tabela, *tmp_results*, na célula anterior.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-310">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span></span> <span data-ttu-id="4dc6c-311">A tabela *tmp_results* pode ser usada para fazer consultas e resultados de saída para o quadro de dados sqlResults para plotagem.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-311">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span></span> <span data-ttu-id="4dc6c-312">Veja o código.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-312">Here is the code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="4dc6c-313">Este é o código para fazer previsões e plotar a curva ROC.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-313">Here is the code to make predictions and plot the ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    # MAKE PREDICTIONS
    predictions_pddf = test_predictions.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVE
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


<span data-ttu-id="4dc6c-314">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-314">**OUTPUT:**</span></span>

![curve.png de ROC de regressão logística](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="4dc6c-316">Classificação de floresta aleatória</span><span class="sxs-lookup"><span data-stu-id="4dc6c-316">Random forest classification</span></span>
<span data-ttu-id="4dc6c-317">O código nesta seção mostra como treinar, avaliar e salvar um modelo de floresta aleatória que prevê se uma gorjeta é paga ou não por uma corrida no conjunto de dados de corridas e tarifas de táxi de Nova York.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-317">The code in this section shows how to train, evaluate, and save a random forest model that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

    #PREDICT WHETHER A TIP IS PAID OR NOT USING RANDOM FOREST

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
    ## UN-COMMENT IF YOU WANT TO PRINT TREES
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

<span data-ttu-id="4dc6c-318">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-318">**OUTPUT:**</span></span>

<span data-ttu-id="4dc6c-319">Área sob ROC = 0,985297691373</span><span class="sxs-lookup"><span data-stu-id="4dc6c-319">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="4dc6c-320">Tempo necessário para executar a célula acima: 31,09 segundos</span><span class="sxs-lookup"><span data-stu-id="4dc6c-320">Time taken to execute above cell: 31.09 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="4dc6c-321">Classificação de árvores de ampliação de gradiente</span><span class="sxs-lookup"><span data-stu-id="4dc6c-321">Gradient boosting trees classification</span></span>
<span data-ttu-id="4dc6c-322">O código nesta seção mostra como treinar, avaliar e salvar um modelo de árvores de ampliação de gradiente que prevê se uma gorjeta é paga ou não por uma corrida no conjunto de dados de corridas e tarifas de táxi de Nova York.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-322">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

    #PREDICT WHETHER A TIP IS PAID OR NOT USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo, numIterations=5)
    ## UNCOMMENT IF YOU WANT TO PRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
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


<span data-ttu-id="4dc6c-323">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-323">**OUTPUT:**</span></span>

<span data-ttu-id="4dc6c-324">Área sob ROC = 0,985297691373</span><span class="sxs-lookup"><span data-stu-id="4dc6c-324">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="4dc6c-325">Tempo necessário para executar a célula acima: 19,76 segundos</span><span class="sxs-lookup"><span data-stu-id="4dc6c-325">Time taken to execute above cell: 19.76 seconds</span></span>

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a><span data-ttu-id="4dc6c-326">Prever valores de gorjetas para corridas de táxi com modelos de regressão</span><span class="sxs-lookup"><span data-stu-id="4dc6c-326">Predict tip amounts for taxi trips with regression models</span></span>
<span data-ttu-id="4dc6c-327">Esta seção mostra como usar três modelos para a tarefa de regressão de prever o valor da gorjeta paga por uma corrida de táxi com base em outros recursos de gorjeta.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-327">This section shows how use three models for the regression task of predicting the amount of the tip paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="4dc6c-328">Os modelos apresentados são:</span><span class="sxs-lookup"><span data-stu-id="4dc6c-328">The models presented are:</span></span>

* <span data-ttu-id="4dc6c-329">Regressão linear regularizada</span><span class="sxs-lookup"><span data-stu-id="4dc6c-329">Regularized linear regression</span></span>
* <span data-ttu-id="4dc6c-330">Floresta aleatória</span><span class="sxs-lookup"><span data-stu-id="4dc6c-330">Random forest</span></span>
* <span data-ttu-id="4dc6c-331">Árvores de Ampliação de Gradiente</span><span class="sxs-lookup"><span data-stu-id="4dc6c-331">Gradient Boosting Trees</span></span>

<span data-ttu-id="4dc6c-332">Esses modelos foram descritos na introdução.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-332">These models were described in the introduction.</span></span> <span data-ttu-id="4dc6c-333">Cada seção de código de compilação de modelo é dividida em etapas:</span><span class="sxs-lookup"><span data-stu-id="4dc6c-333">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="4dc6c-334">**Modelar os dados de treinamento** com um conjunto de parâmetros</span><span class="sxs-lookup"><span data-stu-id="4dc6c-334">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="4dc6c-335">**Modelar a avaliação** em um conjunto de dados de teste com métricas</span><span class="sxs-lookup"><span data-stu-id="4dc6c-335">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="4dc6c-336">**Salvar modelo** no blob para consumo futuro</span><span class="sxs-lookup"><span data-stu-id="4dc6c-336">**Saving model** in blob for future consumption</span></span>

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="4dc6c-337">Regressão linear com SGD</span><span class="sxs-lookup"><span data-stu-id="4dc6c-337">Linear regression with SGD</span></span>
<span data-ttu-id="4dc6c-338">O código nesta seção mostra como usar recursos dimensionados para treinar uma regressão linear que usa SGD (Stochastic Gradient Descent) para otimização e como pontuar, avaliar e salvar o modelo no WASB (Armazenamento de Blobs do Azure).</span><span class="sxs-lookup"><span data-stu-id="4dc6c-338">The code in this section shows how to use scaled features to train a linear regression that uses stochastic gradient descent (SGD) for optimization, and how to score, evaluate, and save the model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="4dc6c-339">Em nossa experiência, pode haver problemas com a convergência de modelos LinearRegressionWithSGD, e os parâmetros precisam ser alterados/otimizados cuidadosamente para a obtenção de um modelo válido.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-339">In our experience, there can be issues with the convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="4dc6c-340">O dimensionamento de variáveis ajuda significativamente com a convergência.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-340">Scaling of variables significantly helps with convergence.</span></span> 
> 
> 

    #PREDICT TIP AMOUNTS USING LINEAR REGRESSION WITH SGD

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

    # PRINT TEST METRICS
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL WITH DATE-STAMP IN THE DEFAULT BLOB FOR THE CLUSTER
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="4dc6c-341">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-341">**OUTPUT:**</span></span>

<span data-ttu-id="4dc6c-342">Coeficientes: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span><span class="sxs-lookup"><span data-stu-id="4dc6c-342">Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span></span>

<span data-ttu-id="4dc6c-343">Interceptação: 0,853872718283</span><span class="sxs-lookup"><span data-stu-id="4dc6c-343">Intercept: 0.853872718283</span></span>

<span data-ttu-id="4dc6c-344">RMSE = 1,24190115863</span><span class="sxs-lookup"><span data-stu-id="4dc6c-344">RMSE = 1.24190115863</span></span>

<span data-ttu-id="4dc6c-345">R-sqr = 0,608017146081</span><span class="sxs-lookup"><span data-stu-id="4dc6c-345">R-sqr = 0.608017146081</span></span>

<span data-ttu-id="4dc6c-346">Tempo necessário para executar a célula acima: 58,42 segundos</span><span class="sxs-lookup"><span data-stu-id="4dc6c-346">Time taken to execute above cell: 58.42 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="4dc6c-347">Regressão de Floresta Aleatória</span><span class="sxs-lookup"><span data-stu-id="4dc6c-347">Random Forest regression</span></span>
<span data-ttu-id="4dc6c-348">O código nesta seção mostra como treinar, avaliar e salvar uma regressão de floresta aleatória que prevê o valor da gorjeta para os dados de corridas de táxi de Nova York.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-348">The code in this section shows how to train, evaluate, and save a random forest regression that predicts tip amount for the NYC taxi trip data.</span></span>

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    ## UN-COMMENT IF YOU WANT TO PRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    ## PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
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

<span data-ttu-id="4dc6c-349">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-349">**OUTPUT:**</span></span>

<span data-ttu-id="4dc6c-350">RMSE = 0,891209218139</span><span class="sxs-lookup"><span data-stu-id="4dc6c-350">RMSE = 0.891209218139</span></span>

<span data-ttu-id="4dc6c-351">R-sqr = 0,759661334921</span><span class="sxs-lookup"><span data-stu-id="4dc6c-351">R-sqr = 0.759661334921</span></span>

<span data-ttu-id="4dc6c-352">Tempo necessário para executar a célula acima: 49,21 segundos</span><span class="sxs-lookup"><span data-stu-id="4dc6c-352">Time taken to execute above cell: 49.21 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="4dc6c-353">Regressão de árvores de ampliação de gradiente</span><span class="sxs-lookup"><span data-stu-id="4dc6c-353">Gradient boosting trees regression</span></span>
<span data-ttu-id="4dc6c-354">O código nesta seção mostra como treinar, avaliar e salvar um modelo de árvores de ampliação de gradiente que prevê o valor da gorjeta para os dados de corridas de táxi de Nova York.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-354">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts tip amount for the NYC taxi trip data.</span></span>

<span data-ttu-id="4dc6c-355">* * Treinar e avaliar * *</span><span class="sxs-lookup"><span data-stu-id="4dc6c-355">**Train and evaluate **</span></span>

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    ## EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # CONVER RESULTS TO DF AND REGISER TEMP TABLE
    test_predictions = sqlContext.createDataFrame(predictionAndLabels)
    test_predictions.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="4dc6c-356">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-356">**OUTPUT:**</span></span>

<span data-ttu-id="4dc6c-357">RMSE = 0,908473148639</span><span class="sxs-lookup"><span data-stu-id="4dc6c-357">RMSE = 0.908473148639</span></span>

<span data-ttu-id="4dc6c-358">R-sqr = 0,753835096681</span><span class="sxs-lookup"><span data-stu-id="4dc6c-358">R-sqr = 0.753835096681</span></span>

<span data-ttu-id="4dc6c-359">Tempo necessário para executar a célula acima: 34,52 segundos</span><span class="sxs-lookup"><span data-stu-id="4dc6c-359">Time taken to execute above cell: 34.52 seconds</span></span>

<span data-ttu-id="4dc6c-360">**Plotar**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-360">**Plot**</span></span>

<span data-ttu-id="4dc6c-361">*tmp_results* é registrado como uma tabela do Hive na célula anterior.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-361">*tmp_results* is registered as a Hive table in the previous cell.</span></span> <span data-ttu-id="4dc6c-362">Os resultados da tabela são gerados no quadro de dados *sqlResults* para plotagem.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-362">Results from the table are output into the *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="4dc6c-363">Veja o código</span><span class="sxs-lookup"><span data-stu-id="4dc6c-363">Here is the code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

<span data-ttu-id="4dc6c-364">Este é o código para plotar os dados usando o servidor do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-364">Here is the code to plot the data using the Jupyter server.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    import numpy as np

    # PLOT 
    ax = test_predictions_pddf.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(test_predictions_pddf['_1'], test_predictions_pddf['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(test_predictions_pddf['_1'], fit[0] * test_predictions_pddf['_1'] + fit[1], color='magenta')
    plt.axis([-1, 20, -1, 20])
    plt.show(ax)


<span data-ttu-id="4dc6c-365">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-365">**OUTPUT:**</span></span>

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a><span data-ttu-id="4dc6c-367">Limpar objetos da memória</span><span class="sxs-lookup"><span data-stu-id="4dc6c-367">Clean up objects from memory</span></span>
<span data-ttu-id="4dc6c-368">Use `unpersist()` para excluir objetos armazenados em cache na memória.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-368">Use `unpersist()` to delete objects cached in memory.</span></span>

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()

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


## <a name="record-storage-locations-of-the-models-for-consumption-and-scoring"></a><span data-ttu-id="4dc6c-369">Registre os locais de armazenamento dos modelos para consumo e pontuação</span><span class="sxs-lookup"><span data-stu-id="4dc6c-369">Record storage locations of the models for consumption and scoring</span></span>
<span data-ttu-id="4dc6c-370">Para o consumo e a pontuação de um conjunto de dados independente descrito no tópico [Pontuar e avaliar modelos de aprendizado de máquina criados com Spark](machine-learning-data-science-spark-model-consumption.md) , você precisa copiar e colar os nomes de arquivos que contêm os modelos salvos criados aqui para o bloco de anotações do Jupyter de Consumo.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-370">To consume and score an independent dataset described in the [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) topic, you need to copy and paste these file names containing the saved models created here into the Consumption Jupyter notebook.</span></span> <span data-ttu-id="4dc6c-371">Aqui está o código para imprimir os caminhos para os arquivos de modelo necessários.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-371">Here is the code to print out the paths to model files you need there.</span></span>

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="4dc6c-372">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="4dc6c-372">**OUTPUT**</span></span>

<span data-ttu-id="4dc6c-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span><span class="sxs-lookup"><span data-stu-id="4dc6c-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span></span>

<span data-ttu-id="4dc6c-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span><span class="sxs-lookup"><span data-stu-id="4dc6c-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span></span>

<span data-ttu-id="4dc6c-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span><span class="sxs-lookup"><span data-stu-id="4dc6c-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span></span>

<span data-ttu-id="4dc6c-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span><span class="sxs-lookup"><span data-stu-id="4dc6c-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span></span>

<span data-ttu-id="4dc6c-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span><span class="sxs-lookup"><span data-stu-id="4dc6c-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span></span>

<span data-ttu-id="4dc6c-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span><span class="sxs-lookup"><span data-stu-id="4dc6c-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span></span>

## <a name="whats-next"></a><span data-ttu-id="4dc6c-379">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="4dc6c-379">What's next?</span></span>
<span data-ttu-id="4dc6c-380">Agora que criou modelos de regressão e classificação com o Spark MlLib, você está pronto para aprender a classificar e avaliar os modelos.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-380">Now that you have created regression and classification models with the Spark MlLib, you are ready to learn how to score and evaluate these models.</span></span> <span data-ttu-id="4dc6c-381">O bloco de anotações de exploração e modelagem de dados avançadas se aprofunda na inclusão da validação cruzada, limpeza de hiperparâmetro e avaliação de modelo.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-381">The advanced data exploration and modeling notebook dives deeper into including cross-validation, hyper-parameter sweeping, and model evaluation.</span></span> 

<span data-ttu-id="4dc6c-382">**Consumo de modelos:** para aprender a pontuar e avaliar os modelos de classificação e regressão criados neste tópico, confira [Pontuar modelos de aprendizado de máquina criados no Spark](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="4dc6c-382">**Model consumption:** To learn how to score and evaluate the classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

<span data-ttu-id="4dc6c-383">**Validação cruzada e limpeza de hiperparâmetro**: confira [Modelagem e exploração de dados avançados com o Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) para saber como os modelos podem ser treinados usando a validação cruzada e a limpeza de hiperparâmetro</span><span class="sxs-lookup"><span data-stu-id="4dc6c-383">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping</span></span>

