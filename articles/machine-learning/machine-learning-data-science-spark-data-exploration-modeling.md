---
title: "exploração de aaaData e modelagem com Spark | Microsoft Docs"
description: "Apresenta Olá recursos do Kit de ferramentas do hello MLlib Spark no Azure de modelagem e exploração de dados."
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
ms.openlocfilehash: cf5cee4575053f5954b08ca659dfc39c53798371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="data-exploration-and-modeling-with-spark"></a><span data-ttu-id="7c3eb-103">Modelagem e exploração de dados com Spark</span><span class="sxs-lookup"><span data-stu-id="7c3eb-103">Data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="7c3eb-104">Este passo a passo usa a exploração de dados do HDInsight Spark toodo e classificação binária e regressão tarefas de modelagem em uma amostra de saudação NYC táxi viagem e passagens de conjunto de dados de 2013.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-104">This walkthrough uses HDInsight Spark toodo data exploration and binary classification and regression modeling tasks on a sample of hello NYC taxi trip and fare 2013 dataset.</span></span>  <span data-ttu-id="7c3eb-105">Lhe orienta pelas etapas de saudação do hello [processo de ciência de dados](http://aka.ms/datascienceprocess), cluster de ponta a ponta, usando um HDInsight Spark para processamento e modelos de dados e Olá Olá toostore de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-105">It walks you through hello steps of hello [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs toostore hello data and hello models.</span></span> <span data-ttu-id="7c3eb-106">processo de saudação explora e visualiza os dados transferidos de um Blob de armazenamento do Azure e, em seguida, prepara Olá dados toobuild modelos de previsão.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-106">hello process explores and visualizes data brought in from an Azure Storage Blob and then prepares hello data toobuild predictive models.</span></span> <span data-ttu-id="7c3eb-107">Esses modelos são compilados usando classificação binária do toodo Olá Spark MLlib Kit de ferramentas e tarefas de modelagem de regressão.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-107">These models are build using hello Spark MLlib toolkit toodo binary classification and regression modeling tasks.</span></span>

* <span data-ttu-id="7c3eb-108">Olá **classificação binária** tarefa é toopredict ou não uma dica é pago para viagem hello.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-108">hello **binary classification** task is toopredict whether or not a tip is paid for hello trip.</span></span> 
* <span data-ttu-id="7c3eb-109">Olá **regressão** tarefa é toopredict Olá Olá dica com base em outros recursos de dica.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-109">hello **regression** task is toopredict hello amount of hello tip based on other tip features.</span></span> 

<span data-ttu-id="7c3eb-110">os modelos de saudação que usamos incluem gradientes árvores aumentadas, florestas aleatórias e regressão logística e linear:</span><span class="sxs-lookup"><span data-stu-id="7c3eb-110">hello models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="7c3eb-111">[Regressão linear com SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) é um modelo de regressão linear que usa um método descendente gradiente Estocástico (SGD) e para a otimização e recurso de dimensionamento quantidades de dica de saudação toopredict pago.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-111">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling toopredict hello tip amounts paid.</span></span> 
* <span data-ttu-id="7c3eb-112">[Regressão logística com LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) ou regressão "logit", é um modelo de regressão que pode ser usado quando a variável dependente de saudação é categórica toodo a classificação de dados.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-112">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when hello dependent variable is categorical toodo data classification.</span></span> <span data-ttu-id="7c3eb-113">LBFGS é um algoritmo de otimização de quase-Newton que aproxima o algoritmo Broyden – Fletcher – Goldfarb – Shanno (BFGS) de saudação usando uma quantidade limitada de memória do computador e que é amplamente usada no aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-113">LBFGS is a quasi-Newton optimization algorithm that approximates hello Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="7c3eb-114">[Florestas aleatórias](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) são conjuntos de árvores de decisão.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-114">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="7c3eb-115">Elas combinam muitas decisões árvores tooreduce Olá risco de superajuste.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-115">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="7c3eb-116">Florestas aleatórias são usadas para classificação e regressão e podem lidar com recursos categóricos e configuração de classificação multiclasse toohello podem ser estendidas.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-116">Random forests are used for regression and classification and can handle categorical features and can be extended toohello multiclass classification setting.</span></span> <span data-ttu-id="7c3eb-117">Eles não exigem recurso escala e são capazes de toocapture não linearidades e interações de recurso.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-117">They do not require feature scaling and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="7c3eb-118">Florestas aleatórias são um dos modelos de classificação e regressão de aprendizado de máquina mais bem-sucedida de saudação.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-118">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="7c3eb-119">[GBTs (árvores com aumento gradiente)](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) são conjuntos de árvores de decisão.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-119">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="7c3eb-120">Árvores de decisão de treinar GBTs iterativamente toominimize uma função de perda.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-120">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="7c3eb-121">GBTs são usados para classificação e regressão pode lidar com recursos categóricos, não requerem o dimensionamento de recurso e são capazes de toocapture não linearidades e interações de recursos.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-121">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="7c3eb-122">Elas também podem ser usadas em uma configuração de classificação multiclasse.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-122">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="7c3eb-123">etapas de modelagem Olá também contêm código que mostra como tootrain, avaliar e salvar cada tipo de modelo.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-123">hello modeling steps also contain code showing how tootrain, evaluate, and save each type of model.</span></span> <span data-ttu-id="7c3eb-124">Python foi usado toocode Olá solução e tooshow Olá relevantes gráficos.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-124">Python has been used toocode hello solution and tooshow hello relevant plots.</span></span>   

> [!NOTE]
> <span data-ttu-id="7c3eb-125">Embora o Kit de ferramentas do hello Spark MLlib toowork projetado em grandes conjuntos de dados, um exemplo relativamente pequeno (aproximadamente 30 Mb usando 170 mil linhas, cerca de 0,1% de saudação original NYC dataset) é usado aqui para sua conveniência.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-125">Although hello Spark MLlib toolkit is designed toowork on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of hello original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="7c3eb-126">Exercício Olá fornecido aqui é executado com eficiência (em cerca de 10 minutos) em um cluster de HDInsight com 2 nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-126">hello exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="7c3eb-127">Olá mesmo código, com pequenas modificações, pode ser usado tooprocess-conjuntos de dados maiores, com as modificações apropriadas para o cache de dados na memória e alterar o tamanho do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-127">hello same code, with minor modifications, can be used tooprocess larger data-sets, with appropriate modifications for caching data in memory and changing hello cluster size.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="7c3eb-128">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7c3eb-128">Prerequisites</span></span>
<span data-ttu-id="7c3eb-129">Você precisa de uma conta do Azure e um Spark 1.6 (ou 2.0 Spark) cluster HDInsight toocomplete este passo a passo.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-129">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster toocomplete this walkthrough.</span></span> <span data-ttu-id="7c3eb-130">Consulte Olá [visão geral de ciência de dados usando o Spark no Azure HDInsight](machine-learning-data-science-spark-overview.md) para obter instruções sobre como toosatisfy esses requisitos.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-130">See hello [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how toosatisfy these requirements.</span></span> <span data-ttu-id="7c3eb-131">Esse tópico também contém uma descrição da saudação dados NYC 2013 táxi usados aqui e instruções sobre como tooexecute código de um bloco de anotações do Jupyter no cluster do Spark hello.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-131">That topic also contains a description of hello NYC 2013 Taxi data used here and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster.</span></span> 

## <a name="spark-clusters-and-notebooks"></a><span data-ttu-id="7c3eb-132">Blocos de notas e clusters do Spark</span><span class="sxs-lookup"><span data-stu-id="7c3eb-132">Spark clusters and notebooks</span></span>
<span data-ttu-id="7c3eb-133">As etapas de configuração e o código são fornecidos neste passo a passo para usar um HDInsight Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-133">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="7c3eb-134">Porém, notebooks Jupyter são fornecidos tanto para o HDInsight Spark 1.6 quanto para os clusters Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-134">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="7c3eb-135">Uma descrição da saudação toothem de anotações e links são fornecidos no hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) para o repositório do GitHub Olá que os contém.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-135">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="7c3eb-136">Além disso, Olá código aqui e em blocos de anotações Olá vinculado é genérico e deve funcionar em qualquer cluster do Spark.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-136">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="7c3eb-137">Se você não estiver usando o HDInsight Spark, as etapas de configuração e gerenciamento de cluster Olá podem ser ligeiramente diferentes da que é mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-137">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="7c3eb-138">Para sua conveniência, aqui estão os links de saudação blocos de anotações do Jupyter toohello para Spark 1.6 (toobe executar no kernel do pySpark de saudação do servidor de Jupyter Notebook de saudação) e o Spark 2.0 (toobe executar no kernel do pySpark3 de saudação do servidor de Jupyter Notebook de saudação):</span><span class="sxs-lookup"><span data-stu-id="7c3eb-138">For convenience, here are hello links toohello Jupyter notebooks for Spark 1.6 (toobe run in hello pySpark kernel of hello Jupyter Notebook server) and  Spark 2.0 (toobe run in hello pySpark3 kernel of hello Jupyter Notebook server):</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="7c3eb-139">Blocos de notas Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="7c3eb-139">Spark 1.6 notebooks</span></span>

<span data-ttu-id="7c3eb-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): fornece informações sobre como tooperform de exploração de dados, modelagem e pontuação com vários algoritmos diferentes.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): Provides information on how tooperform data exploration, modeling, and scoring with several different algorithms.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="7c3eb-141">Blocos de notas Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="7c3eb-141">Spark 2.0 notebooks</span></span>
<span data-ttu-id="7c3eb-142">tarefas de classificação e regressão de saudação que são implementadas usando um cluster Spark 2.0 são blocos de anotações separado e bloco de anotações de classificação Olá usa um conjunto de dados diferente:</span><span class="sxs-lookup"><span data-stu-id="7c3eb-142">hello regression and classification tasks that are implemented using a Spark 2.0 cluster are in separate notebooks and hello classification notebook uses a different data set:</span></span>

- <span data-ttu-id="7c3eb-143">[Spark2.0-pySpark3-Machine-Learning-data-Science-Spark-Advanced-data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): este arquivo fornece informações sobre como tooperform a exploração de dados, modelagem e pontuação no Spark 2.0 clusters usando Olá trip NYC táxi e passagens-conjunto de dados descrito [aqui](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="7c3eb-143">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how tooperform data exploration, modeling, and scoring in Spark 2.0 clusters using hello NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span> <span data-ttu-id="7c3eb-144">Este bloco de anotações pode ser um bom ponto de partida para explorar rapidamente código Olá que fornecemos para Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-144">This notebook may be a good starting point for quickly exploring hello code we have provided for Spark 2.0.</span></span> <span data-ttu-id="7c3eb-145">Para um bloco de anotações mais detalhado analisa Olá dados NYC táxi, consulte o próximo bloco de anotações de saudação nesta lista.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-145">For a more detailed notebook analyzes hello NYC Taxi data, see hello next notebook in this list.</span></span> <span data-ttu-id="7c3eb-146">Consulte as notas de saudação seguinte lista que comparam esses blocos de anotações.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-146">See hello notes following this list that compare these notebooks.</span></span> 
- <span data-ttu-id="7c3eb-147">[Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): esse arquivo mostra como tooperform dados disputa (operações Spark SQL e dataframe), a exploração, modelagem e pontuação usando Olá trip NYC táxi e passagens conjunto de dados descrito [ aqui](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="7c3eb-147">[Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): This file shows how tooperform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using hello NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span>
- <span data-ttu-id="7c3eb-148">[Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): esse arquivo mostra como tooperform dados disputa (operações Spark SQL e dataframe), a exploração, modelagem e pontuação usando Olá conhecida saída em tempo de aérea conjunto de dados de 2011 e 2012.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-148">[Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): This file shows how tooperform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using hello well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="7c3eb-149">Podemos integrada Olá aérea dataset com hello a toomodeling de anteriores de dados (por exemplo, windspeed, temperatura, altitude etc.) do aeroporto clima, para que esses recursos de tempo podem ser incluídos no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-149">We integrated hello airline dataset with hello airport weather data (e.g. windspeed, temperature, altitude etc.) prior toomodeling, so these weather features can be included in hello model.</span></span>

<!-- -->

> [!NOTE]
> <span data-ttu-id="7c3eb-150">Olá aérea dataset foi adicionado toohello 2.0 Spark notebooks toobetter ilustram o uso de saudação de algoritmos de classificação.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-150">hello airline dataset was added toohello Spark 2.0 notebooks toobetter illustrate hello use of classification algorithms.</span></span> <span data-ttu-id="7c3eb-151">Consulte Olá links para obter informações sobre o conjunto de dados de saída em tempo de passagens áreas e conjunto de dados de tempo a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c3eb-151">See hello following links for information about airline on-time departure dataset and weather dataset:</span></span>

>- <span data-ttu-id="7c3eb-152">Dados de partidas no horário em aeroportos: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span><span class="sxs-lookup"><span data-stu-id="7c3eb-152">Airline on-time departure data: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span></span>

>- <span data-ttu-id="7c3eb-153">Dados de clima aeroporto: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span><span class="sxs-lookup"><span data-stu-id="7c3eb-153">Airport weather data: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span></span> 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
<span data-ttu-id="7c3eb-154">Olá Spark 2.0 blocos de anotações Olá táxi NYC e conjuntos de dados de atraso de voo de aérea podem levar 10 minutos ou mais toorun (dependendo do tamanho de saudação do cluster HDI).</span><span class="sxs-lookup"><span data-stu-id="7c3eb-154">hello Spark 2.0 notebooks on hello NYC taxi and airline flight delay data-sets can take 10 mins or more toorun (depending on hello size of your HDI cluster).</span></span> <span data-ttu-id="7c3eb-155">primeiro notebook no hello acima da lista Hello mostra muitos aspectos de exploração de dados hello, visualização e ML do modelo de treinamento em um bloco de anotações que utiliza menos toorun de tempo com convertidos NYC conjunto de dados, no qual Olá táxi e passagens arquivos tem sido previamente Unidos: [ Spark2.0-pySpark3-Machine-Learning-data-Science-Spark-Advanced-data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) este bloco de anotações leva uma quantidade menor tempo toofinish (2-3 minutos) e pode ser um bom ponto de partida para explorar rapidamente código Olá temos fornecido para Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-155">hello first notebook in hello above list shows many aspects of hello data exploration, visualization and ML model training in a notebook that takes less time toorun with down-sampled NYC data set, in which hello taxi and fare files have been pre-joined: [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) This notebook takes a much shorter time toofinish (2-3 mins) and may be a good starting point for quickly exploring hello code we have provided for Spark 2.0.</span></span> 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
<span data-ttu-id="7c3eb-156">descrições de saudação abaixo são relacionada toousing Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-156">hello descriptions below are related toousing Spark 1.6.</span></span> <span data-ttu-id="7c3eb-157">Para versões do Spark 2.0, use anotações Olá descritos e no link acima.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-157">For Spark 2.0 versions, please use hello notebooks described and linked above.</span></span> 

<!-- -->

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="7c3eb-158">Programa de instalação: Olá, bibliotecas e locais de armazenamento predefinição contexto Spark</span><span class="sxs-lookup"><span data-stu-id="7c3eb-158">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="7c3eb-159">Spark é capaz de tooAzure tooread e gravar o Blob de armazenamento (também conhecido como WASB).</span><span class="sxs-lookup"><span data-stu-id="7c3eb-159">Spark is able tooread and write tooAzure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="7c3eb-160">Para qualquer um dos seus dados existentes armazenados podem ser processadas usando Spark e Olá resultados armazenados em WASB.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-160">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="7c3eb-161">toosave modelos ou os arquivos em WASB, o caminho Olá precisa toobe especificado corretamente.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-161">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="7c3eb-162">Olá padrão contêiner anexado toohello Spark cluster pode ser referenciado usando um caminho começando com: "wasb: / / /".</span><span class="sxs-lookup"><span data-stu-id="7c3eb-162">hello default container attached toohello Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="7c3eb-163">Outros locais são referenciados por "wasb://".</span><span class="sxs-lookup"><span data-stu-id="7c3eb-163">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="7c3eb-164">Definir caminhos de diretório para locais de armazenamento no WASB</span><span class="sxs-lookup"><span data-stu-id="7c3eb-164">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="7c3eb-165">Olá, exemplo de código a seguir especifica o local de saudação de Olá toobe de dados de leitura e Olá caminho para a saída do modelo Olá modelo armazenamento diretório toowhich Olá é salvo:</span><span class="sxs-lookup"><span data-stu-id="7c3eb-165">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved:</span></span>

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a><span data-ttu-id="7c3eb-166">Importar bibliotecas</span><span class="sxs-lookup"><span data-stu-id="7c3eb-166">Import libraries</span></span>
<span data-ttu-id="7c3eb-167">A instalação também requer a importação das bibliotecas necessárias.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-167">Set up also requires importing necessary libraries.</span></span> <span data-ttu-id="7c3eb-168">Definir contexto spark e importar bibliotecas necessárias com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c3eb-168">Set spark context and import necessary libraries with hello following code:</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="7c3eb-169">Contexto predefinido do Spark e palavras mágicas do PySpark</span><span class="sxs-lookup"><span data-stu-id="7c3eb-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="7c3eb-170">kernels PySpark de saudação que são fornecidos com blocos de anotações do Jupyter tem um contexto de predefinição.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-170">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="7c3eb-171">Portanto não é necessário tooset Olá Spark ou Hive contextos explicitamente antes de começar a trabalhar com o aplicativo hello que você está desenvolvendo.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-171">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="7c3eb-172">Esses contextos estão disponíveis para você por padrão.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-172">These contexts are available for you by default.</span></span> <span data-ttu-id="7c3eb-173">Esses contextos são:</span><span class="sxs-lookup"><span data-stu-id="7c3eb-173">These contexts are:</span></span>

* <span data-ttu-id="7c3eb-174">sc - para o Spark</span><span class="sxs-lookup"><span data-stu-id="7c3eb-174">sc - for Spark</span></span> 
* <span data-ttu-id="7c3eb-175">sqlContext - para o Hive</span><span class="sxs-lookup"><span data-stu-id="7c3eb-175">sqlContext - for Hive</span></span>

<span data-ttu-id="7c3eb-176">Olá PySpark kernel fornece algumas predefinidas "magics", que são comandos especiais que podem ser chamados com % %.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-176">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="7c3eb-177">Há dois comandos que são usados nesses exemplos de código.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="7c3eb-178">**% % local** Especifica que o código de saudação em linhas subsequentes é toobe executado localmente.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-178">**%%local** Specifies that hello code in subsequent lines is toobe executed locally.</span></span> <span data-ttu-id="7c3eb-179">O código deve ser um código Python válido.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="7c3eb-180">**% % -o do sql <variable name>**  executa uma consulta de Hive em Olá sqlContext.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-180">**%%sql -o <variable name>** Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="7c3eb-181">Se Olá -o parâmetro for passado, resultado de saudação de consulta de saudação é mantido no Olá % % contexto Python local como um DataFrame Pandas.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-181">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="7c3eb-182">Para obter mais informações sobre kernels Olá para blocos de anotações do Jupyter e hello predefinidas "magics" que eles fornecem, consulte [clusters Kernels disponíveis para blocos de anotações do Jupyter com Linux do HDInsight Spark no HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="7c3eb-182">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="7c3eb-183">Ingestão de dados de blob público</span><span class="sxs-lookup"><span data-stu-id="7c3eb-183">Data ingestion from public blob</span></span>
<span data-ttu-id="7c3eb-184">Olá primeira etapa no processo de ciência de dados Olá é tooingest Olá dados toobe analisado de fontes de onde é reside em seu ambiente de modelagem e exploração de dados.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-184">hello first step in hello data science process is tooingest hello data toobe analyzed from sources where is resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="7c3eb-185">ambiente de saudação é Spark neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-185">hello environment is Spark in this walkthrough.</span></span> <span data-ttu-id="7c3eb-186">Esta seção contém Olá código toocomplete uma série de tarefas:</span><span class="sxs-lookup"><span data-stu-id="7c3eb-186">This section contains hello code toocomplete a series of tasks:</span></span>

* <span data-ttu-id="7c3eb-187">Olá toobe de exemplo de dados modelado de ingestão</span><span class="sxs-lookup"><span data-stu-id="7c3eb-187">ingest hello data sample toobe modeled</span></span>
* <span data-ttu-id="7c3eb-188">ler no conjunto de dados entrada hello (armazenado como um arquivo. tsv)</span><span class="sxs-lookup"><span data-stu-id="7c3eb-188">read in hello input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="7c3eb-189">formato e dados saudação normal</span><span class="sxs-lookup"><span data-stu-id="7c3eb-189">format and clean hello data</span></span>
* <span data-ttu-id="7c3eb-190">criar e armazenar objetos em cache (RDDs ou quadros de dados) na memória</span><span class="sxs-lookup"><span data-stu-id="7c3eb-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="7c3eb-191">registrá-lo como uma tabela temporária no contexto do SQL.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="7c3eb-192">Este é o código de saudação para ingestão de dados.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-192">Here is hello code for data ingestion.</span></span>

    # INGEST DATA

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


    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="7c3eb-193">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-193">**OUTPUT:**</span></span>

<span data-ttu-id="7c3eb-194">Tempo gasto tooexecute acima célula: 51.72 segundos</span><span class="sxs-lookup"><span data-stu-id="7c3eb-194">Time taken tooexecute above cell: 51.72 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="7c3eb-195">Visualização e exploração de dados</span><span class="sxs-lookup"><span data-stu-id="7c3eb-195">Data exploration & visualization</span></span>
<span data-ttu-id="7c3eb-196">Quando dados saudação foi colocados no Spark, hello próxima etapa no processo de ciência de dados Olá é toogain de compreensão mais profunda dos dados Olá por meio de exploração e visualização.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-196">Once hello data has been brought into Spark, hello next step in hello data science process is toogain deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="7c3eb-197">Nesta seção, podemos examinar dados de táxi hello usando consultas SQL e recursos em potencial e variáveis de destino de saudação de plotagem para inspeção visual.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-197">In this section, we examine hello taxi data using SQL queries and plot hello target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="7c3eb-198">Especificamente, podemos plotar frequência Olá passageiro de contagens de em viagens táxi, a frequência de saudação de quantidades de ponta e como dicas variam de acordo com o tipo e a quantidade de pagamento.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-198">Specifically, we plot hello frequency of passenger counts in taxi trips, hello frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a><span data-ttu-id="7c3eb-199">Plotar um histograma de frequências de contagem de passageiro no exemplo hello de viagens táxi</span><span class="sxs-lookup"><span data-stu-id="7c3eb-199">Plot a histogram of passenger count frequencies in hello sample of taxi trips</span></span>
<span data-ttu-id="7c3eb-200">Esse código e trechos de código subsequentes usam exemplo do SQL tooquery magic hello e os dados de saudação do tooplot magic local.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-200">This code and subsequent snippets use SQL magic tooquery hello sample and local magic tooplot hello data.</span></span>

* <span data-ttu-id="7c3eb-201">**Magic SQL (`%%sql`)** hello HDInsight PySpark kernel dá suporte a fácil embutido HiveQL consultas em relação a saudação sqlContext.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-201">**SQL magic (`%%sql`)** hello HDInsight PySpark kernel supports easy inline HiveQL queries against hello sqlContext.</span></span> <span data-ttu-id="7c3eb-202">saudação (-o VARIABLE_NAME) argumento persiste saída Olá de consulta do SQL hello como um DataFrame Pandas no servidor do Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-202">hello (-o VARIABLE_NAME) argument persists hello output of hello SQL query as a Pandas DataFrame on hello Jupyter server.</span></span> <span data-ttu-id="7c3eb-203">Isso significa que ele está disponível no modo local hello.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-203">This means it is available in hello local mode.</span></span>
* <span data-ttu-id="7c3eb-204">Olá  **`%%local` mágico** é usado toorun código localmente no servidor de Jupyter hello, que é Olá um nó principal do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-204">hello **`%%local` magic** is used toorun code locally on hello Jupyter server, which is hello headnode of hello HDInsight cluster.</span></span> <span data-ttu-id="7c3eb-205">Normalmente, você usa `%%local` magic em conjunto com hello `%%sql` magic com o parâmetro -o.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-205">Typically, you use `%%local` magic in conjunction with hello `%%sql` magic with -o parameter.</span></span> <span data-ttu-id="7c3eb-206">parâmetro -o de Hello persistir Olá saída de hello SQL consulta localmente e, em seguida, % % magic local irá disparar o próximo conjunto de saudação do toorun de trecho de código localmente contra a saída da saudação de consultas SQL Olá persistido localmente</span><span class="sxs-lookup"><span data-stu-id="7c3eb-206">hello -o parameter would persist hello output of hello SQL query locally and then %%local magic would trigger hello next set of code snippet toorun locally against hello output of hello SQL queries that is persisted locally</span></span>

<span data-ttu-id="7c3eb-207">saída de Hello é visualizada automaticamente depois de executar código hello.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-207">hello output is automatically visualized after you run hello code.</span></span>

<span data-ttu-id="7c3eb-208">Essa consulta recupera viagens Olá por contagem de passageiro.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-208">This query retrieves hello trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

<span data-ttu-id="7c3eb-209">Esse código cria um quadro de dados local de saída da consulta hello e plota dados saudação.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-209">This code creates a local data-frame from hello query output and plots hello data.</span></span> <span data-ttu-id="7c3eb-210">Olá `%%local` mágico cria um local-quadro de dados, `sqlResults`, que pode ser usado para plotar com matplotlib.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-210">hello `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="7c3eb-211">Essas palavras mágicas do PySpark são usadas várias vezes neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-211">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="7c3eb-212">Se a quantidade de saudação de dados for grande, você deve exemplo toocreate um quadro de dados que pode caber na memória local.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-212">If hello amount of data is large, you should sample toocreate a data-frame that can fit in local memory.</span></span>
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="7c3eb-213">Aqui está viagens de Olá Olá código tooplot por passageiro contagens</span><span class="sxs-lookup"><span data-stu-id="7c3eb-213">Here is hello code tooplot hello trips by passenger counts</span></span>

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

<span data-ttu-id="7c3eb-214">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-214">**OUTPUT:**</span></span>

![Frequência de corridas por contagem de passageiros](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

<span data-ttu-id="7c3eb-216">Você pode selecionar entre vários tipos diferentes de visualizações (tabela, pizza, linha, área ou barra) usando Olá **tipo** botões de menu no bloco de anotações de saudação.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-216">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using hello **Type** menu buttons in hello notebook.</span></span> <span data-ttu-id="7c3eb-217">gráfico de barras Olá é mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-217">hello Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="7c3eb-218">Plote um histograma de valores de gorjetas e como o valor das gorjetas varia pelas tarifas e contagens de passageiros.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-218">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="7c3eb-219">Use um banco de dados consulta toosample do SQL.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-219">Use a SQL query toosample data.</span></span>

    #PLOT HISTOGRAM OF TIP AMOUNTS AND VARIATION BY PASSENGER COUNT AND PAYMENT TYPE

    # HIVEQL QUERY AGAINST hello sqlContext
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


<span data-ttu-id="7c3eb-220">Esta célula código usa Olá consulta toocreate três gráficos Olá de dados do SQL.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-220">This code cell uses hello SQL query toocreate three plots hello data.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
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


<span data-ttu-id="7c3eb-221">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-221">**OUTPUT:**</span></span> 

![Distribuição de valores de gorjetas](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![Valor de gorjeta por contagem de passageiros](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Valor de gorjeta por valor de tarifa](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="7c3eb-225">Engenharia de recursos, transformação e preparação de dados para a modelagem</span><span class="sxs-lookup"><span data-stu-id="7c3eb-225">Feature engineering, transformation and data preparation for modeling</span></span>
<span data-ttu-id="7c3eb-226">Esta seção descreve e fornece código Olá para procedimentos usados tooprepare dados para uso em modelagem ML.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-226">This section describes and provides hello code for procedures used tooprepare data for use in ML modeling.</span></span> <span data-ttu-id="7c3eb-227">Ele mostra como as tarefas de saudação toodo a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c3eb-227">It shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="7c3eb-228">Criar um novo recurso reunindo horários em blocos de tempo de tráfego</span><span class="sxs-lookup"><span data-stu-id="7c3eb-228">Create a new feature by binning hours into traffic time buckets</span></span>
* <span data-ttu-id="7c3eb-229">Indexar e codificar recursos categóricos</span><span class="sxs-lookup"><span data-stu-id="7c3eb-229">Index and encode categorical features</span></span>
* <span data-ttu-id="7c3eb-230">Criar objetos de ponto rotulado para entrada em funções de ML</span><span class="sxs-lookup"><span data-stu-id="7c3eb-230">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="7c3eb-231">Cria uma amostragem aleatória de subgrupos de dados hello e dividi-lo em treinamento e conjuntos de teste</span><span class="sxs-lookup"><span data-stu-id="7c3eb-231">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
* <span data-ttu-id="7c3eb-232">Dimensionamento de recursos</span><span class="sxs-lookup"><span data-stu-id="7c3eb-232">Feature scaling</span></span>
* <span data-ttu-id="7c3eb-233">Armazenar objetos em cache na memória</span><span class="sxs-lookup"><span data-stu-id="7c3eb-233">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="7c3eb-234">Criar um novo recurso reunindo horários em blocos de tempo de tráfego</span><span class="sxs-lookup"><span data-stu-id="7c3eb-234">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="7c3eb-235">Esse código mostra como toocreate um novo recurso guardando horas em vez de tráfego buckets e, em seguida, como toocache Olá resultante quadro de dados na memória.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-235">This code shows how toocreate a new feature by binning hours into traffic time buckets and then how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="7c3eb-236">Onde resiliente distribuídas conjuntos de dados (RDDs) e quadros de dados são usados repetidamente, cache leva tooimproved tempos de execução.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-236">Where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly, caching leads tooimproved execution times.</span></span> <span data-ttu-id="7c3eb-237">Da mesma forma, cache RDDs e quadros de dados em vários estágios Olá passo a passo.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-237">Accordingly, we cache RDDs and data-frames at several stages in hello walkthrough.</span></span> 

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

<span data-ttu-id="7c3eb-238">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-238">**OUTPUT:**</span></span> 

<span data-ttu-id="7c3eb-239">126050</span><span class="sxs-lookup"><span data-stu-id="7c3eb-239">126050</span></span>

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a><span data-ttu-id="7c3eb-240">Indexar e codificar recursos categóricos para entrada em funções de modelagem</span><span class="sxs-lookup"><span data-stu-id="7c3eb-240">Index and encode categorical features for input into modeling functions</span></span>
<span data-ttu-id="7c3eb-241">Esta seção mostra como tooindex ou codificar recursos categóricos para entrada em Olá funções da modelagem.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-241">This section shows how tooindex or encode categorical features for input into hello modeling functions.</span></span> <span data-ttu-id="7c3eb-242">Olá modelagem e prever a funções de MLlib exigem recursos com entrada de dados categóricos toobe indexado ou codificado toouse anterior.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-242">hello modeling and predict functions of MLlib require features with categorical input data toobe indexed or encoded prior toouse.</span></span> <span data-ttu-id="7c3eb-243">Dependendo do modelo de hello, você precisa tooindex ou codificá-los de maneiras diferentes:</span><span class="sxs-lookup"><span data-stu-id="7c3eb-243">Depending on hello model, you need tooindex or encode them in different ways:</span></span>  

* <span data-ttu-id="7c3eb-244">**Baseado na árvore de modelagem** requer toobe categorias codificada como valores numéricos (por exemplo, um recurso com três categorias pode ser codificado com 0, 1, 2).</span><span class="sxs-lookup"><span data-stu-id="7c3eb-244">**Tree-based modeling** requires categories toobe encoded as numerical values (for example, a feature with three categories may be encoded with 0, 1, 2).</span></span> <span data-ttu-id="7c3eb-245">Isso é fornecido pela função [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) do MLlib.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-245">This is provided by MLlib’s [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) function.</span></span> <span data-ttu-id="7c3eb-246">Essa função codifica uma coluna de cadeia de caracteres da coluna de tooa de rótulos de índices de rótulo que são ordenados por frequências de rótulo.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-246">This function encodes a string column of labels tooa column of label indices that are ordered by label frequencies.</span></span> <span data-ttu-id="7c3eb-247">Embora indexado com valores numéricos para entrada e manipulação de dados, os algoritmos com base em árvore Olá podem ser tootreat especificado-los adequadamente como categorias.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-247">Although indexed with numerical values for input and data handling, hello tree-based algorithms can be specified tootreat them appropriately as categories.</span></span> 
* <span data-ttu-id="7c3eb-248">**Modelos de regressão Linear e logística** exigem hot uma codificação, onde, por exemplo, um recurso com três categorias pode ser expandido em três colunas de recurso, com cada contendo 0 ou 1 dependendo da categoria de saudação de uma observação.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-248">**Logistic and Linear Regression models** require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="7c3eb-249">Fornece MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) toodo hot uma codificação de função.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-249">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function toodo one-hot encoding.</span></span> <span data-ttu-id="7c3eb-250">Este codificador mapeia uma coluna da coluna de tooa de índices de rótulo de vetores de binários, no máximo um único um valor.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-250">This encoder maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="7c3eb-251">Essa codificação permite que os algoritmos que esperam recursos com valores numéricos, como a regressão logística, recursos de toocategorical toobe aplicado.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-251">This encoding allows algorithms that expect numerical valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

<span data-ttu-id="7c3eb-252">Aqui está o hello tooindex de código e codificar recursos categóricos:</span><span class="sxs-lookup"><span data-stu-id="7c3eb-252">Here is hello code tooindex and encode categorical features:</span></span>

    # INDEX AND ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES    
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

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

<span data-ttu-id="7c3eb-253">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-253">**OUTPUT:**</span></span>

<span data-ttu-id="7c3eb-254">Tempo gasto tooexecute acima célula: 1.28 segundos</span><span class="sxs-lookup"><span data-stu-id="7c3eb-254">Time taken tooexecute above cell: 1.28 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="7c3eb-255">Criar objetos de ponto rotulado para entrada em funções de ML</span><span class="sxs-lookup"><span data-stu-id="7c3eb-255">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="7c3eb-256">Esta seção contém o código que mostra como tipo de dados de texto categóricos tooindex como um rótulo de ponto de dados e codificação-lo para que ele possa ser usado tootrain e teste MLlib Regressão logística e outros modelos de classificação.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-256">This section contains code that shows how tooindex categorical text data as a labeled point data type and encode it so that it can be used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="7c3eb-257">Objetos de ponto rotulados são RDDs (Conjuntos de Dados Resilientes Distribuídos) formatados de uma maneira que é necessária como dados de entrada pela maioria dos algoritmos de ML no MLlib.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-257">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="7c3eb-258">Um [ponto rotulado](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) é um vetor local, denso ou esparso, associado a um rótulo/resposta.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-258">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>  

<span data-ttu-id="7c3eb-259">Esta seção contém o código que mostra como dados de texto categóricos tooindex como um [rotulada ponto](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) tipo de dados e codificá-lo para que ele possa ser usado tootrain e teste MLlib Regressão logística e outros modelos de classificação.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-259">This section contains code that shows how tooindex categorical text data as a [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) data type and encode it so that it can be used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="7c3eb-260">Objetos de ponto de rotulado são RDDs (Conjuntos de Dados Resilientes Distribuídos) que consistem em um rótulo (variável de destino/resposta) e um vetor de recurso.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-260">Labeled point objects are Resilient Distributed Datasets (RDD) consisting of a label (target/response variable) and feature vector.</span></span> <span data-ttu-id="7c3eb-261">Esse formato é necessário como entrada para muitos algoritmos de ML no MLlib.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-261">This format is needed as input by many ML algorithms in MLlib.</span></span>

<span data-ttu-id="7c3eb-262">Aqui está o hello tooindex de código e codificar os recursos de texto para classificação binária.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-262">Here is hello code tooindex and encode text features for binary classification.</span></span>

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


<span data-ttu-id="7c3eb-263">Aqui está o código de saudação tooencode e o índice de recursos categóricos texto para análise de regressão linear.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-263">Here is hello code tooencode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="7c3eb-264">Cria uma amostragem aleatória de subgrupos de dados hello e dividi-lo em treinamento e conjuntos de teste</span><span class="sxs-lookup"><span data-stu-id="7c3eb-264">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
<span data-ttu-id="7c3eb-265">Esse código cria uma amostragem aleatória de dados de saudação (25% é usado aqui).</span><span class="sxs-lookup"><span data-stu-id="7c3eb-265">This code creates a random sampling of hello data (25% is used here).</span></span> <span data-ttu-id="7c3eb-266">Embora não seja necessário para este exemplo devido toohello tamanho do conjunto de dados hello, demonstraremos como você pode criar amostra aqui para saber como toouse-lo para o seu próprio problema quando necessário.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-266">Although it is not required for this example due toohello size of hello dataset, we demonstrate how you can sample here so you know how toouse it for your own problem when needed.</span></span> <span data-ttu-id="7c3eb-267">Quando as amostras são grandes, isso pode economizar um tempo significativo durante o treinamento de modelos.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-267">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="7c3eb-268">Em seguida, dividiremos exemplo hello em uma parte de treinamento (75% aqui) e um teste toouse de parte (25% aqui) de classificação e modelagem de regressão.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-268">Next we split hello sample into a training part (75% here) and a testing part (25% here) toouse in classification and regression modeling.</span></span>

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="7c3eb-269">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-269">**OUTPUT:**</span></span>

<span data-ttu-id="7c3eb-270">Tempo gasto tooexecute acima célula: 0.24 segundos</span><span class="sxs-lookup"><span data-stu-id="7c3eb-270">Time taken tooexecute above cell: 0.24 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="7c3eb-271">Dimensionamento de recursos</span><span class="sxs-lookup"><span data-stu-id="7c3eb-271">Feature scaling</span></span>
<span data-ttu-id="7c3eb-272">Dimensionamento de recurso, também conhecido como normalização de dados assegura que os recursos com valores amplamente distribuídos são não fornecido excessiva pesar na função objetivo hello.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-272">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> <span data-ttu-id="7c3eb-273">código para o recurso de dimensionamento Hello usa Olá [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) variação de toounit tooscale Olá recursos.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-273">hello code for feature scaling uses hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello features toounit variance.</span></span> <span data-ttu-id="7c3eb-274">Ele é fornecido por MLlib para uso na regressão linear com SGD (Stochastic Gradient Descent), um algoritmo popular de treinamento de uma grande variedade de outros modelos de aprendizado de máquina, como regressões regularizadas ou SVM (máquinas de vetor de suporte).</span><span class="sxs-lookup"><span data-stu-id="7c3eb-274">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>

> [!NOTE]
> <span data-ttu-id="7c3eb-275">Encontramos Olá LinearRegressionWithSGD algoritmo toobe toofeature confidencial dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-275">We have found hello LinearRegressionWithSGD algorithm toobe sensitive toofeature scaling.</span></span>
> 
> 

<span data-ttu-id="7c3eb-276">Aqui está a variáveis de tooscale Olá código para uso com o algoritmo SGD linear Olá regularizada.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-276">Here is hello code tooscale variables for use with hello regularized linear SGD algorithm.</span></span>

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="7c3eb-277">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-277">**OUTPUT:**</span></span>

<span data-ttu-id="7c3eb-278">Tempo gasto tooexecute acima célula: 13.17 segundos</span><span class="sxs-lookup"><span data-stu-id="7c3eb-278">Time taken tooexecute above cell: 13.17 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="7c3eb-279">Armazenar objetos em cache na memória</span><span class="sxs-lookup"><span data-stu-id="7c3eb-279">Cache objects in memory</span></span>
<span data-ttu-id="7c3eb-280">tempo Olá para treinamento e teste de algoritmos ML podem ser reduzidos pelo cache de objetos de quadro de dados de entrada hello usados para classificação, regressão, e recursos de escala.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-280">hello time taken for training and testing of ML algorithms can be reduced by caching hello input data frame objects used for classification, regression, and scaled features.</span></span>

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

<span data-ttu-id="7c3eb-281">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-281">**OUTPUT:**</span></span> 

<span data-ttu-id="7c3eb-282">Tempo gasto tooexecute acima célula: 0,15 segundos</span><span class="sxs-lookup"><span data-stu-id="7c3eb-282">Time taken tooexecute above cell: 0.15 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="7c3eb-283">Prever se uma gorjeta é paga ou não com modelos de classificação binária</span><span class="sxs-lookup"><span data-stu-id="7c3eb-283">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="7c3eb-284">Esta seção mostra como usar três modelos para tarefa de classificação binária Olá de prever se uma dica é pago por uma viagem táxi ou não.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-284">This section shows how use three models for hello binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="7c3eb-285">modelos de saudação apresentados são:</span><span class="sxs-lookup"><span data-stu-id="7c3eb-285">hello models presented are:</span></span>

* <span data-ttu-id="7c3eb-286">Regressão logística regularizada</span><span class="sxs-lookup"><span data-stu-id="7c3eb-286">Regularized logistic regression</span></span> 
* <span data-ttu-id="7c3eb-287">Modelo de floresta aleatória</span><span class="sxs-lookup"><span data-stu-id="7c3eb-287">Random forest model</span></span>
* <span data-ttu-id="7c3eb-288">Árvores de Ampliação de Gradiente</span><span class="sxs-lookup"><span data-stu-id="7c3eb-288">Gradient Boosting Trees</span></span>

<span data-ttu-id="7c3eb-289">Cada seção de código de compilação de modelo é dividida em etapas:</span><span class="sxs-lookup"><span data-stu-id="7c3eb-289">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="7c3eb-290">**Modelar os dados de treinamento** com um conjunto de parâmetros</span><span class="sxs-lookup"><span data-stu-id="7c3eb-290">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="7c3eb-291">**Modelar a avaliação** em um conjunto de dados de teste com métricas</span><span class="sxs-lookup"><span data-stu-id="7c3eb-291">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="7c3eb-292">**Salvar modelo** no blob para consumo futuro</span><span class="sxs-lookup"><span data-stu-id="7c3eb-292">**Saving model** in blob for future consumption</span></span>

### <a name="classification-using-logistic-regression"></a><span data-ttu-id="7c3eb-293">Classificação usando regressão logística</span><span class="sxs-lookup"><span data-stu-id="7c3eb-293">Classification using logistic regression</span></span>
<span data-ttu-id="7c3eb-294">código de saudação nesta seção mostra como tootrain, avaliar e salvar um modelo de regressão logística com [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) que prevê se ou não uma dica é pago por uma viagem Olá NYC táxi o conjunto de dados de processamento e passagens.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-294">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

<span data-ttu-id="7c3eb-295">**Treinar o modelo de regressão logística hello usando VC e limpeza de hyperparameter**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-295">**Train hello logistic regression model using CV and hyperparameter sweeping**</span></span>

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

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitModel.weights))
    print("Intercept: " + str(logitModel.intercept))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="7c3eb-296">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-296">**OUTPUT:**</span></span> 

<span data-ttu-id="7c3eb-297">Coeficientes: [0,0082065285375, -0,0223675576104, -0,0183812028036, -3,48124578069e-05, -0,00247646947233, -0,00165897881503, 0,0675394837328, -0,111823113101, -0,324609912762, -0,204549780032, -1,36499216354, 0,591088507921, -0,664263411392, -1,00439726852, 3,46567827545, -3,51025855172, -0,0471341112232, -0,043521833294, 0,000243375810385, 0,054518719222]</span><span class="sxs-lookup"><span data-stu-id="7c3eb-297">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="7c3eb-298">Interceptação: -0,0111216486893</span><span class="sxs-lookup"><span data-stu-id="7c3eb-298">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="7c3eb-299">Tempo gasto tooexecute acima célula: 14.43 segundos</span><span class="sxs-lookup"><span data-stu-id="7c3eb-299">Time taken tooexecute above cell: 14.43 seconds</span></span>

<span data-ttu-id="7c3eb-300">**Avaliar o modelo de classificação binária Olá com métricas padrão**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-300">**Evaluate hello binary classification model with standard metrics**</span></span>

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="7c3eb-301">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-301">**OUTPUT:**</span></span> 

<span data-ttu-id="7c3eb-302">Área sob PR = 0,985297691373</span><span class="sxs-lookup"><span data-stu-id="7c3eb-302">Area under PR = 0.985297691373</span></span>

<span data-ttu-id="7c3eb-303">Área sob ROC = 0,983714670256</span><span class="sxs-lookup"><span data-stu-id="7c3eb-303">Area under ROC = 0.983714670256</span></span>

<span data-ttu-id="7c3eb-304">Estatísticas de resumo</span><span class="sxs-lookup"><span data-stu-id="7c3eb-304">Summary Stats</span></span>

<span data-ttu-id="7c3eb-305">Precisão = 0,984304060189</span><span class="sxs-lookup"><span data-stu-id="7c3eb-305">Precision = 0.984304060189</span></span>

<span data-ttu-id="7c3eb-306">Recuperação = 0,984304060189</span><span class="sxs-lookup"><span data-stu-id="7c3eb-306">Recall = 0.984304060189</span></span>

<span data-ttu-id="7c3eb-307">Pontuação F1 = 0,984304060189</span><span class="sxs-lookup"><span data-stu-id="7c3eb-307">F1 Score = 0.984304060189</span></span>

<span data-ttu-id="7c3eb-308">Tempo gasto tooexecute acima célula: 57.61 segundos</span><span class="sxs-lookup"><span data-stu-id="7c3eb-308">Time taken tooexecute above cell: 57.61 seconds</span></span>

<span data-ttu-id="7c3eb-309">**Plote curva ROC hello.**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-309">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="7c3eb-310">Olá *predictionAndLabelsDF* é registrado como uma tabela, *tmp_results*, na célula de saudação anterior.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-310">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="7c3eb-311">*tmp_results* pode ser usado toodo consultas e resultados de saída em Olá sqlResults-quadro de dados para plotar.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-311">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="7c3eb-312">Aqui está o código de saudação.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-312">Here is hello code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="7c3eb-313">Aqui está o previsões de toomake código hello e Olá plotagem ROC curva.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-313">Here is hello code toomake predictions and plot hello ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="7c3eb-314">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-314">**OUTPUT:**</span></span>

![curve.png de ROC de regressão logística](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="7c3eb-316">Classificação de floresta aleatória</span><span class="sxs-lookup"><span data-stu-id="7c3eb-316">Random forest classification</span></span>
<span data-ttu-id="7c3eb-317">código Olá nesta seção mostra como tootrain, avaliar e salvar um modelo de floresta aleatório que prevê se ou não uma dica é pago por uma viagem Olá NYC táxi viagem e passagens conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-317">hello code in this section shows how tootrain, evaluate, and save a random forest model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

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
    ## UN-COMMENT IF YOU WANT tooPRINT TREES
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

<span data-ttu-id="7c3eb-318">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-318">**OUTPUT:**</span></span>

<span data-ttu-id="7c3eb-319">Área sob ROC = 0,985297691373</span><span class="sxs-lookup"><span data-stu-id="7c3eb-319">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="7c3eb-320">Tempo gasto tooexecute acima célula: 31.09 segundos</span><span class="sxs-lookup"><span data-stu-id="7c3eb-320">Time taken tooexecute above cell: 31.09 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="7c3eb-321">Classificação de árvores de ampliação de gradiente</span><span class="sxs-lookup"><span data-stu-id="7c3eb-321">Gradient boosting trees classification</span></span>
<span data-ttu-id="7c3eb-322">código Olá nesta seção mostra como tootrain, avaliar e salvar um modelo de árvores de ampliação gradiente que prevê se ou não uma dica é pago por uma viagem Olá NYC táxi viagem e passagens conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-322">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

    #PREDICT WHETHER A TIP IS PAID OR NOT USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo, numIterations=5)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="7c3eb-323">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-323">**OUTPUT:**</span></span>

<span data-ttu-id="7c3eb-324">Área sob ROC = 0,985297691373</span><span class="sxs-lookup"><span data-stu-id="7c3eb-324">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="7c3eb-325">Tempo gasto tooexecute acima célula: 19.76 segundos</span><span class="sxs-lookup"><span data-stu-id="7c3eb-325">Time taken tooexecute above cell: 19.76 seconds</span></span>

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a><span data-ttu-id="7c3eb-326">Prever valores de gorjetas para corridas de táxi com modelos de regressão</span><span class="sxs-lookup"><span data-stu-id="7c3eb-326">Predict tip amounts for taxi trips with regression models</span></span>
<span data-ttu-id="7c3eb-327">Esta seção mostra como usar três modelos para tarefa de regressão de saudação de prever a quantidade de saudação de dica Olá pagada para uma viagem de táxi com base em outros recursos de dica.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-327">This section shows how use three models for hello regression task of predicting hello amount of hello tip paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="7c3eb-328">modelos de saudação apresentados são:</span><span class="sxs-lookup"><span data-stu-id="7c3eb-328">hello models presented are:</span></span>

* <span data-ttu-id="7c3eb-329">Regressão linear regularizada</span><span class="sxs-lookup"><span data-stu-id="7c3eb-329">Regularized linear regression</span></span>
* <span data-ttu-id="7c3eb-330">Floresta aleatória</span><span class="sxs-lookup"><span data-stu-id="7c3eb-330">Random forest</span></span>
* <span data-ttu-id="7c3eb-331">Árvores de Ampliação de Gradiente</span><span class="sxs-lookup"><span data-stu-id="7c3eb-331">Gradient Boosting Trees</span></span>

<span data-ttu-id="7c3eb-332">Esses modelos foram descritos na introdução de saudação.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-332">These models were described in hello introduction.</span></span> <span data-ttu-id="7c3eb-333">Cada seção de código de compilação de modelo é dividida em etapas:</span><span class="sxs-lookup"><span data-stu-id="7c3eb-333">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="7c3eb-334">**Modelar os dados de treinamento** com um conjunto de parâmetros</span><span class="sxs-lookup"><span data-stu-id="7c3eb-334">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="7c3eb-335">**Modelar a avaliação** em um conjunto de dados de teste com métricas</span><span class="sxs-lookup"><span data-stu-id="7c3eb-335">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="7c3eb-336">**Salvar modelo** no blob para consumo futuro</span><span class="sxs-lookup"><span data-stu-id="7c3eb-336">**Saving model** in blob for future consumption</span></span>

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="7c3eb-337">Regressão linear com SGD</span><span class="sxs-lookup"><span data-stu-id="7c3eb-337">Linear regression with SGD</span></span>
<span data-ttu-id="7c3eb-338">Olá código nesta seção mostra como toouse dimensionado recursos tootrain uma regressão linear usa descendente do gradiente estocástico (SGD) para a otimização, e como tooscore, avaliar e Salvar modelo Olá no armazenamento de Blob do Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="7c3eb-338">hello code in this section shows how toouse scaled features tootrain a linear regression that uses stochastic gradient descent (SGD) for optimization, and how tooscore, evaluate, and save hello model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="7c3eb-339">Em nossa experiência, pode haver problemas com convergência de saudação de LinearRegressionWithSGD modelos e parâmetros necessário toobe alterado/otimizado cuidadosamente para obter um modelo válido.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-339">In our experience, there can be issues with hello convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="7c3eb-340">O dimensionamento de variáveis ajuda significativamente com a convergência.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-340">Scaling of variables significantly helps with convergence.</span></span> 
> 
> 

    #PREDICT TIP AMOUNTS USING LINEAR REGRESSION WITH SGD

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

    # PRINT TEST METRICS
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL WITH DATE-STAMP IN hello DEFAULT BLOB FOR hello CLUSTER
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="7c3eb-341">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-341">**OUTPUT:**</span></span>

<span data-ttu-id="7c3eb-342">Coeficientes: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span><span class="sxs-lookup"><span data-stu-id="7c3eb-342">Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span></span>

<span data-ttu-id="7c3eb-343">Interceptação: 0,853872718283</span><span class="sxs-lookup"><span data-stu-id="7c3eb-343">Intercept: 0.853872718283</span></span>

<span data-ttu-id="7c3eb-344">RMSE = 1,24190115863</span><span class="sxs-lookup"><span data-stu-id="7c3eb-344">RMSE = 1.24190115863</span></span>

<span data-ttu-id="7c3eb-345">R-sqr = 0,608017146081</span><span class="sxs-lookup"><span data-stu-id="7c3eb-345">R-sqr = 0.608017146081</span></span>

<span data-ttu-id="7c3eb-346">Tempo gasto tooexecute acima célula: 58.42 segundos</span><span class="sxs-lookup"><span data-stu-id="7c3eb-346">Time taken tooexecute above cell: 58.42 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="7c3eb-347">Regressão de Floresta Aleatória</span><span class="sxs-lookup"><span data-stu-id="7c3eb-347">Random Forest regression</span></span>
<span data-ttu-id="7c3eb-348">código Olá nesta seção mostra como tootrain, avaliar e salvar uma regressão de floresta aleatório que prevê a quantidade de dica de saudação dados de viagem táxi NYC.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-348">hello code in this section shows how tootrain, evaluate, and save a random forest regression that predicts tip amount for hello NYC taxi trip data.</span></span>

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
    ## UN-COMMENT IF YOU WANT tooPRING TREES
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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="7c3eb-349">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-349">**OUTPUT:**</span></span>

<span data-ttu-id="7c3eb-350">RMSE = 0,891209218139</span><span class="sxs-lookup"><span data-stu-id="7c3eb-350">RMSE = 0.891209218139</span></span>

<span data-ttu-id="7c3eb-351">R-sqr = 0,759661334921</span><span class="sxs-lookup"><span data-stu-id="7c3eb-351">R-sqr = 0.759661334921</span></span>

<span data-ttu-id="7c3eb-352">Tempo gasto tooexecute acima célula: 49.21 segundos</span><span class="sxs-lookup"><span data-stu-id="7c3eb-352">Time taken tooexecute above cell: 49.21 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="7c3eb-353">Regressão de árvores de ampliação de gradiente</span><span class="sxs-lookup"><span data-stu-id="7c3eb-353">Gradient boosting trees regression</span></span>
<span data-ttu-id="7c3eb-354">código Olá nesta seção mostra como tootrain, avaliar e salvar um modelo de árvores de ampliação gradiente que prevê a quantidade de dica de saudação dados de viagem táxi NYC.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-354">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts tip amount for hello NYC taxi trip data.</span></span>

<span data-ttu-id="7c3eb-355">**Treinar e avaliar**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-355">**Train and evaluate **</span></span>

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

    # CONVER RESULTS tooDF AND REGISER TEMP TABLE
    test_predictions = sqlContext.createDataFrame(predictionAndLabels)
    test_predictions.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="7c3eb-356">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-356">**OUTPUT:**</span></span>

<span data-ttu-id="7c3eb-357">RMSE = 0,908473148639</span><span class="sxs-lookup"><span data-stu-id="7c3eb-357">RMSE = 0.908473148639</span></span>

<span data-ttu-id="7c3eb-358">R-sqr = 0,753835096681</span><span class="sxs-lookup"><span data-stu-id="7c3eb-358">R-sqr = 0.753835096681</span></span>

<span data-ttu-id="7c3eb-359">Tempo gasto tooexecute acima célula: 34.52 segundos</span><span class="sxs-lookup"><span data-stu-id="7c3eb-359">Time taken tooexecute above cell: 34.52 seconds</span></span>

<span data-ttu-id="7c3eb-360">**Plotar**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-360">**Plot**</span></span>

<span data-ttu-id="7c3eb-361">*tmp_results* é registrado como uma tabela Hive na célula anterior hello.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-361">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="7c3eb-362">Resultados da tabela de saudação são saída Olá *sqlResults* quadro de dados para plotar.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-362">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="7c3eb-363">Aqui está o código de saudação</span><span class="sxs-lookup"><span data-stu-id="7c3eb-363">Here is hello code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

<span data-ttu-id="7c3eb-364">Aqui está a dados Olá código tooplot hello usando Olá Jupyter server.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-364">Here is hello code tooplot hello data using hello Jupyter server.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="7c3eb-365">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-365">**OUTPUT:**</span></span>

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a><span data-ttu-id="7c3eb-367">Limpar objetos da memória</span><span class="sxs-lookup"><span data-stu-id="7c3eb-367">Clean up objects from memory</span></span>
<span data-ttu-id="7c3eb-368">Use `unpersist()` toodelete objetos armazenados em cache na memória.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-368">Use `unpersist()` toodelete objects cached in memory.</span></span>

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


## <a name="record-storage-locations-of-hello-models-for-consumption-and-scoring"></a><span data-ttu-id="7c3eb-369">Locais de armazenamento de registro de modelos de saudação para consumo e pontuação</span><span class="sxs-lookup"><span data-stu-id="7c3eb-369">Record storage locations of hello models for consumption and scoring</span></span>
<span data-ttu-id="7c3eb-370">tooconsume e pontuação de um conjunto de dados independente descritas Olá [pontuação e avaliar modelos de aprendizado de máquina criados Spark](machine-learning-data-science-spark-model-consumption.md) tópico, você precisa toocopy e colar esses arquivos nomes que contêm modelos de saudação salvo criados aqui em hello Anotações do Jupyter de consumo.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-370">tooconsume and score an independent dataset described in hello [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) topic, you need toocopy and paste these file names containing hello saved models created here into hello Consumption Jupyter notebook.</span></span> <span data-ttu-id="7c3eb-371">Aqui está a saudação código tooprint out toomodel arquivos Olá caminhos que você precisa existe.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-371">Here is hello code tooprint out hello paths toomodel files you need there.</span></span>

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="7c3eb-372">**SAÍDA**</span><span class="sxs-lookup"><span data-stu-id="7c3eb-372">**OUTPUT**</span></span>

<span data-ttu-id="7c3eb-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span><span class="sxs-lookup"><span data-stu-id="7c3eb-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span></span>

<span data-ttu-id="7c3eb-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span><span class="sxs-lookup"><span data-stu-id="7c3eb-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span></span>

<span data-ttu-id="7c3eb-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span><span class="sxs-lookup"><span data-stu-id="7c3eb-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span></span>

<span data-ttu-id="7c3eb-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span><span class="sxs-lookup"><span data-stu-id="7c3eb-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span></span>

<span data-ttu-id="7c3eb-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span><span class="sxs-lookup"><span data-stu-id="7c3eb-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span></span>

<span data-ttu-id="7c3eb-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span><span class="sxs-lookup"><span data-stu-id="7c3eb-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span></span>

## <a name="whats-next"></a><span data-ttu-id="7c3eb-379">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="7c3eb-379">What's next?</span></span>
<span data-ttu-id="7c3eb-380">Agora que você criou modelos de classificação e regressão com hello Spark MlLib, você está pronto toolearn como tooscore e avaliar esses modelos.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-380">Now that you have created regression and classification models with hello Spark MlLib, you are ready toolearn how tooscore and evaluate these models.</span></span> <span data-ttu-id="7c3eb-381">Olá avançados de exploração de dados e modelagem unidades notebook mais profundo em incluindo a validação cruzada, parâmetro hyper varredura e avaliação de modelo.</span><span class="sxs-lookup"><span data-stu-id="7c3eb-381">hello advanced data exploration and modeling notebook dives deeper into including cross-validation, hyper-parameter sweeping, and model evaluation.</span></span> 

<span data-ttu-id="7c3eb-382">**Consumo de modelo:** toolearn como tooscore e avaliar modelos de classificação e regressão de saudação criados neste tópico, consulte [pontuação e avaliar modelos de aprendizado de máquina criados Spark](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="7c3eb-382">**Model consumption:** toolearn how tooscore and evaluate hello classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

<span data-ttu-id="7c3eb-383">**Validação cruzada e limpeza de hiperparâmetro**: confira [Modelagem e exploração de dados avançados com o Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) para saber como os modelos podem ser treinados usando a validação cruzada e a limpeza de hiperparâmetro</span><span class="sxs-lookup"><span data-stu-id="7c3eb-383">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping</span></span>

